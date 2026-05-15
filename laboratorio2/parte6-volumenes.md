# Parte 6: Persistencia con volúmenes

## Comando ejecutado
docker volume create datos-lab

### Explicación
Crea un volumen administrado por Docker donde se pueden guardar datos
de forma persistente fuera del ciclo de vida del contenedor.

### Resultado obtenido
datos-lab

---

## Comando ejecutado
docker volume ls

### Resultado obtenido
DRIVER    VOLUME NAME
local     datos-lab

---

## Comando ejecutado
docker run -it --name contenedor-volumen -v datos-lab:/datos ubuntu bash

### Explicación
Monta el volumen datos-lab en la carpeta /datos dentro del contenedor.

### Dentro del contenedor
echo "Este archivo está en un volumen" > /datos/archivo.txt
cat /datos/archivo.txt

### Resultado obtenido
Este archivo está en un volumen

---

## Después de eliminar el contenedor y crear uno nuevo con el mismo volumen
cat /datos/archivo.txt

### Resultado obtenido
Este archivo está en un volumen

### Reflexión
El archivo seguía existiendo aunque el primer contenedor fue eliminado,
porque el volumen es independiente del contenedor.

---

## Comando ejecutado
docker volume inspect datos-lab

### Resultado obtenido
{
    "CreatedAt": "2026-05-15T04:39:00Z",
    "Driver": "local",
    "Mountpoint": "/var/lib/docker/volumes/datos-lab/_data",
    "Name": "datos-lab",
    "Scope": "local"
}

---

## Preguntas de reflexión

**1. ¿Qué problema resuelven los volúmenes?**
La pérdida de datos al eliminar un contenedor. Con volúmenes los datos
persisten independientemente del ciclo de vida del contenedor.

**2. ¿El volumen pertenece a un contenedor específico?**
No, el volumen es independiente y puede ser montado por cualquier
contenedor.

**3. ¿Qué diferencia hay entre eliminar un contenedor y eliminar un volumen?**
Eliminar el contenedor no elimina el volumen ni sus datos. Para eliminar
los datos hay que eliminar el volumen explícitamente.

**4. ¿Para qué casos reales se usarían volúmenes?**
Bases de datos, archivos subidos por usuarios, logs, configuraciones
que deben persistir entre reinicios.

## Bind mounts

## Comando ejecutado
docker run --name app-bind -p 5000:5000 -v ${PWD}:/app laboratorio-flask:1.0

### Explicación
En lugar de un volumen administrado por Docker, monta directamente la 
carpeta local del host dentro del contenedor.

### Diferencia entre datos-lab:/datos y ${PWD}:/app
- datos-lab:/datos usa un volumen administrado por Docker, guardado en 
una ubicación interna de Docker.
- ${PWD}:/app monta directamente una carpeta del host, los cambios en 
los archivos locales se reflejan inmediatamente en el contenedor.

### Qué ocurrió al modificar el código local
Al cambiar el mensaje en app.py y reiniciar el contenedor, el cambio 
se reflejó inmediatamente sin necesidad de reconstruir la imagen.

---

## Preguntas de reflexión

**1. ¿Qué diferencia hay entre un volumen y un bind mount?**
Un volumen es administrado por Docker y vive en su sistema interno.
Un bind mount es una carpeta del host montada directamente.

**2. ¿Cuál es más conveniente para desarrollo?**
El bind mount, porque permite editar el código localmente y ver los 
cambios sin reconstruir la imagen.

**3. ¿Cuál es más conveniente para datos persistentes?**
El volumen, porque Docker lo gestiona de forma segura e independiente 
del sistema de archivos del host.

**4. ¿Qué riesgos podría tener montar carpetas del host en el contenedor?**
El contenedor tendría acceso directo a archivos del host, lo que podría 
ser un riesgo de seguridad si el contenedor es comprometido.
