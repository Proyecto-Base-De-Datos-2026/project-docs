# Diccionario de Datos - Sistema de Clínica Veterinaria

Este documento contiene la estructura detallada de la base de datos para el sistema de la clínica veterinaria, especificando campos, tipos de datos y descripciones para cada entidad.

---

## 1. Dueño
| Campo | Tipo | Descripción |
| :--- | :--- | :--- |
| `id_dueño` | INT | Identificador único del dueño |
| `nombre` | VARCHAR | Nombre completo del dueño |
| `telefono` | VARCHAR | Número de contacto |
| `correo` | VARCHAR | Correo electrónico |

## 2. Mascota
| Campo | Tipo | Descripción |
| :--- | :--- | :--- |
| `id_mascota` | INT | Identificador único de la mascota |
| `nombre` | VARCHAR | Nombre de la mascota |
| `especie` | VARCHAR | Tipo de animal |
| `raza` | VARCHAR | Raza de la mascota |
| `edad` | INT | Edad en años |
| `id_dueño` | INT | Relación con el dueño |

## 3. Veterinario
| Campo | Tipo | Descripción |
| :--- | :--- | :--- |
| `id_veterinario` | INT | Identificador único del veterinario |
| `nombre` | VARCHAR | Nombre del veterinario |
| `especialidad` | VARCHAR | Área de especialización |

## 4. Cita
| Campo | Tipo | Descripción |
| :--- | :--- | :--- |
| `id_cita` | INT | Identificador de la cita |
| `fecha` | DATE | Fecha de la cita |
| `motivo` | VARCHAR | Motivo de la consulta |
| `id_mascota` | INT | Mascota atendida |
| `id_veterinario` | INT | Veterinario asignado |

## 5. Historia Clínica
| Campo | Tipo | Descripción |
| :--- | :--- | :--- |
| `id_historia` | INT | Identificador de la historia clínica |
| `diagnostico` | TEXT | Diagnóstico médico |
| `observaciones` | TEXT | Observaciones adicionales |
| `id_cita` | INT | Relación con la cita |

## 6. Tratamiento
| Campo | Tipo | Descripción |
| :--- | :--- | :--- |
| `id_tratamiento` | INT | Identificador del tratamiento |
| `descripcion` | TEXT | Descripción del tratamiento |
| `id_historia` | INT | Relación con historia clínica |

## 7. Medicamento
| Campo | Tipo | Descripción |
| :--- | :--- | :--- |
| `id_medicamento` | INT | Identificador del medicamento |
| `nombre` | VARCHAR | Nombre del medicamento |
| `dosis` | VARCHAR | Dosis recomendada |

## 8. Tratamiento_Medicamento
| Campo | Tipo | Descripción |
| :--- | :--- | :--- |
| `id_tratamiento` | INT | Relación con tratamiento |
| `id_medicamento` | INT | Relación con medicamento |

## 9. Pago
| Campo | Tipo | Descripción |
| :--- | :--- | :--- |
| `id_pago` | INT | Identificador del pago |
| `monto` | DECIMAL | Valor del pago |
| `fecha` | DATE | Fecha del pago |
| `metodo_pago` | VARCHAR | Forma de pago |
| `id_cita` | INT | Relación con la cita |
