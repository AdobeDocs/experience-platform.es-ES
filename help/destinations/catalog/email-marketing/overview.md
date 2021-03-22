---
keywords: correo electrónico;correo electrónico;destinos de correo electrónico
title: Información general sobre los destinos de marketing por correo electrónico
type: Tutorial
description: Los proveedores de servicios de correo electrónico (ESP) le permiten administrar sus actividades de marketing por correo electrónico, como por ejemplo el envío de campañas de correo electrónico promocionales.
translation-type: tm+mt
source-git-commit: 7d579d85d427c45f39d000288ed883c7ffd003bf
workflow-type: tm+mt
source-wordcount: '772'
ht-degree: 1%

---


# Información general sobre destinos de marketing por correo electrónico {#email-marketing-destinations}

Los proveedores de servicios de correo electrónico (ESP) le permiten administrar sus actividades de marketing por correo electrónico, como el envío de campañas de correo electrónico promocionales. Adobe Experience Platform se integra con los ESP permitiéndole activar segmentos en destinos de marketing por correo electrónico.

Para enviar segmentos a destinos de marketing por correo electrónico para sus campañas, Platform primero debe conectarse al destino.

La conexión a destinos de marketing por correo electrónico es un proceso de tres pasos. Cada uno de los pasos se describe más abajo en esta página.

En el flujo de destino de conexión, descrito en la sección siguiente, conéctese a Amazon S3 o SFTP. Platform exporta los segmentos como archivos `.csv` o `.txt` y los envía a la ubicación que prefiera. Programe la importación de datos en su plataforma de marketing por correo electrónico desde la ubicación de almacenamiento habilitada en Platform. El proceso de importación de datos varía según el socio. Consulte los artículos de destinos individuales para obtener más información.

## Configurar destino {#connect-destination}

En **[!UICONTROL Connections]** > **[!UICONTROL Destinations]**, seleccione el destino de marketing por correo electrónico al que desea conectarse y, a continuación, seleccione **[!UICONTROL Configure]**.

![Conectarse al destino](../../assets/catalog/email-marketing/overview/connect-email-marketing.png)

En el paso **[!UICONTROL Authentication]**, si ha configurado anteriormente una conexión con su destino de marketing por correo electrónico, seleccione **[!UICONTROL Existing Account]** y la conexión existente. O bien, puede seleccionar **[!UICONTROL New Account]** para configurar una nueva conexión con su destino de marketing por correo electrónico. En el selector **[!UICONTROL Connection type]** puede seleccionar entre Amazon S3, SFTP con contraseña o SFTP con clave SSH. Rellene la información siguiente, según el tipo de conexión y, a continuación, seleccione **[!UICONTROL Connect]**.

- Para las conexiones **S3**, debe proporcionar el ID de clave de acceso de Amazon y la clave de acceso secreta.
- Para conexiones **SFTP con contraseña**, debe proporcionar dominio, puerto, nombre de usuario y contraseña para el servidor SFTP.
- Para conexiones **SFTP con clave SSH**, debe proporcionar Dominio, Puerto, Nombre de usuario y Clave SSH para su servidor SFTP.

Opcionalmente, puede adjuntar su clave pública con formato RSA para agregar cifrado a los archivos exportados en la sección **[!UICONTROL Key]**. Tenga en cuenta que esta clave pública **debe** escribirse como una cadena codificada Base64.

En el paso **[!UICONTROL Setup]**, introduzca un nombre y una descripción para el nuevo destino, así como el formato de archivo para los archivos exportados.

Si seleccionó Amazon S3 como opción de almacenamiento en el paso anterior, inserte el nombre del bloque y la ruta de carpeta en el destino de almacenamiento en la nube donde se entregarán los archivos. Para la opción de almacenamiento SFTP, inserte la ruta de carpeta donde se entregarán los archivos.

Además, en este paso, puede seleccionar cualquier acción de marketing que deba aplicarse a este destino. Las acciones de marketing indican la intención para la que se exportarán los datos al destino. Puede seleccionar entre las acciones de marketing definidas por el Adobe o crear su propia acción de marketing. Para obtener más información sobre las acciones de marketing, consulte [Información general sobre las políticas de uso de datos](../../../data-governance/policies/overview.md).

![Paso de configuración de correo electrónico](../../assets/catalog/email-marketing/overview/email-setup-step.png)

## Seleccione qué miembros de segmento incluir en las exportaciones de destino {#select-segments}

En la página **[!UICONTROL Select Segments]** , seleccione qué segmentos desea enviar al destino. Encontrará más información sobre los campos en las secciones siguientes.

![Seleccionar segmentos](../../assets/common/email-select-segments.png)

## Configurar nombres de archivo

Para obtener información sobre la programación del segmento y las opciones de edición de nombres de archivo, consulte el paso [Configurar](../../ui/activate-destinations.md#configure) en el tutorial Activar destinos .

## Seleccionar atributos : seleccione qué campos de esquema utilizar como atributos de destino en los archivos exportados {#destination-attributes}

En este paso, se seleccionan los campos que se exportan a los destinos de marketing por correo electrónico, así como la marca de qué campos son obligatorios.

![Atributos de destino](../../assets/catalog/email-marketing/overview/recommended-attributes.png)

Para obtener más información sobre este paso, consulte el paso [Select attributes](../../ui/activate-destinations.md#select-attributes) en el tutorial de activación de destinos.

## Identidad {#identity}

Se recomienda seleccionar un identificador único del [esquema de unión](../../../profile/home.md#profile-fragments-and-union-schemas). Este es el campo en el que se desactivan las identidades de los usuarios. Normalmente, este campo es la dirección de correo electrónico, pero también puede ser un ID de programa de fidelidad o un número de teléfono. Consulte la siguiente tabla para conocer los identificadores únicos más comunes y su campo XDM en el esquema.

| Identificador único | Campo XDM en Esquema unificado |
----------------- | ---------------------------
| Dirección de correo electrónico | `personalEmail.address` |
| Phone | `mobilePhone.number` |
| ID del programa de fidelidad | `Customer-defined XDM field` |

## Otros atributos de destino

En el selector de campos Esquema, elija qué otros campos desea exportar al destino de correo electrónico. Algunas opciones recomendadas son:

| Esquema | Campo XDM |
------ | ---------
| Nombre | `person.name.firstName` |
| Apellidos | `person.name.lastName` |
| Teléfono | `mobilePhone.number` |
| Ciudad de la dirección | `homeAddress.city` |
| Estado de la dirección | `homeAddress.stateProvince` |
| Código postal de la dirección | `homeAddress.postalCode` |
| Cumpleaños | `person.birthDayAndMonth` |
| Pertenencia a segmentos | `segmentMembership.status` |

## Importar datos desde la ubicación de almacenamiento en el destino

Consulte los artículos de destino de marketing por correo electrónico para obtener información sobre cómo importar datos de su ubicación de almacenamiento en destinos:

- [Adobe Campaign](./adobe-campaign.md#import-data-into-campaign)
- [Oracle Eloqua](./oracle-eloqua.md#import-data-into-eloqua)
- [Responsys de oracle](./oracle-responsys.md#import-data-into-responsys)
- [Marketing Cloud de Salesforce](./salesforce-marketing-cloud.md#import-data-into-salesforce)

## Activar segmentos en destinos de marketing por correo electrónico

Para obtener instrucciones sobre cómo activar segmentos en destinos de marketing de correo electrónico, consulte [Activar datos en destinos](../../ui/activate-destinations.md).

## Recursos adicionales

- [Activar datos en destinos](../../ui/activate-destinations.md)
- [Cree destinos de marketing por correo electrónico y active los datos mediante la API de servicio de flujo](../../api/email-marketing.md)