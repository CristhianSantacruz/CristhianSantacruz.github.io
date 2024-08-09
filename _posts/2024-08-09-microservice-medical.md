---
title : "Microservice Medico"
date : 2024-08-09
categories : [Api Clínica HealHub]
tags: [Backend,Quarkus,Java,Microservices,RestApi,Swagger,HealthCheck,RestClient,Microprofile]
---
# Microservicio para los Médicos

## Microservice Medical

Luego de la creación del microservicio de los pacientes, explicaré el de los médicos, el cual tiene el siguiente modelo:

![modeloEntidad](/assets/image/postmedicalmicroservice/modelo%20entidad.png)

Como podemos ver, tenemos un identificador único, nombre, especialización, correo, y cualificaciones, ya sea de un título, doctorado, etc., que este posea. Además, se incluye el departamento donde se encuentra o será asignado, y una lista de `historialMedico` que podrá guardar de los pacientes que estén en la consulta. Ya hablaré o crearé un post acerca del servicio de Historial Médico.

## Métodos o Recursos que Tendrán los Médicos

![imagen de Servicio](/assets/image/postmedicalmicroservice/metodos.png)

Como se muestra en la imagen, el médico podrá registrarse, obtener sus datos, y uno de los métodos permite traer los historiales médicos que haya creado o guardado. Esto se realiza con una comunicación con otro microservicio, que veremos más adelante. Otros métodos incluyen obtener al médico por email, obtener a todos los médicos, actualizar datos, agregar una nueva cualificación, eliminar un médico, y buscar por especialización, departamento, o cualificación. También se puede crear un historial médico.

## Comunicación con los Demás Servicios

Para comunicarnos con los demás servicios utilizamos "MicroProfile Rest Client", que es una especificación dentro del proyecto de Eclipse MicroProfile. Esta se centra en desarrollar microservicios basados en Java, permitiendo crear clientes HTTP tipo Rest de manera sencilla y declarativa utilizando interfaces en Java.

Vamos a analizar la comunicación con el microservicio encargado del historial médico.

![imagen](/assets/image/postmedicalmicroservice/client%20%20Historial%20Medical.png)

Aquí hay una anotación importante a tomar en cuenta: `@RegisterRestClient` permite que Quarkus sepa que esta interfaz está destinada a estar disponible para la inyección como un cliente Rest. Dentro de este tenemos un valor llamado `configKey`, que en pocas palabras tiene el enlace de donde se está ejecutando el microservicio de historial médico, como se puede ver en la siguiente imagen.

![imagen](/assets/image/postmedicalmicroservice/config%20keys.png)

También puedes usar `@RegisterRestClient(baseUri="http://localhost:8090")`.

Y ahí definimos los métodos que necesitamos o queremos que se comuniquen en nuestro servicio. Ahora, ¿cómo lo usamos? En el siguiente ejemplo podemos observarlo en acción:

![imagen](/assets/image/postmedicalmicroservice/client%20%20Historial%20Medical.png)

Vemos que está anotada como `@RegisterRestClient` y tenemos dos métodos con los cuales nos comunicaremos. Uno es para traer la lista de historial médico que los médicos hayan creado, ya que uno de los atributos del modelo de historial médico es el ID del médico que lo creó. El otro método es para crear el historial médico, con el ID del médico y los datos que se guardarán en el historial, que son los siguientes:

### `MedicalHistoryDtoRequest`

![imagen](/assets/image/postmedicalmicroservice/medicalhistoryrequestdto.png)

Tiene el ID del paciente, que básicamente es la cédula, el diagnóstico que se le dio, el tratamiento, unas notas adicionales, los medicamentos que necesite (o no), y cuándo debe volver para una nueva consulta.

Como podemos ver, tiene el ID del paciente, por lo que es importante que no solo se muestre el ID cuando se traigan los datos, sino también el nombre, edad y género del paciente.

Por eso también tenemos una comunicación con el microservicio del paciente, para obtener los datos del paciente, claro, solo los que necesitemos, no es necesario traer todos.

![imagenComunicacion](/assets/image/postmedicalmicroservice/client%20Patient.png)

![imagenPacienteDto](/assets/image/postmedicalmicroservice/dto%20patient.png)

## Ejemplo de Uso en Nuestro Servicio

Aquí un ejemplo de nuestro servicio que trae a un médico por ID, pero además trae el historial médico que él ha creado.

![imagenServicio](/assets/image/postmedicalmicroservice/metodo%20get%20ID.png)

Como podemos ver, la anotación `@Inject` es similar a `@Autowired` de Spring Boot para inyectar dependencias, y `@RestClient` es para inyectar instancias de clientes Rest que utilizan la especificación de MicroProfile Rest Client.

En el método del servicio utilizamos estos servicios de client Rest para traer el historial del médico y, del ID del paciente, traer los datos del paciente que especificamos en el `PacienteDto`, como se vería en este ejemplo:

![imagenEjemplo](/assets/image/postmedicalmicroservice/Ejemlpo%20del%20enpint%20get%20by%20id.png)

## Ejemplo de una Parte de Nuestro Controlador / Recurso para el Servicio de Médicos

![imagenController](/assets/image/postmedicalmicroservice/parte%20del%20resource.png)

Lo que vemos aquí es un método para guardar un médico, y el otro, que es más interesante, trae un médico por ID. Este endpoint es interesante por las siguientes anotaciones:

### `@FallBack` y `@Retry`

Estas son parte de la especificación de MicroProfile Fault Tolerance. Por lo general, cuando trabajamos con arquitectura de microservicios, es normal que un servicio llegue a caerse o no funcione correctamente, y estas anotaciones nos ayudan a manejar estos fallos y mejorar la tolerancia a errores.

- **`@FallBack`** se utiliza para tener un comportamiento alternativo cuando ocurra un error debido a una excepción. Nosotros podemos poner un método que nos respalde a ese fallo.
- **`@Retry`** se utiliza para que si hay un problema, este se vuelva a ejecutar dos veces para ver si el fallo es temporal. Podemos asignar cada cuánto tiempo hacer esto y cuántas veces repetir (por defecto son tres veces).

## Puntos de Salud

Como estamos comunicándonos con otros servicios, es necesario saber cuándo uno está caído. Aquí es donde nos ayudan los health checks en los recursos. Normalmente se tiene un endpoint que nos ayudará a saber si un servicio está funcionando, como en este ejemplo:

![imagenHealthCheckOk](/assets/image/postmedicalmicroservice/puntos%20de%20salud%20de%20los%20clientes.png)

### Cómo Crear Puntos de Salud

Para crear un punto de salud con el microservicio de historial médico, sigue este ejemplo:

![imagencodigo](/assets/image/postmedicalmicroservice/Healh%20Check%20al%20microservicio%20medical.png)

Traemos la ruta donde está la URL de nuestro servicio `medicalHistory` y creamos un método anotado con `@Readiness`, que es parte de la especificación de MicroProfile Health. Esta anotación indica si una instancia de la aplicación está lista para recibir tráfico, básicamente ayudándonos a decir si un servicio o base de datos está disponible. En este caso, visito el método `hello` del servicio para ver si obtengo un status 200 que me indicará que el servicio está funcionando.

En caso de que un servicio no funcione, lo verás de la siguiente manera:

![imagenHealthCheckError](/assets/image/postmedicalmicroservice/cuando%20uno%20falla.png)

## Documentación

Como siempre, documenta tus servicios para que otras personas puedan saber qué pueden obtener o realizar en tus endpoints.

![imagenSwagger](/assets/image/postmedicalmicroservice/documentacion.png)

Importante: en unos días se publicará el servicio de historial médico.

