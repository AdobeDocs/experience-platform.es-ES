---
keywords: correo electrónico;correo electrónico;destinos de correo electrónico;adobe campaign;campaña
title: Conexión Adobe Campaign
description: Adobe Campaign es un conjunto de soluciones que le ayudan a personalizar y entregar campañas en todos sus canales en línea y sin conexión.
exl-id: 0de91738-8f56-41f5-8745-9b14b15db76a
source-git-commit: b1945d42b82b549985d848071762fa6ee2451368
workflow-type: tm+mt
source-wordcount: '764'
ht-degree: 3%

---

# Conexión Adobe Campaign

## Información general {#overview}

Adobe Campaign es un conjunto de soluciones que le ayudan a personalizar y entregar campañas en todos sus canales en línea y sin conexión. Consulte [Introducción a Campaign Classic](https://experienceleague.adobe.com/docs/campaign-classic/using/getting-started/starting-with-adobe-campaign/about-adobe-campaign-classic.html?lang=es) para obtener más información.

Para enviar datos de segmentos a Adobe Campaign, primero debe [conectar el destino](#connect-destination) en Adobe Experience Platform y, a continuación, [configuración de una importación de datos](#import-data-into-campaign) desde su ubicación de almacenamiento a Adobe Campaign.

## Tipo de exportación y frecuencia {#export-type-frequency}

Consulte la tabla siguiente para obtener información sobre el tipo y la frecuencia de exportación de destino.

| Elemento | Tipo | Notas |
---------|----------|---------|
| Tipo de exportación | **[!UICONTROL Basado en perfiles]** | Está exportando todos los miembros de un segmento, junto con los campos de esquema deseados (por ejemplo: dirección de correo electrónico, número de teléfono, apellidos), tal como se elige en la pantalla seleccionar atributos de perfil del [flujo de trabajo de activación de destino](../../ui/activate-batch-profile-destinations.md#select-attributes). |
| Frecuencia de exportación | **[!UICONTROL Lote]** | Los destinos de lote exportan archivos a plataformas descendentes en incrementos de tres, seis, ocho, doce o veinticuatro horas. Más información sobre [destinos basados en archivos por lotes](/help/destinations/destination-types.md#file-based). |

{style=&quot;table-layout:auto&quot;}

## LISTA DE PERMITIDOS de direcciones IP {#allow-list}

Al configurar destinos de marketing por correo electrónico con almacenamiento SFTP, Adobe recomienda que agregue ciertos rangos de IP a la lista de permitidos.

Consulte [LISTA DE PERMITIDOS de direcciones IP para destinos de almacenamiento en la nube](../cloud-storage/ip-address-allow-list.md) si necesita agregar direcciones IP de Adobe a su lista de permitidos.

## Conectarse al destino {#connect}

Para conectarse a este destino, siga los pasos descritos en la sección [tutorial de configuración de destino](../../ui/connect-destination.md).

Adobe Campaign admite los siguientes tipos de conexión:

* **[!UICONTROL Amazon S3]**
* **[!UICONTROL SFTP con contraseña]**
* **[!UICONTROL SFTP con clave SSH]**
* **[!UICONTROL Azure Blob]**

El método preferido para enviar datos a Adobe Campaign es mediante [!DNL Amazon S3] o [!DNL Azure Blob].

### Parámetros de conexión {#parameters}

While [configuración](../../ui/connect-destination.md) Para este destino, debe proporcionar la siguiente información:

* Para **[!UICONTROL Amazon S3]** conexiones, debe proporcionar [!UICONTROL Acceso a ID de clave] y [!UICONTROL Clave de acceso secreto].
* Para **[!UICONTROL SFTP con contraseña]** conexiones, debe proporcionar [!UICONTROL Dominio], [!UICONTROL Puerto], [!UICONTROL Nombre de usuario]y [!UICONTROL Contraseña].
* Para **[!UICONTROL SFTP con clave SSH]** conexiones, debe proporcionar [!UICONTROL Dominio], [!UICONTROL Puerto], [!UICONTROL Nombre de usuario]y [!UICONTROL Clave SSH].
* Para **[!UICONTROL Azure Blob]** conexiones, debe proporcionar una cadena de conexión.
* Opcionalmente, puede adjuntar su clave pública con formato RSA para agregar cifrado con PGP/GPG a los archivos exportados en el **[!UICONTROL Clave]** para obtener más información. La clave pública debe escribirse como un [!DNL Base64] cadena codificada.
* **[!UICONTROL Nombre]**: Elija un nombre relevante para el destino.
* **[!UICONTROL Descripción]**: Escriba una descripción para el destino.
* **[!UICONTROL Nombre del depósito]**: *Para conexiones S3*. Introduzca la ubicación de su compartimento S3 donde [!DNL Platform] depositará los datos de exportación como archivos CSV.
* **[!UICONTROL Ruta de carpeta]**: Proporcione la ruta en su ubicación de almacenamiento donde [!DNL Platform] depositará los datos de exportación como archivos CSV.
* **[!UICONTROL Contenedor]**: *Para conexiones Blob*. El contenedor que alberga el Blob en el que se encuentra la ruta de la carpeta.
* **[!UICONTROL Formato del archivo]**: Select **CSV** para exportar archivos CSV a su ubicación de almacenamiento.

## Activar segmentos en este destino {#activate}

Consulte [Activar datos de audiencia en destinos de exportación de perfiles en lote](../../ui/activate-batch-profile-destinations.md) para obtener instrucciones sobre la activación de segmentos de audiencia en este destino.

### Atributos de destino {#destination-attributes}

Al activar segmentos en este destino, Adobe recomienda que seleccione un identificador único de su [esquema de unión](../../../profile/home.md#profile-fragments-and-union-schemas). Seleccione el identificador único y cualquier otro campo XDM que desee exportar al destino. Para obtener más información, consulte [prácticas recomendadas al activar audiencias en destinos de marketing por correo electrónico](overview.md#best-practices).

## Datos exportados {#exported-data}

Para [!DNL Adobe Campaign] destinos, [!DNL Platform] crea un `.csv` en la ubicación de almacenamiento proporcionada. Para obtener más información sobre los archivos, consulte [verificar activación de segmentos](../../ui/activate-batch-profile-destinations.md#verify) en el tutorial de activación de segmentos.

## Configuración de la importación de datos en Adobe Campaign {#import-data-into-campaign}

>[!IMPORTANT]
>
>* Tenga en cuenta que [!DNL SFTP] límites de almacenamiento de información, límites de almacenamiento de la base de datos y límites de perfil activos según su contrato de Adobe Campaign mientras realiza esta integración.
>* Debe programar, importar y asignar los segmentos exportados en Adobe Campaign mediante [!DNL Campaign] flujos de trabajo. Consulte [Configuración de una importación recurrente](https://experienceleague.adobe.com/docs/campaign-classic/using/automating-with-workflows/use-cases/data-management/recurring-import-workflow.html) en la documentación de Adobe Campaign Classic y [Acerca de las actividades de gestión de datos](https://experienceleague.adobe.com/docs/campaign-standard/using/managing-processes-and-data/data-management-activities/about-data-management-activities.html) en la documentación de Adobe Campaign Standard.
>* El método preferido para enviar datos a Adobe Campaign es mediante [!DNL Amazon S3] o [!DNL Azure Blob].


Después de conectar [!DNL Platform] a su [!DNL Amazon S3] o [!DNL Azure Blob] , debe configurar la importación de datos desde la ubicación de almacenamiento en Adobe Campaign. Para obtener información sobre cómo hacerlo, consulte las siguientes páginas de documentación de Adobe Campaign:
* [Introducción a la importación y exportación de datos](https://experienceleague.adobe.com/docs/campaign-classic/using/getting-started/importing-and-exporting-data/get-started-data-import-export.html?lang=es) y [Carga de datos (archivos)](https://experienceleague.adobe.com/docs/campaign-classic/using/automating-with-workflows/action-activities/data-loading--file-.html) en la documentación de Adobe Campaign Classic.
* [Introducción a la administración de datos y procesos](https://experienceleague.adobe.com/docs/campaign-standard/using/managing-processes-and-data/get-started-workflows.html) y [Cargar archivo](https://experienceleague.adobe.com/docs/campaign-standard/using/managing-processes-and-data/data-management-activities/load-file.html) en la documentación de Adobe Campaign Standard.
