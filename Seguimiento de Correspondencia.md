# Seguimiento de correspondencia

:books: Base de datos:  **activiti**

📋 Tabla consultadas:  **ACT_RU_VARIABLE**

### Atributos de las tablas:

| Campo             | Tipo    | 
|-------------------|-------------|
| ID_   | INT    |
| REV_        | STRING       | 
| TYPE_ | STRING | 
| NAME_         | STRING  | 
| EXECUTION_ID_         | INT  | 
| PROD_INST_ID_        | INT  | 
| TASK_ID_         | INT  | 
| BYTEARRAY_ID_         | INT  | 
| DOUBLE_         | DOUBLE  | 
| LONG_ID_         | LONG  | 
| TEXT_ID_         | STRING  | 
| TEXT2_ID_         | STRING  | 


### Resultado despues de las consulta:

| Campo             | Tipo    | Comentario| 
|-------------------|-------------|-------------|
| ID   | INT    ||
| Numero Radicado        | STRING       | |
| Num Identificacion | STRING | |
| Remitente         | STRING  | |
| Destinatario         | STRING  | |
| Tipo Asunto         | STRING  | |
| Estado         | STRING  | |
| FechaCreacion        | DATE  | |

***

### Consulta SQL🔍

Obtiene todos los campos sin filtro:
 
~~~sql
select ACT_RU_VARIABLE.PROC_INST_ID_ as 'ID',
    MAX(CASE WHEN NAME_ = 'numRadicado' THEN TEXT_ END) as 'Numero Radicado',
    MAX(CASE WHEN NAME_ = 'numDocRem' THEN BYTEARRAY_ID_  END) as 'Num Identificacion',
    MAX(CASE WHEN NAME_ = 'nomRemitente' THEN TEXT_ END) as 'Remitente',
    MAX(CASE WHEN NAME_ = 'nombreTramita' THEN TEXT_ END)as 'Destinatario',
    MAX(CASE WHEN NAME_ = 'tipoAsunto_LABEL' THEN TEXT_ END) as 'Tipo Asunto',
    MAX(CASE WHEN NAME_ = 'estado' THEN TEXT_ END) as 'Estado'
	from activiti.ACT_RU_VARIABLE
	GROUP BY PROC_INST_ID_
~~~

_Tiempo de duración de la consulta y datos totales : 36884 row(s) returned  2.922 s_


## Nueva query con filtros sin paginación 

### Filtro por numero de radicado
Esta query necesita el nombre del filtro “NAME_” y el valor a filtrar “TEXT_”, en este caso se filtro por NAME_ = “numRadicado” y TEXT_ = “2211006663” es decir por numero de radicado

~~~sql
select ACT_RU_VARIABLE.PROC_INST_ID_ as 'ID',
    MAX(CASE WHEN NAME_ = 'numRadicado' THEN TEXT_ END) as 'Numero Radicado',
    MAX(CASE WHEN NAME_ = 'numDocRem' THEN BYTEARRAY_ID_  END) as 'Num Identificacion',
    MAX(CASE WHEN NAME_ = 'nomRemitente' THEN TEXT_ END) as 'Remitente',
    MAX(CASE WHEN NAME_ = 'nombreTramita' THEN TEXT_ END)as 'Destinatario',
    MAX(CASE WHEN NAME_ = 'tipoAsunto_LABEL' THEN TEXT_ END) as 'Tipo Asunto',
    MAX(CASE WHEN NAME_ = 'estado' THEN TEXT_ END) as 'Estado',
    MAX(CASE WHEN NAME_ = 'numDocRem_LABEL' THEN TEXT_ END) as 'Numero de documento Remitente',
    MAX(CASE WHEN NAME_ = 'fecRadicado' THEN TEXT_ END) as 'Fecha radicado'
	from activiti.ACT_RU_VARIABLE
  where PROC_INST_ID_ in (
    select PROC_INST_ID_  from activiti.ACT_RU_VARIABLE
	    where TEXT_ = "2211006663" and NAME_ = "numRadicado"
      )
	GROUP BY PROC_INST_ID_
~~~

_Tiempo de ejecución en Workbench :0.859 sec / 0.000 sec_

***

### Filtro por Estado
esta query necesita el nombre del filtro “NAME_” y el valor a filtrar “TEXT_”, en este caso se filtro por NAME_ = “estado” y TEXT_ = “Anulado” es decir por estado

~~~sql
select ACT_RU_VARIABLE.PROC_INST_ID_ as 'ID',
	MAX(CASE WHEN NAME_ = 'numRadicado' THEN TEXT_ END) as 'Numero Radicado',
	MAX(CASE WHEN NAME_ = 'numDocRem' THEN BYTEARRAY_ID_  END) as 'Num Identificacion',
	MAX(CASE WHEN NAME_ = 'nomRemitente' THEN TEXT_ END) as 'Remitente',
	MAX(CASE WHEN NAME_ = 'nombreTramita' THEN TEXT_ END)as 'Destinatario',
	MAX(CASE WHEN NAME_ = 'tipoAsunto_LABEL' THEN TEXT_ END) as 'Tipo Asunto',
	MAX(CASE WHEN NAME_ = 'estado' THEN TEXT_ END) as 'Estado',
  MAX(CASE WHEN NAME_ = 'numDocRem_LABEL' THEN TEXT_ END) as 'Numero de documento Remitente',
  MAX(CASE WHEN NAME_ = 'fecRadicado' THEN TEXT_ END) as 'Fecha radicado'
	from activiti.ACT_RU_VARIABLE
    where PROC_INST_ID_ in (
      select PROC_INST_ID_  from activiti.ACT_RU_VARIABLE
				where TEXT_ = "Anulado" and NAME_ = "estado"
      )
	  GROUP BY PROC_INST_ID_
~~~
_Tiempo de ejecución en Workbench : 0.703 sec / 0.000 sec_


***

### Filtro por fecha
esta query necesita el nombre del filtro “NAME_” y el valor a filtrar “TEXT_”, en este caso se filtro por NAME_ = “'fecRadicado' ” y TEXT_ = “between '23-09-2020' AND '24-09-2020'” es decir por Fecha sin paginar

~~~sql
select ACT_RU_VARIABLE.PROC_INST_ID_ as 'ID',
	MAX(CASE WHEN NAME_ = 'numRadicado' THEN TEXT_ END) as 'Numero Radicado',
	MAX(CASE WHEN NAME_ = 'numDocRem' THEN BYTEARRAY_ID_  END) as 'Num Identificacion',
	MAX(CASE WHEN NAME_ = 'nomRemitente' THEN TEXT_ END) as 'Remitente',
	MAX(CASE WHEN NAME_ = 'nombreTramita' THEN TEXT_ END)as 'Destinatario',
	MAX(CASE WHEN NAME_ = 'tipoAsunto_LABEL' THEN TEXT_ END) as 'Tipo Asunto',
	MAX(CASE WHEN NAME_ = 'estado' THEN TEXT_ END) as 'Estado',
  MAX(CASE WHEN NAME_ = 'numDocRem_LABEL' THEN TEXT_ END) as 'Numero de documento Remitente',
  MAX(CASE WHEN NAME_ = 'fecRadicado' THEN TEXT_ END) as 'Fecha radicado'
	  from activiti.ACT_RU_VARIABLE
    where PROC_INST_ID_ in (
      select PROC_INST_ID_  from activiti.ACT_RU_VARIABLE
		    where NAME_ = "fecRadicado" AND TEXT_ between '23-09-2020' AND '24-09-2020'
     )
	  GROUP BY PROC_INST_ID_ 
~~~

_Tiempo de ejecución en Workbench : 1.203 sec / 0.203 sec_


***

### Filtro por estado, con paginado
esta query necesita el nombre del filtro “NAME_” y el valor a filtrar “TEXT_”, en este caso se filtro por NAME_ = “estado” y TEXT_ = “Anulado” es decir por estado Para paginarlo además necesita un limit (ej:4) y un offset (ej:3)

~~~sql
select ACT_RU_VARIABLE.PROC_INST_ID_ as 'ID',
	MAX(CASE WHEN NAME_ = 'numRadicado' THEN TEXT_ END) as 'Numero Radicado',
	MAX(CASE WHEN NAME_ = 'numDocRem' THEN BYTEARRAY_ID_  END) as 'Num Identificacion',
	MAX(CASE WHEN NAME_ = 'nomRemitente' THEN TEXT_ END) as 'Remitente',
	MAX(CASE WHEN NAME_ = 'nombreTramita' THEN TEXT_ END)as 'Destinatario',
	MAX(CASE WHEN NAME_ = 'tipoAsunto_LABEL' THEN TEXT_ END) as 'Tipo Asunto',
	MAX(CASE WHEN NAME_ = 'estado' THEN TEXT_ END) as 'Estado',
  MAX(CASE WHEN NAME_ = 'numDocRem_LABEL' THEN TEXT_ END) as 'Numero de documento Remitente',
  MAX(CASE WHEN NAME_ = 'fecRadicado' THEN TEXT_ END) as 'Fecha radicado'
	  from activiti.ACT_RU_VARIABLE
    where PROC_INST_ID_ in (
      select PROC_INST_ID_  from activiti.ACT_RU_VARIABLE
			  where TEXT_ = "Anulado" and NAME_ = "estado"
       )
	  GROUP BY PROC_INST_ID_ limit 4 offset 3
~~~

_Tiempo de ejecución en Workbench : 0.219 sec / 0.000 sec_

***

### Otros filtros

Los demás filtros son iguales solo hay que cambia el NAME_ y el TEXT_ .

LISTA DE POSIBLES  “NAME_” (filtros)

numRadicado :arrow_right: Número Radicado

numDocRem :arrow_right: Num Identificacion

nomRemitente :arrow_right: Remitente

nombreTramita :arrow_right: Destinatario

tipoAsunto_LABEL :arrow_right: Tipo Asunto

estado :arrow_right: Estado

fecRadicado :arrow_right: Fecha radicado

***

### Otras consultas

Query con diferenciación entre Radicados en curso (%unifica%) y Radicados en curso Internos (%inter%)
con join de la tabla ACT_RU_EXECUTION :

~~~sql
select ru.PROC_INST_ID_ as 'ID',
	MAX(CASE WHEN ru.NAME_ = 'numRadicado' THEN TEXT_ END) as 'Numero Radicado',
	MAX(CASE WHEN ru.NAME_ = 'numDocRem' THEN BYTEARRAY_ID_  END) as 'Num Identificacion',
	MAX(CASE WHEN ru.NAME_ = 'nomRemitente' THEN TEXT_ END) as 'Remitente',
	MAX(CASE WHEN ru.NAME_ = 'nombreTramita' THEN TEXT_ END)as 'Destinatario',
	MAX(CASE WHEN ru.NAME_ = 'tipoAsunto_LABEL' THEN TEXT_ END) as 'Tipo Asunto',
	MAX(CASE WHEN ru.NAME_ = 'estado' THEN TEXT_ END) as 'Estado',
  MAX(CASE WHEN ru.NAME_ = 'numDocRem_LABEL' THEN TEXT_ END) as 'Numero de documento Remitente',
  MAX(CASE WHEN ru.NAME_ = 'fecRadicado' THEN TEXT_ END) as 'Fecha radicado',
  exe.PROC_DEF_ID_
	  from activiti.ACT_RU_VARIABLE ru join activiti.ACT_RU_EXECUTION exe on ru.PROC_INST_ID_ = exe.PROC_INST_ID_
    where exe.PROC_DEF_ID_ like '%unifica%' and ru.PROC_INST_ID_ in (
      select PROC_INST_ID_  from activiti.ACT_RU_VARIABLE
			  where NAME_ = "fecRadicado" AND TEXT_ between '23-09-2020' AND '24-09-2020') 
	GROUP BY ru.PROC_INST_ID_ 
~~~

