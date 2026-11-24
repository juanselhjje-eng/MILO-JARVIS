# Contexto maestro — M.I.L.O.

**Estado del documento:** decisiones confirmadas y visión del propietario, consolidadas el 24-11-2026.  
**Propósito:** dar a cualquier modelo de IA, agente de programación o desarrollador el contexto necesario para continuar el proyecto sin convertirlo en otro chatbot genérico.

## 1. Visión del propietario

El propietario ha intentado construir aproximadamente 15 asistentes tipo Jarvis y ninguno ha cumplido su visión. Los intentos anteriores fallaron porque parecían chatbots normales: respondían en texto, pero no podían operar realmente el computador, crear/modificar archivos, controlar mouse y teclado, observar pantalla/cámara, leer documentos ni desarrollar software funcional.

M.I.L.O. debe ser un asistente digital inspirado en la experiencia de un mayordomo tecnológico de ciencia ficción, pero implementado con capacidades reales y comprobables en el mundo digital. No se busca copiar literalmente tecnología ficticia imposible; se busca construir equivalentes prácticos mediante software, modelos de IA, visión artificial, automatización y servicios conectados.

**Regla esencial:** M.I.L.O. no debe afirmar que hizo algo si no ejecutó la acción y verificó el resultado. Una respuesta con código pegado en el chat no equivale a crear un archivo, y escribir archivos no equivale a entregar un programa que funciona.

## 2. Identidad confirmada

- Nombre del producto: **M.I.L.O.**
- Expansión elegida: **My Intelligent Life Operator**.
- Debe identificarse como M.I.L.O.; no como Jarvis.
- El nombre del repositorio `MILO-JARVIS` no cambia el nombre del producto.
- Personalidad: mayordomo digital, competente, discreto, resolutivo, organizado y proactivo.
- Voz deseada: masculina, profunda, elegante y natural, en español.
- Idioma principal de interacción: español. El soporte multilingüe podrá añadirse.
- Estilo de respuesta: claro, contextual y orientado a resultados; informar qué hizo, qué falta y qué bloqueos encontró.

## 3. Plataformas y modo de funcionamiento

Plataformas objetivo:
- PC con Windows como entorno principal de ejecución y desarrollo.
- Celular como interfaz y punto de acceso complementario.
- Internet/nube para modelos de IA, sincronización y servicios remotos.

Modo de operación confirmado:
- M.I.L.O. estará disponible cuando el propietario lo active.
- Una vez activado, podrá permanecer trabajando en segundo plano.
- No se exige que esté ejecutándose permanentemente cuando el propietario no lo haya activado.
- Debe poder detenerse rápidamente y mostrar cuándo utiliza cámara, micrófono, pantalla o control del PC.

Interfaz:
- Dos modos complementarios: una interfaz minimalista para uso cotidiano y una interfaz futurista tipo HUD inspirada en pantallas de ciencia ficción.
- La interfaz futurista debe incluir paneles, estado de tareas, actividad, cámara/pantalla cuando estén activas, proyectos y controles.
- No se debe sacrificar la estabilidad del núcleo por construir primero animaciones o efectos visuales.

## 4. Capacidades personales deseadas

### Conversación e inteligencia
- Conversación natural por voz y texto.
- Comprender objetivos, contexto e intención.
- Planificar tareas de varios pasos sin exigir que el usuario describa cada clic.
- Elegir herramientas según la tarea.
- Recuperarse de errores, pedir aclaración cuando falte un dato crítico y verificar los resultados.
- Iniciativa: detectar asuntos pendientes, preparar análisis y sugerir acciones útiles, sin ejecutar operaciones fuera de los permisos.

### Control del computador
- Ver la pantalla en tiempo real o mediante capturas periódicas mientras la función esté activada.
- Identificar ventanas, textos, botones y errores de interfaz.
- Abrir aplicaciones y archivos.
- Interactuar con mouse y teclado.
- Leer, crear, modificar, mover y organizar archivos dentro de ubicaciones autorizadas.
- Ejecutar herramientas de diagnóstico del PC y explicar los resultados.
- Crear, ejecutar, probar y depurar programas, páginas, aplicaciones y videojuegos.

### Cámara y gestos
- Acceder a la cámara únicamente cuando el usuario active la función y exista un indicador visible.
- Procesar vídeo localmente siempre que sea posible.
- Reconocer manos y gestos configurados mediante visión artificial.
- Permitir asignar gestos a acciones de interfaz, como seleccionar, confirmar o cambiar panel.
- Los gestos deben tener calibración, tolerancia a falsos positivos y opción para desactivarlos.
- No transmitir vídeo continuamente a modelos remotos por defecto.

### Documentos
Debe poder extraer y analizar contenido de, como mínimo:
- PDF.
- Word/DOCX.
- Excel/XLSX.
- PowerPoint/PPTX.
- Archivos de texto, Markdown, CSV y código.
Debe informar si un documento está escaneado, protegido, dañado o requiere OCR.

## 5. Inteligencia artificial: decisión confirmada

Estrategia **híbrida**:
- Modelos gratuitos en la nube cuando estén disponibles y sean adecuados.
- Modelos locales mediante un runtime como Ollama cuando sean viables.
- Proveedores intercambiables mediante una interfaz común.
- Selección de proveedor/modelo según tarea, latencia, calidad, disponibilidad, privacidad y coste.
- Fallback cuando un proveedor falle, respetando límites y evitando bucles de reintento.
- Registrar proveedor, modelo, consumo estimado, latencia y errores cuando la información esté disponible.

No asumir que un modelo o endpoint gratuito será siempre gratuito, estable o ilimitado. El sistema debe poder funcionar con límites y degradarse de forma controlada si no hay proveedor disponible.

## 6. M.I.L.O. y la agencia de programación

M.I.L.O. tiene dos grandes divisiones:
1. **MILO PERSONAL:** asistente personal, voz, visión, memoria, PC y organización.
2. **MILO AGENCY:** centro de operaciones de la agencia de programación.

La agencia ofrece o pretende ofrecer:
- Páginas web.
- Aplicaciones y sistemas.
- Chatbots e inteligencia artificial.
- Automatizaciones.
- Desarrollo de software a medida.
- Videojuegos.
- Otros servicios tecnológicos.

M.I.L.O. debe ayudar a gestionar prácticamente toda la operación de la agencia: clientes, requisitos, propuestas, proyectos, arquitectura, desarrollo, pruebas, infraestructura, costes, entregas y soporte.

### Autonomía confirmada
El propietario eligió: **gestionar autónomamente las operaciones autorizadas e informar de lo realizado**.

Esto significa:
- Puede completar cadenas de tareas rutinarias dentro de permisos aprobados.
- No debe pedir permiso para cada paso pequeño que ya esté autorizado.
- Debe informar avances, resultados, errores, decisiones relevantes y bloqueos.
- Debe solicitar aprobación para operaciones críticas o fuera del alcance autorizado.

## 7. Principios de seguridad y límites de autonomía

La autonomía nunca significa acceso ilimitado.

- Separar datos, archivos, credenciales y contextos de cada cliente y proyecto.
- Aplicar mínimo privilegio: cada herramienta/agente recibe solo los permisos necesarios.
- No guardar claves API en código, repositorios, prompts visibles ni registros.
- Usar variables de entorno o un almacén de secretos.
- No ejecutar comandos arbitrarios propuestos por el modelo sin validación.
- Ejecutar código de proyectos en entornos aislados cuando sea posible.
- Mantener registro auditable de acciones, archivos modificados, comandos, resultados y errores.
- Ofrecer botón/orden de parada y cancelación de tareas.
- Pedir confirmación antes de borrar datos, sobrescribir archivos importantes, instalar software, cambiar configuraciones críticas, enviar comunicaciones externas vinculantes, gastar dinero o desplegar en producción.
- La cámara, el micrófono y la captura de pantalla deben tener indicadores visibles y controles explícitos.
- No realizar acciones de seguridad ofensiva; el trabajo de seguridad de la agencia será defensivo y autorizado.

## 8. Hardware conocido para orientar el diseño

El equipo reportado anteriormente por el propietario:
- Windows 10 Home Single Language.
- Intel Core i5-11400H.
- 16 GB de RAM.
- GPU NVIDIA GeForce RTX 3050 (el identificador completo no quedó confirmado).
- Almacenamiento principal aproximado de 476 GB.

Tratar estos datos como referencia previa, no como diagnóstico actual. Antes de optimizar rendimiento o seleccionar modelos locales, ejecutar un diagnóstico actualizado. Diseñar para que visión, voz y modelos locales puedan limitar recursos o apagarse por separado.

## 9. Qué significa que M.I.L.O. sea realmente funcional

Una capacidad solo se considera implementada cuando:
1. Tiene una implementación real, no una respuesta simulada.
2. Puede ejecutarse en el entorno objetivo.
3. Tiene pruebas repetibles.
4. Maneja errores y permisos.
5. Devuelve un resultado verificable.
6. Está documentada.
7. Se ha probado en un caso real representativo.

No usar interfaces de demostración, datos falsos, funciones vacías ni respuestas simuladas para aparentar capacidades terminadas.

## 10. Criterio de producto

M.I.L.O. debe sentirse como un sistema coherente, no como una colección desordenada de scripts o agentes. Debe compartir identidad, memoria controlada, estado de tareas, herramientas y permisos entre sus módulos.

El primer objetivo no es construir todo de una vez. Es construir un núcleo pequeño, estable y comprobable que permita agregar capacidades sin rehacer el proyecto.
