# NOTAS DE INSTALACIÓN

Instalación de .NET SDK (dotnet) en Linux Mint, aplica para las distribuciones basadas en Debian

## Agregar las keys de Microsoft

[https://learn.microsoft.com/en-us/answers/questions/1659853/the-repository-https-packages-microsoft-com-ubuntu](https://learn.microsoft.com/en-us/answers/questions/1659853/the-repository-https-packages-microsoft-com-ubuntu)

```
wget -qO- https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > packages.microsoft.gpg
sudo install -D -o root -g root -m 644 packages.microsoft.gpg /etc/apt/keyrings/packages.microsoft.gpg
rm -f packages.microsoft.gpg
```

## Agregar Repositorio Microsoft

[https://learn.microsoft.com/en-us/linux/packages](https://learn.microsoft.com/en-us/linux/packages)  
Si bien es cierto Linux Mint está basado en ubuntu 24, este repositorio solo tiene el sdk de .NET 8, por lo cual aún a inicios de 2025 se puede instalar .NET 6/7/8/9 usando el repositorio destinado a ubuntu 22.04

```
curl -sSL -O https://packages.microsoft.com/config/ubuntu/22.04/packages-microsoft-prod.deb
sudo dpkg -i packages-microsoft-prod.deb
rm packages-microsoft-prod.deb
sudo apt-get update
```

## Instalar .NET
Instalar el SDK de .NET 8
```
sudo apt-get install -y dotnet-sdk-8.0
```

## Agregar snapd
Con snap podemos agregar diversas aplicaciones en un entorno aislado, es la forma más rápida de instalar aplicaciones como VS Code o Rider para poder desarrollar en .NET
```
sudo rm /etc/apt/preferences.d/nosnap.pref
sudo apt update
sudo apt install snapd
sudo systemctl enable --now snapd apparmor
```
En caso no se inicien los servicios directamente, se puede usar:
```
sudo systemctl start snapd.service snapd.apparmor
```

## Instalar VS Code
```
snap install code --classic
```

- Extensiones recomendadas
    - .NET Extension Pack
    - C# Dev Kit
    - vscode-solution-explorer
    - Nuget Package Source
    - Visual Nuget

## Instalar Rider
Editor avanzando para .NET de Jet Brains, tiene una versión Community sin costo
```
snap install rider --classic
```

## Confiar en Certificado local de .NET
Antes de ejecutar por primera vez nuestra aplicación en dotnet, debemos aceptar la confianza en el certificado local generado para poder correr levantar la aplicación web usando https
```
dotnet dev-certs https --trust
```


## Comandos básicos de .NET
[https://learn.microsoft.com/en-us/dotnet/core/tools/](https://learn.microsoft.com/en-us/dotnet/core/tools/)  

`dotnet run`: Ejecutar  
`dotnet build`: Compilar  
`dotnet watch`: Ejecutar recompilando automaticamente ante algún cambio
