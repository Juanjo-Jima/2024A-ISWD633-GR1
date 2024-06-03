# VOLUMEN TIPO HOST
Un volumen host (o bind mount) es un tipo de volumen donde se monta un directorio o archivo específico del sistema de archivos del host en un contenedor.

```
docker run -d --name <nombre contenedor> -v <ruta carpeta host>:<ruta carpeta contenedor> <imagen> 
```

### Crear un volumen tipo host con la imagen nginx:alpine, para la ruta carpeta host: directorio en donde se encuentra la carpeta html en tu computador y para la ruta carpeta contenedor: /usr/share/nginx/html esta ruta se obtiene al revisar la se obtiene desde la documentación
![Volúmenes](imagenes/volumen-host.PNG)
# COMANDO

```
docker run -d -p 80:80 --name mi_contenedor -v C:\Users\HP\RESPALDOS\html_Practica3_Docker/html nginx:alpine
```

### ¿Qué sucede al ingresar al servidor de nginx?

Al ingresar al servidor de nginx lo que ocurre es que aparece un error "403 Forbidden"

### ¿Qué pasa con el archivo index.html del contenedor?

El archivo index.html del contenedor estará disponible en el directorio /usr/share/nginx/html. Si has montado correctamente el volumen host, podrás modificar este archivo desde tu sistema de archivos local y los cambios se reflejarán en el contenedor.

### Ir a https://html5up.net/ y descargar un template gratuito, descomprirlo dentro de nginx/html
### ¿Qué sucede al ingresar al servidor de nginx?

Después de descargar y descomprimir el template gratuito dentro de la carpeta html en el sistema de archivos local, los archivos del template estarán disponibles dentro del contenedor en el directorio vinculado, ya que este directorio está vinculado con la carpeta en mi host.

### Eliminar el contenedor

```
docker rm mi_contenedor
```

### ¿Qué sucede al crear nuevamente el mismo contenedor con volumen de tipo host a los directorios definidos anteriormente?

Al crear nuevamente el mismo contenedor con el mismo volumen de tipo host, el contenido de la carpeta html en el sistema de archivos local se volverá a montar en el directorio vinculado del contenedor. Si se realizó cambios en los archivos mientras el contenedor estaba en ejecución, esos cambios se mantendrán.

### ¿Qué hace el comando pwd?

El comando pwd (print working directory) imprime el directorio de trabajo actual en el que te encuentras en tu terminal. Es útil para conocer la ruta completa de un directorio en tu sistema de archivos.

Si quieres incluir el comando pwd dentro de un comando de Docker, lo puedes hacer de diferentes maneras dependiendo del shell que estés utilizando.


### Volumen tipo host usando PWD y PowerShell
```
docker run -d --name <nombre contenedor> --publish published=<valorPuertoHost>,target=<valor> -v ${PWD}/<ruta relativa>:<ruta absoluta> <nombre imagen>:<tag> 
```

### Volumen tipo host usando PWD (Git Bash)

```
docker run -d --name <nombre contenedor> --publish published=<valorPuertoHost>,target=<valor> -v $(pwd -W)/html:/usr/share/nginx/html <nombre imagen>:<tag> 
```

### Volumen tipo host usando PWD (en Linux)

```
docker run -d --name <nombre contenedor> --publish published=<valorPuertoHost>,target=<valor> -v $(pwd)/html:/usr/share/nginx/html <nombre imagen>:<tag> 
```

