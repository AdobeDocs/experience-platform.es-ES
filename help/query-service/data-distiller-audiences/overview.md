---
title: Crear audiencias con SQL
description: Aprenda a utilizar la extensión de audiencia SQL en el Distiller de datos de Adobe Experience Platform para crear, administrar y publicar audiencias mediante comandos SQL. Esta guía cubre todos los aspectos del ciclo vital de la audiencia, incluida la creación, actualización y eliminación de perfiles, y el uso de definiciones de audiencia basadas en datos para dirigirse a destinos basados en archivos.
source-git-commit: b790dc0a485011022ac637f9d9c55f21c882d5fc
workflow-type: tm+mt
source-wordcount: '1166'
ht-degree: 1%

---

# Crear audiencias con SQL

Este documento explica cómo utilizar la extensión de audiencia SQL en Data Distiller de Adobe Experience Platform para crear, administrar y publicar audiencias mediante comandos SQL.

Utilice la extensión de audiencia SQL para crear audiencias con datos del lago de datos, incluidas las entidades de dimensión existentes. Esta extensión le permite definir segmentos de audiencia directamente mediante SQL, lo que ofrece flexibilidad sin necesidad de datos sin procesar en los perfiles. Las audiencias creadas con este método se registran automáticamente en el espacio de trabajo de Audience, donde puede segmentarlas a destinos basados en archivos.

![Infografía que muestra el flujo de trabajo de la extensión de audiencia SQL. Las fases incluyen: generar audiencias con el servicio de consulta mediante comandos SQL, administrarlas en la interfaz de usuario de Platform para activarlas en destinos basados en archivos.](../images/data-distiller/sql-audiences/sql-audience-extension-workflow.png)

## Ciclo de vida de creación de audiencias en Data Distiller {#audience-creation-lifecycle}

Siga estos pasos para administrar sus audiencias de forma eficaz. Las audiencias creadas se integran perfectamente en el flujo de audiencias, lo que le permite generar segmentos a partir de estas audiencias base y segmentar destinos basados en archivos para la segmentación de clientes. Use los siguientes comandos SQL para [crear](#create-audience), [modificar](#add-profiles-to-audience) y [eliminar](#delete-audience) audiencias en Adobe Experience Platform.

### Crear un público {#create-audience}

Utilice el comando `CREATE AUDIENCE AS SELECT` para definir una audiencia nueva. La audiencia creada se guardará en un conjunto de datos y se registrará en el espacio de trabajo de [!UICONTROL Audiencias] en Data Distiller.

```sql
CREATE AUDIENCE table_name  
WITH (primary_identity='IdentitycolName', identity_namespace='Namespace for the identity used', [schema='target_schema_title']) 
AS (select_query)
```

**Parámetros**

Utilice estos parámetros para definir la consulta de creación de audiencias SQL:

| Parámetro | Descripción |
|--------------------|------------------------------------------------------------------|
| `schema` | Opcional. Define el esquema XDM para el conjunto de datos creado por la consulta. |
| `table_name` | Nombre de la tabla y audiencia. |
| `primary_identity` | Especifica la columna de identidad principal de la audiencia. |
| `identity_namespace` | Área de nombres de la identidad. |
| `select_query` | Una instrucción SELECT que define la audiencia. La sintaxis de la consulta SELECT se encuentra en la sección [consultas SELECT](../sql/syntax.md#select-queries). |

{style="table-layout:auto"}

**Ejemplo:**

El siguiente ejemplo muestra cómo estructurar la consulta de creación de audiencias SQL:

```sql
CREATE Audience aud_test 
WITH (primary_identity=month, identity_namespace=queryService) 
AS SELECT month FROM profile_dim_date LIMIT 5;
```

**Limitaciones:**

Tenga en cuenta las siguientes limitaciones al utilizar SQL para la creación de audiencias:

- La columna de identidad principal **debe** estar en el nivel raíz.
- Los nuevos lotes sobrescriben los conjuntos de datos existentes; actualmente no se admite la funcionalidad de anexar.
- Actualmente no se admiten atributos anidados.

### Añadir perfiles a una audiencia existente {#add-profiles-to-audience}

Utilice el comando `INSERT INTO` para agregar perfiles a una audiencia existente.

```sql
INSERT INTO table_name 
SELECT select_query
```

**Parámetros**

En la tabla siguiente se explican los parámetros necesarios para el comando `INSERT INTO`:

| Parámetro | Descripción |
|----------------|--------------------------------------------------------------------------------|
| `table_name` | El nombre de la tabla que se creó como parte del comando crear audiencia. |
| `select_query` | Una instrucción SELECT. La sintaxis de la consulta SELECT se encuentra en la sección consultas SELECT. |

{style="table-layout:auto"}

**Ejemplo:**

El siguiente ejemplo muestra cómo agregar perfiles a una audiencia existente con el comando `INSERT INTO`:

```sql
INSERT INTO Audience aud_test 
SELECT month FROM profile_dim_date LIMIT 10;
```

### Eliminar una audiencia (ELIMINAR AUDIENCIA) {#delete-audience}

Utilice el comando `DROP AUDIENCE` para eliminar una audiencia existente. Si la audiencia no existe, se produce una excepción a menos que se especifique `IF EXISTS`.

```sql
DROP AUDIENCE [IF EXISTS] [db_name.]table_name
```

**Parámetros**

La tabla contiene los parámetros necesarios para el comando `DROP AUDIENCE`:

| Parámetro | Descripción |
|----------------|----------------------------------------------------------------------------------------|
| `IF EXISTS` | Opcional. Si se especifica, en el caso de que no se encuentre la tabla, no se generará ninguna excepción. |
| `db_name` | Especifica el grupo de datos utilizado para calificar el conjunto de datos de audiencia. |
| `table_name` | El nombre de la tabla que se creó como parte del comando crear audiencia. |

{style="table-layout:auto"}

**Ejemplo:**

El siguiente ejemplo muestra cómo eliminar una audiencia mediante el comando DROP AUDIENCE:

```sql
DROP AUDIENCE IF EXISTS aud_test;
```

### Publicación automática de audiencias {#auto-publish-audiences}

Las audiencias creadas con la extensión SQL se registran automáticamente en Distiller de datos en el espacio de trabajo de Audiencias. Una vez registradas, estas audiencias están disponibles para la segmentación y se pueden utilizar en destinos basados en archivos, lo que mejora las estrategias de segmentación y determinación de objetivos.

![El espacio de trabajo de audiencias en Adobe Experience Platform, que muestra las audiencias de Data Distiller publicadas automáticamente y listas para usarse.](../images/data-distiller/sql-audiences/audiences.png)

## Activar audiencias en destinos {#activate-audiences}

Active las audiencias segmentándolas a cualquier destino basado en archivos, como [!DNL Amazon S3], [!DNL SFTP] o [!DNL Azure Blob]. Los atributos de audiencia enriquecidos están disponibles para un mayor refinamiento y filtrado, según sea necesario.

![Diagrama de flujo de los tipos de destinos de Adobe Experience Platform que muestran destinos públicos, privados o personalizados, incluidas las opciones de transmisión por lotes y streaming.](../images/data-distiller/sql-audiences/destination-types.png)

## Aclaraciones de características {#faqs}

Esta sección aborda las preguntas más frecuentes sobre la creación y administración de audiencias externas mediante SQL en Data Distiller.

**Preguntas**:

- ¿La creación de audiencias solo se admite para conjuntos de datos planos?

+++Respuesta

Actualmente, la creación de audiencias se limita a atributos planos (de nivel raíz) al definir la audiencia.

+++

- ¿La creación de audiencias resulta en un único conjunto de datos o en varios conjuntos de datos, o varía según la configuración?

+++Respuesta

Hay una asignación uno a uno entre una audiencia y un conjunto de datos.

+++

- ¿El conjunto de datos creado durante la creación de audiencias está marcado para Perfil?

+++Respuesta

No, el conjunto de datos creado durante la creación de audiencias no está marcado para Perfil.

+++

- ¿Se crea el conjunto de datos en el lago de datos?

+++Respuesta

Sí, el conjunto de datos asociado con la audiencia se crea en el lago de datos. Los atributos de este conjunto de datos están disponibles en el Compositor de audiencias y en el flujo de destino como atributos enriquecidos.

+++

- ¿Los atributos de la audiencia están restringidos a destinos basados en archivos por lotes de empresa? (Sí o No)

+++Respuesta

No. Los atributos enriquecidos en la audiencia están disponibles para su uso tanto en destinos por lotes de empresa como basados en archivos. Si aparece un error como &quot;Los siguientes ID de segmento tienen áreas de nombres no permitidas para este destino: e917f626-a038-42f7-944c-xyxyx&quot;, cree un nuevo segmento en Data Distiller y utilícelo con cualquier destino disponible.

+++

- ¿Puedo crear una audiencia de audiencias que use una audiencia de Data Distiller?

+++Respuesta

Sí, puede crear una audiencia de audiencias que utilice una audiencia de Data Distiller.

+++

- ¿Aparecen estas audiencias en Adobe Journey Optimizer? Si no es así, ¿qué sucede cuando se crea una nueva audiencia en el generador de reglas que incluye a todos los miembros de esta audiencia?

+++Respuesta

Las audiencias del destilador de datos no están disponibles actualmente en Adobe Journey Optimizer. Debe crear una nueva audiencia en el generador de reglas de Adobe Journey Optimizer para que esté disponible en Adobe Journey Optimizer.

+++

- ¿Las audiencias de Data Distiller se eliminan cada 30 días, ya que son audiencias externas?

+++Respuesta

Sí, las audiencias de Data Distiller se eliminan cada 30 días, ya que son audiencias externas.

+++

## Pasos siguientes

Después de leer este documento, ha aprendido a utilizar la extensión de audiencia SQL en Data Distiller para crear, administrar y publicar audiencias de forma eficaz mediante comandos SQL. Ahora puede personalizar las definiciones de audiencias en función de sus requisitos empresariales únicos y activarlas en varios destinos, optimizando las estrategias de marketing y las decisiones basadas en datos.

A continuación, puede leer la siguiente documentación para desarrollar y optimizar aún más sus estrategias de gestión de público de Platform:

- **Explorar la evaluación de audiencias**: Obtenga información acerca de los [métodos de evaluación de audiencias en Adobe Experience Platform](../../segmentation/home.md#evaluate-segments): segmentación de streaming para actualizaciones en tiempo real, segmentación por lotes para procesamiento programado o bajo demanda y segmentación de Edge para evaluación instantánea en el Edge Network.
- **Integrar con destinos**: lea la guía sobre cómo [exportar archivos bajo demanda a destinos por lotes](../../destinations/ui/export-file-now.md) mediante la interfaz de usuario de destinos de Platform.
- **Revisar rendimiento de audiencias**: Analice el rendimiento de las audiencias definidas por SQL en diferentes canales. Utilice perspectivas de datos para ajustar y mejorar las definiciones de audiencia y las estrategias de segmentación. Lea el documento sobre [Información de la audiencia](../../dashboards/insights/audiences.md) para obtener información sobre cómo acceder y adaptar las consultas SQL para obtener información de la audiencia en Adobe Real-time Customer Data Platform. A continuación, puede crear sus propias perspectivas y transformar los datos sin procesar en información procesable personalizando el panel Audiencias para visualizar y utilizar de forma eficaz estas perspectivas y mejorar la toma de decisiones.
