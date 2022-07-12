---
keywords: correo electrónico;correo electrónico;destinos de correo electrónico;eloqua de oracle;oracle
title: Conexión oracle Eloqua
description: Oracle Eloqua es una plataforma de software como servicio (SaaS) para la automatización de marketing que ofrece Oracle y que tiene como objetivo ayudar a los especialistas en marketing B2B y a las organizaciones a administrar las campañas de marketing y la generación de posibles clientes de ventas.
exl-id: 6eaa79ff-8874-423b-bdff-aa04f6101a53
source-git-commit: dd18350387aa6bdeb61612f0ccf9d8d2223a8a5d
workflow-type: tm+mt
source-wordcount: '662'
ht-degree: 1%

---

# [!DNL Oracle Eloqua] connection

[[!DNL Oracle Eloqua]](https://www.oracle.com/cx/marketing/automation/) es una plataforma de software como servicio (SaaS) para la automatización de marketing ofrecida por [!DNL Oracle] que tiene como objetivo ayudar a los especialistas en marketing B2B y a las organizaciones a administrar las campañas de marketing y la generación de posibles clientes de ventas.

Para enviar datos de segmentos a [!DNL Oracle Eloqua], primero debe [conectar el destino](#connect-destination) en Adobe Experience Platform y, a continuación, [configuración de una importación de datos](#import-data-into-eloqua) desde su ubicación de almacenamiento a [!DNL Oracle Eloqua].

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

>[!IMPORTANT]
> 
>Para conectarse al destino, necesita la variable **[!UICONTROL Administrar destinos]** [permiso de control de acceso](/help/access-control/home.md#permissions). Lea el [información general sobre el control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios

Para conectarse a este destino, siga los pasos descritos en la sección [tutorial de configuración de destino](../../ui/connect-destination.md).

Este destino admite los siguientes tipos de conexión:

* **[!UICONTROL SFTP con contraseña]**
* **[!UICONTROL SFTP con clave SSH]**

### Parámetros de conexión {#parameters}

While [configuración](../../ui/connect-destination.md) Para este destino, debe proporcionar la siguiente información:

* Para **[!UICONTROL SFTP con contraseña]** conexiones, debe proporcionar:
   * [!UICONTROL Dominio]
   * [!UICONTROL Puerto ]
   * [!UICONTROL Nombre de usuario]
   * [!UICONTROL Contraseña]
* Para **[!UICONTROL SFTP con clave SSH]** conexiones, debe proporcionar:
   * [!UICONTROL Dominio]
   * [!UICONTROL Puerto ]
   * [!UICONTROL Nombre de usuario]
   * [!UICONTROL Clave SSH]

* Opcionalmente, puede adjuntar su clave pública con formato RSA para agregar cifrado con PGP/GPG a los archivos exportados en el **[!UICONTROL Clave]** para obtener más información. La clave pública debe escribirse como un [!DNL Base64] cadena codificada.
* **[!UICONTROL Nombre]**: Elija un nombre relevante para el destino.
* **[!UICONTROL Descripción]**: Escriba una descripción para el destino.
* **[!UICONTROL Ruta de carpeta]**: Proporcione la ruta en su ubicación de almacenamiento donde Platform depositará los datos de exportación como archivos CSV.
* **[!UICONTROL Formato del archivo]**: Select **CSV** para exportar archivos CSV a su ubicación de almacenamiento.

<!--

Commenting out Amazon S3 bucket part for now until support is clarified

- **[!UICONTROL Bucket name]**: Your Amazon S3 bucket, where Platform will deposit the data export. Your input must be between 3 and 63 characters long. Must begin and end with a letter or number. Must contain only lowercase letters, numbers, or hyphens ( - ). Must not be formatted as an IP address (for example, 192.100.1.1).

-->

### Habilitar alertas {#enable-alerts}

Puede activar las alertas para recibir notificaciones sobre el estado del flujo de datos a su destino. Seleccione una alerta de la lista para suscribirse y recibir notificaciones sobre el estado de su flujo de datos. Para obtener más información sobre las alertas, consulte la guía de [suscripción a alertas de destinos mediante la interfaz de usuario](../../ui/alerts.md).

Cuando haya terminado de proporcionar detalles para la conexión de destino, seleccione **[!UICONTROL Siguiente]**.

## Activar segmentos en este destino {#activate}

>[!IMPORTANT]
> 
>Para activar los datos, necesita la variable **[!UICONTROL Administrar destinos]**, **[!UICONTROL Activar destinos]**, **[!UICONTROL Ver perfiles]** y **[!UICONTROL Ver segmentos]** [permisos de control de acceso](/help/access-control/home.md#permissions). Lea el [información general sobre el control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Consulte [Activar datos de audiencia en destinos de exportación de perfiles en lote](../../ui/activate-batch-profile-destinations.md) para obtener instrucciones sobre la activación de segmentos de audiencia en este destino.

### Atributos de destino {#destination-attributes}

Al activar segmentos en este destino, Adobe recomienda que seleccione un identificador único de su [esquema de unión](../../../profile/home.md#profile-fragments-and-union-schemas). Seleccione el identificador único y cualquier otro campo XDM que desee exportar al destino. Para obtener más información, consulte [prácticas recomendadas al activar audiencias en destinos de marketing por correo electrónico](overview.md#best-practices).

## Datos exportados {#exported-data}

Para [!DNL Oracle Eloqua] destinos, Platform crea un `.csv` en la ubicación de almacenamiento proporcionada. Para obtener más información sobre los archivos, consulte [verificar activación de segmentos](../../ui/activate-batch-profile-destinations.md#verify) en el tutorial de activación de segmentos.

## Configurar la importación de datos en [!DNL Oracle Eloqua] {#import-data-into-eloqua}

Después de conectar [!DNL Platform] a su [!DNL SFTP] , debe configurar la importación de datos desde la ubicación de almacenamiento en [!DNL Oracle Eloqua]. Para obtener información sobre cómo hacerlo, consulte [Importación de contactos o cuentas](https://docs.oracle.com/cloud/latest/marketingcs_gs/OMCAA/Help/DataImportExport/Tasks/ImportingContactsOrAccounts.htm) en el [!DNL Oracle Eloqua Help Center].
