---
title : "Proyecto Backend para una Clinica en Quarkus con Microservicios"
date : 2024-07-30
categories : [Api Clínica HealHub]
tags: [Backend,Quarkus,Java,Microservices,RestApi]
---

# Proyecto Backend para una Clinica en Quarkus con Microservicios

## Descripción del Proyecto

El objetivo de este proyecto es aprender y desarrollar un sistema de gestión hospitalaria basado en microservicios utilizando Quarkus. Este sistema permitirá la gestión eficiente de pacientes, personal médico, expedientes clínicos, inventario de medicamentos, información de citas con pacientes y más funcionalidades que se podrán agregar durante el desarrollo del proyecto. Además, se implementará la autenticación mediante JWT, health checks, prevención de caídas de los servicios y métricas para asegurar la robustez y estabilidad del sistema.

## Tecnologías Utilizadas

- **Java:** Lenguaje de programación principal.
- **Quarkus:** Framework principal para el desarrollo de microservicios.
- **Panache:** Simplificación del acceso a la base de datos utilizando el patrón Active Record.
- **MicroProfile:** Proporciona herramientas para la creación y conexión de microservicios, incluyendo métricas, autenticación, health checks, tolerancia a fallos y comunicación con clientes REST.
- **MongoDB:** Motor de base de datos.

## Microservicios Principales del Proyecto

### Servicio de Pacientes

**Funcionalidad:** Manejo de la lógica de los pacientes y creación de registros de pacientes.

**Características:**
- Registro de pacientes.
- Actualización de pacientes.
- Eliminación de pacientes.

### Servicio de Historial Médico

**Funcionalidad:** Registro de diagnósticos y tratamientos proporcionados por los médicos a los pacientes.

**Características:**
- Registro de consultas.
- Registro de diagnósticos.
- Registro de tratamientos.
- Otros detalles

### Servicio de Programación de Citas

**Funcionalidad:** Permitir a los pacientes agendar citas en los horarios disponibles de los médicos.

**Características:**
- Programación de citas.
- Reprogramación de citas.
- Cancelación de citas.
- Las citas estarán programadas para intervalos de 15 minutos.

### Servicio de Personal Médico

**Funcionalidad:** Manejo de los datos y registros del personal médico.

**Características:**
- Registro de médicos 
- Actualización de información del personal médico.
- Eliminación de información del personal médico.

### Servicio de Gestión de Citas del Día

**Funcionalidad:** Revisión de las citas programadas para el día en curso.

**Características:**
- Listado de citas diarias.
- Detalles de cada cita.
- Estado de la cita.

### Servicio de Inventario de Medicamentos y Equipos Médicos

**Funcionalidad:** Control del inventario y gestión de pedidos de reabastecimiento.

**Características:**
- Registro de inventario.
- Seguimiento de stock.
- Gestión de pedidos.
- Reabastecimiento de inventario.

### Servicio de Expedientes Clínicos

**Funcionalidad:** Generación de recetas médicas y registros de informes de pacientes.

**Características:**
- Registro de informes médicos.
- Generación de recetas médicas.
- Gestión de recetas médicas.

### Servicio de Facturación

**Funcionalidad:** Generación y gestión de facturas por los servicios médicos proporcionados.

**Características:**
- Creación de facturas.
- Procesamiento de pagos.
- Gestión de seguros médicos.

![Quarkus.png](/assets/image/quarkus.png)