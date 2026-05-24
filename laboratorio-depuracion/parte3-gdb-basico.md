# Parte 3: introducción a gdb

## Compilación con símbolos de depuración

    g++ -g -o gdb_basico codigo/03_gdb_basico.cpp

## Ejecución normal

    ./gdb_basico
    Número: 5
    Doble: 10
    Total: 20

## Uso de gdb

    gdb ./gdb_basico

### Comandos usados y resultados

    (gdb) break main
    Breakpoint 1 at 0x11cb: file codigo/03_gdb_basico.cpp, line 14.

    (gdb) run
    Breakpoint 1, main () at codigo/03_gdb_basico.cpp:14
    14          int numero = 5;

    (gdb) next
    15          int doble = duplicar(numero);

    (gdb) next
    16          int total = sumar(doble, 10);

    (gdb) print numero
    $1 = 5

    (gdb) print doble
    $2 = 10

    (gdb) next
    18          std::cout << "Número: " << numero << std::endl;

    (gdb) print total
    $3 = 20

    (gdb) continue
    Número: 5
    Doble: 10
    Total: 20

## Explicación de comandos

- **-g**: incluye símbolos de depuración para que gdb pueda mostrar nombres de variables y líneas de código.
- **break main**: pone un breakpoint al inicio de la función main, el programa se detiene ahí.
- **run**: inicia la ejecución del programa dentro de gdb.
- **next**: avanza una línea sin entrar dentro de las funciones.
- **print**: muestra el valor actual de una variable.

## Valores observados

- `numero` = 5
- `doble` = 10
- `total` = 20

## Preguntas de reflexión

1. **¿Qué es un breakpoint?** Es un punto de parada que le indica a gdb que detenga la ejecución del programa en una línea o función específica.
2. **¿Diferencia entre ejecutar normal y con gdb?** Ejecutar normal corre el programa completo de una vez. Con gdb podemos pausarlo y ver su estado interno.
3. **¿Ventaja de inspeccionar variables?** Permite verificar que los valores son los esperados en cada momento de la ejecución.
4. **¿Por qué next no entra en las funciones?** Porque next avanza línea por línea en la función actual. Para entrar en una función hay que usar step.
