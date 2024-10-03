# Usar Ubuntu como imagen base
FROM ubuntu:20.04

# Evitar prompts interactivos durante la instalación de paquetes
ENV DEBIAN_FRONTEND=noninteractive

# Actualizar el sistema e instalar Nginx, ca-certificates, openjdk-17-jre-headless, git, y curl
RUN apt-get update && \
    apt-get install -y --no-install-recommends \
        nginx \
        ca-certificates \
        openjdk-17-jre-headless \
        git \
        curl && \
    # Limpiar el sistema para reducir el tamaño de la imagen
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

# Crear un usuario sin privilegios con un directorio de trabajo
RUN useradd -m -d /home/nginxuser -s /bin/bash nginxuser

# Cambiar al nuevo usuario
USER nginxuser

# Establecer el directorio de trabajo
WORKDIR /home/nginxuser

# Exponer el puerto 80 para tráfico HTTP
EXPOSE 80

# Comando para iniciar Nginx en modo foreground (necesario para que el contenedor no se detenga)
CMD ["nginx", "-g", "daemon off;"]