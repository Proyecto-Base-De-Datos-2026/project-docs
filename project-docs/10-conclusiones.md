Solución a la problemática operativa: El proyecto aborda eficazmente la falta de un sistema centralizado, lo cual permitirá mitigar la pérdida de información médica, reducir errores en la programación de citas y mejorar el seguimiento de los tratamientos.

Diseño relacional estructurado: Se ha diseñado un modelo lógico sólido que garantiza la integridad de los datos mediante el uso adecuado de llaves primarias (PK) y llaves foráneas (FK). Este diseño permite una gestión organizada de las entidades principales: Dueño, Mascota, Veterinario, Cita, Historia Clínica, Tratamiento, Medicamento y Pago.

Cumplimiento de reglas de negocio: El modelo propuesto integra restricciones fundamentales, tales como la obligatoriedad de un dueño para cada mascota, la asociación única entre citas e historias clínicas, y la validación de pagos, asegurando que la lógica operativa de la clínica se mantenga consistente dentro de la base de datos.

Escalabilidad y tecnología: Al basarse en PostgreSQL y contemplar requisitos no funcionales como la seguridad y la integridad, el sistema está estructurado para ser escalable y capaz de adaptarse a las necesidades futuras de crecimiento de la clínica.

Resolución de relaciones complejas: La implementación de una tabla intermedia (Tratamiento_Medicamento) resuelve correctamente la relación de muchos a muchos entre tratamientos y medicamentos, permitiendo que un tratamiento pueda incluir múltiples medicamentos y viceversa.
