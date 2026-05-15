# Parte 4: Aplicación sencilla con Flask

## ¿Qué hace la aplicación?
Es una aplicación web mínima hecha con Flask que tiene dos rutas:
- /: Muestra un mensaje que puede configurarse con una variable de entorno
- /info: Devuelve información del laboratorio en formato JSON

## Dependencia utilizada
Flask, un framework web liviano para Python.

## ¿Por qué se usa host="0.0.0.0"?
Porque dentro de un contenedor, si la app escucha solo en localhost 
solo sería accesible desde adentro del contenedor. Con 0.0.0.0 acepta 
conexiones desde cualquier dirección, incluyendo desde el host.

## Resultado local
La aplicación corrió correctamente en http://localhost:5000 mostrando
el mensaje "Hola desde Flask en Docker" y en /info devolvió el JSON
con la información del laboratorio.

## Preguntas de reflexión

**1. ¿Qué hace Flask en esta aplicación?**
Flask es el framework que permite crear rutas web y manejar las 
peticiones HTTP de forma sencilla en Python.

**2. ¿Para qué sirve el archivo requirements.txt?**
Lista las dependencias necesarias para correr la aplicación, así 
cualquier persona o contenedor puede instalarlas fácilmente con 
pip install -r requirements.txt.

**3. ¿Por qué una aplicación dentro de un contenedor debe escuchar en 0.0.0.0?**
Porque el contenedor tiene su propia red interna, y para que el host 
pueda acceder a la app, esta debe aceptar conexiones externas.

**4. ¿Qué diferencia hay entre ejecutar la aplicación localmente y en Docker?**
Localmente depende de que Python y Flask estén instalados en la máquina. 
En Docker todo viene empaquetado en la imagen, funcionando igual en 
cualquier sistema donde esté Docker.

## Construcción de la imagen con Dockerfile

## Instrucciones del Dockerfile

**FROM python:3.11-slim**
Define la imagen base, en este caso Python 3.11 en versión slim (liviana, 
sin herramientas innecesarias).

**WORKDIR /app**
Establece el directorio de trabajo dentro del contenedor.

**COPY requirements.txt .**
Copia solo el archivo de dependencias primero para aprovechar el caché 
de Docker.

**RUN pip install --no-cache-dir -r requirements.txt**
Instala las dependencias dentro del contenedor.

**COPY . .**
Copia el resto del código al contenedor.

**EXPOSE 5000**
Indica que la aplicación usará el puerto 5000.

**CMD ["python", "app.py"]**
Define el comando que se ejecuta al iniciar el contenedor.

---

## Preguntas de reflexión

**1. ¿Qué es una imagen base?**
Es la imagen de partida sobre la que se construye la nueva imagen.

**2. ¿Por qué se usa una imagen slim?**
Para reducir el tamaño final de la imagen eliminando herramientas 
innecesarias.

**3. ¿Por qué se copian primero las dependencias y luego el código?**
Para aprovechar el caché de Docker. Si el código cambia pero las 
dependencias no, Docker no las reinstala.

**4. ¿Qué diferencia hay entre RUN y CMD?**
RUN se ejecuta al construir la imagen. CMD se ejecuta cuando se 
inicia el contenedor.

**5. ¿Qué pasaría si se elimina la imagen pero no el Dockerfile?**
Se puede reconstruir la imagen en cualquier momento usando el 
Dockerfile.
