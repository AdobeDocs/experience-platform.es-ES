---
title: Pega conector de perfil
description: Utilice el conector Pega Profile para Amazon S3 en Adobe Experience Platform para exportar datos de perfil completos o incrementales, o ambos, al almacenamiento en la nube de Amazon S3. En Pega Customer decisions Hub, los trabajos de datos se pueden programar en el Diseñador de perfiles de cliente para importar datos de perfil periódicamente desde el almacenamiento de Amazon S3.
source-git-commit: bdc6ef162e9684065b60a13670848dac64be21fd
workflow-type: tm+mt
source-wordcount: '1086'
ht-degree: 1%

---


# Pega conector de perfil

## Información general {#overview}

Utilice la variable [!DNL Pega Profile Connector] en Adobe Experience Platform para crear una conexión de salida activa con su [!DNL Amazon Web Services] (AWS) Almacenamiento S3 para exportar periódicamente datos de perfil a archivos CSV desde Adobe Experience Platform a sus propios bloques S3. En [!DNL Pega Customer Decision Hub], puede programar trabajos de datos para importar estos datos de perfil desde el almacenamiento S3 para actualizar el [!DNL Pega Customer Decision Hub] perfil.

Este conector ayuda a configurar la exportación inicial de datos de perfil y también ayuda a sincronizar nuevos perfiles periódicamente en [!DNL Pega Customer Decision Hub].  El hecho de disponer de datos actualizados en el centro de decisiones de clientes proporciona una vista mejor y actualizada de su base de clientes para la toma de decisiones con las siguientes mejores medidas.

>[!IMPORTANT]
>
>Esta página de documentación fue creada por Pegasystems. Para cualquier consulta o actualización de solicitudes, contacte directamente con Pega [here](mailto:support@pega.com).

## Casos de uso

Para ayudarle a comprender mejor cómo y cuándo debe usar la variable [!DNL Pega Profile Connector] destino, aquí hay ejemplos de casos de uso que los clientes de Adobe Experience Platform pueden resolver utilizando este destino.

### Caso de uso 1

Un especialista en marketing desea configurar inicialmente [!DNL Pega Customer Decision Hub] con datos de perfil cargados desde Adobe Experience Platform. Se trata de una carga completa inicial seguida de cargas delta programadas.

### Caso de uso 2

Un especialista en marketing desea que los datos de perfil actualizados de Adobe Experience Platform estén disponibles en [!DNL Pega Customer Decision Hub] que mejora de forma continua la información de Pega sobre los perfiles de los clientes.

## Requisitos previos {#prerequisites}

Antes de poder usar este destino para exportar datos desde Adobe Experience Platform e importar perfiles a [!DNL Pega Customer Decision Hub], asegúrese de completar los siguientes requisitos previos:

* Configurar [!DNL Amazon S3] bucket y la ruta de carpeta que se utilizará para la exportación e importación de archivos de datos.
* Configure las variables [!DNL Amazon S3] clave de acceso y [!DNL Amazon S3] clave secreta: En [!DNL Amazon S3], genere un `access key - secret access key` par para conceder acceso a Platform a su [!DNL Amazon S3] cuenta.
* Para conectar y exportar datos correctamente a su [!DNL Amazon S3] ubicación de almacenamiento, cree un usuario de Identity and Access Management (IAM) para [!DNL Platform] en [!DNL Amazon S3] y asignar permisos como `s3:DeleteObject`, `s3:GetBucketLocation`, `s3:GetObject`, `s3:ListBucket`, `s3:PutObject`, `s3:ListMultipartUploadParts`
* Asegúrese de que [!DNL Pega Customer Decision Hub] se actualiza a la versión 8.8 o superior.

## Identidades compatibles {#supported-identities}

[!DNL Pega Customer Decision Hub] admite la activación de ID de usuario personalizados que se describen en la tabla siguiente. Para obtener más información, consulte [identidades](/help/identity-service/namespaces.md).

| Identidad de Target | Descripción |
|---|---|
| *CustomerID* | Identificador de usuario común que identifica de forma exclusiva un perfil en [!DNL Pega Customer Decision Hub] y Adobe Experience Platform |

{style=&quot;table-layout:auto&quot;}

## Tipo de exportación y frecuencia {#export-type-frequency}

Consulte la tabla siguiente para obtener información sobre el tipo y la frecuencia de exportación de destino.

| Elemento | Tipo | Notas |
|---------|----------|---------|
| Tipo de exportación | **[!UICONTROL Basado en perfiles]** | Está exportando todos los miembros de un segmento, junto con los campos de esquema deseados (por ejemplo: dirección de correo electrónico, número de teléfono, apellidos), tal como se elige en la pantalla seleccionar atributos de perfil del [flujo de trabajo de activación de destino](../../ui/activate-batch-profile-destinations.md#select-attributes). |
| Frecuencia de exportación | **[!UICONTROL Lote]** | Los destinos de lote exportan archivos a plataformas descendentes en incrementos de tres, seis, ocho, doce o veinticuatro horas. Más información sobre [destinos basados en archivos por lotes](/help/destinations/destination-types.md#file-based). |

{style=&quot;table-layout:auto&quot;}

## Conectarse al destino {#connect}

>[!IMPORTANT]
> 
>Para conectarse al destino, necesita la variable **[!UICONTROL Administrar destinos]** [permiso de control de acceso](/help/access-control/home.md#permissions). Lea el [información general sobre el control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Para conectarse a este destino, siga los pasos descritos en la sección [tutorial de configuración de destino](../../ui/connect-destination.md). En el flujo de trabajo de configuración de destino, rellene los campos que aparecen en las dos secciones siguientes.

### Autenticar en destino {#authenticate}

Para autenticarse en el destino, rellene los campos obligatorios y seleccione **[!UICONTROL Conectarse al destino]**.

* **[!DNL Amazon S3]clave de acceso** y **[!DNL Amazon S3]clave secreta**: En [!DNL Amazon S3], genere un `access key - secret access key` par para conceder acceso a Adobe Experience Platform a su [!DNL Amazon S3] cuenta. Obtenga más información en la [Documentación de Amazon Web Service](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html).

### Rellenar detalles de destino {#destination-details}

Después de establecer la conexión de autenticación en [!DNL Amazon S3], proporcione la siguiente información para el destino:

![Imagen de la pantalla de la interfaz de usuario que muestra los campos completados para los detalles de destino del conector Pega Perfil](../../assets/catalog/personalization/pega-profile/pega-profile-connect-destination.png)

Para configurar los detalles del destino, rellene los campos obligatorios y seleccione **[!UICONTROL Siguiente]**. Un asterisco junto a un campo en la interfaz de usuario indica que el campo es obligatorio.

* **[!UICONTROL Nombre]**: introduzca un nombre que le ayudará a identificar este destino.
* **[!UICONTROL Descripción]**: introduzca una descripción de este destino.
* **[!UICONTROL Nombre del depósito]**: introduzca el nombre del [!DNL Amazon S3] contenedor que utilizará este destino.
* **[!UICONTROL Ruta de carpeta]**: introduzca la ruta a la carpeta de destino que alojará los archivos exportados.
* **[!UICONTROL Tipo de compresión]**: Seleccione el tipo de compresión como GZIP o NONE.

>[!TIP]
>
>En el flujo de trabajo de conexión de destino, puede crear una carpeta personalizada en el almacenamiento de Amazon S3 por archivo de segmento exportado. Lectura [Utilice macros para crear una carpeta en su ubicación de almacenamiento](/help/destinations/catalog/cloud-storage/overview.md#use-macros) para obtener instrucciones.

### Habilitar alertas {#enable-alerts}

Puede activar las alertas para recibir notificaciones sobre el estado del flujo de datos a su destino. Seleccione una alerta de la lista para suscribirse y recibir notificaciones sobre el estado de su flujo de datos. Para obtener más información sobre las alertas, consulte la guía de [suscripción a alertas de destinos mediante la interfaz de usuario](../../ui/alerts.md).

Cuando haya terminado de proporcionar detalles para la conexión de destino, seleccione **[!UICONTROL Siguiente]**.

## Activar segmentos en este destino {#activate}

>[!IMPORTANT]
> 
>Para activar los datos, necesita la variable **[!UICONTROL Administrar destinos]**, **[!UICONTROL Activar destinos]**, **[!UICONTROL Ver perfiles]** y **[!UICONTROL Ver segmentos]** [permisos de control de acceso](/help/access-control/home.md#permissions). Lea el [información general sobre el control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Consulte [Activar datos de audiencia en destinos de exportación de perfiles en lote](../../ui/activate-batch-profile-destinations.md) para obtener instrucciones sobre la activación de segmentos de audiencia en este destino.

### Asignación de atributos e identidades {#map}

En el **[!UICONTROL Asignación]** , puede seleccionar qué campos de atributo e identidad desea exportar para sus perfiles. También puede seleccionar cambiar los encabezados del archivo exportado por cualquier nombre descriptivo que desee. Para obtener más información, consulte [paso de asignación](/help/destinations/ui/activate-batch-profile-destinations.md#mapping) en el tutorial activar la interfaz de usuario de los destinos de lote .

## Validación de la exportación de datos {#exported-data}

Para [!DNL Pega Profile Connector] destinos, [!DNL Platform] crea un `.csv` en la ubicación de almacenamiento de Amazon S3 que ha proporcionado. Para obtener más información sobre los archivos, consulte [Activar datos de audiencia en destinos de exportación de perfiles en lote](../../ui/activate-batch-profile-destinations.md) en el tutorial de activación de segmentos.

Una importación correcta de datos de perfil desde S3 inserta datos en la variable [!DNL Pega Customer] almacén de datos de perfil. Los datos de perfil del cliente importados se pueden validar en [!DNL Pega Customer Profile Designer] , como se muestra en la siguiente figura.
![Imagen de la pantalla de la interfaz de usuario en la que se pueden validar los datos de perfil de Adobe en el Diseñador de perfiles de cliente](../../assets/catalog/personalization/pega-profile/pega-profile-data.png)

En [!DNL Pega Customer Decision Hub], los administradores de datos pueden configurar trabajos de datos en [!DNL Customer Profile Designer] para importar datos de perfil periódicamente desde S3 como se muestra en la siguiente figura. Consulte la [recursos adicionales](#additional-resources) para obtener más información sobre cómo configurar trabajos de datos para importar datos de perfil de [!DNL Amazon S3].
![Imagen de la pantalla de la interfaz de usuario para configurar los trabajos de datos en el Diseñador de perfiles de cliente](../../assets/catalog/personalization/pega-profile/pega-profile-screen-image1.png)

## Recursos adicionales {#additional-resources}

Consulte [Importación de trabajos de datos](https://academy.pega.com/topic/import-data-jobs/v1) en [!DNL Pega Customer Decision Hub].

## Uso y gobernanza de los datos {#data-usage-governance}

Todo [!DNL Adobe Experience Platform] Los destinos de cumplen las políticas de uso de datos al administrar los datos. Para obtener información detallada sobre cómo [!DNL Adobe Experience Platform] exige el control de datos; consulte [Información general sobre la administración de datos](/help/data-governance/home.md).



