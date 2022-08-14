# Notas de SQL

Estas notas son aplicadas para SQLite, también pueden aplicar a otros motores, pero tienen variaciones.

> Nota: Todo query termina con punto y coma (;).
> Nota: Todo texto debe ir entre doble comillas (") o comillas simple (').

## `SELECT` y `FROM`

Para obtener los datos de una tabla se usa la palabra `select` junto con nombre o nombres de las columnas, con la palabra  `from` indicando el nombre de la tabla.

Para obtener los todos los datos se usar el comodín (`*`).

```sql
SELECT * FROM name_table;
```

Para obtener los datos de una columna de la tabla

```sql
SELECT name_column FROM name_table;
```

Para obtener los datos de varias columnas de la tabla

```sql
SELECT name_column_1, name_column_2,... FROM name_table;
```

## Limitando los resultado de la consulta `LIMIT`

Para limitar la cantidad de resultados en una consulta, se usa la palabra `LIMIT` colocando la cantidad que se necesita.

```sql
SELECT name_columns FROM name_table LIMIT number;
```

```sql
SELECT name_columns FROM name_table LIMIT 10;
```

## Creando tablas

Para crear tablas se debe indicar el nombre de la tabla y los atributos con los que se va a construir. 

Cuando se crea una columna se debe definir el nombre de la columna y su tipo, como mínimo. Se pueden agregar más opciones que debe cumplir la variable.

```sql
CREATE TABLE name_table ( name_column_one type options, name_column_two type options,... );
```

```sql
CREATE TABLE name_table ( id INTEGER PRIMARY KEY AUTOINCREMENT, name TEXT NOT NULL, description TEXT(100) );
```

## Tipos de datos

Como en todo lenguaje de programación, existen los tipos datos que se pueden almacenar dentro de una tabla, los mas comunes son:

|Nombre	  |	Tipo	| 
|:---------:|---------------|
|TEXT      |String, cadena de texto, letras|
|INTERGER  |Numero entero|
|REAL      |Numero con punto flotante |

> **Nota**: No existe el tipo `booleano` en SQLite.

### Opciones en los tipos de datos

|Nombre     |Abreviación | Descripción|
|:---------:|:-----------:|------------|
|NOT NULL   |NN          |No permite que se inserte sin contenido, o vacío, es decir, forzosamente debe contener algún valor|
|NULL       |N           |Por default sera `null` o vacío el contenido|
|PRIMARY KEY|PK          |Llave primaria, es decir, esa columna es única en su contenido, normalmente es para el `id` del registro|
|AUTOINCREMENT|AI|Esta columna incrementara en automático su valor, es usada para el `id`|
|UNIQUE     |U           |Es utilizada para indicar que en la columna solo existirán valores únicos, es decir, no se pueden existir repetidos, ejemplo un correo electrónico|
|DEFAULT    |Default     |Con esto definimos que valor se coloca en caso que no sea especificado al insertar el registro|

## Insertando datos `INSERT`

Para insertar datos debemos indicar el nombre de la columna y en el mismo orden el dato a ser insertado. Esto se hace con la instrucción `INSERT INTO`. 

Cuando se tienen definido en la tabla tiene un valor por default, se puede omitir al momento de insertar, al igual que si es `AUTOINCREMENT` que normalmente son los `id`s.

```sql
INSERT INTO name_table (name_column_one, name_column_two,...) VALUE (data1, data2,...);
```

## Creando tablas temporales

Se crean tablas temporales por diferentes situaciones, están tablas no son persistentes, es decir, cuando terminas la sesión estas tablas desaparecen, los datos que se colocan aquí realmente no afectan a la tabla original.

Se agrega la palabra reservada `TEMPORARY`, se le da un nombre y posteriormente damos un query para obtener las columnas y datos específicos para formar esta nueva tabla.

```sql
CREATE TEMPORARY TABLE name_table_temp AS ( SELECT * FROM name_table WHERE comparison );
```

Con este `query` creo una tabla temporal llama `zapatos_temp` y la formo con todos los zapatos que en la columna `color` sean *negro*:

```sql
CREATE TEMPORARY TABLE zapatos_temp AS ( SELECT * FROM zapatos_tabla WHERE color="negros" );
```

## Filtrado `WHERE`

## Operadores matemáticos `AVG`, `COUNT`, `MAX`, `MIN`