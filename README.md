# Análisis de accidentalidad en Madrid en 2025

## 1. Objetivo principal del proyecto 🎯 

Realizar un análisis exploratorio de datos (EDA) de un conjunto de registros de accidentes de tráfico con el fin de identificar patrones, relaciones y factores asociados a la tipología y gravedad de los siniestros. Este análisis busca generar insights útiles para apoyar la toma de decisiones en materia de seguridad vial, prevención y gestión urbana.

## 2. Estructura del proyecto
```bash
|--- Datos
    |-- 2025_Accidentalidad.csv #Datos originales
|--- Excels
    |--Carga_Trans_Datos.xlsx #Datos transformados
    |--Datos_analisis #Tablas de análisis de datos
|--- README
```

## 3. Descripción de las columnas del conjunto de datos

El conjunto de datos utilizado contiene información detallada sobre accidentes de tráfico ocurridos en el primer cuatrimestre de 2025 en la ciudad de Madrid. A continuación se describen las columnas que lo componen:

| **Columna**            | **Descripción**                                                                                 |
| ---------------------- | ----------------------------------------------------------------------------------------------- |
| `num_expediente`       | Identificador único del expediente asociado a cada accidente.                                   |
| `Fecha`                | Fecha en la que ocurrió el accidente (formato: dd/mm/aa).                                       |
| `Hora`                 | Hora exacta del accidente (formato: hh\:mm\:ss).                                                |
| `Localizacion`         | Nombre de la calle donde ocurrió el accidente.                                                  |
| `Numero`               | Número específico dentro de la calle (portal o referencia numérica).                            |
| `cod_distrito`         | Código numérico que representa el distrito donde ocurrió el accidente.                          |
| `Distrito`             | Nombre del distrito correspondiente.                                                            |
| `tipo_accidente`       | Clasificación del tipo de accidente (colisión, atropello, etc.).                                |
| `estado_meteorológico` | Condiciones climáticas al momento del accidente (lluvia, despejado, etc.).                      |
| `tipo_vehiculo`        | Tipo de vehículo involucrado (turismo, motocicleta, bicicleta, etc.).                           |
| `tipo_persona`         | Rol de la persona implicada: conductor, pasajero o peatón.                                      |
| `rango_edad`           | Rango de edad de la persona implicada.                                                          |
| `sexo`                 | Sexo de la persona implicada (Hombre o Mujer).                                                  |
| `cod_lesividad`        | Código que representa el grado de lesividad.                                                    |
| `lesividad`            | Tipo de asistencia recibida: asistencia inmediata, ambulatoria, fallecido, sin asistencia, etc. |
| `coordenada_x_utm`     | Coordenada X en proyección UTM del lugar del accidente.                                         |
| `coordenada_y_utm`     | Coordenada Y en proyección UTM del lugar del accidente.                                         |
| `positiva_alcohol`     | Indica si la persona dio positivo en alcohol (N/S).                                             |
| `positiva_droga`       | Indica si la persona dio positivo en sustancias estupefacientes (1 o vacío).                    |


## 4. 📊 Descripción de EDA (Análisis Exploratorio de Datos)

### 4.1 🔧 Limpieza y transformación de datos

Antes de realizar el análisis, se aplicaron diversas acciones de limpieza y transformación para garantizar la calidad y trazabilidad del dataset:

- **Sin clave primaria:** El dataset original no contaba con una clave única por fila.

- **Eliminación de duplicados:** Se eliminaron registros duplicados. Se identificaron 696 duplicados, quedando 16.020 registros únicos.

- **Generación de columna Mes:** A partir de la columna Fecha, se extrajo el mes del accidente para facilitar análisis temporales.

- **Columna Numero:** No se aplicó transformación ya que su uso es nominal y no será analizado cuantitativamente.

- **Normalización de columna lesividad:** Se creó una nueva columna con valores consistentes, imputando aquellos registros con celdas en blanco mediante una función SI encadenada con LARGO().

- **Transformación en positiva_alcohol:** Se reemplazaron los valores originales para mayor claridad (Si, No, Desconocido) e imputaron celdas vacías.

- **Transformación en positiva_droga:** Se sustituyó la codificación binaria (1 = Sí, blanco = No) por valores explícitos (Sí, No) y se completaron los datos faltantes.

- **Imputación en estado_meteorológico:** Se creó una columna complementaria que asigna el valor "Se desconoce" a las celdas vacías.

- **Imputación en tipo_vehiculo:** Se creó una nueva columna que reemplaza valores vacíos por "Sin datos".

- **Creación de columna id_fila:** Se generó un identificador único por fila para asegurar trazabilidad del dato a lo largo del análisis.

- **Clave compuesta única por persona (clave_persona):**
Se construyó una columna que permite identificar de forma única a cada persona involucrada en un accidente.
Fórmula utilizada:

       =[@[num_expediente]] & "_" & [@tipo_persona] & "_" & [@tipo_vehiculo] & "_" & [@sexo] & "_" & [@rango_edad]

- **Columna dia_semana:** Extraída de la columna Fecha para análisis por día.

- **Columna rango_hora:** Categorización del horario del accidente según el siguiente criterio:

      =SI(HORA([@hora])<6;"Madrugada";SI(HORA([@hora])<12;"Mañana";SI(HORA([@hora])<18;"Tarde";"Noche")))

### 4.2 🧠 Análisis de los datos

Para realizar el dahsboard analizamos las variables que generan una mayor influencia en los resultados de accidentalidad en Madrid.

## 5. Resultados y conclusiones
