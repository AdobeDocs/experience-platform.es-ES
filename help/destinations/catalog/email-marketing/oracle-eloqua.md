---
keywords: correo electrónico;correo electrónico;destinos de correo electrónico;eloqua de oracle;oracle
title: Conexión oracle Eloqua
description: Oracle Eloqua es una plataforma de software como servicio (SaaS) para la automatización de marketing que ofrece Oracle y que tiene como objetivo ayudar a los especialistas en marketing B2B y a las organizaciones a administrar las campañas de marketing y la generación de posibles clientes de ventas.
exl-id: 6eaa79ff-8874-423b-bdff-aa04f6101a53
source-git-commit: 15ea3ab9370541c35b874414a8753e8812eea9c6
workflow-type: tm+mt
source-wordcount: '500'
ht-degree: 1%

---

# [!DNL Oracle Eloqua] connection

[[!DNL Oracle Eloqua]](https://www.oracle.com/cx/marketing/automation/) es una plataforma de software como servicio (SaaS) para la automatización de marketing ofrecida por  [!DNL Oracle] que tiene como objetivo ayudar a los especialistas en marketing B2B y a las organizaciones a administrar las campañas de marketing y la generación de posibles clientes de ventas.

Para enviar datos de segmentos a [!DNL Oracle Eloqua], primero debe [conectar el destino](#connect-destination) en Adobe Experience Platform y luego [configurar una importación de datos](#import-data-into-eloqua) desde la ubicación de almacenamiento a [!DNL Oracle Eloqua].

## Tipo de exportación {#export-type}

**Basado en perfiles** : exporta todos los miembros de un segmento, junto con los campos de esquema deseados (por ejemplo: dirección de correo electrónico, número de teléfono y apellidos), tal como se elige en la pantalla de selección de atributos del flujo de trabajo de activación de  [destino](../../ui/activate-destinations.md#select-attributes).

## LISTA DE PERMITIDOS de direcciones IP {#allow-list}

Al configurar destinos de marketing por correo electrónico con almacenamiento SFTP, Adobe recomienda que agregue ciertos rangos de IP a la lista de permitidos.

Consulte la [lista de permitidos de direcciones IP para destinos de almacenamiento en la nube](../cloud-storage/ip-address-allow-list.md) si necesita agregar IP de Adobe a su lista de permitidos.

## Conectarse al destino {#connect}

Para conectarse a este destino, siga los pasos descritos en el [tutorial de configuración de destino](../../ui/connect-destination.md).

Este destino admite los siguientes tipos de conexión:

* **[!UICONTROL SFTP con contraseña]**
* **[!UICONTROL SFTP con clave SSH]**

### Parámetros de conexión {#parameters}

Mientras [configura](../../ui/connect-destination.md) este destino, debe proporcionar la siguiente información:

* Para conexiones **[!UICONTROL SFTP con contraseña]**, debe proporcionar:
   * [!UICONTROL Dominio]
   * [!UICONTROL Puerto]
   * [!UICONTROL Nombre de usuario]
   * [!UICONTROL Contraseña]
* Para conexiones **[!UICONTROL SFTP con clave SSH]**, debe proporcionar:
   * [!UICONTROL Dominio]
   * [!UICONTROL Puerto]
   * [!UICONTROL Nombre de usuario]
   * [!UICONTROL Clave SSH]

* Opcionalmente, puede adjuntar su clave pública con formato RSA para agregar cifrado con PGP/GPG a los archivos exportados en la sección **[!UICONTROL Clave]**. La clave pública debe escribirse como una cadena codificada [!DNL Base64].
* **[!UICONTROL Nombre]**: Elija un nombre relevante para el destino.
* **[!UICONTROL Descripción]**: Escriba una descripción para el destino.
* **[!UICONTROL Ruta]** de carpeta: Proporcione la ruta en su ubicación de almacenamiento donde Platform depositará sus datos de exportación como archivos CSV o delimitados por tabuladores.
* **[!UICONTROL Formato]** de archivo:  **** CSVo  **TAB_DELIMITED**. Seleccione el formato de archivo que desea exportar a su ubicación de almacenamiento.

<!--

Commenting out Amazon S3 bucket part for now until support is clarified

- **[!UICONTROL Bucket name]**: Your Amazon S3 bucket, where Platform will deposit the data export. Your input must be between 3 and 63 characters long. Must begin and end with a letter or number. Must contain only lowercase letters, numbers, or hyphens ( - ). Must not be formatted as an IP address (for example, 192.100.1.1).

-->

## Activar segmentos en este destino {#activate}

Consulte [Activar perfiles y segmentos en un destino](../../ui/activate-destinations.md) para obtener instrucciones sobre cómo activar segmentos de audiencia en destinos.

## Atributos de destino {#destination-attributes}

Al [activar segmentos](../../ui/activate-destinations.md) en este destino, Adobe recomienda que seleccione un identificador único de su [esquema de unión](../../../profile/home.md#profile-fragments-and-union-schemas). Seleccione el identificador único y cualquier otro campo XDM que desee exportar al destino. Para obtener más información, consulte [Seleccionar qué campos de esquema utilizar como atributos de destino en los archivos exportados](./overview.md#destination-attributes).

## Datos exportados {#exported-data}

Para destinos [!DNL Oracle Eloqua], Platform crea un archivo `.csv` delimitado por tabuladores en la ubicación de almacenamiento proporcionada. Para obtener más información sobre los archivos, consulte [Destinos de marketing por correo electrónico y destinos de almacenamiento en la nube](../../ui/activate-destinations.md#esp-and-cloud-storage) en el tutorial de activación de segmentos.

## Configurar la importación de datos en [!DNL Oracle Eloqua] {#import-data-into-eloqua}

Después de conectar [!DNL Platform] al almacenamiento [!DNL SFTP], debe configurar la importación de datos desde su ubicación de almacenamiento en [!DNL Oracle Eloqua]. Para obtener información sobre cómo lograr esto, consulte [Importación de contactos o cuentas](https://docs.oracle.com/cloud/latest/marketingcs_gs/OMCAA/Help/DataImportExport/Tasks/ImportingContactsOrAccounts.htm) en [!DNL Oracle Eloqua Help Center].
