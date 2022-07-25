---
title: (Beta) [!DNL Google Ad Manager 360] connection
description: Google Ad Manager 360 es una plataforma de servicio de publicidad de Google que proporciona a los editores los medios para administrar la visualización de anuncios en sus sitios web, a través de vídeo y en aplicaciones móviles.
exl-id: 3251145a-3e4d-40aa-b120-d79c8c9c7cae
source-git-commit: aed15e0abfd51a8a08290e78302239792f86535a
workflow-type: tm+mt
source-wordcount: '931'
ht-degree: 1%

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

>[!NOTE]
>
>La lista de permitidos es obligatoria antes de configurar la primera [!DNL Google Ad Manager] destino en Platform. Asegúrese de que el proceso de lista de permitidos que se describe a continuación se haya completado en [!DNL Google] antes de crear un destino.

>[!IMPORTANT]
>
>Google ha simplificado el proceso para conectar plataformas de gestión de público externas a Google Ad Manager 360. Ahora puede pasar por el proceso para vincular a Google Ad Manager 360 de forma autoservicio. Lectura [Segmentos de plataformas de administración de datos](https://support.google.com/admanager/answer/3289669?hl=en) en la documentación de Google. Debe tener a mano los ID que se enumeran a continuación.

* **ID de cuenta**: ID de cuenta de Adobe con Google. ID de cuenta: 87933855.
* **ID de cliente**: ID de cuenta de cliente de Adobe con Google. ID de cliente: 89690775.
* **Código de red**: Esta es su [!DNL Google Ad Manager] identificador de red, encontrado en **[!UICONTROL Administración > Configuración global]** en la interfaz de Google, así como en la URL.
* **ID del vínculo de audiencia**: Este es un identificador específico asociado con su [!DNL Google Ad Manager] red (no su [!DNL Network code]), también se encuentra en **[!UICONTROL Administración > Configuración global]** en la interfaz de Google.
* El tipo de cuenta. DFP de Google o del comprador de AdX.

## Conectarse al destino {#connect}

>[!IMPORTANT]
> 
>Para conectarse al destino, necesita la variable **[!UICONTROL Administrar destinos]** [permiso de control de acceso](/help/access-control/home.md#permissions). Lea el [información general sobre el control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Para conectarse a este destino, siga los pasos descritos en la sección [tutorial de configuración de destino](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/connect-destination.html). En el flujo de trabajo de configuración de destino, rellene los campos que aparecen en las dos secciones siguientes.

### Autenticar en destino {#authenticate}

Para autenticarse en el destino, rellene los campos obligatorios y seleccione **[!UICONTROL Conectarse al destino]**.

* **[!UICONTROL Acceso a ID de clave]**: Una cadena alfanumérica de 61 caracteres que se usa para autenticar su [!DNL Google Cloud Storage] a Platform.
* **[!UICONTROL Clave de acceso secreta]**: Una cadena de 40 caracteres codificada en base a 64 que se usa para autenticar su [!DNL Google Cloud Storage] a Platform.

Para obtener más información sobre estos valores, consulte la [Claves HMAC de Google Cloud Storage](https://cloud.google.com/storage/docs/authentication/hmackeys#overview) guía. Para ver los pasos sobre cómo generar su propio ID de clave de acceso y clave de acceso secreta, consulte la [[!DNL Google Cloud Storage] información general de la fuente](/help/sources/connectors/cloud-storage/google-cloud-storage.md).

### Rellenar detalles de destino {#destination-details}

Para configurar los detalles del destino, rellene los campos opcionales y requeridos a continuación. Un asterisco junto a un campo en la interfaz de usuario indica que el campo es obligatorio.

* **[!UICONTROL Nombre]**: Rellene el nombre preferido para este destino.
* **[!UICONTROL Descripción]**: Opcional. Por ejemplo, puede mencionar para qué campaña utiliza este destino.
* **[!UICONTROL Nombre del depósito]**: Introduzca el nombre del [!DNL Google Cloud Storage] contenedor que utilizará este destino.
* **[!UICONTROL Ruta de carpeta]**: Introduzca la ruta a la carpeta de destino que alojará los archivos exportados.
* **[!UICONTROL ID de cuenta]**: Rellene el ID de cuenta con [!DNL Google]. Puede ser su código de red o su ID de vínculo de audiencia. Normalmente, se trata de un ID de ocho dígitos.
* **[!UICONTROL Tipo de cuenta]**: Seleccione una opción, en función de su cuenta con Google:
   * Uso `DFP by Google` para [!DNL DoubleClick] para editores
   * Uso `AdX buyer` para [!DNL Google AdX]

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
