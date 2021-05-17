---
solution: Experience Platform
title: Clase de definición de segmento
topic-legacy: overview
description: Este documento proporciona información general sobre la clase de definición de segmentos en el Modelo de datos de experiencia (XDM).
exl-id: c0f7b04c-2266-4d08-89a1-67ba758a51a7
source-git-commit: 632ea4e2a94bfcad098a5fc5a5ed8985c0f41e0e
workflow-type: tm+mt
source-wordcount: '374'
ht-degree: 0%

---

# [!UICONTROL Segment ] definitionclass

&quot;[!UICONTROL Definición de segmento]&quot; es una clase estándar del Modelo de datos de experiencia (XDM) que captura los detalles de una definición de segmento. La clase incluye campos obligatorios, como el ID y el nombre de un segmento, junto con otros atributos opcionales. Esta clase debe usarse si introduce definiciones de segmentos de sistemas externos en Adobe Experience Platform.

>[!NOTE]
>
>Esta clase solo debe utilizarse para capturar información sobre las definiciones de segmentos en sí. Para capturar la información de pertenencia a segmentos dentro de los datos de perfil, debe utilizar el grupo de campos [Detalles de pertenencia a segmentos](../field-groups/profile/segmentation.md) en el esquema [!UICONTROL XDM Individual Profile].

![](../images/classes/segment-definition.png)

| Propiedad | Descripción |
| --- | --- |
| `_repo` | Un objeto que contiene los siguientes campos [!UICONTROL DateTime]: <ul><li>`createDate`: La fecha y la hora en que se creó el recurso en el almacén de datos, como cuando se introdujeron por primera vez los datos.</li><li>`modifyDate`: Fecha y hora de la última modificación del recurso.</li></ul> |
| `_id` | Identificador de cadena único generado por el sistema para el registro. Este campo se utiliza para rastrear la exclusividad de un registro individual, evitar la duplicación de datos y buscar ese registro en servicios descendentes.<br><br>Dado que este campo se genera a partir del sistema, no se proporciona un valor explícito durante el consumo de datos. Sin embargo, puede optar por proporcionar sus propios valores de ID únicos si lo desea.<br><br>Es importante distinguir que este campo  **no** presenta una identidad relacionada con una persona individual, sino más bien el registro de los datos en sí. Los datos de identidad relacionados con una persona deben relegarse a [campos de identidad](../schema/composition.md#identity) en su lugar. |
| `createdByBatchID` | El ID del lote ingestado que provocó que se creara el registro. |
| `description` | Descripción de la definición del segmento. |
| `identityMap` | Campo de mapa que contiene un conjunto de identidades con espacio de nombres para las personas a las que se aplica el segmento. Consulte la sección sobre mapas de identidad en [conceptos básicos de la composición de esquema](../schema/composition.md#identityMap) para obtener más información sobre su caso de uso. |
| `modifiedByBatchID` | ID del último lote ingestado que provocó que se actualizara el registro. |
| `repositoryCreatedBy` | ID del usuario que creó el registro. |
| `repositoryLastModifiedBy` | El ID del usuario que modificó el registro por última vez. |
| `segmentName` | **(Obligatorio)** Un nombre para la definición del segmento. |
| `segmentStatus` | Estado del segmento desde el sistema externo. Se aceptan los siguientes valores: <ul><li>`ACTIVE`</li><li>`INACTIVE`</li><li>`DELETED`</li><li>`DRAFT`</li><li>`REVOKED`</li></ul> |
| `version` | El número de versión más reciente de la definición del segmento. |
