---
keywords: correo electrónico;Correo electrónico;correo electrónico;destinos de correo electrónico
title: Resumen de destinos de marketing de correo electrónico
type: Tutorial
description: Los proveedores de servicios de correo electrónico (ESP) le permiten administrar sus actividades de marketing por correo electrónico, como para enviar campañas de correo electrónico promocionales.
exl-id: e07f8c5a-0424-4de5-810f-3d5711ef4606
source-git-commit: ccbc633bfce8f4f66577b50064c28cfc26cb6dca
workflow-type: tm+mt
source-wordcount: '388'
ht-degree: 4%

---

# Resumen de destinos de marketing de correo electrónico {#email-marketing-destinations}

## Información general {#overview}

Los proveedores de servicios de correo electrónico (ESP) permiten administrar las actividades de marketing por correo electrónico, como el envío de campañas de correo electrónico promocionales. Adobe Experience Platform se integra con los ESP, lo que le permite activar segmentos en destinos de marketing por correo electrónico.

Platform exporta los segmentos como `.csv` y los envía a su ubicación preferida. Programe la importación de datos en su plataforma de marketing por correo electrónico desde la ubicación de almacenamiento habilitada en [!DNL Platform]. El proceso de importación de datos varía según el socio. Lea los artículos de destinos individuales para obtener más información.

## Destinos de marketing por correo electrónico admitidos {#supported-destinations}

Adobe Experience Platform admite los siguientes destinos de marketing por correo electrónico:

* [Adobe Campaign](adobe-campaign.md)
* [Oracle Eloqua](oracle-eloqua.md)
* [Oracle Responsys](oracle-responsys.md)
* [Marketing Cloud de Salesforce](salesforce-marketing-cloud.md)
* [SendGrid](sendgrid.md)

## Conectar con un nuevo destino de marketing por correo electrónico {#connect-destination}

Para enviar segmentos a destinos de marketing por correo electrónico para sus campañas, Platform debe conectarse primero al destino. Consulte la [tutorial de creación de destino](../../ui/connect-destination.md) para obtener información detallada sobre la configuración de un nuevo destino.

## Prácticas recomendadas al activar audiencias en destinos de marketing por correo electrónico {#best-practices}

### Selección de identidad {#identity}

El Adobe recomienda seleccionar un identificador único de su [esquema de unión](../../../profile/home.md#profile-fragments-and-union-schemas). Este es el campo desde el que se desactivan las identidades de los usuarios. Normalmente, este campo es la dirección de correo electrónico, pero también puede ser un ID de programa de fidelidad o un número de teléfono. Consulte la tabla siguiente para conocer los identificadores únicos más comunes y su campo XDM en el esquema.

| Identificador único | Campo XDM en el esquema unificado |
|----------------- | ---------------------------|
| Dirección de correo electrónico | `personalEmail.address` |
| Phone | `mobilePhone.number` |
| ID del programa de fidelización | `Customer-defined XDM field` |

### Otros atributos de destino

En el selector de Campos de esquema, elija qué otros campos desea exportar al destino de correo electrónico. Algunas opciones recomendadas son:

| Esquema | Campo XDM |
|------ | ---------|
| Nombre | `person.name.firstName` |
| Apellidos | `person.name.lastName` |
| Phone | `mobilePhone.number` |
| Ciudad de dirección | `homeAddress.city` |
| Estado de dirección | `homeAddress.stateProvince` |
| Código postal de la dirección | `homeAddress.postalCode` |
| Cumpleaños | `person.birthDayAndMonth` |
| Inscripción a segmento | `segmentMembership.status` |

## Importar datos desde su ubicación de almacenamiento al destino {#import-data-into-destination}

Lea los artículos de destino de marketing por correo electrónico individuales para obtener información sobre cómo importar datos desde su ubicación de almacenamiento a los destinos:

* [Adobe Campaign](adobe-campaign.md)
* [Oracle Eloqua](oracle-eloqua.md)
* [Oracle Responsys](oracle-responsys.md)
* [Marketing Cloud de Salesforce](salesforce-marketing-cloud.md)

## Activar segmentos en destinos de marketing por correo electrónico {#activate}

Para obtener instrucciones sobre cómo activar segmentos en destinos de marketing por correo electrónico, consulte [Activar datos de audiencia en destinos de exportación de perfiles por lotes](../../ui/activate-batch-profile-destinations.md).

## Recursos adicionales

* [Activar datos de audiencia en destinos de exportación de perfiles por lotes](../../ui/activate-batch-profile-destinations.md)
* [Cree destinos de marketing por correo electrónico y active datos con la API de Flow Service](../../api/connect-activate-batch-destinations.md)
