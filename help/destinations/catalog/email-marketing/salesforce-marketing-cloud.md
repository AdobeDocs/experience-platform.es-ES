---
keywords: correo electrónico;correo electrónico;destinos de correo electrónico;salesforce;destino de salesforce
title: Conexión de Marketing Cloud de Salesforce
seo-description: Salesforce Marketing Cloud is a digital marketing suite formerly known as ExactTarget that allows you to build and customize journeys for visitors and customers to personalize their experience.
exl-id: e85049a7-eaed-4f8a-b670-9999d56928f8
source-git-commit: b4810dfef7b0d437744ca14a32bd4f5746e8d002
workflow-type: tm+mt
source-wordcount: '459'
ht-degree: 1%

---

# [!DNL Salesforce Marketing Cloud] connection

## Información general {#overview}

[[!DNL Salesforce Marketing Cloud]](https://www.salesforce.com/products/marketing-cloud/email-marketing/) es un grupo de marketing digital anteriormente conocido como ExactTarget que le permite crear y personalizar recorridos para que los visitantes y clientes personalicen su experiencia.

Para enviar datos de segmentos a [!DNL Salesforce Marketing Cloud], primero debe [conectar el destino](#connect-destination) en Platform y, a continuación, [configuración de una importación de datos](#import-data-into-salesforce) desde su ubicación de almacenamiento a [!DNL Salesforce Marketing Cloud].

## Tipo de exportación {#export-type}

**Basado en perfiles** - está exportando todos los miembros de un segmento, junto con los campos de esquema deseados (por ejemplo: dirección de correo electrónico, número de teléfono, apellidos), tal y como se elige en la pantalla de atributos seleccionados del [flujo de trabajo de activación de audiencia](../../ui/activate-batch-profile-destinations.md#select-attributes).

## LISTA DE PERMITIDOS de direcciones IP {#allow-list}

Al configurar destinos de marketing por correo electrónico con almacenamiento SFTP, Adobe recomienda que agregue ciertos rangos de IP a la lista de permitidos.

Consulte [LISTA DE PERMITIDOS de direcciones IP para destinos de almacenamiento en la nube](../cloud-storage/ip-address-allow-list.md) si necesita agregar direcciones IP de Adobe a su lista de permitidos.

## Conectarse al destino {#connect}

Para conectarse a este destino, siga los pasos descritos en la sección [tutorial de configuración de destino](../../ui/connect-destination.md).

Este destino admite los siguientes tipos de conexión:

* **[!UICONTROL SFTP con contraseña]**
* **[!UICONTROL SFTP con clave SSH]**

### Parámetros de conexión {#parameters}

While [configuración](../../ui/connect-destination.md) Para este destino, debe proporcionar la siguiente información:

* Para **[!UICONTROL SFTP con contraseña]** conexiones, debe proporcionar:
   * [!UICONTROL Dominio]
   * [!UICONTROL Puerto]
   * [!UICONTROL Nombre de usuario]
   * [!UICONTROL Contraseña]
* Para **[!UICONTROL SFTP con clave SSH]** conexiones, debe proporcionar:
   * [!UICONTROL Dominio]
   * [!UICONTROL Puerto]
   * [!UICONTROL Nombre de usuario]
   * [!UICONTROL Clave SSH]

* Opcionalmente, puede adjuntar su clave pública con formato RSA para agregar cifrado con PGP/GPG a los archivos exportados en el **[!UICONTROL Clave]** para obtener más información. La clave pública debe escribirse como un [!DNL Base64] cadena codificada.
* **[!UICONTROL Nombre]**: Elija un nombre relevante para el destino.
* **[!UICONTROL Descripción]**: Escriba una descripción para el destino.
* **[!UICONTROL Ruta de carpeta]**: Proporcione la ruta en su ubicación de almacenamiento donde Platform depositará los datos de exportación como archivos CSV.
* **[!UICONTROL Formato del archivo]**: **CSV** o **TAB_DELIMITED**. Seleccione el formato de archivo que desea exportar a su ubicación de almacenamiento.

<!--

Commenting out Amazon S3 bucket part for now until support is clarified

- **[!UICONTROL Bucket name]**: Your Amazon S3 bucket, where Platform will deposit the data export. Your input must be between 3 and 63 characters long. Must begin and end with a letter or number. Must contain only lowercase letters, numbers, or hyphens ( - ). Must not be formatted as an IP address (for example, 192.100.1.1).

-->

## Activar segmentos en este destino {#activate}

Consulte [Activar datos de audiencia en destinos de exportación de perfiles en lote](../../ui/activate-batch-profile-destinations.md) para obtener instrucciones sobre la activación de segmentos de audiencia en este destino.

### Atributos de destino {#destination-attributes}

Al activar segmentos en este destino, Adobe recomienda que seleccione un identificador único de su [esquema de unión](../../../profile/home.md#profile-fragments-and-union-schemas). Seleccione el identificador único y cualquier otro campo XDM que desee exportar al destino. Para obtener más información, consulte [prácticas recomendadas al activar audiencias en destinos de marketing por correo electrónico](overview.md#best-practices).

## Datos exportados {#exported-data}

Para [!DNL Salesforce Marketing Cloud] destinos, Platform crea un `.csv` en la ubicación de almacenamiento proporcionada. Para obtener más información sobre los archivos, consulte [verificar activación de segmentos](../../ui/activate-batch-profile-destinations.md#verify) en el tutorial de activación de segmentos.

## Configurar la importación de datos en [!DNL Salesforce Marketing Cloud] {#import-data-into-salesforce}

Después de conectar [!DNL Platform] a su [!DNL SFTP] , debe configurar la importación de datos desde la ubicación de almacenamiento en [!DNL Salesforce Marketing Cloud]. Para obtener información sobre cómo hacerlo, consulte [Importación de suscriptores a Marketing Cloud desde un archivo](https://help.salesforce.com/articleView?id=mc_es_import_subscribers_from_file.htm&amp;type=5) en el [!DNL Salesforce Help Center].
