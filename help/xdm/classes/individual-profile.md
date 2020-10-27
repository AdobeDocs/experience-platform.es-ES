---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;individual profile;fields;schemas;Schemas;identityMap;identity map;Identity map;Schema design;map;Map;union schema;union
solution: Experience Platform
title: Clase de Perfil individual XDM
topic: overview
description: Este documento proporciona información general sobre la clase de Perfil individual XDM.
translation-type: tm+mt
source-git-commit: f9d8021643e72e3fbb5315b54a19815dcdaaa702
workflow-type: tm+mt
source-wordcount: '363'
ht-degree: 0%

---


# [!DNL XDM Individual Profile] clase

[!DNL XDM Individual Profile] es una clase XDM estándar que forma una representación única (o &quot;perfil&quot;) de los atributos e intereses de las personas identificadas y parcialmente identificadas.

Los perfiles pueden abarcar desde señales conductuales anónimas (como cookies del navegador) hasta perfiles altamente identificados que contienen información detallada como nombre, fecha de nacimiento, ubicación y dirección de correo electrónico. A medida que un perfil crece, se convierte en un sólido repositorio de información personal, identidades, detalles de contacto y preferencias de comunicación para un individuo. Para obtener más información de alto nivel sobre el uso de esta clase en el ecosistema de la Plataforma, consulte la descripción general [de](../home.md#data-behaviors)XDM.

La [!DNL XDM Individual Profile] clase misma proporciona varios valores generados por el sistema que se rellenan automáticamente al ingerir datos, mientras que todos los demás campos deben agregarse mediante mezclas [](#mixins)compatibles:

![](../images/classes/individual-profile.png)

| Propiedad | Descripción |
| --- | --- |
| `_repo` | Objeto que contiene los siguientes campos [!UICONTROL de DateTime] : <ul><li>`createDate`:: La fecha y hora en que se creó el recurso en el almacén de datos, como por ejemplo, la primera vez que se ingirieron datos.</li><li>`modifyDate`:: Fecha y hora en que se modificó el recurso por última vez.</li></ul> |
| `_id` | Identificador de cadena único generado por el sistema para el registro. Este campo se utiliza para rastrear la singularidad de un registro individual, evitar la duplicación de datos y buscar ese registro en los servicios de flujo descendente. Dado que este campo es generado por el sistema, no debe proporcionarse un valor explícito durante la ingestión de datos.<br><br>Es importante distinguir que este campo **no** representa una identidad relacionada con una persona individual, sino más bien el propio registro de datos. Los datos de identidad relativos a una persona deben relegarse a campos [de](../schema/composition.md#identity) identidad. |
| `createdByBatchID` | ID del lote ingestado que provocó la creación del registro. |
| `modifiedByBatchID` | ID del último lote ingestado que provocó la actualización del registro. |
| `repositoryCreatedBy` | ID del usuario que creó el registro. |
| `repositoryLastModifiedBy` | ID del usuario que modificó el registro por última vez. |

## Mezclas compatibles {#mixins}

>[!NOTE]
>
>Los nombres de varias mezclas han cambiado. Consulte el documento sobre las actualizaciones [de nombres de](../mixins/name-updates.md) mezcla para obtener más información.

Adobe proporciona varias mezclas estándar para su uso con la [!DNL XDM Individual Profile] clase. A continuación se presenta una lista de las mezclas más utilizadas para la clase:

* [[!UICONTROL IdentityMap]](../mixins/profile/identitymap.md)
* [[!UICONTROL Detalles demográficos]](../mixins/profile/person-details.md)
* [[!UICONTROL Detalles de contacto personal]](../mixins/profile/personal-details.md)
* [[!UICONTROL Detalles de contacto de trabajo]](../mixins/profile/work-details.md)
* [[!UICONTROL Detalles de pertenencia a segmentos]](../mixins/profile/segmentation.md)