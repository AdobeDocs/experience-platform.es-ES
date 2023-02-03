---
title: (Beta) [!DNL Google Ad Manager 360] connection
description: Google Ad Manager 360 es una plataforma de servicio de publicidad de Google que proporciona a los editores los medios para administrar la visualización de anuncios en sus sitios web, a través de vídeo y en aplicaciones móviles.
exl-id: 3251145a-3e4d-40aa-b120-d79c8c9c7cae
source-git-commit: ec4d064f90348f9eafb1d0fe4b9df5e102295507
workflow-type: tm+mt
source-wordcount: '926'
ht-degree: 2%

---

# (Beta) [!DNL Google Ad Manager 360] connection

## Información general {#overview}

La variable [!DNL Google Ad Manager 360] la conexión habilita la carga por lotes para [!DNL publisher provided identifiers] (PPID) en [!DNL Google Ad Manager 360], a través de [!DNL Google Cloud Storage].

Para obtener más información sobre cómo funcionan los identificadores proporcionados por el editor en Google Ad Manager 360, consulte la [documentación oficial de Google](https://support.google.com/admanager/answer/2880055?hl=en).

>[!IMPORTANT]
>
>Este destino está actualmente en versión beta y solo está disponible para un número limitado de clientes. Para solicitar acceso a la [!DNL Google Ad Manager 360] conexión, póngase en contacto con su representante de Adobe y proporcione su [!DNL IMS Organization ID].

La variable [!DNL Google Ad Manager 360] exportaciones de destino [!DNL CSV] los archivos de [!DNL Google Cloud Storage] cubo. Una vez que haya exportado la variable [!DNL CSV] archivos, debe importarlos en su [!DNL Google Ad Manager 360] cuenta.

## Detalles de destino {#specifics}

Tenga en cuenta los siguientes detalles que son específicos de [!DNL Google Ad Manager 360] destinos.

* Las audiencias activadas se crean mediante programación en la plataforma Google y se rellenan en el archivo CSV.

## Identidades compatibles {#supported-identities}

[!DNL This integration] admite la activación de identidades descritas en la tabla siguiente.

| Identidad de Target | Descripción | Consideraciones |
|---|---|---|
| PPID | [!DNL Publisher provided ID] | Seleccione esta identidad de destino para enviar audiencias a [!DNL Google Ad Manager 360] |

{style=&quot;table-layout:auto&quot;}

## Tipo de exportación y frecuencia {#export-type-frequency}

Consulte la tabla siguiente para obtener información sobre el tipo y la frecuencia de exportación de destino.

| Elemento | Tipo | Notas |
---------|----------|---------|
| Tipo de exportación | **[!UICONTROL Basado en perfiles]** | Está exportando todos los miembros de un segmento, junto con los campos de esquema aplicables (por ejemplo, su PPID), tal como se elige en la pantalla de selección de atributos de perfil del [flujo de trabajo de activación de destino](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes). |
| Frecuencia de exportación | **[!UICONTROL Lote]** | Los destinos de lote exportan archivos a plataformas descendentes en incrementos de tres, seis, ocho, doce o veinticuatro horas. Más información sobre [destinos basados en archivos por lotes](/help/destinations/destination-types.md#file-based). |

{style=&quot;table-layout:auto&quot;}

## Requisitos previos {#prerequisites}

### Permitir inclusión en la lista {#allow-listing}

La inclusión en la lista de permitidos es obligatoria antes de configurar la primera [!DNL Google Ad Manager 360] destino en Platform. Asegúrese de completar el proceso de inclusión en la lista de permitidos que se describe a continuación antes de crear su destino.

>[!NOTE]
>
>La excepción a esta regla es para [Audience Manager](https://docs.adobe.com/content/help/es-ES/experience-cloud/user-guides/home.translate.html) clientes. Si ya ha creado una conexión con este destino de Google en Audience Manager, no es necesario volver a pasar por el proceso de inclusión en la lista de permitidos y puede continuar con los pasos siguientes.

1. Siga los pasos descritos en la sección [Documentación de Google Ad Manager](https://support.google.com/admanager/answer/3289669?hl=en) para agregar Adobe como plataforma de administración de datos (DMP) vinculada.
2. En el [!DNL Google Ad Manager] interfaz, vaya a **[!UICONTROL Administrador]** > **[!UICONTROL Configuración global]** > **[!UICONTROL Configuración de red]** y habilite **[!UICONTROL Acceso a la API]** control deslizante.


## Conectarse al destino {#connect}

>[!IMPORTANT]
> 
>Para conectarse al destino, necesita la variable **[!UICONTROL Administrar destinos]** [permiso de control de acceso](/help/access-control/home.md#permissions). Lea el [información general sobre el control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Para conectarse a este destino, siga los pasos descritos en la sección [tutorial de configuración de destino](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/connect-destination.html). En el flujo de trabajo de configuración de destino, rellene los campos que aparecen en las dos secciones siguientes.

### Autenticar en destino {#authenticate}

Para autenticarse en el destino, rellene los campos obligatorios y seleccione **[!UICONTROL Conectarse al destino]**.

* **[!UICONTROL Acceso a ID de clave]**: Una cadena alfanumérica de 61 caracteres que se usa para autenticar su [!DNL Google Cloud Storage] a Platform.
* **[!UICONTROL Clave de acceso secreta]**: Una cadena con codificación base64 de 40 caracteres que se utiliza para autenticar su [!DNL Google Cloud Storage] a Platform.

Para obtener más información sobre estos valores, consulte la [Claves HMAC de Google Cloud Storage](https://cloud.google.com/storage/docs/authentication/hmackeys#overview) guía. Para ver los pasos sobre cómo generar su propio ID de clave de acceso y clave de acceso secreta, consulte la [[!DNL Google Cloud Storage] información general de la fuente](/help/sources/connectors/cloud-storage/google-cloud-storage.md).

### Rellenar detalles de destino {#destination-details}

Para configurar los detalles del destino, rellene los campos opcionales y requeridos a continuación. Un asterisco junto a un campo en la interfaz de usuario indica que el campo es obligatorio.

* **[!UICONTROL Nombre]**: Rellene el nombre preferido para este destino.
* **[!UICONTROL Descripción]**: Opcional. Por ejemplo, puede mencionar para qué campaña utiliza este destino.
* **[!UICONTROL Ruta de carpeta]**: Introduzca la ruta a la carpeta de destino que alojará los archivos exportados.
* **[!UICONTROL Nombre del depósito]**: Introduzca el nombre del [!DNL Google Cloud Storage] contenedor que utilizará este destino.
* **[!UICONTROL ID de cuenta]**: Escriba la [!DNL Audience Link ID] de su [!DNL Google] cuenta. Este es un identificador específico asociado con su [!DNL Google Ad Manager] red (no su [!DNL Network code]). Puede encontrar esto en **[!UICONTROL Administración > Configuración global]** en el [!DNL Google Ad Manager] interfaz.
* **[!UICONTROL Tipo de cuenta]**: Seleccione una opción, según su [!DNL Google] cuenta:
   * Uso `AdX buyer` para [!DNL Google AdX]
   * Uso `DFP by Google` para [!DNL DoubleClick] para editores

### Habilitar alertas {#enable-alerts}

Puede activar las alertas para recibir notificaciones sobre el estado del flujo de datos a su destino. Seleccione una alerta de la lista para suscribirse y recibir notificaciones sobre el estado de su flujo de datos. Para obtener más información sobre las alertas, consulte la guía de [suscripción a alertas de destinos mediante la interfaz de usuario](../../ui/alerts.md).

Cuando haya terminado de proporcionar detalles para la conexión de destino, seleccione **[!UICONTROL Siguiente]**.

## Activar segmentos en este destino {#activate}

>[!IMPORTANT]
> 
>Para activar los datos, necesita la variable **[!UICONTROL Administrar destinos]**, **[!UICONTROL Activar destinos]**, **[!UICONTROL Ver perfiles]** y **[!UICONTROL Ver segmentos]** [permisos de control de acceso](/help/access-control/home.md#permissions). Lea el [información general sobre el control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Consulte [Activar datos de audiencia en destinos de exportación de perfiles en lote](../../ui/activate-batch-profile-destinations.md) para obtener instrucciones sobre la activación de segmentos de audiencia en este destino.

En el paso de asignación de identidad, puede ver las siguientes asignaciones rellenadas previamente:

| Asignación previamente rellenada | Descripción |
|---------|----------|
| `ECID` -> `ppid` | Esta es la única asignación previamente completada editable por el usuario. Puede seleccionar cualquiera de los atributos o áreas de nombres de identidad de Platform y asignarlos a `ppid`. |
| `metadata.segment.alias` -> `list_id` | Asigna nombres de segmento de Experience Platform a ID de segmento en la plataforma Google. |
| `iif(${segmentMembership.ups.seg_id.status}=="exited", "1","0")` -> `delete` | Indica a la plataforma de Google cuándo eliminar de los segmentos a los usuarios no cualificados. |

Estas asignaciones son necesarias para [!DNL Google Ad Manager 360] y son creados automáticamente por Adobe Experience Platform para todos [!DNL Google Ad Manager 360] conexiones.

![Imagen de la interfaz de usuario que muestra el paso de asignación para Google Ad Manager 360.](../../assets/catalog/advertising/google-ad-manager-360/ad-manager-360-mapping.png)

## Datos exportados {#exported-data}

Para comprobar si los datos se han exportado correctamente, consulte [!DNL Google Cloud Storage] y asegúrese de que los archivos exportados contienen las poblaciones de perfiles esperadas.

## Resolución de problemas {#troubleshooting}

En caso de que encuentre algún error al utilizar este destino y necesite ponerse en contacto con Adobe o Google, mantenga los siguientes ID a mano.

Estos son los ID de cuenta de Google de Adobe:

* **[!UICONTROL ID de cuenta]**: 87933855
* **[!UICONTROL ID de cliente]**: 89690775