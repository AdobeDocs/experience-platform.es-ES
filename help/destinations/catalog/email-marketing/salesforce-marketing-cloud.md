---
keywords: correo electrónico;correo electrónico;correo electrónico;destinos de correo electrónico;salesforce;destino de salesforce
title: Conexión de Marketing Cloud de Salesforce
description: El Marketing Cloud de Salesforce es un grupo de marketing digital anteriormente conocido como ExactTarget que le permite crear y personalizar recorridos para que los visitantes y clientes personalicen su experiencia.
exl-id: e85049a7-eaed-4f8a-b670-9999d56928f8
source-git-commit: 72225ac673ed921b5857a14070660134949e7e3e
workflow-type: tm+mt
source-wordcount: '783'
ht-degree: 2%

---

# [!DNL (Files) Salesforce Marketing Cloud] conexión

## Información general {#overview}

[[!DNL Salesforce Marketing Cloud]](https://www.salesforce.com/products/marketing-cloud/email-marketing/) es un grupo de marketing digital anteriormente conocido como ExactTarget que le permite crear y personalizar recorridos para que los visitantes y clientes personalicen su experiencia.

Para enviar datos de audiencia a [!DNL Salesforce Marketing Cloud], primero debe [conectar el destino](#connect-destination) en Platform y luego [configuración de una importación de datos](#import-data-into-salesforce) desde su ubicación de almacenamiento a [!DNL Salesforce Marketing Cloud].

## Audiencias compatibles {#supported-audiences}

Esta sección describe qué tipo de audiencias puede exportar a este destino.

| Origen de audiencia | Admitido | Descripción |
---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Audiencias generadas mediante el Experience Platform [Servicio de segmentación](../../../segmentation/home.md). |
| Cargas personalizadas | ✓ | Audiencias [importado](../../../segmentation/ui/overview.md#import-audience) en el Experience Platform desde archivos CSV. |

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
>Para conectarse al destino, necesita el **[!UICONTROL Administrar destinos]** [permiso de control de acceso](/help/access-control/home.md#permissions). Lea el [información general de control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Para conectarse a este destino, siga los pasos descritos en la sección [tutorial de configuración de destino](../../ui/connect-destination.md).

Este destino admite los siguientes tipos de conexión:

* **[!UICONTROL SFTP con contraseña]**
* **[!UICONTROL SFTP con clave SSH]**

### Parámetros de conexión {#parameters}

While [configuración](../../ui/connect-destination.md) Para este destino, debe proporcionar la siguiente información:

* Para **[!UICONTROL SFTP con contraseña]** conexiones, debe proporcionar:
   * **[!UICONTROL Dominio]**: la dirección IP o el nombre de dominio de la cuenta SFTP;
   * **[!UICONTROL Puerto]**: el puerto utilizado por la ubicación de almacenamiento SFTP;
   * **[!UICONTROL Nombre de usuario]**: el nombre de usuario para iniciar sesión en la ubicación de almacenamiento SFTP;
   * **[!UICONTROL Contraseña]**: contraseña para iniciar sesión en la ubicación de almacenamiento SFTP.
* Para **[!UICONTROL SFTP con clave SSH]** conexiones, debe proporcionar:
   * **[!UICONTROL Dominio]**: la dirección IP o el nombre de dominio de la cuenta SFTP;
   * **[!UICONTROL Puerto]**: el puerto utilizado por la ubicación de almacenamiento SFTP;
   * **[!UICONTROL Nombre de usuario]**: el nombre de usuario para iniciar sesión en la ubicación de almacenamiento SFTP;
   * **[!UICONTROL Clave SSH]**: clave SSH privada que se utiliza para iniciar sesión en la ubicación de almacenamiento SFTP. La clave privada debe tener el formato de cadena codificada Base64 y no debe estar protegida por contraseña.

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

## Activar audiencias en este destino {#activate}

>[!IMPORTANT]
> 
>Para activar los datos, necesita el **[!UICONTROL Administrar destinos]**, **[!UICONTROL Activar destinos]**, **[!UICONTROL Ver perfiles]**, y **[!UICONTROL Ver segmentos]** [permisos de control de acceso](/help/access-control/home.md#permissions). Lea el [información general de control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Consulte [Activar datos de audiencia en destinos de exportación de perfiles por lotes](../../ui/activate-batch-profile-destinations.md) para obtener instrucciones sobre cómo activar audiencias en este destino.

### Atributos de destino {#destination-attributes}

Al activar audiencias en este destino, Adobe recomienda seleccionar un identificador único de su [esquema de unión](../../../profile/home.md#profile-fragments-and-union-schemas). Seleccione el identificador único y cualquier otro campo XDM que desee exportar al destino. Para obtener más información, consulte [prácticas recomendadas al activar audiencias en destinos de marketing por correo electrónico](overview.md#best-practices).

## Datos exportados {#exported-data}

Para [!DNL Salesforce Marketing Cloud] destinos, Platform crea un `.csv` en la ubicación de almacenamiento proporcionada. Para obtener más información sobre los archivos, consulte [verificar activación de audiencia](../../ui/activate-batch-profile-destinations.md#verify) en el tutorial de activación de audiencia.

## Configuración de la importación de datos en [!DNL Salesforce Marketing Cloud] {#import-data-into-salesforce}

Después de conectar [!DNL Platform] a su [!DNL SFTP] almacenamiento, debe configurar la importación de datos desde su ubicación de almacenamiento en [!DNL Salesforce Marketing Cloud]. Para obtener información sobre cómo hacerlo, consulte [Importación de suscriptores al Marketing Cloud desde un archivo](https://help.salesforce.com/articleView?id=mc_es_import_subscribers_from_file.htm&amp;type=5) en el [!DNL Salesforce Help Center].
