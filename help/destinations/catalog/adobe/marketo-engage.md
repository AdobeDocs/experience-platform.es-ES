---
title: Destino del Marketo Engage
description: Marketo Engage es la única solución integral de administración de experiencias del cliente (CXM) para marketing, publicidad, análisis y comercio. Permite automatizar y administrar actividades desde la administración de posibles clientes de CRM y la participación de los clientes hasta el marketing basado en cuentas y la atribución de ingresos.
exl-id: 5ae5f114-47ba-4ff6-8e42-f8f43eb079f7
source-git-commit: 9f305ee7824bd8790dec57ccbd2d9462ccfa8b49
workflow-type: tm+mt
source-wordcount: '870'
ht-degree: 2%

---

# destino del Marketo Engage {#beta-marketo-engage-destination}

## Registro de cambios del destino {#changelog}

>[!IMPORTANT]
>
>Con el lanzamiento del [conector de destino Marketo V2 mejorado](/help/release-notes/2022/july-2022.md#destinations), ahora verá dos tarjetas Marketo en el catálogo de destinos.
>* Si ya está activando datos en la variable **[!UICONTROL Marketo V1]** destino: Cree nuevos flujos de datos en la variable **[!UICONTROL Marketo V2]** destino y eliminación de flujos de datos existentes a **[!UICONTROL Marketo V1]** destino antes de febrero de 2023. A partir de esa fecha, la variable **[!UICONTROL Marketo V1]** se eliminará la tarjeta de destino.
>* Si aún no ha creado ningún flujo de datos en la variable **[!UICONTROL Marketo V1]** destino, utilice el nuevo **[!UICONTROL Marketo V2]** para conectarse a Marketo y exportar datos a.


![Imagen de las dos tarjetas de destino de Marketo en una vista en paralelo.](/help/destinations/assets/catalog/adobe/marketo-side-by-side-view.png)

Las mejoras en el destino de Marketo V2 incluyen:

* En el **[!UICONTROL Programar segmento]** paso del flujo de trabajo de activación, en Marketo V1, debe añadir manualmente un **ID de asignación** para exportar datos correctamente a Marketo. Este paso manual ya no es necesario en Marketo V2.
* En el **[!UICONTROL Asignación]** del flujo de trabajo de activación, en Marketo V1, solo se han podido asignar campos XDM a tres campos de destino en Marketo: `firstName`, `lastName`y `companyName`. Con la versión Marketo V2, ahora puede asignar campos XDM a muchos más campos en Marketo. Para obtener más información, lea la [atributos admitidos](#supported-attributes) más abajo.

## Información general {#overview}

[!DNL Marketo Engage] es la única solución integral de administración de experiencias del cliente (CXM) para marketing, publicidad, análisis y comercio. Permite automatizar y administrar actividades desde la administración de posibles clientes de CRM y la participación de los clientes hasta el marketing basado en cuentas y la atribución de ingresos.

El destino permite a los especialistas en marketing insertar los segmentos creados en Adobe Experience Platform en Marketo, donde aparecerán como listas estáticas.

## Identidades y atributos admitidos {#supported-identities-attributes}

>[!NOTE]
>
>En el [paso de asignación](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping) del flujo de trabajo de activación de destino, es *mandatory* para asignar identidades y *opcional* para asignar atributos. La asignación de correo electrónico o ECID desde la pestaña Área de nombres de identidad es lo más importante para garantizar que la persona coincida en Marketo. Asignación de correo electrónico garantiza la tasa de coincidencia más alta.

### Identidades compatibles {#supported-identities}

| Identidad de Target | Descripción |
|---|---|
| ECID | Un espacio de nombres que representa ECID. Este espacio de nombres también puede ser referenciado por los siguientes alias: &quot;Adobe Marketing Cloud ID&quot;, &quot;Adobe Experience Cloud ID&quot;, &quot;Adobe Experience Platform ID&quot;. Consulte el siguiente documento sobre [ECID](/help/identity-service/ecid.md) para obtener más información. |
| Correo electrónico | Área de nombres que representa una dirección de correo electrónico. Este tipo de área de nombres suele estar asociado a una sola persona y, por lo tanto, se puede utilizar para identificar a esa persona en diferentes canales. |

{style=&quot;table-layout:auto&quot;}

### Atributos admitidos {#supported-attributes}

Puede asignar atributos de Experience Platform a cualquiera de los atributos a los que tiene acceso su organización en Marketo. En Marketo, puede usar la variable [Describir solicitud de API](https://developers.marketo.com/rest-api/lead-database/leads/#describe) para recuperar los campos de atributo a los que su organización tiene acceso.

## Tipo de exportación y frecuencia {#export-type-frequency}

Consulte la tabla siguiente para obtener información sobre el tipo y la frecuencia de exportación de destino.

| Elemento | Tipo | Notas |
---------|----------|---------|
| Tipo de exportación | **[!UICONTROL Exportación de segmentos]** | Está exportando todos los miembros de un segmento (audiencia) con los identificadores (correo electrónico, ECID) utilizados en la variable [!DNL Marketo Engage] destino. |
| Frecuencia de exportación | **[!UICONTROL Transmisión]** | Los destinos de flujo continuo son conexiones basadas en API &quot;siempre activadas&quot;. Tan pronto como un perfil se actualiza en el Experience Platform en función de la evaluación de segmentos, el conector envía la actualización descendente a la plataforma de destino. Más información sobre [destinos de flujo continuo](/help/destinations/destination-types.md#streaming-destinations). |

{style=&quot;table-layout:auto&quot;}

## Configuración del destino y activación de segmentos {#set-up}

>[!IMPORTANT]
> 
>* Para conectarse al destino, necesita la variable **[!UICONTROL Administrar destinos]** [permiso de control de acceso](/help/access-control/home.md#permissions).
>* Para activar los datos, necesita la variable **[!UICONTROL Administrar destinos]**, **[!UICONTROL Activar destinos]**, **[!UICONTROL Ver perfiles]** y **[!UICONTROL Ver segmentos]** [permisos de control de acceso](/help/access-control/home.md#permissions). Lea el [información general sobre el control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.


Para obtener instrucciones detalladas sobre cómo configurar el destino y activar segmentos, lea [Insertar un segmento de Adobe Experience Platform en una lista estática de Marketo](https://experienceleague.adobe.com/docs/marketo/using/product-docs/core-marketo-concepts/smart-lists-and-static-lists/static-lists/push-an-adobe-experience-cloud-segment-to-a-marketo-static-list.html?lang=en) en la documentación de Marketo.

El siguiente vídeo también muestra los pasos para configurar un destino de Marketo y activar segmentos.

>[!IMPORTANT]
>
>El vídeo no refleja completamente la capacidad actual. Para obtener la información más actualizada, consulte la guía que aparece más arriba. Las siguientes partes del vídeo están obsoletas:
> 
>* La tarjeta de destino que debe usar en la interfaz de usuario del Experience Platform es **[!UICONTROL Marketo V2]**.
>* El vídeo no muestra el nuevo **[!UICONTROL Creación de personas]** en el flujo de trabajo connect to destination .
>* Las dos limitaciones indicadas en el vídeo ya no se aplican. Ahora puede asignar muchos otros campos de atributos de perfil además de la información de pertenencia a segmentos que se admitía en el momento en que se grabó el vídeo. También puede exportar miembros del segmento a Marketo que aún no existan en sus listas estáticas de Marketo y que se añadirán a las listas.
>* En el **[!UICONTROL Programar paso del segmento]** del flujo de trabajo de activación, en Marketo V1, era necesario añadir manualmente un **[!UICONTROL ID de asignación]** para exportar datos correctamente a Marketo. Este paso manual ya no es necesario en Marketo V2.


>[!VIDEO](https://video.tv.adobe.com/v/338248?quality=12)

<!--

## Connect to the destination {#connect}

To connect to this destination, follow the steps described in the [destination configuration tutorial](../../ui/connect-destination.md).

-->

## Uso y gobernanza de los datos {#data-usage-governance}

Todo [!DNL Adobe Experience Platform] Los destinos de cumplen las políticas de uso de datos al administrar los datos. Para obtener información detallada sobre cómo [!DNL Adobe Experience Platform] exige el control de datos; consulte [información general sobre la administración de datos](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html?lang=es).

<!--

## Activate segments to this destination {#activate}

See [Activate audience data to streaming segment export destinations](../../ui/activate-segment-streaming-destinations.md) for instructions on activating audience segments to this destination.

-->
