---
solution: Experience Platform
title: Clase de definición de segmento
description: Obtenga información acerca de la clase de definición de segmento en el Modelo de datos de experiencia (XDM).
exl-id: c0f7b04c-2266-4d08-89a1-67ba758a51a7
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '370'
ht-degree: 1%

---

# clase [!UICONTROL Segment definition]

&quot;[!UICONTROL Segment definition]&quot; es una clase de modelo de datos de experiencia (XDM) estándar que captura los detalles de una definición de segmento. La clase incluye campos obligatorios, como el ID y el nombre de una audiencia, junto con otros atributos opcionales. Esta clase debe utilizarse si va a introducir definiciones de segmentos de sistemas externos en Adobe Experience Platform.

>[!NOTE]
>
>Esta clase solo debe utilizarse para recopilar información sobre las propias definiciones de segmentos. Para capturar la información de pertenencia a audiencias dentro de los datos de perfil, debe usar el grupo de campos [Detalles de pertenencia a segmento](../field-groups/profile/segmentation.md) en su esquema [!UICONTROL XDM Individual Profile].

![](../images/classes/segment-definition.png)

| Propiedad | Descripción |
| --- | --- |
| `_repo` | Objeto que contiene los [!UICONTROL campos DateTime] siguientes: <ul><li>`createDate`: la fecha y hora en que se creó el recurso en el almacén de datos, como cuándo se ingerieron los datos por primera vez.</li><li>`modifyDate`: la fecha y la hora en que se modificó el recurso por última vez.</li></ul> |
| `_id` | Un identificador de cadena único generado por el sistema para el registro. Este campo se utiliza para realizar un seguimiento de la exclusividad de un registro individual, evitar la duplicación de datos y buscar ese registro en servicios descendentes.<br><br>Dado que este campo es generado por el sistema, no se le proporciona un valor explícito durante la ingesta de datos. Sin embargo, puede optar por proporcionar sus propios valores de ID únicos si lo desea.<br><br>Es importante distinguir que este campo **no** representa una identidad relacionada con una persona individual, sino más bien el registro de datos en sí. Los datos de identidad relacionados con una persona deben relegarse a [campos de identidad](../schema/composition.md#identity). |
| `createdByBatchID` | El ID del lote ingerido que provocó la creación del registro. |
| `description` | Una descripción para la definición del segmento. |
| `identityMap` | Campo de asignación que contiene un conjunto de identidades con espacio de nombres para las personas a las que se aplica la audiencia. Consulte la sección sobre mapas de identidad en los [conceptos básicos de la composición de esquemas](../schema/composition.md#identityMap) para obtener más información sobre su caso de uso. |
| `modifiedByBatchID` | El ID del último lote ingerido que provocó que se actualizara el registro. |
| `repositoryCreatedBy` | El ID del usuario que creó el registro. |
| `repositoryLastModifiedBy` | El ID del usuario que modificó el registro por última vez. |
| `segmentName` | **(Obligatorio)** Un nombre para la definición del segmento. |
| `segmentStatus` | El estado de la audiencia del sistema externo. Se aceptan los siguientes valores: <ul><li>`ACTIVE`</li><li>`INACTIVE`</li><li>`DELETED`</li><li>`DRAFT`</li><li>`REVOKED`</li></ul> |
| `version` | Número de versión más reciente de la definición del segmento. |

{style="table-layout:auto"}
