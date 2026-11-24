# Arquitectura técnica — M.I.L.O.

**Estado:** arquitectura propuesta para validar mediante prototipos. La visión funcional y las decisiones de producto están confirmadas en `MASTER_SPEC.md`; las tecnologías de esta página son recomendaciones técnicas, no compromisos irreversibles.

## 1. Principios arquitectónicos

1. Modularidad: cada capacidad debe tener límites claros y contratos documentados.
2. Núcleo desacoplado: el orquestador no depende directamente de un proveedor de IA.
3. Herramientas explícitas: el modelo solicita herramientas; el runtime valida permisos y ejecuta.
4. Verificación: toda herramienta devuelve estado, salida, errores y evidencia suficiente.
5. Asincronía: las tareas largas se ejecutan como trabajos con estado, cancelación y eventos.
6. Seguridad por diseño: permisos por usuario, proyecto, herramienta y operación.
7. Observabilidad: logs estructurados, trazas de tareas, métricas de uso y auditoría.
8. Portabilidad razonable: evitar dependencias innecesarias de un único proveedor de IA.

## 2. Arquitectura lógica

```text
                  INTERFACES
      Desktop / Voz / HUD / Móvil / Web
                       |
                API + Event Gateway
                       |
              CORE / ORCHESTRATOR
       Intent -> Context -> Plan -> Policy
                       |
          +------------+-------------+
          |            |             |
      AI Gateway   Memory        Task Engine
          |            |             |
     Cloud/Local   Personal/     Queue/State/
     providers     Agency/       Scheduler
                   Project
                       |
                 TOOL REGISTRY
                       |
      +----------------+-------------------+
      |                |                   |
   PC & Files      Development         Perception
   Documents       Browser/Git         Screen/Camera
   Diagnostics     Tests/Build         Gestures
      |
  Agency modules: clients, projects, delivery, support
                       |
          Storage / Audit / Secrets / Policy
```

## 3. Tecnologías recomendadas (provisionales)

| Área | Opción inicial | Motivo / condición |
|---|---|---|
| Backend | Python 3.12+ | Ecosistema de IA, automatización y documentos |
| API local | FastAPI + Uvicorn | API tipada y WebSocket |
| Validación | Pydantic | Contratos de entrada/salida |
| Persistencia inicial | SQLite + SQLAlchemy + aiosqlite | Desarrollo local y prototipo |
| Persistencia multiusuario/remota | PostgreSQL | Incorporar cuando exista sincronización/operación remota |
| Cliente desktop | Evaluar Tauri o Electron | Elegir tras prototipo de cámara, ventanas, HUD y empaquetado |
| UI | HTML/CSS/TypeScript | Reutilización entre desktop y posible móvil/web |
| Comunicación | REST + WebSocket | Solicitudes y eventos de tareas |
| Proveedores IA | Adaptadores propios + HTTPX | Mantener intercambiables OpenRouter y Ollama |
| Visión | OpenCV + MediaPipe | Cámara y gestos locales |
| Captura de pantalla | MSS / APIs nativas de Windows | Captura bajo demanda y con límites |
| Voz a texto | Faster-Whisper u opción equivalente | Comparar calidad, latencia y recursos |
| Texto a voz | Piper u opción equivalente | Evaluar voces españolas y licencia |
| Documentos | PyMuPDF, python-docx, openpyxl, python-pptx | PDF, Word, Excel y PowerPoint |
| Automatización Windows | UI Automation / pywinauto, PyWin32; PyAutoGUI solo cuando proceda | Preferir accesibilidad semántica sobre coordenadas |
| Diagnóstico | psutil + APIs de Windows | Procesos y recursos |
| Pruebas | pytest + pytest-asyncio | Validación automatizada |
| Calidad | Ruff + mypy/pyright | Estilo y análisis estático |
| Versionado | Git + GitHub | Historial y revisión |

**Importante:** no instalar todas las dependencias al inicio. Cada módulo agrega solo lo que necesita. Verificar compatibilidad, mantenimiento, licencias y requisitos de Windows antes de fijar versiones.

## 4. Componentes del backend

### Core
- `orchestrator`: coordina el ciclo de solicitud.
- `intent`: clasifica objetivo y contexto.
- `planner`: crea un plan de pasos y dependencias.
- `policy`: valida permisos antes de cada acción.
- `task_engine`: administra tareas, estados, reintentos y cancelación.
- `personality`: identidad, tono e instrucciones de M.I.L.O.

### AI Gateway
- Interfaz común de proveedor.
- Adaptadores cloud y local.
- Selección de modelo según tarea.
- Fallback con límite de reintentos.
- Timeouts, control de concurrencia y presupuesto.
- Registro de latencia, errores y consumo cuando el proveedor lo exponga.

### Memory
- Conversaciones y contexto de sesión.
- Memoria personal.
- Memoria de agencia.
- Memoria por cliente y proyecto.
- Recuperación por permisos: un agente no puede recuperar contexto de otro cliente.
- Posible búsqueda semántica en una fase posterior; no es requisito para el primer prototipo.

### Tool Registry
Cada herramienta declara:
- Nombre y descripción.
- Esquema de argumentos.
- Permisos requeridos.
- Riesgo y nivel de aprobación.
- Timeout y límites de recursos.
- Función de ejecución.
- Resultado estructurado.
- Pruebas y política de auditoría.

El modelo no ejecuta herramientas directamente: solicita una acción al orquestador, que valida y delega.

### Perception
- Captura de pantalla con frecuencia configurable.
- Cámara activada explícitamente.
- Procesamiento local preferente.
- Eventos de detección de manos/gestos.
- Indicadores de cámara y pantalla activos.
- Botón de apagado y límites de rendimiento.

### Voice
- Detección de activación o pulsar-para-hablar inicialmente.
- STT para transcripción.
- TTS con voz española seleccionable.
- Interrupción de reproducción y control de turnos.
- No mantener micrófono abierto sin un estado visible y controlable.

## 5. API y eventos propuestos

Rutas iniciales:
- `GET /health`: salud del servicio.
- `POST /v1/chat`: enviar mensaje.
- `GET /v1/tasks/{task_id}`: consultar tarea.
- `POST /v1/tasks/{task_id}/cancel`: cancelar tarea.
- `GET /v1/tools`: herramientas habilitadas para el usuario.
- `GET /v1/activity`: actividad reciente.
- `WS /v1/events`: eventos de ejecución y estado.

Eventos sugeridos:
- `task.created`
- `task.started`
- `task.progress`
- `tool.requested`
- `tool.approved`
- `tool.completed`
- `tool.failed`
- `task.completed`
- `task.cancelled`
- `approval.required`

Los nombres y esquemas deben versionarse y documentarse.

## 6. Modelo de ejecución de tareas

Estados mínimos:
`queued -> planning -> awaiting_approval (si aplica) -> running -> verifying -> completed`

Estados alternativos:
`failed`, `cancelled`, `blocked`.

Cada paso registra:
- ID de tarea y paso.
- Objetivo.
- Herramienta invocada.
- Parámetros no secretos.
- Permisos evaluados.
- Inicio y fin.
- Resultado y evidencia.
- Error y reintentos.
- Archivos afectados.
- Coste/uso estimado cuando esté disponible.

## 7. Seguridad y aislamiento

- Separar secretos de la base de datos de contenido y de los logs.
- No registrar API keys, tokens, contraseñas ni contenido sensible innecesario.
- Directorios de trabajo por proyecto con rutas permitidas.
- Validar rutas para evitar traversal y acceso fuera del workspace.
- Entornos aislados para ejecutar código generado o de clientes.
- Limitar CPU, RAM, tiempo, red y tamaño de archivos en tareas de desarrollo.
- Herramientas de producción requieren aprobación explícita.
- Auditar acceso a documentos y datos de clientes.
- Separar configuración de desarrollo, pruebas y producción.
- Mantener copias de seguridad y recuperación para datos empresariales; no confundir respaldo con permiso para modificar producción.

## 8. Decisiones pendientes de prototipo

No presentar como confirmadas hasta probarlas:
- Electron frente a Tauri para escritorio.
- Proveedor y modelo concreto de voz española.
- Proveedor cloud principal y modelos gratuitos disponibles.
- Modelo local que funcione adecuadamente en el hardware real.
- Framework de agentes o implementación propia del orquestador.
- Cuándo migrar SQLite a PostgreSQL.
- Estrategia móvil: app nativa, PWA o cliente multiplataforma.
- Framework de búsqueda semántica/vectorial, si se demuestra necesario.

## 9. Restricciones de implementación

- No crear carpetas o clases vacías para aparentar progreso.
- No crear un "agente" por cada función trivial.
- No introducir microservicios en la primera versión: empezar con un monolito modular local.
- No depender de que un modelo mantenga memoria implícita; persistir estado explícitamente.
- No ejecutar código arbitrario en el proceso principal.
- No exponer la API local sin autenticación/controles adecuados si se habilita acceso desde red o móvil.
