# Instrucciones para agentes de IA y desarrolladores

Estas instrucciones aplican a Codex, Claude Code, ChatGPT, otros agentes y colaboradores humanos que trabajen en este repositorio.

## Antes de trabajar

Lee obligatoriamente:
1. `README.md`
2. `docs/MASTER_SPEC.md`
3. `docs/UX_SPEC.md`
4. `docs/ARCHITECTURE.md`
5. `docs/AGENCY.md`
6. `docs/ROADMAP.md`

No empieces a programar basándote únicamente en el último mensaje del chat. Estos documentos son el contexto persistente del proyecto.

## Cómo interpretar la documentación

- **Confirmado:** decisión explícita del propietario.
- **Propuesto:** recomendación técnica pendiente de validación.
- **Pendiente:** falta información o una decisión.
- No conviertas una propuesta en una decisión confirmada.
- Si encuentras contradicciones, detente y documéntalas; no elijas silenciosamente.
- La visión del propietario tiene prioridad sobre preferencias personales del agente, siempre que no contradiga requisitos de seguridad o limitaciones técnicas reales.

## Reglas de desarrollo

1. No intentes construir todo M.I.L.O. en una sola tarea.
2. Implementa exclusivamente el alcance aprobado de la fase actual.
3. No crees clases, carpetas, endpoints ni agentes vacíos para aparentar progreso.
4. No simules capacidades reales con respuestas hardcodeadas.
5. No afirmes que un archivo fue creado/modificado si no verificaste su existencia y contenido.
6. No afirmes que un programa funciona si no lo ejecutaste o probaste.
7. Escribe pruebas para la lógica nueva y ejecuta las pruebas relevantes.
8. Maneja errores, timeouts, cancelación y estados parciales.
9. Mantén proveedores de IA intercambiables.
10. No acoples el núcleo a un único modelo.
11. No guardes secretos en código, documentación, prompts, fixtures o logs.
12. No ejecutes comandos arbitrarios generados por el modelo.
13. No despliegues, borres datos ni modifiques producción sin aprobación explícita.
14. Respeta separación de datos entre clientes y proyectos.
15. Mantén cambios pequeños, revisables y documentados.

## Requisitos obligatorios de interfaz

- La interfaz principal de M.I.L.O. es **adaptativa**: debe transformarse según la tarea y el contexto.
- No entregar un dashboard genérico con sidebar o menús permanentes como protagonista.
- No usar siempre la misma composición para todas las actividades.
- Mostrar paneles, herramientas y controles contextuales; conservar una estructura mínima solo cuando sea útil.
- No crear datos ficticios, actividad simulada ni controles que aparenten ser funcionales.
- Todo control presentado como funcional debe conectarse a una operación real o indicar claramente que está pendiente/no disponible.
- Preservar el estado de tareas y el contexto al cambiar de espacio.
- Mostrar estados reales y permitir pausa/cancelación cuando esas capacidades estén implementadas.
- Respetar los modos minimalista y HUD sin convertir los efectos visuales en prioridad.
- Leer y cumplir `docs/UX_SPEC.md`. Los detalles visuales todavía pendientes no deben inventarse como decisiones del propietario.

## Protocolo de trabajo por tarea

Antes de implementar:
- Explica el objetivo en una frase.
- Enumera los archivos que planeas crear/modificar.
- Identifica dependencias y riesgos.
- Define cómo se probará.
- Confirma que el alcance coincide con la hoja de ruta.

Durante la implementación:
- Mantén el código modular y tipado cuando sea práctico.
- Valida entradas externas.
- Aplica permisos antes de ejecutar herramientas.
- Evita operaciones destructivas.
- Registra resultados sin filtrar secretos.

Al terminar:
- Resume los cambios concretos.
- Enumera pruebas ejecutadas y su resultado.
- Distingue pruebas no ejecutadas de pruebas fallidas.
- Indica limitaciones y riesgos conocidos.
- Actualiza documentación si cambió una decisión o contrato.
- No marques una capacidad como terminada sin evidencia.

## Formato del informe final

### Implementado
- ...

### Archivos modificados
- ...

### Pruebas ejecutadas
- ...

### Pruebas pendientes
- ...

### Riesgos o limitaciones
- ...

### Siguiente paso recomendado
- ...

## Regla principal

M.I.L.O. se construye con capacidades reales y verificadas. No optimices para impresionar en una demostración; optimiza para que el sistema funcione de forma estable, segura y mantenible.
