# Hoja de ruta — M.I.L.O.

**Estado:** plan inicial. Las fases son objetivos; ninguna se considera completada hasta que sus criterios de aceptación se prueben en el entorno real.

## Reglas para avanzar

- Trabajar por incrementos pequeños.
- Mantener una rama de trabajo por tarea o módulo.
- Añadir pruebas junto con la implementación.
- Ejecutar pruebas y análisis antes de marcar una tarea como terminada.
- Documentar decisiones técnicas importantes.
- No construir funcionalidades ficticias ni módulos vacíos.
- No iniciar la siguiente fase si el núcleo de la fase anterior no es estable.

## Fase 0 — Preparación del repositorio
- Documentación de visión, arquitectura, agencia, roadmap e instrucciones.
- Convenciones de código y seguridad.
- Estructura mínima de proyecto.
- Configuración de entorno de desarrollo.
**Aceptación:** un desarrollador/IA puede explicar correctamente la visión, instalar el entorno y ejecutar las comprobaciones iniciales.

## Fase 1 — MILO CORE FOUNDATION (primer módulo)
Objetivo: núcleo funcional mínimo.

Incluye:
- Configuración y validación.
- Personalidad M.I.L.O. configurable.
- API local.
- Orquestador básico.
- Adaptador común de modelos.
- Un proveedor cloud y un proveedor local, con configuración opcional.
- Fallback limitado.
- Memoria persistente de conversaciones.
- Registro de herramientas.
- Herramienta demostrativa segura.
- Logs estructurados.
- Manejo de errores.
- Pruebas automatizadas.

**Criterios de aceptación:**
- El servicio inicia en Windows.
- La API recibe una solicitud y devuelve respuesta.
- Puede conversar en español.
- El proveedor se configura sin modificar código.
- Los fallos del proveedor se informan y el fallback se comporta según configuración.
- La conversación persiste tras reiniciar.
- Una herramienta de demostración se ejecuta realmente.
- La respuesta distingue entre herramienta ejecutada, fallida y no ejecutada.
- Los secretos no aparecen en logs ni repositorio.
- Las pruebas automatizadas pasan.

No incluir todavía interfaz gráfica, cámara, control de mouse, voz ni ejecución arbitraria de comandos.

## Fase 2 — MEMORY ENGINE
- Memoria de sesión y conversaciones.
- Memoria personal explícita y editable.
- Contexto de agencia.
- Contexto separado por cliente y proyecto.
- Retención, exportación y eliminación controladas.
**Aceptación:** recuperar información pertinente sin filtrar datos entre contextos.

## Fase 3 — TOOL SYSTEM
- Registro formal de herramientas.
- Esquemas de entrada/salida.
- Política de permisos.
- Niveles de riesgo.
- Aprobaciones.
- Timeout, cancelación y auditoría.
**Aceptación:** el modelo puede solicitar herramientas y el runtime decide de forma segura si ejecutarlas.

## Fase 4 — FILE & DOCUMENT ENGINE
- Listar, leer, crear y editar archivos en workspaces autorizados.
- PDF, DOCX, XLSX, PPTX, texto y código.
- Extracción de contenido y manejo de documentos escaneados/OCR cuando proceda.
- Versionado y registro de cambios.
**Aceptación:** crear y modificar archivos reales, volver a leerlos y verificar su contenido.

## Fase 5 — AGENCY FOUNDATION
- Clientes, contactos y oportunidades.
- Proyectos, requisitos y documentos.
- Tareas, hitos y asignaciones.
- Actividad y permisos por cliente/proyecto.
- Panel básico de agencia.
**Aceptación:** registrar y consultar proyectos completos con aislamiento de datos.

## Fase 6 — DEVELOPMENT ENGINE
- Gestión segura de repositorios.
- Workspaces por proyecto.
- Lectura y modificación de código.
- Ejecución en entornos aislados.
- Construcción, pruebas y depuración.
- Git y ramas.
**Aceptación:** implementar una modificación pequeña en un proyecto de prueba, ejecutar pruebas y presentar diff y evidencia.

## Fase 7 — AGENT ORCHESTRATOR
- Agentes especializados bajo demanda.
- Descomposición de tareas.
- Dependencias y concurrencia limitada.
- Asignación por habilidades.
- Revisión independiente.
- Presupuesto por tarea/proyecto.
**Aceptación:** coordinar un flujo de varios agentes sin perder trazabilidad ni mezclar contextos.

## Fase 8 — QUALITY ENGINE
- Pruebas unitarias, integración y funcionales.
- Revisión de código.
- Criterios de aceptación.
- Reportes de defectos y regresiones.
**Aceptación:** impedir que un trabajo se marque completado si las verificaciones obligatorias fallan.

## Fase 9 — PC CONTROL
- Estado y diagnóstico de Windows.
- Abrir aplicaciones y ventanas.
- Mouse y teclado mediante APIs apropiadas.
- Automatización semántica preferida sobre coordenadas.
- Confirmación para acciones de riesgo.
**Aceptación:** ejecutar un flujo autorizado en una aplicación de prueba y verificar el resultado.

## Fase 10 — VISION ENGINE
- Captura de pantalla bajo demanda/intervalos configurables.
- Identificación de ventanas y contenido.
- Cámara local activada explícitamente.
- Indicadores visibles y controles.
**Aceptación:** describir elementos visibles de una pantalla/cámara de prueba con límites de privacidad y rendimiento.

## Fase 11 — GESTURE ENGINE
- Detección de manos.
- Gestos configurables.
- Calibración y control de falsos positivos.
- Mapeo de gestos a acciones no críticas.
**Aceptación:** reconocer gestos de prueba de forma consistente y permitir desactivarlos.

## Fase 12 — VOICE ENGINE
- Activación por botón o palabra de activación evaluada.
- STT español.
- TTS con voz masculina profunda/elegante/natural, según voces disponibles y licencias.
- Interrupciones y control de audio.
**Aceptación:** conversación hablada estable, latencia medida y controles claros de micrófono.

## Fase 13 — AUTONOMY ENGINE
- Planificación multi-paso.
- Scheduler.
- Trabajos en segundo plano.
- Recuperación y reanudación.
- Informes proactivos.
- Políticas de aprobación.
**Aceptación:** completar una tarea autorizada de varios pasos, recuperarse de un fallo y registrar cada acción.

## Fase 14 — DESKTOP / HUD
- Aplicación de escritorio.
- Interfaz minimalista y modo HUD.
- Actividad, tareas, permisos y estado de sensores.
- Controles de emergencia.
**Aceptación:** UI conectada al backend real, no una maqueta con datos falsos.

## Fase 15 — MOBILE & CLOUD
- Acceso desde celular.
- Sincronización segura.
- Notificaciones.
- Acceso remoto autenticado.
- Base de datos/servicios remotos cuando sea necesario.
**Aceptación:** acceso desde dispositivo autorizado con autenticación, cifrado y aislamiento de datos.

## MILO AGENCY — hitos funcionales

La operación de agencia se implementará progresivamente dentro de las fases anteriores:
1. Registrar clientes y proyectos.
2. Capturar requisitos.
3. Crear tareas y asignaciones.
4. Gestionar repositorios y documentos.
5. Coordinar agentes de desarrollo.
6. Ejecutar pruebas y auditorías.
7. Preparar entregas y documentación.
8. Gestionar incidencias y soporte.
9. Registrar presupuestos y costes.
10. Integrar canales de comunicación autorizados.

## Primer encargo de implementación: TASK-001

**Nombre:** MILO CORE FOUNDATION.

Antes de escribir código:
1. Leer README y todos los documentos de `docs/`.
2. Resumir requisitos y decisiones confirmadas.
3. Identificar contradicciones o datos faltantes.
4. Proponer estructura mínima y dependencias justificadas.
5. Implementar solo el alcance de Fase 1.
6. Añadir pruebas y documentación.
7. Ejecutar las pruebas en Windows o declarar con precisión qué no pudo ejecutarse.

No declarar Fase 1 terminada si solo se creó la estructura o si las pruebas no se ejecutaron.
