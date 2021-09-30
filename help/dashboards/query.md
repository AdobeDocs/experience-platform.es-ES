---
solution: Experience Platform
title: Explorar y procesar conjuntos de datos sin procesar que alimenten los tableros de la plataforma
type: Documentation
description: Aprenda a utilizar el servicio de consulta para explorar y procesar conjuntos de datos sin procesar que alimentan los paneles de perfil, segmento y destino en Experience Platform.
exl-id: 0087dcab-d5fe-4a24-85f6-587e9ae74fb8
source-git-commit: b9dd7584acc43b5946f8c0669d7a81001e44e702
workflow-type: tm+mt
source-wordcount: '738'
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

Las perspectivas del panel de perfiles están vinculadas a las políticas de combinación que su organización ha definido. Para cada directiva de combinación activa, hay un conjunto de datos de atributo de perfil disponible en el lago de datos.

La convención de nomenclatura de estos conjuntos de datos es **Profile-Snapshot-Export** seguida de un valor alfanumérico aleatorio generado por el sistema. Por ejemplo: `Profile-Snapshot-Export-abbc7093-80f4-4b49-b96e-e743397d763f`.

Para comprender el esquema completo de cada conjunto de datos de exportación de instantánea de perfil, puede obtener una vista previa y explorar los conjuntos de datos [utilizando el visor de conjuntos de datos](../catalog/datasets/user-guide.md) en la interfaz de usuario del Experience Platform.

![](images/query/profile-attribute.png)

#### Asignación de conjuntos de datos de atributos de perfil para combinar ID de directivas

Cada conjunto de datos de atributo de perfil se titula **Profile Snapshot Export** seguido de un valor numérico alfanumérico aleatorio generado por el sistema. Por ejemplo: `Profile-Snapshot-Export-abbc7093-80f4-4b49-b96e-e743397d763f`.

Este valor numérico alfa es una cadena aleatoria generada por el sistema que se asigna a un ID de política de combinación de una de las políticas de combinación creadas por su organización. La asignación de cada ID de directiva de combinación a su cadena de conjunto de datos de atributo de perfil relacionado se mantiene en el conjunto de datos `adwh_dim_merge_policies`.

El conjunto de datos `adwh_dim_merge_policies` contiene los siguientes campos:

* `merge_policy_name`
* `merge_policy_id`
* `merge_policy`
* `dataset_id`

Este conjunto de datos se puede explorar mediante la interfaz de usuario del Editor de consultas en Experience Platform. Para obtener más información sobre el uso del Editor de consultas, consulte la [guía de IU del Editor de consultas](../query-service/ui/user-guide.md).

### Conjunto de datos de metadatos de segmentos

Hay un conjunto de datos de metadatos de segmento disponible en el lago de datos que contiene metadatos para cada uno de los segmentos de su organización.

La convención de nomenclatura de este conjunto de datos es **Segmentdefinition-Snapshot-Export** seguida de un valor numérico alfa. Por ejemplo: `Segmentdefinition-Snapshot-Export-acf28952-2b6c-47ed-8f7f-016ac3c6b4e7`

Para comprender el esquema completo de cada conjunto de datos de exportación de instantánea de definición de segmento, puede obtener una vista previa y explorar los conjuntos de datos [utilizando el visor de conjuntos de datos](../catalog/datasets/user-guide.md) en la interfaz de usuario del Experience Platform.

![](images/query/segment-metadata.png)

### Conjunto de datos de metadatos de destino

Los metadatos de todos los destinos activados de su organización están disponibles como un conjunto de datos sin procesar en el lago de datos.

La convención de nomenclatura de este conjunto de datos es **DIM_Destination**.

Para comprender el esquema completo del conjunto de datos de destino DIM, puede obtener una vista previa y explorar el conjunto de datos [mediante el visor de conjuntos de datos](../catalog/datasets/user-guide.md) en la interfaz de usuario del Experience Platform.

![](images/query/destinations-metadata.png)

## Consultas de ejemplo

Las siguientes consultas de ejemplo incluyen SQL de muestra que se puede utilizar en el servicio de consulta para explorar, verificar y procesar los conjuntos de datos sin procesar que alimentan los paneles.

### Recuento de perfiles por identidad

Esta perspectiva de perfil proporciona un desglose de identidades en todos los perfiles combinados del conjunto de datos.

>[!NOTE]
>
>El número total de perfiles por identidad (es decir, sumando los valores mostrados para cada área de nombres) puede ser mayor que el número total de perfiles combinados, ya que un perfil podría tener varias áreas de nombres asociadas. Por ejemplo, si un cliente interactúa con la marca en más de un canal, se asociarán varias áreas de nombres con ese cliente individual.

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
              Profile-Snapshot-Export-abbc7093-80f4-4b49-b96e-e743397d763f
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
                    Profile-Snapshot-Export-abbc7093-80f4-4b49-b96e-e743397d763f
              )
        )
      group by
      segment_id
```

## Pasos siguientes

Al leer esta guía, ahora puede utilizar el servicio de consulta para realizar varias consultas con el fin de explorar y procesar los conjuntos de datos sin procesar que alimentan los paneles de perfil, segmento y destinos.

Para obtener más información sobre cada tablero y sus métricas, seleccione un tablero de la lista de tableros disponibles en la navegación de documentación.
