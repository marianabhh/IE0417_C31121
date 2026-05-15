# Parte 5: Publicación de puertos

## Comando ejecutado
docker run --name app-puertos -p 5000:5000 laboratorio-flask:1.0

### Explicación
La opción -p mapea puertos entre el host y el contenedor.
-p 5000:5000 significa puerto 5000 del host → puerto 5000 del contenedor.

### Resultado obtenido
La aplicación fue accesible en http://localhost:5000 mostrando
"Hola desde Flask en Docker"
<img width="1919" height="1023" alt="image" src="https://github.com/user-attachments/assets/970a1b2f-f03c-4de1-a943-3fbbcafbb3dd" />

---

## Comando ejecutado
docker run --name app-puertos-2 -p 8080:5000 laboratorio-flask:1.0

### Explicación
-p 8080:5000 mapea el puerto 8080 del host al puerto 5000 del contenedor.
El contenedor sigue escuchando en 5000 internamente, pero desde afuera
se accede por el 8080.

### Resultado obtenido
La misma aplicación fue accesible en http://localhost:8080
<img width="1919" height="1001" alt="image2" src="https://github.com/user-attachments/assets/adc51510-e1dd-4849-9ac7-b9612c45b4d5" />

---

## Preguntas de reflexión

**1. ¿Por qué no basta con que la aplicación escuche en el puerto 5000 
dentro del contenedor?**
Porque el contenedor tiene su propia red interna aislada. Sin mapear 
el puerto, el host no puede acceder a la aplicación.

**2. ¿Qué función cumple el mapeo de puertos?**
Conecta un puerto del host con un puerto del contenedor, permitiendo 
acceder a la aplicación desde fuera del contenedor.

**3. ¿Cuál es la diferencia entre el puerto del host y el puerto del contenedor?**
El puerto del host es el que usamos en el navegador. El puerto del 
contenedor es donde la aplicación escucha internamente.

**4. ¿Qué pasaría si dos contenedores intentan usar el mismo puerto del host?**
Daría error porque un puerto del host solo puede estar ocupado por 
un proceso a la vez.
