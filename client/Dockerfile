# --------------[ ETAPA DE ARMADO DE LOS RECURSOS ]--------------
# Le decimos a docker con qué crear la imagen y la nombramos build
FROM node:20 AS build

# Establecemos el directorio de trabajo de la imagen
WORKDIR /app

# Copiamos los package de nuestro proyecto al directorio de trabajo
# package.json
# package-lock.json
COPY package*.json ./

# Instalamos los paquetes de node
RUN npm install

# Y copiamos todo lo demas
COPY . .

# Para finalizar construyendo el proyecto
RUN npm run build

# --------------[ ETAPA DE ARMADO DE LA IMAGEN ]--------------
# Le decimos a docker que cree la imagen con un nginx
FROM nginx:alpine

# Copiamos los recursos de la etapa anterior almacenados en la fase de build a la carpeta de nginx
COPY --from=build /app/dist /usr/share/nginx/html

# Exponemos la imagen en un puerto
EXPOSE 80

# Y le decimos los comandos para correr el nginx
CMD ["nginx", "-g", "daemon off;"]