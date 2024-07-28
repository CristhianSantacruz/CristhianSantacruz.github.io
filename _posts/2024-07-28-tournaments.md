---
title : "Creando servico para la creacionde torneos para varios grupos"
date : 2024-07-28
categories : [Api Reserva Canchas]
tags: [Backend,SpringBoot,Kotlin,RestApi]
---

# Creacion del modelo torneo
Este sera como sera la logica del modelo de torneo que tendra el nombre del torneo la fecha de cuando comiece el dia de terminara el resutaldo del torneo que puede describir al grupo ganador y la relacion de **Uno a muchos** , donde en un torneo puede haber muchos grupo compitiendo.

![TournamentEntity](/assets/image/posttournaments/tournament1.2.png)

# Entidad grupo
Tendra la relacion de muchos a uno mapeada por el atributo **tournamentEntity**.
![GroupEntity](/assets/image/posttournaments/tournament1.3.png)


# Rutas del servicio
Tenemos la url mapping de nuestro controlador de torneo es **"/tournament"** 

 **Endpoint Create Post**
Este endpoint lo que hara es crear un torneo donde se inicaliza la lista de grupo como vacia, se le pasa la fecha de inicio y fin y el nombre del torneo.
 **Endpont Add Group**
Este endpoint lo que hara es registrar o agregar a un grupo al torneo.

![Controlador](/assets/image/posttournaments/tournament1.4.png)


> Ejemplo en postman
{: .prompt-tip }

![EjemploSolicitud](/assets/image/posttournaments/tournament1.png)

Como podemos ver en este ejemplo es un torneo que se ha creado para comenzar el mismo dia y terminar el mismo donde ya hay dos grupo registrados para el torneo.
