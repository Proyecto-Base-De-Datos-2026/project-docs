-Separación DDL/DML

DDL (Data Definition Language): Se estructuraron las migraciones encargadas de definir el esquema de la base de datos.
Se dividió en archivos independientes para las tablas maestras (dueno, mascota, veterinario), las tablas relacionales/transaccionales
(cita, pago, historia_clinica, etc.) y la lógica programable (funciones, procedimientos y disparadores).
Esto garantiza que el motor cree los contenedores de datos respetando estrictamente la integridad referencial.

DML (Data Manipulation Language): Se aisló la manipulación de datos en scripts independientes agrupados jerárquicamente en las carpetascanonical y volumetric, permitiendo poblar la base de datos de manera controlada una vez que la estructura DDL se encuentre completamente desplegada.

DDL


<img width="317" height="312" alt="image" src="https://github.com/user-attachments/assets/c89e3064-f149-4237-942a-d906ff7e1fe9" />


DML


<img width="312" height="466" alt="image" src="https://github.com/user-attachments/assets/bf35b8c0-fe54-440a-8d52-0818a3c66a8e" />



-Descripción de Datos Canónicos

Corresponden al conjunto de datos maestros, estandarizados e invariables que el sistema requiere para su correcto funcionamiento operativo desde el primer día. Incluye:

Tipos de especialidades de los veterinarios.

Catálogo base de medicamentos estándar con sus respectivas unidades de medida.

Registros iniciales de administración y configuración del sistema.


-Descripción de Datos Volumétricos

Corresponden a la carga masiva y transaccional diseñada para simular el comportamiento de la veterinaria en un entorno real de alta producción. Se distribuyeron más de 100 registros (distribuidos en 9 archivos SQL secuenciales) que generan una densa red de relaciones entre dueños, mascotas, registros de citas médicas, generación de facturas y seguimientos en historias clínicas.


-Evidencia de Docker.



<img width="986" height="87" alt="image" src="https://github.com/user-attachments/assets/f49c815e-7d7a-4250-833f-47ffdd6570fb" />



Evidencia de migraciones y carga de datos.



<img width="464" height="165" alt="image" src="https://github.com/user-attachments/assets/4c9fe096-c161-4137-a711-c0fa6d89d37f" />




Evidencia de rollback.




<img width="694" height="618" alt="image" src="https://github.com/user-attachments/assets/51910e35-430d-40cc-af54-96929e96d12f" />



Evidencia de Migración

Descripción: Se ejecutó el pipeline de Liquibase aplicando 31 cambios estructurales (DDL) y de datos (DML) de forma exitosa.


Evidencia de Carga de Datos

Descripción: Proceso de carga volumétrica finalizado con éxito, insertando 232 registros en las tablas del sistema.



<img width="692" height="207" alt="image" src="https://github.com/user-attachments/assets/b7bd3939-5d2b-45ce-8d21-93ed72feb4ed" />









