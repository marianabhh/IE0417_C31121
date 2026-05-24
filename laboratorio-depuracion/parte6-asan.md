# Parte 6: AddressSanitizer

## Código base: use after free

### Comando de compilación normal

    g++ -g -o use_after_free codigo/07_use_after_free.cpp

### Ejecución sin sanitizer

    ./use_after_free
    Número: 2000161699

El programa imprimió basura porque la memoria ya había sido liberada.

### Compilación con AddressSanitizer

    g++ -g -fsanitize=address -o use_after_free_asan codigo/07_use_after_free.cpp

### Reporte de AddressSanitizer

    ERROR: AddressSanitizer: heap-use-after-free on address 0x502000000010
    READ of size 4 at codigo/07_use_after_free.cpp:9
    freed by thread T0 here: codigo/07_use_after_free.cpp:7

### Qué significa heap-use-after-free
Significa que el programa intentó leer memoria que ya fue liberada con delete. Es un error grave porque esa memoria puede haber sido reasignada a otro uso.

### Línea del error
Línea 9: se usó *numero después de haberlo liberado en la línea 7.

### Corrección
Se movió el cout antes del delete y se asignó nullptr al puntero después de liberar.

### Resultado final

    ./use_after_free_asan
    Número: 42

### Preguntas de reflexión

1. **¿Qué significa usar memoria después de liberarla?** Acceder a una dirección de memoria que ya fue devuelta al sistema, lo que produce resultados impredecibles.
2. **¿Por qué es difícil de detectar sin herramientas?** Porque a veces el programa parece funcionar aunque el valor sea basura.
3. **¿Ventaja de AddressSanitizer?** Detecta el error exacto con número de línea, sin necesidad de ejecutar valgrind por separado.
4. **¿Diferencia con valgrind?** AddressSanitizer se compila junto al programa y es más rápido. Valgrind analiza el ejecutable sin recompilarlo.
5. **¿Por qué asignar nullptr después de delete?** Para evitar que el puntero quede apuntando a memoria inválida y cause errores si se usa accidentalmente.
