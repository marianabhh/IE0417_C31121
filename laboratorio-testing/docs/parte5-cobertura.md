# Parte 5: Cobertura de código

## Qué es cobertura de código

La cobertura de código es una métrica que indica qué porcentaje de las líneas, funciones o ramas del código fueron ejecutadas durante las pruebas.

## Comandos utilizados

```bash
cmake -DENABLE_COVERAGE=ON ..
make
./run_tests
lcov --capture --directory . --output-file coverage.info --ignore-errors mismatch,gcov
lcov --remove coverage.info '/usr/*' '*/_deps/*' '*/tests/*' --output-file coverage_filtered.info --ignore-errors empty
genhtml coverage_filtered.info --output-directory coverage_report
```

## Porcentaje de cobertura obtenido

- Líneas: 100.0% (40 de 40)
- Funciones: 100.0% (12 de 12)

## Archivos cubiertos

- `src/calculator.cpp`: 7 líneas, 5 funciones — 100