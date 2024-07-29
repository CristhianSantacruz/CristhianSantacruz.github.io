---
title : "Manejo de Excepciones"
date : 2024-07-28
categories : [Api Reserva Canchas]
tags: [Backend,SpringBoot,Kotlin,RestApi]
---


# Manejo de Excepciones 

He creado un manejo de excepciones para los diferentes problemas que ocurren en la lógica de servicio del api uno de ellos puede ser que la cantidad de usuario máxima que puede haber en un grupo es de 16 personas o que   un usuario no puede ser agregado dos veces al mismo grupo para eso he hecho una clase **ErrorMessageDto** que nos servirá como molde para mostrar al usuario el status y un string explicando el error.

![ErrorMessageDto](/assets/image/postexceptions/ErrorMessageDto.png)

Luego creo la clase ResponseEntityExceptionHandler que será anotada por **@RestControllerAdvice** que indica que la clase manejara excepciones lanzadas por los controladores de la aplicación y en el método exceptions **@ExceptionHandler** Se usa para indicar que el método debe manejar las excepciones especificas el método recibe un RuntimeExceptooon por que las demás excepciones extienden de esta y luego mediante la clase ErrorMessageDto para como status el HttpStatus.NOT_FOUND y el mensaje de la exception como descripción del error.

![Manejador](/assets/image/postexceptions/ExceptionHandler.png)


> Algunos ejemplos
{: .prompt-tip }


![Ejemplo1](/assets/image/postexceptions/ejemplo1.png)
![Ejemplo2](/assets/image/postexceptions/ejemplo2.png)
![Ejemplo3](/assets/image/postexceptions/ejemplo3.png)

