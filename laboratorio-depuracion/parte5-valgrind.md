# Parte 5: análisis de memoria con valgrind

## Ejercicio 1: pérdida de memoria

### Qué hace el programa
Crea un arreglo dinámico de 10 enteros, asigna valores y muestra el primero, pero nunca libera la memoria.

### Comando de compilación

    g++ -g -o memory_leak codigo/05_memory_leak.cpp

### Ejecución normal

    ./memory_leak
    Primer elemento: 0

### Reporte de valgrind (antes de corregir)

    definitely lost: 40 bytes in 1 blocks
    at crear_arreglo() (05_memory_leak.cpp:4)
    ERROR SUMMARY: 1 errors from 1 contexts

### Qué significa "definitely lost"
Significa que el programa terminó y hay memoria que fue reservada con new pero nunca liberada con delete. Esa memoria ya no es accesible y nunca será recuperada.

### Corrección

Se agregó delete[] datos; al final de la función crear_arreglo().

### Reporte de valgrind (después de corregir)

    All heap blocks were freed -- no leaks are possible
    ERROR SUMMARY: 0 errors from 0 contexts

### Preguntas de reflexión

1. **¿Qué es una pérdida de memoria?** Es cuando el programa reserva memoria dinámica y nunca la libera.
2. **¿Por qué el programa termina bien aunque tenga pérdida?** Porque el OS recupera la memoria al terminar el proceso, pero en programas largos esto causa problemas.
3. **¿Qué significa liberar memoria dinámica?** Devolver al sistema la memoria reservada con new usando delete.
4. **¿Por qué delete[] y no delete?** Porque se reservó un arreglo con new[], y delete[] libera todos los elementos.
5. **¿Qué problemas causa en programas grandes?** El programa consume cada vez más memoria hasta agotar los recursos del sistema.

---

## Ejercicio 2: acceso fuera de límites

### Comando de compilación

    g++ -g -o invalid_access codigo/06_invalid_access.cpp

### Ejecución normal

    ./invalid_access
    Programa finalizado

### Reporte de valgrind (antes de corregir)

    Invalid write of size 4
    at main (06_invalid_access.cpp:7)
    Address 0x4e1f094 is 0 bytes after a block of size 20 alloc'd
    ERROR SUMMARY: 1 errors from 1 contexts

### Qué significa "Invalid write"
Significa que el programa intentó escribir en una dirección de memoria fuera del arreglo reservado.

### Línea del problema
Línea 7: el ciclo usaba i <= 5 en vez de i < 5, accediendo a arreglo[5] que no existe.

### Corrección

    for (int i = 0; i < 5; i++)

### Reporte de valgrind (después de corregir)

    All heap blocks were freed -- no leaks are possible
    ERROR SUMMARY: 0 errors from 0 contexts

### Preguntas de reflexión

1. **¿Por qué el programa no falló?** Porque accedió a memoria adyacente que en ese momento no causó un crash, pero es comportamiento indefinido.
2. **¿Qué significa escribir fuera de límites?** Modificar memoria que no pertenece al arreglo, pudiendo corromper otros datos.
3. **¿Por qué es peligroso?** Puede corromper datos, causar crashes inesperados o crear vulnerabilidades de seguridad.
4. **¿Diferencia entre error visible y comportamiento indefinido?** Un error visible falla siempre. El comportamiento indefinido puede fallar o no dependiendo del sistema.
