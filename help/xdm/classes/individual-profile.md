---
keywords: Experience Platform;inicio;temas populares;esquema;Esquema;XDM;perfil individual;campos;esquemas;esquemas;identityMap;mapa de identidad;mapa de identidad;diseño de esquema;mapa;esquema;esquema de unión;;esquema;esquema de unión
solution: Experience Platform
title: Clase de perfil individual de XDM
description: Obtenga información acerca de la clase de perfil individual de XDM.
exl-id: 83b22462-79ce-4024-aa50-a9bd800c0f81
source-git-commit: ce937f1335283382189fa40f65aa268735c02715
workflow-type: tm+mt
source-wordcount: '552'
ht-degree: 0%

---

# [!DNL XDM Individual Profile] clase

[!DNL XDM Individual Profile] es una clase de modelo de datos de experiencia (XDM) estándar que forma una representación singular (o &quot;perfil&quot;) de una persona individual. Específicamente, la clase (y sus grupos de campos compatibles) captura los atributos e intereses de las personas identificadas y parcialmente identificadas que interactúan con su marca.

Los perfiles pueden variar desde señales de comportamiento anónimas (como las cookies del explorador) hasta perfiles altamente identificados que contienen información detallada como nombre, fecha de nacimiento, ubicación y dirección de correo electrónico. A medida que un perfil crece, se convierte en un repositorio sólido de información personal, identidades, detalles de contacto y preferencias de comunicación para un individuo. Para obtener más información de alto nivel sobre el uso de esta clase en el ecosistema de Platform, consulte la [descripción general de XDM](../home.md#data-behaviors).

![Diagrama de esquema de la clase de perfil individual de XDM.](../images/classes/individual-profile.png)

| Propiedad | Descripción |
| --- | --- |
| `_repo` | Objeto que contiene los [!UICONTROL campos DateTime] siguientes: <ul><li>`createDate`: la fecha y hora en que se creó el recurso en el almacén de datos, como cuándo se ingerieron los datos por primera vez.</li><li>`modifyDate`: la fecha y la hora en que se modificó el recurso por última vez.</li></ul> |
| `_id` | Un identificador de cadena único para el registro. Este campo se utiliza para realizar el seguimiento de la exclusividad de un registro individual, evitar la duplicación de datos y buscar ese registro en los servicios descendentes. En algunos casos, `_id` puede ser un [Identificador único universal (UUID)](https://tools.ietf.org/html/rfc4122) o un [Identificador único global (GUID)](https://docs.microsoft.com/en-us/dotnet/api/system.guid?view=net-5.0).<br><br>Si está transmitiendo datos desde una conexión de origen o ingiriendo directamente desde un archivo de Parquet, debe generar este valor concatenando una cierta combinación de campos que hacen que el registro sea único, como un ID principal, una marca de tiempo, un tipo de registro, etc. El valor concatenado debe ser una cadena con formato `uri-reference`, lo que significa que se deben eliminar los caracteres de dos puntos. Después, el valor concatenado debe tener un cifrado hash con SHA-256 u otro algoritmo de su elección.<br><br>Es importante distinguir que **este campo no representa una identidad relacionada con una persona individual**, sino más bien el registro de datos en sí. Los datos de identidad relacionados con una persona deben relegarse a [campos de identidad](../schema/composition.md#identity) proporcionados por grupos de campos compatibles. |
| `createdByBatchID` | El ID del lote ingerido que provocó la creación del registro. |
| `modifiedByBatchID` | El ID del último lote ingerido que provocó que se actualizara el registro. |
| `personID` | Un identificador único de la persona a la que se relaciona este registro. Este campo no representa necesariamente una identidad relacionada con la persona a menos que también se designe como [campo de identidad](../schema/composition.md#identity). |
| `repositoryCreatedBy` | El ID del usuario que creó el registro. |
| `repositoryLastModifiedBy` | El ID del usuario que modificó el registro por última vez. |

{style="table-layout:auto"}

## Grupos de campos compatibles {#field-groups}

>[!NOTE]
>
>Los nombres de varios grupos de campos han cambiado. Consulte el documento sobre [actualizaciones de nombre de grupo de campos](../field-groups/name-updates.md) para obtener más información.

El Adobe proporciona varios grupos de campos estándar para su uso con la clase [!DNL XDM Individual Profile]. A continuación se muestra una lista de algunos grupos de campos utilizados comúnmente para la clase:

* [[!UICONTROL Consentimientos y preferencias]](../field-groups/profile/consents.md)
* [[!UICONTROL Detalles demográficos]](../field-groups/profile/demographic-details.md)
* [[!UICONTROL mapa de identidad]](../field-groups/profile/identitymap.md)
* [[!UICONTROL Detalles de fidelización]](../field-groups/profile/loyalty-details.md)
* [[!UICONTROL Datos personales de contacto]](../field-groups/profile/personal-contact-details.md)
* [[!UICONTROL Detalles de pertenencia a segmento]](../field-groups/profile/segmentation.md)
* [[!UICONTROL Suscripción de telecomunicaciones]](../field-groups/profile/telecom-subscription.md)
* [[!UICONTROL Detalles de contacto de trabajo]](../field-groups/profile/work-contact-details.md)
* [[!UICONTROL Componentes de persona de negocios XDM]](../field-groups/profile/business-person-components.md)\*
* [[!UICONTROL Detalles de persona de negocios de XDM]](../field-groups/profile/business-person-details.md)\*

*\*Este grupo de campos solo está disponible para las organizaciones con acceso a la edición B2B de Adobe Real-time Customer Data Platform.*

Para obtener una lista completa de todos los grupos de campos compatibles con [!DNL XDM Individual Profile], consulte el [repositorio de GitHub de XDM](https://github.com/adobe/xdm/tree/master/components/fieldgroups/profile).
