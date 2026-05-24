# Parte 1: instalación y verificación del ambiente

## Sistema operativo
Ubuntu 24.04 en WSL2 sobre Windows.

## Versiones de herramientas

- `g++`: 13.3.0
- `gdb`: 15.1
- `valgrind`: 3.22.0

## Compilación y ejecución de prueba

### Comando de compilación

    g++ -g -o prueba codigo/prueba.cpp

### Resultado

    Ambiente listo para depuración

## Para qué sirve cada herramienta

- **g++**: compilador de C++. Convierte el código fuente en un ejecutable.
- **gdb**: depurador. Permite ejecutar el programa paso a paso e inspeccionar variables.
- **valgrind**: detector de errores de memoria. Encuentra pérdidas de memoria y accesos inválidos.

## Preguntas de reflexión

1. **¿Para qué sirve g++?** Para compilar programas en C++ y convertirlos en ejecutables.
2. **¿Para qué sirve gdb?** Para depurar programas, detenerlos en puntos específicos e inspeccionar su estado.
3. **¿Para qué sirve valgrind?** Para detectar errores de memoria como pérdidas o accesos fuera de límites.
4. **¿Por qué compilar con -g?** Porque incluye símbolos de depuración que permiten a gdb mostrar nombres de variables y líneas de código.
5. **¿Diferencia entre compilar y depurar?** Compilar convierte el código en ejecutable. Depurar es analizar ese ejecutable en ejecución para encontrar errores.
