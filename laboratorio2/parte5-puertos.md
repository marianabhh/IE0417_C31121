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
## Logs e inspección

## Comando ejecutado
docker run -d --name app-logs -p 5000:5000 laboratorio-flask:1.0

### Explicación
La opción -d ejecuta el contenedor en segundo plano (detached mode),
liberando la terminal para seguir usándola.

---

## Comando ejecutado
docker logs app-logs

### Explicación
Muestra los logs históricos del contenedor, todo lo que la aplicación
ha impreso desde que inició.

### Resultado obtenido
* Serving Flask app 'app'
* Running on all addresses (0.0.0.0)
* Running on http://127.0.0.1:5000

---

## Comando ejecutado
docker logs -f app-logs

### Explicación
Muestra los logs en tiempo real, útil para monitorear la aplicación
mientras recibe peticiones.

---

## Comando ejecutado
docker inspect app-logs

### Explicación
Muestra información detallada del contenedor en formato JSON, incluyendo
configuración de red, puertos, variables de entorno, imagen usada y estado.

---

## Comando ejecutado
docker stats

### Explicación
Muestra el consumo de recursos en tiempo real de los contenedores activos.

### Resultado obtenido
CONTAINER ID   NAME       CPU %   MEM USAGE / LIMIT     MEM %
b347aabc7727   app-logs   0.01%   21.59MiB / 7.706GiB   0.27%

---

## Preguntas de reflexión

**1. ¿Por qué los logs son importantes al trabajar con contenedores?**
Porque los contenedores no tienen interfaz gráfica, los logs son la 
única forma de ver qué está pasando adentro.

**2. ¿Qué diferencia hay entre logs históricos y logs en tiempo real?**
Los históricos muestran todo lo que pasó desde que inició. Los en 
tiempo real muestran nuevos eventos mientras ocurren.

**3. ¿Qué información útil se puede obtener con docker inspect?**
IP del contenedor, puertos mapeados, variables de entorno, imagen base,
estado del contenedor y configuración de red.

**4. ¿Por qué es importante observar el consumo de recursos?**
Para detectar si un contenedor está consumiendo demasiada memoria o 
CPU y está afectando el rendimiento del sistema.
