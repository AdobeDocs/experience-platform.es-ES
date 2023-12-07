---
title: Destino del Marketo Engage
description: Marketo Engage es la única solución integral de administración de la experiencia del cliente (CXM) para marketing, publicidad, análisis y comercio. Le permite automatizar y administrar las actividades desde la administración de clientes potenciales y la participación de los clientes hasta el marketing basado en cuentas y la atribución de ingresos.
exl-id: 5ae5f114-47ba-4ff6-8e42-f8f43eb079f7
source-git-commit: 34ae6f0f791a40584c2d476ed715bb7c5b733c42
workflow-type: tm+mt
source-wordcount: '882'
ht-degree: 1%

---

# destino del Marketo Engage {#beta-marketo-engage-destination}

## Registro de cambios de destino {#changelog}

>[!IMPORTANT]
>
>Con el lanzamiento de [conector de destino mejorado de Marketo V2](/help/release-notes/2022/july-2022.md#destinations), ahora verá dos tarjetas de Marketo en el catálogo de destinos.
>* Si ya está activando datos en el **[!UICONTROL Marketo V1]** destino: cree nuevos flujos de datos para el **[!UICONTROL Marketo V2]** destino y eliminación de flujos de datos existentes en **[!UICONTROL Marketo V1]** destino para febrero de 2023. A partir de esa fecha, la variable **[!UICONTROL Marketo V1]** se eliminará la tarjeta de destino.
>* Si todavía no ha creado ningún flujo de datos en **[!UICONTROL Marketo V1]** destino, utilice el nuevo **[!UICONTROL Marketo V2]** para conectarse y exportar datos a Marketo.

![Imagen de las dos tarjetas de destino de Marketo en una vista en paralelo.](../..//assets/catalog/adobe/marketo-side-by-side-view.png)

Las mejoras en el destino de Marketo V2 incluyen las siguientes:

* En el **[!UICONTROL Programar segmento]** paso del flujo de trabajo de activación, en Marketo V1, debía añadir manualmente una **ID de asignación** para exportar correctamente datos a Marketo. Este paso manual ya no es necesario en Marketo V2.
* En el **[!UICONTROL Asignación]** En este paso del flujo de trabajo de activación, en Marketo V1, se podían asignar campos XDM a solo tres campos de destino en Marketo: `firstName`, `lastName`, y `companyName`. Con la versión 2.0 de Marketo, ahora puede asignar campos XDM a muchos más campos en Marketo. Para obtener más información, lea la [atributos admitidos](#supported-attributes) más abajo.

## Información general {#overview}

[!DNL Marketo Engage] es la única solución de administración de la experiencia del cliente (CXM) de extremo a extremo para marketing, publicidad, análisis y comercio. Le permite automatizar y administrar las actividades desde la administración de clientes potenciales y la participación de los clientes hasta el marketing basado en cuentas y la atribución de ingresos.

El destino permite a los especialistas en marketing insertar audiencias creadas en Adobe Experience Platform en Marketo, donde aparecerán como listas estáticas.

## Identidades y atributos admitidos {#supported-identities-attributes}

>[!NOTE]
>
>En el [paso de asignación](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping) del flujo de trabajo activar destino, es *obligatorio* para asignar identidades y *opcional* para asignar atributos. Asignar un correo electrónico o ECID desde la pestaña Área de nombres de identidad es lo más importante para garantizar que la persona coincida en Marketo. Asignar correo electrónico garantiza la tasa de coincidencia más alta.

### Identidades admitidas {#supported-identities}

| Identidad de destino | Descripción |
|---|---|
| ECID | Un área de nombres que representa ECID. Este área de nombres también se puede mencionar mediante los siguientes alias: &quot;Adobe Marketing Cloud ID&quot;, &quot;Adobe Experience Cloud ID&quot;, &quot;Adobe Experience Platform ID&quot;. Consulte el siguiente documento sobre [ECID](/help/identity-service/ecid.md) para obtener más información. |
| Correo electrónico | Un área de nombres que representa una dirección de correo electrónico. Este tipo de área de nombres suele estar asociado a una sola persona y, por lo tanto, se puede utilizar para identificarla en diferentes canales. |

{style="table-layout:auto"}

### Atributos admitidos {#supported-attributes}

Puede asignar atributos de Experience Platform a cualquiera de los atributos a los que su organización tiene acceso en Marketo. En Marketo, puede utilizar el complemento [Describir solicitud de API](https://developers.marketo.com/rest-api/lead-database/leads/#describe) para recuperar los campos de atributos a los que su organización tiene acceso.

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
| Tipo de exportación | **[!UICONTROL Exportación de audiencia]** | Va a exportar todos los miembros de una audiencia con los identificadores (correo electrónico, ECID) utilizados en [!DNL Marketo Engage] destino. |
| Frecuencia de exportación | **[!UICONTROL Transmisión]** | Los destinos de streaming son conexiones basadas en API &quot;siempre activadas&quot;. Tan pronto como se actualiza un perfil en Experience Platform según la evaluación de audiencias, el conector envía la actualización de forma descendente a la plataforma de destino. Más información sobre [destinos de streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Configuración del destino y activación de audiencias {#set-up}

>[!IMPORTANT]
> 
>* Para conectarse al destino, necesita el **[!UICONTROL Administrar destinos]** [permiso de control de acceso](/help/access-control/home.md#permissions).
>* Para activar los datos, necesita el **[!UICONTROL Administrar destinos]**, **[!UICONTROL Activar destinos]**, **[!UICONTROL Ver perfiles]**, y **[!UICONTROL Ver segmentos]** [permisos de control de acceso](/help/access-control/home.md#permissions). Lea el [información general de control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Para obtener instrucciones detalladas sobre cómo configurar el destino y activar audiencias, lea [Insertar una audiencia de Adobe Experience Platform en una lista estática de Marketo](https://experienceleague.adobe.com/docs/marketo/using/product-docs/core-marketo-concepts/smart-lists-and-static-lists/static-lists/push-an-adobe-experience-cloud-segment-to-a-marketo-static-list.html) en la documentación de Marketo.

El siguiente vídeo también muestra los pasos para configurar un destino de Marketo y activar audiencias.

>[!IMPORTANT]
>
>El vídeo no refleja completamente la capacidad actual. Para obtener la información más actualizada, consulte la guía vinculada anteriormente. Las siguientes partes del vídeo están obsoletas:
> 
>* La tarjeta de destino que debe utilizar en la interfaz de usuario de Experience Platform es **[!UICONTROL Marketo V2]**.
>* El vídeo no muestra el nuevo **[!UICONTROL Creación de personas]** en el flujo de trabajo conectar con destino.
>* Las dos limitaciones indicadas en el vídeo ya no se aplican. Ahora puede asignar muchos otros campos de atributos de perfil además de la información de pertenencia a audiencias compatible en el momento de grabar el vídeo. También puede exportar a Marketo miembros de la audiencia que aún no existan en sus listas estáticas de Marketo y que se añadirán a las listas.
>* En el **[!UICONTROL Paso Programar audiencia]** del flujo de trabajo de activación, en Marketo V1, debía añadir manualmente una **[!UICONTROL ID de asignación]** para exportar correctamente datos a Marketo. Este paso manual ya no es necesario en Marketo V2.

>[!VIDEO](https://video.tv.adobe.com/v/338248?quality=12)

<!--

## Connect to the destination {#connect}

To connect to this destination, follow the steps described in the [destination configuration tutorial](../../ui/connect-destination.md).

-->

## Uso de datos y gobernanza {#data-usage-governance}

Todo [!DNL Adobe Experience Platform] Los destinos de cumplen con las políticas de uso de datos al gestionar los datos. Para obtener información detallada sobre cómo [!DNL Adobe Experience Platform] aplica la gobernanza de datos. Consulte la [información general sobre gobernanza de datos](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html?lang=es).

<!--

## Activate audiences to this destination {#activate}

See [Activate audience data to streaming audience export destinations](../../ui/activate-segment-streaming-destinations.md) for instructions on activating audiences to this destination.

-->
