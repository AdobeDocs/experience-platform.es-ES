---
solution: Experience Platform
title: Explorar y procesar conjuntos de datos sin procesar que alimentan los tableros del Experience Platform
type: Documentation
description: Aprenda a utilizar el servicio de consulta para explorar y procesar conjuntos de datos sin procesar que alimentan los paneles de perfil, segmento y destino en Experience Platform.
source-git-commit: 743367431144e9714a967b0340c755bf2120559c
workflow-type: tm+mt
source-wordcount: '592'
ht-degree: 1%

---


# Explorar, verificar y procesar conjuntos de datos de tablero mediante el servicio de consulta

Adobe Experience Platform proporciona información importante sobre los datos de perfil, segmento y destino de su organización a través de los paneles disponibles en la interfaz de usuario del Experience Platform. A continuación, puede utilizar el servicio de consulta de Adobe Experience Platform para explorar, verificar y procesar los conjuntos de datos sin procesar que alimentan estos paneles en el lago de datos.

## Introducción a Query Service

El servicio de consulta de Adobe Experience Platform permite a los especialistas en marketing obtener perspectivas de sus datos mediante el uso de SQL estándar para consultar datos en el lago de datos. El servicio de consulta ofrece una interfaz de usuario y una API que se pueden usar para unirse a cualquier conjunto de datos en el lago de datos y capturar los resultados de la consulta como nuevos conjuntos de datos para su uso en sistemas de informes, aprendizaje automático o para su incorporación al Perfil del cliente en tiempo real.

Para obtener más información sobre el servicio de consulta y su función dentro de Experience Platform, comience leyendo la [información general del servicio de consulta](../query-service/home.md).

## Conjuntos de datos disponibles

Puede utilizar el servicio de consulta para consultar conjuntos de datos sin procesar en tableros de perfil, segmentos y destinos. Las secciones siguientes describen los conjuntos de datos sin procesar que se pueden encontrar en el lago de datos.

### Conjuntos de datos de atributos de perfil

Por cada política de combinación activa en el Perfil del cliente en tiempo real, hay un conjunto de datos de atributos de perfil disponible en el lago de datos.

La convención de nomenclatura de este conjunto de datos es **Atributo de perfil** seguida de un valor numérico alfa. Por ejemplo: `Profile Attribute 14adf268-2a20-4dee-bee6-a6b0e34616a9`

Para comprender el esquema completo del conjunto de datos, puede obtener una vista previa del esquema y explorarlo con el visor de conjuntos de datos en la interfaz de usuario del Experience Platform.

### Conjunto de datos de metadatos de segmentos

Hay un conjunto de datos de metadatos de segmento disponible en el lago de datos para cada segmento de su organización.

La convención de nomenclatura de este conjunto de datos es **Definición de segmento de perfil** seguida de un valor numérico alfa. Por ejemplo: `Profile Segment Definition 6591ba8f-1422-499d-822a-543b2f7613a3`

La siguiente imagen muestra el esquema del conjunto de datos de metadatos del segmento.

![](images/query/segment-metadata.png)

### Conjunto de datos de metadatos de destino

Los metadatos de los destinos activados están disponibles como un conjunto de datos sin procesar en el lago de datos.

La convención de nomenclatura de este conjunto de datos es **DIM_Destination**.

La siguiente imagen muestra el esquema del conjunto de datos de metadatos de destino.

![](images/query/destinations-metadata.png)

## Consultas de ejemplo

Las siguientes consultas de ejemplo incluyen SQL de muestra que se puede utilizar en el servicio de consulta para explorar, verificar y procesar los conjuntos de datos sin procesar que alimentan los paneles.

### Recuento de perfiles por identidad

Esta perspectiva de perfil proporciona un desglose de identidades en todos los perfiles combinados del conjunto de datos. El número total de perfiles por identidad (es decir, sumando los valores mostrados para cada área de nombres) puede ser mayor que el número total de perfiles combinados, ya que un perfil podría tener varias áreas de nombres asociadas. Por ejemplo, si un cliente interactúa con la marca en más de un canal, se asociarán varias áreas de nombres con ese cliente individual.

**Consulta**

```sql
Select
        Key namespace,
        count(1) count_of_profiles
     from
        (
           Select
               explode(identitymap)
           from
              profile_attribute_14adf268-2a20-4dee-bee6-a6b0e34616a9
        )
     group by
        namespace;
```

### Recuento de perfiles por segmento

Esta perspectiva de audiencia proporciona la cantidad total de perfiles combinados dentro de cada segmento en el conjunto de datos. Este número es el resultado de aplicar la política de combinación de segmentos a los datos de perfil para combinar fragmentos de perfil y formar un único perfil para cada individuo en el segmento.

```sql
Select          
        concat_ws('-', key, source_namespace) segment_id,
        count(1) count_of_profiles
      from
        (
            Select
              Upper(key) as source_namespace,
              explode(value)
            from
              (
                  Select
                    explode(Segmentmembership)
                  from
                    profile_attribute_14adf268-2a20-4dee-bee6-a6b0e34616a9
              )
        )
      group by
      segment_id
```

### Recuento de segmentos activados por destino para todos los destinos

## Pasos siguientes

Al leer esta guía, ahora puede utilizar el servicio de consulta para realizar varias consultas con el fin de explorar y procesar los conjuntos de datos sin procesar que alimentan los paneles de perfil, segmento y destinos.

Para obtener más información sobre cada tablero y sus métricas, seleccione un tablero de la lista de tableros disponibles en la navegación de documentación.
