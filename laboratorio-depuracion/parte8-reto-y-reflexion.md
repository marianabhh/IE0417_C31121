# Parte 8: mini reto de depuración

## Mini reto de depuración

### Resultado inicial

    g++ -g -o reto codigo/10_reto.cpp
    ./reto
    Mayor: 0
    Promedio: -80

### Herramientas usadas
- valgrind
- AddressSanitizer

### Errores encontrados

1. **Acceso fuera de límites**: el ciclo usaba i <= tamano en vez de i < tamano.
2. **Error lógico en obtener_mayor**: int mayor = 0 falla con números negativos, debe ser mayor = datos[0].
3. **Error lógico en calcular_promedio**: retornaba suma en vez de suma/tamano.
4. **Memory leak**: faltaba delete[] datos al final de main.

### Cómo se encontró cada error

- valgrind detectó el Invalid read y el definitely lost.
- AddressSanitizer confirmó el heap-buffer-overflow en línea 7.
- Comparando el resultado esperado con el obtenido se encontraron los errores lógicos.

### Correcciones realizadas

- i <= tamano → i < tamano
- int mayor = 0 → int mayor = datos[0]
- return suma → return (double)suma / tamano
- Se agregó delete[] datos antes del return 0

### Resultado final

    ./reto
    Mayor: -5
    Promedio: -16

    valgrind --leak-check=full ./reto
    All heap blocks were freed -- no leaks are possible
    ERROR SUMMARY: 0 errors from 0 contexts

### Herramienta más útil
valgrind fue la más útil porque detectó tanto el acceso fuera de límites como la pérdida de memoria en una sola ejecución.

---

## Reflexión final

1. **¿Qué entiendo por depuración?** Es el proceso de encontrar y corregir errores en un programa usando herramientas y razonamiento sistemático.
2. **¿Por qué no basta con que compile?** Porque un programa puede compilar perfectamente y aun así tener errores lógicos o de memoria que solo aparecen al ejecutarse.
3. **¿Diferencia entre error de sintaxis y error lógico?** El error de sintaxis lo detecta el compilador. El error lógico el programa lo ejecuta pero produce resultados incorrectos.
4. **¿Ventaja de gdb?** Permite pausar el programa, inspeccionar variables y seguir la ejecución línea por línea.
5. **¿Ventaja de valgrind?** Detecta errores de memoria como pérdidas y accesos inválidos sin necesidad de modificar el código.
6. **¿Ventaja de AddressSanitizer?** Es más rápido que valgrind y da mensajes de error muy claros con número de línea exacto.
7. **¿Qué aprendí sobre errores de memoria?** Que pueden no causar un crash visible pero corrompan datos o desperdicien recursos.
8. **¿Qué aprendí sobre errores de concurrencia?** Que son difíciles de reproducir porque dependen del orden de ejecución de los hilos.
9. **¿Error más fácil de encontrar?** El error de sintaxis, porque el compilador indica exactamente la línea.
10. **¿Error más difícil de entender?** La condición de carrera, porque el programa a veces funciona bien y a veces no.
11. **¿Qué herramienta usaría si el resultado es incorrecto?** gdb para inspeccionar variables y seguir la ejecución.
12. **¿Qué herramienta usaría si hay segmentation fault?** AddressSanitizer o valgrind para encontrar el acceso inválido.
13. **¿Qué herramienta usaría si sospecho pérdida de memoria?** valgrind con --leak-check=full.
14. **¿Qué herramienta usaría si sospecho problema con hilos?** Helgrind o ThreadSanitizer.
15. **¿Cómo aplicaría estas herramientas en proyectos futuros?** Las usaría como parte del proceso de desarrollo, no solo cuando algo falle, para detectar errores temprano.
