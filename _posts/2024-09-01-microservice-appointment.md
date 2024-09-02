---
title : "Microservice Medical Appointment"
date : 2024-09-01
categories : [Api Clínica HealHub]
tags: [Backend,Quarkus,Java,Microservices,RestApi,Swagger,HealthCheck,Metrics]
---

# 🚀 ¡Volvemos al Desarrollo! 🚀

Después de un breve retraso debido a responsabilidades estudiantiles, ¡estamos de regreso y listos para continuar con el desarrollo de nuestro **Microservicio de Citas**! 🎉

## 🏥 **Microservicio de Citas**

Este microservicio tiene como objetivo gestionar las citas médicas en el hospital. Cada cita estará asignada a un doctor y a un departamento específico, donde el paciente podrá reservar su cita. Las citas pueden tener diferentes estados: **Programada**, **Completada**, **Disponible** o **Cancelada**. ¡Vamos a sumergirnos en los detalles del desarrollo!

---

## 📅 **Modelo de Cita**

Una **cita** incluye los siguientes atributos:

- **Fecha** de la cita
- **Hora** de la cita
- **Estado** de la cita (Programada, Completada, Disponible)
- **Médico** asignado a la cita
- **Lugar** o departamento de la consulta

![Modelo de Cita](/assets/image/postcitas/model.png)

---

## 🛠️ **Servicios Disponibles**

Este microservicio ofrece los siguientes servicios:

- **Crear una cita**
- **Obtener una cita por su ID**
- **Obtener todas las citas**
- **Obtener citas reservadas por un paciente**
- **Obtener citas de un doctor**
- **Obtener citas por estado**
- **Actualizar una cita**
- **Eliminar una cita**
- **Marcar una cita como completada, cancelada o programada**

![Servicios](/assets/image/postcitas/metodosServicioCitas.png)

---

## 💡 **Fragmento de la Lógica de Negocio**

Aquí te mostramos cómo se gestiona la creación de una cita:

- Al crear una cita, se puede especificar la fecha, hora, el estado (por defecto, se marcará como disponible), el doctor que atenderá la cita y el consultorio correspondiente.

![Lógica de Negocio](/assets/image/postcitas/ImplService.png)

---

## 🔍 **Otros Aspectos Importantes**

- **Reservar una cita**: Se necesitan los datos del paciente y una breve razón de la visita, lo que puede ser útil para el doctor como referencia. La cita se marcará como programada.

- **Cancelar una cita**: Esto implica eliminar los datos del paciente de esa cita y marcarla como disponible nuevamente.
  
![Reservar Cita](/assets/image/postcitas/ImplService2.png)

---

## 📝 **Controlador**

Este es un ejemplo de cómo se ve nuestro controlador y endpoints:

![Controlador](/assets/image/postcitas/comtroladorCitas.png)

---

## 🤝 **Comunicación con el Microservicio de Paciente**

Utilizamos `@RegisterRestClient` para permitir la comunicación entre servicios y así integrar funcionalidades del microservicio de paciente, quienes son los usuarios que podrán reservar las citas que deseen.

![Comunicación](/assets/image/postcitas/RegiserClient.png)

---

## 🛠️ **Servicio**

El servicio se encarga de inyectar este cliente para poder realizar las llamadas al otro microservicio, pasando los datos de `idPatient` y `reason` que sería la razón de la cita.

![Servicio](/assets/image/postcitas/InyeccionServicio.png)

---

## 📝 **Controlador del Servicio**

Con su respectivo controlador:

![Controlador del Servicio](/assets/image/postcitas/ControladorPaciente.png)

---

¡Gracias por seguir el progreso de este emocionante proyecto! 💪🚀
