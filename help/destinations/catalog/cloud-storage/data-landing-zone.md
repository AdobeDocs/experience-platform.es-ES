---
title: Destino de la zona de aterrizaje de datos
description: Obtenga información sobre cómo conectarse a la zona de aterrizaje de datos para activar segmentos y exportar conjuntos de datos.
exl-id: 40b20faa-cce6-41de-81a0-5f15e6c00e64
source-git-commit: 6fbf1b87becebee76f583c6e44b1c42956e561ab
workflow-type: tm+mt
source-wordcount: '1163'
ht-degree: 1%

---

# (Beta) Destino de la zona de aterrizaje de datos

>[!IMPORTANT]
>
>* Este destino está actualmente en versión beta y solo está disponible para un número limitado de clientes. Para solicitar acceso a la [!DNL Data Landing Zone] conexión, póngase en contacto con su representante de Adobe y proporcione su [!DNL Organization ID].
>* Esta página de documentación hace referencia a [!DNL Data Landing Zone] *destino*. También hay un [!DNL Data Landing Zone] *source* en el catálogo de fuentes. Para obtener más información, lea la [[!DNL Data Landing Zone] source](/help/sources/connectors/cloud-storage/data-landing-zone.md) documentación.



## Información general {#overview}

[!DNL Data Landing Zone] es un [!DNL Azure Blob] interfaz de almacenamiento de información aprovisionada por Adobe Experience Platform, lo que le otorga acceso a una instalación de almacenamiento de archivos segura y basada en la nube para exportar archivos desde Platform. Tiene acceso a uno [!DNL Data Landing Zone] contenedores por entorno limitado, y el volumen total de datos en todos los contenedores se limita a los datos totales proporcionados con la licencia de productos y servicios de Platform. Todos los clientes de Platform y sus servicios de aplicación, como [!DNL Customer Journey Analytics], [!DNL Journey Orchestration], [!DNL Intelligent Services]y [!DNL Real-Time Customer Data Platform] se aprovisionan con uno [!DNL Data Landing Zone] contenedor por simulador de pruebas. Puede leer y escribir archivos en el contenedor a través de [!DNL Azure Storage Explorer] o su interfaz de línea de comandos.

[!DNL Data Landing Zone] admite la autenticación basada en SAS y sus datos están protegidos con [!DNL Azure Blob] mecanismos de seguridad del almacenamiento en reposo y en tránsito. La autenticación basada en SAS le permite acceder de forma segura a su [!DNL Data Landing Zone] a través de una conexión pública a Internet. No se requieren cambios de red para acceder a su [!DNL Data Landing Zone] contenedor, lo que significa que no necesita configurar ninguna lista de permitidos o configuración entre regiones para su red.

Platform exige un tiempo de vida estricto de siete días (TTL) en todos los archivos cargados en un [!DNL Data Landing Zone] contenedor. Todos los archivos se eliminan al cabo de siete días.

## Tipo de exportación y frecuencia {#export-type-frequency}

Consulte la tabla siguiente para obtener información sobre el tipo y la frecuencia de exportación de destino.

| Elemento | Tipo | Notas |
---------|----------|---------|
| Tipo de exportación | **[!UICONTROL Basado en perfiles]** | Está exportando todos los miembros de un segmento, junto con los campos de esquema aplicables (por ejemplo, su PPID), tal como se elige en la pantalla de selección de atributos de perfil del [flujo de trabajo de activación de destino](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes). |
| Frecuencia de exportación | **[!UICONTROL Lote]** | Los destinos de lote exportan archivos a plataformas descendentes en incrementos de tres, seis, ocho, doce o veinticuatro horas. Más información sobre [destinos basados en archivos por lotes](/help/destinations/destination-types.md#file-based). |

{style=&quot;table-layout:auto&quot;}

## Requisitos previos {#prerequisites}

Tenga en cuenta los siguientes requisitos previos que deben cumplirse para poder usar la variable [!DNL Data Landing Zone] destino.

### Conecte su [!DNL Data Landing Zone] contenedor para [!DNL Azure Storage Explorer]

Puede usar [[!DNL Azure Storage Explorer]](https://azure.microsoft.com/en-us/features/storage-explorer/) para administrar el contenido de su [!DNL Data Landing Zone] contenedor. Para empezar a usar [!DNL Data Landing Zone], primero debe recuperar sus credenciales, introdúzcalas en [!DNL Azure Storage Explorer]y conecte el [!DNL Data Landing Zone] contenedor para [!DNL Azure Storage Explorer].

En el [!DNL Azure Storage Explorer] En la interfaz de usuario, seleccione el icono de conexión en la barra de navegación izquierda. La variable **Seleccionar recurso** , proporcionando las opciones a las que conectarse. Select **[!DNL Blob container]** para conectarse a su [!DNL Data Landing Zone] almacenamiento.

![select-resource](/help/sources/images/tutorials/create/dlz/select-resource.png)

A continuación, seleccione **URL de firma de acceso compartido (SAS)** como método de conexión y, a continuación, seleccione **Siguiente**.

![select-connection-method](/help/sources/images/tutorials/create/dlz/select-connection-method.png)

Después de seleccionar el método de conexión, debe proporcionar una **nombre para mostrar** y **[!DNL Blob]URL de contenedor SAS** que corresponde a su [!DNL Data Landing Zone] contenedor.

>[!BEGINSHADEBOX]

### Recupere las credenciales de su [!DNL Data Landing Zone]

Debe utilizar las API de Platform para recuperar su [!DNL Data Landing Zone] credenciales. A continuación se describe la llamada de API para recuperar sus credenciales. Para obtener información sobre cómo obtener los valores necesarios para los encabezados, consulte la [Introducción a las API de Adobe Experience Platform](/help/landing/api-guide.md) guía.

**Formato de API**

```http
GET /data/foundation/connectors/landingzone/credentials?type=dlz_destination
```

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

La siguiente respuesta devuelve la información de credenciales de su zona de aterrizaje, incluida la `SASToken` y `SASUri`, así como el `storageAccountName` que corresponde al contenedor de su zona de aterrizaje.

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
| `containerName` | Nombre de la zona de aterrizaje. |
| `SASToken` | Token de firma de acceso compartido para su zona de aterrizaje. Esta cadena contiene toda la información necesaria para autorizar una solicitud. |
| `SASUri` | El URI de firma de acceso compartido para su zona de aterrizaje. Esta cadena es una combinación de la URI con la zona de aterrizaje a la que se está autenticando y su token SAS correspondiente, |

>[!ENDSHADEBOX]

Proporcione su nombre para mostrar (`containerName`) y [!DNL Data Landing Zone] URL de SAS, tal como se devuelve en la llamada de API descrita anteriormente, y luego seleccione **Siguiente**.

![enter-connection-info](/help/sources/images/tutorials/create/dlz/enter-connection-info.png)

La variable **Resumen** , que le proporciona una descripción general de la configuración, incluida información sobre [!DNL Blob] y permisos. Cuando esté listo, seleccione **Connect**.

![summary](/help/sources/images/tutorials/create/dlz/summary.png)

Una conexión correcta actualiza su [!DNL Azure Storage Explorer] La interfaz de usuario de [!DNL Data Landing Zone] contenedor.

![dlz-user-container](/help/sources/images/tutorials/create/dlz/dlz-user-container.png)

Con [!DNL Data Landing Zone] contenedor conectado a [!DNL Azure Storage Explorer], ahora puede empezar a exportar archivos de Experience Platform a su [!DNL Data Landing Zone] contenedor. Para exportar archivos, debe establecer una conexión con la variable [!DNL Data Landing Zone] en la interfaz de usuario del Experience Platform, tal como se describe en la sección siguiente.

## Conectarse al destino {#connect}

>[!IMPORTANT]
> 
>Para conectarse al destino, necesita la variable **[!UICONTROL Administrar destinos]** [permiso de control de acceso](/help/access-control/home.md#permissions). Lea el [información general sobre el control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Para conectarse a este destino, siga los pasos descritos en la sección [tutorial de configuración de destino](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/connect-destination.html). En el flujo de trabajo de configuración de destino, rellene los campos que aparecen en las dos secciones siguientes.

### Autenticar en destino {#authenticate}

Asegúrese de haber conectado su [!DNL Data Landing Zone] contenedor para [!DNL Azure Storage Explorer] tal como se describe en la sección [requisitos previos](#prerequisites) para obtener más información. Porque [!DNL Data Landing Zone] es un almacenamiento proporcionado por Adobes, no es necesario realizar más pasos en la interfaz de usuario del Experience Platform para autenticarse en el destino.

### Rellenar detalles de destino {#destination-details}

Para configurar los detalles del destino, rellene los campos opcionales y requeridos a continuación. Un asterisco junto a un campo en la interfaz de usuario indica que el campo es obligatorio.

* **[!UICONTROL Nombre]**: Rellene el nombre preferido para este destino.
* **[!UICONTROL Descripción]**: Opcional. Por ejemplo, puede mencionar para qué campaña utiliza este destino.
* **[!UICONTROL Ruta de carpeta]**: Introduzca la ruta a la carpeta de destino que alojará los archivos exportados.
* **[!UICONTROL Tipo de archivo]**: seleccione el Experience Platform de formato que debe utilizar para los archivos exportados. Al seleccionar la variable [!UICONTROL CSV] también puede [configuración de las opciones de formato del archivo](../../ui/batch-destinations-file-formatting-options.md).
* **[!UICONTROL Formato de compresión]**: seleccione el tipo de compresión que debe utilizar el Experience Platform para los archivos exportados.

### Habilitar alertas {#enable-alerts}

Puede activar las alertas para recibir notificaciones sobre el estado del flujo de datos a su destino. Seleccione una alerta de la lista para suscribirse y recibir notificaciones sobre el estado de su flujo de datos. Para obtener más información sobre las alertas, consulte la guía de [suscripción a alertas de destinos mediante la interfaz de usuario](../../ui/alerts.md).

Cuando haya terminado de proporcionar detalles para la conexión de destino, seleccione **[!UICONTROL Siguiente]**.

## Activar segmentos en este destino {#activate}

>[!IMPORTANT]
> 
>Para activar los datos, necesita la variable **[!UICONTROL Administrar destinos]**, **[!UICONTROL Activar destinos]**, **[!UICONTROL Ver perfiles]** y **[!UICONTROL Ver segmentos]** [permisos de control de acceso](/help/access-control/home.md#permissions). Lea el [información general sobre el control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Consulte [Activar datos de audiencia en destinos de exportación de perfiles en lote](../../ui/activate-batch-profile-destinations.md) para obtener instrucciones sobre la activación de segmentos de audiencia en este destino.

### Programación

En el **[!UICONTROL Programación]** paso, puede [configuración de la programación de exportación](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling) para su [!DNL Data Landing Zone] destino y también puede [configurar el nombre de los archivos exportados](/help/destinations/ui/activate-batch-profile-destinations.md#file-names).

### Asignación de atributos e identidades {#map}

En el **[!UICONTROL Asignación]** , puede seleccionar qué campos de atributo e identidad desea exportar para sus perfiles. También puede seleccionar cambiar los encabezados del archivo exportado por cualquier nombre descriptivo que desee. Para obtener más información, consulte [paso de asignación](/help/destinations/ui/activate-batch-profile-destinations.md#mapping) en el tutorial activar la interfaz de usuario de los destinos de lote .

## (Beta) Exportar conjuntos de datos {#export-datasets}

Este destino admite exportaciones de conjuntos de datos. Para obtener información completa sobre cómo configurar las exportaciones de conjuntos de datos, lea la [tutorial de exportación de conjuntos de datos](/help/destinations/ui/export-datasets.md).

## Validar la exportación de datos correcta {#exported-data}

Para comprobar si los datos se han exportado correctamente, consulte [!DNL Data Landing Zone] y asegúrese de que los archivos exportados contienen las poblaciones de perfiles esperadas.
