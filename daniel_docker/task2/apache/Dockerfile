# Usar Ubuntu como imagen base
FROM ubuntu:20.04

# Evitar prompts interactivos durante la instalación de paquetes
ENV DEBIAN_FRONTEND=noninteractive

# Actualizar el sistema e instalar Apache, ca-certificates, openjdk-17-jre-headless, git, y curl
RUN apt-get update && \
    apt-get install -y --no-install-recommends \
        apache2 \
        ca-certificates \
        openjdk-17-jre-headless \
        git \
        curl && \
    # Limpiar el sistema para reducir el tamaño de la imagen
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

# Crear un usuario sin privilegios con un directorio de trabajo
RUN useradd -m -d /home/apacheuser -s /bin/bash apacheuser

# Cambiar al nuevo usuario
USER apacheuser

# Establecer el directorio de trabajo
WORKDIR /home/apacheuser

# Exponer el puerto 80 para tráfico HTTP
EXPOSE 80

# Iniciar Apache en modo foreground (necesario para que el contenedor siga ejecutándose)
CMD ["apachectl", "-D", "FOREGROUND"]
