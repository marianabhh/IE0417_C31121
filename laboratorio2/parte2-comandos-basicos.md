# Parte 2: Primer contenedor

## Comando ejecutado
docker run hello-world

### Explicación
Este comando busca la imagen hello-world localmente, como no la encontró 
la descargó automáticamente de Docker Hub y ejecutó un contenedor con ella.

### Resultado obtenido
Unable to find image 'hello-world:latest' locally
latest: Pulling from library/hello-world
Status: Downloaded newer image for hello-world:latest
Hello from Docker!

### Reflexión
Cuando la imagen no está descargada localmente, Docker la busca y descarga 
automáticamente desde Docker Hub antes de ejecutarla.

---

## Comando ejecutado
docker ps

### Explicación
Lista los contenedores que están actualmente en ejecución.

### Resultado obtenido
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
(vacío, ningún contenedor activo)

### Reflexión
El contenedor hello-world no aparece porque ya terminó su ejecución.

---

## Comando ejecutado
docker ps -a

### Explicación
Lista todos los contenedores, incluyendo los que ya se detuvieron.

### Resultado obtenido
CONTAINER ID   IMAGE         COMMAND    CREATED            STATUS
0b445a2cc3f4   hello-world   "/hello"   About a minute ago Exited (0)

### Reflexión
El contenedor aparece aquí porque -a muestra todos los contenedores 
sin importar su estado.

---

## Preguntas de reflexión

**1. ¿Qué es la imagen hello-world?**
Es una imagen mínima de Docker Hub diseñada para verificar que Docker 
funciona correctamente. Solo imprime un mensaje y termina.

**2. ¿El contenedor quedó ejecutándose después de imprimir el mensaje?**
No, el contenedor se detuvo automáticamente al terminar su única tarea 
que era imprimir el mensaje.

**3. ¿Por qué aparece en docker ps -a pero no en docker ps?**
Porque docker ps solo muestra contenedores en ejecución, mientras que 
docker ps -a muestra todos incluyendo los detenidos.

**4. ¿Qué demuestra este primer ejemplo sobre Docker?**
Demuestra que Docker puede descargar imágenes automáticamente, crear 
contenedores y ejecutarlos de forma aislada muy fácilmente.
