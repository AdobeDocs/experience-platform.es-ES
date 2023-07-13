---
solution: Experience Platform
title: Explorar, comprobar y procesar conjuntos de datos del panel mediante el servicio de consultas
type: Documentation
description: Aprenda a utilizar el servicio de consultas para explorar y procesar conjuntos de datos sin procesar y activar paneles de perfil, audiencia y destino en Experience Platform.
exl-id: 0087dcab-d5fe-4a24-85f6-587e9ae74fb8
source-git-commit: 79966442f5333363216da17342092a71335a14f0
workflow-type: tm+mt
source-wordcount: '964'
ht-degree: 0%

---

# Explorar, comprobar y procesar conjuntos de datos de tableros mediante [!DNL Query Service]

Adobe Experience Platform proporciona información importante sobre los datos de perfil, audiencia y destinos de su organización a través de los paneles disponibles en la interfaz de usuario de Experience Platform. A continuación, puede utilizar Adobe Experience Platform [!DNL Query Service] para explorar, verificar y procesar los conjuntos de datos sin procesar que alimentan estos paneles en el lago de datos.

## Introducción a [!DNL Query Service]

Adobe Experience Platform [!DNL Query Service] admite que los especialistas en marketing obtengan información de sus datos permitiendo el uso de SQL estándar para consultar datos en el lago de datos. [!DNL Query Service] ofrece una interfaz de usuario y una API que se pueden utilizar para unirse a cualquier conjunto de datos del lago de datos y capturar los resultados de la consulta como nuevos conjuntos de datos para utilizarlos en el sistema de informes, el aprendizaje automático o para incluirlos en el Perfil del cliente en tiempo real.

Para obtener más información acerca de [!DNL Query Service] y su función dentro del Experience Platform, comience por leer el [[!DNL Query Service] descripción general](../query-service/home.md).

## Acceso a conjuntos de datos disponibles

Puede utilizar [!DNL Query Service] para consultar conjuntos de datos sin procesar paneles de perfil, audiencia y destinos. Para ver los conjuntos de datos disponibles, en la interfaz de usuario del Experience Platform, seleccione **Conjuntos de datos** en el panel de navegación izquierdo para abrir el panel Conjuntos de datos. El panel enumera todos los conjuntos de datos disponibles para su organización. Se muestran los detalles de cada conjunto de datos enumerado, incluido su nombre, el esquema al que se adhiere y el estado de la ejecución de la ingesta más reciente.

![El panel Examinar conjunto de datos con la pestaña Conjuntos de datos resaltada en el panel de navegación izquierdo.](./images/query/browse-datasets.png)

### Conjuntos de datos generados por el sistema

>[!IMPORTANT]
>
>Los conjuntos de datos generados por el sistema están ocultos de forma predeterminada. De forma predeterminada, la variable [!UICONTROL Examinar] La pestaña solo muestra los conjuntos de datos en los que ha introducido datos.

Para ver los conjuntos de datos generados por el sistema, seleccione el icono de filtro (![Un icono de filtro.](./images/query/filter.png)), situado a la izquierda de la barra de búsqueda.

![La pestaña Examinar conjuntos de datos con el icono de filtro resaltado.](./images/query/filter-datasets.png)

Aparecerá una barra lateral que contiene dos conmutadores, [!UICONTROL Incluido en el perfil] y [!UICONTROL Mostrar conjuntos de datos del sistema]. Seleccione la opción para [!UICONTROL Mostrar conjuntos de datos del sistema] para incluir conjuntos de datos generados por el sistema en la lista explorable de conjuntos de datos.

![La pestaña Examinar conjuntos de datos con la opción Mostrar conjuntos de datos del sistema resaltada.](./images/query/show-system-datasets.png)

### Conjuntos de datos de atributos de perfil

La información del panel de perfil está vinculada a las políticas de combinación definidas por su organización. Por cada política de combinación activa, hay un conjunto de datos de atributos de perfil disponible en el lago de datos.

La convención de nombres de estos conjuntos de datos es **Profile-Snapshot-Export** seguido de un valor alfanumérico aleatorio generado por el sistema. Por ejemplo: `Profile-Snapshot-Export-abbc7093-80f4-4b49-b96e-e743397d763f`.

Para comprender el esquema completo de cada conjunto de datos de exportación de instantáneas de perfil, puede obtener una vista previa y explorar los conjuntos de datos [uso del visor de conjuntos de datos](../catalog/datasets/user-guide.md) en la interfaz de usuario de Experience Platform.

![Vista previa del conjunto de datos de exportación de instantáneas de perfil.](images/query/profile-attribute.png)

#### Asignación de conjuntos de datos de atributos de perfil para combinar ID de políticas

El valor alfanumérico asignado a cada conjunto de datos de atributos de perfil generado por el sistema es una cadena aleatoria que se asigna a un ID de política de combinación de una de las políticas de combinación creadas por su organización. La asignación de cada ID de política de combinación a su cadena de conjunto de datos de atributos de perfil relacionada se mantiene en `adwh_dim_merge_policies` conjunto de datos.

El `adwh_dim_merge_policies` dataset contiene los campos siguientes:

* `merge_policy_name`
* `merge_policy_id`
* `merge_policy`
* `dataset_id`

Este conjunto de datos se puede explorar mediante la interfaz de usuario del Editor de consultas en Experience Platform. Para obtener más información sobre el uso del Editor de consultas, consulte la [Guía de IU del Editor de consultas](../query-service/ui/user-guide.md).

### Conjunto de datos de metadatos de audiencia

Hay un conjunto de datos de metadatos de audiencia disponible en el lago de datos que contiene metadatos para cada una de las audiencias de la organización.

La convención de nombres de este conjunto de datos es **Segmentdefinition-Snapshot-Export** seguido de un valor alfanumérico. Por ejemplo: `Segmentdefinition-Snapshot-Export-acf28952-2b6c-47ed-8f7f-016ac3c6b4e7`

Para comprender el esquema completo de cada conjunto de datos de exportación de instantáneas de definición de segmento, puede obtener una vista previa y explorar los conjuntos de datos [uso del visor de conjuntos de datos](../catalog/datasets/user-guide.md) en la interfaz de usuario de Experience Platform.

### Conjunto de datos de metadatos de destino

Los metadatos de todos los destinos activados de su organización están disponibles como un conjunto de datos sin procesar en el lago de datos.

La convención de nombres de este conjunto de datos es **DIM_Destination**.

Para comprender el esquema completo del conjunto de datos de destino DIM, puede obtener una vista previa y explorar el conjunto de datos [uso del visor de conjuntos de datos](../catalog/datasets/user-guide.md) en la interfaz de usuario de Experience Platform.

![Vista previa del conjunto de datos DIM_Destination.](images/query/destinations-metadata.png)

## (Beta) Informes de perspectivas de la plataforma de datos del cliente (CDP)

>[!IMPORTANT]
>
>La función de modelos de datos de perspectivas de CDP está en versión beta. Sus funciones y documentación están sujetas a cambios.

La función de modelos de datos de perspectivas de CDP expone el SQL que alimenta las perspectivas para varios widgets de perfil, destino y segmentación. Puede personalizar estas plantillas de consulta SQL para crear informes CDP para sus casos de uso de KPI y marketing.

Los informes de CDP proporcionan perspectivas sobre los datos de perfil y su relación con las audiencias y los destinos. Consulte la documentación del modelo de datos de perspectivas de CDP para obtener información detallada sobre cómo [aplique los modelos de datos de perspectivas de CDP a sus casos de uso de KPI particulares](./cdp-insights-data-model.md).

## Consultas de ejemplo

Las siguientes consultas de ejemplo incluyen SQL de ejemplo que se puede utilizar en [!DNL Query Service] para explorar, verificar y procesar los conjuntos de datos sin procesar que alimentan los paneles.

### Recuento de perfiles por identidad

Esta perspectiva de perfil proporciona un desglose de identidades en todos los perfiles combinados del conjunto de datos.

>[!NOTE]
>
>El número total de perfiles por identidad (es decir, sumando los valores mostrados para cada área de nombres) puede ser mayor que el número total de perfiles combinados, ya que un perfil podría tener varias áreas de nombres asociadas. Por ejemplo, si un cliente interactúa con su marca en más de un canal, se asociarán varias áreas de nombres a ese cliente individual.

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

### Recuento de perfiles por audiencia

Esta perspectiva de audiencia proporciona el número total de perfiles combinados dentro de cada audiencia en el conjunto de datos. Este número es el resultado de aplicar la política de combinación de audiencias a los datos del perfil para combinar fragmentos de perfil y formar un único perfil para cada individuo en la audiencia.

```sql
Select          
        concat_ws('-', key, source_namespace) audience_id,
        count(1) count_of_profiles
      from
        (
            Select
              Upper(key) as source_namespace,
              explode(value)
            from
              (
                  Select
                    explode(Audiencemembership)
                  from
                    Profile-Snapshot-Export-abbc7093-80f4-4b49-b96e-e743397d763f
              )
        )
      group by
      audience_id
```

## Pasos siguientes

Al leer esta guía, ahora puede utilizar [!DNL Query Service] para realizar varias consultas para explorar y procesar los conjuntos de datos sin procesar y alimentar los paneles de perfil, audiencia y destinos.

Para obtener más información acerca de cada panel y sus métricas, seleccione un panel de la lista de paneles disponibles en la navegación de la documentación.
