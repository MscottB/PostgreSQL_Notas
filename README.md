# PostgreSQL

Pequeño Tutorial sobre postgreSQL por sentencia SQL.

El material que ocupe para este documento son los siguientes:

* [PostgreSQL desde Cero](https://www.tutorialesprogramacionya.com/postgresqlya/index.php?inicio=0)

Y en gran medida ocupe este curso de youtube.
* [Curso de PostgreSQL](https://www.youtube.com/playlist?list=PL8gxzfBmzgex2nuVanqvxoTXTPovVSwi2)

Presentado los creditos, se inicia la pequeña ayuda memoria.

## 1.-Instalacion PostgreSQL

No tiene mucha ciencia por lo cual, dejare el link de descarga [PostgreSQL](https://www.postgresql.org/download/)

## 2.- Creacion Base de datos

```sql
create database "nombreBD";
```
>Para comentar codigo anteponer doble guion(--).
## 3.- Eliminar Base de datos

1. Elimina la base de datos despues de confirmar que existe.

```sql
drop database if exists "nombreDB";
```

2. Elimina la base base de datos sin confirmar.

```sql
drop database "nombreDB";
```
## 4.- Crear Tabla

```sql
create table nombretabla(
	idnombretabla int not null,
	primeracolumna varchar(40),
	segundacolumna varchar(20)
);
```
>La restricción NOT NULL sirve para especificar que una columna no acepta el valor NULL, es decir, que esa columna siempre tiene que tener algún valor, no puede estar vacía.

>para ver la tabla en pgadmin debe ir a nombreDB>Schemas(Esquemas)>Tables(tablas).

## 5.- Insertar Datos a una tabla(INSERT)

1. Primera opcion:
```sql
insert into nombretabla values ('datoColumna1','datoColumna2','datoColumna3');
```
2. Segunda opcion:
```sql
insert into nombretabla (nombreColumna1,nombreColumna2) values ('datoColumna1','datoColumna2');
```

## 5.-Actualizar datos(UPDATE)

1. Actualizar campo unico.
```sql
update nombretabla set nombreCampoaCambiar='nuevoDato' where campoaIdentificar='datoExistente';
```
2. Actualizar multiples campos.
```sql
update nombretabla set nombreCampoaCambiar='nuevoDato', nombreCampoaCambiar2='nuevoDato2' where campoaIdentificar='datoExistente';
```

3. Actualizar dato null.
```sql
update nombretabla set nombreCampoaCambiar='nuevoDato' where campoaIdentificar is null;
```

## 6.- Tipo de Datos Basicos

| Tipo Dato | Descripcion|
|:---------:|:----------:|
| `Boolean` | Verdadero o falso |
| `Character(n)`| cadena de caracteres de tamaño fijo |
| `Date` | fecha(sin hora) |
| `Float` | Flotante(Numero Punto Flotante) |
| `Int, Integer` | Numero Entero |
| `Decimal` | Numero Exacto |
| `Time` | Tiempo en Hora, Minutos, Segundo |
| `Varchar(n)` | Cadena de caracteres de tamaño variable |

>Para mas Informacion, consultar la documentación de postgreSQL en el siguiente [Enlace](https://www.postgresql.org/docs/11/datatype.html)

## 6.- Consultar Datos(SELECT)

1. Consultar todos los datos de una tabla
```sql
select * from nombreTabla;
```

2. Consultar campos especificos

```sql
select (nombreColumna1, nombreColumna2) from nombreTabla;
```
3. Consulta con multiples devolucion datos en columna que incluye alias(Devuelte columna con nombre asignado por el usuario)

```sql
select (nombreColumna1, nombreColumna2)as nombreColumnaEntregada from nombreTabla;
```
4. Consulta con devolucion de multiples columnas integradas en el alias

```sql
select (nombreColumna1)as nombreColumnaEntregada1, nombreColumnaEntregada2 from nombreTabla;
```
5. Consultar dato y fila especifica

```sql
select nombreColumna from NombreTabla where nombreColumnaDatoaBuscar='DatoQueSeBuscara';
```

## 7.- Where y uso de operadores de comparacion(condicionales)(= , != , > , < , >= , <=)(WHERE)

1. Consulta basica con WHERE
```sql
select * from nombreTabla where nombreColumna = 'Dato a Buscar';
```

2. Consulta devuelve todos los datos excepto el que se consulta.
```sql
select * from nombreTabla where nombreColumna != 'Dato a Buscar';
```

3. Consulta con condicionales numerales(> , < , >= , <=), devolvera resultados dependiendo del operador seleccionado.
```sql
select * from nombreTabla where nombreColumna > 'Numero';
select * from nombreTabla where nombreColumna < 'Numero';
select * from nombreTabla where nombreColumna <= 'Numero';
select * from nombreTabla where nombreColumna >= 'Numero';
```
>en el nombre columna esté, debe contener datos numericos(EJ: int)

4. Condicionales "mas" para programacion (and y or son operadores logicos).

- Doble condicional(**and**), debe cumplir las 2 condiciones para devolver datos.
```sql
select * from nombreTabla where nombreColumna = "Dato a buscar" and nombreColumna = 'Dato a buscar';
```

- Doble condicional(**or**), debe cumplir una de las dos condiciones para devolver datos.
```sql
select * from nombreTabla where nombreColumna = "Dato a buscar" or nombreColumna = 'Dato a buscar';
```

## 8.- Eliminar datos de Tabla(DELETE)

- Borrar **TODOS** los registros de una tabla.(No me hago responsable si alguien se equivoca)
```sql
delete from nombreTabla;
```

- Eliminar fila especifica.
```sql
delete from nombreTabla where nombreColumna ='Dato a Eliminar';
```

## 9.- Comentar lineas en PostgreSQL

- Comentario Simple(toma una linea), anteponer doble guion(--).
```sql
-- select * from nombreTabla;
```

- Comentario MultiLinea(/**/).
```sql
/*
delete from nombreTabla 
where nombreColumna ='Dato a Eliminar';
*/
```

## 10.- Modificar Tabla/Columna(ALTER)

- Agregar Columna a tabla existente. Inicialmente acepta **nulos**, posteriormente se puede modificar.
```sql
alter table nombreTabla add column nombreColumna TipoDato;
```
>Ejemplo Tipo de Dato: Varchar(10).

- Renombrar nombre de columna existente.
```sql
alter table nombreTabla rename NombreColumnaExistente to nuevoNombre; 
```

- Eliminar Columna de una tabla existente.
```sql
alter table nombreTabla drop column nombreColumna;
```
- Agregar la opcion que no acepte nulos en la columna.
```sql
alter table nombreTabla alter column nombreColumna set not null;
```
> La columna debe tener datos ingresados previamente antes de ejecutar esto, o saldra **ERROR**, puede ajecutar un UPDATE para agregar datos a la columna.

- Quitar la opcion **not null** a una columna.
```sql
alter table nombreTabla alter nombreColumna test drop not null;
```
> **DROP** en SQL es para quitar o eliminar.

- Cambiar tipo de dato que se ingresa a una columna.
```sql
alter table nombretabla alter column nombreColumna type TipoDato; 
```
>En tipoDato se asignara el nuevo valor, que aceptara la columna.

>**Precaucion** al realizar este cambio ya que puede causar error, al cambiar el tipo de dato a ingresar, ejemplo de varchar a int.

>**PGADMIN** debe evitar este tipo de modificaciones, presentando un Error.

## 11.- Claves Primarias(Primary Key)

* Ejemplo **primary key** al crear una tabla.

```sql
create table nombreTabla(
	idNombreTabla int not null,
	campoEjemplo varchar(20),
	campoEjemplo varchar(10),
	primary key (idNombreTabla)
)
```
>Normalmente se asigna como **primary key** a las id de las tablas.

* Agregar **Primary key** a una tabla existente.

```sql
alter table nombreTabla add primary key(idNombreTabla);
```
>En el diseño de bases de datos relacionales, se llama clave principal a un campo o a una combinación de campos que identifica de forma **única** a cada fila de una tabla. Una clave primaria comprende de esta manera una columna o conjunto de columnas.

>Los datos ingresados en el campo asignado con **primary key** son unicos y no puede existir dos numeros identicos o duplicados.
>
>**Lo que esta en la siguiente tabla no es posible.**
>| ID | Campo1 |
>|:--:|:------:|
>| 22 | XXXXXX |
>| 22 | XXXXXX | 

## 12.- Auto Incrementar - SERIAL - SMALLSERIAL - BIGSERIAL

Incrementa en **1** el valor numerico de un campo, de manera secuencial con cada dato ingresado en la tabla.

```sql
create table nombreTabla (
	idNombreTabla Serial primary key,
	campoEjemplo varchar(20),
	campoEjemplo varchar(10)
);
```

Ejemplo:
| ID | Dato |
|:--:|:----:|
| 1  |  X   |
| 2  |  X   |

* **Datos Extras**

| Nombre | Tamaño del almacenamiento | Rango Numerico |
|:-----------:|:------:|:---------:|
| **SMALLSERIAL** | 2 Bytes | 1 a 32,767 |
| **SERIAL** | 4 Bytes | 1 a 2,147,483,647 |
| **BIGSERIAL** | 8 Bytes | 1 a 922,337,2036,854,775,807 |

>El concepto de SERIAL en PostgreSQL es similar al concepto AUTO_INCREMENT en MySQL .

>Agrega la secuencia NOT NULL a la columna.

>Es importante notar que el SERIAL no crea implícitamente un índice en la columna o hace que la columna sea la columna clave primaria. Sin embargo, esto se puede hacer fácilmente especificando la restricción PRIMARY KEY para la columna SERIAL.

## 13.- Diferencia en DROP / TRUNCATE

* El **DROP** elimina la tabla.
```sql
drop from nombretabla;
```

Para eliminar las tablas y sus relaciones, se ocupa la siguiente Query:
```sql
drop table NombreTabla1,NombreTabla2 cascade;
```
>eliminara incluso las vistas.

* El **TRUNCATE** reinicia la tabla(Elimina los datos) sin tocar el autoincremento del id.
```sql
truncate table nombreTabla;
```

si tiene un autoincrementar lo reinicia con **restart identity**, este ultimo no funciona con DROP.
```sql
truncate table nombreTabla restart identity;
```

>Diferencia entre TRUNCATE, DELETE y DROP
>
>**TRUNCATE**
>
>* No podemos usar la cláusula Where con TRUNCATE.
>* Elimina todas las filas de una tabla(la Re-hace).
>* Es más rápido en cuanto al rendimiento.
>
>**DELETE**
>
>* Podemos usar la cláusula where con DELETE para filtrar y eliminar registros específicos.
>* El comando DELETE se utiliza para eliminar filas de una tabla según la condición WHERE.
>* Mantiene los datos, por lo que es más lento que TRUNCATE.
>* La instrucción DELETE elimina las líneas de una en una.
>
>**DROP**
>
>* El comando DROP elimina una tabla de la base de datos.
>* También se eliminarán todas las filas, índices y privilegios de las tablas.
>* **La operación no se puede anular.**
>
>**Las operaciones DELETE pueden deshacerse, mientras que las operaciones DROP y TRUNCATE no pueden deshacerse.** __~~Eso dice internet~~__

## 14.- Valores por DEFAULT

Valores por defecto o pre-establecidos, que se ocupan en ausencia de algun dato no recibido. Se puede ocupar como alternativa al valor **nulo**, de ser necesario.

```sql
create table nombreTabla(
	idnombreTabla serial primary key,
	nombreCampo varchar(20),
	telefono varchar(10) default 'XXXXXX'
)
```
> XXXXXX puede ser remplazado por 'TEXTO'(entre comillas) o numeros.

## 15.- Columnas calculadas.

Se crea una columna **Temporal**, despues de algun calculo previo.

**EJEMPLO**:

Tabla que se trabajará:

|nombreTrabajador|N°Identificacion|salario|
|:----:|:----:|:----:|
|trabajador1|1234|2000|
|trabajador2|5678|4000|
|trabajador3|1267|6000|

```sql
select nombreTrabajador, salario,(salario + 1500)as NombreNuevaColumna from NombreTabla
```
Despues de ejecutar el **Select**, el resultado sería el siguiente:

|nombreTrabajador|salario|NombreNuevaColumna|
|:--:|:--:|:--:|
|trabajador1|2000|3500|
|trabajador2|4000|5500|
|trabajador3|6000|7500|

>**EXTRA**
>
>Si deseamos mantener los cambios realizados por el **select**, se ejecuta el siguiente **UPDATE**, 
>donde se especifica a que trabajador.
>
>```sql
>update NombreTabla set salario = salario + 1500 where nombreTrabajador = 'trabajador1'
>```
> El **SET** envia los nuevos datos a la columna especificada, en este caso salario.
> y **WHERE** es para especificar al trabajador.

## 16.- Ordenar una columna dentro de una tabla (ORDER BY)

Ayuda a ordenar la devolucion de datos realizado mediante un **Select**.

* `ORDER BY` Predeterminado.
```sql
select * from nombreTabla order by nombreColumna
```
>Si el contenido de la columna es texto, se ordenara de manera alfabetica(A-Z).
>
>**nombreColumna** es la que se ordenará
* `ORDER BY` **Ascendente**.
```sql
select * from nombreTabla order by nombreColumna asc
```
>**ORDER BY** trabaja de manera _Ascendente_ por defecto.

* `ORDER BY` **Descendente**.
```sql
select * from nombreTabla order by nombreColumna desc
```

* Ordenar por numero de la columna
```sql
select * from nombreTabla order by NumeroColumna
```
>El numeroColumna puede ser 1, 2, 3 o cualquiera que posea una tabla. dicha columna es la que se ordenara...en resumen reemplazas el nombre de la columna por un numero.

* **ORDER BY** Combinados.
```sql
select * from nombreTabla order by nombreColumna1 desc, nombreColumna2 asc
```
> Se debe especificar el orden de cada columna (Ascendente, Descendente).

## 17.- Buscar dentro de una tabla (like - not like)

* **LIKE** sirver para buscar una palabra o parte de ella dentro de una tabla.
```sql
select * from nombreTabla where nombreColumna like '%parte de la palabra que se buscara%'
```
>nombreColumna es donde se realizara la busqueda.
>
>El **LIKE** es sensible a minusculas y mayusculas (case sensitive).
>
>El simbolo **%**(porcentaje) reemplaza la parte que no esta presente, o en algunos casos ningun caracter presente. En resumen es un comodin.

Busqueda ocupando **_**(Guion Bajo).
```sql
select * from nombreTabla where nombreColumna like 'palabra_'
```
> El guion bajo reemplaza un solo caracter a diferencia del simbolo de porcentaje.

* **Not Like** es lo contrario a **LIKE**, ya que buscara todo menos la palabra o parte de esta que deseamos.

```sql
select * from nombreTabla where nombreColumna not like 'palabra'
select * from nombreTabla where nombreColumna not like 'palabra%'
select * from nombreTabla where nombreColumna not like '%palabra'
select * from nombreTabla where nombreColumna not like '%palabra%'
select * from nombreTabla where nombreColumna not like 'palabra_'
select * from nombreTabla where nombreColumna not like '_palabra'
```

## 18.- Contar registro (COUNT)

* Sirve para saber la cantidad de registros de una tabla.
```sql
select count(*) from nombreTabla
```
* Para contar una columna especifica se reemplaza el simbolo asterisco(*) por el nombre de la columna.
```sql
select count(nombreColumna) from nombreTabla
```
* Contar registros con un condicional
```sql
select count(nombreColumna) from nombreTabla where nombreColumna Like '%Letra%'
```

## 19.- Sumar registros (SUM)

Sirver para sumar datos de diferentes registros.

```sql
select sum(nombreColumna) from nombreTabla
```
* Sumar con condicional
```sql
select sum(nombreColumna1) from nombreTabla where nombreColumna2 like '%Letra%'
```
>nombreColumna1 es lo que se sumara y nombreColumna2 es lo que se seleccionara para realizar la suma.

## 20 .- Funciones con registros (Max - Min - Group by)

* Buscar el valor **MINIMO** en una columna especifica.
```sql
select min(nombreColumna) from nombreTabla;
```
* Buscar el valor **MAXIMO** en una columna especifica.
```sql
select max(nombreColumna) from nombreTabla;
```

* Agrupa los resultados en este caso repetidos de una columna.

```sql
select nombreColumna, count(*)
from nombreTabla
group by nombreColumna
```
segundo ejemplo
```sql
select nombreColumna1, nombreColumna2 from nombreTabla
where nombreColumna1='palabra'
group by nombreColumna1, nombreColumna2
```
> En **group by** debe colocarse lo mismo que se agrego inicialmente en el **select**
* Ejemplo:

**Tabla Base**
|nombre|identificacion|salario|
|:--:|:--:|:--:|
|trabajador1|1|2500|
|trabajador2|2|4500|
|trabajador3|3|3500|
|trabajador1|4|5500|

 **QUERY a ejecutar**
```sql
select nombre, max(salario)as maximo, min(salario)as minimo from planilla group by nombre
```

**Resultado**
|nombre|maximo|minimo|
|:--:|:--:|:--:|
|trabajador1|5500|2500|
|trabajador2|4500|4500|
|trabajador3|3500|3500|

>Como se ve el trabajador 1 posee un maximo y minimo distinto, ya que tenia 2 registros en la tabla.
>
>__~~lo entendi pero no supe explicarlo en palabras..espero que el ejemplo sirva~__
>
>**RESUMEN** para agrupar columna entre registros identicos.

## 21.- Funcion Promedio (AVG)

Promedio de registros de una columna

```sql
select avg(nombreColumna) from nombreTabla
```
>La columna seleccionada debe poseer numeros.

ejemplo con **group by**
```sql
select nombreColumna1, avg(nombreColumna2) from nombreTabla group by nombreColumna1
```
## 22.- Filtrado de grupos (HAVING)

Realiza un filtro en una columna especificada con parametros que nosotros le damos.

```sql
select nombreColumna1, nombreColumna2 from nombreTabla
where nombreColumna1='palabra'
group by nombreColumna1, nombreColumna2
having nombreColumna2 > valorNumerico
```
>aqui buscara en la primera columna con la palabra que nosotros especifiquemos y filtrara quien posee un valor numerico mayor al que nosotros le coloquemos.
>
>El **where** trabaja sobre el **select** y el **having** trabaja sobre el **group by**

Ejemplo incluye **order by**
```sql
select nombreColumna1, nombreColumna2 from nombreTabla
where nombreColumna1='palabra'
group by nombreColumna1, nombreColumna2
having nombreColumna2 > valorNumerico
order by nombreColumna1
```
Ejemplo N°2:
```sql
select nombreTrabajador, sueldo from ListaTrabajador
where nombreTrabajador='Pedro'
group by nombreTrabajador, sueldo
having sueldo > 2500
```

## 23.- Buscar resultados diferentes (DISTINCT)

Sirve para ignorar datos duplicados en un registro, al realizar una busqueda.

```sql
select distinct nombreColumna from nombreTabla
```

Ejemplo 2

contara los datos despues de aplicar distinct, para no contar los repetidos.

```sql
select count(distinct nombreColumna) from nombreTabla
```

## 24.- ver rango de registro (BETWEEN)

* Reliza una busqueda en una columna especifica con parametros que nosotros entregamos.

```sql
select * from nombreTabla
where nombreColumna between valorInicial and valorFinal
```
> Realizara una busqueda en la columna especificada y entregara los resultados que esten entre el rango inicial y rango Final.

* Para mostrar registro que quedan excluidos del rango anteponer **not**
```sql
select * from nombreTabla
where nombreColumna not between valorInicial and valorFinal
```

## 25.- Restringir valores de Tabla (UNIQUE)

Sirve para agregar restricciones a una tabla, agregando a una columna la opcion de prohibir datos duplicados

>A diferencia del **primary key** se puede ocupar en cualquier campo y las veces que sean necesarias. Ejemplo puede estar en dos columnas de una tabla.

```sql
alter table nombreTabla
add constraint nombreRestriccion
unique(nombreColumna)
```

## 26.- Eliminar restriccion de una tabla (DROP CONSTRAINT)

Elimina restricciones de una tabla.

```sql
alter table nombreTabla
drop constraint nombreRestriccion
```

## 27.- Relacionar dos tablas con llave Foranea (FOREIGN KEY)

Sirve para relacionar dos tablas y datos existentes, asi se evita que se ingrese datos inexistente.

```sql
alter table nombretabla add constraint nombreForeignKey
foreign key(columnaOrigen) references tablaDestino(ColumnaDestino)
```

>(ColumnaOrigen) -> (ColumnaDestino)

## 28.- Crear una Función (FUNCTION)

 Como el nombre indica, realizara una funcion especifica que se programara. 

creacion de una funcion
```sql
create or replace function NombreFuncion(valoresRecibidos o variables)
returns TipoDato
as 
$$
Codigo a Implementar
$$
language LenguajeaOcupar

```

Para ejecutar una funcion:

```sql
select nombreFuncion (valores a enviar);
```

Ejemplo suma de dos numeros:

```sql
create or replace function Suma(numero1 int,numero2 integer)
returns integer
as 
$$
select numero1 + numero2;
$$
language SQL
```

Ejecucion de la funcion:
```sql
select Suma ('33','66');
```
Resultado
|Suma|
|:-:|
| 99 |

Ejemplo dos, devolucion de informacion mediante nombre.

```sql
create function  buscarSalario(varchar) returns integer
as
$$
select salario from planilla
where nombre = $1
$$
language sql
```
## 29.- funcion sin parametro y sin retorno de resultado.

estructura ejemplo

```sql
create function nombreFuncion() returns void
as
$$
insert into nombreTabla values (Datos);
$$
language sql
```
>El **VOID** hace que no devuelva ningun valor.

Para ejecutar funcion
```sql
select nombreFuncion();
```

Ejemplo 1
```sql
create function InsertarPersona() returns void
as
$$
insert into planilla values ('david','4','6500');
insert into planilla values ('luis','5','7000');
insert into planilla values ('german','6','2000');
insert into planilla values ('olga','7','4500');
$$
language sql
```
> VOID especifica que no retornara un valor(sujeto a correción).

Ejemplo 2
```sql
create function buscarInfo(int) returns planilla
as
$$
select * from planilla
where nid = $1;
$$
language sql

Select buscarInfo(DatoBuscar)
```
## 30.- Como hacer un TOP (LIMIT)

PostgreSQL no posee un TOP como tal, pero se puede ocupar el LIMIT para realizar la misma funcion.

```sql
select * from nombreTabla
limit NumeroResultadosAMostrar
```
Ejemplo
```sql
select * from lista
limit 5
```

## 31.- Como hacer "Disparador" y su funcion (TRIGGER-BEFORE)

Son codigos que se disparan(ejecuta) en la base de datos.

```sql
create function nombreFuncion() returns Trigger
as
$$
begin

CodigoFuncion

end
$$
language nombreLenguaje;


```

Ejemplo
Guarda primero la informacion antes de realizar un update.
Sentencia para un trigger que se active antes de que se realice un update.

```sql
create function SP_test() returns Trigger
as
$$
begin

insert into "Log_Triggers" values (old.nombre, old.nid, old.salario);
return new;

end
$$
language plpgsql;

create trigger TR_Update before Update on planilla 
for each row
execute procedure SP_test();
```
>En values esta la opcion ocupar dos clausulas **NEW**, que contiene la informacion nueva que contiene el update, y **OLD** que guarda la informacion que actualmente contiene la tabla.

>Si no se coloca **return new;** no funcionara el trigger, al tenerlo se le informa que ya puede realizar la accion con la nueva informacion.

>for each row --> significado por cada linea que se trabaje. Por cada update que se ejecute.(Eso dice el video)

>Resumen, guarda la informacion antigua en otra tabla antes de ingresar los nuevos datos.

## 32.-  Como usar clausula AFTER para el insert (TRIGGER-AFTER)



```sql
create function SP_TR_Insert() returns trigger
as 
$$
Declare 

Usuario Varchar(250) := User;
Fecha Date := current_date;
Tiempo Time := current_time;

begin

insert into log_triggers values(new.nombre, new.nid, new.salario, Usuario, Fecha, Tiempo);

return new;
end
$$
language plpgsql;
```

> **:=** es para asignar valor a una variable en una funcion.
>
> **NEW.** es para establecer que recibira informacion nueva a diferencia del trigger anterior que ocupaba OLD

```sql
Create trigger TR_Insert after insert on planilla
for each row
execute procedure SP_TR_Insert();
```
>En el trigger se ocupara el after para que se ejecute despues de ejecutar el insert
>
>**for each row** por cada linea ejecuta

**Resumen**
Al realizar un insert a una tabla X(Planilla), ejecuta la funcion y "crea" un respaldo de la informacion insertada en otra tabla.

## 33.- Clausula IN

Se utiliza "in" para averiguar si el valor de un campo está incluido en una lista de valores especificada.

Ejemplo:

Uso actual con multiples condiciones (OR)
```sql
select * from planilla
where nid = '2' or nid = '11' or nid = '3';
```

Mismo ejemplo con clausula IN
```sql
select * from planilla
where nid in ('2','11', '3');
```

>siempre que sea posible, emplee condiciones de búsqueda positivas ("in"), evite las negativas ("not in") porque con ellas se evalúan todos los registros y esto hace más lenta la recuperación de los datos.

## 34.- Clausulas LIMIT y OFFSET

Offset establece el lugar de inicio del LIMIT

```sql
select * from nombre_tabla limit numero_limit offset Numero_offset
```
> El limit se la cantidad de resultados que entregara la consulta y offset es desde donde se consideran los datos.

EJEMPLO

Tabla Completa

|nombre|maximo|
|:--:|:--:|
|trabajador1|5500|
|trabajador2|4500|
|trabajador3|3500|
|trabajador4|5500|
|trabajador5|4500|
|trabajador6|3500|

Query a ejecutar

```sql
select * from trabajador limit 2 offset 2
```

Resultado

|nombre|maximo|
|:--:|:--:|
|trabajador3|3500|
|trabajador4|5500|

## 35.- Crear Vista (VIEW)

Es una tabla "resumen" que obtiene datos de otras tablas y no es temporal, ademas es posible mostrar algunas partes de las tablas.

```sql
create view view_datafrompersona
as
select nombre,nid from planilla;

select * from view_datafrompersona;
```
> es posible ocupar cualquier opcion disponible que los select posee.
>
>La tabla vista es dinamica, si las tablas desde donde provienen los datos cambian su informacion, en la vista tambien se mostraran.
>
>la vista puede realizar la union de varias tablas.

## 36.- Consulta de dos o mas tablas (UNION)

El operador "union" combina el resultado de dos o más instrucciones "select" en un único resultado.

Se usa cuando los datos que se quieren obtener pertenecen a distintas tablas y no se puede acceder a ellos con una sola consulta.

Es necesario que las tablas referenciadas tengan tipos de datos similares, la misma cantidad de campos y el mismo orden de campos en la lista de selección de cada consulta. No se incluyen las filas duplicadas en el resultado, a menos que coloque la opción "all".

Se deben especificar los nombres de los campos en la primera instrucción "select".

Puede emplear la cláusula "order by".

Puede dividir una consulta compleja en varias consultas "select" y luego emplear el operador "union" para combinarlas.

```sql
select nombre,nid from planilla
union all
select nombre, idpersona from persona;
```
>al agregar **ALL** despues de union mostrara los resultados duplicados.

Para ver el origen de los datos se ocupa lo siguiente.

```sql
select nombre, nid, 'Planilla' as Origen from planilla
union all
select nombre, idpersona, 'Persona' from persona;
```
>se agrega una nueva columna llamada origen y se agrega en cada select un tercer dato, epsecificando su origen

Para ordenar el origen se agrega **Order By**
```sql
select nombre, nid, 'Planilla' as Origen from planilla
union all
select nombre, idpersona, 'Persona' from persona
order by Origen;
```

Tambien es posible crear una vista con los datos requeridos, desde dos tablas.
```sql
create view View_Union
as
select nombre, nid, 'Planilla' as Origen from planilla
union all
select nombre, idpersona, 'Persona' from persona
order by Origen;

select * from View_Union;
```

## 37.- Combinar 2 o mas tablas (INNER JOIN)

Un join es una operación que relaciona dos o más tablas para obtener un resultado que incluya datos (campos y registros) de ambas; las tablas participantes se combinan según los campos comunes a ambas tablas.

Hay tres tipos de combinaciones:

* combinaciones internas (inner join o join)
* combinaciones externas
* combinaciones cruzadas

También es posible emplear varias combinaciones en una consulta "select", incluso puede combinarse una tabla consigo misma.

La combinación interna emplea "join", que es la forma abreviada de "inner join". Se emplea para obtener información de dos tablas y combinar dicha información en una salida.

La sintaxis básica es la siguiente:

 select CAMPOS
  from TABLA1
  join TABLA2
  on CONDICIONdeCOMBINACION;

```sql
select * from planilla
inner join persona
on planilla.nid = persona.idpersona
```
>cuando se combina información de varias tablas, es necesario especificar qué registro de una tabla se combinará con qué registro de la otra tabla, con "on". Se debe especificar la condición para enlazarlas, es decir, el campo por el cual se combinarán, que tienen en común.
>
>"on" hace coincidir registros de ambas tablas basándose en el valor de tal campo, en el ejemplo, el campo "codigoeditorial" de "libros" y el campo "codigo" de "editoriales" son los que enlazarán ambas tablas. Se emplean campos comunes, que deben tener tipos de datos iguales o similares.

Para resumir se pueden agregar alias
```sql
select * from planilla as a1
inner join persona b1
on a1.nid = b1.idpersona
```

## 38.- Combinacion Externa Izquierda (LEFT JOIN)

Si queremos saber qué registros de una tabla NO encuentran correspondencia en la otra, es decir, no existe valor coincidente en la segunda, necesitamos otro tipo de combinación, "outer join" (combinación externa).

Las combinaciones externas combinan registros de dos tablas que cumplen la condición, más los registros de la segunda tabla que no la cumplen; es decir, muestran todos los registros de las tablas relacionadas, aún cuando no haya valores coincidentes entre ellas.

```sql
select * from planilla as a1
left join persona a2
on a1.nid = a2.idpersona
```
> En resumen le da prioridad a mostrar los tados de la tabla izquierda(la primera tabla en el select).
>
>Si en los datos que muestra no tiene relacion mostrara NULO.

## 39.- Combinacion externa derecha (Right Join)

Vimos que una combinación externa izquierda (left join) encuentra registros de la tabla izquierda que se correspondan con los registros de la tabla derecha y si un valor de la tabla izquierda no se encuentra en la tabla derecha, el registro muestra los campos correspondientes a la tabla de la derecha seteados a "null".

Una combinación externa derecha ("right outer join" o "right join") opera del mismo modo sólo que la tabla derecha es la que localiza los registros en la tabla izquierda.

```sql
select * from planilla as a1
right join persona as a2
on a1.nid = a2.idpersona;
```

## 40.- Combinacion de ambos lados (Full Join)

Vimos que un "left join" encuentra registros de la tabla izquierda que se correspondan con los registros de la tabla derecha y si un valor de la tabla izquierda no se encuentra en la tabla derecha, el registro muestra los campos correspondientes a la tabla de la derecha seteados a "null". Aprendimos también que un "right join" opera del mismo modo sólo que la tabla derecha es la que localiza los registros en la tabla izquierda.

Una combinación externa completa ("full outer join" o "full join") retorna todos los registros de ambas tablas. Si un registro de una tabla izquierda no encuentra coincidencia en la tabla derecha, las columnas correspondientes a campos de la tabla derecha aparecen seteadas a "null", y si la tabla de la derecha no encuentra correspondencia en la tabla izquierda, los campos de esta última aparecen conteniendo "null".

```sql
select * from planilla as a1
full join persona as a2
on a1.nid = a2.idpersona;
```

## 41.- Combinaciones posibles (Cross Join)

hay tres tipos de combinaciones: 1) combinaciones internas (join), 2) combinaciones externas (left, right y full join) y 3) combinaciones cruzadas.

Las combinaciones cruzadas (cross join) muestran todas las combinaciones de todos los registros de las tablas combinadas. Para este tipo de join no se incluye una condición de enlace. Se genera el producto cartesiano en el que el número de filas del resultado es igual al número de registros de la primera tabla multiplicado por el número de registros de la segunda tabla, es decir, si hay 5 registros en una tabla y 6 en la otra, retorna 30 filas.

```sql
select * from planilla as a1
cross join persona as a2;
```
## 42.- Vistas (with check option)

Esta sentencia trabaja unicamente con las vistas.
 Evita **insert** fantasmas, esto quiere decir que al realizar insert a una vista y si esta ultima se creó utilizando un where como el siguiente ejemplo;
 ```sql
create view view_personas
as
select * from NombreTabla
where "Lugar" = 'America'
 ```
Si el insert no contiene en la columna "Lugar" el contenido America, esta informacion no se mostrara en la vista que se esta trabajando, pero la informacion si estara presente en la tabla desde donde la vista obtiene la información.

Para evitar esta situacion se agrega el **With check Option** a la query al momento de crear la vista.

 ```sql
create view view_personas
as
select * from NombreTabla
where "Lugar" = 'America'
with check option
 ```

 Al momento de realizar un insert y al no cumplir el where, entregara un error.

## 43.- Resumen JOIN

![Alt text](/img/Joins_SQL.PNG "JOINS SQL")

## 44.- Funciones Matematicas (ABS, CBRT, Ceiling, Floor)

### ABS: 
Valor absoluto de un argumento(Numero).
```sql
select abs(-50)
```
Salida:
|abs|
|:--:|
|50|

### CBRT: 
Retornar raiz cubica de un numero.
```sql
select cbrt(27)
```
Salida:
|cbrt|
|:--:|
|3|

### Ceiling:
Redondear Numero al valor siguiente.
```sql
select ceiling(9.22)
```
Salida:
|ceiling|
|:--:|
|10|

### Floor:
Redondear numero al valor anterior.

```sql
select floor(9.22)
```
Salida:
|floor|
|:--:|
|9|

## 45.- Funciones Matematicas (Power, Round, Sign, Sqrt)

### Power(X, Y) - Potencia

X: es el numero que se desea aumentar en la potencia.
Y: es el numero por el cual se va a aumentar la potencia.

```sql
select power(4,4)
```
Salida:
|power|
|:--:|
|256|

### Round(N, D)

Round sirve para redondear al mas cercano al numero inferior.

N: es el numero que se desea redondear.

D: es el numero de decimales que se desea.

* Ejemplo normal:
```sql
select round(15.55);
```
Salida:
|round|
|:--:|
|15|

* Ejemplo con decimal:
```sql
select round(15.5555, 2);
```
Salida:
|round|
|:--:|
|15.56|

### Sing(X)

si el numero que se le asigna a sign es;

Positivo: 1
Negativo: -1
Cero: 0

* Ejemplo con positivo:
```sql
select sign(5);
```
Salida:
|sign|
|:--:|
|1|
* Ejemplo con negativo:
```sql
select sign(-5);
```
Salida:
|sign|
|:--:|
|-1|
* Ejemplo con cero:
```sql
select sign(0);
```
Salida:
|sign|
|:--:|
|0|

### Sqrt(X)

Sirve para entregar la raiz cuadrada, de un numero.
```sql
select sqrt(64);
```
Salida:
|sqrt|
|:--:|
|8|

## 46.- Funciones Matematicas (Mod, Pi, Random, Trunc)

### Mod(X, Y)

Entrega el resto de una division.
```sql
select Mod(33,2);
```
Salida:
|mod|
|:--:|
|1|

### Pi()

Entrega el numero pi.
```sql
select Pi();
```
Salida:
|pi|
|:--:|
|3.14159265358979|

### Random()

Entrega numeros aleatorios entre 0 y 1.
```sql
select Random();
```
Salida:
|random|
|:--:|
|0.227234418038279|

### Trunc (X)/(X, D)

Entrega el numero entero.
```sql
select Trunc(-24.336699);
```
Salida:
|trunc|
|:--:|
|-24|

Tambien es posible especificar la cantidad de decimales que debe entregar.
```sql
select Trunc(-24.336699, 3);
```
Salida:
|trunc|
|:--:|
|-24.336|

## 47.- Manejo de caracteres (char_length, Upper, Lower, Position)

### Char_Length

Sirve para realizar un conteo de los caracteres en la palafra y/o frase que se le entrega.
```sql
select char_length('Planeta Tierra');
```
Salida:
|cher_length|
|:--:|
|14|

### Upper

Sirve para pasar el texto completo a mayuscula.
```sql
select Upper('Planeta Tierra');
```
Salida:
|upper|
|:--:|
|PLANETA TIERRA|

### Lower
Sirve para pasar el texto completo a minuscula.
```sql
select Lower('Planeta Tierra');
```
Salida:
|lower|
|:--:|
|planeta tierra|

### Position

Sirve para entregar la posicion de un STRING dentro de otro.
Position es sensible a mayusculas o minusculas.
* Ejemplo 1:
```sql
select position('Planeta'in 'Planeta Tierra');
```
Salida:
|position|
|:--:|
|1|
* Ejemplo 2:
```sql
select position('Tierra'in 'Planeta Tierra');
```
Salida:
|position|
|:--:|
|9|
>En caso de que se entrege una palabra diferente para buscar su posicion en una frase, esté entregara el valor CERO.

## 48.- Manejo de caracteres (SUBSTRING, TRIM)

### SubString

Toma una seccion del texto, desde el primer numero que pide en el from hasta el segundo numero que pide en el for.

```sql
select substring ('Texto' from NumeroInicial for NumeroFinal);
```

Ejemplo:
```sql
select substring ('Planeta Tierra' from 2 for 6);
```
Salida:
|substring|
|:--:|
|laneta|

### Trim

#### Default

La opcion por default permite eliminar caracteres(solo espacios en blanco) al princio y al final de un string.

```sql
select trim (' Planeta Tierra ');
```
Salida:
|trim|
|:--:|
|Planeta Tierra|

#### Trim Leading

Permite eliminar caracteres al principio de una cadena(texto).
```sql
select trim (leading '-' from '--Planeta Tierra--');
```
Salida:
|ltrim|
|:--:|
|Planeta Tierra--|

#### Trim Trailing

Permite eliminar caracteres al final de una cadena(texto).
```sql
select trim (leading '-' from '--Planeta Tierra--');
```
Salida:
|rtrim|
|:--:|
|--Planeta Tierra|

#### Trim Both

Permite eliminar caracteres al principio y al final de una cadena(texto).

```sql
select trim (leading '-' from '--Planeta Tierra--');
```
Salida:
|btrim|
|:--:|
|Planeta Tierra|

## 49.- Manejo de caracteres (LTRIM, RTRIM, SUBSTR, LPAD, RPAD)

### Ltrim

Elimina el texto o caracteres que se le indiquen del  lado izquierdo.

* Ejemplo 1
```sql
select ltrim ('   Planeta Tierra');
```
Salida:
|ltrim|
|:--:|
|Planeta Tierra|

* Ejemplo 2

```sql
select ltrim ('***Planeta Tierra***', '*');
```
Salida:
|ltrim|
|:--:|
|Planeta Tierra***|

### Rtrim

Elimina texto o caracteres que se le indique del lado derecho.

```sql
select rtrim ('***Planeta Tierra***', '*');
```
Salida:
|rtrim|
|:--:|
|***Planeta Tierra|

### Substr

Muestra los caracteres que se le indiquen.

* Ejemplo 1
```sql
select substr('Planeta Tierra', 5);
```
Salida:
|substr|
|:--:|
|eta Tierra|

* Ejemplo 2
```sql
select substr('Planeta Tierra', 5, 8);
```
Salida:
|substr|
|:--:|
|eta Tier|

### Lpad

Agrega caracteres tantas veces como se le indique, en el lado izquierdo. 

Por lo tanto primero contara los caracteres existentes y despues agregará los faltantes hasta completar el numero indicado.

```sql
select lpad('Planeta Tierra',16,'*');
```
Salida:
|lpad|
|:--:|
|**Planeta Tierra|

### Rpad

Lo mismo que el **LPAD** pero del lado derecho.

```sql
select rpad('Planeta Tierra',16,'*');
```
Salida:
|rpad|
|:--:|
|Planeta Tierra**|

## 50.- Funciones Fecha y Tiempo(Date, Time, Timestamp, Extract)

### Current_Date
Para saber fecha actual
```sql
select current_date;
```
Salida:
|current_date|
|:--:|
|2019-02-24|

### Current_Time
Para saber Hora actual y zona horaria.
```sql
select current_time;
```
Salida:
|current_time|
|:--:|
|21:47:53.611545-03:00|

### current_timestamp

Entrega fecha actual, hora actual y zona horaria.
```sql
select current_timestamp;
```
Salida:
|current_timestamp|
|:--:|
|2019-02-25 20:30:17.838263-03|

### extract

Puede extraer un dato en especifico.

Ejemplos
```sql
select extract(century from current_timestamp);
select extract(quarter from current_timestamp);
select extract(year from current_timestamp);
select extract(month from current_timestamp);
select extract(week from current_timestamp);
select extract(dow from current_timestamp);
select extract(day from current_timestamp);
select extract(doy from current_timestamp);
select extract(hour from current_timestamp);
select extract(minute from current_timestamp);
select extract(second from current_timestamp);
```
Salida:
|date_part|Tipo Dato|
|:--:|:--:|
|21|Century|
|1|Quarter|
|2019|Year|
|2|Month|
|9|week|
|1|dow|
|25|Day|
|56|Doy|
|20|Hour|
|47|Minute|
|32.059645|Second|
>Quarter muestra en que cuarto del año se encuentra
>
>Century muestra el siglo.
>
>Dow es dia de la semana
>
>Doy es dia del año

## 51.- Operadores Controladores Null

Para saber si una columna trae valores nulos ocupar lo siguiente:

```sql
select * from NombreTabla
where "Nombre Columna" is null;
```

Para saber los que no traen nulo.
```sql
select * from NombreTabla
where "Nombre Columna" is not null;
```

## 52.- Crear Secuencias(Create, Alter, Drop)

Es un registro para crear valores secuenciales unicos, y asignarlos a campos numericos.

La secuencia es un numero inicial que aumentara hasta un limite determinado.

Sirve para los PK.

### Create
```sql
create sequence NombreSecuencia
start with N°Comienza
increment by N°Incrementar
minvalue N°ValorMinimo
maxvalue N°Maximo
cycle;
```
> cycle es para que no devuelva un error al intentar superar el maxvalue. Este es opcional.

Ejemplo:
```sql
create sequence sec_Index
start with 1
increment by 20
minvalue 1
maxvalue 100
cycle;

select * from sec_Index;
```

Para ejecutar el autoincremento
```sql
select nextval('NombreSecuencia');
```
### Alter
Para modificar una secuencia ocupar el alter.
```sql
alter sequence NombreSecuencia
start with N°Comienza
increment by N°Incrementar
minvalue N°ValorMinimo
maxvalue N°Maximo
restart Valor
cycle;
```
>cambiar al valor que se desea modificar en la secuencia ya creada.
>
>En caso de que de error y diga el restart no puede ser menor que el minvalue agregar restart con el mismo valor que minvalue
>
>Tambien se puede cambiar **cycle** **no cycle** pero este al querer superar su valor maximo presentara un error.

### Drop

Para Eliminar una secuencia.
```sql
Drop sequence NombreSecuencia
```
