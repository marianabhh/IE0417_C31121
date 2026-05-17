# Análisis de resultados

## Parte 1: Creación básica de hilos

### Resultados observados
Los mensajes no aparecen siempre en el mismo orden. En algunas ejecuciones
los mensajes se mezclaron en la misma línea, como "Hola desde el hilo Hola desde el hilo 4".

### Preguntas

1. ¿Los mensajes aparecen siempre en el mismo orden?
No, el orden varía entre ejecuciones. 

2. ¿Por qué podría cambiar el orden de impresión?
Porque el sistema operativo decide cuándo ejecutar cada hilo y no hay garantía de orden. Cada hilo compite por el CPU de forma independiente.

3. ¿Qué función cumple join()?
Hace que el hilo principal espere a que cada hilo termine antes de continuar.

4. ¿Qué podría pasar si no se llama a join()?
El objeto std::thread se destruiría al final del scope estando aún activo. En C++, si un hilo destructible sigue siendo joinable, el entorno de ejecución invoca automáticamente a std::terminate(), lo que provoca que el programa aborte y falle críticamente (un crash) en lugar de simplemente dejar que los hilos terminen de fondo.


## Parte 2: Condición de carrera

### Resultados observados

| Ejecución | Valor esperado | Valor obtenido |
|-----------|---------------|----------------|
| 1         | 4000000       | 1129292        |
| 2         | 4000000       | 1025870        |
| 3         | 4000000       | 1022841        |
| 4         | 4000000       | 1035607        |
| 5         | 4000000       | 1020336        |

### Preguntas

1. ¿El valor obtenido siempre coincide con el valor esperado?
No, en ninguna ejecución coincidió. El resultado quedó drásticamente por debajo del esperado, rondando apenas la cuarta parte del total real.

2. ¿Por qué se pierden incrementos?
Porque múltiples hilos acceden simultáneamente a la misma dirección de memoria. Sin sincronización, varios hilos leen el mismo valor base, incrementan por separado en sus registros y luego escriben el resultado, pisando de forma destructiva el trabajo de los demás hilos.

3. ¿La operación contador++ es realmente una sola operación a nivel de CPU?
No, a nivel de ensamblador no es atómica. El procesador la divide en tres pasos:
- Load: copia el valor de contador desde RAM a un registro del CPU.
- Increment: le suma 1 al valor en ese registro.
- Store: copia el nuevo valor de vuelta a RAM.
Si el planificador interrumpe un hilo en medio de este ciclo, los demás trabajarán con un valor desactualizado, perdiéndose incrementos.

4. ¿Qué problema de concurrencia se está observando?
Una condición de carrera (race condition). Ocurre porque los hilos modifican concurrentemente una sección crítica sin exclusión mutua que garantice la atomicidad de la operación.


## Parte 3: Corrección usando mutex

### Resultados observados
En las 5 ejecuciones el valor obtenido siempre fue 4000000, coincidiendo
exactamente con el valor esperado.

### Preguntas

1. ¿Qué cambió con respecto al programa anterior?
Se agregó un std::mutex y se protege cada incremento con std::lock_guard, garantizando que solo un hilo a la vez pueda modificar el contador.

2. ¿Qué hace std::mutex?
Es un mecanismo de exclusión mutua. Permite que solo un hilo acceda a la sección crítica a la vez. Los demás hilos quedan bloqueados esperando hasta que el mutex sea liberado.

3. ¿Qué hace std::lock_guard?
Es un wrapper RAII que adquiere el mutex al crearse y lo libera automáticamente al salir del scope, evitando olvidar llamar a unlock().

4. ¿Por qué ahora el resultado sí debería ser correcto?
Porque el mutex garantiza que el ciclo load-increment-store de contador++ se ejecuta de forma atómica desde la perspectiva de los demás hilos. Solo un hilo puede estar en esa sección crítica a la vez.

5. ¿Qué desventaja podría tener proteger cada incremento individual con un mutex?
Genera mucha contención. Los hilos pasan más tiempo esperando el mutex que haciendo trabajo real, lo que puede hacer la versión con mutex más lenta que la secuencial.


## Parte 4: Mini benchmark secuencial vs paralelo

### Resultados observados

| Ejecución | Tiempo secuencial | Tiempo paralelo | ¿Cuál fue más rápido? |
|-----------|------------------|-----------------|----------------------|
| 1         | 26 ms            | 9 ms            | Paralelo             |
| 2         | 28 ms            | 10 ms           | Paralelo             |
| 3         | 27 ms            | 10 ms           | Paralelo             |

### Preguntas

1. ¿El resultado secuencial y el paralelo son iguales?
Sí, ambos dieron 100000000, lo que confirma que la paralelización no afecta la correctitud del resultado.

2. ¿La versión paralela siempre fue más rápida?
Sí, en las tres ejecuciones fue aproximadamente 3 veces más rápida.

3. ¿Por qué dividir el vector en bloques permite paralelizar el trabajo?
Porque cada hilo trabaja sobre una porción independiente del vector, sin necesidad de sincronización. No hay datos compartidos entre hilos durante el cálculo parcial.

4. ¿Qué costos adicionales tiene la versión paralela?
La creación y destrucción de hilos, la sincronización con join(), y la suma final de resultados parciales.

5. ¿Qué podría pasar si el vector fuera muy pequeño?
La versión paralela podría ser más lenta que la secuencial porque el costo de crear los hilos superaría el beneficio de dividir el trabajo.


## Parte 5: Cantidad de hilos vs rendimiento

### Resultados observados

| Cantidad de hilos | Tiempo obtenido |
|-------------------|-----------------|
| 1                 | 76 ms           |
| 2                 | 24 ms           |
| 4                 | 14 ms           |
| 8                 | 11 ms           |
| 16                | 12 ms           |

### Conclusión
La mejora de rendimiento no es lineal al aumentar los hilos. La mayor ganancia
ocurrió de 1 a 4 hilos. De 8 a 16 hilos el tiempo incluso empeoró levemente,
lo que indica que el overhead de administrar más hilos supera el beneficio.

### Preguntas

1. ¿Cuál cantidad de hilos produjo el mejor tiempo?
8 hilos con 11 ms.

2. ¿El tiempo mejoró siempre al aumentar los hilos?
No, de 8 a 16 hilos el tiempo aumentó de 11 ms a 12 ms.

3. ¿Cuántos núcleos tiene la computadora donde se ejecutó el programa?
16 núcleos según el comando nproc.

4. ¿Qué ocurre cuando se usan más hilos que núcleos disponibles?
El sistema operativo debe hacer context switching, alternando la ejecución entre hilos en el mismo núcleo, lo que agrega overhead y puede empeorar el rendimiento.

5. ¿Qué relación tiene esto con el context switching?
Con 16 hilos y 16 núcleos teóricamente no debería haber context switching, pero el sistema operativo también tiene otros procesos corriendo, lo que genera competencia por los núcleos disponibles.

6. ¿Por qué la versión con 16 hilos podría no ser la mejor?
Porque el overhead de crear, administrar y sincronizar 16 hilos puede superar la ganancia de paralelismo, especialmente cuando el trabajo por hilo es relativamente pequeño.


## Parte 6: Deadlock

### Preguntas

1. ¿El programa termina normalmente?
No, el programa se bloqueó indefinidamente y fue necesario detenerlo con Ctrl+C.

2. ¿Qué recurso tomó primero el hilo A?
El recurso 1.

3. ¿Qué recurso tomó primero el hilo B?
El recurso 2.

4. ¿Por qué ninguno de los dos hilos puede continuar?
Porque el hilo A tiene el recurso 1 y espera el recurso 2, mientras que el hilo B tiene el recurso 2 y espera el recurso 1. Ninguno puede avanzar porque el recurso que necesita está bloqueado por el otro.

5. ¿Qué significa espera circular?
Es cuando dos o más hilos forman un ciclo de dependencias donde cada uno espera un recurso que tiene el siguiente. En este caso: A espera a B y B espera a A.

6. ¿Cómo se podría evitar este problema?
Adquiriendo siempre los mutex en el mismo orden en todos los hilos, o usando std::scoped_lock que adquiere múltiples mutex de forma atómica sin riesgo de deadlock.

### Pregunta final
¿Por qué std::scoped_lock ayuda a evitar este deadlock?
std::scoped_lock adquiere todos los mutex que se le pasan de forma atómica, usando un algoritmo que evita la espera circular. Si no puede tomar todos al mismo tiempo, no toma ninguno, evitando así que un hilo quede con un recurso a medias esperando el otro.


## Parte 7: Reflexión final

1. ¿Cuál fue la diferencia más clara que observó entre ejecución secuencial y ejecución con hilos?
Con hilos el orden de ejecución es no determinista y los mensajes pueden mezclarse, mientras que la ejecución secuencial es predecible y ordenada. Además, con hilos se puede aprovechar mejor el hardware para tareas pesadas.

2. ¿Qué es una condición de carrera?
Es un error que ocurre cuando dos o más hilos acceden simultáneamente a un recurso compartido sin sincronización, y el resultado depende del orden impredecible en que se ejecutan.

3. ¿Por qué contador++ puede fallar cuando muchos hilos lo ejecutan al mismo tiempo?
Porque no es una operación atómica. Se divide en leer, incrementar y escribir, y otro hilo puede interrumpir ese proceso y trabajar con un valor desactualizado, causando que se pierdan incrementos.

4. ¿Qué problema resuelve un mutex?
Garantiza exclusión mutua, permitiendo que solo un hilo a la vez acceda a una sección crítica, evitando condiciones de carrera.

5. ¿Qué ventaja tiene std::lock_guard sobre llamar manualmente a lock() y unlock()?
lock_guard libera el mutex automáticamente al salir del scope, incluso si ocurre una excepción. Con lock/unlock manual se corre el riesgo de olvidar el unlock o de que una excepción lo impida, dejando el mutex bloqueado forever.

6. ¿Por qué más hilos no siempre significan mejor rendimiento?
Porque crear y administrar hilos tiene un costo, y cuando hay más hilos que trabajo real que paralelizar, el overhead supera la ganancia. También el context switching entre hilos consume tiempo del CPU.

7. ¿Qué es un deadlock?
Es una situación donde dos o más hilos quedan bloqueados indefinidamente esperando recursos que están siendo retenidos por los otros hilos, formando una espera circular de la que ninguno puede salir.

8. ¿Qué buenas prácticas aplicaría al programar con hilos?
- Usar lock_guard o scoped_lock en lugar de lock/unlock manual.
- Minimizar el tamaño de las secciones críticas.
- Adquirir siempre los mutex en el mismo orden.
- No crear más hilos de los necesarios.
- Preferir variables locales sobre variables globales compartidas.

9. ¿En qué tipo de programas reales podría ser útil la programación concurrente?
En servidores web que atienden múltiples clientes simultáneamente, aplicaciones con interfaces gráficas que deben responder al usuario mientras procesan datos en segundo plano, y sistemas de bases de datos.

10. ¿En qué tipo de programas reales podría ser útil la programación paralela?
En procesamiento de imágenes y video, simulaciones científicas, entrenamiento de modelos de machine learning, renderizado 3D y análisis de grandes volúmenes de datos donde el trabajo puede dividirse en partes independientes.
