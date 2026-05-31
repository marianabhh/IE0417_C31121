# Reflexión final

## Mini reto de testing

Se implementó la función `is_valid_grade(int grade)` que retorna `true` si la nota está entre 0 y 100.

### Casos de prueba diseñados

| Prueba | Entrada | Esperado | Tipo |
|---|---|---|---|
| ValidGradeNormalValue | 85 | true | Normal |
| InvalidGradeBelowZero | -1 | false | Inválido |
| ValidGradeLowerBound | 0 | true | Borde |
| ValidGradeUpperBound | 100 | true | Borde |
| InvalidGradeAbove100 | 101 | false | Inválido |
| InvalidGradeFarBelow | -50 | false | Inválido |

Se escogieron estos casos porque cubren el comportamiento normal, los dos bordes exactos y valores fuera del rango por ambos lados.

Resultado: 47/47 pruebas pasaron. Los cambios se subieron a GitHub y Actions ejecutó exitosamente.

## Reflexión final

1. El software testing es el proceso de verificar que un programa funciona correctamente mediante pruebas sistemáticas que detectan errores antes de que lleguen al usuario.

2. El testing mejora la calidad porque detecta errores temprano, documenta el comportamiento esperado y permite hacer cambios con confianza sabiendo que las pruebas avisarán si algo se rompe.

3. La verificación comprueba que el software fue construido correctamente (cumple las especificaciones técnicas). La validación comprueba que el software correcto fue construido (cumple las necesidades del usuario).

4. Una prueba unitaria verifica una unidad pequeña de código de forma aislada, como una función individual, sin depender de otras partes del sistema.

5. Una prueba funcional verifica el comportamiento del sistema desde la perspectiva del usuario o del requisito, sin importar la implementación interna.

6. `EXPECT_` reporta el fallo pero continúa ejecutando el resto de la prueba. `ASSERT_` detiene la prueba inmediatamente al fallar, útil cuando continuar no tiene sentido.

7. Las pruebas deben ser deterministas para que sus resultados sean confiables. Una prueba que a veces pasa y a veces falla no aporta información útil.

8. Una semilla fija hace que los valores aleatorios sean siempre los mismos, permitiendo reproducir exactamente el mismo escenario de prueba cada vez.

9. La cobertura de código es el porcentaje del código que fue ejecutado durante las pruebas. Indica qué partes del código han sido ejercitadas.

10. Una cobertura alta no garantiza ausencia de errores porque las pruebas pueden ejecutar el código con valores correctos sin probar combinaciones problemáticas.

11. GitHub Actions ejecuta las pruebas automáticamente en cada push, asegurando que el código siempre funcione antes de integrarse y detectando errores en cualquier entorno.

12. La parte más útil fue ver cómo una prueba fallida identifica exactamente dónde está el error y qué valor incorrecto se obtuvo.

13. La parte más difícil fue configurar correctamente CMake y entender los flags de cobertura con lcov.

14. En proyectos futuros, escribiría pruebas unitarias desde el inicio para cada función nueva, ejecutaría las pruebas antes de cada commit y configuraría CI desde el principio del proyecto.
