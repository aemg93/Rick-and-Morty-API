# Prueba - README

## Project setup

Para configurar el proyecto, sigue los siguientes pasos:

```bash
yarn install
```

### Compiles and hot-reloads for development

Para compilar y recargar la aplicación en modo de desarrollo, utiliza el siguiente comando:

```bash
yarn serve
```

### Compiles and minifies for production

Si deseas compilar y minimizar la aplicación para su uso en producción, ejecuta el siguiente comando:

```bash
yarn build
```

### Lints and fixes files

Para analizar y corregir los archivos mediante ESLint, utiliza el comando:

```bash
yarn lint
```

### Customize configuration

Para personalizar la configuración de la aplicación, puedes consultar la [Referencia de Configuración](https://cli.vuejs.org/config/).

## Dependencias

- Axios: Biblioteca para realizar solicitudes HTTP y acceder a la API de Rick and Morty.
- Boxicons: Conjunto de iconos vectoriales utilizados en la interfaz del proyecto.
- Bootstrap: Framework CSS utilizado para el diseño y la estructura de la aplicación.

## Descripción del proyecto

Este proyecto utiliza Vue.js para crear una aplicación que muestra información sobre los personajes de la serie Rick and Morty. La aplicación consume la API de Rick and Morty utilizando Axios para realizar solicitudes HTTP y obtener los datos de los personajes.

La interfaz de la aplicación utiliza los iconos de Boxicons y el framework CSS Bootstrap para un diseño atractivo y responsivo.

## Ejecución con Docker

Si deseas ejecutar esta aplicación con Docker, asegúrate de tener Docker instalado en tu sistema y sigue estos pasos:

1. Construye la imagen de Docker utilizando el siguiente comando en el directorio raíz del proyecto:

   ```bash
   docker build -t vue-app .
   ```

2. Una vez que la imagen se haya construido, puedes ejecutar la aplicación en un contenedor Docker con el siguiente comando:

   ```bash
   docker run -p 8000:8080 vue-app
   ```

La aplicación estará disponible en http://localhost:8000.

¡Disfruta utilizando nuestra aplicación con Docker!