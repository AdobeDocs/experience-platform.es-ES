---
keywords: correo electrónico;Correo electrónico;correo electrónico;destinos de correo electrónico;destino de oracle responsys
title: Conexión de Oracle Responsys
description: Responsys es una herramienta de marketing por correo electrónico empresarial para campañas de marketing entre canales que ofrece Oracle para personalizar las interacciones entre correo electrónico, móvil, pantalla y redes sociales.
exl-id: 70f2f601-afee-4315-bf7a-ed2c92397ebe
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '659'
ht-degree: 3%

---

# [!DNL Oracle Responsys] conexión

## Información general {#overview}

[Responsys](https://www.oracle.com/cx/marketing/campaign-management/) es una herramienta de marketing por correo electrónico empresarial para campañas de marketing entre canales ofrecida por [!DNL Oracle] para personalizar interacciones entre correo electrónico, móvil, pantalla y redes sociales.

Para enviar datos de audiencia a [!DNL Oracle Responsys], primero debe [conectarse al destino](#connect-destination) en Adobe Experience Platform y luego [configurar una importación de datos](#import-data-into-responsys) desde su ubicación de almacenamiento en [!DNL Oracle Responsys].

## Audiencias compatibles {#supported-audiences}

Esta sección describe qué tipos de audiencias puede exportar a este destino.

| Origen de audiencia | Admitido | Descripción |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Audiencias generadas a través del [servicio de segmentación](../../../segmentation/home.md) de Experience Platform. |
| Cargas personalizadas | ✓ | Las audiencias [importadas](../../../segmentation/ui/audience-portal.md#import-audience) en Experience Platform desde archivos CSV. |

{style="table-layout:auto"}

## Tipo y frecuencia de exportación {#export-type-frequency}

Consulte la tabla siguiente para obtener información sobre el tipo y la frecuencia de exportación de destino.

| Elemento | Tipo | Notas |
|---------|----------|---------|
| Tipo de exportación | **[!UICONTROL Profile-based]** | Va a exportar todos los miembros de un segmento, junto con los campos de esquema deseados (por ejemplo: dirección de correo electrónico, número de teléfono, apellidos), tal como se eligió en la pantalla Seleccionar atributos de perfil del [flujo de trabajo de activación de destino](../../ui/activate-batch-profile-destinations.md#select-attributes). |
| Frecuencia de exportación | **[!UICONTROL Batch]** | Los destinos por lotes exportan archivos a plataformas descendentes en incrementos de tres, seis, ocho, doce o veinticuatro horas. Obtenga más información sobre [destinos basados en archivos por lotes](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## LISTA DE PERMITIDOS de direcciones IP {#allow-list}

Al configurar destinos de marketing por correo electrónico con almacenamiento SFTP, Adobe recomienda añadir determinados rangos de IP a la lista de permitidos.

Consulte la [lista de permitidos de direcciones IP para destinos SFTP](../cloud-storage/ip-address-allow-list.md) si necesita agregar direcciones IP de Adobe a la lista de permitidos.

## Conectar con el destino {#connect}

>[!IMPORTANT]
> 
>Para conectarse al destino, necesita los **[!UICONTROL View Destinations]** y **[!UICONTROL Manage Destinations]** [permisos de control de acceso](/help/access-control/home.md#permissions). Lea la [descripción general del control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Para conectarse a este destino, siga los pasos descritos en el [tutorial de configuración de destino](../../ui/connect-destination.md).

Este destino admite los siguientes tipos de conexión:

* **[!UICONTROL SFTP with Password]**
* **[!UICONTROL SFTP with SSH Key]**

### Parámetros de conexión {#parameters}

Mientras [configura](../../ui/connect-destination.md) este destino, debe proporcionar la siguiente información:

* Para las conexiones de **[!UICONTROL SFTP with Password]**, debe proporcionar:
   * [!UICONTROL Domain]
   * [!UICONTROL Port]
   * [!UICONTROL Username]
   * [!UICONTROL Password]
* Para las conexiones de **[!UICONTROL SFTP with SSH Key]**, debe proporcionar:
   * [!UICONTROL Domain]
   * [!UICONTROL Port]
   * [!UICONTROL Username]
   * [!UICONTROL SSH Key]
* Opcionalmente, puede adjuntar la clave pública con formato RSA para agregar cifrado con PGP/GPG a los archivos exportados en la sección **[!UICONTROL Key]**. La clave pública debe escribirse como una cadena con codificación [!DNL Base64].
* **[!UICONTROL Name]**: elige un nombre relevante para tu destino.
* **[!UICONTROL Description]**: escriba una descripción para el destino.
* **[!UICONTROL Folder Path]**: proporcione la ruta de acceso a la ubicación de almacenamiento en la que Experience Platform depositará los datos exportados como archivos CSV.
* **[!UICONTROL File Format]**: seleccione **CSV** para exportar archivos CSV a su ubicación de almacenamiento.

<!--

Commenting out Amazon S3 bucket part for now until support is clarified

- **[!UICONTROL Bucket name]**: Your Amazon S3 bucket, where Experience Platform will deposit the data export. Your input must be between 3 and 63 characters long. Must begin and end with a letter or number. Must contain only lowercase letters, numbers, or hyphens ( - ). Must not be formatted as an IP address (for example, 192.100.1.1).

-->

### Habilitar alertas {#enable-alerts}

Puede activar alertas para recibir notificaciones sobre el estado del flujo de datos a su destino. Seleccione una alerta de la lista a la que suscribirse para recibir notificaciones sobre el estado del flujo de datos. Para obtener más información sobre las alertas, consulte la guía sobre [suscripción a alertas de destinos mediante la interfaz de usuario](../../ui/alerts.md).

Cuando termine de proporcionar detalles para la conexión de destino, seleccione **[!UICONTROL Next]**.

## Activar públicos en este destino {#activate}

>[!IMPORTANT]
> 
>* Para activar los datos, necesita los permisos de control de acceso **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** y **[!UICONTROL View Segments]** [5&rbrace;. &#x200B;](/help/access-control/home.md#permissions) Lea la [descripción general del control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.
>* Para exportar *identidades*, necesita el **[!UICONTROL View Identity Graph]** [permiso de control de acceso](/help/access-control/home.md#permissions). <br> ![Seleccione el área de nombres de identidad resaltada en el flujo de trabajo para activar audiencias en los destinos.](/help/destinations/assets/overview/export-identities-to-destination.png "Seleccione el área de nombres de identidad resaltada en el flujo de trabajo para activar audiencias en los destinos."){width="100" zoomable="yes"}

Consulte [Activar datos de audiencia en destinos de exportación de perfiles por lotes](../../ui/activate-batch-profile-destinations.md) para obtener instrucciones sobre cómo activar audiencias en este destino.

### Atributos de destino {#destination-attributes}

Al activar audiencias en este destino, Adobe recomienda que seleccione un identificador único de su [esquema de unión](../../../profile/home.md#profile-fragments-and-union-schemas). Seleccione el identificador único y cualquier otro campo XDM que desee exportar al destino. Para obtener más información, consulte [prácticas recomendadas al activar audiencias en destinos de marketing por correo electrónico](overview.md#best-practices).

## Datos exportados {#exported-data}

Para [!DNL Oracle Responsys] destinos, Experience Platform crea un archivo de `.csv` en la ubicación de almacenamiento proporcionada. Para obtener más información sobre los archivos, consulte [comprobar la activación de la audiencia](../../ui/activate-batch-profile-destinations.md#verify) en el tutorial de activación de audiencia.

## Configurar la importación de datos en [!DNL Oracle Responsys] {#import-data-into-responsys}

Después de conectar [!DNL Experience Platform] a su almacenamiento de [!DNL SFTP], debe configurar la importación de datos desde su ubicación de almacenamiento en [!DNL Oracle Responsys]. Para obtener información sobre cómo hacerlo, consulte [Importación de contactos o cuentas](https://docs.oracle.com/cloud/latest/marketingcs_gs/OMCEA/Connect_WizardUpload.htm) en [!DNL Oracle Responsys Help Center].
