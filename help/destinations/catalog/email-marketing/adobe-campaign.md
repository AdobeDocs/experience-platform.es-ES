---
keywords: correo electrónico;correo electrónico;correo electrónico;destinos de correo electrónico;adobe campaign;campaign
title: Conexión de Adobe Campaign
description: Adobe Campaign es un conjunto de soluciones que le ayudan a personalizar y entregar campañas en todos sus canales con y sin conexión.
exl-id: 0de91738-8f56-41f5-8745-9b14b15db76a
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '906'
ht-degree: 5%

---

# Conexión de Adobe Campaign

## Información general {#overview}

Adobe Campaign es un conjunto de soluciones que le ayudan a personalizar y entregar campañas en todos sus canales en línea y sin conexión. Consulte [Introducción a Campaign Classic](https://experienceleague.adobe.com/docs/campaign-classic/using/getting-started/starting-with-adobe-campaign/about-adobe-campaign-classic.html) para obtener más información.

Para enviar datos de audiencia a Adobe Campaign, primero debe [conectar el destino](#connect-destination) en Adobe Experience Platform y, a continuación, [configurar una importación de datos](#import-data-into-campaign) desde su ubicación de almacenamiento en Adobe Campaign.

## Audiencias compatibles {#supported-audiences}

Esta sección describe qué tipos de audiencias puede exportar a este destino.

| Origen de audiencia | Admitido | Descripción |
| ---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Audiencias generadas a través del [servicio de segmentación](../../../segmentation/home.md) de Experience Platform. |
| Cargas personalizadas | ✓ | Las audiencias [importadas](../../../segmentation/ui/audience-portal.md#import-audience) en Experience Platform desde archivos CSV. |

{style="table-layout:auto"}

## Tipo y frecuencia de exportación {#export-type-frequency}

Consulte la tabla siguiente para obtener información sobre el tipo y la frecuencia de exportación de destino.

| Elemento | Tipo | Notas |
---------|----------|---------|
| Tipo de exportación | **[!UICONTROL Basado en perfil]** | Va a exportar todos los miembros de un segmento, junto con los campos de esquema deseados (por ejemplo: dirección de correo electrónico, número de teléfono, apellidos), tal como se eligió en la pantalla Seleccionar atributos de perfil del [flujo de trabajo de activación de destino](../../ui/activate-batch-profile-destinations.md#select-attributes). |
| Frecuencia de exportación | **[!UICONTROL Lote]** | Los destinos por lotes exportan archivos a plataformas descendentes en incrementos de tres, seis, ocho, doce o veinticuatro horas. Obtenga más información sobre [destinos basados en archivos por lotes](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## LISTA DE PERMITIDOS de direcciones IP {#allow-list}

Al configurar destinos de marketing por correo electrónico con almacenamiento SFTP, Adobe recomienda añadir determinados rangos de IP a la lista de permitidos.

Consulte la [lista de permitidos de direcciones IP para destinos SFTP](../cloud-storage/ip-address-allow-list.md) si necesita agregar direcciones IP de Adobe a la lista de permitidos.

## Conexión al destino {#connect}

>[!IMPORTANT]
> 
>Para conectarse al destino, necesita el **[!UICONTROL permiso Administrar destinos]** [control de acceso](/help/access-control/home.md#permissions). Lea la [descripción general del control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios

Para conectarse a este destino, siga los pasos descritos en el [tutorial de configuración de destino](../../ui/connect-destination.md).

Adobe Campaign admite los siguientes tipos de conexión:

* **[!UICONTROL Amazon S3]**
* **[!UICONTROL SFTP con contraseña]**
* **[!UICONTROL SFTP con clave SSH]**
* **[!UICONTROL blob de Azure]**

El método preferido para enviar datos a Adobe Campaign es mediante [!DNL Amazon S3] o [!DNL Azure Blob].

### Parámetros de conexión {#parameters}

Mientras [configura](../../ui/connect-destination.md) este destino, debe proporcionar la siguiente información:

* Para las conexiones de **[!UICONTROL Amazon S3]**, debe proporcionar su [!UICONTROL identificador de clave de acceso] y su [!UICONTROL clave de acceso secreta].
* Para **[!UICONTROL SFTP con conexiones Password]**, debe proporcionar [!UICONTROL dominio], [!UICONTROL puerto], [!UICONTROL nombre de usuario] y [!UICONTROL contraseña].
* Para **[!UICONTROL SFTP con conexiones con clave SSH]**, debe proporcionar [!UICONTROL dominio], [!UICONTROL puerto], [!UICONTROL nombre de usuario] y [!UICONTROL clave SSH].
* Para las conexiones de **[!UICONTROL Azure Blob]**, debe proporcionar una cadena de conexión.
* Opcionalmente, puede adjuntar la clave pública con formato RSA para agregar cifrado con PGP/GPG a los archivos exportados en la sección **[!UICONTROL Key]**. La clave pública debe escribirse como una cadena con codificación [!DNL Base64].
* **[!UICONTROL Nombre]**: elige un nombre relevante para tu destino.
* **[!UICONTROL Descripción]**: escribe una descripción para el destino.
* **[!UICONTROL Nombre del contenedor]**: *Para conexiones S3*. Escriba la ubicación de su espacio de S3 donde [!DNL Experience Platform] depositará los datos de exportación como archivos CSV.
* **[!UICONTROL Ruta de carpeta]**: proporcione la ruta de acceso en su ubicación de almacenamiento donde [!DNL Experience Platform] depositará los datos de exportación como archivos CSV.
* **[!UICONTROL Contenedor]**: *Para conexiones Blob*. El contenedor que contiene el blob en el que se encuentra la ruta de la carpeta.
* **[!UICONTROL Formato de archivo]**: seleccione **CSV** para exportar archivos CSV a su ubicación de almacenamiento.

### Habilitar alertas {#enable-alerts}

Puede activar alertas para recibir notificaciones sobre el estado del flujo de datos a su destino. Seleccione una alerta de la lista a la que suscribirse para recibir notificaciones sobre el estado del flujo de datos. Para obtener más información sobre las alertas, consulte la guía sobre [suscripción a alertas de destinos mediante la interfaz de usuario](../../ui/alerts.md).

Cuando termine de proporcionar detalles para la conexión de destino, seleccione **[!UICONTROL Siguiente]**.

## Activar públicos en este destino {#activate}

>[!IMPORTANT]
> 
>* Para activar los datos, necesita los **[!UICONTROL permisos de control de acceso]**, **[!UICONTROL Activar destinos]**, **[!UICONTROL Ver perfiles]** y **[!UICONTROL Ver segmentos]**&#x200B;[para ](/help/access-control/home.md#permissions). Lea la [descripción general del control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.
>* Para exportar *identidades*, necesita el **[[!UICONTROL permiso de control de acceso]](/help/access-control/home.md#permissions) de&rbrack;** Ver gráfico de identidad&lbrack;. <br> ![Seleccione el área de nombres de identidad resaltada en el flujo de trabajo para activar audiencias en los destinos.](/help/destinations/assets/overview/export-identities-to-destination.png "Seleccione el área de nombres de identidad resaltada en el flujo de trabajo para activar audiencias en los destinos."){width="100" zoomable="yes"}


Consulte [Activar datos de audiencia en destinos de exportación de perfiles por lotes](../../ui/activate-batch-profile-destinations.md) para obtener instrucciones sobre cómo activar audiencias en este destino.

### Atributos de destino {#destination-attributes}

Al activar audiencias en este destino, Adobe recomienda que seleccione un identificador único de su [esquema de unión](../../../profile/home.md#profile-fragments-and-union-schemas). Seleccione el identificador único y cualquier otro campo XDM que desee exportar al destino. Para obtener más información, consulte [prácticas recomendadas al activar audiencias en destinos de marketing por correo electrónico](overview.md#best-practices).

## Datos exportados {#exported-data}

Para [!DNL Adobe Campaign] destinos, [!DNL Experience Platform] crea un archivo de `.csv` en la ubicación de almacenamiento proporcionada. Para obtener más información sobre los archivos, consulte la sección [comprobar la activación de la audiencia](../../ui/activate-batch-profile-destinations.md#verify) en el tutorial de activación de audiencia.

## Configuración de la importación de datos en Adobe Campaign {#import-data-into-campaign}

>[!IMPORTANT]
>
>* Tenga en cuenta los límites de almacenamiento de [!DNL SFTP], el almacenamiento de la base de datos y el perfil activo según el contrato de Adobe Campaign al utilizar esta integración.
>* Debe programar, importar y asignar los segmentos exportados en Adobe Campaign mediante [!DNL Campaign] flujos de trabajo. Consulte [Configuración de una importación recurrente](https://experienceleague.adobe.com/docs/campaign-classic/using/automating-with-workflows/use-cases/data-management/recurring-import-workflow.html) en la documentación de Adobe Campaign Classic y [Acerca de las actividades de administración de datos](https://experienceleague.adobe.com/docs/campaign-standard/using/managing-processes-and-data/data-management-activities/about-data-management-activities.html) en la documentación de Adobe Campaign Standard.
>* El método preferido para enviar datos a Adobe Campaign es mediante [!DNL Amazon S3] o [!DNL Azure Blob].

Después de conectar [!DNL Experience Platform] a su almacenamiento de [!DNL Amazon S3] o [!DNL Azure Blob], debe configurar la importación de datos desde su ubicación de almacenamiento en Adobe Campaign. Para aprender a hacerlo, consulte las siguientes páginas de documentación de Adobe Campaign:
* [Introducción a la importación y exportación de datos](https://experienceleague.adobe.com/docs/campaign-classic/using/getting-started/importing-and-exporting-data/get-started-data-import-export.html?lang=es) y [Carga de datos (archivo)](https://experienceleague.adobe.com/docs/campaign-classic/using/automating-with-workflows/action-activities/data-loading--file-.html) en la documentación de Adobe Campaign Classic.
* [Empiece con la administración de datos y procesos](https://experienceleague.adobe.com/docs/campaign-standard/using/managing-processes-and-data/get-started-workflows.html) y [Cargue el archivo](https://experienceleague.adobe.com/docs/campaign-standard/using/managing-processes-and-data/data-management-activities/load-file.html) en la documentación de Adobe Campaign Standard.
