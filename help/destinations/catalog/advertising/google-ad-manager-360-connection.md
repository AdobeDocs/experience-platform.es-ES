---
title: (Beta) [!DNL Google Ad Manager 360] conexión
description: Google Ad Manager 360 es una plataforma de servicio de anuncios de Google que ofrece a los editores los medios para administrar la visualización de anuncios en sus sitios web, a través de vídeo y en aplicaciones móviles.
exl-id: 3251145a-3e4d-40aa-b120-d79c8c9c7cae
source-git-commit: 21b76877e8b36d6b844d9c0726a2347b1fab170e
workflow-type: tm+mt
source-wordcount: '1217'
ht-degree: 6%

---

# Conexión de (Beta) [!DNL Google Ad Manager 360]

>[!IMPORTANT]
>
> Google está publicando cambios en la [API de Google Ads](https://developers.google.com/google-ads/api/docs/start), [Customer Match](https://ads-developers.googleblog.com/2023/10/updates-to-customer-match-conversion.html) y la [API de Display &amp; Video 360](https://developers.google.com/display-video/api/guides/getting-started/overview) para admitir los requisitos relacionados con el cumplimiento y el consentimiento definidos en la [Ley de Mercados Digitales](https://digital-markets-act.ec.europa.eu/index_es) (DMA) de la Unión Europea ([Política de consentimiento del Usuario de la UE](https://www.google.com/about/company/user-consent-policy/)). La aplicación de estos cambios en los requisitos de consentimiento está activa desde el 6 de marzo de 2024.
><br/>
>Para adherirse a la política de consentimiento de usuario de la UE y seguir creando listas de audiencia para usuarios en el Espacio Económico Europeo (EEE), los anunciantes y socios deben asegurarse de que están pasando el consentimiento del usuario final al cargar datos de audiencia. Como socio de Google, Adobe le proporciona las herramientas necesarias para cumplir con estos requisitos de consentimiento según la DMA en la Unión Europea.
><br/>
>Los clientes que hayan adquirido Adobe Privacy &amp; Security Shield y hayan configurado una [política de consentimiento](../../../data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation) para filtrar los perfiles no consentidos no tienen que realizar ninguna acción.
><br/>
>Los clientes que no hayan adquirido Adobe Privacy &amp; Security Shield deben utilizar las funciones de [definición de segmento](../../../segmentation/home.md#segment-definitions) de [Generador de segmentos](../../../segmentation/ui/segment-builder.md) para filtrar los perfiles no consentidos y así poder seguir utilizando los destinos de Real-Time CDP Google existentes sin interrupción.

La conexión [!DNL Google Ad Manager 360] habilita la carga por lotes de [!DNL publisher provided identifiers] (PPID) en [!DNL Google Ad Manager 360], a través de [!DNL Google Cloud Storage].

Para obtener más información sobre cómo funcionan los identificadores proporcionados por el editor en Google Ad Manager 360, consulte la [documentación oficial de Google](https://support.google.com/admanager/answer/2880055?hl=en).

>[!IMPORTANT]
>
>Actualmente, este destino está en Beta y solo está disponible para un número limitado de clientes. Para solicitar acceso a la conexión de [!DNL Google Ad Manager 360], póngase en contacto con el representante del Adobe y proporcione su [!DNL organization ID].

El destino [!DNL Google Ad Manager 360] exporta [!DNL CSV] archivos a su bloque [!DNL Google Cloud Storage]. Una vez exportados los archivos de [!DNL CSV], debe importarlos a su cuenta de [!DNL Google Ad Manager 360].

## Detalles del destino {#specifics}

Tenga en cuenta los siguientes detalles que son específicos de [!DNL Google Ad Manager 360] destinos.

* Actualmente, este destino no admite la característica [exportar archivos bajo demanda](../../ui/export-file-now.md).
* Las audiencias activadas se crean mediante programación en la plataforma de Google y se rellenan en el archivo CSV.

## Identidades admitidas {#supported-identities}

[!DNL This integration] admite la activación de las identidades descritas en la tabla siguiente.

| Identidad de destino | Descripción | Consideraciones |
|---|---|---|
| PPID | [!DNL Publisher provided ID] | Seleccione esta identidad de destino para enviar audiencias a [!DNL Google Ad Manager 360] |

{style="table-layout:auto"}

## Audiencias compatibles {#supported-audiences}

Esta sección describe qué tipos de audiencias puede exportar a este destino.

| Origen de audiencia | Admitido | Descripción |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Audiencias generadas a través del Experience Platform [Servicio de segmentación](../../../segmentation/home.md). |
| Cargas personalizadas | ✓ | Las audiencias [importadas](../../../segmentation/ui/audience-portal.md#import-audience) en el Experience Platform desde archivos CSV. |

{style="table-layout:auto"}

## Tipo y frecuencia de exportación {#export-type-frequency}

Consulte la tabla siguiente para obtener información sobre el tipo y la frecuencia de exportación de destino.

| Elemento | Tipo | Notas |
---------|----------|---------|
| Tipo de exportación | **[!UICONTROL Basado en perfil]** | Está exportando todos los miembros de un segmento, junto con los campos de esquema aplicables (por ejemplo, su PPID), tal como se eligió en la pantalla Seleccionar atributos de perfil del [flujo de trabajo de activación de destino](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes). |
| Frecuencia de exportación | **[!UICONTROL Lote]** | Los destinos por lotes exportan archivos a plataformas descendentes en incrementos de tres, seis, ocho, doce o veinticuatro horas. Obtenga más información sobre [destinos basados en archivos por lotes](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## Requisitos previos {#prerequisites}

### Lista de permitidos {#allow-listing}

La inclusión en la lista de permitidos es obligatoria antes de configurar su primer destino de [!DNL Google Ad Manager 360] en Platform. Asegúrese de completar el proceso de inclusión en la lista de permitidos que se describe a continuación antes de crear su destino.

>[!NOTE]
>
>La excepción a esta regla es para clientes existentes de [Audience Manager](https://docs.adobe.com/content/help/es-ES/experience-cloud/user-guides/home.translate.html). Si ya ha creado una conexión con este destino de Google en Audience Manager, no es necesario volver a pasar por el proceso de inclusión en la lista de permitidos y puede continuar con los siguientes pasos.

1. Siga los pasos descritos en la [documentación de Google Ad Manager](https://support.google.com/admanager/answer/3289669?hl=en) para agregar Adobe como plataforma de administración de datos vinculada (DMP).
2. En la interfaz de [!DNL Google Ad Manager], vaya a **[!UICONTROL Administración]** > **[!UICONTROL Configuración global]** > **[!UICONTROL Configuración de red]** y habilite el control deslizante **[!UICONTROL Acceso a la API]**.


## Conexión al destino {#connect}

>[!IMPORTANT]
> 
>Para conectarse al destino, necesita los **[!UICONTROL permisos de control de acceso](/help/access-control/home.md#permissions) de Ver destinos]** y **[!UICONTROL Administrar destinos]**[5}. Lea la [descripción general del control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Para conectarse a este destino, siga los pasos descritos en el [tutorial de configuración de destino](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/connect-destination.html). En el flujo de trabajo de configuración de destino, rellene los campos enumerados en las dos secciones siguientes.

### Autenticarse en el destino {#authenticate}

Para autenticarse en el destino, rellene los campos obligatorios y seleccione **[!UICONTROL Conectar con destino]**.

* **[!UICONTROL Id. de clave de acceso]**: cadena alfanumérica de 61 caracteres usada para autenticar su cuenta de [!DNL Google Cloud Storage] en Platform.
* **[!UICONTROL Clave de acceso secreta]**: cadena de 40 caracteres codificada en Base64 que se usa para autenticar la cuenta de [!DNL Google Cloud Storage] en Platform.

Para obtener más información sobre estos valores, consulte la guía [Claves HMAC de Google Cloud Storage](https://cloud.google.com/storage/docs/authentication/hmackeys#overview). Para ver los pasos sobre cómo generar tu propio identificador de clave de acceso y clave de acceso secreta, consulta la [[!DNL Google Cloud Storage] descripción general de origen](/help/sources/connectors/cloud-storage/google-cloud-storage.md).

### Rellenar detalles de destino {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_gam360_appendSegmentID"
>title="Anexar el ID de público al nombre de público"
>abstract="Seleccione esta opción para que el nombre de público en este destino incluya el ID de público de Experience Platform, de la manera siguiente: `Audience Name (Audience ID)`"

Para configurar los detalles del destino, rellene los campos obligatorios y opcionales a continuación. Un asterisco junto a un campo en la interfaz de usuario indica que el campo es obligatorio.

* **[!UICONTROL Nombre]**: rellene el nombre preferido para este destino.
* **[!UICONTROL Descripción]**: Opcional. Por ejemplo, puede mencionar para qué campaña está usando este destino.
* **[!UICONTROL Ruta de carpeta]**: escriba la ruta de acceso a la carpeta de destino que alojará los archivos exportados.
* **[!UICONTROL Nombre del contenedor]**: Escriba el nombre del contenedor [!DNL Google Cloud Storage] que usará este destino.
* **[!UICONTROL ID de cuenta]**: escribe tu [!DNL Audience Link ID] desde tu cuenta de [!DNL Google]. Este es un identificador específico asociado con su red [!DNL Google Ad Manager] (no con su [!DNL Network code]). Puede encontrar esto en **[!UICONTROL Administración > Configuración global]** en la interfaz de [!DNL Google Ad Manager].
* **[!UICONTROL Tipo de cuenta]**: selecciona una opción, según tu cuenta de [!DNL Google]:
   * Usar `AdX buyer` para [!DNL Google AdX]
   * Usar `DFP by Google` para [!DNL DoubleClick] para editores
* **[!UICONTROL Anexar ID de audiencia al nombre de audiencia]**: seleccione esta opción para que el nombre de audiencia en Google Ad Manager 360 incluya el ID de audiencia del Experience Platform, de esta manera: `Audience Name (Audience ID)`.

### Habilitar alertas {#enable-alerts}

Puede activar alertas para recibir notificaciones sobre el estado del flujo de datos a su destino. Seleccione una alerta de la lista a la que suscribirse para recibir notificaciones sobre el estado del flujo de datos. Para obtener más información sobre las alertas, consulte la guía sobre [suscripción a alertas de destinos mediante la interfaz de usuario](../../ui/alerts.md).

Cuando termine de proporcionar detalles para la conexión de destino, seleccione **[!UICONTROL Siguiente]**.

## Activar públicos en este destino {#activate}

>[!IMPORTANT]
> 
>* Para activar los datos, necesita los **[!UICONTROL permisos de control de acceso]**, **[!UICONTROL Activar destinos]**, **[!UICONTROL Ver perfiles]** y **[!UICONTROL Ver segmentos]**[para ](/help/access-control/home.md#permissions). Lea la [descripción general del control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.
>* Para exportar *identidades*, necesita el **[!UICONTROL permiso de control de acceso](/help/access-control/home.md#permissions) de]** Ver gráfico de identidad[. <br> ![Seleccione el área de nombres de identidad resaltada en el flujo de trabajo para activar audiencias en los destinos.](/help/destinations/assets/overview/export-identities-to-destination.png "Seleccione el área de nombres de identidad resaltada en el flujo de trabajo para activar audiencias en los destinos."){width="100" zoomable="yes"}

Consulte [Activar datos de audiencia en destinos de exportación de perfiles por lotes](../../ui/activate-batch-profile-destinations.md) para obtener instrucciones sobre cómo activar audiencias en este destino.

En el paso de asignación de identidad, puede ver las siguientes asignaciones rellenadas previamente:

| Asignación rellenada previamente | Descripción |
|---------|----------|
| `ECID` -> `ppid` | Esta es la única asignación rellenada previamente que puede editar el usuario. Puede seleccionar cualquiera de sus atributos o áreas de nombres de identidad de Platform y asignarlos a `ppid`. |
| `metadata.segment.alias` -> `list_id` | Asigna nombres de audiencia de Experience Platform a ID de audiencia en la plataforma de Google. |
| `iif(${segmentMembership.ups.seg_id.status}=="exited", "1","0")` -> `delete` | Indica a la plataforma Google cuándo quitar usuarios no cualificados de los segmentos. |

Estas asignaciones son requeridas por [!DNL Google Ad Manager 360] y Adobe Experience Platform las crea automáticamente para las [!DNL Google Ad Manager 360] conexiones.

![Imagen de la interfaz de usuario que muestra el paso de asignación de Google Ad Manager 360.](../../assets/catalog/advertising/google-ad-manager-360/ad-manager-360-mapping.png)

## Datos exportados {#exported-data}

Para comprobar si los datos se han exportado correctamente, compruebe el bloque [!DNL Google Cloud Storage] y asegúrese de que los archivos exportados contienen las poblaciones de perfiles esperadas.

## Resolución de problemas {#troubleshooting}

Si encuentra algún error al utilizar este destino y necesita ponerse en contacto con Adobe o Google, mantenga los siguientes ID a mano.

Estos son los ID de cuenta de Google de Adobe:

* **[!UICONTROL Id. de cuenta]**: 87933855
* **[!UICONTROL ID de cliente]**: 89690775