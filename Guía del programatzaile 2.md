# Guía del Programatzaile 2
# ---------------------------

# 1 CONSULTAS

Al realizar una consulta a la base de datos podemos obtener un conjunto de registros diferente de la propia tabla. Seleccionar algunos de los campos, dando a los datos obtenidos el formato que se precise, definir uno o más criterios para aplicar un filtro sobre los datos a obtener, ordenar los registros por uno o varios campos,

![Consulta 1](/images/Consulta01.png)

En la imagen vemos la pantalla de diseño de una consulta. En este caso estamos seleccionando los Players cuyo campo Raza empieza por Elf. La interfaz gráfica del diseño de la consulta hace más fácil e intuitiva esta tarea, pero en definitiva la consulta se guardará y ejecutará meidante la sentencia SQL que le corresponda que podemos obtener en la Vista Diseño de la misma y que en este caso será:

``` SQL
SELECT Players.Id, Players.Player, Players.Raza, Players.Clase
FROM Players
WHERE (((Players.Raza) Like "elf*"));
```

Y el resultado de la consulta...

![Consulta 2](/images/Consulta02.png)

Vamos ahora con otra consulta: Los players que sean de Clase Warrior o Druida, por ejemplo:

![Consulta 3](/images/Consulta03.png)

``` SQL
SELECT Players.Id, Players.Player, Players.Raza, Players.Clase
FROM Players
WHERE Players.Clase= "Warrior" OR Players.Clase= "Druida";
```

Y el resultado de la consulta...

![Consulta 4](/images/Consulta04.png)

# 2 CONSULTAS DE TOTALES

Con una consulta de totales, podremos calcular totales, promedios, cuenta... sobre uno o vairios cmpos, agrupando por uno o varios campos.

![Consulta 5](/images/Consulta05.png)

``` SQL
SELECT Players.Raza, Count(Players.Id) AS CuentaDeId
FROM Players
GROUP BY Players.Raza;
```

Y el resultado de la consulta...

![Consulta 6](/images/Consulta06.png)