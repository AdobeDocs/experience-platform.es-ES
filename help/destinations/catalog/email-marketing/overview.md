---
keywords: correo electrónico;Correo electrónico;correo electrónico;destinos de correo electrónico
title: Resumen de destinos de marketing de correo electrónico
type: Tutorial
description: Los proveedores de servicios de correo electrónico (ESP) le permiten administrar sus actividades de marketing por correo electrónico, como para enviar campañas de correo electrónico promocionales. Descubra qué ESP son compatibles como destinos de Experience Platform.
exl-id: e07f8c5a-0424-4de5-810f-3d5711ef4606
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '377'
ht-degree: 5%

---

# Resumen de destinos de marketing de correo electrónico {#email-marketing-destinations}

## Información general {#overview}

Los proveedores de servicios de correo electrónico (ESP) permiten administrar las actividades de marketing por correo electrónico, como el envío de campañas de correo electrónico promocionales. Adobe Experience Platform se integra con los ESP, lo que le permite activar audiencias en destinos de marketing por correo electrónico.

## Destinos de marketing por correo electrónico admitidos {#supported-destinations}

Adobe Experience Platform admite los siguientes destinos de marketing por correo electrónico:

* [Adobe Campaign](adobe-campaign.md)
* [Adobe Campaign Managed Cloud Services](adobe-campaign-managed-services.md)
* [Categorías de interés en Mailchimp](mailchimp-interest-categories.md)
* [Etiquetas de Mailchimp](mailchimp-tags.md)
* [(API) Oracle Eloqua](oracle-eloqua-api.md)
* [(API) [!DNL Salesforce Marketing Cloud]](salesforce-marketing-cloud-exact-target.md)
* [(Archivos) Oracle Eloqua](oracle-eloqua.md)
* [(Archivos) [!DNL Salesforce Marketing Cloud]](salesforce-marketing-cloud.md)
* [[!DNL Salesforce Marketing Cloud Account Engagement]](salesforce-marketing-cloud-account-engagement.md)
* [Oracle Responsys](oracle-responsys.md)
* [SendGrid](sendgrid.md)

## Conectar con un nuevo destino de marketing por correo electrónico {#connect-destination}

Para enviar audiencias a destinos de marketing por correo electrónico para sus campañas, Experience Platform debe conectarse primero al destino. Consulte el [tutorial de creación de destinos](../../ui/connect-destination.md) para obtener información detallada sobre cómo configurar un nuevo destino.

## Prácticas recomendadas al activar audiencias en destinos de marketing por correo electrónico {#best-practices}

### Selección de identidad {#identity}

Adobe recomienda seleccionar un identificador único de su [esquema de unión](../../../profile/home.md#profile-fragments-and-union-schemas). Este es el campo desde el que se desactivan las identidades de los usuarios. Normalmente, este campo es la dirección de correo electrónico, pero también puede ser un ID de programa de fidelidad o un número de teléfono. Consulte la tabla siguiente para conocer los identificadores únicos más comunes y su campo XDM en el esquema.

| Identificador único | Campo XDM en el esquema unificado |
|----------------- | ---------------------------|
| Correo electrónico | `personalEmail.address` |
| Teléfono | `mobilePhone.number` |
| ID del programa de fidelización | `Customer-defined XDM field` |

{style="table-layout:auto"}

### Otros atributos de destino {#other-destination-attributes}

En el selector de Campos de esquema, elija qué otros campos desea exportar al destino de correo electrónico. Algunas opciones recomendadas son:

| Esquema | Campo XDM |
|------ | ---------|
| Nombre | `person.name.firstName` |
| Apellidos | `person.name.lastName` |
| Teléfono | `mobilePhone.number` |
| Ciudad de dirección | `homeAddress.city` |
| Estado de dirección | `homeAddress.stateProvince` |
| Código postal de la dirección | `homeAddress.postalCode` |
| Cumpleaños | `person.birthDayAndMonth` |
| Pertenencia al segmento | `segmentMembership.status` |

{style="table-layout:auto"}

## Activar audiencias en destinos de marketing por correo electrónico {#activate}

Algunos destinos de marketing por correo electrónico en el catálogo exportan perfiles de forma streaming, a través de una integración de API con el destino.

Otros destinos exportan archivos a una ubicación de almacenamiento en la nube. Una vez completada la exportación, debe importar datos de la ubicación de almacenamiento en la nube al destino de marketing de correo electrónico.

Siga los vínculos de la sección [destinos de marketing por correo electrónico admitidos](#supported-destinations) para obtener información sobre cómo activar audiencias en cada destino de marketing por correo electrónico.

## Recursos adicionales {#additional-resources}

* [Activar datos de audiencia en destinos de exportación de perfiles por lotes](../../ui/activate-batch-profile-destinations.md)
* [Cree destinos de marketing por correo electrónico y active datos con la API de Flow Service](../../api/connect-activate-batch-destinations.md)
