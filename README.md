# Equipo MicroArquitectos

---

## Integrantes

* Nicolas Carvajal Chaves
* Wyo Hann Chu Mendez
* Sofia Velasquez Marin
* Valeria Caro Ramirez

---

## Descripción

A continuación se presenta el proyecto de la materia Diseño y construcción de soluciones no monolíticas, en el cual exploramos la división por dominios de Salud Tech de los Alpes. A continuación se muestran los hallazgos de los dominios de negocio, la documentación del lenguaje ubicuo con respecto al flujo de "anonimización,
ingestión y enriquecimiento de datos" AS-IS y TO-BE, y los contextos acotados AS-IS y TO-BE.
## Estructura del proyecto

```bash
.
├── README.md
├── build.gradle
├── gradle
├── gradle.properties
├── gradlew
├── gradlew.bat
├── images
├── settings.gradle
└── src (aquí encuentra los fragmentos de código para su calificación)
```

El proyecto cuenta con la estructura por defecto de un proyecto para correr `Context Mapper` en el cual se encuentran los archivos de configuración (`build.gradle`, `gradle.properties`, `gradlew`, `gradlew.bat`, `settings.gradle`) y la carpeta de `src/cml` en donde se encuentran donde se encuentran los archivos de código para generar los diagramas de Context Mapper. Puede visaulizar los diagramas con su respectiva información y comentarios. La carpeta `images` contiene las imágenes de los diagramas generados.

En el README se encuentra la información de los hallazgos de los dominios de negocio, la documentación del lenguaje ubicuo con respecto al flujo de "anonimización, ingestión y enriquecimiento de datos" AS-IS y TO-BE, y los contextos acotados AS-IS y TO-BE.

## Dominio de negocio

## **Dominio Principal**
| Dominio                        | Vision Statement                                                              |
|--------------------------------|-------------------------------------------------------------------------------|
| **InformacionImagenesMedicas** | Recaudar, procesar y distribuir imágenes médicas y diagnósticos anonimizados. |

## **Subdominios**
| Subdominio                               | Tipo              | Vision Statement                                                            |
|------------------------------------------|-------------------|-----------------------------------------------------------------------------|
| **Ingestion**                            | CORE_DOMAIN       | Recaudar y almacenar los datos de las imágenes médicas.                     |
| **Limpieza**                             | CORE_DOMAIN       | Limpiar y anonimizar los datos de las imágenes médicas.                     |
| **Procesamiento**                        | CORE_DOMAIN       | Estructuración y enriquecimiento de los datos de las imágenes médicas.      |
| **Distribucion**                         | CORE_DOMAIN       | Distribuir los datos de las imágenes médicas.                               |
| **Entrenamiento**                        | CORE_DOMAIN       | Crear los modelos, entrenamientos e investigación de las imágenes médicas.  |
| **Facturacion**                          | GENERIC_SUBDOMAIN | Facturar los servicios de las imágenes médicas y adquisición de datos.      |
| **GestionUsuarios**                      | GENERIC_SUBDOMAIN | Gestionar los usuarios y permisos de la plataforma de las imágenes médicas. |
| **Ventas**                               | SUPPORTING_DOMAIN | Contactar y vender los servicios Enterprise de las imágenes médicas.        |
| **SeguridadYCompliance (Solo en TO-BE)** | SUPPORTING_DOMAIN | Supervisar y regular los procesos de la operación de las imágenes médicas.  |
| **RegionEEUU (Solo en TO-BE)**           | SUPPORTING_DOMAIN | Segmentar y almacenar los datos de las imágenes médicas en EE.UU.           |
| **RegionLATAM (Solo en TO-BE)**          | SUPPORTING_DOMAIN | Segmentar y almacenar los datos de las imágenes médicas en LATAM.           |

## Lenguaje ubicuo flujo "anonimización, ingestión y enriquecimiento de datos"

### AS-IS

![Lenguaje ubicuo (AS-IS) flujo "anonimización, ingestión y enriquecimiento de datos"](./images/flujo-asis.png)

// TODO: Descripción del flujo AS-IS

### TO-BE

![Lenguaje ubicuo (TO-BE) flujo "anonimización, ingestión y enriquecimiento de datos"](./images/flujo-tobe.png)

// TODO: Descripción del flujo TO-BE

## Contexto acotado

### AS-IS

![Contexto acotado (AS-IS)](./images/saludtech_ContextMap.png)

// TODO: Descripción del contexto acotado AS-IS


### TO-BE

![Contexto acotado (TO-BE)](./images/saludtech_ContextMapTOBE.png)

##### Contextos Acotados en InformacionImagenesMedicasMap_TO_BE

###### **Contextos Acotados**
| Contexto                         | Descripción                                                                                                                                                                |
|----------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **ContextoIngestion**            | Maneja la recolección, limpieza y almacenamiento de datos de imágenes médicas.                                                                                             |
| **ContextoProcesamiento**        | Estructura y enriquece los datos de las imágenes médicas antes de su uso en otros contextos.                                                                               |
| **ContextoDistribucion**         | Se encarga de la entrega de datos procesados a los diferentes consumidores, esto incluye tanto a clientes como a los expertos que se contratan para los planes enterprise. |
| **ContextoEntrenamiento**        | Administra la creación, entrenamiento e investigación de modelos basados en imágenes médicas cuando se solicita un plan enterprise.                                        |
| **ContextoFacturacion**          | Gestiona la facturación de los servicios de la compaía.                                                                                                                    |
| **ContextoGestionUsuarios**      | Administra usuarios y sus permisos dentro de la plataforma.                                                                                                                |
| **ContextoSeguridadYCompliance** | Supervisa la regulación y cumplimiento de normativas en la gestión de imágenes médicas.                                                                                    |
| **ContextoRegionEEUU**           | Maneja el almacenamiento y segmentación de datos en EE.UU., respetando normativas locales.                                                                                 |
| **ContextoRegionLATAM**          | Maneja el almacenamiento y segmentación de datos en LATAM, respetando normativas locales.                                                                                  |

---

## **Relaciones entre Contextos Acotados**
Las relaciones entre los contextos se justifican con los siguientes patrones:

1. **Uso de ACL (Anti-Corruption Layer)**: Se emplea en **Facturación y Gestión de Usuarios** para interactuar con sistemas externos y evitar el acoplamiento directo con modelos internos.
2. **Uso de OHS (Open Host Service) y PL (Published Language)**: Se aplica en los contextos de **Ingestión, Procesamiento, Distribución, Entrenamiento, Seguridad y Regiones** para proteger a los consumidores de cambios en el modelo y facilitar la traducción del modelo a un lenguaje publicado.

| Relación                                                       | Explicación                                                                                                                                   |
|----------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------|
| **ContextoProcesamiento ← [OHS, PL] ContextoIngestion**        | El procesamiento depende de la ingesta de imágenes y debe recibir datos en un formato estable y estandarizado.                                |
| **ContextoProcesamiento ← [OHS, PL] ContextoDistribucion**     | La distribución usa los datos procesados, por lo que el modelo de datos debe mantenerse estable para los consumidores.                        |
| **ContextoProcesamiento ← [OHS, PL] ContextoEntrenamiento**    | Los modelos de entrenamiento dependen de los datos procesados de imágenes, por lo que necesitan una interfaz pública clara.                   |
| **ContextoEntrenamiento ← [OHS, PL] ContextoDistribucion**     | La distribución facilita el acceso a modelos entrenados, por lo que el lenguaje publicado es clave para interoperabilidad.                    |
| **ContextoFacturacion ← [ACL] ContextoEntrenamiento**          | Se usa ACL porque la facturación depende de información de modelos y entrenamientos que provienen de otro sistema.                            |
| **ContextoFacturacion ← [ACL] ContextoDistribucion**           | La facturación de acceso a datos y servicios de distribución requiere ACL para desacoplar la lógica de negocio. e ntegrar con otros sistemas. |
| **ContextoDistribucion ← [ACL] ContextoGestionUsuarios**       | Los permisos de usuarios impactan en la distribución de datos, por lo que se necesita ACL para interactuar con el sistema de autenticación.   |
| **ContextoFacturacion ← [ACL] ContextoGestionUsuarios**        | La facturación está ligada a la gestión de usuarios, y ACL permite integrar sin modificar modelos internos.                                   |
| **ContextoSeguridadYCompliance ← [OHS, PL] ContextoIngestion** | La seguridad y cumplimiento necesitan un acceso estable a la información ingerida, protegiéndose de cambios internos.                         |
| **ContextoRegionEEUU ← [OHS, PL] ContextoIngestion**           | Para garantizar normativas locales, este contexto consume datos ingeridos en un formato estandarizado.                                        |
| **ContextoRegionLATAM ← [OHS, PL] ContextoIngestion**          | Similar al contexto de EE.UU., este módulo necesita datos ingeridos en un formato predefinido para cumplir regulaciones.                      |
