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
