# Parte 4: step, next y backtrace

## Compilación

    g++ -g -o gdb_funciones codigo/04_gdb_funciones.cpp

## Ejecución normal (con error)

    ./gdb_funciones
    Floating point exception (core dumped)

## Uso de gdb

### Comandos y resultados

    (gdb) break main
    Breakpoint 1 at 0x11e1: file codigo/04_gdb_funciones.cpp, line 15.

    (gdb) run
    Breakpoint 1, main () at codigo/04_gdb_funciones.cpp:15
    15          int valor = 5;

    (gdb) next
    16          int respuesta = calcular(valor);

    (gdb) step
    calcular (x=5) at codigo/04_gdb_funciones.cpp:9
    9           int divisor = x - 5;

    (gdb) step
    10          int resultado = dividir(100, divisor);

    (gdb) print x
    $1 = 5

    (gdb) print divisor
    $2 = 0

    (gdb) step
    dividir (a=100, b=0) at codigo/04_gdb_funciones.cpp:4
    4           int resultado = a / b;

    (gdb) print a
    $3 = 100

    (gdb) print b
    $4 = 0

    (gdb) backtrace
    #0  dividir (a=100, b=0) at codigo/04_gdb_funciones.cpp:4
    #1  0x00005555555551cd in calcular (x=5) at codigo/04_gdb_funciones.cpp:10
    #2  0x00005555555551f2 in main () at codigo/04_gdb_funciones.cpp:16

## Análisis

GDB mostró que divisor vale 0 porque calcular recibe x=5 y hace 5-5=0.
Luego dividir recibe b=0 y falla al intentar dividir 100/0.

## Diferencia entre next y step

- **next**: avanza una línea sin entrar dentro de las funciones.
- **step**: avanza una línea y entra dentro de las funciones si las hay.

## Resultado de backtrace

Muestra la cadena de llamadas: main llamó a calcular, que llamó a dividir.
Esto permite saber exactamente cómo se llegó al punto donde ocurrió el error.

## Código corregido

    int dividir(int a, int b) {
        if (b == 0) {
            std::cout << "Error: no se puede dividir entre cero." << std::endl;
            return 0;
        }
        int resultado = a / b;
        return resultado;
    }

## Resultado final

    Error: no se puede dividir entre cero.
    Respuesta: 0

## Preguntas de reflexión

1. **¿Diferencia entre next y step?** next no entra en funciones, step sí entra.
2. **¿Para qué sirve backtrace?** Para ver la cadena de funciones que llevaron al punto actual de ejecución.
3. **¿Cuál fue la causa del error?** calcular(5) hace divisor = 5-5 = 0, y luego se intenta dividir entre cero.
4. **¿Por qué es un error de tiempo de ejecución?** Porque el código compila bien pero falla al ejecutarse.
5. **¿Cómo prevenirlo?** Validar que el divisor no sea cero antes de dividir.
