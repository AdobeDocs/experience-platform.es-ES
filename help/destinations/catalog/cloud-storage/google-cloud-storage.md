---
title: Conexión de Google Cloud Storage
description: Obtenga información sobre cómo conectarse a Google Cloud Storage y activar audiencias o exportar conjuntos de datos.
last-substantial-update: 2023-07-26T00:00:00Z
exl-id: ab274270-ae8c-4264-ba64-700b118e6435
source-git-commit: 16365865e349f8805b8346ec98cdab89cd027363
workflow-type: tm+mt
source-wordcount: '1031'
ht-degree: 0%

---

# [!DNL Google Cloud Storage] conexión

## Información general {#overview}

Cree una conexión saliente activa a [!DNL Google Cloud Storage] para exportar periódicamente archivos de datos de Adobe Experience Platform a sus propios contenedores.

## Conéctese a su [!DNL Google Cloud Storage] mediante API o IU {#connect-api-or-ui}

* Para conectarse a su [!DNL Google Cloud Storage] Ubicación de almacenamiento mediante la interfaz de usuario de Platform, lea las secciones [Conectar con el destino](#connect) y [Activar audiencias en este destino](#activate) más abajo.
* Para conectarse a su [!DNL Google Cloud Storage] ubicación de almacenamiento mediante programación, lea el [Activación de audiencias en destinos basados en archivos mediante el tutorial de la API de Flow Service](../../api/activate-segments-file-based-destinations.md).

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
| Tipo de exportación | **[!UICONTROL Basado en perfiles]** | Está exportando todos los miembros de un segmento, junto con los campos de esquema aplicables, tal como se elige en la pantalla Seleccionar atributos de perfil del [flujo de trabajo de activación de destino](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes). |
| Frecuencia de exportación | **[!UICONTROL Lote]** | Los destinos por lotes exportan archivos a plataformas descendentes en incrementos de tres, seis, ocho, doce o veinticuatro horas. Más información sobre [destinos basados en archivos por lotes](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## Configuración previa necesaria para conectar su [!DNL Google Cloud Storage] account {#prerequisites}

Para conectar Platform a [!DNL Google Cloud Storage], primero debe habilitar la interoperabilidad para su [!DNL Google Cloud Storage] cuenta. Para acceder a la configuración de interoperabilidad, abra [!DNL Google Cloud Platform] y seleccione **[!UICONTROL Configuración]** desde el **[!UICONTROL Almacenamiento en la nube]** en el panel de navegación.

![Panel de Google Cloud Platform con Almacenamiento en la nube y Configuración resaltados.](../../../sources/images/tutorials/create/google-cloud-storage/nav.png)

El **[!UICONTROL Configuración]** página. A partir de aquí, puede ver información sobre su [!DNL Google] ID de proyecto y detalles sobre su [!DNL Google Cloud Storage] cuenta. Para acceder a la configuración de interoperabilidad, seleccione **[!UICONTROL Interoperación]** desde el encabezado superior.

![La pestaña Interoperabilidad resaltada en el panel de Google Cloud Platform.](../../../sources/images/tutorials/create/google-cloud-storage/project-access.png)

El **[!UICONTROL Interoperación]** contiene información sobre la autenticación, las claves de acceso y el proyecto predeterminado asociado a su cuenta de servicio. Para generar un nuevo ID de clave de acceso y una clave de acceso secreta para su cuenta de servicio, seleccione **[!UICONTROL Creación de una clave para una cuenta de servicio]**.

![La opción Crear una clave para un control de cuenta de servicio resaltada en el panel de Google Cloud Platform.](../../../sources/images/tutorials/create/google-cloud-storage/interoperability.png)

Puede utilizar el ID de clave de acceso y la clave de acceso secreta generados recientemente para conectar su [!DNL Google Cloud Storage] a Platform.

## Conectar con el destino {#connect}

>[!IMPORTANT]
> 
>Para conectarse al destino, necesita el **[!UICONTROL Administrar destinos]** [permiso de control de acceso](/help/access-control/home.md#permissions). Lea el [información general de control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Para conectarse a este destino, siga los pasos descritos en la sección [tutorial de configuración de destino](/help/destinations/ui/connect-destination.md). En el flujo de trabajo de configuración de destino, rellene los campos enumerados en las dos secciones siguientes.

### Autenticar en el destino {#authenticate}

Para autenticarse en el destino, rellene los campos obligatorios y seleccione **[!UICONTROL Conectar con destino]**.

* **[!UICONTROL ID de clave de acceso]**: una cadena alfanumérica de 61 caracteres que se utiliza para autenticar su [!DNL Google Cloud Storage] a Platform. Para obtener información sobre cómo obtener este valor, lea la [requisitos previos](#prerequisites) sección anterior.
* **[!UICONTROL Clave de acceso secreta]**: una cadena de 40 caracteres codificada en Base64 que se utiliza para autenticar su [!DNL Google Cloud Storage] a Platform. Para obtener información sobre cómo obtener este valor, lea la [requisitos previos](#prerequisites) sección anterior.
* **[!UICONTROL Clave de cifrado]**: Opcionalmente, puede adjuntar la clave pública con formato RSA para agregar cifrado a los archivos exportados. Vea un ejemplo de una clave de cifrado con formato correcto en la siguiente imagen.

  ![Imagen que muestra un ejemplo de una clave PGP con formato correcto en la IU de](../../assets/catalog/cloud-storage/sftp/pgp-key.png)

Para obtener más información sobre estos valores, lea la [Claves HMAC de Google Cloud Storage](https://cloud.google.com/storage/docs/authentication/hmackeys#overview) guía. Para obtener información sobre cómo generar su propio ID de clave de acceso y clave de acceso secreta, consulte la [[!DNL Google Cloud Storage] descripción general de origen](/help/sources/connectors/cloud-storage/google-cloud-storage.md).

### Rellenar detalles de destino {#destination-details}

Para configurar los detalles del destino, rellene los campos obligatorios y opcionales a continuación. Un asterisco junto a un campo en la interfaz de usuario indica que el campo es obligatorio.

* **[!UICONTROL Nombre]**: complete el nombre preferido para este destino.
* **[!UICONTROL Descripción]**: Opcional. Por ejemplo, puede mencionar para qué campaña está usando este destino.
* **[!UICONTROL Nombre del cubo]**: introduzca el nombre del [!DNL Google Cloud Storage] contenedor que utilizará este destino.
* **[!UICONTROL Ruta de carpeta]**: introduzca la ruta a la carpeta de destino que alojará los archivos exportados.
* **[!UICONTROL Tipo de archivo]**: seleccione el Experience Platform de formato que debe utilizar para los archivos exportados. Al seleccionar la variable [!UICONTROL CSV] , también puede hacer lo siguiente [configurar las opciones de formato de archivo](../../ui/batch-destinations-file-formatting-options.md).
* **[!UICONTROL Formato de compresión]**: seleccione el tipo de compresión que el Experience Platform debe utilizar para los archivos exportados.
* **[!UICONTROL Incluir archivo de manifiesto]**: active esta opción si desea que las exportaciones incluyan un archivo JSON de manifiesto que contenga información sobre la ubicación de exportación, el tamaño de exportación, etc.

### Habilitar alertas {#enable-alerts}

Puede activar alertas para recibir notificaciones sobre el estado del flujo de datos a su destino. Seleccione una alerta de la lista a la que suscribirse para recibir notificaciones sobre el estado del flujo de datos. Para obtener más información sobre las alertas, consulte la guía de [suscripción a alertas de destinos mediante la IU](../../ui/alerts.md).

Cuando haya terminado de proporcionar detalles para la conexión de destino, seleccione **[!UICONTROL Siguiente]**.

## Activar audiencias en este destino {#activate}

>[!IMPORTANT]
> 
>Para activar los datos, necesita el **[!UICONTROL Administrar destinos]**, **[!UICONTROL Activar destinos]**, **[!UICONTROL Ver perfiles]**, y **[!UICONTROL Ver segmentos]** [permisos de control de acceso](/help/access-control/home.md#permissions). Lea el [información general de control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Consulte [Activar datos de audiencia en destinos de exportación de perfiles por lotes](../../ui/activate-batch-profile-destinations.md) para obtener instrucciones sobre cómo activar audiencias en este destino.

### Programación

En el **[!UICONTROL Programación]** paso, puede [configuración de la programación de exportación](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling) para su [!DNL Google Cloud Storage] y también puede hacer lo siguiente [configurar el nombre de los archivos exportados](/help/destinations/ui/activate-batch-profile-destinations.md#file-names).

### Asignar atributos e identidades {#map}

En el **[!UICONTROL Asignación]** paso, puede seleccionar qué campos de atributo e identidad desea exportar para los perfiles. También puede seleccionar cambiar los encabezados del archivo exportado por cualquier nombre descriptivo que desee. Para obtener más información, consulte [paso de asignación](/help/destinations/ui/activate-batch-profile-destinations.md#mapping) en el tutorial de la interfaz de usuario activar destinos por lotes.

## (Beta) Exportar conjuntos de datos {#export-datasets}

Este destino admite exportaciones de conjuntos de datos. Para obtener información completa sobre cómo configurar exportaciones de conjuntos de datos, lea los tutoriales:

* Cómo: [exportación de conjuntos de datos mediante la interfaz de usuario de Platform](/help/destinations/ui/export-datasets.md).
* Cómo: [exportar conjuntos de datos mediante programación utilizando la API de Flow Service](/help/destinations/api/export-datasets.md).

## Validación de la exportación de datos correcta {#exported-data}

Para comprobar si los datos se han exportado correctamente, compruebe su [!DNL Google Cloud Storage] y asegúrese de que los archivos exportados contienen las poblaciones de perfiles esperadas.
