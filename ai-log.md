# Bitácora de IA

Esta bitácora registra cómo trabajaste con el agente durante el laboratorio: qué le pediste, qué propuso, qué decidiste y cómo lo comprobaste. No se evalúa cuánto código escribió la IA, sino tu criterio: por qué aceptaste, rechazaste o ajustaste cada propuesta.

## Entrada 1

- **Fecha:** 2026-11-21 11:50
- **Paso del laboratorio:** memoria del proyecto (`AGENTS.md`)
- **Prompt clave (literal):**
  > Create or update `AGENTS.md` for this repository.
- **Qué propuso el agente:** un `AGENTS.md` compacto en español con comandos (`python -m pytest`, `python servidor.py`), reglas (no tocar `servidor.py` ni `almacen.py`, solo biblioteca estándar, mensajes de error exactos, nunca cambiar un test para que pase), flujo TDD, contratos de retorno y convenciones de tests.
- **Decisión:** aceptado. Se mantuvieron solo los datos que el agente no puede deducir leyendo el código; se descartaron descripciones archivo por archivo y consejos genéricos.
- **Cómo lo verifiqué:** leí el archivo completo y confirmé que los comandos que menciona existen en `README.md`.

## Entrada 2

- **Fecha:** 2026-11-21 12:05
- **Paso del laboratorio:** plan
- **Prompt clave (literal):**
  > Vamos a implementar los tests de las funciones completar, eliminar y editar ... se realizará en el orden indicado ... antes de implementar los test de la siguiente función pedir mi aprobación.
- **Qué propuso el agente:** plan TDD función por función (`completar` → `eliminar` → `editar`), un test por cada regla del docstring, correr `python -m pytest`, pedir aprobación antes de la siguiente función y registrar cada paso en `ai-log.md`.
- **Decisión:** ajustado. Se aclaró que "guardar" significa reescribir `ai-log.md` según el avance, que en `AGENTS.md` se agregan las reglas de flujo resumidas y que la decisión se pide en cada aprobación. Luego se aprobó empezar por `completar`.
- **Cómo lo verifiqué:** revisé que cada test propuesto correspondiera a una regla del docstring y que el plan no tocara `servidor.py`, `almacen.py` ni agregara dependencias.

## Entrada 3

- **Fecha:** 2026-11-21 12:10
- **Paso del laboratorio:** RED de `completar`
- **Prompt clave (literal):**
  > Paso de laboratorio RED de completar , implementemos los test de completar
- **Qué propuso el agente:** tres tests en `test_tareas.py`: `test_completar_marca_la_tarea_y_la_devuelve`, `test_completar_tarea_inexistente_da_error` (mensaje `"No existe la tarea 7"` y lista intacta) y `test_completar_una_tarea_ya_hecha_no_da_error`.
- **Decisión:** aceptado. Cubren las dos reglas del docstring y el contrato de modificar la lista en sitio y devolver la tarea.
- **Cómo lo verifiqué:** `python -m pytest` da `3 failed, 8 passed`; los tres tests nuevos fallan con `NotImplementedError` (RED) y los de `agregar` siguen en verde.

## Entrada 4

- **Fecha:** 2026-11-21 12:17
- **Paso del laboratorio:** GREEN de `completar`
- **Prompt clave (literal):**
  > ajustemos el flujo. implementemos ahora la función en @tareas.py sin modificar los test ya aprobados. Posteriormente correr todos los test y pedir mi aprobación para pasar a los siguientes funcion. el flujo se repetirá en las siguientes tareas, implementar test -> correr -> verifico -> apruebo -> implementamos la funcion -> apruebo y continuamos.
- **Qué propuso el agente:** implementar `completar` recorriendo la lista, poniendo `hecha = True` en la tarea con ese id, devolviéndola; si no existe, `ValueError(f"No existe la tarea {id_tarea}")`. Sin tocar los tests.
- **Decisión:** aceptado. Es la implementación mínima que cumple las dos reglas del docstring y el contrato de devolver la tarea.
- **Cómo lo verifiqué:** `python -m pytest` da `11 passed` (8 de `agregar` + 3 de `completar`), sin modificar ningún test.

## Entrada 5

- **Fecha:** 2026-11-21 12:21
- **Paso del laboratorio:** RED de `eliminar`
- **Prompt clave (literal):**
  > corre todos los test antes de pasar a la siguiente etapa y crea otro registro en @ai-log.md
- **Qué propuso el agente:** tres tests en `test_tareas.py`: `test_eliminar_quita_la_tarea_y_la_devuelve`, `test_eliminar_tarea_inexistente_da_error` (mensaje `"No existe la tarea 7"` y lista intacta) y `test_eliminar_no_cambia_los_ids_de_las_demas`.
- **Decisión:** aceptado. Cubren las dos reglas del docstring y el contrato de quitar y devolver la tarea. No se implementa `eliminar` todavía: se detuvo el paso aquí.
- **Cómo lo verifiqué:** `python -m pytest` da `3 failed, 11 passed`; los tres tests nuevos fallan con `NotImplementedError` (RED) y los anteriores siguen en verde.

## Entrada 6

- **Fecha:** 2026-11-21 12:25
- **Paso del laboratorio:** GREEN de `eliminar`
- **Prompt clave (literal):**
  > sigamos con la implementación de eliminar
- **Qué propuso el agente:** implementar `eliminar` recorriendo la lista, quitando con `pop` la tarea con ese id y devolviéndola; si no existe, `ValueError(f"No existe la tarea {id_tarea}")`. Sin tocar los tests.
- **Decisión:** ajustado. La implementación se acepta, pero se agrega al flujo hacer un commit después de cada implementación de función (por eso hay un commit para `completar` y otro para `eliminar`).
- **Cómo lo verifiqué:** `python -m pytest` da `14 passed` (8 de `agregar` + 3 de `completar` + 3 de `eliminar`), sin modificar ningún test.
