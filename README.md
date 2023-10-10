# Contenerización de Aplicaciones .NET Core con Docker

## Tabla de Contenido

- [Creación de la imagen](#creación-de-la-imagen)
- [Ejecución del contenedor](#ejecución-del-contenedor)
- [Reconstrucción de la imagen](#reconstrucción-de-la-imagen)  
- [Docker Compose](#docker-compose)
- [Reconstruir con Docker Compose](#reconstruir-con-docker-compose)

## Creación de la imagen  

Para crear la imagen Docker debemos definir un Dockerfile. Aquí un ejemplo:

```
dockerfile
FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build-env  

WORKDIR /app

COPY . .  

EXPOSE 5054

ENTRYPOINT [\"dotnet\"]  
CMD [\"dotnet\", \"watch\", \"run\", \"--project\", \"app.csproj\"]  
```

Construimos la imagen:  

```
docker build -t dotnet-image -f Dockerfile.yml .
```

## Ejecución del contenedor   

Una vez tenemos la imagen, ejecutamos un contenedor:

```
docker run -dp 5054:5054 --name dotnet-container dotnet-image  
```

Esto expondrá el puerto 5054 del contenedor al 5054 del host y montará la aplicación.  


## Reconstrucción de la imagen 

Si realizamos cambios debemos reconstruir la imagen:

```
docker build --no-cache -t dotnet-image -f Dockerfile.yml .
```

Esto forzará una nueva build/construcción sin cache.

## Docker Compose   

Podemos definir la configuración en un docker-compose.yml:  

```
yaml
version: \"3.8\"

services:

  app:  
    image: dotnet-image   
    build:
      context: .
      dockerfile: Dockerfile.yml
    ports:
      - \"8000:5054\"
    volumes:
      - ./:/app
```

E iniciar con:   

```
docker-compose up -d   
```

## Reconstruir con Docker Compose

Forzar reconstrucción:

```
docker-compose up -d --build
```

Esto aplicará los últimos cambios.


### desmontar el stack del docker-compose

Para desmontar el stack:

```  
docker-compose down
```

## Fin  
