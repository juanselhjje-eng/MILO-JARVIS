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


---

# Segunda revisión — Funciones adicionales y evaluación de integración

**Fecha:** 24-11-2026  
**Alcance:** revisión ampliada de documentación oficial actual. No se ejecutó el proyecto ni se inspeccionó cada línea del código fuente.

## 11. Hallazgo importante: sistema de Skills

OpenJarvis incorpora un sistema de habilidades extensible. Una skill puede contener instrucciones en `SKILL.md`, una secuencia estructurada de pasos en `skill.toml`, o ambos.

Características documentadas:
- Importar skills desde Hermes Agent, OpenClaw y repositorios GitHub.
- Mostrar un catálogo ligero de skills disponibles al agente.
- Permitir que el agente decida cuándo invocar una skill.
- Componer skills como subprocesos, con validación de ciclos y profundidad.
- Restringir herramientas disponibles por skill.
- Comprobar capacidades, aplicar límites y registrar eventos de auditoría.
- Descubrir secuencias recurrentes en trazas y proponerlas como skills.
- Optimizar descripciones y ejemplos mediante DSPy o GEPA.
- Desactivar por defecto la importación de scripts ejecutables de algunas fuentes salvo que se habilite expresamente.

**Valor para M.I.L.O.: muy alto.** Podemos estudiar un catálogo de habilidades para que M.I.L.O. aprenda flujos reutilizables de la agencia: preparar un proyecto, analizar requisitos, revisar un repositorio, generar pruebas o preparar una entrega. No debemos importar habilidades sin revisar su procedencia, permisos y contenido.

Fuente: https://open-jarvis.github.io/OpenJarvis/user-guide/skills/

## 12. Canales de mensajería: WhatsApp

OpenJarvis documenta un sistema de canales conectables. Entre ellos:
- WhatsApp Business Cloud API.
- WhatsApp mediante Baileys.
- Telegram.
- Discord.
- Slack.
- Webhooks y otros canales.

El canal Baileys se conecta mediante un puente Node.js, permite recibir y enviar mensajes y conserva el estado de autenticación. La documentación aclara que funciona mediante el protocolo de WhatsApp Web y requiere autenticación QR. El adaptador de WhatsApp Cloud API se documenta como send-only en la referencia consultada.

**Valor para M.I.L.O. AGENCY: alto, pero con una decisión técnica pendiente.** No asumir que el canal Baileys es equivalente a una integración oficial de WhatsApp Business. Para una operación comercial real hay que evaluar condiciones de plataforma, estabilidad, privacidad y soporte; preferir una integración oficial cuando el caso de uso lo requiera.

Fuentes:
- https://open-jarvis.github.io/OpenJarvis/user-guide/channels/
- https://open-jarvis.github.io/OpenJarvis/api-reference/openjarvis/channels/whatsapp/

## 13. Seguridad y permisos

OpenJarvis documenta varias capas:
- Escaneo del equipo anfitrión.
- Revisión de límites entre datos locales y servicios externos.
- Escaneo de entradas y salidas para secretos, datos personales y rutas sensibles.
- Registro de auditoría.
- Configuración para advertir, redactar o bloquear hallazgos.
- Envoltorio de guardrails que puede colocarse delante de distintos motores de inferencia.

**Advertencia importante encontrada en la documentación:** la opción `enforce_tool_confirmation` aparece aceptada por el cargador de configuración, pero la propia documentación indica que actualmente no está aplicada de forma efectiva. Por tanto, no se debe asumir que activar esa opción garantiza confirmación antes de cada herramienta. M.I.L.O. tendría que implementar su propio control de permisos y aprobaciones en el runtime, y probarlo.

Fuente: https://open-jarvis.github.io/OpenJarvis/user-guide/security/

## 14. Aplicación de escritorio

OpenJarvis dispone de una aplicación nativa de escritorio basada en Tauri/React, con instaladores para Windows x64 y otras plataformas. La aplicación abre la misma experiencia de chat que la interfaz web, muestra telemetría y consumo energético y puede permanecer accesible desde la bandeja del sistema.

El backend sigue siendo un proceso separado que debe iniciarse en el equipo.

**Conclusión:** tener un instalador de escritorio no significa tener una interfaz adaptativa. La experiencia descrita sigue centrada en chat y telemetría; M.I.L.O. debe diseñar su propia experiencia contextual.

Fuente: https://open-jarvis.github.io/OpenJarvis/downloads/

## 15. Compatibilidad y requisitos: implicaciones para el PC del propietario

La guía de instalación actual indica Python 3.11–3.13, uv, Git y Rust para el entorno principal. Node.js 22+ es necesario para la interfaz web y el puente Baileys. También se documenta instalación nativa en Windows, además de WSL2.

El hardware previamente reportado por el propietario incluye Intel i5-11400H, 16 GB de RAM y una NVIDIA RTX 3050 cuyo identificador completo no está confirmado. Esto no basta para asegurar qué modelos locales serán prácticos: antes se debe consultar VRAM exacta, memoria disponible, espacio libre y temperatura/rendimiento bajo carga.

Fuentes:
- https://open-jarvis.github.io/OpenJarvis/getting-started/installation/
- https://open-jarvis.github.io/OpenJarvis/getting-started/windows-native/

## 16. Arquitectura recomendada para M.I.L.O. tras la segunda revisión

No recomiendo convertir OpenJarvis en toda la aplicación M.I.L.O. La separación aconsejada es:

1. **MILO EXPERIENCE:** interfaz adaptativa propia, voz, HUD y espacios de trabajo contextuales.
2. **MILO CORE:** identidad, contexto, memoria de producto, permisos, auditoría y ciclo de tareas.
3. **AI ADAPTER LAYER:** contrato propio para modelos locales y cloud; OpenJarvis podría evaluarse como implementación/adaptador de agentes e inferencia, no como dependencia obligatoria.
4. **AGENT & SKILL RUNTIME:** agentes especializados, skills revisadas, composición de tareas y ejecución aislada.
5. **TOOL GATEWAY:** herramientas del PC, archivos, documentos, navegador, cámara y canales, cada una con permisos y registro.
6. **MILO AGENCY:** clientes, proyectos, requisitos, planificación, entregas y soporte; separado del runtime genérico de agentes.
7. **CONNECTORS:** WhatsApp y otros canales mediante adaptadores intercambiables.

La UI no debe hablar directamente con herramientas privilegiadas. Debe comunicarse con el backend de M.I.L.O.; el backend verifica identidad, permisos, límites y aprobaciones antes de ejecutar una acción.

## 17. Matriz de capacidades revisada

| Área | Evidencia en OpenJarvis | Evaluación para M.I.L.O. |
|---|---|---|
| Modelos locales y cloud | Documentado | Evaluar como adaptador |
| Agentes multi-paso | Documentado | Evaluar e integrar si pasa pruebas |
| Skills importables y componibles | Documentado | Referencia prioritaria |
| Programación con ejecución de código | Documentado | Probar aislado |
| Memoria y recuperación documental | Documentado | Evaluar y comparar |
| Tareas programadas/monitorización | Documentado | Reutilización posible |
| WhatsApp y otros canales | Documentado | Evaluar canal y condiciones |
| Seguridad y auditoría | Documentado, con límites | No delegar todas las garantías |
| Escritorio Windows | Documentado | No resuelve el diseño adaptativo |
| Cámara y gestos en vivo | No confirmado | Requiere módulo aparte |
| Visión continua de pantalla | No confirmado | Requiere módulo aparte |
| Control universal mouse/teclado | No confirmado | Requiere módulo aparte |
| Voz conversacional continua | No confirmado en la documentación consultada | Requiere módulo aparte |
| Gestión integral de agencia | No es su objetivo principal | Construir en MILO AGENCY |

## 18. Próxima fase de investigación: prueba técnica, no más suposiciones

La siguiente actividad debe ser una prueba de concepto controlada en Windows, sin conceder acceso general al equipo:

- Preparar un entorno separado de pruebas.
- Instalar OpenJarvis siguiendo la guía oficial y verificar versiones.
- Ejecutar diagnóstico y registrar hardware/modelos recomendados.
- Probar chat local, agente orchestrator y un modelo cloud opcional.
- Probar una skill instructiva y otra estructurada, revisando antes sus permisos.
- Probar lectura y creación de archivos solo dentro de una carpeta de prueba.
- Probar programación de una tarea inocua y comprobar su persistencia.
- Revisar cómo se registran trazas, errores y llamadas a herramientas.
- Verificar el comportamiento real de guardrails y aprobaciones; no confiar en una opción de configuración sin prueba.
- Medir RAM, VRAM, latencia y estabilidad.
- Revisar licencia del proyecto y de cualquier componente/skill antes de incorporarlo.

**No instalar ni ejecutar todavía con acceso general a documentos personales, credenciales, producción o cuentas comerciales.** La decisión de adopción se toma después de los resultados.

## 19. Fuentes oficiales añadidas

- Skills: https://open-jarvis.github.io/OpenJarvis/user-guide/skills/
- Channels: https://open-jarvis.github.io/OpenJarvis/user-guide/channels/
- Security: https://open-jarvis.github.io/OpenJarvis/user-guide/security/
- Desktop downloads: https://open-jarvis.github.io/OpenJarvis/downloads/
- Windows native: https://open-jarvis.github.io/OpenJarvis/getting-started/windows-native/
- Installation: https://open-jarvis.github.io/OpenJarvis/getting-started/installation/

**Estado de la investigación:** revisión documental ampliada. Sigue pendiente la prueba de ejecución en el PC. No se afirma que OpenJarvis ya haya sido instalado, ejecutado o validado en el entorno del propietario.
