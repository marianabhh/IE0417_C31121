# Parte 2: tipos de errores

## Ejercicio 1: error de sintaxis

### Código original

    #include <iostream>

    int main() {
        std::cout << "Hola mundo" << std::endl
        return 0;
    }

### Comando de compilación

    g++ -g -o error_sintaxis codigo/01_error_sintaxis.cpp

### Error observado

    codigo/01_error_sintaxis.cpp: In function 'int main()':
    codigo/01_error_sintaxis.cpp:4:43: error: expected ';' before 'return'
        4 |     std::cout << "Hola mundo" << std::endl
          |                                           ^
          |                                           ;
        5 |     return 0;
          |     ~~~~~~

### Causa del error

Faltaba un punto y coma al final de la línea 4, después de std::endl.

### Código corregido

    std::cout << "Hola mundo" << std::endl;

### Resultado final

    Hola mundo

### Reflexión

1. **¿Este error fue detectado antes o durante la ejecución?** Antes, en tiempo de compilación.
2. **¿Qué herramienta detectó el error?** El compilador g++.
3. **¿Por qué este error es más fácil de corregir que uno lógico?** Porque el compilador indica exactamente la línea y el problema, no hay que buscar nada.


## Ejercicio 2: error lógico

### Código original

    double calcular_promedio(const std::vector<int>& notas) {
        int suma = 0;
        for (int nota : notas) {
            suma += nota;
        }
        return suma;
    }

### Comando de compilación

    g++ -g -o error_logico codigo/02_error_logico.cpp

### Resultado original

    Promedio: 270

### Resultado esperado

    Promedio: 90

### Causa del error

La función devolvía la suma directamente en vez de dividirla entre la cantidad de notas.

### Código corregido

    return (double)suma / notas.size();

### Resultado final

    Promedio: 90

### Preguntas de reflexión

1. **¿Por qué el compilador no detectó este error?** Porque el código es sintácticamente correcto, simplemente hace un cálculo equivocado.
2. **¿Por qué es un error lógico?** Porque el programa compila y corre sin fallar, pero produce un resultado incorrecto.
3. **¿Qué estrategia usé para encontrarlo?** Calcular manualmente el promedio esperado y compararlo con el resultado obtenido.
4. **¿Qué pruebas adicionales podría hacer?** Probar con otros conjuntos de números para verificar que el promedio siempre es correcto.
