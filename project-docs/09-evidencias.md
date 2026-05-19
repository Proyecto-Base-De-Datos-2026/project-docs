Separación DDL/DML
DDL (Data Definition Language): Se estructuraron las migraciones encargadas de definir el esquema de la base de datos.
Se dividió en archivos independientes para las tablas maestras (dueno, mascota, veterinario), las tablas relacionales/transaccionales
(cita, pago, historia_clinica, etc.) y la lógica programable (funciones, procedimientos y disparadores).
Esto garantiza que el motor cree los contenedores de datos respetando estrictamente la integridad referencial.

DML (Data Manipulation Language): Se aisló la manipulación de datos en scripts independientes agrupados jerárquicamente en las carpetascanonical y volumetric, permitiendo poblar la base de datos de manera controlada una vez que la estructura DDL se encuentre completamente desplegada.

<img width="986" height="87" alt="image" src="https://github.com/user-attachments/assets/f49c815e-7d7a-4250-833f-47ffdd6570fb" />


df
