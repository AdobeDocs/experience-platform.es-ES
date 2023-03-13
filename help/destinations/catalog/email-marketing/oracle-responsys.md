---
keywords: correo electrónico;Correo electrónico;correo electrónico;destinos de correo electrónico;oracle responsys destination
title: Conexión de oracle de Responsys
description: Responsys es una herramienta de marketing por correo electrónico empresarial para campañas de marketing entre canales que ofrece Oracle para personalizar las interacciones entre correo electrónico, móvil, pantalla y redes sociales.
exl-id: 70f2f601-afee-4315-bf7a-ed2c92397ebe
source-git-commit: dd18350387aa6bdeb61612f0ccf9d8d2223a8a5d
workflow-type: tm+mt
source-wordcount: '643'
ht-degree: 1%

---

# [!DNL Oracle Responsys] conexión

## Información general {#overview}

[Responsys](https://www.oracle.com/cx/marketing/campaign-management/) es una herramienta de marketing por correo electrónico empresarial para campañas de marketing entre canales que ofrece [!DNL Oracle] para personalizar las interacciones en correos electrónicos, móviles, pantallas y medios sociales.

Para enviar datos de segmentos a [!DNL Oracle Responsys], primero debe [conectar con el destino](#connect-destination) en Adobe Experience Platform y, a continuación [configuración de una importación de datos](#import-data-into-responsys) desde su ubicación de almacenamiento a [!DNL Oracle Responsys].

## Tipo y frecuencia de exportación {#export-type-frequency}

Consulte la tabla siguiente para obtener información sobre el tipo y la frecuencia de exportación de destino.

| Elemento | Tipo | Notas |
---------|----------|---------|
| Tipo de exportación | **[!UICONTROL Basado en perfiles]** | Va a exportar todos los miembros de un segmento, junto con los campos de esquema deseados (por ejemplo: dirección de correo electrónico, número de teléfono, apellidos), tal como se elige en la pantalla seleccionar atributos de perfil del [flujo de trabajo de activación de destino](../../ui/activate-batch-profile-destinations.md#select-attributes). |
| Frecuencia de exportación | **[!UICONTROL Lote]** | Los destinos por lotes exportan archivos a plataformas descendentes en incrementos de tres, seis, ocho, doce o veinticuatro horas. Más información sobre [destinos basados en archivos por lotes](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## LISTA DE PERMITIDOS de direcciones IP {#allow-list}

Al configurar destinos de marketing por correo electrónico con almacenamiento SFTP, el Adobe recomienda añadir determinados rangos de IP a la lista de permitidos.

Consulte [LISTA DE PERMITIDOS de direcciones IP para destinos de almacenamiento en la nube](../cloud-storage/ip-address-allow-list.md) si necesita agregar direcciones IP de Adobe a la lista de permitidos.

## Conectar con el destino {#connect}

>[!IMPORTANT]
> 
>Para conectarse al destino, necesita el **[!UICONTROL Administrar destinos]** [permiso de control de acceso](/help/access-control/home.md#permissions). Lea el [información general de control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

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
* De forma opcional, puede adjuntar la clave pública con formato RSA para agregar cifrado con PGP/GPG a los archivos exportados en **[!UICONTROL Clave]** sección. La clave pública debe escribirse como [!DNL Base64] cadena codificada.
* **[!UICONTROL Nombre]**: Elija un nombre relevante para el destino.
* **[!UICONTROL Descripción]**: introduzca una descripción para el destino.
* **[!UICONTROL Ruta de carpeta]**: Proporcione la ruta en la ubicación de almacenamiento en la que Platform depositará los datos de exportación como archivos CSV.
* **[!UICONTROL Formato de archivo]**: Seleccionar **CSV** para exportar archivos CSV a su ubicación de almacenamiento.

<!--

Commenting out Amazon S3 bucket part for now until support is clarified

- **[!UICONTROL Bucket name]**: Your Amazon S3 bucket, where Platform will deposit the data export. Your input must be between 3 and 63 characters long. Must begin and end with a letter or number. Must contain only lowercase letters, numbers, or hyphens ( - ). Must not be formatted as an IP address (for example, 192.100.1.1).

-->

### Habilitar alertas {#enable-alerts}

Puede activar alertas para recibir notificaciones sobre el estado del flujo de datos a su destino. Seleccione una alerta de la lista a la que suscribirse para recibir notificaciones sobre el estado del flujo de datos. Para obtener más información sobre las alertas, consulte la guía de [suscripción a alertas de destinos mediante la IU](../../ui/alerts.md).

Cuando haya terminado de proporcionar detalles para la conexión de destino, seleccione **[!UICONTROL Siguiente]**.

## Activar segmentos en este destino {#activate}

>[!IMPORTANT]
> 
>Para activar los datos, necesita el **[!UICONTROL Administrar destinos]**, **[!UICONTROL Activar destinos]**, **[!UICONTROL Ver perfiles]**, y **[!UICONTROL Ver segmentos]** [permisos de control de acceso](/help/access-control/home.md#permissions). Lea el [información general de control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Consulte [Activar datos de audiencia en destinos de exportación de perfiles por lotes](../../ui/activate-batch-profile-destinations.md) para obtener instrucciones sobre cómo activar segmentos de audiencia en este destino.

### Atributos de destino {#destination-attributes}

Al activar segmentos en este destino, Adobe recomienda seleccionar un identificador único de su [esquema de unión](../../../profile/home.md#profile-fragments-and-union-schemas). Seleccione el identificador único y cualquier otro campo XDM que desee exportar al destino. Para obtener más información, consulte [prácticas recomendadas al activar audiencias en destinos de marketing por correo electrónico](overview.md#best-practices).

## Datos exportados {#exported-data}

Para [!DNL Oracle Responsys] destinos, Platform crea un `.csv` en la ubicación de almacenamiento proporcionada. Para obtener más información sobre los archivos, consulte [verificar activación de segmentos](../../ui/activate-batch-profile-destinations.md#verify) en el tutorial de activación de segmentos.

## Configuración de la importación de datos en [!DNL Oracle Responsys] {#import-data-into-responsys}

Después de conectar [!DNL Platform] a su [!DNL SFTP] almacenamiento, debe configurar la importación de datos desde su ubicación de almacenamiento en [!DNL Oracle Responsys]. Para obtener información sobre cómo hacerlo, consulte [Importación de contactos o cuentas](https://docs.oracle.com/cloud/latest/marketingcs_gs/OMCEA/Connect_WizardUpload.htm) en el [!DNL Oracle Responsys Help Center].
