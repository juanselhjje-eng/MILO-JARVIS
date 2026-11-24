# Investigación técnica — OpenJarvis como referencia para M.I.L.O.

**Fecha de revisión:** 24-11-2026  
**Estado:** investigación documental inicial basada en el repositorio y documentación oficiales.  
**Proyecto analizado:** https://github.com/open-jarvis/OpenJarvis  
**Sitio oficial:** https://open-jarvis.github.io/OpenJarvis/

## 1. Resumen ejecutivo

OpenJarvis es un framework open-source de IA personal orientado a ejecución local y composición de agentes. No es simplemente un chatbot terminado ni un asistente de escritorio equivalente al Jarvis de Iron Man. Proporciona infraestructura reutilizable para modelos, motores de inferencia, agentes, herramientas, memoria, aprendizaje/evaluación y una interfaz de chat.

**Conclusión para M.I.L.O.:** merece una evaluación técnica como posible base o fuente de componentes para el núcleo de IA y agentes. No debe adoptarse como producto completo ni copiar su interfaz como diseño final, porque la interfaz documentada es principalmente una experiencia de chat web con telemetría, no la interfaz adaptativa contextual que el propietario ha confirmado.

## 2. Arquitectura documentada

OpenJarvis organiza su sistema en cinco primitivas:

1. **Intelligence:** catálogo y selección de modelos; permite elegir modelo o recomendarlo según el hardware.
2. **Engine:** capa intercambiable para ejecutar inferencia con Ollama, vLLM, SGLang, llama.cpp, MLX, Exo, LiteLLM y APIs cloud, entre otros.
3. **Agents:** agentes con razonamiento de varios pasos y uso de herramientas.
4. **Tools & Memory:** búsqueda web, calculadora, lectura de archivos, intérprete de código, recuperación documental, memoria persistente y servidores MCP externos.
5. **Learning:** registra trazas de interacción y ofrece mecanismos para evaluar y optimizar modelos, prompts y comportamiento.

La documentación también destaca funcionamiento local/offline-first, API compatible con OpenAI, detección de hardware y telemetría de latencia, tokens y coste/consumo.

## 3. Agentes incluidos

La documentación oficial enumera ocho agentes:

- `simple`: chat de una sola interacción, sin herramientas.
- `orchestrator`: bucle de uso de herramientas y razonamiento multi-turno.
- `operative`: agente orientado a tareas con planificación/ejecución estructurada.
- `native_react`: patrón ReAct de razonamiento, acción y observación.
- `native_openhands`: agente CodeAct que genera y ejecuta código Python.
- `deep_research`: investigación multi-etapa en web y documentos locales, con citas.
- `morning_digest`: informe diario programado con síntesis y salida de voz.
- `monitor_operative`: agente continuo de supervisión con estado y memoria.

Los modos se describen como bajo demanda, programados y continuos.

## 4. Capacidades documentadas relevantes

### Modelos y motores
- Admite motores locales y proveedores cloud.
- Detecta CPU, GPU, VRAM y RAM para recomendar configuración.
- Gestiona modelos disponibles y descargas.
- Ofrece política de selección/ruteo de modelos.
- Expone una API compatible con clientes OpenAI.

### Herramientas y programación
- Orquestación con llamadas a herramientas.
- Herramientas documentadas como calculadora, recuperación, lectura de archivos con validación de rutas y búsqueda web.
- El preset `code-assistant` declara ejecución de código, file I/O y acceso a shell.
- Puede generar y ejecutar código Python con el agente `native_openhands`.

Esto no equivale automáticamente a un entorno completo de ingeniería de software con editor visual, Git, pruebas de todo tipo, aislamiento robusto y control de escritorio: esos elementos deben evaluarse por separado.

### Memoria documental
- Indexa archivos y directorios.
- Divide el contenido en fragmentos y lo almacena; SQLite/FTS5 aparece como backend predeterminado en la guía.
- Recupera fragmentos relevantes e inyecta contexto en las consultas.
- Incluye búsqueda y estadísticas de memoria.

### Automatización
- Incluye scheduler basado en cron.
- Permite configurar tareas recurrentes y agentes de monitorización.
- Documenta trabajos como revisar correos de un proyecto en un horario.

### Interfaz y API
- Ofrece CLI, SDK Python, servidor API y aplicación web de navegador.
- La guía describe el frontend React como una interfaz de chat similar a ChatGPT, con streaming, uso de herramientas, monitorización energética y panel de telemetría.
- `jarvis gui` abre la interfaz gráfica en navegador.
- La documentación menciona instaladores de escritorio para Windows, macOS y Linux.

## 5. Lo que no debe darse por hecho

En las capacidades y guías oficiales revisadas no se encontró evidencia suficiente para afirmar que OpenJarvis ya proporcione, como capacidades integradas y listas para usar:

- Observación continua de la pantalla del usuario en tiempo real.
- Control general del mouse y teclado de Windows.
- Comprensión visual en vivo de cualquier ventana/aplicación.
- Acceso y análisis de cámara web en tiempo real.
- Reconocimiento de gestos de mano para controlar el PC.
- HUD de ventanas/paneles flotantes que se reorganizan contextualmente.
- Una experiencia completa de mayordomo por voz con conversación hablada continua e interrupciones naturales.

El informe diario con TTS no debe confundirse con un motor de conversación por voz en tiempo real. La ejecución de código y shell tampoco debe confundirse con control gráfico universal del computador.

Esta sección expresa el alcance que se pudo verificar en las páginas consultadas; no demuestra que ningún colaborador o integración externa pueda implementar esas funciones.

## 6. Instalación y compatibilidad

La documentación oficial presenta instalación para Windows nativo, además de macOS, Linux y WSL2. El instalador indica que puede preparar uv, entorno Python, Ollama y un modelo inicial. La interfaz de navegador requiere Node.js 22+ según la guía de inicio consultada. La documentación también describe requisitos Python 3.11–3.13 para el flujo de instalación.

La selección final de modelos locales debe depender de un diagnóstico real de CPU, GPU, VRAM y RAM. No asumir que cualquier modelo funcionará con buen rendimiento en el hardware del propietario.

## 7. Comparación con la visión de M.I.L.O.

| Necesidad de M.I.L.O. | OpenJarvis según documentación revisada | Decisión |
|---|---|---|
| IA híbrida local/nube | Sí | Evaluar/adaptar |
| Enrutamiento de modelos | Sí | Referencia importante |
| Agentes multi-paso | Sí | Evaluar/adaptar |
| Programación y ejecución de código | Sí, mediante preset/agente | Probar en sandbox |
| Lectura y recuperación documental | Sí | Evaluar/adaptar |
| Memoria persistente | Sí | Comparar diseño y aislamiento |
| Tareas programadas/monitorización | Sí | Evaluar/adaptar |
| API para integrar frontend propio | Sí | Evaluar/adaptar |
| Interfaz adaptativa contextual | No es lo documentado; su UI es chat web/telemetría | Diseñar en M.I.L.O. |
| Ver pantalla en vivo | No verificado | Construir/integrar aparte |
| Control mouse/teclado general | No verificado | Construir/integrar aparte |
| Cámara y visión en vivo | No verificado | Construir/integrar aparte |
| Gestos de mano | No verificado | Construir/integrar aparte |
| Voz conversacional natural continua | No verificado; sí se documenta TTS para digest | Construir/integrar aparte |
| Gestión integral de MILO AGENCY | No | Construir específicamente |

## 8. Recomendación técnica provisional

No hacer un fork completo todavía. Primero ejecutar una prueba de concepto aislada y medible:

1. Instalar OpenJarvis en un entorno de prueba compatible con Windows.
2. Ejecutar diagnóstico de hardware y registrar modelos/motores recomendados.
3. Probar un modelo local y un proveedor cloud opcional.
4. Probar el agente orchestrator con herramientas.
5. Probar el preset code-assistant en un proyecto desechable y sin secretos.
6. Indexar documentación de prueba y comprobar recuperación.
7. Ejecutar una tarea programada y verificar persistencia/registro.
8. Medir consumo de RAM/VRAM, latencia, estabilidad y calidad de resultados.
9. Revisar licencias, dependencias, superficie de seguridad y facilidad de integrar el runtime con el backend propio de M.I.L.O.

Solo después decidir si conviene: (a) usar OpenJarvis como base del núcleo, (b) integrar componentes específicos, o (c) tomar sus patrones de arquitectura como referencia y mantener implementación propia.

## 9. Criterios de decisión

OpenJarvis se adoptará como dependencia/base únicamente si la prueba demuestra:
- Compatibilidad estable con el Windows y hardware objetivo.
- Licencia compatible con el uso previsto.
- Integración limpia con memoria, permisos y auditoría de M.I.L.O.
- Posibilidad de intercambiar motores/modelos sin acoplar el producto.
- Capacidad de ejecutar herramientas con límites y aislamiento suficientes.
- Mantenimiento activo y dependencias aceptables.
- Ausencia de conflictos con la interfaz adaptativa y la arquitectura de MILO AGENCY.

## 10. Fuentes oficiales consultadas

- Repositorio: https://github.com/open-jarvis/OpenJarvis
- Documentación principal: https://open-jarvis.github.io/OpenJarvis/
- Guía Quick Start: https://github.com/open-jarvis/OpenJarvis/blob/main/docs/getting-started/quickstart.md
- Guía de instalación: https://github.com/open-jarvis/OpenJarvis/blob/main/docs/getting-started/installation.md

**Nota:** investigación inicial de documentación; no se ha instalado, ejecutado ni auditado el código de OpenJarvis en el PC del propietario. Las capacidades descritas son las que declaran las fuentes oficiales y requieren validación práctica antes de decidir una integración.
