---
keywords: correo electrónico;correo electrónico;correo electrónico;destinos de correo electrónico;adobe campaign;campaign
title: Conexión de Adobe Campaign
description: Adobe Campaign es un conjunto de soluciones que le ayudan a personalizar y entregar campañas en todos sus canales en línea y sin conexión.
exl-id: 0de91738-8f56-41f5-8745-9b14b15db76a
source-git-commit: 16365865e349f8805b8346ec98cdab89cd027363
workflow-type: tm+mt
source-wordcount: '941'
ht-degree: 2%

---

# Conexión de Adobe Campaign

## Información general {#overview}

Adobe Campaign es un conjunto de soluciones que le ayudan a personalizar y entregar campañas en todos sus canales en línea y sin conexión. Consulte [Introducción a Campaign Classic](https://experienceleague.adobe.com/docs/campaign-classic/using/getting-started/starting-with-adobe-campaign/about-adobe-campaign-classic.html?lang=es) para obtener más información.

Para enviar datos de audiencia a Adobe Campaign, primero debe [conectar el destino](#connect-destination) en Adobe Experience Platform y, a continuación [configuración de una importación de datos](#import-data-into-campaign) desde su ubicación de almacenamiento a Adobe Campaign.

## Audiencias compatibles {#supported-audiences}

Esta sección describe todas las audiencias que puede exportar a este destino.

Este destino admite la activación de todas las audiencias generadas a través del Experience Platform [Servicio de segmentación](../../../segmentation/home.md).

*Adicionalmente* Sin embargo, este destino también admite la activación de las audiencias que se describen en la tabla siguiente.

| Tipo de audiencia | Descripción |
---------|----------|
| Cargas personalizadas | Audiencias [importado](../../../segmentation/ui/overview.md#import-audience) en el Experience Platform desde archivos CSV. |

{style="table-layout:auto"}

## Tipo y frecuencia de exportación {#export-type-frequency}

Consulte la tabla siguiente para obtener información sobre el tipo y la frecuencia de exportación de destino.

| Elemento | Tipo | Notas |
---------|----------|---------|
| Tipo de exportación | **[!UICONTROL Basado en perfiles]** | Va a exportar todos los miembros de un segmento, junto con los campos de esquema deseados (por ejemplo: dirección de correo electrónico, número de teléfono, apellidos), tal como se elige en la pantalla seleccionar atributos de perfil del [flujo de trabajo de activación de destino](../../ui/activate-batch-profile-destinations.md#select-attributes). |
| Frecuencia de exportación | **[!UICONTROL Lote]** | Los destinos por lotes exportan archivos a plataformas descendentes en incrementos de tres, seis, ocho, doce o veinticuatro horas. Más información sobre [destinos basados en archivos por lotes](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## LISTA DE PERMITIDOS de direcciones IP {#allow-list}

Al configurar destinos de marketing por correo electrónico con almacenamiento SFTP, el Adobe recomienda añadir determinados rangos de IP a la lista de permitidos.

Consulte [LISTA DE PERMITIDOS de direcciones IP para destinos SFTP](../cloud-storage/ip-address-allow-list.md) si necesita agregar direcciones IP de Adobe a la lista de permitidos.

## Conectar con el destino {#connect}

>[!IMPORTANT]
> 
>Para conectarse al destino, necesita el **[!UICONTROL Administrar destinos]** [permiso de control de acceso](/help/access-control/home.md#permissions). Lea el [información general de control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios

Para conectarse a este destino, siga los pasos descritos en la sección [tutorial de configuración de destino](../../ui/connect-destination.md).

Adobe Campaign admite los siguientes tipos de conexión:

* **[!UICONTROL Amazon S3]**
* **[!UICONTROL SFTP con contraseña]**
* **[!UICONTROL SFTP con clave SSH]**
* **[!UICONTROL Azure Blob]**

El método preferido para enviar datos a Adobe Campaign es mediante [!DNL Amazon S3] o [!DNL Azure Blob].

### Parámetros de conexión {#parameters}

While [configuración](../../ui/connect-destination.md) Para este destino, debe proporcionar la siguiente información:

* Para **[!UICONTROL Amazon S3]** conexiones, debe proporcionar su [!UICONTROL Identificador de clave de acceso] y [!UICONTROL Clave de acceso secreta].
* Para **[!UICONTROL SFTP con contraseña]** conexiones, debe proporcionar [!UICONTROL Dominio], [!UICONTROL Puerto], [!UICONTROL Nombre de usuario], y [!UICONTROL Contraseña].
* Para **[!UICONTROL SFTP con clave SSH]** conexiones, debe proporcionar [!UICONTROL Dominio], [!UICONTROL Puerto], [!UICONTROL Nombre de usuario], y [!UICONTROL Clave SSH].
* Para **[!UICONTROL Azure Blob]** conexiones, debe proporcionar una cadena de conexión.
* De forma opcional, puede adjuntar la clave pública con formato RSA para agregar cifrado con PGP/GPG a los archivos exportados en **[!UICONTROL Clave]** sección. La clave pública debe escribirse como [!DNL Base64] cadena codificada.
* **[!UICONTROL Nombre]**: Elija un nombre relevante para el destino.
* **[!UICONTROL Descripción]**: introduzca una descripción para el destino.
* **[!UICONTROL Nombre del cubo]**: *Para conexiones S3*. Introduzca la ubicación del compartimento de S3 donde [!DNL Platform] depositará sus datos de exportación como archivos CSV.
* **[!UICONTROL Ruta de carpeta]**: proporcione la ruta en su ubicación de almacenamiento donde [!DNL Platform] depositará sus datos de exportación como archivos CSV.
* **[!UICONTROL Contenedor]**: *Para conexiones de blob*. El contenedor que contiene el blob en el que se encuentra la ruta de la carpeta.
* **[!UICONTROL Formato de archivo]**: Seleccionar **CSV** para exportar archivos CSV a su ubicación de almacenamiento.

### Habilitar alertas {#enable-alerts}

Puede activar alertas para recibir notificaciones sobre el estado del flujo de datos a su destino. Seleccione una alerta de la lista a la que suscribirse para recibir notificaciones sobre el estado del flujo de datos. Para obtener más información sobre las alertas, consulte la guía de [suscripción a alertas de destinos mediante la IU](../../ui/alerts.md).

Cuando haya terminado de proporcionar detalles para la conexión de destino, seleccione **[!UICONTROL Siguiente]**.

## Activar audiencias en este destino {#activate}

>[!IMPORTANT]
> 
>Para activar los datos, necesita el **[!UICONTROL Administrar destinos]**, **[!UICONTROL Activar destinos]**, **[!UICONTROL Ver perfiles]**, y **[!UICONTROL Ver segmentos]** [permisos de control de acceso](/help/access-control/home.md#permissions). Lea el [información general de control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.


Consulte [Activar datos de audiencia en destinos de exportación de perfiles por lotes](../../ui/activate-batch-profile-destinations.md) para obtener instrucciones sobre cómo activar audiencias en este destino.

### Atributos de destino {#destination-attributes}

Al activar audiencias en este destino, Adobe recomienda seleccionar un identificador único de su [esquema de unión](../../../profile/home.md#profile-fragments-and-union-schemas). Seleccione el identificador único y cualquier otro campo XDM que desee exportar al destino. Para obtener más información, consulte [prácticas recomendadas al activar audiencias en destinos de marketing por correo electrónico](overview.md#best-practices).

## Datos exportados {#exported-data}

Para [!DNL Adobe Campaign] destinos, [!DNL Platform] crea un `.csv` en la ubicación de almacenamiento proporcionada. Para obtener más información sobre los archivos, consulte [verificar activación de audiencia](../../ui/activate-batch-profile-destinations.md#verify) en el tutorial de activación de audiencia.

## Configuración de la importación de datos en Adobe Campaign {#import-data-into-campaign}

>[!IMPORTANT]
>
>* Tenga en cuenta lo siguiente [!DNL SFTP] límites de almacenamiento, límites de almacenamiento de la base de datos y límites de perfil activo según el contrato de Adobe Campaign al realizar esta integración.
>* Debe programar, importar y asignar los segmentos exportados en Adobe Campaign mediante [!DNL Campaign] flujos de trabajo. Consulte [Configuración de una importación recurrente](https://experienceleague.adobe.com/docs/campaign-classic/using/automating-with-workflows/use-cases/data-management/recurring-import-workflow.html) Adobe Campaign Classic en la documentación y [Acerca de las actividades de gestión de datos](https://experienceleague.adobe.com/docs/campaign-standard/using/managing-processes-and-data/data-management-activities/about-data-management-activities.html) en la documentación de Adobe Campaign Standard.
>* El método preferido para enviar datos a Adobe Campaign es mediante [!DNL Amazon S3] o [!DNL Azure Blob].

Después de conectar [!DNL Platform] a su [!DNL Amazon S3] o [!DNL Azure Blob] almacenamiento, debe configurar la importación de datos desde su ubicación de almacenamiento en Adobe Campaign. Para aprender a hacerlo, consulte las siguientes páginas de documentación de Adobe Campaign:
* [Introducción a la importación y exportación de datos](https://experienceleague.adobe.com/docs/campaign-classic/using/getting-started/importing-and-exporting-data/get-started-data-import-export.html?lang=es) y [Carga de datos (archivo)](https://experienceleague.adobe.com/docs/campaign-classic/using/automating-with-workflows/action-activities/data-loading--file-.html) en la documentación de Adobe Campaign Classic.
* [Introducción a la administración de datos y procesos](https://experienceleague.adobe.com/docs/campaign-standard/using/managing-processes-and-data/get-started-workflows.html) y [Cargar archivo](https://experienceleague.adobe.com/docs/campaign-standard/using/managing-processes-and-data/data-management-activities/load-file.html) en la documentación de Adobe Campaign Standard.
