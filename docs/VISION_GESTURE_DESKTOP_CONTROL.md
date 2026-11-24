# M.I.L.O. — Especificación del módulo de visión, gestos y control visual

**Fecha:** 24-11-2026  
**Estado:** diseño técnico inicial; pendiente de prototipo y pruebas en Windows.

## 1. Objetivo

Cuando el usuario active explícitamente estas funciones, M.I.L.O. podrá:
- Capturar vídeo de una cámara seleccionada.
- Detectar manos y estimar puntos clave en tiempo real.
- Reconocer gestos configurables.
- Convertir gestos confirmados en eventos de interfaz.
- Capturar una ventana o pantalla seleccionada.
- Interpretar capturas y controles de accesibilidad.
- Interactuar con aplicaciones Windows mediante UI Automation y, como último recurso, coordenadas visuales.
- Mostrar qué sensor está activo y qué acción se ejecutará.

Ver la pantalla, reconocer gestos y controlar Windows son capacidades diferentes. No se debe activar cámara o captura de pantalla de forma oculta.

## 2. Arquitectura

Separar en cinco servicios:

1. **Camera Service:** enumera dispositivos, gestiona permisos, abre/cierra la cámara y entrega frames.
2. **Hand Tracking Service:** detecta manos y landmarks; nunca ejecuta acciones del PC.
3. **Gesture Interpreter:** convierte landmarks en eventos semánticos con confianza, duración y estado; filtra falsos positivos.
4. **Screen Perception Service:** captura una ventana/pantalla elegida y obtiene metadatos accesibles.
5. **Desktop Action Gateway:** única puerta de entrada para acciones en Windows; valida permisos, contexto, límites y confirmaciones.

Flujo de gestos: Camera → Hand Tracking → Gesture Interpreter → MILO Core → Adaptive Experience.

Flujo visual: Screen Capture + UI Automation Metadata → Screen Perception → MILO Core → Action Plan → Desktop Action Gateway → Windows.

La interfaz no debe llamar directamente a APIs privilegiadas.

## 3. Tecnologías candidatas

### Cámara y manos
- **OpenCV (Python):** captura desde webcam, selección de cámara, conversión de color y preprocesamiento.
- **MediaPipe Hand Landmarker:** candidato principal para detectar landmarks. Admite IMAGE, VIDEO y LIVE_STREAM; permite configurar número de manos y umbrales de detección, presencia y seguimiento.
- **Gesture Interpreter propio:** clasificador determinista inicial basado en geometría de landmarks; evaluar modelos aprendidos solo si las reglas no bastan.

La detección básica debe funcionar localmente. Enviar imágenes a modelos cloud será una opción separada, visible y consentida.

### Captura de pantalla
- **Windows.Graphics.Capture:** API nativa para capturar una pantalla o ventana elegida mediante el selector del sistema. Windows muestra un borde de notificación mientras la captura está activa.
- Empezar con capturas puntuales de una ventana autorizada; no activar captura global continua hasta medir rendimiento y definir permisos.

### Control de Windows
- **pywinauto con backend UIA:** primera opción para localizar controles por nombre, tipo, Automation ID y jerarquía.
- **Win32 backend:** alternativa para aplicaciones clásicas.
- **Coordenadas/ratón/teclado:** último recurso cuando no hay controles accesibles. Comprobar que la ventana destino sigue siendo la correcta.

Priorizar acciones semánticas como “presionar el botón Guardar” sobre coordenadas fijas.

## 4. Catálogo inicial de gestos

Empezar con cinco candidatos, no con decenas:

| Gesto | Acción inicial | Salvaguarda |
|---|---|---|
| Palma abierta sostenida | Mostrar/ocultar HUD | Mantener 700 ms y activar modo gestos |
| Puño sostenido | Pausar reconocimiento | No cerrar aplicaciones ni detener procesos |
| Índice apuntando | Mover cursor virtual | No hacer clic por sí solo |
| Pinza pulgar-índice | Seleccionar elemento enfocado | Requiere foco y confirmación en prototipo |
| Dos manos visibles sostenidas | Cambiar espacio de trabajo | Exigir estabilidad y ausencia de oclusión |

Son propuestas para probar, no asignaciones definitivas. El usuario podrá personalizar y desactivar cada gesto. No asignar gestos a acciones destructivas, compras, envíos externos o cambios de seguridad.

## 5. Robustez

- Exigir confianza mínima y estabilidad durante varios frames.
- Aplicar histéresis, cooldown y suavizado temporal.
- Detectar pérdida de mano y cancelar acciones pendientes.
- Exigir postura neutral entre gestos confundibles.
- Calibrar iluminación, distancia y zona de interacción.
- Nunca ejecutar por un solo frame.
- Ante baja confianza, oclusión o ambigüedad, no actuar.
- Incluir interruptor visible y atajo de teclado para detener el control gestual.

## 6. Permisos

Definir tres modos explícitos:

1. **Observación:** cámara/pantalla generan contexto; ninguna acción de Windows.
2. **Control asistido:** M.I.L.O. propone una acción y espera aprobación antes de hacer clic, escribir o navegar.
3. **Automatización autorizada:** lista acotada de acciones no destructivas en aplicaciones o carpetas autorizadas, con registro y límites.

Confirmar siempre acciones externas o difíciles de revertir: enviar mensajes, publicar, comprar, borrar, instalar, cambiar seguridad o ejecutar comandos privilegiados.

El modelo visual no debe generar directamente comandos arbitrarios de terminal. Debe producir una propuesta estructurada que el Action Gateway valide.

## 7. Privacidad

- Cámara y pantalla apagadas por defecto.
- Activación explícita e indicador persistente mientras capturan.
- Apagado inmediato.
- Procesamiento local por defecto.
- No almacenar vídeo ni capturas salvo solicitud expresa.
- No guardar imágenes en logs.
- Para análisis cloud, mostrar qué imagen/ventana se enviará y pedir autorización.
- No eludir indicadores ni permisos del sistema.

## 8. Rendimiento

Separar detección ligera local, capturas bajo demanda y análisis multimodal pesado solo cuando se necesite. Medir FPS, latencia de gesto, CPU, RAM y VRAM.

El hardware reportado anteriormente es Intel i5-11400H, 16 GB RAM y NVIDIA RTX 3050 (modelo exacto y VRAM por confirmar). No prometer aceleración GPU hasta medir compatibilidad y rendimiento reales.

## 9. Primer prototipo: Gesture Lab

Construir primero un prototipo aislado, sin controlar Windows:

1. Enumerar cámaras y permitir elegir una.
2. Mostrar vista previa local con indicador CÁMARA ACTIVA.
3. Detectar hasta dos manos con MediaPipe.
4. Dibujar landmarks.
5. Reconocer palma abierta y puño sostenidos.
6. Mostrar evento, confianza y FPS.
7. Incluir pausa, cierre de cámara y atajo de emergencia.
8. No mover el cursor ni ejecutar acciones de Windows.

### Criterios de aceptación
- Apertura y cierre fiables.
- Nunca activar sin consentimiento.
- Landmarks en vivo sin bloquear la interfaz.
- Reconocimiento consistente en distintas condiciones de iluminación.
- Sin eventos repetidos por gestos accidentales.
- Cancelación al desaparecer la mano o caer la confianza.
- Apagado inmediato.
- Métricas sin guardar imágenes.

## 10. Segunda fase: Screen Lab

1. Elegir ventana o pantalla mediante selector de Windows.
2. Capturar un frame bajo demanda.
3. Extraer título y controles mediante UI Automation.
4. Comparar análisis estructural UIA con análisis visual.
5. Permitir preguntas sobre la ventana elegida.
6. No ejecutar acciones todavía.

## 11. Tercera fase: Desktop Control Lab

1. Conectar pywinauto/UIA al Action Gateway.
2. Empezar con Notepad y una aplicación de prueba.
3. Abrir una aplicación de prueba y escribir en un documento temporal.
4. Mostrar acción propuesta y control objetivo antes de ejecutarla.
5. Registrar acción, aplicación, resultado y errores.
6. Aplicar lista de aplicaciones autorizadas y apagado de emergencia.
7. Añadir coordenadas visuales solo cuando UIA no exponga el control.

## 12. Dependencias candidatas

No fijar versiones hasta probar instalación en Windows:
- Python 3.11–3.13, sujeto a compatibilidad.
- opencv-python
- mediapipe
- pywinauto
- pywin32, según backend e integración.
- Pillow
- API Windows.Graphics.Capture mediante un componente Windows dedicado.
- pytest para pruebas.

Separar dependencias de visión, captura y control para que Gesture Lab funcione sin instalar el stack completo.

## 13. Riesgos

- Iluminación baja, cámara de baja calidad, oclusiones y manos fuera del encuadre reducen precisión.
- Algunas aplicaciones no exponen controles a UI Automation.
- Coordenadas fallan si cambia resolución, escala, posición o diseño.
- Captura continua y modelos visuales pueden consumir recursos.
- No toda aplicación permite captura o automatización.
- La cámara no sustituye seguimiento ocular ni implica comprender intención.
- Mantener voz, ratón y teclado como alternativas.

## 14. Fuentes técnicas

- MediaPipe Hand Landmarker: https://developers.google.com/edge/mediapipe/solutions/vision/hand_landmarker
- MediaPipe Python API: https://developers.google.com/edge/api/mediapipe/python/mp/tasks/vision/HandLandmarker
- Microsoft Windows.Graphics.Capture: https://learn.microsoft.com/en-us/windows/apps/develop/media-authoring-processing/screen-capture
- pywinauto: https://github.com/pywinauto/pywinauto
- pywinauto documentation: https://pywinauto.readthedocs.io/

## 15. Decisión propuesta

Construir primero **Gesture Lab**. Es el módulo más acotado para demostrar visión en vivo y gestos sin mezclar todavía automatización del escritorio. Después construir Screen Lab y finalmente Desktop Control Lab.

**Estado:** especificación propuesta; no se ha instalado ni ejecutado el prototipo en el PC del usuario.
