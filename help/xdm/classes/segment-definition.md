---
solution: Experience Platform
title: Clase de definición de segmento
topic-legacy: overview
description: Este documento proporciona información general sobre la clase de definición de segmentos en el Modelo de datos de experiencia (XDM).
exl-id: c0f7b04c-2266-4d08-89a1-67ba758a51a7
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '378'
ht-degree: 0%

---

# [!UICONTROL Segment definition] class

&quot;[!UICONTROL Segment definition]&quot; es una clase estándar del Modelo de datos de experiencia (XDM) que captura los detalles de una definición de segmento. La clase incluye campos obligatorios, como el ID y el nombre de un segmento, junto con otros atributos opcionales. Esta clase debe usarse si introduce definiciones de segmentos de sistemas externos en Adobe Experience Platform.

>[!NOTE]
>
>Esta clase solo debe utilizarse para capturar información sobre las definiciones de segmentos en sí. Para capturar la información de pertenencia a segmentos dentro de los datos de perfil, debe utilizar la [mezcla de Detalles de pertenencia a segmentos](../mixins/profile/segmentation.md) en su esquema [!UICONTROL XDM Individual Profile].

![](../images/classes/segment-definition.png)

| Propiedad | Descripción |
| --- | --- |
| `_repo` | Un objeto que contiene los siguientes campos [!UICONTROL DateTime]: <ul><li>`createDate`: La fecha y la hora en que se creó el recurso en el almacén de datos, como cuando se introdujeron por primera vez los datos.</li><li>`modifyDate`: Fecha y hora de la última modificación del recurso.</li></ul> |
| `_id` | Identificador de cadena único generado por el sistema para el registro. Este campo se utiliza para rastrear la exclusividad de un registro individual, evitar la duplicación de datos y buscar ese registro en servicios descendentes.<br><br>Dado que este campo se genera a partir del sistema, no se proporciona un valor explícito durante el consumo de datos. Sin embargo, puede optar por proporcionar sus propios valores de ID únicos si lo desea.<br><br>Es importante distinguir que este campo  **no** presenta una identidad relacionada con una persona individual, sino más bien el registro de los datos en sí. Los datos de identidad relacionados con una persona deben relegarse a [campos de identidad](../schema/composition.md#identity) en su lugar. |
| `createdByBatchID` | El ID del lote ingestado que provocó que se creara el registro. |
| `description` | Descripción de la definición del segmento. |
| `identityMap` | Campo de mapa que contiene un conjunto de identidades con espacio de nombres para las personas a las que se aplica el segmento. El sistema actualiza automáticamente este campo a medida que se incorporan los datos de identidad.<br /><br />Consulte la sección sobre mapas de identidad en los  [conceptos básicos de la ](../schema/composition.md#identityMap) composición de esquemas para obtener más información sobre su caso de uso. |
| `modifiedByBatchID` | ID del último lote ingestado que provocó que se actualizara el registro. |
| `repositoryCreatedBy` | ID del usuario que creó el registro. |
| `repositoryLastModifiedBy` | El ID del usuario que modificó el registro por última vez. |
| `segmentName` | **(Obligatorio)** Un nombre para la definición del segmento. |
| `segmentStatus` | Estado del segmento desde el sistema externo. Se aceptan los siguientes valores: <ul><li>`ACTIVE`</li><li>`INACTIVE`</li><li>`DELETED`</li><li>`DRAFT`</li><li>`REVOKED`</li></ul> |
| `version` | El número de versión más reciente de la definición del segmento. |
