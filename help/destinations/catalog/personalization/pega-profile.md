---
title: Conector De Perfil Pega
description: Utilice el conector de perfil Pega para Amazon S3 en Adobe Experience Platform para exportar datos de perfil completos o incrementales, o ambos, al almacenamiento en la nube de Amazon S3. En el centro de decisiones del cliente de Pega, los trabajos de datos se pueden programar en el Diseñador de perfiles de cliente para importar datos de perfil periódicamente desde el almacenamiento de Amazon S3.
last-substantial-update: 2023-01-25T00:00:00Z
exl-id: f422f21b-174a-4b93-b05d-084b42623314
source-git-commit: 05e996f9e33e0d8be3d15a9ab3baaaf6d8152b5a
workflow-type: tm+mt
source-wordcount: '1120'
ht-degree: 2%

---

# Conector De Perfil Pega

## Información general {#overview}

Utilice el [!DNL Pega Profile Connector] en Adobe Experience Platform para crear una conexión saliente activa con su [!DNL Amazon Web Services] (AWS) Almacenamiento de S3 para exportar periódicamente datos de perfil a archivos CSV desde Adobe Experience Platform en sus propios contenedores de S3. En [!DNL Pega Customer Decision Hub], puede programar trabajos de datos para importar estos datos de perfil desde el almacenamiento de S3 y actualizar el perfil [!DNL Pega Customer Decision Hub].

Este conector ayuda a configurar la exportación inicial de datos de perfil y también ayuda a sincronizar nuevos perfiles periódicamente en [!DNL Pega Customer Decision Hub].  Tener datos actualizados en Customer Decision Hub proporciona una vista mejor y actualizada de su base de clientes para la toma de decisiones de la siguiente mejor acción.

>[!IMPORTANT]
>
>Pegasystems crea y mantiene este conector de destino y esta página de documentación. Para cualquier consulta o solicitud de actualización, póngase en contacto directamente con Pega [aquí](mailto:support@pega.com).

## Casos de uso

Para ayudarle a comprender mejor cómo y cuándo debe utilizar el [!DNL Pega Profile Connector] Destino. Estos son ejemplos de casos de uso que los clientes de Adobe Experience Platform pueden solucionar mediante este destino.

### Caso de uso 1

Un experto en marketing desea configurar inicialmente [!DNL Pega Customer Decision Hub] con datos de perfil cargados desde Adobe Experience Platform. Se trata de una carga completa inicial seguida de cargas delta programadas.

### Caso de uso 2

Un especialista en marketing desea tener disponibles datos de perfil actualizados de Adobe Experience Platform en [!DNL Pega Customer Decision Hub] que mejora la información de Pega en torno a los perfiles de los clientes de forma continua.

## Requisitos previos {#prerequisites}

Antes de poder usar este destino para exportar datos desde Adobe Experience Platform e importar perfiles en [!DNL Pega Customer Decision Hub], asegúrese de completar los siguientes requisitos previos:

* Configurar [!DNL Amazon S3] contenedor y ruta de la carpeta que se utilizará para la exportación e importación de archivos de datos.
* Configure las variables [!DNL Amazon S3] clave de acceso y [!DNL Amazon S3] clave secreta: en [!DNL Amazon S3], genere un `access key - secret access key` par para conceder acceso de plataforma a su [!DNL Amazon S3] cuenta.
* Para conectar y exportar datos correctamente a su [!DNL Amazon S3] ubicación de almacenamiento, crear un usuario de Identity and Access Management (IAM) para [!DNL Platform] in [!DNL Amazon S3] y asignar permisos como `s3:DeleteObject`, `s3:GetBucketLocation`, `s3:GetObject`, `s3:ListBucket`, `s3:PutObject`, `s3:ListMultipartUploadParts`
* Asegúrese de que su [!DNL Pega Customer Decision Hub] La instancia de se ha actualizado a la versión 8.8 o superior.

## Identidades admitidas {#supported-identities}

[!DNL Pega Customer Decision Hub] admite la activación de los ID de usuario personalizados que se describen en la tabla siguiente. Para obtener más información, consulte [identidades](/help/identity-service/namespaces.md).

| Identidad de destino | Descripción |
|---|---|
| *CustomerID* | Identificador de usuario común que identifica de forma exclusiva un perfil en [!DNL Pega Customer Decision Hub] y ADOBE EXPERIENCE PLATFORM |

{style="table-layout:auto"}

## Tipo y frecuencia de exportación {#export-type-frequency}

Consulte la tabla siguiente para obtener información sobre el tipo y la frecuencia de exportación de destino.

| Elemento | Tipo | Notas |
|---------|----------|---------|
| Tipo de exportación | **[!UICONTROL Basado en perfiles]** | Va a exportar todos los miembros de un segmento, junto con los campos de esquema deseados (por ejemplo: dirección de correo electrónico, número de teléfono, apellidos), tal como se elige en la pantalla seleccionar atributos de perfil del [flujo de trabajo de activación de destino](../../ui/activate-batch-profile-destinations.md#select-attributes). |
| Frecuencia de exportación | **[!UICONTROL Lote]** | Los destinos por lotes exportan archivos a plataformas descendentes en incrementos de tres, seis, ocho, doce o veinticuatro horas. Más información sobre [destinos basados en archivos por lotes](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## Conectar con el destino {#connect}

>[!IMPORTANT]
> 
>Para conectarse al destino, necesita el **[!UICONTROL Administrar destinos]** [permiso de control de acceso](/help/access-control/home.md#permissions). Lea el [información general de control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Para conectarse a este destino, siga los pasos descritos en la sección [tutorial de configuración de destino](../../ui/connect-destination.md). En el flujo de trabajo de configuración de destino, rellene los campos enumerados en las dos secciones siguientes.

### Autenticar en el destino {#authenticate}

Para autenticarse en el destino, rellene los campos obligatorios y seleccione **[!UICONTROL Conectar con destino]**.

* **[!DNL Amazon S3]tecla de acceso** y **[!DNL Amazon S3]clave secreta**: en [!DNL Amazon S3], genere un `access key - secret access key` emparejar para conceder acceso a Adobe Experience Platform a su [!DNL Amazon S3] cuenta. Obtenga más información en la [Documentación de Amazon Web Service](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html).

### Rellenar detalles de destino {#destination-details}

Después de establecer la conexión de autenticación con [!DNL Amazon S3], proporcione la siguiente información para el destino:

![Imagen de la pantalla de la interfaz de usuario que muestra los campos completados para los detalles de destino del conector de perfil de Pega](../../assets/catalog/personalization/pega-profile/pega-profile-connect-destination.png)

Para configurar los detalles del destino, rellene los campos obligatorios y seleccione **[!UICONTROL Siguiente]**. Un asterisco junto a un campo en la interfaz de usuario indica que el campo es obligatorio.

* **[!UICONTROL Nombre]**: introduzca un nombre que le ayude a identificar este destino.
* **[!UICONTROL Descripción]**: introduzca una descripción para este destino.
* **[!UICONTROL Nombre del cubo]**: introduzca el nombre del [!DNL Amazon S3] contenedor que utilizará este destino.
* **[!UICONTROL Ruta de carpeta]**: introduzca la ruta a la carpeta de destino que alojará los archivos exportados.
* **[!UICONTROL Tipo de compresión]**: seleccione el tipo de compresión como GZIP o NONE.

>[!TIP]
>
>En el flujo de trabajo Connect destination, puede crear una carpeta personalizada en el almacenamiento de Amazon S3 por archivo de audiencia exportado. Leer [Usar macros para crear una carpeta en la ubicación de almacenamiento](/help/destinations/catalog/cloud-storage/overview.md#use-macros) para obtener instrucciones.

### Habilitar alertas {#enable-alerts}

Puede activar alertas para recibir notificaciones sobre el estado del flujo de datos a su destino. Seleccione una alerta de la lista a la que suscribirse para recibir notificaciones sobre el estado del flujo de datos. Para obtener más información sobre las alertas, consulte la guía de [suscripción a alertas de destinos mediante la IU](../../ui/alerts.md).

Cuando haya terminado de proporcionar detalles para la conexión de destino, seleccione **[!UICONTROL Siguiente]**.

## Activar audiencias en este destino {#activate}

>[!IMPORTANT]
> 
>* Para activar los datos, necesita el **[!UICONTROL Administrar destinos]**, **[!UICONTROL Activar destinos]**, **[!UICONTROL Ver perfiles]**, y **[!UICONTROL Ver segmentos]** [permisos de control de acceso](/help/access-control/home.md#permissions). Lea el [información general de control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.
>* Para exportar *identidades*, necesita el **[!UICONTROL Ver gráfico de identidad]** [permiso de control de acceso](/help/access-control/home.md#permissions). <br> ![Seleccione el área de nombres de identidad resaltada en el flujo de trabajo para activar audiencias en los destinos.](/help/destinations/assets/overview/export-identities-to-destination.png "Seleccione el área de nombres de identidad resaltada en el flujo de trabajo para activar audiencias en los destinos."){width="100" zoomable="yes"}

Consulte [Activar datos de audiencia en destinos de exportación de perfiles por lotes](../../ui/activate-batch-profile-destinations.md) para obtener instrucciones sobre cómo activar audiencias en este destino.

### Asignar atributos e identidades {#map}

En el **[!UICONTROL Asignación]** paso, puede seleccionar qué campos de atributo e identidad desea exportar para los perfiles. También puede seleccionar cambiar los encabezados del archivo exportado por cualquier nombre descriptivo que desee. Para obtener más información, consulte [paso de asignación](/help/destinations/ui/activate-batch-profile-destinations.md#mapping) en el tutorial de la interfaz de usuario activar destinos por lotes.

## Validar exportación de datos {#exported-data}

Para [!DNL Pega Profile Connector] destinos, [!DNL Platform] crea un `.csv` en la ubicación de almacenamiento de Amazon S3 proporcionada. Para obtener más información sobre los archivos, consulte [Activar datos de audiencia en destinos de exportación de perfiles por lotes](../../ui/activate-batch-profile-destinations.md) en el tutorial de activación de audiencia.

Si la importación de datos de perfil de S3 se realiza correctamente, los datos se insertan en [!DNL Pega Customer] almacén de datos de perfil. Los datos de perfil del cliente importados se pueden validar en [!DNL Pega Customer Profile Designer] , como se muestra en la siguiente figura.
![Imagen de la pantalla de la IU de donde se pueden validar los datos del perfil de Adobe en el Diseñador de perfiles de cliente](../../assets/catalog/personalization/pega-profile/pega-profile-data.png)

Entrada [!DNL Pega Customer Decision Hub], los administradores de datos pueden configurar los trabajos de datos en [!DNL Customer Profile Designer] para importar datos de perfil periódicamente desde S3, como se muestra en la siguiente figura. Consulte la [recursos adicionales](#additional-resources) para obtener más información sobre cómo configurar trabajos de datos para importar datos de perfil de [!DNL Amazon S3].
![Imagen de la pantalla IU para configurar los trabajos de datos en el Diseñador de perfiles de cliente](../../assets/catalog/personalization/pega-profile/pega-profile-screen-image1.png)

## Recursos adicionales {#additional-resources}

Consulte [Importar trabajos de datos](https://academy.pega.com/topic/import-data-jobs/v1) in [!DNL Pega Customer Decision Hub].

## Uso de datos y gobernanza {#data-usage-governance}

Todo [!DNL Adobe Experience Platform] Los destinos de cumplen con las políticas de uso de datos al gestionar los datos. Para obtener información detallada sobre cómo [!DNL Adobe Experience Platform] aplica la gobernanza de datos. Consulte la [Resumen de gobernanza de datos](/help/data-governance/home.md).
