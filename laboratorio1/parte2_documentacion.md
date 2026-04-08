### URL del repositorio utilizado
https://github.com/pallets/flask

### Herramienta seleccionada
Sphinx

### Pasos realizados 

Primero descargué el repositorio desde GitHub usando el comando git clone y luego entré a la carpeta del proyecto con cd flask. Esto me permitió trabajar directamente con el código fuente.

Después instalé Sphinx con el comando pip install sphinx, el cual permite generar documentación automática para proyectos en Python.

Luego ejecuté python -m sphinx.cmd.quickstart para crear la estructura inicial del proyecto de documentación. Esto generó carpetas como source y build junto con archivos de configuración.

Posteriormente generé la documentación automática del código usando python -m sphinx.ext.apidoc -o source ., lo cual creó archivos que describen los módulos del proyecto.

Después edité el archivo index.rst dentro de la carpeta source para incluir los módulos generados agregando la palabra modules dentro del bloque toctree.

Finalmente generé la documentación en HTML con el comando python -m sphinx -b html source build/html. Luego abrí el archivo build/html/index.html en el navegador para verificar que la documentación fuera navegable.

### Problemas encontrados y solución

Uno de los problemas fue que el comando sphinx-quickstart no era reconocido en la terminal, por lo que se solucionó utilizando python -m sphinx.cmd.quickstart.

También hubo un error donde sphinx-build no era encontrado, lo cual se resolvió usando python -m sphinx -b html en lugar del comando tradicional.

Otro problema fue que no aparecían los módulos en la documentación generada, y se solucionó agregando modules en el archivo index.rst.

Finalmente hubo un error con la ruta al generar la documentación, ya que se intentó usar flask como carpeta, pero se solucionó utilizando . para indicar el directorio actual.

### Capturas de pantalla de la documentación generada

Aquí se deben incluir capturas de pantalla de la página principal de la documentación y de los módulos generados.

### Enlace público a la documentación desplegada

No se realizó despliegue en línea.
