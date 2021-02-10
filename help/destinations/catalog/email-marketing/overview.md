---
keywords: correo electrónico;correo electrónico;correo electrónico;destinos de correo electrónico
title: Introducción a los destinos de mercadotecnia por correo electrónico
type: Tutorial
description: Los Proveedores de servicio de correo electrónico (ESP) le permiten administrar sus actividades de mercadotecnia por correo electrónico, por ejemplo, para enviar campañas de correo electrónico promocionales.
translation-type: tm+mt
source-git-commit: e13a19640208697665b0a7e0106def33fd1e456d
workflow-type: tm+mt
source-wordcount: '791'
ht-degree: 1%

---


# Información general sobre los destinos de mercadotecnia de correo electrónico {#email-marketing-destinations}

Los Proveedores de servicio de correo electrónico (ESP) le permiten administrar sus actividades de marketing por correo electrónico, como el envío de campañas de correo electrónico promocionales. Adobe Experience Platform se integra con ESP permitiéndole activar segmentos en destinos de marketing por correo electrónico.

Para enviar segmentos a destinos de marketing por correo electrónico para sus campañas, primero Platform debe conectarse al destino.

La conexión a destinos de marketing por correo electrónico es un proceso de tres pasos. Cada uno de los pasos se describe más abajo en esta página.

En el flujo de destino de conexión, descrito en la sección siguiente, conéctese a Amazon S3 o SFTP. Platform exporta los segmentos como `.csv` o `.txt` archivos y los envía a la ubicación que prefiera. Programe la importación de datos en la plataforma de marketing por correo electrónico desde la ubicación de almacenamiento habilitada en Plataforma. El proceso de importación de datos varía según el socio. Consulte los artículos de destinos individuales para obtener más información.

## Configurar destino {#connect-destination}

En **[!UICONTROL Conexiones]** > **[!UICONTROL Destinos]**, seleccione el destino de mercadotecnia de correo electrónico al que desea conectarse y, a continuación, seleccione **[!UICONTROL Configurar]**.

![Conectar al destino](../../assets/catalog/email-marketing/overview/connect-email-marketing.png)

En el paso **[!UICONTROL Autenticación]**, si anteriormente había configurado una conexión con el destino de mercadotecnia de correo electrónico, seleccione **[!UICONTROL Cuenta existente]** y seleccione la conexión existente. O bien, puede seleccionar **[!UICONTROL Nueva cuenta]** para configurar una nueva conexión con su destino de mercadotecnia de correo electrónico. En el selector **[!UICONTROL Tipo de conexión]**, puede seleccionar entre Amazon S3, SFTP con contraseña o SFTP con clave SSH. Rellene la información siguiente, según el tipo de conexión, luego seleccione **[!UICONTROL Conectar]**.

- Para las conexiones **S3**, debe proporcionar el ID de clave de acceso de Amazon y la clave de acceso secreto.
- Para conexiones **SFTP con contraseña**, debe proporcionar dominio, puerto, nombre de usuario y contraseña para el servidor SFTP.
- Para conexiones **SFTP con clave SSH**, debe proporcionar dominio, puerto, nombre de usuario y clave SSH para el servidor SFTP.

Opcionalmente, puede adjuntar su clave pública con formato RSA para agregar cifrado a los archivos exportados en la sección **[!UICONTROL Clave]**. Tenga en cuenta que esta clave pública **debe** escribirse como una cadena con codificación Base64.

En el paso **[!UICONTROL Configuración]**, escriba un nombre y una descripción para el nuevo destino, así como el formato de archivo para los archivos exportados.

Si seleccionó Amazon S3 como opción de almacenamiento en el paso anterior, inserte el nombre del bucket y la ruta de la carpeta en el destino de almacenamiento en la nube donde se enviarán los archivos. Para la opción almacenamiento SFTP, inserte la ruta de la carpeta en la que se enviarán los archivos.

También en este paso puede seleccionar cualquier caso de uso de mercadotecnia que deba aplicarse a este destino. Los casos de uso de mercadotecnia indican la intención para la cual se exportarán los datos al destino. Puede seleccionar entre los casos de uso de mercadotecnia definidos por el Adobe o puede crear su propio caso de uso de mercadotecnia. Para obtener más información acerca de los casos de uso de mercadotecnia, consulte la [información general de las directivas de uso de datos](../../../data-governance/policies/overview.md).

![Paso de configuración de correo electrónico](../../assets/catalog/email-marketing/overview/email-setup-step.png)

## Seleccione qué miembros de segmento incluir en las exportaciones de destino {#select-segments}

En la página **[!UICONTROL Seleccionar segmentos]**, seleccione qué segmentos enviar al destino. Encontrará más información sobre los campos en las secciones siguientes.

![Seleccionar segmentos](../../assets/common/email-select-segments.png)

## Configurar nombres de archivo

Para obtener más información sobre la programación de segmentos y las opciones de edición de nombres de archivo, consulte el paso [Configurar](../../ui/activate-destinations.md#configure) en el tutorial de activación de destinos.

## Seleccionar atributos: seleccione los campos de esquema que desea utilizar como atributos de destino en los archivos exportados {#destination-attributes}

En este paso, se seleccionan los campos que se van a exportar a destinos de marketing por correo electrónico y se marcan los campos obligatorios.

![Atributos de destino](../../assets/catalog/email-marketing/overview/recommended-attributes.png)

Para obtener más información sobre este paso, consulte el paso [Seleccionar atributos](../../ui/activate-destinations.md#select-attributes) en el tutorial de activación de destinos.

### Identidad {#identity}

Le recomendamos que seleccione un identificador único del esquema de [unión](../../../profile/home.md#profile-fragments-and-union-schemas). Este es el campo en el que se definen las identidades de los usuarios. Normalmente, este campo es la dirección de correo electrónico, pero también puede ser un ID de programa de lealtad o un número de teléfono. Consulte la tabla siguiente para ver los identificadores únicos más comunes y su campo XDM en el esquema.

| Identificador único | Campo XDM en Esquema unificado |
----------------- | ---------------------------
| Dirección de correo electrónico | `personalEmail.address` |
| Phone | `mobilePhone.number` |
| ID de programa de lealtad | `Customer-defined XDM field` |

### Otros atributos de destino

En el selector de campos de Esquema, elija qué otros campos desea exportar al destino de correo electrónico. Algunas opciones recomendadas son:

| Esquema | Campo XDM |
------ | ---------
| Nombre | `person.name.firstName` |
| Apellidos | `person.name.lastName` |
| Teléfono | `mobilePhone.number` |
| Ciudad de dirección | `homeAddress.city` |
| Estado de la dirección | `homeAddress.stateProvince` |
| Dirección Código postal | `homeAddress.postalCode` |
| Cumpleaños | `person.birthDayAndMonth` |
| Membresía del segmento | `segmentMembership.status` |

## Importar datos desde la ubicación del almacenamiento al destino

Consulte los artículos de destino de marketing por correo electrónico individuales para obtener información sobre cómo importar datos de la ubicación del almacenamiento a los destinos:

- [Adobe Campaign](./adobe-campaign.md#import-data-into-campaign)
- [Oracle Eloqua](./oracle-eloqua.md#import-data-into-eloqua)
- [Oracle Responsys](./oracle-responsys.md#import-data-into-responsys)
- [Marketing Cloud de Salesforce](./salesforce-marketing-cloud.md#import-data-into-salesforce)

## Activar segmentos en destinos de mercadotecnia de correo electrónico

Para obtener instrucciones sobre cómo activar segmentos en destinos de mercadotecnia de correo electrónico, consulte [Activar datos en destinos](../../ui/activate-destinations.md).

## Recursos adicionales

- [Activar datos en destinos](../../ui/activate-destinations.md)
- [Creación de destinos de marketing por correo electrónico y activación de datos mediante la API de servicio de flujo](../../api/email-marketing.md)