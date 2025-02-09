# NOTAS DE INSTALACIÓN

Instalación de dotnet en Linux Mint, aplica para las distribuciones basadas en Debian

## Agregar las keys de Microsoft

[https://learn.microsoft.com/en-us/answers/questions/1659853/the-repository-https-packages-microsoft-com-ubuntu](https://learn.microsoft.com/en-us/answers/questions/1659853/the-repository-https-packages-microsoft-com-ubuntu)

```
wget -qO- https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > packages.microsoft.gpg
sudo install -D -o root -g root -m 644 packages.microsoft.gpg /etc/apt/keyrings/packages.microsoft.gpg
rm -f packages.microsoft.gpg
```

## Agregar Repositorio Microsoft

[https://learn.microsoft.com/en-us/linux/packages](https://learn.microsoft.com/en-us/linux/packages)
Si bien es cierto linux Mint está basado en ubuntu 24, esta solo tiene el sdk de dotnet-8, por lo cual aún a inicios de 2025 se puede instalar usando el repositorio destinado a ubuntu 22.04

```
curl -sSL -O https://packages.microsoft.com/config/ubuntu/22.04/packages-microsoft-prod.deb
sudo dpkg -i packages-microsoft-prod.deb
rm packages-microsoft-prod.deb
sudo apt-get update
```

## Instalar Dotnet
Instalar el SDK
```
sudo apt-get install -y dotnet-sdk-8.0
```

## Agregar snapd
Con snap podemos agregar diversas aplicaciones en un entorno aislado
```
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

## Confiar en Certificado local de dotnet
Antes de ejecutar por primera vez nuestra aplicación en dotnet, debemos aceptar la confianza en el certificado local generado para poder correr levantar la aplicación web usando https
```
dotnet dev-certs https --trust
```
