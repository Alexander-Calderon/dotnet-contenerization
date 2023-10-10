# Publicación de una aplicación web ASP.NET

```display
Copyright (C)  2023  JOSÉ DANIEL RODRÍGUEZ CHINCHILLA.
Permission is granted to copy, distribute and/or modify this document
under the terms of the GNU Free Documentation License, Version 1.3
or any later version published by the Free Software Foundation;
with no Invariant Sections, no Front-Cover Texts, and no Back-Cover Texts.
A copy of the license is included in the section entitled "GNU
Free Documentation License".
```

## Prerrequisitos

Antes de publicar y desplegar tu aplicación, necesitarás tener instalados en tu sistema el SDK y el runtime de ASP.NET. Es importante mencionar que para publicar tu aplicación necesitas el SDK, mientras que para simplemente ejecutar la API necesitarás el runtime.

1. **SDK de .NET:**
   - [Descargar SDK de .NET 7.0](https://dotnet.microsoft.com/es-es/download/dotnet/7.0)

2. **ASP.NET Runtime:**

    - **En Windows:**
        Utiliza el siguiente comando para instalar el ASP.NET runtime a través de Winget:

        ```shell
        winget install Microsoft.DotNet.AspNetCore.7
        ```

    - **En Ubuntu:**
        Utiliza los siguientes comandos para instalar el SDK y el runtime de ASP.NET:

        ```shell        
        sudo apt-get update && \
        sudo apt-get install -y aspnetcore-runtime-7.0
        ```
3. **Winget:**
    - Si no tienes Winget instalado en tu sistema, puedes descargarlo desde [GitHub](https://github.com/microsoft/winget-cli/releases).

## Publicación

La publicación de tu aplicación ASP.NET puede requerir especificar un identificador de tiempo de ejecución (Runtime Identifier, RID) dependiendo del sistema operativo destino. Puedes hacer esto de dos maneras: modificando el archivo `.csproj` de tu proyecto o mediante un flag al momento de publicar.

### Especificando el RID en el archivo `.csproj`

1. Abre el archivo `.csproj` de tu proyecto en un editor de texto.
2. Agrega la siguiente línea dentro del elemento `<PropertyGroup>` para Linux o Windows, según corresponda:

    ```xml
    <!-- Para Linux -->
    <RuntimeIdentifier>linux-x64</RuntimeIdentifier>

    <!-- Para Windows -->
    <RuntimeIdentifier>win-x64</RuntimeIdentifier>
    ```

3. Guarda y cierra el archivo `.csproj`.
4. Ahora puedes publicar tu proyecto normalmente usando el comando `dotnet publish -c Release --self-contained false`.

### Especificando el RID mediante un flag

1. Abre una terminal.
2. Usa el siguiente comando para publicar tu proyecto especificando el RID para Linux o Windows, según corresponda:

    ```shell
    # Para Linux
    dotnet publish -c Release -r linux-x64 --self-contained false
    
    # Para Windows
    dotnet publish -c Release -r win-x64 --self-contained false
    ```

#### Explicación de las flags adicionales

- `-c Release`: Esta flag especifica la configuración de la compilación. En este caso, `Release` indica una compilación de release, que está optimizada para el rendimiento y no incluye información de depuración.

- `--self-contained false`: Esta flag indica si la publicación será autocontenida o no. Una publicación autocontenida incluye todo lo necesario para ejecutar la aplicación, incluyendo el runtime de .NET. Especificar `false` significa que la publicación no será autocontenida, y se espera que el runtime de .NET esté instalado en el sistema destino.

Ambos métodos son válidos y puedes elegir el que prefieras según tu flujo de trabajo. Especificar el RID en el archivo `.csproj` puede ser útil si siempre vas a publicar para el mismo sistema operativo, mientras que usar un flag permite cambiar el RID fácilmente en cada publicación.

## Despliegue

Una vez que hayas publicado tu aplicación, el siguiente paso es desplegarla en el servidor o en la máquina destino. A continuación, se presentan los pasos para desplegar tu aplicación en Linux y Windows.

### Despliegue en Linux

1. Abre una terminal.
2. Navega a la carpeta donde se publicó tu aplicación. Por ejemplo:

    ```shell
    cd API/bin/Release/net7.0/linux-x64/publish/
    ```

3. Ejecuta el siguiente comando para desplegar tu aplicación:

    ```shell
    dotnet API.dll
    ```

### Despliegue en Windows

1. Abre una terminal o el Símbolo del sistema.
2. Navega a la carpeta donde se publicó tu aplicación. Por ejemplo:

    ```shell
    cd API\bin\Release\net7.0\win-x64\publish\
    ```

3. Ejecuta el siguiente comando para desplegar tu aplicación:

    ```shell
    dotnet API.dll
    ```

Estos pasos deberían ayudarte a desplegar tu aplicación en Linux y Windows. Asegúrate de tener el runtime de .NET instalado en la máquina destino, ya que es necesario para ejecutar tu aplicación.

## Videodemo

[![asciicast](https://asciinema.org/a/613089.svg)](https://asciinema.org/a/613089)

## License

This project is licensed under the [GNU Free Documentation License v1.3](https://www.gnu.org/licenses/fdl-1.3.html) - see the [LICENSE](LICENSE) file for more details.
