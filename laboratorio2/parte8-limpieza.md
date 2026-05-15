# Parte 8: Limpieza del ambiente

## Recursos que quedaron creados
- 3 contenedores detenidos: app-bind, intelligent_austin, confident_golick
- 5 imágenes: hello-world, laboratorio-flask, nginx, redis, ubuntu
- 1 volumen: datos-lab
- Redes por defecto: bridge, host, none

---

## Comando ejecutado
docker container prune

### Explicación
Elimina todos los contenedores detenidos de una sola vez.

### Resultado obtenido
Deleted Containers: 3 contenedores eliminados
Total reclaimed space: 217.1kB

---

## Comando ejecutado
docker image prune

### Explicación
Elimina imágenes huérfanas, es decir, imágenes sin nombre ni contenedor
asociado.

### Resultado obtenido
Total reclaimed space: 0B (no había imágenes huérfanas)

---

## Comando ejecutado
docker volume prune

### Explicación
Elimina volúmenes que no están siendo usados por ningún contenedor.

---

## Comando ejecutado
docker system df

### Resultado obtenido
TYPE            TOTAL     ACTIVE    SIZE      RECLAIMABLE
Images          5         0         12.63GB   553.1MB (4%)
Containers      0         0         0B        0B
Local Volumes   1         0         33B       33B (100%)
Build Cache     17        0         18.02GB   17.81GB

---

## Comando ejecutado
docker system prune

### Explicación
Limpia contenedores detenidos, redes no usadas, imágenes huérfanas y
caché de build de una sola vez.

### Resultado obtenido
Total reclaimed space: 17.81GB

---

## Preguntas de reflexión

**1. ¿Por qué Docker puede consumir mucho espacio en disco?**
Porque cada imagen descargada, cada capa de build y cada volumen ocupan
espacio que se acumula con el tiempo.

**2. ¿Qué diferencia hay entre eliminar un contenedor y eliminar una imagen?**
Eliminar un contenedor solo borra esa instancia. Eliminar la imagen borra
la plantilla completa y ya no se pueden crear nuevos contenedores de ella.

**3. ¿Por qué se debe tener cuidado al eliminar volúmenes?**
Porque los volúmenes contienen datos persistentes que podrían perderse
permanentemente si se eliminan sin querer.

**4. ¿Qué buenas prácticas aplicaría para mantener limpio el ambiente?**
Eliminar contenedores después de usarlos, usar imágenes slim, limpiar
el caché de build regularmente y revisar el espacio con docker system df.
