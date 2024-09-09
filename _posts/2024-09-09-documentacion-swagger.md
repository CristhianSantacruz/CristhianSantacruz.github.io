---
title : "Documentar Apis en Quarkus"
date : 2024-09-09
categories : [Quarkus Magi]
tags: [Backend,Quarkus,Java,Swagger,OpenApi]
---

# Documentación de API en Quarkus con OpenAPI y Swagger UI

## ¿Qué es Swagger (OpenAPI)?

![image](/assets/image/postdocumentacion/documentacion%20openapi.png)

Básicamente, **Swagger** es una especificación independiente del lenguaje que nos ayuda a describir nuestras API REST sin tener acceso directo al código, todo a través de una interfaz de usuario que permite visualizar y probar la API.

## Creando el proyecto en Quarkus

Para crear nuestro proyecto en **Quarkus**, si ya viste mi post anterior [PostAnteriores](https://cristhiansantacruz.github.io/posts/estrategia-datos/) , tendrás una idea de cómo configurarlo y qué extensiones usar para probar la API y nuesta APi de ejemplo de usuario. Las extensiones que usaremos son:

- Rest
- Hibernate ORM with Panache
- SmallRye OpenAPI

### Modelo de datos

A continuación se muestra el modelo de datos que utilizaremos:

![image](/assets/image/postdocumentacion/Modelo%20Repository.png)

### Recurso/Controlador a documentar

Este es el recurso/controlador que vamos a documentar:

![image](/assets/image/postdocumentacion/Controlador%20Repository.png)

## Agregar la extensión SmallRye OpenAPI

Si no tenemos la extensión **SmallRye OpenAPI**, podemos agregarla de las siguientes maneras:

### Usando Quarkus CLI:

 ```bash
 quarkus  extension  add  quarkus-smallrye-openapi
 ```
Si no tenemos el cli de quarkus, no hay problema lo podemos hacer con Maven 


 ```bash
./mvnw quarkus:add-extension -Dextensions='quarkus-smallrye-openapi'
 ```
 o simplemente ubicar nuestra dependencia
  ```bash
<dependency>
    <groupId>io.quarkus</groupId>
    <artifactId>quarkus-smallrye-openapi</artifactId>
</dependency>
 ```

 Una vez agregada esta dependencia  a nuestro proyecto vemos que ya tenemos levantado nuestra interfaz de swagger sin realizar otra configuración en **http://localhost:8080/q/swagger-ui/** - [SwaggerUi](http://localhost:8080/q/swagger-ui/) pero como podemos editar nuestros datos.
![image](/assets/image/postdocumentacion/Screenshot%20(95).png)



Por ejemplo para uno de nuestros endpoint podemos agregar un resumen y descripción de la siguiente manera.

Con la anotación **@Operation** podemos agregar un resumen y una descripción a demás de agregar otras configuraciones como si esta deprecado o no.
Como se ve esto , pues de la siguiente manera
![image](/assets/image/postdocumentacion/description%20and%20summary%20endpoint.png)
y nuestra interfaz de Swagger es la siguiente
![image](/assets/image/postdocumentacion/result%20description%20and%20summary.png)

Ahora configuramos los datos como la información de la api , el contacto de la persona que lo realizo básicamente información importante en Quarkus puedes hacerlo de dos manera la primera es crear una clase que extienda de Aplication anotada con @OpeanApiDefinitation

# Primer Forma

De la siguiente manera
![image](/assets/image/postdocumentacion/swagger%20code.png)
Y nuestra interfaz de Swagger se ve ahora así.
![image](/assets/image/postdocumentacion/ui%20swagger.png)

# Seguna Forma

La otra manera de la cual se puede hacer es hacer estos cambios directamente desde el aplication.properties  de la siguiente manera
![image](/assets/image/postdocumentacion/swagger%20properties.png)
Y vemos como podemos editar los datos de nuestro properties
![image](/assets/image/postdocumentacion/ui%20swagger%20properties.png)

Gracias por ver