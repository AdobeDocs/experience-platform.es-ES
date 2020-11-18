---
keywords: email;Email;e-mail;email destinations
title: Destinos de mercadotecnia de correo electrónico
seo-title: Destinos de mercadotecnia de correo electrónico
type: Tutorial
description: Los Proveedores de servicio de correo electrónico (ESP) le permiten administrar sus actividades de mercadotecnia por correo electrónico, por ejemplo, para enviar campañas de correo electrónico promocionales.
seo-description: Los Proveedores de servicio de correo electrónico (ESP) le permiten administrar sus actividades de mercadotecnia por correo electrónico, por ejemplo, para enviar campañas de correo electrónico promocionales.
translation-type: tm+mt
source-git-commit: 425287d78deebf0113d6cf6350bcb516c99ee995
workflow-type: tm+mt
source-wordcount: '838'
ht-degree: 1%

---


# Destinos de mercadotecnia de correo electrónico {#email-marketing-destinations}

Los Proveedores de servicio de correo electrónico (ESP) le permiten administrar sus actividades de marketing por correo electrónico, como el envío de campañas de correo electrónico promocionales. La plataforma de datos del cliente en tiempo real de Adobe se integra con los ESP permitiéndole activar segmentos en destinos de marketing por correo electrónico.

Para enviar segmentos a destinos de marketing por correo electrónico para sus campañas, CDP en tiempo real de Adobe primero debe conectarse al destino.

La conexión a destinos de marketing por correo electrónico es un proceso de tres pasos. Cada uno de los pasos se describe más abajo en esta página.

En el flujo de destino de conexión, descrito en la sección siguiente, conéctese a Amazon S3 o SFTP. CDP en tiempo real exporta sus segmentos como `.csv` `.txt` o como archivos y los envía a su ubicación preferida. Programe la importación de datos en su plataforma de marketing por correo electrónico desde la ubicación de almacenamiento habilitada en CDP en tiempo real. El proceso de importación de datos varía según el socio. Consulte los artículos de destinos individuales para obtener más información.

## Configurar destino {#connect-destination}

En **[!UICONTROL Conexiones]** > **[!UICONTROL Destinos]**, seleccione el destino de marketing por correo electrónico al que desea conectarse y, a continuación, seleccione **[!UICONTROL Configurar]**.

![Conectar al destino](./assets/connect-email-marketing.png)

En el paso **[!UICONTROL Autenticación]** , si ya ha configurado una conexión con el destino de marketing por correo electrónico, seleccione Cuenta **** existente y seleccione la conexión existente. O bien, puede seleccionar **[!UICONTROL Nueva cuenta]** para configurar una nueva conexión con su destino de marketing por correo electrónico. En el selector de tipo **** de conexión, puede seleccionar entre Amazon S3, SFTP con contraseña o SFTP con clave SSH. Rellene la información siguiente, según el tipo de conexión y, a continuación, seleccione **[!UICONTROL Connect]**.

- Para las conexiones **** S3, debe proporcionar el ID de clave de acceso de Amazon y la clave de acceso secreto.
- Para **SFTP con conexiones de contraseña** , debe proporcionar dominio, puerto, nombre de usuario y contraseña para el servidor SFTP.
- Para **SFTP con conexiones SSH Key** , debe proporcionar Dominio, Puerto, Nombre de usuario y Clave SSH para el servidor SFTP.

Opcionalmente, puede adjuntar su clave pública con formato RSA para agregar encriptación a sus archivos exportados en la sección **[!UICONTROL Clave]** . Tenga en cuenta que esta clave pública **debe** escribirse como una cadena con codificación Base64.

En el paso **[!UICONTROL Configuración]** , introduzca un nombre y una descripción para el nuevo destino, así como el formato de archivo para los archivos exportados.

Si seleccionó Amazon S3 como opción de almacenamiento en el paso anterior, inserte el nombre del bucket y la ruta de la carpeta en el destino de almacenamiento en la nube donde se enviarán los archivos. Para la opción almacenamiento SFTP, inserte la ruta de la carpeta en la que se enviarán los archivos.

También en este paso, puede seleccionar cualquier caso de uso de mercadotecnia que deba aplicarse a este destino. Los casos de uso de mercadotecnia indican la intención para la cual se exportarán los datos al destino. Puede seleccionar entre los casos de uso de mercadotecnia definidos por el Adobe o puede crear su propio caso de uso de mercadotecnia. Para obtener más información sobre los casos de uso de mercadotecnia, consulte la página [Administración de datos en tiempo real de CDP](/help/rtcdp/privacy/data-governance-overview.md#destinations) . Para obtener información sobre los casos individuales de uso de mercadotecnia definidos por el Adobe, consulte la descripción general [de las políticas de uso de](/help/data-governance/policies/overview.md#core-actions)datos.

![Paso de configuración de correo electrónico](./assets/email-setup-step.png)

## Seleccione qué miembros de segmento incluir en las exportaciones de destino {#select-segments}

En la página **[!UICONTROL Seleccionar segmentos]** , seleccione qué segmentos enviar al destino. Encontrará más información sobre los campos en las secciones siguientes.

![Seleccionar segmentos](/help/rtcdp/destinations/assets/email-select-segments.png)

## Configurar nombres de archivo

Para obtener información sobre la programación de segmentos y las opciones de edición de nombres de archivo, consulte el paso [Configurar](/help/rtcdp/destinations/activate-destinations.md#configure) del tutorial de activación de destinos.

## Seleccionar atributos: seleccione los campos de esquema que desea utilizar como atributos de destino en los archivos exportados {#destination-attributes}

En este paso, se seleccionan los campos que se van a exportar a destinos de marketing por correo electrónico y se marcan los campos obligatorios.

![Atributos de destino](/help/rtcdp/destinations/assets/recommended-attributes.png)

Para obtener más información sobre este paso, consulte el paso [Seleccionar atributos](/help/rtcdp/destinations/activate-destinations.md#select-attributes) en el tutorial de activación de destinos.

### Identidad {#identity}

Le recomendamos que seleccione un identificador único en el esquema [de](../../profile/home.md#profile-fragments-and-union-schemas)unión. Este es el campo en el que se definen las identidades de los usuarios. Normalmente, este campo es la dirección de correo electrónico, pero también puede ser un ID de programa de lealtad o un número de teléfono. Consulte la tabla siguiente para ver los identificadores únicos más comunes y su campo XDM en el esquema.

| Identificador único | Campo XDM en Esquema unificado |
---------|----------
| Dirección de correo electrónico | `personalEmail.address` |
| Phone | `mobilePhone.number` |
| ID de programa de lealtad | `Customer-defined XDM field` |

### Otros atributos de destino

En el selector de campos de Esquema, elija qué otros campos desea exportar al destino de correo electrónico. Algunas opciones recomendadas son:

| Esquema | Campo XDM |
---------|----------
| Nombre | `person.name.firstName` |
| Apellidos | `person.name.lastName` |
| Phone | `mobilePhone.number` |
| Ciudad de dirección | `homeAddress.city` |
| Estado de la dirección | `homeAddress.stateProvince` |
| Dirección Código postal | `homeAddress.postalCode` |
| Cumpleaños | `person.birthDayAndMonth` |
| Membresía del segmento | `segmentMembership.status` |

## Importar datos desde la ubicación del almacenamiento al destino

Consulte los artículos de destino de marketing por correo electrónico individuales para obtener información sobre cómo importar datos de la ubicación del almacenamiento a los destinos:

- [Adobe Campaign](/help/rtcdp/destinations/adobe-campaign-destination.md#import-data-into-campaign)
- [Marketing Cloud de Salesforce](/help/rtcdp/destinations/salesforce-marketing-cloud-destination.md#import-data-into-salesforce)
- [Oracle Eloqua](/help/rtcdp/destinations/oracle-eloqua-destination.md#import-data-into-eloqua)
- [Oracle Responsys](/help/rtcdp/destinations/oracle-responsys-destination.md#import-data-into-responsys)

## Activar segmentos en destinos de mercadotecnia de correo electrónico

Para obtener instrucciones sobre cómo activar segmentos en destinos de marketing de correo electrónico, consulte [Activar datos en destinos](/help/rtcdp/destinations/activate-destinations.md).

## Recursos adicionales

- [Activar datos en destinos](/help/rtcdp/destinations/activate-destinations.md)
- [Creación de destinos de marketing por correo electrónico y activación de datos mediante la API de servicio de flujo](https://docs.adobe.com/content/help/en/experience-platform/tutorials/destinations/email-marketing-api.html)