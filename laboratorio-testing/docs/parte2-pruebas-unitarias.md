# Parte 2: Pruebas unitarias

## Módulos creados

- `calculator`: operaciones aritméticas básicas
- `string_utils`: manipulación de cadenas de texto
- `grade_utils`: manejo de notas académicas

## Función de los archivos .h

Los archivos `.h` declaran las funciones disponibles en cada módulo. Actúan como contratos que indican qué funciones existen y qué parámetros reciben.

## Función de los archivos .cpp

Los archivos `.cpp` contienen la implementación real de cada función declarada en los `.h`.

## Casos normales, borde e inválidos por función

- `add`, `subtract`, `multiply`: casos normales con positivos y negativos
- `divide`: caso inválido con divisor cero
- `is_even`: caso borde con cero
- `to_uppercase`: caso borde con cadena vacía
- `is_palindrome`: casos borde con cadena vacía y un solo carácter
- `letter_grade`: casos borde en cada límite (60, 70, 80, 90, 100); caso inválido con nota negativa o mayor a 100
- `average`: caso inválido con vector vacío

## Comandos de compilación

```bash
mkdir build && cd build
cmake ..
make
```

## Comandos de ejecución

```bash
./run_tests
ctest --output-on-failure
```

## Resultado de ./run_tests

```
[==========] Running 47 tests from 3 test suites.
[  PASSED  ] 47 tests.
```

## Pruebas ejecutadas: 47. Pruebas exitosas: 47.

## Explicación de cinco pruebas

### AddPositiveNumbers
Verifica que `add(2, 3)` retorne 5. Caso normal básico de suma.

### DivideByZeroThrowsException
Verifica que dividir entre cero lanza `std::invalid_argument`. Prueba el manejo de casos inválidos.

### DetectPalindromeWithSpaces
Verifica que "anita lava la tina" sea palíndromo ignorando espacios. Prueba normalización de entrada.

### GradeBoundaryBetweenBAndA
Verifica que 89 retorne B y 90 retorne A. Prueba exactamente el límite entre dos categorías.

### AverageEmptyVectorThrowsException
Verifica que calcular el promedio de un vector vacío lanza excepción. Prueba caso inválido.

## EXPECT vs ASSERT

Cuando `divisor = 2`: `ASSERT_NE` pasa y la prueba continúa normalmente.
Cuando `divisor = 0`: `ASSERT_NE` falla y detiene la prueba inmediatamente, sin ejecutar `divide(10, 0)` que lanzaría una excepción no capturada.

`EXPECT_` reporta el fallo pero continúa ejecutando el resto de la prueba. `ASSERT_` detiene la prueba inmediatamente al fallar.
