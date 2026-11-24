# Especificación de experiencia e interfaz — M.I.L.O.

**Estado:** decisión principal confirmada el 24-11-2026; detalles de interacción pendientes de definición.
**Propósito:** evitar que M.I.L.O. termine como un chatbot convencional rodeado de un dashboard genérico.

## 1. Decisión confirmada: interfaz adaptativa

La pantalla principal de M.I.L.O. será **adaptive**: la interfaz se transformará según la tarea, el contexto y el estado de trabajo actual.

El propietario lo definió así: «Quiero que la interfaz se transforme según lo que esté haciendo, sin menús permanentes como protagonista».

Esto significa:
- No usar una barra lateral fija, un conjunto de pestañas o un menú permanente como elemento principal de la experiencia.
- No presentar siempre el mismo dashboard independientemente de la tarea.
- Mostrar de forma contextual los paneles, herramientas, controles, información y resultados que sean relevantes para la actividad actual.
- Mantener una forma clara y consistente de conversar con M.I.L.O. y de acceder a controles esenciales.
- Permitir que la interfaz cambie de composición sin perder el contexto, el estado de las tareas ni la orientación del usuario.

## 2. Comportamiento esperado

Ejemplos conceptuales —no son diseños finales ni autorizan todavía una implementación específica—:

- **Conversación:** priorizar el intercambio por voz o texto y el contexto necesario.
- **Desarrollo de software:** dar espacio al proyecto, archivos, cambios, pruebas, terminal controlada y estado de ejecución cuando esas funciones existan.
- **Análisis de documentos:** priorizar el documento, sus hallazgos y las acciones disponibles.
- **MILO AGENCY:** mostrar el cliente, proyecto, tareas, hitos y actividad pertinentes, respetando permisos y separación de datos.
- **Control del PC:** mostrar la aplicación o pantalla observada, las acciones propuestas y los controles de autorización.
- **Tarea en segundo plano:** mostrar progreso real, etapa actual, bloqueos, resultados y controles para pausar o cancelar.

La interfaz no debe mostrar paneles irrelevantes solo para llenar espacio.

## 3. Estructura y navegación

- La experiencia principal será contextual y dinámica.
- Puede existir una estructura base mínima para identidad, conversación y controles esenciales, pero no debe dominar la pantalla.
- Las funciones secundarias podrán aparecer como paneles, ventanas o espacios de trabajo según la necesidad.
- El usuario debe poder comprender dónde está, qué tarea está activa y cómo volver al espacio anterior.
- Los cambios de vista deben preservar el estado de trabajo y evitar perder información.
- Los modos minimalista y HUD futurista definidos en la especificación maestra deberán respetar el mismo principio adaptativo.

## 4. Requisitos funcionales obligatorios

1. **Contexto real:** la composición de la interfaz debe depender del estado real de la aplicación y de las tareas, no de datos inventados.
2. **Controles operativos:** los botones y controles visibles deben ejecutar acciones reales o indicar claramente que todavía no están disponibles.
3. **Estado verificable:** diferenciar tareas pendientes, en ejecución, pausadas, completadas y fallidas.
4. **Control del usuario:** ofrecer pausa, cancelación y autorización cuando corresponda.
5. **Continuidad:** cambiar de espacio o modo no debe borrar conversaciones, progreso ni datos de trabajo.
6. **Permisos:** no mostrar una acción como ejecutable si el usuario o el agente no tienen autorización.
7. **Errores:** explicar errores y ofrecer una salida útil; no ocultarlos detrás de animaciones.
8. **Adaptabilidad:** funcionar en los tamaños de ventana previstos para el escritorio y permitir reorganizar contenido sin perder controles esenciales.
9. **Accesibilidad:** mantener legibilidad, contraste, navegación por teclado y estados comprensibles.
10. **Rendimiento:** las transiciones y elementos visuales no deben bloquear las tareas ni consumir recursos desproporcionados.

## 5. Restricciones de diseño

- Prohibido entregar como resultado principal una plantilla genérica de administración con sidebar permanente, tarjetas repetidas y gráficas decorativas.
- Prohibido crear paneles que solo parezcan interactivos.
- Prohibido usar cifras, actividad, proyectos o estados ficticios para aparentar que el sistema está funcionando.
- No añadir animaciones, hologramas o efectos por decoración si no comunican estado o permiten una interacción útil.
- No sacrificar claridad, velocidad, estabilidad o accesibilidad para conseguir una apariencia futurista.
- No confundir «adaptativa» con una interfaz desordenada o impredecible.

## 6. Criterios de aceptación para la futura interfaz

La interfaz no podrá considerarse aceptada hasta demostrar que:

- Al menos tres tipos de tareas diferentes producen espacios de trabajo contextuales claramente distintos.
- Los cambios de contexto conservan la tarea y los datos asociados.
- Los controles principales están conectados a operaciones reales del backend.
- Los estados mostrados coinciden con el estado real de las tareas.
- Las tareas largas permiten consultar progreso y, cuando esté implementado, pausarse o cancelarse.
- No existen datos ficticios ni controles decorativos presentados como funcionales.
- Se puede usar la interfaz en modo minimalista y HUD sin romper el comportamiento adaptativo.
- Se han probado los flujos principales, errores, permisos, accesibilidad básica y tamaños de ventana.

## 7. Pendiente de definición

Esta decisión establece el principio de diseño, pero no define todavía:
- La composición exacta de la pantalla inicial.
- La ubicación y comportamiento de la conversación por voz y texto.
- Cómo se crean, apilan, cierran y recuperan los espacios de trabajo.
- Qué controles permanecen siempre accesibles.
- Las transiciones, animaciones y reglas visuales del HUD.
- La diferencia visual detallada entre MILO PERSONAL y MILO AGENCY.
- Los flujos de teclado, mouse, gestos y pantallas pequeñas.

No inventar estas decisiones. Resolverlas en el análisis de experiencia antes de implementar la interfaz.

## 8. Instrucción para agentes de desarrollo

Leer este documento antes de diseñar o implementar cualquier interfaz de M.I.L.O. La decisión adaptativa es un requisito confirmado del propietario. Si una solución técnica obliga a comprometerlo, explicar la limitación y proponer alternativas antes de cambiar el diseño.
