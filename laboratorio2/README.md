# Laboratorio 2: Introducción práctica a contenedores con Docker

## Índice
- [Parte 1: Verificación](parte1-verificacion.md)
- [Parte 2: Primer contenedor](parte2-comandos-basicos.md)
- [Parte 3: Imágenes y contenedores](parte3-imagenes-y-contenedores.md)
- [Parte 4: Dockerfile](parte4-dockerfile.md)
- [Parte 5: Puertos, logs y variables de entorno](parte5-puertos.md)
- [Parte 6: Volúmenes y bind mounts](parte6-volumenes.md)
- [Parte 7: Redes](parte7-redes.md)
- [Parte 8: Limpieza](parte8-limpieza.md)

---

## Reflexión final

**1. ¿Qué es un contenedor?**
Es una unidad liviana y autónoma que empaqueta una aplicación con todo
lo necesario para ejecutarla, compartiendo el kernel con el host.

**2. ¿Qué problema resuelve Docker?**
El problema de "en mi máquina funciona". Con Docker la aplicación corre
igual en cualquier entorno donde esté instalado Docker.

**3. ¿Qué diferencia hay entre una imagen y un contenedor?**
La imagen es la plantilla estática e inmutable. El contenedor es la
instancia en ejecución creada a partir de esa imagen.

**4. ¿Qué diferencia hay entre un contenedor y una máquina virtual?**
Una VM virtualiza hardware completo con su propio sistema operativo.
Un contenedor comparte el kernel del host y es mucho más liviano y rápido.

**5. ¿Qué aprendí sobre puertos?**
Que los contenedores tienen su propia red interna y hay que mapear
puertos explícitamente para acceder a ellos desde el host.

**6. ¿Qué aprendí sobre volúmenes?**
Que los datos dentro de un contenedor se pierden al eliminarlo, y los
volúmenes permiten persistir datos fuera del ciclo de vida del contenedor.

**7. ¿Qué aprendí sobre redes?**
Que Docker permite crear redes personalizadas donde los contenedores
pueden comunicarse entre sí usando sus nombres.

**8. ¿En qué casos usaría Docker en un proyecto de software?**
Para empaquetar y distribuir aplicaciones, configurar entornos de
desarrollo consistentes y separar servicios como bases de datos y
backends en contenedores independientes.

**9. ¿Qué parte del laboratorio pareció más útil?**
La parte de redes, porque mostró cómo varios servicios pueden
comunicarse entre sí de forma sencilla usando nombres de contenedor.

**10. ¿Qué parte pareció más confusa?**
La parte de volúmenes y bind mounts, porque la diferencia entre ambos
no era tan obvia al principio.
