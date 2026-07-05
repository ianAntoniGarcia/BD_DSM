## Diccionario de Datos de la base de datos de control escolar 
# 1. Informacion General 

# Diccionario de Datos de la base de datos de control escolar 

## 1. Informacion General 

| ELEMENTO | VALOR |
| :--- | :--- |
| Proyecto | Control Escolar |
| Version | 1.0 |
| Fecha | Junio 2026 |
| Elaboro | Angel Santiago Jimenez Sarabia | 
| SGBD | SQLServer |   

## 2. Descripcion del sistema de Base de Datos 

El sistema administra:

    - Carreras
    - Alumnos 
    - Profesores
    - Materias 
    - Grupos 
    - Inscripciones

Permite controlar la Oferta académica y la Inscripción de estudiantes.

## 3. Catalogo de restricciones utilizadas

| CODIGO | SIGNIFICADO |
| :--- | :--- |
| PK | Primary Key |
| FK | Foreign Key |
| NN | NOT NULL |
| UQ | Unique |
| AI | Auto Increment |
| CK | Check |
| DF | Default |


## 4. Diccionario de Datos 

### Tabla: Carrera 

Almacena las carreras ofertadas en la institución.

| CAMPO | TIPO | LONGITUD | RESTRICCIONES | DESCRIPCION |
| :--- | :--- | :--- | :--- | :--- |
| id_carrera | INT | - | PK, AI, NN | Identificador único de la carrera |
| nombre_carrera | VARCHAR | 100 | NN, UQ | Nombre oficial de la carrera |

### Tabla: Alumno 

Almacena la información de los alumnos inscritos.

| CAMPO | TIPO | LONGITUD | RESTRICCIONES | DESCRIPCION |
| :--- | :--- | :--- | :--- | :--- |
| id_Alumno | INT | - | PK, AI, NN | Identificador único del alumno |
| Matricula | VARCHAR | 10 | UQ, NN | Matrícula institucional |
| nombre | VARCHAR | 30 | NN | Nombre del alumno |
| apellido_paterno | VARCHAR | 50 | NN | Apellido paterno |
| apellido_Materno | VARCHAR | 50 | NN | Apellido materno |
| Correo | VARCHAR | 100 | NN | Correo institucional |
| Fecha_Nacimiento | DATE | - | NN | Fecha de nacimiento |
| id_carrera | INT | - | FK, NN | Carrera a la que pertenece |

### Tabla: Profesor 

Almacena los datos del personal docente.

| CAMPO | TIPO | LONGITUD | RESTRICCIONES | DESCRIPCION |
| :--- | :--- | :--- | :--- | :--- |
| id_profesor | INT | - | PK, AI, NN | Identificador único del profesor |
| numero_empleado | VARCHAR | 10 | UQ, NN | Número de empleado docente |
| nombre | VARCHAR | 30 | NN | Nombre del profesor |
| apellido_paterno | VARCHAR | 50 | NN | Apellido paterno |
| apellido_materno | VARCHAR | 50 | NN | Apellido materno |
| correo | VARCHAR | 100 | NN | Correo institucional |

### Tabla: Materia 

Almacena las materias que forman parte de los planes de estudio.

| CAMPO | TIPO | LONGITUD | RESTRICCIONES | DESCRIPCION |
| :--- | :--- | :--- | :--- | :--- |
| id_materia | INT | - | PK, AI, NN | Identificador único de la materia |
| clave_materia | VARCHAR | 10 | UQ, NN | Clave oficial de la materia |
| nombre_materia | VARCHAR | 100 | NN | Nombre de la asignatura |
| id_carrera | INT | - | FK, NN | Carrera a la que pertenece la materia |

### Tabla: Grupo 
 
Almacena los grupos abiertos para impartir clases en un periodo académico.

| CAMPO | TIPO | LONGITUD | RESTRICCIONES | DESCRIPCION |
| :--- | :--- | :--- | :--- | :--- |
| id_grupo | INT | - | PK, AI, NN | Identificador único del grupo |
| codigo_grupo | VARCHAR | 10 | UQ, NN | Código del grupo (ej. 401-A) |
| id_materia | INT | - | FK, NN | Materia que se imparte en el grupo |
| id_profesor | INT | - | FK, NN | Profesor asignado al grupo |

### Tabla: Inscripcion 
 
Registra la inscripción de los alumnos en sus respectivos grupos y sus calificaciones.

| CAMPO | TIPO | LONGITUD | RESTRICCIONES | DESCRIPCION |
| :--- | :--- | :--- | :--- | :--- |
| id_inscripcion | INT | - | PK, AI, NN | Identificador único de la inscripción |
| id_alumno | INT | - | FK, NN | Alumno inscrito |
| id_grupo | INT | - | FK, NN | Grupo en el que se inscribe |
| calificacion | DECIMAL | 4,2 | CK | Calificación final obtenida |

## 5. Relaciones en la Base de Datos

| Relacion | Cardinalidad | Descripcion |
| :--- | :--- | :--- |
| Carrera --> Alumno | 1:N | Una carrera tiene muchos alumnos |
| Carrera --> Materia | 1:N | Una carrera tiene muchas materias |
| Profesor --> Grupo | 1:N | Un profesor puede impartir varios grupos |
| Materia --> Grupo | 1:N | Una materia puede abrirse en varios grupos |
| Alumno --> Inscripcion | 1:N | Un alumno puede tener varias inscripciones |
| Grupo --> Inscripcion | 1:N | Un grupo puede tener muchos alumnos inscritos |

## 6. Llaves Foráneas (FK)

| Tabla | Campo FK | Referencia |
| :--- | :--- | :--- |
| Alumno | id_carrera | Carrera (id_carrera) |
| Materia | id_carrera | Carrera (id_carrera) |
| Grupo | id_materia | Materia (id_materia) |
| Grupo | id_profesor | Profesor (id_profesor) |
| Inscripcion | id_alumno | Alumno (id_Alumno) |
| Inscripcion | id_grupo | Grupo (id_grupo) |


## 7. Integridad Referencial

| Reglas | Descripcion |
| :--- | :--- |
| IR-01 | No se puede registrar un alumno con una carrera inexistente. |
| IR-02 | No se puede crear un grupo para una materia inexistente. |
| IR-03 | No se puede crear un grupo para un profesor inexistente. |
| IR-04 | No se puede inscribir un alumno en un grupo inexistente. |
| IR-05 | No se puede eliminar una carrera que tenga alumnos asociados sin antes reasignarlos o eliminarlos. |

## 8. Reglas de Negocio

| Codigo | Regla |
| :--- | :--- |
| RN-01 | Un alumno pertenece a una sola carrera. |
| RN-02 | Una carrera puede tener muchos alumnos. |
| RN-03 | Una carrera puede tener muchas Materias. |
| RN-04 | Un profesor puede impartir varios grupos. |
| RN-05 | Un grupo solo puede tener un profesor asignado. |
| RN-06 | La calificación debe estar configurada numéricamente entre 0.0 y 10.0. |

## 9. Diagrama Relacional

 ![ Ejercicio 1](/img/E-R/ejercicio1.1.png)

# EJECICIO 2

## Diccionario de Datos de la base de datos de control escolar (Profesores, Cursos y Especialidades)

## 1. Informacion General 

| ELEMENTO | VALOR |
| :--- | :--- |
| Proyecto | Control Escolar - Cursos y Especialidades |
| Version | 1.0 |
| Fecha | Junio 2026 |
| Elaboro | Angel Santiago Jimenez Sarabia | 
| SGBD | SQLServer |   

## 2. Descripcion del sistema de Base de Datos 

El sistema administra:

    - Profesores
    - Cursos
    - Especialidades

Permite controlar la asignación de cursos a los profesores y el registro de sus especialidades correspondientes.

## 3. Catalogo de restricciones utilizadas

| CODIGO | SIGNIFICADO |
| :--- | :--- |
| PK | Primary Key |
| FK | Foreign Key |
| NN | NOT NULL |
| UQ | Unique |
| AI | Auto Increment |
| CK | Check |
| DF | Default |

## 4. Diccionario de Datos 

### Tabla: Profesor (Table)

Almacena los datos del personal docente de la institución.

| CAMPO | TIPO | LONGITUD | RESTRICCIONES | DESCRIPCION |
| :--- | :--- | :--- | :--- | :--- |
| IDprofesor | INT | - | PK, AI, NN | Identificador único del profesor |
| nombre | VARCHAR | 50 | NN | Nombre(s) del profesor |
| apellido1 | VARCHAR | 50 | NN | Primer apellido |
| apellido2 | VARCHAR | 50 | - | Segundo apellido (opcional) |

### Tabla: Curso

Almacena la información de los cursos ofertados y el profesor asignado a impartirlos.

| CAMPO | TIPO | LONGITUD | RESTRICCIONES | DESCRIPCION |
| :--- | :--- | :--- | :--- | :--- |
| NumCurso | INT | - | PK, AI, NN | Número identificador del curso |
| Nombre | VARCHAR | 100 | NN | Nombre del curso / asignatura |
| Cresitos | INT | - | NN | Créditos académicos del curso (Nota: Campo "Cresitos" en diagrama) |
| IDProfesor | INT | - | FK, NN | Identificador del profesor que imparte el curso |

### Tabla: Especialidad

Almacena las diferentes especialidades técnicas o profesionales asociadas a los profesores.

| CAMPO | TIPO | LONGITUD | RESTRICCIONES | DESCRIPCION |
| :--- | :--- | :--- | :--- | :--- |
| IDespecialidad | INT | - | PK, AI, NN | Identificador único de la especialidad |
| nombre | VARCHAR | 100 | NN | Nombre de la especialidad académica |
| IDProfesor | INT | - | FK, NN | Identificador del profesor que posee esta especialidad |

## 5. Relaciones en la Base de Datos

| Relacion | Cardinalidad | Descripcion |
| :--- | :--- | :--- |
| Profesor --> Curso | 1:N | Un profesor puede impartir varios cursos |
| Profesor --> Especialidad | 1:N | Un profesor puede tener muchas especialidades |

## 6. Llaves Foráneas (FK)

| Tabla | Campo FK | Referencia |
| :--- | :--- | :--- |
| Curso | IDProfesor | Profesor (IDprofesor) |
| Especialidad | IDProfesor | Profesor (IDprofesor) |

## 7. Integridad Referencial

| Reglas | Descripcion |
| :--- | :--- |
| IR-01 | No se puede asignar un curso a un profesor que no exista en el sistema. |
| IR-02 | No se puede registrar una especialidad ligada a un ID de profesor inexistente. |
| IR-03 | Si se elimina un profesor, se deben reasignar o eliminar sus cursos y especialidades dependientes. |

## 8. Reglas de Negocio

| Codigo | Regla |
| :--- | :--- |
| RN-01 | Cada curso debe poseer obligatoriamente un profesor asignado para su apertura. |
| RN-02 | Los créditos ("Cresitos") de un curso deben ser un valor entero mayor a cero. |
| RN-03 | Un profesor puede estar registrado sin tener un curso o especialidad asignada inmediatamente. |

## 9. Diagrama Relacional

 ![ Ejercicio 2](/img/E-R/ejercicio2.2.png)

 # EJERCICIO 3
 ## Diccionario de Datos de la base de datos de control escolar (Profesores, Cursos y Especialidades)

## 1. Informacion General 

| ELEMENTO | VALOR |
| :--- | :--- |
| Proyecto | Control Escolar - Cursos y Especialidades |
| Version | 1.0 |
| Fecha | Junio 2026 |
| Elaboro | Angel Santiago Jimenez Sarabia | 
| SGBD | SQLServer |   

## 2. Descripcion del sistema de Base de Datos 

El sistema administra:

    - Profesores
    - Cursos
    - Especialidades

Permite controlar la asignación de cursos a los profesores y el registro de sus especialidades correspondientes.

## 3. Catalogo de restricciones utilizadas

| CODIGO | SIGNIFICADO |
| :--- | :--- |
| PK | Primary Key |
| FK | Foreign Key |
| NN | NOT NULL |
| UQ | Unique |
| AI | Auto Increment |
| CK | Check |
| DF | Default |

## 4. Diccionario de Datos 

### Tabla: Profesor (Table)
 
Almacena los datos del personal docente de la institución.

| CAMPO | TIPO | LONGITUD | RESTRICCIONES | DESCRIPCION |
| :--- | :--- | :--- | :--- | :--- |
| IDprofesor | INT | - | PK, AI, NN | Identificador único del profesor |
| nombre | VARCHAR | 50 | NN | Nombre(s) del profesor |
| apellido1 | VARCHAR | 50 | NN | Primer apellido |
| apellido2 | VARCHAR | 50 | - | Segundo apellido (opcional) |

### Tabla: Curso
 
Almacena la información de los cursos ofertados y el profesor asignado a impartirlos.

| CAMPO | TIPO | LONGITUD | RESTRICCIONES | DESCRIPCION |
| :--- | :--- | :--- | :--- | :--- |
| NumCurso | INT | - | PK, AI, NN | Número identificador del curso |
| Nombre | VARCHAR | 100 | NN | Nombre del curso / asignatura |
| Cresitos | INT | - | NN | Créditos académicos del curso (Nota: Campo "Cresitos" en diagrama) |
| IDProfesor | INT | - | FK, NN | Identificador del profesor que imparte el curso |

### Tabla: Especialidad

Almacena las diferentes especialidades técnicas o profesionales asociadas a los profesores.

| CAMPO | TIPO | LONGITUD | RESTRICCIONES | DESCRIPCION |
| :--- | :--- | :--- | :--- | :--- |
| IDespecialidad | INT | - | PK, AI, NN | Identificador único de la especialidad |
| nombre | VARCHAR | 100 | NN | Nombre de la especialidad académica |
| IDProfesor | INT | - | FK, NN | Identificador del profesor que posee esta especialidad |

## 5. Relaciones en la Base de Datos

| Relacion | Cardinalidad | Descripcion |
| :--- | :--- | :--- |
| Profesor --> Curso | 1:N | Un profesor puede impartir varios cursos |
| Profesor --> Especialidad | 1:N | Un profesor puede tener muchas especialidades |

## 6. Llaves Foráneas (FK)

| Tabla | Campo FK | Referencia |
| :--- | :--- | :--- |
| Curso | IDProfesor | Profesor (IDprofesor) |
| Especialidad | IDProfesor | Profesor (IDprofesor) |

## 7. Integridad Referencial

| Reglas | Descripcion |
| :--- | :--- |
| IR-01 | No se puede asignar un curso a un profesor que no exista en el sistema. |
| IR-02 | No se puede registrar una especialidad ligada a un ID de profesor inexistente. |
| IR-03 | Si se elimina un profesor, se deben reasignar o eliminar sus cursos y especialidades dependientes. |

## 8. Reglas de Negocio

| Codigo | Regla |
| :--- | :--- |
| RN-01 | Cada curso debe poseer obligatoriamente un profesor asignado para su apertura. |
| RN-02 | Los créditos ("Cresitos") de un curso deben ser un valor entero mayor a cero. |
| RN-03 | Un profesor puede estar registrado sin tener un curso o especialidad asignada inmediatamente. |

## 9. Diagrama Relacional
 ![ Ejercicio 3](/img/E-R/ejercicio3.3.png)


 # EJERCICIO 4


## Diccionario de Datos de la base de datos de control de pedidos y productos

## 1. Informacion General 

| ELEMENTO | VALOR |
| :--- | :--- |
| Proyecto | Control de Pedidos y Productos |
| Version | 1.0 |
| Fecha | Junio 2026 |
| Elaboro | Angel Santiago Jimenez Sarabia | 
| SGBD | SQLServer |   

## 2. Descripcion del sistema de Base de Datos 

El sistema administra:

    - Clientes
    - Pedidos
    - Productos
    - Detalle de elementos por pedido (Tiene)

Permite controlar la gestión de compras corporativas de los clientes, registrando el historial temporal de cada pedido (fecha, hora, mes, año) y el desglose de productos incluidos con sus cantidades y precios específicos.

## 3. Catalogo de restricciones utilizadas

| CODIGO | SIGNIFICADO |
| :--- | :--- |
| PK | Primary Key |
| FK | Foreign Key |
| NN | NOT NULL |
| UQ | Unique |
| AI | Auto Increment |
| CK | Check |
| DF | Default |

## 4. Diccionario de Datos 

### Tabla: CLIENTE

Almacena el registro de las empresas clientes de la organización.

| CAMPO | TIPO | LONGITUD | RESTRICCIONES | DESCRIPCION |
| :--- | :--- | :--- | :--- | :--- |
| IdCliente | INT | - | PK, AI, NN | Identificador único del cliente |
| Empresa | VARCHAR | 150 | NN | Nombre comercial o razón social de la empresa |
| RFC | VARCHAR | 13 | NN, UQ | Registro Federal de Contribuyentes de la empresa |
| NoPedidos | INT | - | FK, - | Relación foránea de referencia con el pedido |

### Tabla: PEDIDOS
 
Almacena la cabecera y metadatos temporales de las órdenes de compra solicitadas.

| CAMPO | TIPO | LONGITUD | RESTRICCIONES | DESCRIPCION |
| :--- | :--- | :--- | :--- | :--- |
| NumPedidos | INT | - | PK, AI, NN | Número identificador único del pedido |
| IdCliente | INT | - | FK, NN | Identificador del cliente que realizó el pedido |
| Fecha | DATE | - | NN | Fecha de emisión de la orden |
| Hora | TIME | - | NN | Hora exacta de registro del pedido |
| Mes | INT | - | NN | Mes calendario de procesamiento (1-12) |
| Año | INT | - | NN | Año de procesamiento del pedido |

### Tabla: PRODUCTO

Almacena el catálogo de productos disponibles para la venta.

| CAMPO | TIPO | LONGITUD | RESTRICCIONES | DESCRIPCION |
| :--- | :--- | :--- | :--- | :--- |
| IDPedidos | INT | - | PK, AI, NN | Identificador único del producto (Nota: Etiquetado como IDPedidos en diagrama) |
| Precio | DECIMAL | 10,2 | NN | Precio base o de lista del producto |
| Nombre | VARCHAR | 100 | NN | Nombre comercial del producto |
| NoPedidos | INT | - | FK, - | Llave foránea de referencia hacia la orden |

### Tabla: TIENE
 
Tabla intermedia que detalla el desglose y la cantidad de productos incluidos dentro de cada pedido.

| CAMPO | TIPO | LONGITUD | RESTRICCIONES | DESCRIPCION |
| :--- | :--- | :--- | :--- | :--- |
| IdCliente | INT | - | FK, NN | Relación foránea de referencia del cliente |
| Cantidad | INT | - | NN | Cantidad de unidades solicitadas de este producto |
| Precio | DECIMAL | 10,2 | NN | Precio unitario aplicado en la transacción del producto |
| NoPedidos | INT | - | FK, NN | Relación foránea de referencia con el número de pedido |

## 5. Relaciones en la Base de Datos

| Relacion | Cardinalidad | Descripcion |
| :--- | :--- | :--- |
| CLIENTE --> PEDIDOS | 1:N | Un cliente puede generar múltiples pedidos en el sistema |
| PEDIDOS --> TIENE | 1:N | Un pedido contiene una o muchas filas de productos |
| PRODUCTO --> TIENE | 1:N | Un producto puede estar presente en múltiples listas de pedidos |

## 6. Llaves Foráneas (FK)

| Tabla | Campo FK | Referencia |
| :--- | :--- | :--- |
| PEDIDOS | IdCliente | CLIENTE (IdCliente) |
| CLIENTE | NoPedidos | PEDIDOS (NumPedidos) |
| PRODUCTO | NoPedidos | PEDIDOS (NumPedidos) |
| TIENE | IdCliente | CLIENTE (IdCliente) |
| TIENE | NoPedidos | PEDIDOS (NumPedidos) |

## 7. Integridad Referencial

| Reglas | Descripcion |
| :--- | :--- |
| IR-01 | No se puede registrar un pedido en `PEDIDOS` con un `IdCliente` que no exista en la tabla `CLIENTE`. |
| IR-02 | No se pueden añadir desgloses en la tabla `TIENE` vinculados a un `NumPedidos` inexistente. |
| IR-03 | Cualquier modificación o eliminación de un elemento principal (Cliente o Pedido) activará restricciones en cascada para evitar registros huérfanos en `TIENE`. |

## 8. Reglas de Negocio

| Codigo | Regla |
| :--- | :--- |
| RN-01 | El campo `RFC` en `CLIENTE` debe cumplir con la estructura de longitud y validación alfanumérica estándar de personas morales. |
| RN-02 | El campo `Mes` en la tabla `PEDIDOS` solo acepta valores enteros dentro del rango del 1 al 12 mediante una restricción CK. |
| RN-03 | Los campos de `Precio` y `Cantidad` en las tablas `PRODUCTO` y `TIENE` deben ser estrictamente superiores a cero. |
## 9. Diagrama Relacional
 ![ Ejercicio 4](/img/E-R/ejercicio4.4.png)


 # EJERCICIO 5

## Diccionario de Datos de la base de datos de gestión de empleados y departamentos

## 1. Informacion General 

| ELEMENTO | VALOR |
| :--- | :--- |
| Proyecto | Control de Empleados, Departamentos y Proyectos |
| Version | 1.0 |
| Fecha | Junio 2026 |
| Elaboro | Angel Santiago Jimenez Sarabia | 
| SGBD | SQLServer |   

## 2. Descripcion del sistema de Base de Datos 

El sistema administra:

    - Empleados 
    - Departamentos y sus ubicaciones (Locations)
    - Proyectos asignados a los departamentos
    - Control de horas trabajadas por proyecto (Works On)
    - Dependientes o familiares de los empleados

Permite controlar la estructura interna de una empresa, los gerentes a cargo de cada departamento, las horas invertidas por los empleados en proyectos específicos y el registro de beneficiarios directos (dependientes) para fines de prestaciones.

## 3. Catalogo de restricciones utilizadas

| CODIGO | SIGNIFICADO |
| :--- | :--- |
| PK | Primary Key |
| FK | Foreign Key |
| NN | NOT NULL |
| UQ | Unique |
| AI | Auto Increment |
| CK | Check |
| DF | Default |

## 4. Diccionario de Datos 

### Tabla: EMPLOYE

Almacena el registro del personal de la empresa, incluyendo su información básica y su relación de subordinación o jefatura.

| CAMPO | TIPO | LONGITUD | RESTRICCIONES | DESCRIPCION |
| :--- | :--- | :--- | :--- | :--- |
| IDEmploye | INT | - | PK, AI, NN | Identificador único del empleado |
| FirstName | VARCHAR | 50 | NN | Nombre(s) del empleado |
| SNN | VARCHAR | 11 | NN, UQ | Número de Seguro Social o identificador fiscal |
| addres | VARCHAR | 200 | - | Dirección residencial del empleado |
| Salary | DECIMAL | 10,2 | - | Sueldo o salario asignado |
| Serv | VARCHAR | 50 | - | Área de servicio o puesto específico |
| Birthday | DATE | - | NN | Fecha de nacimiento |
| NumDepartament | INT | - | FK, NN | Departamento al que pertenece el empleado |
| Jef | INT | - | FK, - | Identificador del jefe directo (Autorelación/Relación reflexiva) |

### Tabla: Departament

Almacena los departamentos operativos o administrativos que constituyen la empresa.

| CAMPO | TIPO | LONGITUD | RESTRICCIONES | DESCRIPCION |
| :--- | :--- | :--- | :--- | :--- |
| numDep | INT | - | PK, AI, NN | Número identificador único del departamento |
| manager | INT | - | FK, NN, UQ | Identificador del empleado que ejerce como gerente |
| StardDate | DATE | - | NN | Fecha de asignación o inicio del gerente en el cargo |
| nombre | VARCHAR | 100 | NN, UQ | Nombre oficial del departamento |

### Tabla: Lcations

Almacena las diferentes sedes, regiones o ubicaciones geográficas asignadas a los departamentos.

| CAMPO | TIPO | LONGITUD | RESTRICCIONES | DESCRIPCION |
| :--- | :--- | :--- | :--- | :--- |
| NumDep | INT | - | PK, FK, NN | Número del departamento vinculado a la ubicación |
| NameLocations | VARCHAR | 100 | NN | Nombre de la ubicación o sucursal |
| numLocations | INT | - | - | Código numérico o identificador de la zona |

### Tabla: Proyects

Almacena los proyectos de desarrollo o investigación gestionados por los departamentos.

| CAMPO | TIPO | LONGITUD | RESTRICCIONES | DESCRIPCION |
| :--- | :--- | :--- | :--- | :--- |
| NumberProyects | INT | - | PK, AI, NN | Número identificador único del proyecto |
| NameProyects | VARCHAR | 100 | NN | Nombre comercial o técnico del proyecto |
| Locations | VARCHAR | 100 | - | Ubicación o sede donde se desarrolla el proyecto |
| NumberDep | INT | - | FK, NN | Departamento responsable de la ejecución del proyecto |

### Tabla: WORKS_ON
 
Tabla intermedia que desglosa la asignación de los empleados a los proyectos y controla el tiempo invertido en cada uno.

| CAMPO | TIPO | LONGITUD | RESTRICCIONES | DESCRIPCION |
| :--- | :--- | :--- | :--- | :--- |
| EmployedID | INT | - | PK, FK, NN | Identificador del empleado asignado |
| NumberProyecto | INT | - | PK, FK, NN | Identificador del proyecto en desarrollo |
| hours | DECIMAL | 5,2 | - | Cantidad de horas acumuladas de trabajo |

### Tabla: Dependiente
 
Almacena el registro de los familiares directos de los empleados para control de seguros o prestaciones.

| CAMPO | TIPO | LONGITUD | RESTRICCIONES | DESCRIPCION |
| :--- | :--- | :--- | :--- | :--- |
| DependientiID | INT | - | PK, AI, NN | Identificador único del dependiente |
| Employe | INT | - | FK, NN | Identificador del empleado del cual depende |
| sex | CHAR | 1 | CK | Género o sexo del dependiente (M/F) |
| Birthday | DATE | - | NN | Fecha de nacimiento del dependiente |
| RelationShip | VARCHAR | 50 | NN | Parentesco con el empleado (ej. Hijo, Cónyuge) |
| Name | VARCHAR | 100 | NN | Nombre completo del dependiente |

## 5. Relaciones en la Base de Datos

| Relacion | Cardinalidad | Descripcion |
| :--- | :--- | :--- |
| EMPLOYE --> EMPLOYE | 1:N | Un empleado puede ser jefe directo de muchos otros empleados |
| Departament --> EMPLOYE | 1:N | Un departamento agrupa a muchos empleados |
| EMPLOYE --> Departament | 1:1 | Un empleado puede ser gerente de un único departamento |
| Departament --> Lcations | 1:N | Un departamento puede operar en múltiples ubicaciones |
| Departament --> Proyects | 1:N | Un departamento puede tener a su cargo varios proyectos |
| EMPLOYE --> WORKS_ON | 1:N | Un empleado puede estar asignado a varios proyectos mediante horas |
| Proyects --> WORKS_ON | 1:N | Un proyecto puede contar con la participación de varios empleados |
| EMPLOYE --> Dependiente | 1:N | Un empleado puede tener registrados múltiples dependientes familiares |

## 6. Llaves Foráneas (FK)

| Tabla | Campo FK | Referencia |
| :--- | :--- | :--- |
| EMPLOYE | NumDepartament | Departament (numDep) |
| EMPLOYE | Jef | EMPLOYE (IDEmploye) |
| Departament | manager | EMPLOYE (IDEmploye) |
| Lcations | NumDep | Departament (numDep) |
| Proyects | NumberDep | Departament (numDep) |
| WORKS_ON | EmployedID | EMPLOYE (IDEmploye) |
| WORKS_ON | NumberProyect | Proyects (NumberProyects) |
| Dependiente | Employe | EMPLOYE (IDEmploye) |

## 7. Integridad Referencial

| Reglas | Descripcion |
| :--- | :--- |
| IR-01 | No se puede asignar un jefe en el campo `Jef` si este no existe previamente como un registro válido en `EMPLOYE`. |
| IR-02 | El `manager` de un departamento debe apuntar forzosamente a un `IDEmploye` activo. |
| IR-03 | Si se elimina un registro de la tabla `EMPLOYE`, se deben eliminar en cascada sus dependientes asociados en la tabla `Dependiente` y sus registros de horas en `WORKS_ON`. |
| IR-04 | No se puede registrar una ubicación en `Lcations` para un número de departamento inexistente. |

## 8. Reglas de Negocio

| Codigo | Regla |
| :--- | :--- |
| RN-01 | La combinación de `EmployedID` y `NumberProyect` en `WORKS_ON` debe ser única para evitar duplicidades en el cómputo del mismo proyecto. |
| RN-02 | El campo `sex` en la tabla `Dependiente` está restringido mediante un CK a caracteres específicos correspondientes al género. |
| RN-03 | El campo `Salary` de la tabla `EMPLOYE` debe ser configurado con valores monetarios estrictamente positivos. |
| RN-04 | La fecha de asignación de gerencia `StardDate` no puede ser menor a la fecha de creación del departamento. |

## 9. Diagrama Relacional
 ![ Ejercicio 5](/img/E-R/ejercicio5.5.png)


 ## EJERCICIO 6

# Diccionario de Datos de la base de datos de control escolar integral

## 1. Informacion General 

| ELEMENTO | VALOR |
| :--- | :--- |
| Proyecto | Sistema Integral de Control Escolar, Profesores y Proyectos |
| Version | 1.0 |
| Fecha | Junio 2026 |
| Elaboro | Angel Santiago Jimenez Sarabia | 
| SGBD | SQLServer |   

## 2. Descripcion del sistema de Base de Datos 

El sistema administra:

    - Alumnos, sus credenciales y sus números telefónicos de contacto.
    - Control de materias cursadas por los alumnos (Cursa) con sus calificaciones finales.
    - Profesores con adscripción a departamentos específicos y sus dependientes familiares.
    - Participación de profesores en proyectos institucionales (Participa) bajo roles definidos.

Permite controlar la gestión del ciclo escolar completo, el historial de inscripciones y calificaciones de asignaturas, la estructura administrativa de profesores adscritos a edificios/departamentos y la asignación laboral a proyectos con presupuesto específico.

## 3. Catalogo de restricciones utilizadas

| CODIGO | SIGNIFICADO |
| :--- | :--- |
| PK | Primary Key |
| FK | Foreign Key |
| NN | NOT NULL |
| UQ | Unique |
| AI | Auto Increment |
| CK | Check |
| DF | Default |

## 4. Diccionario de Datos 

### Tabla: Alumno
 
Almacena el registro principal y los datos personales de los estudiantes de la institución.

| CAMPO | TIPO | LONGITUD | RESTRICCIONES | DESCRIPCION |
| :--- | :--- | :--- | :--- | :--- |
| Matricula | VARCHAR | 20 | PK, NN | Matrícula única institucional del alumno |
| Nombre | VARCHAR | 50 | NN | Nombre(s) del alumno |
| apellido1 | VARCHAR | 50 | NN | Primer apellido |
| apellido2 | VARCHAR | 50 | - | Segundo apellido (opcional) |
| correo | VARCHAR | 100 | NN, UQ | Correo electrónico de contacto |
| fechaNaci | DATE | - | NN | Fecha de nacimiento |

### Tabla: Telefono

Almacena los números telefónicos asociados a las matrículas de los alumnos.

| CAMPO | TIPO | LONGITUD | RESTRICCIONES | DESCRIPCION |
| :--- | :--- | :--- | :--- | :--- |
| TelefonoID | VARCHAR | 15 | PK, FK, NN | Número telefónico / Identificador de línea |
| Matricula | VARCHAR | 20 | PK, FK, NN | Matrícula del alumno al que pertenece el teléfono |
| numeroTotal | INT | - | - | Total o contador de teléfonos registrados (Opcional) |

### Tabla: Credencial

Almacena los datos de la credencial de identificación física asignada a cada alumno.

| CAMPO | TIPO | LONGITUD | RESTRIPCIONES | DESCRIPCION |
| :--- | :--- | :--- | :--- | :--- |
| Numcredencial | VARCHAR | 20 | PK, NN | Número de serie único de la credencial |
| FechaInscripcion | DATE | - | NN, DF | Fecha de expedición o inscripción inicial |
| Vigencia | DATE | - | NN | Fecha de expiración del documento |
| Matricula | VARCHAR | 20 | FK, NN, UQ | Matrícula del alumno titular de la credencial |

### Tabla: Cursa

Tabla intermedia que rompe la relación N:M entre alumnos y materias, registrando las asignaturas tomadas y sus notas.

| CAMPO | TIPO | LONGITUD | RESTRICCIONES | DESCRIPCION |
| :--- | :--- | :--- | :--- | :--- |
| Matricula | VARCHAR | 20 | PK, FK, NN | Matrícula del alumno |
| ClaveMateria | VARCHAR | 10 | PK, FK, NN | Clave de la materia cursada |
| Transcripcion | VARCHAR | 250 | - | Notas adicionales, observaciones o minuta del curso |
| CalificacionFinal | DECIMAL | 4,2 | CK | Calificación definitiva obtenida en la asignatura |

### Tabla: Materia
 
Almacena las materias académicas que componen la oferta institucional.

| CAMPO | TIPO | LONGITUD | RESTRICCIONES | DESCRIPCION |
| :--- | :--- | :--- | :--- | :--- |
| ClaveMateria | VARCHAR | 10 | PK, NN | Código alfanumérico identificador de la materia |
| NombreMateria | VARCHAR | 100 | NN | Nombre de la asignatura |
| Creditos | INT | - | NN | Valor en créditos académicos |
| numProf | INT | - | FK, NN | Profesor titular asignado de manera global |

### Tabla: Profesor
 
Almacena el registro laboral del personal docente de la institución.

| CAMPO | TIPO | LONGITUD | RESTRICCIONES | DESCRIPCION |
| :--- | :--- | :--- | :--- | :--- |
| Numprofe | INT | - | PK, AI, NN | Número identificador del profesor |
| nombre | VARCHAR | 30 | NN | Nombre(s) del profesor |
| apellido1 | VARCHAR | 50 | NN | Primer apellido |
| apellido2 | VARCHAR | 50 | - | Segundo apellido |
| NumDepa | INT | - | FK, NN | Departamento administrativo al que pertenece |

### Tabla: Dependiente

Almacena los familiares beneficiarios directos vinculados a cada profesor.

| CAMPO | TIPO | LONGITUD | RESTRICCIONES | DESCRIPCION |
| :--- | :--- | :--- | :--- | :--- |
| NumProf | INT | - | PK, FK, NN | Número del profesor del cual es dependiente |
| Nombre | VARCHAR | 100 | PK, NN | Nombre completo del familiar |
| FechaNaci | DATE | - | NN | Fecha de nacimiento del dependiente |
| Parentesco | VARCHAR | 50 | NN | Vínculo familiar (Hijo, Hija, Cónyuge, etc.) |

### Tabla: Departamento

Almacena las divisiones o departamentos académicos institucionales.

| CAMPO | TIPO | LONGITUD | RESTRICCIONES | DESCRIPCION |
| :--- | :--- | :--- | :--- | :--- |
| numDepa | INT | - | PK, AI, NN | Número único identificador del departamento |
| nombre | VARCHAR | 100 | NN, UQ | Nombre de la facultad o departamento |
| Edificio | VARCHAR | 50 | - | Ubicación o bloque físico dentro del campus |

### Tabla: Proyectos
 
Almacena los proyectos de investigación o desarrollo institucionales.

| CAMPO | TIPO | LONGITUD | RESTRICCIONES | DESCRIPCION |
| :--- | :--- | :--- | :--- | :--- |
| NumberProyects | INT | - | PK, AI, NN | Código único asignado al proyecto |
| NameProyects | VARCHAR | 150 | NN | Título o nombre del proyecto |
| Presupuesto | DECIMAL | 12,2 | - | Fondo económico asignado al proyecto |

### Tabla: Participa

Tabla intermedia que controla los profesores asignados a los diferentes proyectos de desarrollo.

| CAMPO | TIPO | LONGITUD | RESTRICCIONES | DESCRIPCION |
| :--- | :--- | :--- | :--- | :--- |
| NumProfe | INT | - | PK, FK, NN | Código del profesor que participa |
| NumProyect | INT | - | PK, FK, NN | Código del proyecto en el que colabora (Nota: Vinculado a NumberProyects) |
| Rol | VARCHAR | 50 | NN | Función desempeñada (Director, Investigador, etc.) |
| FechaInicio | DATE | - | NN | Fecha en la que el profesor se integra al proyecto |

## 5. Relaciones en la Base de Datos

| Relacion | Cardinalidad | Descripcion |
| :--- | :--- | :--- |
| Alumno --> Telefono | 1:N | Un alumno puede registrar varios números de teléfono |
| Alumno --> Credencial | 1:1 | Un alumno posee una única credencial de identificación activa |
| Alumno --> Cursa | 1:N | Un alumno puede tomar varias materias |
| Materia --> Cursa | 1:N | Una materia puede ser cursada por múltiples alumnos |
| Profesor --> Materia | 1:N | Un profesor puede ser titular de varias materias |
| Profesor --> Dependiente | 1:N | Un profesor puede tener múltiples dependientes registrados |
| Departamento --> Profesor | 1:N | Un departamento coordina a muchos profesores |
| Profesor --> Participa | 1:N | Un profesor puede colaborar en diversos proyectos |
| Proyectos --> Participa | 1:N | Un proyecto cuenta con la participación de varios profesores |

## 6. Llaves Foráneas (FK)

| Tabla | Campo FK | Referencia |
| :--- | :--- | :--- |
| Telefono | Matricula | Alumno (Matricula) |
| Credencial | Matricula | Alumno (Matricula) |
| Cursa | Matricula | Alumno (Matricula) |
| Cursa | ClaveMateria | Materia (ClaveMateria) |
| Materia | numProf | Profesor (Numprofe) |
| Profesor | NumDepa | Departamento (numDepa) |
| Dependiente | NumProf | Profesor (Numprofe) |
| Participa | NumProfe | Profesor (Numprofe) |
| Participa | NumProyect | Proyectos (NumberProyects) |

## 7. Integridad Referencial

| Reglas | Descripcion |
| :--- | :--- |
| IR-01 | No se puede emitir una credencial si la `Matricula` del alumno no existe previamente. |
| IR-02 | No se puede asentar un registro en `Cursa` si los datos del alumno (`Matricula`) o la materia (`ClaveMateria`) no están dados de alta. |
| IR-03 | No se puede eliminar un departamento de la tabla `Departamento` si este posee profesores asignados en `Profesor`. |
| IR-04 | Al dar de baja a un profesor (`Numprofe`), sus dependientes y asignaciones de participación en proyectos deben limpiarse para evitar inconsistencias. |

## 8. Reglas de Negocio

| Codigo | Regla |
| :--- | :--- |
| RN-01 | La `CalificacionFinal` contenida en la tabla `Cursa` debe evaluarse exclusivamente en un rango de 0.00 a 10.00. |
| RN-02 | La fecha de `Vigencia` de la credencial debe ser estrictamente posterior a la `FechaInscripcion`. |
| RN-03 | El campo `Presupuesto` de la tabla `Proyectos` solo aceptará valores numéricos positivos. |
| RN-04 | La llave primaria compuesta de la tabla `Telefono` (`TelefonoID`, `Matricula`) impide que dos alumnos tengan registrada la misma línea telefónica bajo la misma cuenta. |

## 9. Diagrama Relacional
 ![ Ejercicio 6](/img/E-R/ejercicio5.6.png)

# EJERCICIO 7

## Diccionario de Datos de la Base de Datos de Control Escolar Integral

## 1. Información General

| ELEMENTO | VALOR |
| :--- | :--- |
| Proyecto | Sistema Integral de Control Escolar, Profesores y Proyectos |
| Version | 1.0 |
| Fecha | Junio 2026 |
| Elaboró | Angel Santiago Jimenez Sarabia |
| SGBD | SQL Server |

## 2. Descripción del Sistema de Base de Datos

El sistema administra la información académica y administrativa de una institución educativa.

Permite controlar:

    - Registro de alumnos.
    - Registro de teléfonos asociados a los alumnos.
    - Credenciales institucionales.
    - Materias impartidas.
    - Historial de materias cursadas.
    - Profesores.
    - Departamentos académicos.
    - Dependientes de los profesores.
    - Proyectos institucionales.
    - Participación de profesores en proyectos.

El objetivo principal es mantener organizada la información académica y administrativa mediante relaciones entre las diferentes entidades de la base de datos.

## 3. Catálogo de Restricciones Utilizadas

| CODIGO | SIGNIFICADO |
| :--- | :--- |
| PK | Primary Key |
| FK | Foreign Key |
| NN | NOT NULL |
| UQ | UNIQUE |
| AI | Auto Increment |
| CK | CHECK |
| DF | DEFAULT |

# 4. Diccionario de Datos

## Tabla: Alumno

Almacena la información personal de los estudiantes inscritos.

| CAMPO | TIPO | LONGITUD | RESTRICCIONES | DESCRIPCIÓN |
| :--- | :--- | :--- | :--- | :--- |
| Matricula | VARCHAR | 20 | PK, NN | Identificador único del alumno |
| Nombre | VARCHAR | 50 | NN | Nombre del alumno |
| Apellido1 | VARCHAR | 50 | NN | Primer apellido |
| Apellido2 | VARCHAR | 50 | | Segundo apellido |
| Correo | VARCHAR | 100 | NN, UQ | Correo electrónico |
| FechaNac | DATE | | NN | Fecha de nacimiento |

## Tabla: Telefono

Almacena los números telefónicos registrados por los alumnos.

| CAMPO | TIPO | LONGITUD | RESTRICCIONES | DESCRIPCIÓN |
| :--- | :--- | :--- | :--- | :--- |
| TelefonoID | VARCHAR | 15 | PK, NN | Identificador del teléfono |
| Matricula | VARCHAR | 20 | FK, NN | Alumno propietario |
| NumeroTotal | VARCHAR | 15 | NN | Número telefónico |

## Tabla: Credencial

Guarda la información de las credenciales institucionales.

| CAMPO | TIPO | LONGITUD | RESTRICCIONES | DESCRIPCIÓN |
| :--- | :--- | :--- | :--- | :--- |
| NumCredencial | VARCHAR | 20 | PK, NN | Número único de credencial |
| FechaInscripcion | DATE | | NN | Fecha de inscripción |
| Vigencia | DATE | | NN | Fecha de vigencia |
| Matricula | VARCHAR | 20 | FK, NN, UQ | Alumno propietario |

## Tabla: Materia

Contiene el catálogo de materias.

| CAMPO | TIPO | LONGITUD | RESTRICCIONES | DESCRIPCIÓN |
| :--- | :--- | :--- | :--- | :--- |
| ClaveMateria | VARCHAR | 10 | PK, NN | Clave única |
| NombreMateria | VARCHAR | 100 | NN | Nombre de la materia |
| Creditos | INT | | NN | Créditos asignados |
| NumProf | INT | | FK, NN | Profesor responsable |

## Tabla: Cursa

Representa la relación entre alumnos y materias.

| CAMPO | TIPO | LONGITUD | RESTRICCIONES | DESCRIPCIÓN |
| :--- | :--- | :--- | :--- | :--- |
| Matricula | VARCHAR | 20 | PK, FK, NN | Alumno inscrito |
| ClaveMateria | VARCHAR | 10 | PK, FK, NN | Materia cursada |
| FechaInscripcion | DATE | | NN | Fecha de inscripción |
| CalifFinal | DECIMAL | 4,2 | CK | Calificación final |

## Tabla: Profesor

Registra los profesores de la institución.

| CAMPO | TIPO | LONGITUD | RESTRICCIONES | DESCRIPCIÓN |
| :--- | :--- | :--- | :--- | :--- |
| NumProf | INT | | PK, AI, NN | Identificador del profesor |
| Nombre | VARCHAR | 50 | NN | Nombre |
| Apellido1 | VARCHAR | 50 | NN | Primer apellido |
| Apellido2 | VARCHAR | 50 | | Segundo apellido |
| NumDepto | INT | | FK, NN | Departamento al que pertenece |

## Tabla: Departamento

Registra los departamentos académicos.

| CAMPO | TIPO | LONGITUD | RESTRICCIONES | DESCRIPCIÓN |
| :--- | :--- | :--- | :--- | :--- |
| NumDepto | INT | | PK, AI, NN | Identificador |
| Nombre | VARCHAR | 100 | NN | Nombre del departamento |
| Edificio | VARCHAR | 50 | | Edificio asignado |

## Tabla: Proyecto

Contiene los proyectos institucionales.

| CAMPO | TIPO | LONGITUD | RESTRICCIONES | DESCRIPCIÓN |
| :--- | :--- | :--- | :--- | :--- |
| NumProy | INT | | PK, AI, NN | Número del proyecto |
| NombreProy | VARCHAR | 150 | NN | Nombre del proyecto |
| Presupuesto | DECIMAL | 12,2 | NN | Presupuesto asignado |

## Tabla: Participa

Relaciona profesores con proyectos.

| CAMPO | TIPO | LONGITUD | RESTRICCIONES | DESCRIPCIÓN |
| :--- | :--- | :--- | :--- | :--- |
| NumProf | INT | | PK, FK, NN | Profesor |
| NumProy | INT | | PK, FK, NN | Proyecto |
| Rol | VARCHAR | 50 | NN | Rol desempeñado |
| FechaInicio | DATE | | NN | Fecha de inicio |

## Tabla: Dependiente

Registra los dependientes de cada profesor.

| CAMPO | TIPO | LONGITUD | RESTRICCIONES | DESCRIPCIÓN |
| :--- | :--- | :--- | :--- | :--- |
| NumProf | INT | | PK, FK, NN | Profesor |
| Nombre | VARCHAR | 100 | PK, NN | Nombre del dependiente |
| FechaNac | DATE | | NN | Fecha de nacimiento |
| Parentesco | VARCHAR | 50 | NN | Relación familiar |

# 5. Relaciones en la Base de Datos

| Relación | Cardinalidad | Descripción |
| :--- | :--- | :--- |
| Alumno → Telefono | 1:N | Un alumno puede tener varios teléfonos. |
| Alumno → Credencial | 1:1 | Cada alumno posee una credencial. |
| Alumno → Cursa | 1:N | Un alumno puede cursar muchas materias. |
| Materia → Cursa | 1:N | Una materia puede ser cursada por muchos alumnos. |
| Profesor → Materia | 1:N | Un profesor puede impartir varias materias. |
| Departamento → Profesor | 1:N | Un departamento administra varios profesores. |
| Profesor → Dependiente | 1:N | Un profesor puede registrar varios dependientes. |
| Profesor → Participa | 1:N | Un profesor puede participar en varios proyectos. |
| Proyecto → Participa | 1:N | Un proyecto puede tener varios profesores. |

# 6. Llaves Foráneas

| Tabla | Campo FK | Referencia |
| :--- | :--- | :--- |
| Telefono | Matricula | Alumno(Matricula) |
| Credencial | Matricula | Alumno(Matricula) |
| Cursa | Matricula | Alumno(Matricula) |
| Cursa | ClaveMateria | Materia(ClaveMateria) |
| Materia | NumProf | Profesor(NumProf) |
| Profesor | NumDepto | Departamento(NumDepto) |
| Dependiente | NumProf | Profesor(NumProf) |
| Participa | NumProf | Profesor(NumProf) |
| Participa | NumProy | Proyecto(NumProy) |

# 7. Integridad Referencial

| Código | Descripción |
| :--- | :--- |
| IR-01 | No puede existir un teléfono sin un alumno registrado. |
| IR-02 | No puede existir una credencial sin un alumno. |
| IR-03 | No puede registrarse una materia cursada sin alumno y materia existentes. |
| IR-04 | No puede asignarse una materia a un profesor inexistente. |
| IR-05 | No puede eliminarse un departamento mientras existan profesores asociados. |
| IR-06 | No puede eliminarse un profesor mientras tenga dependientes o proyectos asignados. |

# 8. Reglas de Negocio

| Código | Regla |
| :--- | :--- |
| RN-01 | Un alumno solo puede tener una credencial activa. |
| RN-02 | La vigencia de la credencial debe ser mayor a la fecha de inscripción. |
| RN-03 | La calificación final debe estar entre 0 y 10. |
| RN-04 | El presupuesto de un proyecto debe ser mayor que cero. |
| RN-05 | Un profesor puede impartir varias materias pero cada materia tiene un solo profesor responsable. |
| RN-06 | Un profesor puede participar en varios proyectos desempeñando distintos roles. |

# 9. Diagrama Relacional
![Resultado Ejercicio 1](/img/E-R/ejercicio6.7.png)
