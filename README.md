Kuichi
======

Breve guía para obtener el paquete oficial desde las Releases de GitHub y ejecutar el proyecto localmente. Descargar desde Releases evita problemas con submódulos y metadatos .git.

Descargar desde Releases
------------------------

1.  Abre: https://github.com/AelStGermain/kuichi/releases

2.  Descarga la última Release (por ejemplo kuichi-v1.0.0.zip).

3.  Descomprime y entra en la carpeta del proyecto:

bash

```
unzip kuichi-v1.0.0.zip -d kuichi
cd kuichi

```

Requisitos
----------

-   Java 11 o superior y Maven o Gradle

-   Node 16 o superior y npm

-   Angular CLI opcional: `npm install -g @angular/cli`

-   Git solo si decides usar el repositorio en lugar de la Release

Backend arranque local
----------------------

1.  Ir a la carpeta backend:

bash

```
cd backend

```

1.  Revisar y ajustar variables en `src/main/resources/application.yml` o `application.properties` como base de datos o JWT secret.

2.  Ejecutar en desarrollo:

bash

```
./mvnw spring-boot:run

```

o empaquetar y ejecutar:

bash

```
./mvnw clean package -DskipTests
java -jar target/*.jar

```

1.  Endpoints principales

-   API base `http://localhost:8080/api`

-   Pets `GET /api/pets/mine` `POST /api/pets` `PUT /api/pets/{id}` `DELETE /api/pets/{id}`

-   Auth en `/api/auth/**`

Notas

-   En desarrollo permita CORS para `http://localhost:4200` si arranca el frontend con `ng serve`.

Frontend arranque local
-----------------------

1.  Ir a la carpeta frontend:

bash

```
cd frontend
npm install

```

1.  Levantar servidor de desarrollo:

bash

```
ng serve --open

```

-   La app por defecto queda en `http://localhost:4200`.

-   Si cambia el puerto o URL del backend, actualiza `src/environments/*.ts`.

Usuario de prueba
-----------------

-   Hay un usuario de prueba cargado por el seeder. Usuario sugerido **sofi**.

-   Revisa la clase `DataSeeder` o `DataLoader` en el backend para obtener usuario y contraseña exactos.

-   Ejemplo de uso con curl:

bash

```
# Login obtener token
curl -H "Content-Type: application/json" -d '{"username":"sofi","password":"<PASSWORD>"}' http://localhost:8080/api/auth/login

# Crear mascota usando token
curl -H "Authorization: Bearer <TOKEN>" -H "Content-Type: application/json"\
  -d '{"name":"Kira","species":"perro","note":"prueba"}' http://localhost:8080/api/pets
```
