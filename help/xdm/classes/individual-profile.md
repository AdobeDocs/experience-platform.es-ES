---
keywords: Experience Platform;inicio;temas populares;esquema;esquema;XDM;perfil individual;campos;esquemas;esquemas;mapa de identidad;mapa de identidad;mapa de identidad;diseño de esquema;mapa;mapa;esquema de unión;unión
solution: Experience Platform
title: Clase de perfil individual XDM
topic-legacy: overview
description: Este documento proporciona información general sobre la clase XDM Individual Profile.
exl-id: 83b22462-79ce-4024-aa50-a9bd800c0f81
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '375'
ht-degree: 0%

---

# [!DNL XDM Individual Profile] class

[!DNL XDM Individual Profile] es una clase XDM estándar que forma una representación singular (o &quot;perfil&quot;) de los atributos y los intereses de personas identificadas y parcialmente identificadas.

Los perfiles pueden abarcar desde señales de comportamiento anónimas (como cookies de navegador) hasta perfiles altamente identificados que contienen información detallada como nombre, fecha de nacimiento, ubicación y dirección de correo electrónico. A medida que un perfil crece, se convierte en un sólido repositorio de información personal, identidades, detalles de contacto y preferencias de comunicación para un individuo. Para obtener más información de alto nivel sobre el uso de esta clase en el ecosistema de Platform, consulte la [información general de XDM](../home.md#data-behaviors).

La propia clase [!DNL XDM Individual Profile] proporciona varios valores generados por el sistema que se rellenan automáticamente cuando se introducen datos, mientras que todos los demás campos deben añadirse mediante el uso de [mezclas compatibles](#mixins):

![](../images/classes/individual-profile.png)

| Propiedad | Descripción |
| --- | --- |
| `_repo` | Un objeto que contiene los siguientes campos [!UICONTROL DateTime]: <ul><li>`createDate`: La fecha y la hora en que se creó el recurso en el almacén de datos, como cuando se introdujeron por primera vez los datos.</li><li>`modifyDate`: Fecha y hora de la última modificación del recurso.</li></ul> |
| `_id` | Identificador de cadena único generado por el sistema para el registro. Este campo se utiliza para rastrear la exclusividad de un registro individual, evitar la duplicación de datos y buscar ese registro en servicios descendentes. Dado que este campo se genera a partir del sistema, no se debe proporcionar un valor explícito durante el consumo de datos.<br><br>Es importante distinguir que este campo  **no** presenta una identidad relacionada con una persona individual, sino más bien el registro de los datos en sí. Los datos de identidad relacionados con una persona deben relegarse a [campos de identidad](../schema/composition.md#identity) en su lugar. |
| `createdByBatchID` | El ID del lote ingestado que provocó que se creara el registro. |
| `modifiedByBatchID` | ID del último lote ingestado que provocó que se actualizara el registro. |
| `repositoryCreatedBy` | ID del usuario que creó el registro. |
| `repositoryLastModifiedBy` | El ID del usuario que modificó el registro por última vez. |

## Mezclas compatibles {#mixins}

>[!NOTE]
>
>Los nombres de varias mezclas han cambiado. Consulte el documento sobre [mezcin name updates](../mixins/name-updates.md) para obtener más información.

El Adobe proporciona varias mezclas estándar para su uso con la clase [!DNL XDM Individual Profile]. La siguiente es una lista de las mezclas más utilizadas para la clase:

* [[!UICONTROL IdentityMap]](../mixins/profile/identitymap.md)
* [[!UICONTROL Demographic Details]](../mixins/profile/person-details.md)
* [[!UICONTROL Personal Contact Details]](../mixins/profile/personal-details.md)
* [[!UICONTROL Work Contact Details]](../mixins/profile/work-details.md)
* [[!UICONTROL Segment Membership Details]](../mixins/profile/segmentation.md)
