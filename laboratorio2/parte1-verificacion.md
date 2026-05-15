# Parte 1: Verificación de instalación de Docker

## Sistema operativo utilizado
Windows 11 con WSL2

## Comando ejecutado
````docker --version```

### Explicación
Este comando muestra la versión de Docker instalada en el sistema.

### Resultado obtenido
Docker version 29.4.3, build 055a478

### Reflexión
Verificar la versión confirma que Docker se instaló correctamente.

---

## Comando ejecutado
```docker info```

### Explicación
Este comando muestra información detallada del sistema Docker, incluyendo
contenedores activos, imágenes descargadas, versión del sistema operativo,
memoria disponible y configuración del daemon.

### Resultado obtenido
Client:
 Version: 29.4.3
 Context: desktop-linux
 Debug Mode: false

### Reflexión
Es importante verificar la instalación antes de continuar porque si el
daemon no está corriendo, ningún comando de Docker va a funcionar.

---

## Preguntas de reflexión

**1. ¿Qué diferencia hay entre instalar Docker y tenerlo ejecutándose correctamente?**
Instalar Docker solo copia los archivos necesarios en el sistema. Para que funcione, el daemon de Docker debe estar activo en segundo plano.

**2. ¿Qué información útil muestra docker info?**
Muestra la versión, contexto, plugins instalados, cantidad de contenedores e imágenes, y configuración del sistema.

**3. ¿Por qué Docker necesita un daemon ejecutándose en segundo plano?**
Porque el daemon es el que realmente gestiona los contenedores. Sin él, el cliente no tiene con quién comunicarse.
```

