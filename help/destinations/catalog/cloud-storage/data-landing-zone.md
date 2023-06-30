---
title: Destino de zona de aterrizaje de datos
description: Obtenga información sobre cómo conectarse a la zona de aterrizaje de datos para activar segmentos y exportar conjuntos de datos.
exl-id: 40b20faa-cce6-41de-81a0-5f15e6c00e64
source-git-commit: cf89f40625bedda633ad26cf3e882983600f0d52
workflow-type: tm+mt
source-wordcount: '1378'
ht-degree: 1%

---

# (Beta) Destino de la zona de aterrizaje de datos

>[!IMPORTANT]
>
>* Este destino está actualmente en versión beta y solo está disponible para un número limitado de clientes. Para solicitar acceso a [!DNL Data Landing Zone] conexión, póngase en contacto con el representante del Adobe y proporcione a [!DNL Organization ID].
>* Esta página de documentación hace referencia a [!DNL Data Landing Zone] *destino*. También hay un [!DNL Data Landing Zone] *origen* en el catálogo de fuentes. Para obtener más información, lea la [[!DNL Data Landing Zone] origen](/help/sources/connectors/cloud-storage/data-landing-zone.md) documentación.


## Información general {#overview}

[!DNL Data Landing Zone] es un [!DNL Azure Blob] interfaz de almacenamiento aprovisionada por Adobe Experience Platform, que le concede acceso a una función de almacenamiento de archivos segura y basada en la nube para exportar archivos fuera de Platform. Tiene acceso a uno [!DNL Data Landing Zone] contenedor por zona protegida y el volumen total de datos en todos los contenedores se limita a los datos totales proporcionados con la licencia de productos y servicios de Platform. Todos los clientes de Platform y sus servicios de aplicaciones como [!DNL Customer Journey Analytics], [!DNL Journey Orchestration], [!DNL Intelligent Services], y [!DNL Real-Time Customer Data Platform] se han aprovisionado con uno [!DNL Data Landing Zone] contenedor por zona protegida. Puede leer y escribir archivos en el contenedor mediante [!DNL Azure Storage Explorer] o su interfaz de línea de comandos.

[!DNL Data Landing Zone] admite la autenticación basada en SAS y sus datos están protegidos con [!DNL Azure Blob] mecanismos de seguridad de almacenamiento en reposo y en tránsito. La autenticación basada en SAS le permite acceder de forma segura a su [!DNL Data Landing Zone] a través de una conexión pública a internet. No se requieren cambios de red para acceder a su [!DNL Data Landing Zone] contenedor, lo que significa que no es necesario configurar listas de permitidos ni configuraciones entre regiones para la red.

Platform aplica un estricto tiempo de vida de siete días (TTL) a todos los archivos cargados en una [!DNL Data Landing Zone] contenedor. Todos los archivos se eliminan a los siete días.

## Conéctese a su [!UICONTROL Zona de aterrizaje de datos] mediante API o IU {#connect-api-or-ui}

* Para conectarse a su [!UICONTROL Zona de aterrizaje de datos] Ubicación de almacenamiento mediante la interfaz de usuario de Platform, lea las secciones [Conectar con el destino](#connect) y [Activar segmentos en este destino](#activate) más abajo.
* Para conectarse a su [!UICONTROL Zona de aterrizaje de datos] ubicación de almacenamiento mediante programación, lea el [Activación de segmentos en destinos basados en archivos mediante el tutorial de la API de Flow Service](../../api/activate-segments-file-based-destinations.md).

## Tipo y frecuencia de exportación {#export-type-frequency}

Consulte la tabla siguiente para obtener información sobre el tipo y la frecuencia de exportación de destino.

| Elemento | Tipo | Notas |
---------|----------|---------|
| Tipo de exportación | **[!UICONTROL Basado en perfiles]** | Está exportando todos los miembros de un segmento, junto con los campos de esquema aplicables (por ejemplo, su PPID), tal como se elige en la pantalla Seleccionar atributos de perfil del [flujo de trabajo de activación de destino](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes). |
| Frecuencia de exportación | **[!UICONTROL Lote]** | Los destinos por lotes exportan archivos a plataformas descendentes en incrementos de tres, seis, ocho, doce o veinticuatro horas. Más información sobre [destinos basados en archivos por lotes](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## Requisitos previos {#prerequisites}

Tenga en cuenta los siguientes requisitos previos que deben cumplirse para poder utilizar la variable [!DNL Data Landing Zone] destino.

### Conecte su [!DNL Data Landing Zone] contenedor a [!DNL Azure Storage Explorer]

Puede utilizar [[!DNL Azure Storage Explorer]](https://azure.microsoft.com/en-us/products/storage/storage-explorer/) para administrar el contenido de su [!DNL Data Landing Zone] contenedor. Para empezar a utilizar [!DNL Data Landing Zone], primero debe recuperar las credenciales e introducirlas en [!DNL Azure Storage Explorer]y conecte su [!DNL Data Landing Zone] contenedor a [!DNL Azure Storage Explorer].

En el [!DNL Azure Storage Explorer] IU, seleccione el icono de conexión en la barra de navegación izquierda. El **Seleccionar medio** aparece una ventana de, que le proporciona opciones para conectarse a. Seleccionar **[!DNL Blob container]** para conectarse a su [!DNL Data Landing Zone] almacenamiento.

![select-resource](/help/sources/images/tutorials/create/dlz/select-resource.png)

A continuación, seleccione **URL de firma de acceso compartido (SAS)** como método de conexión y, a continuación, seleccione **Siguiente**.

![select-connection-method](/help/sources/images/tutorials/create/dlz/select-connection-method.png)

Después de seleccionar el método de conexión, debe proporcionar un **nombre para mostrar** y el **[!DNL Blob]URL de SAS de contenedor** que se corresponde con su [!DNL Data Landing Zone] contenedor.

>[!BEGINSHADEBOX]

### Recupere las credenciales de su [!DNL Data Landing Zone]

Debe utilizar las API de Platform para recuperar los [!DNL Data Landing Zone] credenciales. A continuación, se describe la llamada de API para recuperar sus credenciales. Para obtener información sobre la obtención de los valores necesarios para los encabezados, consulte la [Introducción a las API de Adobe Experience Platform](/help/landing/api-guide.md) guía.

**Formato de API**

```http
GET /data/foundation/connectors/landingzone/credentials?type=dlz_destination
```

| Parámetros de consulta | Descripción |
| --- | --- |
| `dlz_destination` | El `dlz_destination` permite a la API distinguir un contenedor de destino de zona de aterrizaje de otros tipos de contenedores disponibles para usted. |

{style="table-layout:auto"}

**Solicitud**

El siguiente ejemplo de solicitud recupera las credenciales de una zona de aterrizaje existente.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/connectors/landingzone/credentials?type=dlz_destination' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

**Respuesta**

La siguiente respuesta devuelve la información de credenciales de la zona de aterrizaje, incluida la actual `SASToken` y `SASUri`, y el `storageAccountName` que corresponde al contenedor de la zona de aterrizaje.

```json
{
    "containerName": "dlz-user-container",
    "SASToken": "sv=2022-09-11&si=dlz-ed86a61d-201f-4b50-b10f-a1bf173066fd&sr=c&sp=racwdlm&sig=4yTba8voU3L0wlcLAv9mZLdZ7NlMahbfYYPTMkQ6ZGU%3D",
    "storageAccountName": "dlblobstore99hh25i3df123",
    "SASUri": "https://dlblobstore99hh25i3dflek.blob.core.windows.net/dlz-user-container?sv=2022-09-11&si=dlz-ed86a61d-201f-4b50-b10f-a1bf173066fd&sr=c&sp=racwdlm&sig=4yTba8voU3L0wlcLAv9mZLdZ7NlMahbfYYPTMkQ6ZGU%3D"
}
```

| Propiedad | Descripción |
| --- | --- |
| `containerName` | El nombre de su zona de aterrizaje. |
| `SASToken` | El token de firma de acceso compartido para su zona de aterrizaje. Esta cadena contiene toda la información necesaria para autorizar una solicitud. |
| `SASUri` | El URI de firma de acceso compartido para su zona de aterrizaje. Esta cadena es una combinación del URI de la zona de aterrizaje para la que se está autenticando y su token SAS correspondiente, |

{style="table-layout:auto"}

## Actualizar [!DNL Data Landing Zone] credenciales

También puede actualizar sus credenciales cuando lo desee. Puede actualizar su `SASToken` realizando una petición de POST a la `/credentials` punto final del [!DNL Connectors] API.

**Formato de API**

```http
POST /data/foundation/connectors/landingzone/credentials?type=dlz_destination&action=refresh
```

| Parámetros de consulta | Descripción |
| --- | --- |
| `dlz_destination` | El `dlz_destination` permite a la API distinguir un contenedor de destino de zona de aterrizaje de otros tipos de contenedores disponibles para usted. |
| `refresh` | El `refresh` Esta acción le permite restablecer las credenciales de su zona de aterrizaje y generar automáticamente una nueva `SASToken`. |

{style="table-layout:auto"}

**Solicitud**

La siguiente solicitud actualiza las credenciales de la zona de aterrizaje.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/connectors/landingzone/credentials?type=dlz_destination&action=refresh' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

**Respuesta**

La siguiente respuesta devuelve valores actualizados para su `SASToken` y `SASUri`.

```json
{
    "containerName": "dlz-user-container",
    "SASToken": "sv=2020-04-08&si=dlz-9c4d03b8-a6ff-41be-9dcf-20123e717e99&sr=c&sp=racwdlm&sig=JbRMoDmFHQU4OWOpgrKdbZ1d%2BkvslO35%2FXTqBO%2FgbRA%3D",
    "storageAccountName": "dlblobstore99hh25i3dflek",
    "SASUri": "https://dlblobstore99hh25i3dflek.blob.core.windows.net/dlz-user-container?sv=2020-04-08&si=dlz-9c4d03b8-a6ff-41be-9dcf-20123e717e99&sr=c&sp=racwdlm&sig=JbRMoDmFHQU4OWOpgrKdbZ1d%2BkvslO35%2FXTqBO%2FgbRA%3D"
}
```

>[!ENDSHADEBOX]

Proporcione su nombre para mostrar (`containerName`) y [!DNL Data Landing Zone] URL de SAS, tal como se devuelve en la llamada de API descrita anteriormente, y luego seleccione **Siguiente**.

![enter-connection-info](/help/sources/images/tutorials/create/dlz/enter-connection-info.png)

El **Resumen** aparece una ventana que le proporciona información general sobre su configuración, incluida la información sobre su [!DNL Blob] punto de conexión y permisos. Cuando esté listo, seleccione **Connect**.

![summary](/help/sources/images/tutorials/create/dlz/summary.png)

Una conexión correcta actualiza su [!DNL Azure Storage Explorer] Interfaz de usuario con su [!DNL Data Landing Zone] contenedor.

![dlz-user-container](/help/sources/images/tutorials/create/dlz/dlz-user-container.png)

Con su [!DNL Data Landing Zone] contenedor conectado a [!DNL Azure Storage Explorer], ahora puede empezar a exportar archivos de Experience Platform a su [!DNL Data Landing Zone] contenedor. Para exportar archivos, debe establecer una conexión con el [!DNL Data Landing Zone] en la interfaz de usuario de Experience Platform, tal como se describe en la sección siguiente.

## Conectar con el destino {#connect}

>[!IMPORTANT]
> 
>Para conectarse al destino, necesita el **[!UICONTROL Administrar destinos]** [permiso de control de acceso](/help/access-control/home.md#permissions). Lea el [información general de control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Para conectarse a este destino, siga los pasos descritos en la sección [tutorial de configuración de destino](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/connect-destination.html). En el flujo de trabajo de configuración de destino, rellene los campos enumerados en las dos secciones siguientes.

### Autenticar en el destino {#authenticate}

Asegúrese de haber conectado su [!DNL Data Landing Zone] contenedor a [!DNL Azure Storage Explorer] como se describe en la [requisitos previos](#prerequisites) sección. Porque [!DNL Data Landing Zone] es un almacenamiento aprovisionado por Adobe, no es necesario realizar ningún paso adicional en la interfaz de usuario de Experience Platform para autenticarse en el destino.

### Rellenar detalles de destino {#destination-details}

Para configurar los detalles del destino, rellene los campos obligatorios y opcionales a continuación. Un asterisco junto a un campo en la interfaz de usuario indica que el campo es obligatorio.

* **[!UICONTROL Nombre]**: complete el nombre preferido para este destino.
* **[!UICONTROL Descripción]**: Opcional. Por ejemplo, puede mencionar para qué campaña está usando este destino.
* **[!UICONTROL Ruta de carpeta]**: introduzca la ruta a la carpeta de destino que alojará los archivos exportados.
* **[!UICONTROL Tipo de archivo]**: seleccione el Experience Platform de formato que debe utilizar para los archivos exportados. Al seleccionar la variable [!UICONTROL CSV] , también puede hacer lo siguiente [configurar las opciones de formato de archivo](../../ui/batch-destinations-file-formatting-options.md).
* **[!UICONTROL Formato de compresión]**: seleccione el tipo de compresión que el Experience Platform debe utilizar para los archivos exportados.
* **[!UICONTROL Incluir archivo de manifiesto]**: active esta opción si desea que las exportaciones incluyan un archivo JSON de manifiesto que contenga información sobre la ubicación de exportación, el tamaño de exportación, etc.

### Habilitar alertas {#enable-alerts}

Puede activar alertas para recibir notificaciones sobre el estado del flujo de datos a su destino. Seleccione una alerta de la lista a la que suscribirse para recibir notificaciones sobre el estado del flujo de datos. Para obtener más información sobre las alertas, consulte la guía de [suscripción a alertas de destinos mediante la IU](../../ui/alerts.md).

Cuando haya terminado de proporcionar detalles para la conexión de destino, seleccione **[!UICONTROL Siguiente]**.

## Activar segmentos en este destino {#activate}

>[!IMPORTANT]
> 
>Para activar los datos, necesita el **[!UICONTROL Administrar destinos]**, **[!UICONTROL Activar destinos]**, **[!UICONTROL Ver perfiles]**, y **[!UICONTROL Ver segmentos]** [permisos de control de acceso](/help/access-control/home.md#permissions). Lea el [información general de control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Consulte [Activar datos de audiencia en destinos de exportación de perfiles por lotes](../../ui/activate-batch-profile-destinations.md) para obtener instrucciones sobre cómo activar segmentos de audiencia en este destino.

### Programación

En el **[!UICONTROL Programación]** paso, puede [configuración de la programación de exportación](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling) para su [!DNL Data Landing Zone] y también puede hacer lo siguiente [configurar el nombre de los archivos exportados](/help/destinations/ui/activate-batch-profile-destinations.md#file-names).

### Asignar atributos e identidades {#map}

En el **[!UICONTROL Asignación]** paso, puede seleccionar qué campos de atributo e identidad desea exportar para los perfiles. También puede seleccionar cambiar los encabezados del archivo exportado por cualquier nombre descriptivo que desee. Para obtener más información, consulte [paso de asignación](/help/destinations/ui/activate-batch-profile-destinations.md#mapping) en el tutorial de la interfaz de usuario activar destinos por lotes.

## (Beta) Exportar conjuntos de datos {#export-datasets}

Este destino admite exportaciones de conjuntos de datos. Para obtener información completa sobre cómo configurar exportaciones de conjuntos de datos, lea los tutoriales:

* Cómo: [exportación de conjuntos de datos mediante la interfaz de usuario de Platform](/help/destinations/ui/export-datasets.md).
* Cómo: [exportar conjuntos de datos mediante programación utilizando la API de Flow Service](/help/destinations/api/export-datasets.md).

## Validación de la exportación de datos correcta {#exported-data}

Para comprobar si los datos se han exportado correctamente, compruebe su [!DNL Data Landing Zone] y asegúrese de que los archivos exportados contienen las poblaciones de perfiles esperadas.
