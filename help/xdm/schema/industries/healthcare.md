---
title: Modelo de datos de la industria sanitaria ERD
description: Vea un diagrama de relación de entidades (ERD) que describe un modelo de datos estandarizado para el sector sanitario. Este modelo de datos es compatible con el Modelo de datos de experiencia (XDM) para su uso en Adobe Experience Platform.
exl-id: ebcf97ec-f5a4-46e5-b1ad-c80d55aa2c6e
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '606'
ht-degree: 0%

---

# [!UICONTROL Sanidad] modelo de datos del sector ERD

El siguiente diagrama de relación de entidades (ERD) representa un modelo de datos estandarizado para el sector sanitario. El ERD se presenta intencionalmente de manera desnormalizada y teniendo en cuenta cómo se almacenan los datos en Adobe Experience Platform.

>[!NOTE]
>
>El ERD tal como se describe es una recomendación sobre cómo debe modelar los datos para este caso de uso del sector. Para utilizar este modelo de datos en Experience Platform, debe construir los esquemas recomendados y sus relaciones. Consulte las guías sobre la administración de [esquemas](../../ui/resources/schemas.md) y [relaciones](../../tutorials/relationship-ui.md) en la interfaz de usuario para obtener más información.

Utilice la siguiente leyenda para interpretar este ERD:

* Cada entidad mostrada en se basa en una clase [Experience Data Model (XDM) subyacente](../composition.md#class).
* Los campos con sangría debajo de un campo principal representan un campo secundario, o subcampo, que pertenece al grupo de campos del elemento principal.
* Los campos más importantes de una entidad determinada se resaltan en rojo.
* Todas las propiedades que se pueden utilizar para identificar clientes individuales se marcan como &quot;identidad&quot;, con una de estas propiedades marcada como &quot;identidad principal&quot;.
* Las relaciones de entidad se marcan como no dependientes, ya que los eventos basados en cookies a menudo no pueden determinar la persona o individuo que realizó la transacción.

![Ejemplo de ERD para un modelo de datos del sector sanitario](../../images/industries/healthcare.png)

>[!NOTE]
>
>Cada entidad incluye un campo &quot;_ID&quot;, que representa el atributo de identificador de cadena único (`_id`) para el registro o evento en cuestión. Este campo se utiliza para realizar un seguimiento de la exclusividad del registro o evento individual, evitar la duplicación de datos y buscar esos datos en servicios descendentes. En algunos casos, `_id` puede ser un [Identificador único universal (UUID)](https://tools.ietf.org/html/rfc4122) o un [Identificador único global (GUID)](https://docs.microsoft.com/en-us/dotnet/api/system.guid?view=net-5.0).<br><br>Es importante distinguir que **este campo no representa una identidad relacionada con una persona individual**, sino más bien el registro de datos en sí. Los datos de identidad relacionados con una persona, evento o entidad empresarial deben relegarse a [campos de identidad](../composition.md#identity) proporcionados por grupos de campos compatibles.

## Casos de uso de [!UICONTROL Healthcare]

La siguiente tabla describe las clases recomendadas y los grupos de campos de esquema para varios casos de uso sanitarios comunes.

| Ejemplo de uso | Clases y grupos de campos recomendados |
| --- | --- |
| Mejorar la adquisición digital y la experiencia entre los consumidores que buscan un seguro. Algunos ejemplos son: <ul><li>Cuando las personas acceden a una página que contiene información general (como planes, nombres/niveles de planes, medicaid, programas de bienestar, etc.), entienden su comportamiento y lo que buscan para enviar correos electrónicos promocionales o dirigirlos a plataformas de terceros con anuncios.</li><li>Cuando las personas busquen información sobre la salud del corazón y la vacuna, envíeles información relacionada con la vacuna sobre la salud del corazón para crear conciencia de marca o pídale que programe vacunas.</li></ul> | <ul><li>**[[!UICONTROL Perfil individual de XDM]](../../classes/individual-profile.md)**:<ul><li>[[!UICONTROL Detalles del miembro de atención médica]](../../field-groups/profile/healthcare-member-details.md)</li><li>Campos de relación establecidos entre `planID` atributos y esquemas que utilizan la clase [!UICONTROL Plan].</li></ul></li><li>**[[!UICONTROL Pagador]](../../classes/payer.md)**</li><li>**[[!UICONTROL Plan]](../../classes/plan.md)**:<ul><li>[[!UICONTROL Detalles del plan de atención médica]](../../field-groups/plan/healthcare-plan-details.md)</li></ul></li><li>**[[!UICONTROL ExperienceEvent de XDM]](../../classes/experienceevent.md)**:<ul><li>[[!UICONTROL Detalles de la aplicación]](../../field-groups/event/application-details.md)</li><li>[[!UICONTROL Detalles de la herramienta de sitio]](../../field-groups/event/sitetool-details.md)</li><li>[[!UICONTROL &#x200B; detalles de marketing de campaña]](../../field-groups/event/campaign-marketing-details.md)</li></ul></li></ul> |
| Aumente la adquisición digital de pacientes a través de anuncios dirigidos basados en el comportamiento en línea y los datos de salud pasados. | <ul><li>**[[!UICONTROL Perfil individual de XDM]](../../classes/individual-profile.md)**:<ul><li>[[!UICONTROL Detalles del miembro de atención médica]](../../field-groups/profile/healthcare-member-details.md)</li></ul></li><li>**[[!UICONTROL Proveedor]](../../classes/provider.md)**:<ul><li>[[!UICONTROL Proveedor de atención médica]](../../field-groups/provider/healthcare-provider.md)</li></ul></li><li>**[[!UICONTROL ExperienceEvent de XDM]](../../classes/experienceevent.md)**:<ul><li>[[!UICONTROL Detalles web]](../../field-groups/event/web-details.md)</li><li>[[!UICONTROL Detalles de Advertising]](../../field-groups/event/advertising-details.md)</li></ul></li></ul> |
| Mejorar la inscripción y la creación de cuentas en los planes de salud mediante el seguimiento de la comercialización de los seguros a través de diferentes canales, con el fin de comprender cómo un cliente se enteró de una compañía de seguros. | <ul><li>**[[!UICONTROL Perfil individual de XDM]](../../classes/individual-profile.md)**:<ul><li>[[!UICONTROL Detalles del miembro de atención médica]](../../field-groups/profile/healthcare-member-details.md)</li></ul></li><li>**[[!UICONTROL Pagador]](../../classes/payer.md)**</li><li>**[[!UICONTROL Plan]](../../classes/plan.md)**:<ul><li>[[!UICONTROL Detalles del plan de atención médica]](../../field-groups/plan/healthcare-plan-details.md)</li></ul></li><li>**[[!UICONTROL ExperienceEvent de XDM]](../../classes/experienceevent.md)**:<ul><li>[[!UICONTROL Detalles web]](../../field-groups/event/web-details.md)</li><li>[[!UICONTROL Detalles de Advertising]](../../field-groups/event/advertising-details.md)</li></ul></li></ul> |
| Evite los lapsos en la cobertura del seguro médico. | <ul><li>**[[!UICONTROL Perfil individual de XDM]](../../classes/individual-profile.md)**:<ul><li>[[!UICONTROL Detalles del miembro de atención médica]](../../field-groups/profile/healthcare-member-details.md)</li></ul></li><li>**[[!UICONTROL Plan]](../../classes/plan.md)**:<ul><li>[[!UICONTROL Detalles del plan de atención médica]](../../field-groups/plan/healthcare-plan-details.md)</li></ul></li></ul> |
| Promocione información sobre los medicamentos a los proveedores mediante anuncios directos a los clientes (DTC). | <ul><li>**[[!UICONTROL Perfil individual de XDM]](../../classes/individual-profile.md)**:<ul><li>[[!UICONTROL Detalles del miembro de atención médica]](../../field-groups/profile/healthcare-member-details.md)</li></ul></li><li>**[[!UICONTROL Medicamento]](../../classes/medication.md)**:<ul><li>[[!UICONTROL Medicación para el cuidado de la salud]](../../field-groups/medication/healthcare-medication.md)</li></ul></li><li>**[[!UICONTROL ExperienceEvent de XDM]](../../classes/experienceevent.md)**:<ul><li>[[!UICONTROL Detalles web]](../../field-groups/event/web-details.md)</li><li>[[!UICONTROL Detalles de Advertising]](../../field-groups/event/advertising-details.md)</li></ul></li></ul> |

