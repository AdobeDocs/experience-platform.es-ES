---
keywords: Experience Platform;inicio;temas populares;esquema;esquema;XDM;perfil individual;campos;esquemas;esquemas;mapa de identidad;mapa de identidad;mapa de identidad;diseño de esquema;mapa;mapa;esquema de unión;unión
solution: Experience Platform
title: Clase de perfil individual XDM
description: Este documento proporciona información general sobre la clase XDM Individual Profile.
exl-id: 83b22462-79ce-4024-aa50-a9bd800c0f81
source-git-commit: 983682489e2c0e70069dbf495ab90fc9555aae2d
workflow-type: tm+mt
source-wordcount: '598'
ht-degree: 1%

---

# [!DNL XDM Individual Profile] clase

[!DNL XDM Individual Profile] es una clase estándar de Experience Data Model (XDM) que forma una representación singular (o &quot;perfil&quot;) de una persona individual. Concretamente, la clase (y sus grupos de campos compatibles) captura los atributos y los intereses de las personas identificadas y parcialmente identificadas que interactúan con su marca.

Los perfiles pueden abarcar desde señales de comportamiento anónimas (como cookies de navegador) hasta perfiles altamente identificados que contienen información detallada como nombre, fecha de nacimiento, ubicación y dirección de correo electrónico. A medida que un perfil crece, se convierte en un sólido repositorio de información personal, identidades, detalles de contacto y preferencias de comunicación para un individuo. Para obtener más información de alto nivel sobre el uso de esta clase en el ecosistema de la Plataforma, consulte [Información general de XDM](../home.md#data-behaviors).

La variable [!DNL XDM Individual Profile] La propia clase proporciona varios valores generados por el sistema que se rellenan automáticamente cuando se introducen datos, mientras que los demás campos se deben agregar mediante el uso de [grupos de campos de esquema compatibles](#field-groups):

![](../images/classes/individual-profile.png)

| Propiedad | Descripción |
| --- | --- |
| `_repo` | Un objeto que contiene lo siguiente [!UICONTROL DateTime] campos: <ul><li>`createDate`: La fecha y la hora en que se creó el recurso en el almacén de datos, como cuando se introdujeron por primera vez los datos.</li><li>`modifyDate`: Fecha y hora de la última modificación del recurso.</li></ul> |
| `_id` | Identificador de cadena único para el registro. Este campo se utiliza para rastrear la exclusividad de un registro individual, evitar la duplicación de datos y buscar ese registro en servicios descendentes. En algunos casos, `_id` puede ser [Identificador único universal (UUID)](https://tools.ietf.org/html/rfc4122) o [Identificador único global (GUID)](https://docs.microsoft.com/en-us/dotnet/api/system.guid?view=net-5.0).<br><br>Si transmite datos desde una conexión de origen o realiza la ingesta directamente desde un archivo de parquet, debe generar este valor concatenando una combinación determinada de campos que hagan que el registro sea único, como un ID principal, una marca de tiempo, un tipo de registro, etc. El valor concatenado debe ser un `uri-reference` cadena con formato , lo que significa que se deben eliminar los caracteres de dos puntos. Después, el valor concatenado debe tener un cifrado hash con SHA-256 u otro algoritmo de su elección.<br><br>Es importante distinguir que **este campo no representa una identidad relacionada con una persona individual**, sino más bien el registro de los datos en sí. Los datos de identidad relacionados con una persona deben relegarse a [campos de identidad](../schema/composition.md#identity) proporcionado por grupos de campos compatibles en su lugar. |
| `createdByBatchID` | El ID del lote ingestado que provocó que se creara el registro. |
| `modifiedByBatchID` | ID del último lote ingestado que provocó que se actualizara el registro. |
| `personID` | Un identificador único para la persona a la que se relaciona este registro. Este campo no representa necesariamente una identidad relacionada con la persona a menos que también se designe como [campo de identidad](../schema/composition.md#identity). |
| `repositoryCreatedBy` | ID del usuario que creó el registro. |
| `repositoryLastModifiedBy` | El ID del usuario que modificó el registro por última vez. |

{style=&quot;table-layout:auto&quot;}

## Grupos de campos compatibles {#field-groups}

>[!NOTE]
>
>Los nombres de varios grupos de campos han cambiado. Consulte el documento en [actualizaciones del nombre del grupo de campos](../field-groups/name-updates.md) para obtener más información.

Adobe proporciona varios grupos de campos estándar para su uso con la variable [!DNL XDM Individual Profile] Clase . A continuación se muestra una lista de algunos grupos de campos que se utilizan con más frecuencia para la clase :

* [[!UICONTROL Consentimientos y preferencias]](../field-groups/profile/consents.md)
* [[!UICONTROL Detalles demográficos]](../field-groups/profile/demographic-details.md)
* [[!UICONTROL Mapa de identidades]](../field-groups/profile/identitymap.md)
* [[!UICONTROL Detalles de fidelidad]](../field-groups/profile/loyalty-details.md)
* [[!UICONTROL Detalles de contacto personal]](../field-groups/profile/personal-contact-details.md)
* [[!UICONTROL Detalles de pertenencia a segmentos]](../field-groups/profile/segmentation.md)
* [[!UICONTROL Suscripción a Telecom]](../field-groups/profile/telecom-subscription.md)
* [[!UICONTROL Detalles de contacto de trabajo]](../field-groups/profile/work-contact-details.md)
* [[!UICONTROL Componentes de persona empresarial XDM]](../field-groups/profile/business-person-components.md)\*
* [[!UICONTROL Detalles de persona comercial XDM]](../field-groups/profile/business-person-details.md)\*

*\*Este grupo de campos solo está disponible para organizaciones con acceso a la edición B2B de Adobe Real-time Customer Data Platform.*

Para obtener una lista completa de todos los grupos de campos compatibles con [!DNL XDM Individual Profile], consulte [Repositorio de GitHub XDM](https://github.com/adobe/xdm/tree/master/components/fieldgroups/profile).
