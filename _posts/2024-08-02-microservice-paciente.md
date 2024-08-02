---
title : "Microservice Paciente"
date : 2024-08-02
categories : [Api Clínica HealHub]
tags: [Backend,Quarkus,Java,Microservices,RestApi,Swagger,HealthCheck,Metrics]
---

# Microservicio Paciente

Este servicio nos permite manejar y utilizar los datos de los usuarios. Podemos guardar pacientes, consultar a un paciente por su DNI, por su email, actualizar los datos de los usuarios, actualizar el número de teléfono, además de consultar a los pacientes que solo están activos y/o por su tipo de imagen y eliminar a un usuario.

## Funcionalidades

- Guardar pacientes
- Consultar a un paciente por su DNI
- Consultar a un paciente por su email
- Actualizar los datos de los usuarios
- Actualizar el número de teléfono
- Consultar a los pacientes activos
- Consultar a los pacientes por su tipo de imagen
- Eliminar a un usuario

## Arquitectura

Estamos utilizando Consul para manejar los key/values de la base de datos MongoDB. Consul nos ayuda a conectarnos de forma segura a las aplicaciones.

![Consul](/assets/image/postpacientemicroservice/consul%20registro%20de%20la%20conexion%20a%20la%20base%20de%20datos.png)

### Modelo de Paciente

El modelo de nuestro paciente es el siguiente. Hacemos validaciones de algunos de nuestros atributos, como el DNI, que no puede ser nulo ni estar vacío, entre otros. Además, lo anotamos como una entidad de MongoDB que se guarda en la colección `patient`.

![Modelo Paciente](/assets/image/postpacientemicroservice/modelo%20paciente.png)

### Manejo de Excepciones

Para manejar las excepciones de manera sencilla para el usuario, creamos un `ExceptionMapper` que envía una respuesta con un estado de 404 y el tipo de `ConstraintViolation` que se ha realizado en formato JSON.

![ExceptionMapper](/assets/image/postpacientemicroservice/paciente%20mapper.png)

Ejemplo de respuesta:

![Ejemplo de Respuesta](/assets/image/postpacientemicroservice/example%20exception.png)

## Documentación de Paciente

La documentación se realiza con Swagger. Las configuraciones generales de Swagger se realizan en el archivo `application.properties`.

![Swagger Configuration](/assets/image//postpacientemicroservice/swaagger%20data.png)

Así es como se visualiza en la interfaz:

![Swagger UI](/assets/image/postpacientemicroservice/documentacion%20de%20pacientes.png)

## Chequeos de Salud

Por defecto, cuando tenemos la dependencia de chequeos de salud en Quarkus, ya se levantan algunos chequeos. Por ejemplo, si estamos usando la base de datos MongoDB, se levantará un chequeo que nos indicará si está lista para usarse. También podemos crear nuestros propios `HealthCheck`.

Ejemplo de `SimpleHealthCheck`:

![SimpleHealthCheck](/assets/image/postpacientemicroservice/health%20code.png)

Quarkus ofrece muchas herramientas, una de ellas es `/health-ui`, que nos muestra qué servicios están levantados.

![HealthCheck UI](/assets/image/postpacientemicroservice/health%20ui.png)

## Controlador

Vamos a analizar algunos extractos de las imágenes de nuestro `resource` o controlador de pacientes.

![Controlador 1](/assets/image/postpacientemicroservice/extracto%20controller%201.png)

En esta primera imagen vemos algunas anotaciones:

- `@Operation`: Esta es una anotación de OpenAPI que nos ayuda a agregar información y un resumen a nuestro endpoint para brindar una explicación detallada.
- `@Counted`: Es una anotación de métrica que nos ayuda a tener un conteo de cuántas veces se utiliza este endpoint.
- `@Timed`: Otra métrica que nos ayuda con el tiempo que tomó en dar un resultado.

![Controlador 2](/assets/image/postpacientemicroservice/extracto%20controller%202.png)

Lo diferente aquí es la anotación `@Metered` del endpoint que actualizará el número de teléfono del usuario. Esta anotación es otra manera en la que podemos medir la eficiencia de la respuesta que tiene ese endpoint.

Finalmente, las métricas se visualizan de la siguiente manera:

![Métricas](/assets/image/postpacientemicroservice/metricas.png)
