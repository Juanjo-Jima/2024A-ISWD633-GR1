## Esquema para el ejercicio
![Imagen](imagenes/esquema-ejercicio3.PNG)

### Crear red net-wp

```
docker network create net-wp
```

### Listar todas las redes disponibles en Docker:

```
docker network ls
```

### Conectar un contenedor a la red net-wp, se puede utilizar los siguientes comandos al crear el contenedor:

### Explicación

```
docker run -d --name mi_contenedor --network net-wp imagen_contenedor
```

### Comando 1

```
docker run -d --name mysql --network net-wp -e MYSQL_ROOT_PASSWORD=wordpress -e MYSQL_DATABASE=wordpress -e MYSQL_USER=wordpress -e MYSQL_PASSWORD=wordpress -v C:/ejercicio3/db:/var/lib/mysql mysql:8
```

### Comando 2

```
docker run -d --name wordpress --network net-wp -e WORDPRESS_DB_HOST=mysql:3306 -e WORDPRESS_DB_USER=wordpress -e WORDPRESS_DB_PASSWORD=wordpress -e WORDPRESS_DB_NAME=wordpress -p 9500:80 -v C:/ejercicio3/www/html:/var/www/html wordpress
```

### Para que persista la información es necesario conocer en dónde mysql almacena la información.
# COMPLETAR LA SIGUIENTE ORACIÓN. REVISAR LA DOCUMENTACIÓN DE LA IMAGEN EN https://hub.docker.com/)
En el esquema del ejercicio la carpeta contenedor (a) es "/var/lib/mysql"
Ruta carpeta host: .../ejercicio3/db

### ¿Qué contiene la carpeta db del host?

La carpeta db del host se encuentra vacia.

### Crear un contenedor con la imagen mysql:8  en la red net-wp, configurar las variables de entorno: MYSQL_ROOT_PASSWORD, MYSQL_DATABASE, MYSQL_USER y MYSQL_PASSWORD

```
docker run -d --name mysql-container --network net-wp -v C:\Users\pilco\Desktop\ejercicio3\db:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=root_password -e MYSQL_DATABASE=wordpress -e MYSQL_USER=wordpress_user -e MYSQL_PASSWORD=wordpress_password mysql:8
```

### ¿Qué observa en la carpeta db que se encontraba inicialmente vacía?

Ahora la carpeta db del host contiene los archivos db relacionados de la base de datos de MYSQL.

### Para que persista la información es necesario conocer en dónde wordpress almacena la información.
# COMPLETAR LA SIGUIENTE ORACIÓN. REVISAR LA DOCUMENTACIÓN DE LA IMAGEN EN https://hub.docker.com/)
En el esquema del ejercicio la carpeta contenedor (b) es "/var/www/html"
Ruta carpeta host: .../ejercicio3/www

### Crear un contenedor con la imagen wordpress en la red net-wp, configurar las variables de entorno WORDPRESS_DB_HOST, WORDPRESS_DB_USER, WORDPRESS_DB_PASSWORD y WORDPRESS_DB_NAME (los valores de estas variables corresponden a los del contenedor creado previamente)

```
docker run -d --name wordpress-container --network net-wp -v C:\Users\pilco\Desktop\ejercicio3\www:/var/www/html -e WORDPRESS_DB_HOST=mysql-container -e WORDPRESS_DB_USER=wordpress_user -e WORDPRESS_DB_PASSWORD=wordpress_password -e WORDPRESS_DB_NAME=wordpress -p 8080:80 wordpress
```

### Personalizar la apariencia de wordpress y agregar una entrada

### Eliminar el contenedor y crearlo nuevamente, ¿qué ha sucedido?

Cuando se elimina y se vuelve a crear el contenedor en WordPress, se perderá todas las modificaciones que se haya hecho en él, ya que los datos se guardan dentro del contenedor y se borran cuando se elimina. Sin embargo, la información almacenada en la base de datos MySQL seguirá existiendo debido al volumen montado. Esto significa que al recrear el contenedor de WordPress, podrás acceder al sitio nuevamente, pero es probable que se tenga que reconfigurar o reinstalar cualquier cambio o personalización que se haya realizado anteriormente.







