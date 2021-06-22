---
keywords: Experience Platform;perfil;perfil de cliente en tiempo real;solución de problemas;API;perfil unificado;perfil unificado;unificado;perfil;rtcp;habilitar perfil;Activar perfil;esquema de unión;PERFIL DE UNIÓN;perfil de unión
title: Guía de la interfaz de usuario del perfil del cliente en tiempo real
topic-legacy: guide
description: El perfil del cliente en tiempo real crea una vista holística de cada uno de sus clientes individuales, combinando datos de varios canales, incluidos datos en línea, sin conexión, CRM y de terceros. Este documento sirve como guía para interactuar con el Perfil del cliente en tiempo real en la interfaz de usuario de Adobe Experience Platform.
exl-id: 792a3a73-58a4-4163-9212-4d43d24c2770
source-git-commit: 2791c32abe582d51d05d4bf0488ba82dfadfd053
workflow-type: tm+mt
source-wordcount: '1319'
ht-degree: 0%

---

# [!DNL Real-time Customer Profile] Guía de la interfaz de usuario

[!DNL Real-time Customer Profile] crea una vista holística de cada uno de sus clientes individuales, combinando datos de varios canales, incluidos datos en línea, sin conexión, CRM y de terceros. Este documento sirve como guía para interactuar con datos [!DNL Real-time Customer Profile] en la interfaz de usuario (IU) de Adobe Experience Platform.

## Primeros pasos

Esta guía de la interfaz de usuario requiere conocer los distintos [!DNL Experience Platform] servicios relacionados con la administración de [!DNL Real-time Customer Profiles]. Antes de leer esta guía o de trabajar en la interfaz de usuario, revise la documentación de los siguientes servicios:

* [[!DNL Real-time Customer Profile]](../home.md): Proporciona un perfil de cliente unificado y en tiempo real basado en datos agregados de varias fuentes.
* [[!DNL Identity Service]](../../identity-service/home.md): Habilita  [!DNL Real-time Customer Profile] mediante el puente de identidades de fuentes de datos dispares a medida que se incorporan en  [!DNL Platform].
* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): El marco estandarizado mediante el cual se  [!DNL Platform] organizan los datos de experiencia del cliente.

## Información general

En la interfaz de usuario del Experience Platform, seleccione **[!UICONTROL Profiles]** en el panel de navegación izquierdo para abrir la pestaña **[!UICONTROL Overview]** que muestra el panel [!UICONTROL Profiles].

>[!NOTE]
>
>Si su organización es nueva en Platform y aún no tiene conjuntos de datos de perfil activos o políticas de combinación creadas, el panel [!UICONTROL Perfiles] no está visible. En su lugar, la pestaña [!UICONTROL Información general] muestra vínculos y documentación para ayudarle a empezar con el Perfil del cliente en tiempo real.

###  Panel de perfiles  {#profile-dashboard}

El tablero **[!UICONTROL Profiles]** describe métricas clave relacionadas con los datos de perfil de su organización.

Para obtener más información, consulte la [Guía del tablero de perfil](../../dashboards/guides/profiles.md).

![](../../dashboards/images/profiles/dashboard-overview.png)

## Examinar

Seleccione la pestaña **[!UICONTROL Browse]** para examinar los perfiles por identidad.

![](../images/user-guide/profiles-browse.png)

### Métricas de perfil {#profile-metrics}

A la derecha de la pestaña **[!UICONTROL Browse]** hay varias métricas importantes relacionadas con los datos de perfil, incluido su [recuento de perfiles](#profile-count) total, así como una lista de [perfiles por área de nombres](#profiles-by-namespace).

Estas métricas de perfil se evalúan mediante la política de combinación predeterminada de su organización. Para obtener más información sobre cómo trabajar con políticas de combinación, incluida cómo definir una directiva de combinación predeterminada, consulte [merge policy overview](../merge-policies/overview.md).

Además de estas métricas, la sección de métricas de perfil también proporciona una fecha y hora de última actualización, que muestra cuándo se evaluaron las métricas por última vez.

![](../images/user-guide/profiles-profile-metrics.png)

### Recuento de perfiles {#profile-count}

El recuento de perfiles muestra el número total de perfiles que tiene la organización en [!DNL Experience Platform], después de que la política de combinación predeterminada de la organización se haya fusionado con fragmentos de perfil para formar un único perfil para cada cliente individual. En otras palabras, su organización puede tener varios fragmentos de perfil relacionados con un único cliente que interactúa con su marca a través de diferentes canales, pero estos fragmentos se fusionarían juntos (según la política de combinación predeterminada) y devolverían un recuento de &quot;1&quot; perfil porque todos están relacionados con la misma persona.

El recuento de perfiles también incluye perfiles con atributos (datos de registro) y perfiles que solo contienen datos de series temporales (eventos), como perfiles de Adobe Analytics. El recuento de perfiles se actualiza regularmente para proporcionar un número total actualizado de perfiles dentro de Platform.

Cuando la ingesta de registros en el almacén [!DNL Profile] aumenta o disminuye el recuento en más del 5 %, se activa un trabajo para actualizar el recuento. Para los flujos de trabajo de datos de flujo continuo, se realiza una comprobación cada hora para determinar si se ha alcanzado el umbral de aumento o reducción del 5 %. Si lo ha hecho, se activa automáticamente un trabajo para actualizar el recuento de perfiles. Para la ingesta por lotes, en un plazo de 15 minutos tras la ingesta correcta de un lote en el Almacenamiento de perfiles, si se alcanza el umbral de aumento o disminución del 5 %, se ejecuta un trabajo para actualizar el recuento de perfiles.

### Perfiles por área de nombres {#profiles-by-namespace}

La métrica **[!UICONTROL Perfiles por área de nombres]** muestra el recuento total y el desglose de áreas de nombres en todos los perfiles combinados en el Almacenamiento de perfiles. El número total de perfiles por área de nombres (es decir, sumando los valores mostrados para cada área de nombres) siempre será mayor que la métrica de recuento de perfiles porque un perfil podría tener varias áreas de nombres asociadas. Por ejemplo, si un cliente interactúa con la marca en más de un canal, se asociarán varias áreas de nombres con ese cliente individual.

De forma similar a la métrica [recuento de perfiles](#profile-count), cuando la ingesta de registros en el almacén [!DNL Profile] aumenta o disminuye el recuento en más del 5%, se activa un trabajo para actualizar las métricas del área de nombres. Para los flujos de trabajo de datos de flujo continuo, se realiza una comprobación cada hora para determinar si se ha alcanzado el umbral de aumento o reducción del 5 %. Si lo ha hecho, se activa automáticamente un trabajo para actualizar el recuento de perfiles. Para la ingesta por lotes, en un plazo de 15 minutos tras la ingesta correcta de un lote en el almacén [!DNL Profile], si se alcanza el umbral de aumento o disminución del 5 %, se ejecuta un trabajo para actualizar las métricas.

### Combinar directiva

El selector **[!UICONTROL Merge policy]** selecciona automáticamente la directiva de combinación predeterminada para su organización. Si no desea utilizar esa política de combinación, puede seleccionar `X` junto a la directiva de combinación predeterminada para abrir el cuadro de diálogo **[!UICONTROL Seleccionar política de combinación]**, donde puede elegir otra política de combinación.

Para obtener más información sobre las políticas de combinación y su función dentro de Platform, consulte la [información general sobre las políticas de combinación](../merge-policies/overview.md).

![](../images/user-guide/profiles-search-merge-policy.png)

### Área de nombres de identidad

El selector **[!UICONTROL Área de nombres de identidad]** abre un cuadro de diálogo en el que puede elegir el área de nombres de identidad por el que desea buscar y puede personalizar los atributos que se muestran en la búsqueda seleccionando el icono de filtro y eligiendo qué atributos desea agregar o quitar.

![](../images/user-guide/profiles-search-filter.png)

En el cuadro de diálogo **[!UICONTROL Seleccionar área de nombres de identidad]**, elija el área de nombres en la que desea buscar o utilice la barra de búsqueda del cuadro de diálogo para empezar a escribir el nombre de un área de nombres. Puede seleccionar un área de nombres para ver detalles adicionales y una vez encontrado el área de nombres que desee utilizar, puede seleccionar el botón de opción y pulsar **[!UICONTROL Select]** para continuar.

![](../images/user-guide/profiles-select-identity-namespace.png)

### Valor de identidad

Después de seleccionar un área de nombres de identidad, vuelva a la pestaña **[!UICONTROL Browse]** donde puede introducir un **[!UICONTROL Identity value]**. Este valor es específico de un perfil de cliente individual y debe ser una entrada válida para el área de nombres proporcionada. Por ejemplo, seleccionar el área de nombres de identidad &quot;Correo electrónico&quot; requeriría un valor de identidad en forma de dirección de correo electrónico válida.

![](../images/user-guide/profiles-show-profile.png)

Una vez introducido un valor, seleccione **[!UICONTROL Mostrar perfil]** y se devuelve un solo perfil que coincida con el valor. Seleccione el **[!UICONTROL ID de perfil]** para ver los detalles del perfil.

![](../images/user-guide/profiles-display-profile.png)

### Detalles de perfil {#profile-detail}

Al seleccionar el **[!UICONTROL ID de perfil]**, se abre la pestaña **[!UICONTROL Detail]**. La información de perfil mostrada en la pestaña **[!UICONTROL Detail]** se ha combinado desde varios fragmentos de perfil para formar una sola vista del cliente individual. Esto incluye detalles del cliente, como atributos básicos, identidades vinculadas y preferencias de canal. Los campos predeterminados mostrados también se pueden cambiar en el nivel de organización para mostrar los atributos de perfil preferidos. Para obtener más información sobre la personalización de estos campos, incluidas las instrucciones paso a paso para agregar y eliminar atributos y cambiar el tamaño de los paneles del tablero, consulte la [guía de personalización de detalles del perfil](profile-customization.md).

![](../images/user-guide/profiles-profile-detail.png)

Puede ver información adicional relacionada con el perfil individual seleccionando otra de las pestañas disponibles. Estas pestañas incluyen atributos, eventos y pertenencia a segmentos, que muestran los segmentos para los que el perfil está cualificado actualmente.

![](../images/user-guide/profiles-attributes-events-segments.png)

## Combinar directivas

En el menú principal **[!UICONTROL Profiles]**, seleccione la pestaña **[!UICONTROL Merge Policies]** para ver una lista de directivas de combinación que pertenecen a su organización. Cada directiva de la lista muestra su nombre, tanto si es la directiva de combinación predeterminada como la clase de esquema a la que se aplica.

Para obtener más información sobre las políticas de combinación, consulte [merge policy overview](../merge-policies/overview.md).

![](../images/user-guide/profiles-merge-policies.png)

## Esquema de unión {#union-schema}

En el menú principal **[!UICONTROL Profiles]**, seleccione la pestaña **[!UICONTROL Union Schema]** para ver los esquemas de unión disponibles para sus datos introducidos. Un esquema de unión es una combinación de todos los campos [!DNL Experience Data Model] (XDM) de la misma clase, cuyos esquemas se han habilitado para su uso en [!DNL Real-time Customer Profile].

Para obtener más información sobre los esquemas de unión, visite la [guía de la interfaz de usuario del esquema de unión](union-schema.md).

![](../images/user-guide/profiles-union-schema.png)

## Pasos siguientes

Al leer esta guía, ahora sabe cómo ver y administrar sus datos [!DNL Profile] mediante la interfaz de usuario [!DNL Experience Platform]. Para obtener información sobre cómo trabajar con datos de perfil mediante la API de perfil de cliente en tiempo real, consulte la [Guía para desarrolladores de perfil](../api/overview.md).
