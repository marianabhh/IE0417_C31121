# Parte 1: Plan de pruebas

## Qué es CMake

CMake es una herramienta de construcción multiplataforma que genera archivos de compilación (como Makefiles) a partir de un archivo de configuración llamado `CMakeLists.txt`. Permite compilar proyectos en C++ de forma automatizada y portable.

## Para qué sirve Google Test

Google Test es un framework de pruebas unitarias para C++. Permite escribir pruebas de forma estructurada, ejecutarlas automáticamente y obtener reportes claros sobre cuáles pasaron y cuáles fallaron.

## Qué significa automatizar pruebas

Automatizar pruebas significa que las verificaciones del código se ejecutan sin intervención manual. Basta con un comando para correr todas las pruebas y saber si el sistema funciona correctamente.

## Qué significa que las pruebas sean repetibles

Una prueba repetible produce el mismo resultado cada vez que se ejecuta bajo las mismas condiciones. Esto garantiza que los resultados sean confiables y no dependan de factores externos.

## Archivos y carpetas creados

- `CMakeLists.txt`: configuración del proyecto
- `include/`: cabeceras de las funciones
- `src/`: implementaciones
- `tests/`: archivos de prueba
- `docs/`: documentación
- `.github/workflows/testing.yml`: workflow de CI

## Preguntas de reflexión

1. Separar el código fuente de las pruebas mantiene el proyecto organizado y evita que el código de prueba se mezcle con el código de producción.
2. CMake permite compilar el proyecto con un solo comando y de forma portable entre sistemas operativos.
3. Ejecutar pruebas con un solo comando ahorra tiempo y reduce errores humanos al verificar manualmente.
4. Las pruebas manuales son lentas, propensas a errores y no escalables. Las automáticas son rápidas, consistentes y repetibles.

## Tabla de casos funcionales

| ID | Requisito | Entrada | Resultado esperado | Tipo de caso |
|---|---|---:|---|---|
| TC-001 | Convertir nota excelente | 95 | A | Normal |
| TC-002 | Límite inferior de A | 90 | A | Borde |
| TC-003 | Límite superior de B | 89 | B | Borde |
| TC-004 | Nota inválida baja | -1 | Excepción | Inválido |
| TC-005 | Nota inválida alta | 101 | Excepción | Inválido |

Todos estos casos están cubiertos en `tests/test_grade_utils.cpp`.
