# MILO AGENCY — Departamentos y operación

**Estado:** estructura organizativa solicitada y aprobada por el propietario como objetivo de producto. La implementación se hará por etapas.

## 1. Propósito

MILO AGENCY es el centro de operaciones de la agencia de programación del propietario. M.I.L.O. debe ayudar a gestionar prácticamente toda la operación: desde registrar una oportunidad y entender al cliente hasta planificar, construir, probar, entregar y mantener productos tecnológicos.

Servicios contemplados:
- Páginas web.
- Aplicaciones y sistemas.
- Chatbots e inteligencia artificial.
- Automatizaciones.
- Desarrollo de software a medida.
- Videojuegos.
- Otros servicios tecnológicos.

## 2. Modelo de dirección

M.I.L.O. actúa como director/coordinador digital de la operación. El propietario sigue siendo el responsable de la agencia y conserva las decisiones reservadas.

M.I.L.O. debe:
- Mantener una visión global de clientes, proyectos, tareas, riesgos y recursos.
- Coordinar departamentos y especialistas.
- Distribuir tareas según habilidades y disponibilidad.
- Detectar bloqueos y retrasos.
- Supervisar calidad y cumplimiento de requisitos.
- Informar avances y decisiones relevantes.
- Ejecutar de forma autónoma operaciones que estén expresamente autorizadas.

No debe inventar aprobaciones, comprometer precios o plazos con clientes, realizar pagos, firmar acuerdos ni desplegar a producción sin la autorización correspondiente.

## 3. Departamentos definitivos

### 3.1 Dirección general
Responsabilidad: coordinar el conjunto de la agencia.
- Prioridades y planificación global.
- Asignación de recursos y agentes.
- Seguimiento de proyectos.
- Resolución/escalamiento de bloqueos.
- Informes para el propietario.
- Control de objetivos y riesgos.

### 3.2 Comercial y clientes
- Registro de prospectos y clientes.
- Contactos y canales autorizados.
- Historial de conversaciones.
- Oportunidades y solicitudes.
- Preparación de propuestas y cotizaciones para revisión.
- Seguimiento comercial.
- Comunicación con clientes solo con permisos y plantillas aprobadas.

### 3.3 Análisis y requisitos
- Entrevistar/analizar necesidades.
- Identificar usuarios, flujos y funcionalidades.
- Definir requisitos funcionales y no funcionales.
- Identificar restricciones, integraciones y riesgos.
- Preparar criterios de aceptación.
- Registrar dudas y supuestos.
- Mantener trazabilidad entre requisito, tarea, prueba y entrega.

### 3.4 Arquitectura tecnológica
- Selección justificada de tecnologías.
- Diseño de componentes, APIs y datos.
- Arquitectura de seguridad y permisos.
- Infraestructura y escalabilidad.
- Estándares y convenciones.
- Decisiones técnicas documentadas (ADR).
- Revisión de impacto y deuda técnica.

### 3.5 Desarrollo e ingeniería
Especialidades activables según el proyecto:
- Frontend y experiencia de usuario.
- Backend y APIs.
- Full-stack.
- Aplicaciones móviles.
- Aplicaciones de escritorio.
- IA y agentes.
- Automatización e integraciones.
- Videojuegos y motores.
- Bases de datos.
- Documentación técnica.

El equipo de agentes no debe estar ejecutándose todo el tiempo. M.I.L.O. crea agentes/tareas bajo demanda, con límites de concurrencia y presupuesto.

### 3.6 Calidad y auditoría
- Pruebas unitarias, integración y extremo a extremo.
- Revisión de código.
- Verificación de requisitos.
- Accesibilidad y compatibilidad.
- Rendimiento.
- Análisis de seguridad defensiva.
- Registro de defectos y regresiones.
- Aprobación técnica de entregables basada en evidencias.

El desarrollador no puede aprobar por sí solo su propio trabajo como validado. La verificación debe ejecutar pruebas independientes siempre que sea posible.

### 3.7 Infraestructura y despliegues
- Repositorios y flujos Git.
- Entornos de desarrollo, pruebas y producción.
- Servidores, dominios y certificados.
- Bases de datos y migraciones.
- Secretos y variables de entorno.
- CI/CD, monitorización y logs.
- Preparación de despliegues y rollback.

Desplegar, migrar o cambiar producción requiere autorización explícita.

### 3.8 Operaciones y coordinación
- Descomposición de proyectos en tareas.
- Asignación y dependencias.
- Calendario e hitos.
- Estados, prioridades y bloqueos.
- Coordinación entre departamentos.
- Seguimiento de capacidad y concurrencia.
- Informes operativos.

### 3.9 Administración y costes
- Presupuestos y estimaciones.
- Costes de proveedores, hosting y modelos.
- Consumo de IA por proyecto.
- Registro de gastos y tiempo.
- Margen estimado.
- Comparación estimado/real.
- Informes financieros internos.

M.I.L.O. puede calcular y preparar información; no debe realizar pagos ni asumir compromisos económicos.

### 3.10 Soporte y mantenimiento
- Registro de incidencias.
- Clasificación y prioridad.
- Diagnóstico.
- Propuestas de corrección.
- Seguimiento de versiones.
- Mantenimiento preventivo.
- Comunicación de estado autorizada.
- Historial de soporte por cliente/proyecto.

## 4. Agentes especializados

M.I.L.O. coordina agentes bajo demanda. Roles iniciales:
- Arquitecto de software.
- Analista de requisitos.
- Desarrollador por especialidad.
- Revisor de código.
- Ingeniero de pruebas.
- Especialista de bases de datos.
- Especialista de infraestructura.
- Auditor de seguridad defensiva.
- Redactor de documentación.

Reglas:
- No crear agentes permanentes sin necesidad.
- Cada agente recibe una tarea, contexto mínimo necesario, herramientas permitidas y criterio de aceptación.
- Los agentes no comparten credenciales directamente.
- Los cambios de código deben quedar en ramas/commits identificables.
- Los agentes informan resultados verificables, no autocalificaciones.
- M.I.L.O. resuelve conflictos y consolida resultados.
- Un agente no puede ampliar sus propios permisos.

## 5. Flujo estándar de un proyecto

1. Registrar prospecto/cliente.
2. Registrar solicitud y contexto.
3. Analizar requisitos y dudas.
4. Preparar propuesta, alcance, riesgos y estimación.
5. Obtener aprobación comercial del propietario/cliente según corresponda.
6. Diseñar arquitectura y criterios de aceptación.
7. Crear proyecto, repositorio, hitos y tareas.
8. Desarrollar en entorno aislado.
9. Ejecutar pruebas y revisión independiente.
10. Corregir defectos.
11. Preparar documentación y paquete de entrega.
12. Solicitar aprobación para despliegue/entrega externa cuando aplique.
13. Registrar entrega, versión y aceptación.
14. Pasar a soporte y mantenimiento.

## 6. Base de datos lógica de agencia

Entidades recomendadas para el modelo de datos:
- `clients`: clientes.
- `contacts`: contactos.
- `leads`: oportunidades.
- `communications`: comunicaciones registradas.
- `proposals`: propuestas/cotizaciones.
- `projects`: proyectos.
- `requirements`: requisitos.
- `acceptance_criteria`: criterios de aceptación.
- `repositories`: repositorios.
- `documents`: documentos.
- `milestones`: hitos.
- `tasks`: tareas.
- `assignments`: asignaciones a personas/agentes.
- `agent_runs`: ejecuciones de agentes.
- `test_runs`: ejecuciones de pruebas.
- `incidents`: incidencias.
- `deployments`: despliegues.
- `time_entries`: tiempo registrado.
- `expenses`: gastos.
- `activity_logs`: auditoría.

Todas las entidades deben tener identificadores estables, timestamps, estado y relaciones apropiadas. Los datos deben estar asociados al cliente/proyecto correspondiente y protegidos por controles de acceso.

## 7. Panel MILO AGENCY

Vistas previstas:
- Resumen de agencia.
- Clientes y oportunidades.
- Proyectos activos.
- Tablero de tareas.
- Agentes y ejecuciones.
- Incidencias y bloqueos.
- Calendario e hitos.
- Repositorios y entregas.
- Costes y uso de IA.
- Actividad y auditoría.

El panel debe distinguir estados reales: pendiente, en curso, esperando aprobación, bloqueado, fallido, verificando y completado.

## 8. Comunicación con clientes

La integración de WhatsApp/correo y la gestión directa de conversaciones son una capacidad propuesta para la agencia, pero el canal, proveedor y alcance todavía deben definirse. No asumir que ya existe una cuenta API, número conectado o autorización de envío.

Diseño deseado:
- Recibir solicitudes por canales conectados.
- Asociarlas al cliente correcto.
- Registrar conversaciones y consentimientos necesarios.
- Preparar respuestas y propuestas.
- Enviar automáticamente solo mensajes de bajo riesgo que estén expresamente autorizados.
- Escalar precios, compromisos, quejas, cambios de alcance y asuntos sensibles al propietario.
- Nunca compartir información de un cliente con otro.

## 9. Indicadores de operación

Métricas futuras:
- Proyectos por estado.
- Tareas completadas y bloqueadas.
- Tiempo estimado frente al real.
- Defectos por versión.
- Entregas a tiempo.
- Incidencias abiertas.
- Coste de IA por proyecto.
- Coste de infraestructura.
- Tiempo de respuesta de soporte.

No mostrar métricas inventadas: si falta información, indicar que no está registrada.
