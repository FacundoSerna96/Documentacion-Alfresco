# Reportes

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
| Numero de documento Remitente  | INT  | |
| FechaCreacion        | DATE  | |

***

## Consulta SQL🔍

### Obtiene todos los campos sin filtro:
 
~~~sql
select ACT_RU_VARIABLE.PROC_INST_ID_ as 'ID',
    MAX(CASE WHEN NAME_ = 'numRadicado' THEN TEXT_ END) as 'Numero Radicado',
    MAX(CASE WHEN NAME_ = 'numDocRem_LABEL' THEN TEXT_ END) as 'Num Identificacion',
    MAX(CASE WHEN NAME_ = 'nomRemitente' THEN TEXT_ END) as 'Remitente',
    MAX(CASE WHEN NAME_ = 'nombreTramita' THEN TEXT_ END)as 'Destinatario',
    MAX(CASE WHEN NAME_ = 'tipoAsunto_LABEL' THEN TEXT_ END) as 'Tipo Asunto',
    MAX(CASE WHEN NAME_ = 'estado' THEN TEXT_ END) as 'Estado',
    MAX(CASE WHEN NAME_ = 'numDocRem_LABEL' THEN TEXT_ END) as 'Numero de documento Remitente',
    MAX(CASE WHEN NAME_ = 'fecRadicado' THEN TEXT_ END) as 'Fecha radicado'
	from activiti.ACT_RU_VARIABLE
	GROUP BY PROC_INST_ID_
~~~

_Tiempo de duración de la consulta:   363ms_

***

### Filtro por numero de radicado

~~~sql
select ACT_RU_VARIABLE.PROC_INST_ID_ as 'ID',
    MAX(CASE WHEN NAME_ = 'numRadicado' THEN TEXT_ END) as 'Numero Radicado',
    MAX(CASE WHEN NAME_ = 'numDocRem_LABEL' THEN TEXT_ END) as 'Num Identificacion',
    MAX(CASE WHEN NAME_ = 'nomRemitente' THEN TEXT_ END) as 'Remitente',
    MAX(CASE WHEN NAME_ = 'nombreTramita' THEN TEXT_ END)as 'Destinatario',
    MAX(CASE WHEN NAME_ = 'tipoAsunto_LABEL' THEN TEXT_ END) as 'Tipo Asunto',
    MAX(CASE WHEN NAME_ = 'estado' THEN TEXT_ END) as 'Estado',
    MAX(CASE WHEN NAME_ = 'numDocRem_LABEL' THEN TEXT_ END) as 'Numero de documento Remitente',
    MAX(CASE WHEN NAME_ = 'fecRadicado' THEN TEXT_ END) as 'Fecha radicado'
    from activiti.ACT_RU_VARIABLE
    where PROC_INST_ID_ in (
      select PROC_INST_ID_  from activiti.ACT_RU_VARIABLE
        where TEXT_ = "2214000043" and NAME_ = "numRadicado"
        )
    GROUP BY PROC_INST_ID_
~~~

_Tiempo de duración de la consulta:  706ms_


***

### Filtro por fecha desde-hasta

~~~sql
select ACT_RU_VARIABLE.PROC_INST_ID_ as 'ID',
    MAX(CASE WHEN NAME_ = 'numRadicado' THEN TEXT_ END) as 'radicado',
    MAX(CASE WHEN NAME_ = 'compania_LABEL' THEN TEXT_ END) as 'compañia',
    MAX(CASE WHEN NAME_ = 'tipoAsunto_LABEL' THEN TEXT_ END) as 'asunto', 
    MAX(CASE WHEN NAME_ = 'tramitador_LABEL' THEN TEXT_ END) as 'tramitador',
    MAX(CASE WHEN NAME_ = 'fecRadicado' THEN TEXT_ END) as 'fecha',
    MAX(CASE WHEN NAME_ = 'nombreRadicador' THEN TEXT_ END) as 'usuario creacion',
    MAX(CASE WHEN NAME_ = 'nombreTramita' THEN TEXT_ END) as 'asignado'
    from activiti.ACT_RU_VARIABLE
    where PROC_INST_ID_ in (
      select PROC_INST_ID_  from activiti.ACT_RU_VARIABLE
           where NAME_ = "fecRadicado" AND TEXT_ between '23-09-2020' AND '24-09-2020'
        )
    GROUP BY PROC_INST_ID_
~~~

_Tiempo de duración de la consulta:  937ms_

***

### Filtro por compania

~~~sql
select ACT_RU_VARIABLE.PROC_INST_ID_ as 'ID',
    MAX(CASE WHEN NAME_ = 'numRadicado' THEN TEXT_ END) as 'radicado',
    MAX(CASE WHEN NAME_ = 'compania_LABEL' THEN TEXT_ END) as 'compañia',
    MAX(CASE WHEN NAME_ = 'tipoAsunto_LABEL' THEN TEXT_ END) as 'asunto', 
    MAX(CASE WHEN NAME_ = 'tramitador_LABEL' THEN TEXT_ END) as 'tramitador',
    MAX(CASE WHEN NAME_ = 'fecRadicado' THEN TEXT_ END) as 'fecha',
    MAX(CASE WHEN NAME_ = 'nombreRadicador' THEN TEXT_ END) as 'usuario creacion',
    MAX(CASE WHEN NAME_ = 'nombreTramita' THEN TEXT_ END) as 'asignado'
    from activiti.ACT_RU_VARIABLE
    where PROC_INST_ID_ in (
      select PROC_INST_ID_  from activiti.ACT_RU_VARIABLE
        where 
          TEXT_ = "UNE EPM Telecomunicaciones S.A." and NAME_ = "compania_LABEL" 
        )
    GROUP BY PROC_INST_ID_
~~~

_Tiempo de duración de la consulta:  981ms_

***

### Con todos los filtros

~~~sql
select ACT_RU_VARIABLE.PROC_INST_ID_ as 'ID',
    MAX(CASE WHEN NAME_ = 'numRadicado' THEN TEXT_ END) as 'radicado',
    MAX(CASE WHEN NAME_ = 'compania_LABEL' THEN TEXT_ END) as 'compañia',
    MAX(CASE WHEN NAME_ = 'tipoAsunto_LABEL' THEN TEXT_ END) as 'asunto', 
    MAX(CASE WHEN NAME_ = 'tramitador_LABEL' THEN TEXT_ END) as 'tramitador',
    MAX(CASE WHEN NAME_ = 'fecRadicado' THEN TEXT_ END) as 'fecha',
    MAX(CASE WHEN NAME_ = 'nombreRadicador' THEN TEXT_ END) as 'usuario creacion',
    MAX(CASE WHEN NAME_ = 'nombreTramita' THEN TEXT_ END) as 'asignado'
	from activiti.ACT_RU_VARIABLE
	  where PROC_INST_ID_ in (
	    select PROC_INST_ID_  from activiti.ACT_RU_VARIABLE
		    where 
		TEXT_ = "2212000248" and NAME_ = "numRadicado" AND
			    TEXT_ = "UNE EPM Telecomunicaciones S.A." and NAME_ = "compania_LABEL" or
		NAME_ = "fecRadicado" AND TEXT_ between '23-09-2020' AND '24-09-2020'
	      )
    GROUP BY PROC_INST_ID_
~~~

_Tiempo de duración de la consulta:  928ms_


***

### Filtro por tipo de asunto

~~~sql
select ACT_RU_VARIABLE.PROC_INST_ID_ as 'ID',
    MAX(CASE WHEN NAME_ = 'numRadicado' THEN TEXT_ END) as 'radicado',
    MAX(CASE WHEN NAME_ = 'compania_LABEL' THEN TEXT_ END) as 'compañia',
    MAX(CASE WHEN NAME_ = 'tipoAsunto_LABEL' THEN TEXT_ END) as 'asunto', 
    MAX(CASE WHEN NAME_ = 'tramitador_LABEL' THEN TEXT_ END) as 'tramitador',
    MAX(CASE WHEN NAME_ = 'fecRadicado' THEN TEXT_ END) as 'fecha',
    MAX(CASE WHEN NAME_ = 'nombreRadicador' THEN TEXT_ END) as 'usuario creacion',
    MAX(CASE WHEN NAME_ = 'nombreTramita' THEN TEXT_ END) as 'asignado'
    from activiti.ACT_RU_VARIABLE
    where PROC_INST_ID_ in (
      select PROC_INST_ID_  from activiti.ACT_RU_VARIABLE
        where TEXT_ = "Solicitudes y peticiones generales PQR" and NAME_ = "tipoAsunto_LABEL" 
        )
    GROUP BY PROC_INST_ID_
~~~

_Tiempo de duración de la consulta:  913ms_


***

## Consultas para los componentes de reportes (PQR, Correspondencia General, Fraudes, Legal)

### Para PQR
~~~sql
select ACT_RU_VARIABLE.PROC_INST_ID_ as 'ID',
    MAX(CASE WHEN NAME_ = 'numRadicado' THEN TEXT_ END) as 'radicado',
    MAX(CASE WHEN NAME_ = 'compania_LABEL' THEN TEXT_ END) as 'compañia',
    MAX(CASE WHEN NAME_ = 'tipoAsunto_LABEL' THEN TEXT_ END) as 'asunto', 
    MAX(CASE WHEN NAME_ = 'tramitador_LABEL' THEN TEXT_ END) as 'tramitador',
    MAX(CASE WHEN NAME_ = 'fecRadicado' THEN TEXT_ END) as 'fecha',
    MAX(CASE WHEN NAME_ = 'nombreRadicador' THEN TEXT_ END) as 'usuario creacion',
    MAX(CASE WHEN NAME_ = 'nombreTramita' THEN TEXT_ END) as 'asignado'
    from activiti.ACT_RU_VARIABLE
    where PROC_INST_ID_ in (
      select PROC_INST_ID_  from activiti.ACT_RU_VARIABLE
        where TEXT_ = "Solicitudes y peticiones generales PQR" and NAME_ = "tipoAsunto_LABEL" 
        )
    GROUP BY PROC_INST_ID_
~~~

_Tiempo de duración de la consulta:  913ms_


### Para Correspondencia General y Facturas
~~~sql
select ACT_RU_VARIABLE.PROC_INST_ID_ as 'ID',
    MAX(CASE WHEN NAME_ = 'nomRemitente' THEN TEXT_ END) as 'Procedencia', 
    MAX(CASE WHEN NAME_ = 'numRadicado' THEN TEXT_ END) as 'radicado',
    MAX(CASE WHEN NAME_ = 'tipoAsunto_LABEL' THEN TEXT_ END) as 'asunto', 
    MAX(CASE WHEN NAME_ = 'fecRadicado' THEN TEXT_ END) as 'fecha',
    MAX(CASE WHEN NAME_ = 'tramitador_LABEL' THEN TEXT_ END) as 'tramitador'   
	from activiti.ACT_RU_VARIABLE
	  where PROC_INST_ID_ in (
	    select PROC_INST_ID_  from activiti.ACT_RU_VARIABLE
		    where TEXT_ = "Gestión de correspondencia general" OR 
			TEXT_ = "Facturas arrendamiento inmuebles" OR 
			TEXT_ = "Facturas impuesto predial" OR 
			TEXT_ = "Facturas arrendamiento antenas" OR 
			TEXT_ = "Facturas título valor" OR 
			TEXT_ = "Gestión Pagos servicios Públicos" OR 
			TEXT_ = "Facturas / Cuentas de cobro proveedores" OR 
			TEXT_ = "Facturas servicios públicos" OR 
			TEXT_ = "Facturas impuestos generales" and NAME_ = "tipoAsunto_LABEL" 
	      )
    GROUP BY PROC_INST_ID_
~~~

_Tiempo de duración de la consulta:  1.122s_


### Para Fraudes
~~~sql
select ACT_RU_VARIABLE.PROC_INST_ID_ as 'ID',
    MAX(CASE WHEN NAME_ = 'nomRemitente' THEN TEXT_ END) as 'Procedencia', 
    MAX(CASE WHEN NAME_ = 'numRadicado' THEN TEXT_ END) as 'radicado',
    MAX(CASE WHEN NAME_ = 'tipoAsunto_LABEL' THEN TEXT_ END) as 'asunto', 
    MAX(CASE WHEN NAME_ = 'fecRadicado' THEN TEXT_ END) as 'fecha',
    MAX(CASE WHEN NAME_ = 'tramitador_LABEL' THEN TEXT_ END) as 'tramitador'   
	from activiti.ACT_RU_VARIABLE
	  where PROC_INST_ID_ in (
	    select PROC_INST_ID_  from activiti.ACT_RU_VARIABLE
		    where TEXT_ = "Gestión requerimientos judiciales" and NAME_ = "tipoAsunto_LABEL" 
	      )
    GROUP BY PROC_INST_ID_
~~~

_Tiempo de duración de la consulta:  709ms_


### Para Legal
~~~sql
select ACT_RU_VARIABLE.PROC_INST_ID_ as 'ID',    
    MAX(CASE WHEN NAME_ = 'nomRemitente' THEN TEXT_ END) as 'Procedencia', 
    MAX(CASE WHEN NAME_ = 'numRadicado' THEN TEXT_ END) as 'radicado',
    MAX(CASE WHEN NAME_ = 'tipoAsunto_LABEL' THEN TEXT_ END) as 'asunto', 
    MAX(CASE WHEN NAME_ = 'fecRadicado' THEN TEXT_ END) as 'fecha',
    MAX(CASE WHEN NAME_ = 'tramitador_LABEL' THEN TEXT_ END) as 'tramitador'   
	from activiti.ACT_RU_VARIABLE
	  where PROC_INST_ID_ in (
	    select PROC_INST_ID_  from activiti.ACT_RU_VARIABLE
		    where TEXT_ = "Demandas" OR TEXT_ = "Tutelas" OR TEXT_ = "Requerimientos Legales" and NAME_ = "tipoAsunto_LABEL" 
      )
    GROUP BY PROC_INST_ID_
~~~

_Tiempo de duración de la consulta:  2.459s_








