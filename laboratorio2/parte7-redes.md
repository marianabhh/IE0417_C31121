# Parte 7: Redes de Docker

## Comando ejecutado
docker network create red-lab

### Explicación
Crea una red personalizada tipo bridge donde los contenedores pueden
comunicarse entre sí usando sus nombres.

### Resultado obtenido
dfde1b921ee692494c4dcdf38f7099346784e6c9c87e6f9c6f76e7d295b07bc8

---

## Comando ejecutado
docker network ls

### Resultado obtenido
NETWORK ID     NAME      DRIVER    SCOPE
11e1c2119532   bridge    bridge    local
cc6bf2226590   host      host      local
9ad7e8fceb7c   none      null      local
dfde1b921ee6   red-lab   bridge    local

---

## Comandos ejecutados
docker run -d --name servidor-web --network red-lab nginx
docker run -it --name cliente --network red-lab ubuntu bash

### Explicación
Ambos contenedores se conectaron a la misma red red-lab, lo que les
permite comunicarse entre sí usando sus nombres.

---

## Dentro del contenedor cliente
curl http://servidor-web

### Resultado obtenido
<!DOCTYPE html>
<html>
<head><title>Welcome to nginx!</title></head>
...
</html>

### Reflexión
El contenedor cliente pudo acceder al servidor nginx usando solo su
nombre, sin necesidad de conocer su IP.

---

## Preguntas de reflexión

**1. ¿Por qué los contenedores necesitan redes?**
Para poder comunicarse entre sí de forma controlada y segura.

**2. ¿Qué ventaja tiene usar nombres en lugar de IPs?**
Las IPs pueden cambiar cada vez que se crea un contenedor, los nombres
son siempre los mismos y más fáciles de recordar.

**3. ¿Qué diferencia hay entre publicar un puerto hacia el host y 
comunicarse dentro de una red Docker?**
Publicar un puerto permite acceso desde fuera del contenedor. 
Comunicarse dentro de una red es solo entre contenedores, sin
exponer nada al exterior.

**4. ¿Qué ejemplos reales podrían usar una red Docker?**
Una app web comunicándose con su base de datos, un backend con
un servidor de caché como Redis, microservicios entre sí.

## Comunicación entre servicios

## Comandos ejecutados
docker network create red-app
docker run -d --name redis-lab --network red-app redis
docker run -it --name cliente-redis --network red-app redis redis-cli -h redis-lab

### Qué es Redis en este ejemplo
Redis es una base de datos en memoria que se usó como servicio separado
al que la aplicación cliente se conectó a través de la red.

### Qué representa redis-lab
Es el contenedor que actúa como servidor de base de datos, accesible
por su nombre dentro de la red red-app.

### Cómo se conectó el cliente al servidor
Usando el nombre redis-lab como host, Docker resolvió automáticamente
la IP del contenedor dentro de la red.

### Resultado obtenido
ping → PONG
set curso IE0417 → OK
get curso → "IE0417"

### Qué significa recibir PONG
Que la conexión entre los dos contenedores fue exitosa.

---

## Preguntas de reflexión

**1. ¿Por qué una app web necesitaría comunicarse con una base de datos?**
Para guardar y recuperar información de forma persistente.

**2. ¿Por qué ambos contenedores deben estar en la misma red?**
Porque por defecto los contenedores están aislados, solo los de la
misma red pueden comunicarse entre sí.

**3. ¿Qué ventaja tiene separar servicios en contenedores distintos?**
Cada servicio puede actualizarse, escalarse o reiniciarse de forma
independiente sin afectar a los demás.

**4. ¿Qué limitación tiene hacerlo manualmente con varios docker run?**
Es tedioso, propenso a errores y difícil de mantener. Para eso existe
Docker Compose que automatiza todo esto.
