---
title: (Beta) [!DNL Google Ad Manager 360] conexión
description: Google Ad Manager 360 es una plataforma de servicio de anuncios de Google que ofrece a los editores los medios para administrar la visualización de anuncios en sus sitios web, a través de vídeo y en aplicaciones móviles.
exl-id: 3251145a-3e4d-40aa-b120-d79c8c9c7cae
source-git-commit: d5a22d4692226c865f6489c821366b4ce8bc2887
workflow-type: tm+mt
source-wordcount: '1211'
ht-degree: 4%

---

# (Beta) [!DNL Google Ad Manager 360] conexión

>[!IMPORTANT]
>
> Google está publicando cambios en la [API de Google Ads](https://developers.google.com/google-ads/api/docs/start), [Coincidencia de clientes](https://ads-developers.googleblog.com/2023/10/updates-to-customer-match-conversion.html), y el [API de Display &amp; Video 360](https://developers.google.com/display-video/api/guides/getting-started/overview) con el fin de respaldar los requisitos de conformidad y relacionados con el consentimiento definidos en el [Digital Markets Act](https://digital-markets-act.ec.europa.eu/index_en) (DMA) en la Unión Europea ([Política de consentimiento del usuario de UE](https://www.google.com/about/company/user-consent-policy/)). Se espera que la aplicación de estos cambios en los requisitos de consentimiento entre en vigor a partir del 6 de marzo de 2024.
><br/><br/>
>Para adherirse a la política de consentimiento de usuario de la UE y seguir creando listas de audiencia para usuarios en el Espacio Económico Europeo (EEE), los anunciantes y socios deben asegurarse de que están pasando el consentimiento del usuario final al cargar datos de audiencia. Como socio de Google, Adobe le proporciona las herramientas necesarias para cumplir con estos requisitos de consentimiento según DMA en la Unión Europea.
><br/><br/>
>Clientes que han adquirido Adobe Privacy &amp; Security Shield y que han configurado un [política de consentimiento](../../../data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation) para filtrar los perfiles no consentidos, no es necesario realizar ninguna acción.
><br/><br/>
>Los clientes que no hayan adquirido Adobe Privacy &amp; Security Shield deben utilizar [definición del segmento](../../../segmentation/home.md#segment-definitions) funciones dentro de [Generador de segmentos](../../../segmentation/ui/segment-builder.md) para filtrar los perfiles no consentidos con el fin de seguir utilizando los destinos de Google de Real-Time CDP existentes sin interrupción.

El [!DNL Google Ad Manager 360] la conexión habilita la carga por lotes para [!DNL publisher provided identifiers] (PPID) en [!DNL Google Ad Manager 360], mediante [!DNL Google Cloud Storage].

Para obtener más información sobre cómo funcionan los identificadores proporcionados por el editor en Google Ad Manager 360, consulte la [documentación oficial de Google](https://support.google.com/admanager/answer/2880055?hl=en).

>[!IMPORTANT]
>
>Este destino está actualmente en versión beta y solo está disponible para un número limitado de clientes. Para solicitar acceso a [!DNL Google Ad Manager 360] conexión, póngase en contacto con el representante del Adobe y proporcione a [!DNL organization ID].

El [!DNL Google Ad Manager 360] exportaciones de destino [!DNL CSV] archivos a su [!DNL Google Cloud Storage] cubo. Una vez que haya exportado el [!DNL CSV] archivos, debe importarlos en su [!DNL Google Ad Manager 360] cuenta.

## Detalles del destino {#specifics}

Tenga en cuenta los siguientes detalles específicos de [!DNL Google Ad Manager 360] destinos.

* Las audiencias activadas se crean mediante programación en la plataforma de Google y se rellenan en el archivo CSV.

## Identidades admitidas {#supported-identities}

[!DNL This integration] admite la activación de identidades descritas en la tabla siguiente.

| Identidad de destino | Descripción | Consideraciones |
|---|---|---|
| PPID | [!DNL Publisher provided ID] | Seleccione esta identidad de destino a la que enviar audiencias [!DNL Google Ad Manager 360] |

{style="table-layout:auto"}

## Audiencias compatibles {#supported-audiences}

Esta sección describe qué tipos de audiencias puede exportar a este destino.

| Origen de audiencia | Admitido | Descripción |
---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Audiencias generadas mediante el Experience Platform [Servicio de segmentación](../../../segmentation/home.md). |
| Cargas personalizadas | ✓ | Audiencias [importado](../../../segmentation/ui/overview.md#import-audience) en el Experience Platform desde archivos CSV. |

{style="table-layout:auto"}

## Tipo y frecuencia de exportación {#export-type-frequency}

Consulte la tabla siguiente para obtener información sobre el tipo y la frecuencia de exportación de destino.

| Elemento | Tipo | Notas |
---------|----------|---------|
| Tipo de exportación | **[!UICONTROL Basado en perfiles]** | Está exportando todos los miembros de un segmento, junto con los campos de esquema aplicables (por ejemplo, su PPID), tal como se elige en la pantalla Seleccionar atributos de perfil del [flujo de trabajo de activación de destino](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes). |
| Frecuencia de exportación | **[!UICONTROL Lote]** | Los destinos por lotes exportan archivos a plataformas descendentes en incrementos de tres, seis, ocho, doce o veinticuatro horas. Más información sobre [destinos basados en archivos por lotes](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## Requisitos previos {#prerequisites}

### Lista de permitidos {#allow-listing}

La inclusión en la lista de permitidos es obligatoria antes de configurar la primera [!DNL Google Ad Manager 360] en Platform. Asegúrese de completar el proceso de inclusión en la lista de permitidos que se describe a continuación antes de crear su destino.

>[!NOTE]
>
>La excepción a esta regla es para [Audience Manager](https://docs.adobe.com/content/help/es-ES/experience-cloud/user-guides/home.translate.html) clientes. Si ya ha creado una conexión con este destino de Google en Audience Manager, no es necesario volver a pasar por el proceso de inclusión en la lista de permitidos y puede continuar con los siguientes pasos.

1. Siga los pasos descritos en la sección [Documentación de Google Ad Manager](https://support.google.com/admanager/answer/3289669?hl=en) para agregar Adobe como plataforma de administración de datos (DMP) vinculada.
2. En el [!DNL Google Ad Manager] interfaz, vaya a **[!UICONTROL Administrador]** > **[!UICONTROL Configuración global]** > **[!UICONTROL Configuración de red]** y habilite la opción **[!UICONTROL Acceso a API]** deslizador.


## Conexión al destino {#connect}

>[!IMPORTANT]
> 
>Para conectarse al destino, necesita el **[!UICONTROL Ver destinos]** y **[!UICONTROL Administrar destinos]** [permisos de control de acceso](/help/access-control/home.md#permissions). Lea el [información general de control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Para conectarse a este destino, siga los pasos descritos en la sección [tutorial de configuración de destino](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/connect-destination.html). En el flujo de trabajo de configuración de destino, rellene los campos enumerados en las dos secciones siguientes.

### Autenticarse en el destino {#authenticate}

Para autenticarse en el destino, rellene los campos obligatorios y seleccione **[!UICONTROL Conectar con destino]**.

* **[!UICONTROL ID de clave de acceso]**: una cadena alfanumérica de 61 caracteres que se utiliza para autenticar su [!DNL Google Cloud Storage] a Platform.
* **[!UICONTROL Clave de acceso secreta]**: una cadena de 40 caracteres codificada en Base64 que se utiliza para autenticar su [!DNL Google Cloud Storage] a Platform.

Para obtener más información sobre estos valores, consulte la [Claves HMAC de Google Cloud Storage](https://cloud.google.com/storage/docs/authentication/hmackeys#overview) guía. Para obtener información sobre cómo generar su propio ID de clave de acceso y clave de acceso secreta, consulte la [[!DNL Google Cloud Storage] descripción general de origen](/help/sources/connectors/cloud-storage/google-cloud-storage.md).

### Rellenar detalles de destino {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_gam360_appendSegmentID"
>title="Anexar el ID de público al nombre de público"
>abstract="Seleccione esta opción para que el nombre de público en Google Ad Manager 360 incluya el ID de público de Experience Platform, de esta manera: `Audience Name (Audience ID)`"

Para configurar los detalles del destino, rellene los campos obligatorios y opcionales a continuación. Un asterisco junto a un campo en la interfaz de usuario indica que el campo es obligatorio.

* **[!UICONTROL Nombre]**: complete el nombre preferido para este destino.
* **[!UICONTROL Descripción]**: Opcional. Por ejemplo, puede mencionar para qué campaña está usando este destino.
* **[!UICONTROL Ruta de carpeta]**: introduzca la ruta a la carpeta de destino que alojará los archivos exportados.
* **[!UICONTROL Nombre del cubo]**: introduzca el nombre del [!DNL Google Cloud Storage] contenedor que utilizará este destino.
* **[!UICONTROL ID de cuenta]**: introduzca su [!DNL Audience Link ID] de su [!DNL Google] cuenta. Se trata de un identificador específico asociado con su [!DNL Google Ad Manager] red (no su [!DNL Network code]). Puede encontrar esto en **[!UICONTROL Administración > Configuración global]** en el [!DNL Google Ad Manager] interfaz.
* **[!UICONTROL Tipo de cuenta]**: Seleccione una opción, según sus [!DNL Google] cuenta:
   * Uso `AdX buyer` para [!DNL Google AdX]
   * Uso `DFP by Google` para [!DNL DoubleClick] para editores
* **[!UICONTROL Anexar ID de audiencia al nombre de audiencia]**: seleccione esta opción para que el nombre de audiencia en Google Ad Manager 360 incluya el ID de audiencia de Experience Platform, de esta manera: `Audience Name (Audience ID)`.

### Habilitar alertas {#enable-alerts}

Puede activar alertas para recibir notificaciones sobre el estado del flujo de datos a su destino. Seleccione una alerta de la lista a la que suscribirse para recibir notificaciones sobre el estado del flujo de datos. Para obtener más información sobre las alertas, consulte la guía de [suscripción a alertas de destinos mediante la IU](../../ui/alerts.md).

Cuando haya terminado de proporcionar detalles para la conexión de destino, seleccione **[!UICONTROL Siguiente]**.

## Activar públicos en este destino {#activate}

>[!IMPORTANT]
> 
>* Para activar los datos, necesita el **[!UICONTROL Ver destinos]**, **[!UICONTROL Activar destinos]**, **[!UICONTROL Ver perfiles]**, y **[!UICONTROL Ver segmentos]** [permisos de control de acceso](/help/access-control/home.md#permissions). Lea el [información general de control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.
>* Para exportar *identidades*, necesita el **[!UICONTROL Ver gráfico de identidad]** [permiso de control de acceso](/help/access-control/home.md#permissions). <br> ![Seleccione el área de nombres de identidad resaltada en el flujo de trabajo para activar audiencias en los destinos.](/help/destinations/assets/overview/export-identities-to-destination.png "Seleccione el área de nombres de identidad resaltada en el flujo de trabajo para activar audiencias en los destinos."){width="100" zoomable="yes"}

Consulte [Activar datos de audiencia en destinos de exportación de perfiles por lotes](../../ui/activate-batch-profile-destinations.md) para obtener instrucciones sobre cómo activar audiencias en este destino.

En el paso de asignación de identidad, puede ver las siguientes asignaciones rellenadas previamente:

| Asignación rellenada previamente | Descripción |
|---------|----------|
| `ECID` -> `ppid` | Esta es la única asignación rellenada previamente que puede editar el usuario. Puede seleccionar cualquiera de sus atributos o áreas de nombres de identidad de Platform y asignarlos a `ppid`. |
| `metadata.segment.alias` -> `list_id` | Asigna nombres de audiencia de Experience Platform a ID de audiencia en la plataforma de Google. |
| `iif(${segmentMembership.ups.seg_id.status}=="exited", "1","0")` -> `delete` | Indica a la plataforma Google cuándo quitar usuarios no cualificados de los segmentos. |

Estas asignaciones son necesarias para [!DNL Google Ad Manager 360] y los crea automáticamente Adobe Experience Platform para todos [!DNL Google Ad Manager 360] conexiones.

![Imagen de la IU que muestra el paso de asignación de Google Ad Manager 360.](../../assets/catalog/advertising/google-ad-manager-360/ad-manager-360-mapping.png)

## Datos exportados {#exported-data}

Para comprobar si los datos se han exportado correctamente, compruebe su [!DNL Google Cloud Storage] y asegúrese de que los archivos exportados contienen las poblaciones de perfiles esperadas.

## Resolución de problemas {#troubleshooting}

Si encuentra algún error al utilizar este destino y necesita ponerse en contacto con Adobe o Google, mantenga los siguientes ID a mano.

Estos son los ID de cuenta de Google de Adobe:

* **[!UICONTROL ID de cuenta]**: 87933855
* **[!UICONTROL ID de cliente]**: 89690775