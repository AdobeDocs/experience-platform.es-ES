---
keywords: correo electrónico;correo electrónico;destinos de correo electrónico
title: Información general sobre los destinos de marketing por correo electrónico
type: Tutorial
description: Los proveedores de servicios de correo electrónico (ESP) le permiten administrar sus actividades de marketing por correo electrónico, como por ejemplo el envío de campañas de correo electrónico promocionales.
exl-id: e07f8c5a-0424-4de5-810f-3d5711ef4606
source-git-commit: 802b1844bec1e577e978da5d5a69de87278c04b9
workflow-type: tm+mt
source-wordcount: '382'
ht-degree: 4%

---

# Información general sobre los destinos de marketing por correo electrónico {#email-marketing-destinations}

## Información general {#overview}

Los proveedores de servicios de correo electrónico (ESP) le permiten administrar sus actividades de marketing por correo electrónico, como el envío de campañas de correo electrónico promocionales. Adobe Experience Platform se integra con los ESP permitiéndole activar segmentos en destinos de marketing por correo electrónico.

Platform exporta los segmentos como archivos `.csv` y los envía a la ubicación que prefiera. Programe la importación de datos en su plataforma de marketing por correo electrónico desde la ubicación de almacenamiento habilitada en [!DNL Platform]. El proceso de importación de datos varía según el socio. Lea los artículos de destinos individuales para obtener más información.

## Destinos de marketing por correo electrónico compatibles {#supported-destinations}

Adobe Experience Platform admite los siguientes destinos de marketing por correo electrónico:

* [Adobe Campaign](adobe-campaign.md)
* [Oracle Eloqua](oracle-eloqua.md)
* [Responsys de oracle](oracle-responsys.md)
* [Marketing Cloud de Salesforce](salesforce-marketing-cloud.md)

## Conectarse a un nuevo destino de marketing por correo electrónico {#connect-destination}

Para enviar segmentos a destinos de marketing por correo electrónico para sus campañas, Platform primero debe conectarse al destino. Consulte el [tutorial de creación de destino](../../ui/connect-destination.md) para obtener información detallada sobre la configuración de un nuevo destino.

## Prácticas recomendadas al activar audiencias en destinos de marketing por correo electrónico {#best-practices}

### Selección de identidad {#identity}

Adobe recomienda seleccionar un identificador único del [esquema de unión](../../../profile/home.md#profile-fragments-and-union-schemas). Este es el campo en el que se desactivan las identidades de usuario. Normalmente, este campo es la dirección de correo electrónico, pero también puede ser un ID de programa de fidelidad o un número de teléfono. Consulte la siguiente tabla para los identificadores únicos más comunes y su campo XDM en el esquema.

| Identificador único | Campo XDM en Esquema unificado |
|----------------- | ---------------------------|
| Dirección de correo electrónico | `personalEmail.address` |
| Phone | `mobilePhone.number` |
| ID del programa de fidelidad | `Customer-defined XDM field` |

### Otros atributos de destino

En el selector de campos Esquema, elija qué otros campos desea exportar al destino de correo electrónico. Algunas opciones recomendadas son:

| Esquema | Campo XDM |
|------ | ---------|
| Nombre | `person.name.firstName` |
| Apellidos | `person.name.lastName` |
| Teléfono | `mobilePhone.number` |
| Ciudad de la dirección | `homeAddress.city` |
| Estado de la dirección | `homeAddress.stateProvince` |
| Código postal de la dirección | `homeAddress.postalCode` |
| Cumpleaños | `person.birthDayAndMonth` |
| Pertenencia a segmentos | `segmentMembership.status` |

## Importar datos desde la ubicación de almacenamiento en el destino {#import-data-into-destination}

Lea los artículos de destino de marketing por correo electrónico para aprender a importar datos de su ubicación de almacenamiento en destinos:

* [Adobe Campaign](adobe-campaign.md)
* [Oracle Eloqua](oracle-eloqua.md)
* [Responsys de oracle](oracle-responsys.md)
* [Marketing Cloud de Salesforce](salesforce-marketing-cloud.md)

## Activar segmentos en destinos de marketing por correo electrónico {#activate}

Para obtener instrucciones sobre cómo activar segmentos en destinos de marketing de correo electrónico, consulte [Activar perfiles y segmentos en un destino](../../ui/activate-destinations.md).

## Recursos adicionales

* [Activar datos en destinos](../../ui/activate-destinations.md)
* [Cree destinos de marketing por correo electrónico y active los datos mediante la API de servicio de flujo](../../api/email-marketing.md)
