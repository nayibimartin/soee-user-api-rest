# SOEE USER API REST
El proyecto esta enfocado en resolver el ejercicio propuesto por SOEE, donde se deben desarrollar las tres funcionalidades siguientes:
1. `Alta de usuario`: Consiste en la creación de nuevos usuarios.La aplicación tendrá dos opciones para el almacenamiento de los usuarios:
    - Persistente: Los usuarios se almacenarán en una base de datos, en archivo o en cualquier otra solución de 
    persistencia que se elija.
    - Volátil: Los usuarios serán almacenados en memoria (ejemplo, sesión).

2. `Autenticación de usuario`: Validará las credenciales introducidas por el usuario, mostrando errores oportunos (las credenciales no son correctas, no se ha indicado el campo de email o es incorrecto su formato y no se ha indicado el campo de contraseña). Si la validación es correcta, se mostrará el listado de usuarios.

3. `Listado de usuarios`: Se listarán los usuarios dados de alta para comprobar que todo funciona correctamente. 

Para dar solución al ejercicio planteado de documentó la Api Rest empleando `Open API Swagger`, y para el desarrollo se utilizaron, como lenguaje de programación `Java`, y los frameworks `Spring Boot`, `Spring Security` y `Spring JPA`. El almacenanamiento de los datos podrá realizarse persistentemente a través de `PostgreSQL` o en memoria con `H2`. Se realizaron pruebas utilizando la herramienta `Postman` y pruebas unitarias automatizadas haciendo uso de los frameworks `JUnit` y `Mockito`. Para la estructuración del proyecto se definió una `Arquitectura Hexagonal` siguiendo el enfoque `Domain Driver Design`, lo que permitió la utilización de patrones como: Repository, Adapter, Entity, Service y Factory, así como el empleo de los principios `SOLID`. Se empleó el framework `Hateoas` para el manejo de los recursos a través de hipermedia, para la optimizacion y rendimiento de las respuestas se empleó compresión `GZip` y `HTTP/2` a partir de configuraciones en el archivo `application.properties` del proyecto.

## Despliegue
1. Como IDE de desarrollo se emplea `Intellij IDEA`. Descargar [aquí](https://www.jetbrains.com/es-es/idea/download/).
     - Instalar en el IDE el plugin `Lombok`. Para Intellij descargar [aquí](https://plugins.jetbrains.com/plugin/6317-lombok/). 
   
2. Para gestionar las dependencia se emplea `MAVEN`. Descargar [aquí](https://maven.apache.org/download.cgi/).

    - El `pom/xml` contiene todas las dependencias que deben ser descargadas para el despliegue de este proyecto.
      
3. Para la persistencia en memoria se emplea `H2`. 
    - Descargar para Windows [aquí](https://h2database.com/h2-setup-2019-03-13.exe)
    - Descargar para Linux [aquí](https://h2database.com/h2-2019-03-13.zip). Puede seguir esta guía [aquí](https://o7planning.org/11895/install-h2-database-and-use-h2-console)
    - Puede modificar la configuración de H2 como nombre de la base de datos, puerto y host mediante el `aplication.properties`

4. Para la persistencia en base de datos se emplea `PostgreSQL`. 

5. `Postman` para probar los endpoint de las APIs. Descargar [aquí](https://www.postman.com/downloads/).

6. Debe tener libre el puerto 8082 o modificar la variable `server.port` en el archivo `aplication.properties` del proyecto

## Persitencia
Para poder seleccionar el modo de almacenamiento de dispone de la variable de configuración `app.persistence.type` ubicada en el `application.properties`.
la aplicación trabaja de un modo o de otro, no utiliza los dos de forma simultánea.

- Activar la persistencia en memoria: `app.persistence.type=memory`
- Activar la persistencia en base de datos: `app.persistence.type=db`

En ambos casos podrá configurar los puertos y datos de conexión:
- Para H2:

        db.name=users
        db.h2.username=sa
        db.h2.password=

- Para postgres:
    
        db.sql.username=postgres
        db.sql.password=postgres
        db.sql.port=5432

## Restricciones y endpoints
La solución consta de 3 endpoints fundamentales.

Endpoint #1 Alta de usuario
 - POST /soee/v1/users
 - Ejemplo: http://127.0.0.1:8082/soee/v1/users
  
Endpoint #2 Autenticación de usuario
 - POST /soee/v1/authentication
 - Ejemplo: http://127.0.0.1:8082/soee/v1/authentication
   
   
Endpoint #3 Listado de usuarios
 - GET /soee/v1/users
 - Ejemplo: http://127.0.0.1:8082/soee/v1/users

Se desarrollaron otros endpoints que se encuentan documentados con open-api/swagger:
- Una vez que el proyecto esté corriendo, podrá acceder a la documentación mediante el enlace:

`http://localhost:8082/soee-users-api-docs`

## Testing
Se implementaron `test` para las funcionalidades principales del ejercicio.
   
