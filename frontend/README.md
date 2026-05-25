Documentación (README)

El proyecto esta construido sobre el stack MERN (MongoDB, Express, React, Node.js) y desplegado bajo una arquitectura de microservicios en la nube de Amazon Web Services (AWS).
Arquitectura de Software
Frontend (Capa de Presentacion): Desarrollado con React.js y empaquetado con Vite para maxima velocidad. El enrutamiento es manejado con react-router-dom y las peticiones HTTP son gestionadas a traves de axios.
Backend (Capa Logica): Construido con Node.js y Express.js. Es una API RESTful que procesa la logica de envios, autenticacion y contactos.
Base de Datos (Capa de Datos): MongoDB Atlas (Cloud Database). El modelado de datos se realiza mediante Mongoose utilizando los modelos User, Shipment y Contact.
Infraestructura Cloud (AWS)
Frontend Hosting: AWS Amplify con CI/CD conectado a GitHub.
Backend PaaS: AWS Elastic Beanstalk utilizando una instancia EC2 con un Application Load Balancer.
Seguridad: AWS Certificate Manager (ACM) para el cifrado SSL/TLS mediante HTTPS.
Redes y DNS: AWS Route 53 gestionando el dominio principal prograwebskyship.click y el subdominio de la API api.prograwebskyship.click.
Como ejecutar el proyecto (Local)
Para correr este proyecto en tu entorno local para desarrollo o pruebas, sigue estos pasos. Es necesario tener dos terminales abiertas simultaneamente (una para el frontend y otra para el backend).
Requisitos previos
Node.js (version 18 o superior recomendada)
Git
Una cadena de conexion valida de MongoDB Atlas
Configuracion del Backend
Abre una terminal y navega a la carpeta del servidor: cd backend npm install
Crea un archivo llamado .env en la raiz de la carpeta backend/ con las siguientes variables: MONGO_URI=mongodb://db_skyship:skyship123…..
JWT_SECRET=SKYSHIP_1201922_1273922 PORT=5000
Inicia el servidor: npm run dev El servidor correra en http://localhost:5000
Configuracion del Frontend
Abre una nueva terminal y navega a la carpeta del cliente: cd frontend npm install
Crea un archivo llamado .env en la raiz de la carpeta frontend/ con la siguiente variable apuntando a tu backend local: VITE_API_URL=http://localhost:5000
Inicia la aplicacion de React: npm run dev La aplicacion correra en http://localhost:5173
Decisiones Tecnicas Relevantes
Durante el desarrollo e implementacion de SkyShip Express, se tomaron las siguientes decisiones arquitectonicas para garantizar escalabilidad, seguridad y buenas practicas:
Desacoplamiento Front/Back: Se decidio separar fisicamente el codigo de React y el de Node.js en carpetas distintas. Esto permitio desplegar el Frontend en una CDN global (Amplify) para cargas rapidas, y el Backend en un entorno balanceado (Elastic Beanstalk), permitiendo escalar cada capa de forma independiente segun la demanda.
Autenticacion Stateless (JWT): En lugar de usar sesiones en memoria que limitan la escalabilidad del servidor, se implemento JSON Web Tokens (JWT). El token se almacena en el localStorage del cliente y se intercepta en el backend mediante un middleware personalizado que valida la firma criptografica antes de procesar cualquier transaccion en la base de datos.
Manejo de Variables de Entorno Dinamicas: Se utilizo import.meta.env (Vite) para evitar escribir en codigo fijo la URL de la API. Esto permite que el codigo funcione perfectamente en desarrollo (localhost) y que se adapte automaticamente al subdominio de produccion (api.prograwebskyship.click) sin modificar una sola linea de codigo en los commits.
Seguridad de Red (AWS): Se configuraron los Security Groups de AWS para que el Balanceador de Carga solo acepte trafico cifrado por el puerto 443 (HTTPS), rechazando conexiones no seguras. Adicionalmente, el backend en Express tiene configurado CORS (Cross-Origin Resource Sharing) para aceptar peticiones exclusivamente desde el dominio oficial del frontend.


Credenciales de Prueba
Para evaluar la plataforma, puedes utilizar los siguientes usuarios pre-configurados. Cada uno tiene asignado un rol especifico que condiciona las vistas and permisos dentro de la aplicacion.
Rol: Administrador
Tiene acceso al Panel de Control (/admin), puede cambiar estados de envio, eliminar guias, ver contactos comerciales y dar de baja usuarios.
Correo: luis@gmail.com
Contrasena: luis123456
Rol: Cliente
Tiene acceso unicamente a la cotizacion, generacion de guias y visualizacion de su propio historial de envios.
Correo: juan@gmail.com
Contrasena: juan123
