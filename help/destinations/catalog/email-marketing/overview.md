---
keywords: correo electrónico;correo electrónico;destinos de correo electrónico
title: Información general sobre los destinos de marketing por correo electrónico
type: Tutorial
description: Los proveedores de servicios de correo electrónico (ESP) le permiten administrar sus actividades de marketing por correo electrónico, como por ejemplo el envío de campañas de correo electrónico promocionales. Descubra qué ESP son compatibles como destinos de Experience Platform.
exl-id: e07f8c5a-0424-4de5-810f-3d5711ef4606
source-git-commit: d6ea94b275ab0ed7c0638200188fe7ada7bacf5c
workflow-type: tm+mt
source-wordcount: '377'
ht-degree: 4%

---

# Información general sobre los destinos de marketing por correo electrónico {#email-marketing-destinations}

## Información general {#overview}

Los proveedores de servicios de correo electrónico (ESP) le permiten administrar sus actividades de marketing por correo electrónico, como el envío de campañas de correo electrónico promocionales. Adobe Experience Platform se integra con los ESP permitiéndole activar segmentos en destinos de marketing por correo electrónico.

## Destinos de marketing por correo electrónico compatibles {#supported-destinations}

Adobe Experience Platform admite los siguientes destinos de marketing por correo electrónico:

* [Adobe Campaign](adobe-campaign.md)
* [Adobe Campaign Managed Cloud Services](adobe-campaign-managed-services.md)
* [(API) Oracle Eloqua](oracle-eloqua-api.md)
* [(API) Marketing Cloud de Salesforce](salesforce-marketing-cloud-exact-target.md)
* [(Archivos) Oracle Eloqua](oracle-eloqua.md)
* [(Archivos) Marketing Cloud de Salesforce](salesforce-marketing-cloud.md)
* [Responsys de oracle](oracle-responsys.md)
* [SendGrid](sendgrid.md)

## Conectarse a un nuevo destino de marketing por correo electrónico {#connect-destination}

Para enviar segmentos a destinos de marketing por correo electrónico para sus campañas, Platform primero debe conectarse al destino. Consulte la [tutorial de creación de destino](../../ui/connect-destination.md) para obtener información detallada sobre la configuración de un nuevo destino.

## Prácticas recomendadas al activar audiencias en destinos de marketing por correo electrónico {#best-practices}

### Selección de identidad {#identity}

Adobe recomienda seleccionar un identificador único de su [esquema de unión](../../../profile/home.md#profile-fragments-and-union-schemas). Este es el campo en el que se desactivan las identidades de usuario. Normalmente, este campo es la dirección de correo electrónico, pero también puede ser un ID de programa de fidelidad o un número de teléfono. Consulte la siguiente tabla para los identificadores únicos más comunes y su campo XDM en el esquema.

| Identificador único | Campo XDM en Esquema unificado |
|----------------- | ---------------------------|
| Dirección de correo electrónico | `personalEmail.address` |
| Phone | `mobilePhone.number` |
| ID del programa de fidelidad | `Customer-defined XDM field` |

{style="table-layout:auto"}

### Otros atributos de destino {#other-destination-attributes}

En el selector de campos Esquema, elija qué otros campos desea exportar al destino de correo electrónico. Algunas opciones recomendadas son:

| Esquema | Campo XDM |
|------ | ---------|
| Nombre | `person.name.firstName` |
| Apellidos | `person.name.lastName` |
| Phone | `mobilePhone.number` |
| Ciudad de la dirección | `homeAddress.city` |
| Estado de la dirección | `homeAddress.stateProvince` |
| Código postal de la dirección | `homeAddress.postalCode` |
| Cumpleaños | `person.birthDayAndMonth` |
| Inscripción a segmento | `segmentMembership.status` |

{style="table-layout:auto"}

## Activar segmentos en destinos de marketing por correo electrónico {#activate}

Algunos destinos de marketing por correo electrónico en los perfiles de exportación del catálogo exportan de forma continua, a través de una integración de API con el destino.

Otros destinos exportan archivos a una ubicación de almacenamiento en la nube. Una vez finalizada la exportación, debe importar los datos de la ubicación de almacenamiento en la nube a su destino de marketing por correo electrónico.

Siga los vínculos de la sección [destinos de marketing por correo electrónico compatibles](#supported-destinations) para obtener información sobre cómo activar segmentos en cada destino de marketing por correo electrónico.

## Recursos adicionales {#additional-resources}

* [Activar datos de audiencia en destinos de exportación de perfiles en lote](../../ui/activate-batch-profile-destinations.md)
* [Cree destinos de marketing por correo electrónico y active los datos mediante la API de servicio de flujo](../../api/connect-activate-batch-destinations.md)
