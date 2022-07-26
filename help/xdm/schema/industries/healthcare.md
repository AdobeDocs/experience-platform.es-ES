---
title: Modelo de datos del sector sanitario ERD
description: Vea un diagrama de relación de entidades (ERD) que describe un modelo de datos estandarizado para el sector sanitario. Este modelo de datos es compatible con Experience Data Model (XDM) para su uso en Adobe Experience Platform.
source-git-commit: 721059a87347e371228d00edeac141afa894af47
workflow-type: tm+mt
source-wordcount: '627'
ht-degree: 1%

---

# [!UICONTROL Atención] modelo de datos de la industria ERD

El siguiente diagrama de relación de entidades (ERD) representa un modelo de datos estandarizado para el sector sanitario. El ERD se presenta intencionalmente de forma desnormalizada y teniendo en cuenta cómo se almacenan los datos en Adobe Experience Platform.

>[!NOTE]
>
>El ERD como se describe es una recomendación sobre cómo debe modelar sus datos para este caso de uso del sector. Para utilizar este modelo de datos en Platform, debe crear los esquemas recomendados y sus relaciones usted mismo. Consulte las guías sobre la administración [esquemas](../../ui/resources/schemas.md) y [relaciones](../../tutorials/relationship-ui.md) en la interfaz de usuario para obtener más información.

Utilice la siguiente leyenda para interpretar este ERD:

* Cada entidad mostrada en se basa en un [Clase del Modelo de datos de experiencia (XDM)](../composition.md#class).
* Para una entidad determinada, cada fila marcada en **bold** representa un grupo de campos o un tipo de datos, con los campos relevantes que proporciona enumerados a continuación en texto sin negrita.
* Los campos más importantes de una entidad determinada se resaltan en rojo.
* Todas las propiedades que podrían utilizarse para identificar clientes individuales se marcan como &quot;identidad&quot;, con una de estas propiedades marcadas como &quot;identidad principal&quot;.
* Las relaciones de entidad se marcan como no dependientes, ya que los eventos basados en cookies a menudo no pueden determinar la persona o el individuo que realizó la transacción.

![Imagen que muestra el diagrama de relación de entidad para el modelo de datos del sector sanitario](../../images/industries/healthcare.png)

>[!NOTE]
>
>Cada entidad incluye un campo &quot;_ID&quot;, que representa el identificador de cadena único (`_id`) para el registro o evento en cuestión. Este campo se utiliza para rastrear la exclusividad del registro o evento individual, evitar la duplicación de datos y buscar esos datos en servicios descendentes. En algunos casos, `_id` puede ser [Identificador único universal (UUID)](https://tools.ietf.org/html/rfc4122) o [Identificador único global (GUID)](https://docs.microsoft.com/en-us/dotnet/api/system.guid?view=net-5.0).<br><br>Es importante distinguir que **este campo no representa una identidad relacionada con una persona individual**, sino más bien el registro de los datos en sí. Los datos de identidad relacionados con una persona, evento o entidad empresarial deben relegarse a [campos de identidad](../composition.md#identity) proporcionado por grupos de campos compatibles en su lugar.

## [!UICONTROL Atención] casos de uso

La siguiente tabla describe las clases recomendadas y los grupos de campos de esquema para varios casos de uso de asistencia sanitaria comunes.

| Caso de uso | Clases recomendadas y grupos de campos |
| --- | --- |
| Mejore la adquisición digital y la experiencia entre los consumidores que compran seguros. Algunos ejemplos son: <ul><li>Cuando las personas acceden a una página que contiene información general (como planes, niveles de plan, medicamentos, programas de bienestar, etc.), comprendan su comportamiento y lo que buscan para enviar correos electrónicos promocionales o dirigirlos a plataformas de terceros con anuncios.</li><li>Cuando la gente busque información sobre la salud cardiaca y la vacuna, envíenles información relacionada con la vacuna sobre la salud cardiaca para crear conciencia sobre la marca o pedirles que programen vacunas.</li></ul> | <ul><li>**[[!UICONTROL Perfil individual XDM]](../../classes/individual-profile.md)**:<ul><li>[[!UICONTROL Detalles de los miembros del sector sanitario]](../../field-groups/profile/healthcare-member-details.md)</li><li>Campos de relación establecidos entre `planID` atributos y esquemas que utilizan la variable [!UICONTROL Plan] Clase .</li></ul></li><li>**[[!UICONTROL Pagador]](../../classes/payer.md)**</li><li>**[[!UICONTROL Plan]](../../classes/plan.md)**:<ul><li>[[!UICONTROL Detalles del plan de atención médica]](../../field-groups/plan/healthcare-plan-details.md)</li></ul></li><li>**[[!UICONTROL XDM ExperienceEvent]](../../classes/experienceevent.md)**:<ul><li>[[!UICONTROL Detalles de la aplicación]](../../field-groups/event/application-details.md)</li><li>[[!UICONTROL Detalles del sitio]](../../field-groups/event/sitetool-details.md)</li><li>[[!UICONTROL  Detalles de marketing de campaña]](../../field-groups/event/campaign-marketing-details.md)</li></ul></li></ul> |
| Aumente la adquisición digital de pacientes a través de anuncios específicos basados en comportamiento en línea y datos de salud anteriores. | <ul><li>**[[!UICONTROL Perfil individual XDM]](../../classes/individual-profile.md)**:<ul><li>[[!UICONTROL Detalles de los miembros del sector sanitario]](../../field-groups/profile/healthcare-member-details.md)</li></ul></li><li>**[[!UICONTROL Proveedor]](../../classes/provider.md)**:<ul><li>[[!UICONTROL Proveedor de atención médica]](../../field-groups/provider/healthcare-provider.md)</li></ul></li><li>**[[!UICONTROL XDM ExperienceEvent]](../../classes/experienceevent.md)**:<ul><li>[[!UICONTROL Detalles web]](../../field-groups/event/web-details.md)</li><li>[[!UICONTROL Detalles publicitarios]](../../field-groups/event/advertising-details.md)</li></ul></li></ul> |
| Mejorar la inscripción y la creación de cuentas en los planes de salud mediante el seguimiento del marketing de los seguros a través de diferentes canales, con el fin de comprender cómo descubrió un cliente una compañía de seguros. | <ul><li>**[[!UICONTROL Perfil individual XDM]](../../classes/individual-profile.md)**:<ul><li>[[!UICONTROL Detalles de los miembros del sector sanitario]](../../field-groups/profile/healthcare-member-details.md)</li></ul></li><li>**[[!UICONTROL Pagador]](../../classes/payer.md)**</li><li>**[[!UICONTROL Plan]](../../classes/plan.md)**:<ul><li>[[!UICONTROL Detalles del plan de atención médica]](../../field-groups/plan/healthcare-plan-details.md)</li></ul></li><li>**[[!UICONTROL XDM ExperienceEvent]](../../classes/experienceevent.md)**:<ul><li>[[!UICONTROL Detalles web]](../../field-groups/event/web-details.md)</li><li>[[!UICONTROL Detalles publicitarios]](../../field-groups/event/advertising-details.md)</li></ul></li></ul> |
| Evite que se produzcan fallos en la cobertura del seguro médico. | <ul><li>**[[!UICONTROL Perfil individual XDM]](../../classes/individual-profile.md)**:<ul><li>[[!UICONTROL Detalles de los miembros del sector sanitario]](../../field-groups/profile/healthcare-member-details.md)</li></ul></li><li>**[[!UICONTROL Plan]](../../classes/plan.md)**:<ul><li>[[!UICONTROL Detalles del plan de atención médica]](../../field-groups/plan/healthcare-plan-details.md)</li></ul></li></ul> |
| Promocione la información sobre medicamentos a los proveedores mediante anuncios directos a los clientes (DTC). | <ul><li>**[[!UICONTROL Perfil individual XDM]](../../classes/individual-profile.md)**:<ul><li>[[!UICONTROL Detalles de los miembros del sector sanitario]](../../field-groups/profile/healthcare-member-details.md)</li></ul></li><li>**[[!UICONTROL Medicación]](../../classes/medication.md)**:<ul><li>[[!UICONTROL Medicación médica]](../../field-groups/medication/healthcare-medication.md)</li></ul></li><li>**[[!UICONTROL XDM ExperienceEvent]](../../classes/experienceevent.md)**:<ul><li>[[!UICONTROL Detalles web]](../../field-groups/event/web-details.md)</li><li>[[!UICONTROL Detalles publicitarios]](../../field-groups/event/advertising-details.md)</li></ul></li></ul> |
