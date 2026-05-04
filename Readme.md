Para clonar todo por primera vez:
git clone --recursive https://github.com/tu-usuario/MS_Metarepo.git

Para actualizar todos los microservicios a su última versión:
git submodule update --remote --merge

Prompt:
Eres un desarrollador de software experto en NodeJS, NestJS, Docker Hub, PostgreSQL, NATS (https://nats.io/), Git, GitHub, GitHub Actions, WSO2 como API Manager, VPS (Contabo) como hosting y React para desarrollo del frontend con Tankstack Query. Me ayudarás a crear una solución de software basada en una arquitectura de microservicios donde uno de estos microservicios será una implementación de Keycloak como IDM/IAM para resolver la autenticación y autorización de usuarios de mi aplicativo, donde desarrollaremos un tema de login personalizado. Otro microservicio será una implementación de WSO2 como API manager. Otro microservicio será un desarrollo de una API Restfull en NestJS que se utilizará para interactuar con los microservicios que se desarrollen dentro de la aplicación. Un microservicio más que será el frontend de la aplicación desarrolada en React que en principio tendrá una pantalla de login (proveniente de Keycloak) para autenticar al usuario y registrar nuevos usuarios, una pantalla central para usuarios autenticados con un menú con una sola opción que llevará a la página de gestión de usuarios y un encabezado con un título "Mi aplicación" a la izquierda y un ícono representativo del usuario registrado a la derecha donde se permita acceder al perfil y editar datos personales como nombre, apellido, teléfono, foto de perfil, etc. Utilizaremos imágenes de docker y Docker Compose como orquestador y Docker Hub como registry de las imágenes generadas. Las imágenes las generará el GitHub Actions de cada repositorio y las subirá a Docker Hub. El resguardo del desarrollo en repositorios se realizará en Github, no utilizaremos monorepo sino que se creará un repositorio por cada microservicio y tendremos un repositorio central (Metarepo) basado en una Arquitectura de Repositorios Distribuidos. El repositorio central tendrá referencias a todos los demás repositorios de microservicios que componen la aplicación.


Despliegue de aplicación:
docker compose up -d

Para detener los contenedores:
docker compose stop (Los contenedores se detienen pero no se borran. No pierdes nada, incluso sin volúmenes. Es como apagar la computadora.)
docker compose down (Los contenedores se detienen y se eliminan.)
docker compose down -v (El flag -v borra incluso los volúmenes. Úsalo solo si quieres resetear todo el proyecto de cero.)

Para bajar las imágenes:
docker compose pull

Exportar/Importar configuración Keycloak:
docker exec keycloak /opt/keycloak/bin/kc.sh export --realm Quasar_Solutions --file /tmp/Quasar_Solutions-realm.json
docker cp keycloak:/tmp/Quasar_Solutions-realm.json ./MS_Keycloak/config/


Servicio.   Acceso Externo (Tu navegador).   Acceso Interno (Entre contenedores)
Keycloak.   localhost:8087                   keycloak:8080
NestJS API  localhost:3017                   ms_auth:3000
Frontend.   localhost:80                     ms_frontend:80
Postgres.   No mapeado                       postgres_iam:5432

