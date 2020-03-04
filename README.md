![Sentry](https://sentry-brand.storage.googleapis.com/sentry-logo-black.png)]

# sentry-docker-compose 

Permite orquestar y desplegar Sentry On-Premise con docker-compose utilizando los contenedores disponibles en
[Docker Hub](https://hub.docker.com/_/sentry/)

## Desplegar una instancia completa con docker-compose.yml

### Clonar el repositorio

```
$ git clone https://github.com/neotrons/sentry-docker-compose.git
$ cd sentry-docker-compose/
```

### Variables de entorno

Copiar y configurar los archivos de variables de entorno

```
$ cp envs/sentry.env.example envs/sentry.env
$ cp envs/psql.env.example envs/psql.env
```
Recuerda que si cambiar el usuario o clave de postgres se del archivo `envs/psql.env` se debe cambiar tambien en las variables de 
relacionadas al base de datos del archivo `envs/sentry.env`

### Genenado la sentry secret key

```
$ docker-compose run --rm sentry config generate-secret-key
```

Agregar la key resultante en la variable `SENTRY_SECRET_KEY` in `envs/sentry.env`.

### Inicializar la base de datos

Si es una nuva base de datos debemos ejecutar  `sentry upgrade`.

```
$ docker-compose run --rm sentry upgrade
```

En el proceso pedira crear el usuario administrador

### Iniciar Sentry

```
$ docker-compose up -d
```

Abrir el navegador en `http://localhost:9000`


### Iniciar con nginx

```
$ docker-compose -f docker-compose.yml -f docker-compose-nginx.yml up -d
```

Abrir el navegador en `http://localhost`
