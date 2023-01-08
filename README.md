
# INSTALACION

Antes de la instalacion se debe tener los siguientes requerimientos:

* docker
* docker compose
* liberar puertos: 8000, 9000

### Preparacion

Clonar el repositorio
```shell
git clone git@github.com:jjanampa/wallet.git
cd wallet
```

descargar repositorios complementarios ( git submodules)
```shell
git config core.fileMode false && git submodule init && git submodule update
```  

### Levantar servicios con docker compose ( puerto 80 libre)
levantar servicios
> la primera vez puede tardar
```shell
docker compose up -d --build
```

### Levantar api soap ( http://localhost:8000)
Agregar Configuracion:
```shell
docker compose exec soap sh -c 'cp .env.example .env'
```

Agregar configuracion para envio de email en .env

Instalar dependencias:
```shell
docker compose exec soap sh -c 'composer install'
```

Iniciar:
```shell
docker compose exec soap sh -c 'php artisan key:generate'
```

Ejecutar migrations:
```shell
docker compose exec soap sh -c 'php artisan migrate'
```

### Levantar api rest ( http://localhost:9000)
Agregar Configuracion:
```shell
docker compose exec rest sh -c 'cp .env.example .env'
```

Instalar dependencias:
```shell
docker compose exec rest sh -c 'composer install'
```



----------
----------

## *Nota*:
### Comandos comunes
* Levantar servicios y contenedores docker:
```shell 
docker compose up -d
```
* Detener la ejecución de los contenedores:
```shell 
docker compose stop
```
* Actualizar cambios en docker(reconstruir):
```shell 
docker compose stop && docker compose up -d --build
```

### Accesos
Los accesos a los recursos se obtienen de docker-compose.yml

* database:
    ```
    'hostname' => 'buskeros_mysql', (external : localhost)
    'database' => 'app',
    'username' => 'root',
    'password' => 'root',
    'port' => '3306', (external : 3309)
    ```
* phpmyadmin : (http://localhost:8183)

