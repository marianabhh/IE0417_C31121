# Parte 3: Imágenes y contenedores

## Comando ejecutado
docker pull ubuntu

### Explicación
Descarga la imagen de Ubuntu desde Docker Hub al sistema local sin 
ejecutar ningún contenedor.

### Resultado obtenido
Status: Downloaded newer image for ubuntu:latest
docker.io/library/ubuntu:latest

### Reflexión
docker pull permite tener la imagen lista localmente antes de usarla,
sin necesidad de ejecutar un contenedor inmediatamente.

---

## Comando ejecutado
docker images

### Explicación
Lista todas las imágenes descargadas localmente en el sistema.

### Resultado obtenido
IMAGE                ID             DISK USAGE
hello-world:latest   0e760fdfbc48   25.9kB
ubuntu:latest        f3d28607ddd7   160MB

### Reflexión
Se pueden ver las dos imágenes descargadas, hello-world y ubuntu, 
con su ID y tamaño en disco.

---

## Comando ejecutado
docker run -it ubuntu bash

### Explicación
Ejecuta un contenedor de Ubuntu en modo interactivo (-it) y abre 
una terminal bash dentro de él.

### Resultado obtenido
Dentro del contenedor se ejecutaron:
- ls: mostró los directorios del sistema Linux (bin, boot, dev, etc.)
- pwd: mostró que estamos en el directorio raíz /
- cat /etc/os-release: mostró que es Ubuntu 26.04 LTS

### Reflexión
El contenedor se ve como un sistema Linux completo por dentro, aunque 
no es una máquina virtual, comparte el kernel con el host.

---

## Comando ejecutado
docker ps -a

### Resultado obtenido
CONTAINER ID   IMAGE         COMMAND    STATUS
23b0c609f1d0   ubuntu        "bash"     Exited (0)
0b445a2cc3f4   hello-world   "/hello"   Exited (0)

### Reflexión
Al salir con exit el contenedor se detuvo automáticamente porque su 
proceso principal (bash) terminó.

---

## Preguntas de reflexión

**1. ¿La imagen Ubuntu es lo mismo que una máquina virtual Ubuntu?**
No, la imagen es una plantilla liviana que no incluye su propio kernel 
ni hardware virtualizado. Comparte el kernel del host.

**2. ¿Por qué el contenedor puede parecer un sistema Linux si no es una VM?**
Porque Docker aísla el sistema de archivos y los procesos usando 
tecnologías del kernel de Linux como namespaces y cgroups, dando la 
apariencia de un sistema separado.

**3. ¿Qué significa que el contenedor comparta el kernel con el host?**
Significa que no necesita virtualizar hardware completo, lo que lo hace 
mucho más liviano y rápido que una máquina virtual.

**4. ¿Qué diferencia hay entre una imagen descargada y un contenedor creado?**
La imagen es una plantilla estática e inmutable. El contenedor es una 
instancia en ejecución creada a partir de esa imagen, con su propio 
sistema de archivos temporal.


## Administración de contenedores

## Comando ejecutado
docker run -it --name mi-ubuntu ubuntu bash

### Explicación
Crea un contenedor con un nombre específico usando --name, lo que facilita 
referenciarlo después sin usar el ID.

---

## Dentro del contenedor
echo "Hola desde el contenedor" > mensaje.txt
cat mensaje.txt

### Resultado obtenido
Hola desde el contenedor

---

## Comandos ejecutados
docker start mi-ubuntu
docker exec -it mi-ubuntu bash

### Explicación
docker start reinicia un contenedor detenido. docker exec permite entrar 
a un contenedor que ya está corriendo sin crear uno nuevo.

### Resultado obtenido
El archivo mensaje.txt seguía existiendo con su contenido original.

---

## Comandos ejecutados
docker stop mi-ubuntu
docker rm mi-ubuntu

### Explicación
docker stop detiene el contenedor. docker rm lo elimina. No se puede 
eliminar un contenedor mientras está corriendo.

### Reflexión
Los datos creados dentro del contenedor se pierden al eliminarlo, por 
eso se dice que los contenedores son desechables.

---

## Preguntas de reflexión

**1. ¿Qué ventaja tiene asignar nombres a los contenedores?**
Permite referenciarlo fácilmente con un nombre legible en lugar de 
usar el ID largo.

**2. ¿Qué diferencia hay entre crear un contenedor nuevo y reiniciar uno existente?**
Al crear uno nuevo se parte de cero. Al reiniciar uno existente se 
conservan los cambios hechos dentro de él.

**3. ¿Qué sucede con los datos creados dentro de un contenedor si este se elimina?**
Se pierden permanentemente porque el sistema de archivos del contenedor 
se elimina junto con él.

**4. ¿Por qué se dice que los contenedores son desechables?**
Porque están diseñados para crearse, usarse y eliminarse fácilmente, 
sin que los datos importantes dependan de ellos.
