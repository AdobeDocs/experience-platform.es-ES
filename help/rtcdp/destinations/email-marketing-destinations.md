---
title: Destinos de mercadotecnia de correo electrónico
seo-title: Destinos de mercadotecnia de correo electrónico
description: Los proveedores de servicios de correo electrónico (ESP) le permiten administrar sus actividades de mercadotecnia por correo electrónico, por ejemplo, para enviar campañas de correo electrónico promocionales.
seo-description: Los proveedores de servicios de correo electrónico (ESP) le permiten administrar sus actividades de mercadotecnia por correo electrónico, por ejemplo, para enviar campañas de correo electrónico promocionales.
translation-type: tm+mt
source-git-commit: 463212a8fabb9dd5962b4d3f523a6f2d88bb1d9d

---


# Destinos de mercadotecnia de correo electrónico {#email-marketing-destinations}

Los proveedores de servicios de correo electrónico (ESP) le permiten administrar sus actividades de mercadotecnia por correo electrónico, como el envío de campañas de correo electrónico promocionales. La plataforma de datos del cliente en tiempo real de Adobe se integra con los ESP permitiéndole activar segmentos en destinos de marketing por correo electrónico.

Para enviar segmentos a destinos de marketing por correo electrónico para sus campañas, el CDP en tiempo real de Adobe primero debe conectarse al destino.

La conexión a destinos de marketing por correo electrónico es un proceso de tres pasos. Cada uno de los pasos se describe más abajo en esta página.

En el flujo de destino de conexión, descrito en la sección siguiente, conéctese a Amazon S3 o SFTP. CDP en tiempo real exporta sus segmentos como `.csv` `.txt` o como archivos y los envía a su ubicación preferida. Programe la importación de datos en su plataforma de marketing por correo electrónico desde la ubicación de almacenamiento habilitada en CDP en tiempo real. El proceso de importación de datos varía según el socio. Consulte los artículos de destinos individuales para obtener más información.

## Paso 1: Conectar destino {#connect-destination}

1. En **[!UICONTROL Connections > Destinations]**, seleccione el destino de marketing por correo electrónico al que desea conectarse y, a continuación, seleccione **[!UICONTROL Connect destination]**.

   ![Conectar al destino](/help/rtcdp/destinations/assets/connect-destination.png)

2. En el asistente de Connect, seleccione la ubicación **[!UICONTROL Connection type]** del almacenamiento. Puede seleccionar entre **Amazon S3**, **SFTP con contraseña**, **SFTP con clave** SSH. Rellene la información siguiente, según el tipo de conexión y seleccione **[!UICONTROL Connect]**.

Para las conexiones **** S3, debe proporcionar el ID de clave de acceso y la clave de acceso secreto.

Para **SFTP con conexiones de contraseña** , debe proporcionar Dominio, Puerto, Nombre de usuario y Contraseña.

Para **SFTP con conexiones SSH Key** , debe proporcionar Dominio, Puerto, Nombre de usuario y Clave SSH.

## Paso 2: Seleccione los campos de esquema que desea utilizar como atributos de destino en los archivos exportados {#destination-attributes}

En este paso, está seleccionando los campos que desea exportar a destinos de marketing por correo electrónico.

![Atributos de destino](/help/rtcdp/destinations/assets/destination-attributes.png)

### Identidad {#identity}

Le recomendamos que seleccione un identificador único del esquema [de](https://www.adobe.io/apis/experienceplatform/home/profile-identity-segmentation/profile-identity-segmentation-services.html#!api-specification/markdown/narrative/technical_overview/unified_profile_architectural_overview/unified_profile_architectural_overview.md)unión. Este es el campo en el que se definen las identidades de los usuarios. Normalmente, este campo es la dirección de correo electrónico, pero también puede ser un ID de programa de fidelidad o un número de teléfono. Consulte la tabla siguiente para ver los identificadores únicos más comunes y su campo XDM en un esquema unificado.

| Identificador único | Campo XDM en Esquema unificado |
---------|----------
| Email Address | `personalEmail.address` |
| Phone | `mobilePhone.number` |
| ID del programa de fidelidad | `Customer-defined XDM field` |

### Otros atributos de destino

En el selector de campo Esquema, elija los otros campos que desea exportar al destino de correo electrónico. Algunas opciones recomendadas son:

| Esquema | Campo XDM |
---------|----------
| Nombre | `person.name.firstName` |
| Apellidos | `person.name.lastName` |
| Phone | `mobilePhone.number` |
| Ciudad de dirección | `homeAddress.city` |
| Estado de la dirección | `homeAddress.stateProvince` |
| Dirección Código postal | `homeAddress.postalCode` |
| Cumpleaños | `person.birthDayAndMonth` |

## Paso 3: Importar datos desde la ubicación de almacenamiento en el destino

Consulte los artículos individuales de destino de marketing por correo electrónico para obtener información sobre cómo importar datos de su ubicación de almacenamiento en destinos:

* [Adobe Campaign](/help/rtcdp/destinations/adobe-campaign-destination.md#import-data-into-campaign)
* [Salesforce Marketing Cloud](/help/rtcdp/destinations/salesforce-marketing-cloud-destination.md#import-data-into-salesforce)
* [Oracle Eloqua](/help/rtcdp/destinations/oracle-eloqua-destination.md#import-data-into-eloqua)
* [Oracle Responsys](/help/rtcdp/destinations/oracle-responsys-destination.md#import-data-into-responsys)

## Activar segmentos en destinos de mercadotecnia de correo electrónico

Para obtener instrucciones sobre cómo activar segmentos en destinos de marketing de correo electrónico, consulte [Activar datos en destinos](/help/rtcdp/destinations/activate-destinations.md).