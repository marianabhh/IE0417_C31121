# Laboratorio de programación concurrente y paralela en C++

## Estudiante
Nombre: Mariana Bernal Hernández
Carné: C31121

## Descripción
Este laboratorio explora conceptos básicos de programación concurrente y paralela usando C++.

## Requisitos
- g++
- C++17 o superior
- Linux o WSL

## Compilación y ejecución

### Parte 1
```bash
g++ -std=c++17 -Wall -Wextra -pthread src/parte1_threads.cpp -o parte1
./parte1
```

### Parte 2
```bash
g++ -std=c++17 -Wall -Wextra -pthread src/parte2_race_condition.cpp -o parte2
./parte2
```

### Parte 3
```bash
g++ -std=c++17 -Wall -Wextra -pthread src/parte3_mutex.cpp -o parte3
./parte3
```

### Parte 4
```bash
g++ -std=c++17 -O2 -Wall -Wextra -pthread src/parte4_benchmark.cpp -o parte4
./parte4
```

### Parte 5
```bash
g++ -std=c++17 -O2 -Wall -Wextra -pthread src/parte5_hilos_vs_rendimiento.cpp -o parte5
./parte5
```

### Parte 6
```bash
g++ -std=c++17 -Wall -Wextra -pthread src/parte6_deadlock.cpp -o parte6
./parte6
g++ -std=c++17 -Wall -Wextra -pthread src/parte6_deadlock_corregido.cpp -o parte6_corregido
./parte6_corregido
```

