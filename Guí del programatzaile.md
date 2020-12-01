# Guía del Programatzaile
# ---------------------------

# 1 TABLAS 

* Para empezar a trabajar en una base de datos, primero tenemos que diseñar las tablas donde se guardaran esos datos.
* Una buena estructura de datos hará que el trabajo de programación posterior sea más sencillo. Una mala estructura supondrá más trabajo y éste será más desagradable.
* Aunque puede resultar una tarea costosa, siempre es posible redefinir la estructura de datos. 
* Los nombres que pongamos tanto a las tablas como a los campos pueden ser una ayuda si están bien puestos. Es más fácil pensar y visualizar entidades bien nombradas.

En este proyecto, a modo de ejercicio, vamos a migrar desde una hoja de Excel con numerosos datos relacionados a una base de datos Access. Comprobaremos que para manejar Access necesitamos un trabajo previo de diseño de tablas, consultas y formularios y de programación en VBA para conseguir que la entrada y salida de datos sea fácil y accesible a cualquiera. Pero la base de datos nos proporcionará una aplicación sólida y capaz de procesar una cantidad mucho mayor y con mayor eficiencia que la hoja Excel.

## Quimera 2020.xlsx
![Roster](/images/Roster.png)

Quimera 2020.xlsx es una hoja Excel bien compleja de la que, a día de hoy, podría explicar muy poco: se trata de el cuaderno de notas, cuadro de mandos, diario de juego, o algo parecido, de un grupo de jugadoras/es de - - - - - compuesto por más de 50 miembros. Podemos repasar las diferentes clasificaciones que existen en la hoja **Profesiones**: ALQUIMIA ENCANTAMIENTO, SASTRERÍA, PELETERÍA, HERRERÍA, cada una con diferentes herramientas o poderes que se usarán en el juego.
En la hoja **Roster**, la de la imagen anterior, vemos la lista (Roster) de jugadores. Varias columnas, encuadradas en rojo en la imagen, refieren propiedades que configuran cada jugador. 

![Assists](/images/Assists.png)

En la hoja **Assists** vemos un cuadro donde se lleva la cuenta de las asistencias a las batallas o Raids que son asaltos previamente acordados a los que los miembros del equipo deben acudir para participar y colaborar con el resto del equipo. 

Nos centraremos ahora en los Jugadores y la asistencia a las batallas. Vamos a definir las tablas para poder registrar estos datos y poder trabajar con ellos.

## Quimera 2020.accdb

La primera tabla que vamos a crear es la de Jugadores/as. La denominamos Players

### Players
Nombre del campo | Tipo de datos | Otras Características
------------ | ------------- | -------------
Id | Autonumeración | Campo Clave
Player | Texto (25) | Nombre del/a jugador/a
Raza | Texto (25) | Lista de valores: Humana;Humano;Enana;Enano;Gnoma;Gnomo;Elfa, Elfo
Clase | Texto (25) | Lista de valores: Warrior;Rogue;Hunter;Mago;Warlock;Druida;Priest;Paladin
MainS | Texto (25) | Consulta: SELECT DISTINCT [Players].MainS FROM Players ORDER BY [Players].MainS; 
OffS | Texto (25) | Consulta: SELECT DISTINCT [Players].OffS FROM Players ORDER BY [Players].OffS; 
Rango | Texto (25) | Lista de valores: Ascendente;Miembro;Raider;Suboficial;Oficial

La segunda la vamos a llamar Raids (Batallas, Incursiones) en la que guardaremos la fecha y el tipo:

### Raids
Nombre del campo | Tipo de datos | Otras Características
------------ | ------------- | -------------
Id | Autonumeración | Campo Clave
Fecha | Fecha/Hora | Fecha del Raid
Raid | Texto (25) | Es un tipo, hasta aclarar los posibles tipos lo dejamos como un texto libre

Para registrar los asistentes a las Raids vamos a servirnos de una tercera tabla relacionada con las dos anteriores

### Raids_Assist
Nombre del campo | Tipo de datos | Otras Características
------------ | ------------- | -------------
Id | Autonumeración | Campo Clave
IdRaid | Número | Clave externa para enlazar con la tabla Raids.
IdPlayer | Número | Clave externa para enlazar con la tabla Players.
AsistenciaSNR | Texto (1) | S/N/R : Ní asiste, No asiste, Rotación
HoraInicio | Fecha/Hora | Creo que se indica cuando un player asiste pero más tarde que la hora acordada.

### Relaciones entre tablas

![Relaciones](/images/RelacionesTablas.png)

Como se puede intuir en la imagen. la relación es de uno a muchos desde Raids a Raids_Assist, eso quiere decir que un registro de Raids (con un únio Id) puede tener varios registros en Raids_Assist con ese mismo IdRaid. Lo que se traduce en que a una Raid pueden asistir varios jugadores. Lo mismo ocurre en la parte derecha del esquema de las relaciones, un jugador (un único Id en Players) puede tener varios registros en Raids_Assist, es decir un jugador puede ir a diferentes Raids.

Ahora bien, Con lo que hemos dicho hasta ahora podría ocurrir que existiesen varios registros del mismo jugador en la misma Raid, lo cual no tiene sentido. Para evitarlo tenemos que crear un índice único en la tabla Raids_Assist sobre los campos IdRaid, IdPlayer de forma que la base de datos no va a permitr la existencia de esa repetición.

![Índice Único](/images/IndiceUnico.png)

:eyes: Fijarse, la manera de definir un índice sobre dos campos o más es rellenar la casilla nombre del índice sólo en el primero de los campos del índice.

Hasta aquí la primera lectura @martineizrod espero sus comentarios :ear: :ear:
