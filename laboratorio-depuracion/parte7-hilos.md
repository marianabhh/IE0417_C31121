# Parte 7: análisis de hilos y condiciones de carrera

## Código con condición de carrera

### Compilación

    g++ -g -pthread -o race_condition codigo/08_race_condition.cpp

### Ejecución varias veces

    ./race_condition
    Contador final: 164563

    ./race_condition
    Contador final: 148333

    ./race_condition
    Contador final: 200000

### Resultado esperado
Siempre 200000 (100000 incrementos por cada hilo).

### Resultado obtenido
Variable cada ejecución. La condición de carrera hace que algunos incrementos se pierdan.

### ThreadSanitizer
ThreadSanitizer no funcionó en WSL2 debido a una limitación conocida:
    FATAL: ThreadSanitizer: unexpected memory mapping

### Reporte de Helgrind

    Possible data race during read of size 4 at contador by thread #3
    Locks held: none
    at incrementar() (08_race_condition.cpp:8)

    Possible data race during write of size 4 at contador by thread #3
    Locks held: none
    at incrementar() (08_race_condition.cpp:8)

    ERROR SUMMARY: 2 errors from 2 contexts

### Qué es una condición de carrera
Es un error que ocurre cuando dos o más hilos acceden a la misma variable compartida al mismo tiempo y al menos uno la modifica, sin ningún mecanismo de sincronización. El resultado depende del orden en que se ejecuten los hilos, que no es predecible.

### Corrección con std::mutex

Se usó std::mutex y std::lock_guard para proteger el acceso a contador.

    g++ -g -pthread -o race_condition_corregido codigo/09_race_condition_corregido.cpp

### Ejecución después de corregir

    ./race_condition_corregido
    Contador final: 200000

    ./race_condition_corregido
    Contador final: 200000

    ./race_condition_corregido
    Contador final: 200000

### Helgrind después de corregir

    ERROR SUMMARY: 0 errors from 0 contexts

## Preguntas de reflexión

1. **¿Por qué contador++ no es seguro entre hilos?** Porque es una operación de tres pasos: leer, incrementar y escribir. Dos hilos pueden leer el mismo valor antes de que alguno escriba.
2. **¿Qué significa que dos hilos accedan a la misma variable?** Que ambos pueden leer y modificar el mismo espacio de memoria simultáneamente, causando resultados impredecibles.
3. **¿Qué resuelve std::mutex?** Garantiza que solo un hilo pueda acceder a la sección crítica a la vez.
4. **¿Qué hace std::lock_guard?** Bloquea el mutex al crearse y lo libera automáticamente al salir del scope.
5. **¿Por qué los errores de concurrencia son difíciles de reproducir?** Porque dependen del orden de ejecución de los hilos, que varía en cada corrida.
6. **¿Cuál herramienta fue más clara?** Helgrind, porque indicó exactamente la línea y variable con la condición de carrera.
