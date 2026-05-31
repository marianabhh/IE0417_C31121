# Parte 4: Casos borde

## Qué es un caso borde

Un caso borde es una entrada que se encuentra en los límites del rango válido de una función, como el valor mínimo, el máximo, o valores justo fuera del rango permitido.

## Casos borde agregados

- `ZeroIsEven`: verifica que 0 sea par
- `DivideNegativeNumbers`: divide dos negativos
- `DividePositiveByNegative`: divide positivo entre negativo
- `EmptyStringToUppercase`: cadena vacía a mayúsculas
- `EmptyStringIsPalindrome`: cadena vacía como palíndromo
- `SingleLetterIsPalindrome`: una letra sola es palíndromo
- `MinimumValidGrade`: nota 0 retorna F
- `MaximumValidGrade`: nota 100 retorna A
- `GradeBoundaryBetweenFAndD`: 59→F, 60→D
- `GradeBoundaryBetweenDAndC`: 69→D, 70→C
- `GradeBoundaryBetweenCAndB`: 79→C, 80→B
- `GradeBoundaryBetweenBAndA`: 89→B, 90→A

## Por qué son importantes

Los errores en software ocurren frecuentemente en los límites. Una función puede manejar bien el caso 85 pero fallar exactamente en 80 si el operador de comparación está mal escrito.

## Resultado

```
[  PASSED  ] 47 tests.
```

## Semillas en pruebas

La semilla inicializa el generador de números aleatorios en un estado conocido. Con la misma semilla, la secuencia de números generados es siempre la misma, haciendo la prueba determinista y repetible. Al cambiar la semilla cambian los valores pero la lógica sigue siendo válida. Esto ayuda a reproducir errores: si una prueba falla con cierta semilla, se puede volver a ejecutar exactamente igual.

## Preguntas de reflexión

1. No basta con casos normales porque los errores suelen ocurrir en los límites y casos extremos.
2. Un caso borde es una entrada en el límite del rango válido, como 0, 100, -1 o 101.
3. Un caso inválido es una entrada fuera del rango aceptado que debería ser rechazada.
4. Probar 85 verifica el comportamiento general; probar 80, 90, 70 verifica exactamente dónde cambia el comportamiento.
5. Un caso borde puede revelar errores de operadores como `>` versus `>=`.
