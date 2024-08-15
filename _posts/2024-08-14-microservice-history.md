---
title : "Microservice History Medical"
date : 2024-08-02
categories : [Api Clínica HealHub]
tags: [Backend,Quarkus,Java,Microservices,RestApi,Swagger,HealthCheck,Metrics]
---

## Microservicio de Historial Médico

Este post será breve ya que la principal utilidad de este servicio es comunicarse con el microservicio de médicos, el cual ya está publicado.

### Microservicio Médico

[Enlace al microservicio de médicos](https://cristhiansantacruz.github.io/posts/microservice-medical/) <!-- Aquí puedes insertar el link real -->

### Entidad

![Entidad Historial Médico](/assets/image/posthistorymicroservice/entity.png)

Podemos observar que un historial médico incluirá el ID del médico y el ID del paciente. Esto es importante para que tanto los médicos como los pacientes puedan ver sus historiales. En el historial se pueden registrar diagnósticos, tratamientos, medicamentos (en caso de que se requieran), y notas importantes. Además, se puede programar la fecha para la siguiente cita con el paciente.

### Servicio

![Diagrama del Servicio](/assets/image/posthistorymicroservice/methods%20service.png)

Los métodos o endpoints que tendrá nuestro microservicio son los siguientes:

- **Crear un historial médico**
- **Obtener un historial médico por su ID**
- **Obtener todos los historiales**
- **Obtener el historial por ID de paciente**
- **Obtener el historial por ID de médico**
- **Actualizar datos de un historial**
- **Eliminar un historial**

El método más importante podría ser el `createMedicalHistory`. Este método realiza lo siguiente:

![Implementación del Servicio](/assets/image/posthistorymicroservice/implements%20service.png)

El método recibe al médico que desea crear el historial y los datos del historial. Realiza algunas validaciones, como verificar si los medicamentos están vacíos o si no se ha recetado ningún tipo de medicamento al paciente, en cuyo caso se muestran vacíos.

### Recurso

Nuestros endpoints más utilizados en el microservicio serían los siguientes:

![Endpoints del Recurso](/assets/image/posthistorymicroservice/resources.png)

Los endpoints más utilizados serían para obtener la lista de historiales de pacientes y médicos, ya que es común que los pacientes revisen sus recetas o notas pasadas, y que los médicos revisen el historial de un paciente.


[imagenPost](/assets/image/posthistorymicroservice/post.png)

Y el metodo para crear el medico que este se estara comunicandoo con el microservicio medico utilizando las espeficicancion de Rest Client de Microprofile.