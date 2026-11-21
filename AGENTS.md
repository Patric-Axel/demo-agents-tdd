# AGENTS.md

Gestor de tareas (laboratorio). Python 3.10+ con pytest.

## Comandos

- `python -m pytest` — todos los tests.
- `python -m pytest test_tareas.py::test_<nombre>` — un test suelto.
- `python servidor.py [puerto]` — vista web en http://127.0.0.1:8000 (usa `8001` si el puerto está ocupado).
- El servidor recarga `tareas.py` en cada petición: basta F5, no lo reinicies.

## Reglas

- No modifiques `servidor.py` ni `almacen.py`.
- Solo biblioteca estándar; `pytest` únicamente para los tests. No agregues dependencias.
- Los mensajes de error deben ser exactamente los de los docstrings de `tareas.py`: los tests los comparan.
- Nunca cambies un test para que pase.

## Flujo de trabajo

- TDD, una función a la vez: tests que fallan (RED), implementación (GREEN), commit por función.
- Al escribir solo tests, seguir el orden `completar` → `eliminar` → `editar`, con un test por cada regla del docstring.
- Correr `python -m pytest` tras cada función y confirmar el fallo esperado (`NotImplementedError`) antes de seguir.
- Pedir aprobación del usuario antes de escribir los tests de la siguiente función.
- Hacer un commit después de implementar cada función (tests e implementación juntos).
- Reescribir `ai-log.md` en cada paso con fecha y hora, paso, prompt clave, propuesta, decisión y verificación.
- `agregar` ya funciona y es el modelo; `completar`, `eliminar` y `editar` lanzan `NotImplementedError`.
- `editar` comparte las reglas de título de `agregar`: extrae la validación a una sola función (paso REFACTOR).
- Actualiza `ai-log.md` con una entrada por cada paso del laboratorio.

## Contratos

- Cada función de `tareas.py` modifica la lista en sitio y devuelve la tarea afectada (dict).
- `servidor.py:143` exige que la función devuelva un dict con `"id"`; si no, avisa "no devolvió la tarea".
- `tareas.json` está en `.gitignore` y se crea con 3 tareas de ejemplo al arrancar el servidor: no lo commitees.

## Tests

- Un test por cada regla del docstring, con nombres en español `test_<funcion>_...` y el mismo estilo que los de `agregar` en `test_tareas.py`.
