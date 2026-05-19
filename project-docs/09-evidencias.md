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


-Evidencia de Migración:

Descripción: Se ejecutó el pipeline de Liquibase aplicando 31 cambios estructurales (DDL) y de datos (DML) de forma exitosa.


-Evidencia de Carga de Datos:

Descripción: Proceso de carga volumétrica finalizado con éxito, insertando 232 registros en las tablas del sistema.



Evidencia de rollback.




<img width="694" height="618" alt="image" src="https://github.com/user-attachments/assets/51910e35-430d-40cc-af54-96929e96d12f" />






<img width="692" height="207" alt="image" src="https://github.com/user-attachments/assets/b7bd3939-5d2b-45ce-8d21-93ed72feb4ed" />



-Evidencia de los trigger, procedure, function y JOIN de más de 5 tablas de cada integrante



Integrante 1: Carlos Andrés Zuluaga Acuña

Evidencia de Función: fn_total_gastado_dueno. Calcula el monto acumulado invertido por un cliente cruzando pago, cita y mascota. Maneja valores nulos mediante COALESCE.

Evidencia de Procedimiento: pr_cancelar_cita. Actualiza el estado de una fila específica en la tabla cita a 'cancelada' mediante su identificador.

Evidencia de Gatillo (Trigger): tr_alerta_nueva_cita. Monitorea inserciones en cita (AFTER INSERT) y dispara un RAISE NOTICE capturando el ID de la mascota entrante con la variable contextual NEW.

Evidencia de JOIN (> 5 tablas): Consulta avanzada de 7 tablas (medicamento $\rightarrow$ tratamiento_medicamento $\rightarrow$ tratamiento $\rightarrow$ historia_clinica $\rightarrow$ cita $\rightarrow$ mascota $\rightarrow$ dueno). Rastrea qué fármacos consume cada paciente según su raza y propietario.

----------------------------------------------------------------------------------------------------------

Integrante 2: [Nombre Integrante 2]
Evidencia de Función: fn_contar_citas_mascota. Ejecuta un conteo (COUNT(*)) de las citas que registren el estado explícito de 'completada' para un paciente específico.

Evidencia de Procedimiento: pr_registrar_mascota. Encapsula y estandariza la inserción segura de nuevos registros en la tabla mascota.

Evidencia de Gatillo (Trigger): tr_validar_edad_mascota. Bloque de seguridad analítica (BEFORE INSERT OR UPDATE) que intercepta la transacción e impide el registro de edades incoherentes (menores a 0 o mayores a 30) mediante un RAISE EXCEPTION.

Evidencia de JOIN (> 5 tablas): Consulta avanzada de 6 tablas que unifica pago, cita, mascota, dueno, veterinario e historia_clinica para auditar la relación financiera directa por cada procedimiento médico.

--------------------------------------------------------------------------------------------------------------------

👤 Integrante 3: [Nombre Integrante 3]
Evidencia de Función: fn_veterinario_mas_activo. Agrupa el volumen de citas del personal médico y a través de un ordenamiento descendente con un límite estricto (LIMIT 1), aísla el nombre del médico con mayor tasa de atención.

Evidencia de Procedimiento: pr_actualizar_contacto_dueno. Rutina de mantenimiento de datos que actualiza de manera focalizada la información de contacto de los clientes.

Evidencia de Gatillo (Trigger): tr_crear_historial_automatico. Automatización del negocio que reacciona de forma inmediata a la creación de una cita (AFTER INSERT) e inserta una fila paralela en la tabla historia_clinica con diagnóstico en estado "Pendiente".

Evidencia de JOIN (> 5 tablas): Consulta avanzada de 7 tablas que cruza el personal médico con tratamientos y facturas para generar un reporte gerencial de rentabilidad operativa.

--------------------------------------------------------------------------------------------------------------------

Integrante 4: [Nombre Integrante 4]
Evidencia de Función: fn_edad_promedio_especie. Realiza un cálculo estadístico sobre el conjunto de mascotas, utilizando AVG(edad) y aplicando COALESCE para manejar de forma segura los casos donde no existan registros para una especie determinada.

Evidencia de Procedimiento: pr_actualizar_vacunas. Rutina crítica de negocio que actualiza el estado de inmunización de una mascota, validando la existencia del registro antes de aplicar la modificación.

Evidencia de Gatillo (Trigger): tr_bloqueo_borrado_citas. Mecanismo de seguridad (BEFORE DELETE) que intercepta cualquier intento de eliminación de una cita, lanzando un RAISE EXCEPTION para prevenir la pérdida de registros históricos de atención médica.

Evidencia de JOIN (> 5 tablas): Consulta avanzada de 6 tablas que integra el historial médico completo: uniendo mascota, dueno, cita, tratamiento, medicamento y veterinario, permitiendo un análisis consolidado de la trazabilidad del tratamiento prescrito a cada paciente.
----------------------------------------------------------------------------------------------------------------
-Problemas encontrados y Soluciones aplicadas


Durante el desarrollo, presentamos dificultades para diferenciar el alcance de las herramientas de consola (PowerShell) frente a la interfaz de ejecución de PostgreSQL. Esto nos llevó a ajustar nuestro flujo de trabajo, asegurando primero el acceso al contenedor (docker exec) antes de ejecutar cualquier sentencia DML. Asimismo, tuvimos dudas sobre la correcta trazabilidad de las migraciones, lo cual resolvimos validando la diferencia entre los cambios de estructura (DDL) y la carga de datos volumétricos (DML) mediante los logs de Liquibase.

-----------------------------------------------------------------------------------------
-Instrucciones de ejecución


1. Navegar al directorio del proyecto:
Abra su terminal y ubíquese en la carpeta donde descargó el proyecto:

cd C:\Users\Asus\Downloads\project-db-liquibase--main\project-db-liquibase--main
---------------------------------------
2. Limpieza si ya tiene el contenedor.

docker compose down -v
------------------------------------
3.Despliegue del motor de base de datos en segundo plano:

docker compose up -d postgres-db
---------------------------------
4. Ejecución automatizada del pipeline de migraciones (DDL/DML):

docker compose run --rm liquibase
---------------------------------------------
5. Ahora, para ver lo que hay dentro, entra a la consola de PostgreSQL:

docker-compose exec postgres-db psql -U carlos_admin -d veterinaria_db

-------------------------------------------------------------------
6.Comprobar que todo está ahí
Una vez dentro, escribe este comando para listar tus tablas:

SQL
\dt
-----------------------------------------------
7. Salir
Cuando termines de revisar, solo escribe:

SQL
\q
