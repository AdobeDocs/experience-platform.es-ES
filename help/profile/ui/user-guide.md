---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
solution: Adobe Experience Platform
title: Guía del usuario de Perfil del cliente en tiempo real
topic: guide
translation-type: tm+mt
source-git-commit: 59dff7687f8a0c5b5084eb1ce7dd222cc18d8dbf
workflow-type: tm+mt
source-wordcount: '1208'
ht-degree: 0%

---


# Guía del usuario de Perfil del cliente en tiempo real

El Perfil del cliente en tiempo real crea una vista holística de cada uno de sus clientes individuales, combinando datos de varios canales, incluidos datos en línea, sin conexión, CRM y de terceros.

Este documento sirve como guía para interactuar con el Perfil del cliente en tiempo real en la interfaz de usuario de Adobe Experience Platform.

## Primeros pasos

Esta guía del usuario requiere conocer los distintos servicios de Experience Platform que se utilizan para administrar los Perfiles de los clientes en tiempo real. Antes de leer esta guía del usuario, consulte la documentación de los siguientes servicios:

* [Perfil](../home.md)del cliente en tiempo real: Proporciona un perfil de consumo unificado y en tiempo real basado en datos agregados de varias fuentes.
* [Servicio](../../identity-service/home.md)de identidad: Permite el Perfil del cliente en tiempo real al enlazar identidades de orígenes de datos dispares a medida que se van ingeriendo en Platform.
* [Modelo de datos de experiencia (XDM)](../../xdm/home.md): El marco estandarizado por el cual Platform organiza los datos de experiencia del cliente.

## Información general

En la interfaz de usuario [del](http://platform.adobe.com)Experience Platform, haga clic en **Perfiles** en el panel de navegación izquierdo para abrir la ficha _Información general_ . Esta ficha proporciona vínculos a documentación y vídeos para ayudarle a comprender y comenzar a trabajar con perfiles.

![](../images/user-guide/profiles-overview.png)

## Examinar

Seleccione la ficha *Examinar* para examinar los perfiles por identidad.

![](../images/user-guide/profiles-browse.png)

### Métricas de Perfil {#profile-metrics}

A la derecha de la ficha *Examinar* hay varias métricas importantes relacionadas con los datos de perfil, incluido el recuento [total de](#profile-count) perfiles, así como una lista de [perfiles por Área de nombres](#profiles-by-namespace).

Estas métricas de perfil se evalúan mediante la directiva de combinación predeterminada de su organización. Para obtener más información sobre cómo trabajar con políticas de combinación, incluida la definición de una directiva de combinación predeterminada, consulte la guía [de usuario Políticas de](merge-policies.md)combinación.

Además de estas métricas, la sección Métricas de perfil también proporciona una fecha y hora de *última actualización* , que muestra cuándo se evaluaron las métricas por última vez.

![](../images/user-guide/profiles-profile-metrics.png)

### Recuento de Perfiles {#profile-count}

El recuento de perfiles muestra el número total de perfiles que su organización tiene en Experience Platform, después de que la directiva de combinación predeterminada de su organización haya combinado fragmentos de perfil para formar un único perfil para cada cliente individual. En otras palabras, su organización puede tener varios fragmentos de perfil relacionados con un único cliente que interactúa con su marca en diferentes canales, pero estos fragmentos se combinarán (según la política de combinación predeterminada) y devolverá un recuento de perfiles &quot;1&quot; porque todos están relacionados con el mismo individuo.

El recuento de perfiles también incluye tanto perfiles con atributos (datos de registro) como perfiles que contienen únicamente datos de series temporales (eventos), como perfiles de Adobe Analytics. El recuento de perfiles se actualiza con regularidad para proporcionar un número total actualizado de perfiles dentro de Platform.

Cuando la ingestión de registros en el almacén de Perfiles aumenta o disminuye el recuento en más de un 5 %, se activa un trabajo para actualizar el recuento. Para los flujos de trabajo de datos de flujo continuo, se realiza una comprobación por hora para determinar si se ha alcanzado el umbral de aumento o reducción del 5 %. Si lo ha hecho, se activa automáticamente un trabajo para actualizar el recuento de perfiles. Para la ingestión por lotes, dentro de los 15 minutos siguientes a la ingestión satisfactoria de un lote en el almacén de Perfiles, si se alcanza el umbral de aumento o disminución del 5 %, se ejecuta un trabajo para actualizar el recuento de perfiles.

### Perfiles por Área de nombres {#profiles-by-namespace}

La métrica *Perfiles por Área de nombres* muestra el recuento total y el desglose de Áreas de nombres en todos los perfiles combinados de su almacén de Perfiles. El número total de perfiles por Área de nombres (es decir, sumar los valores mostrados para cada Área de nombres) siempre será mayor que la métrica de recuento de perfiles porque un perfil podría tener varias Áreas de nombres asociadas. Por ejemplo, si un cliente interactúa con su marca en más de un canal, se asociarán varias Áreas de nombres con ese cliente individual.

De forma similar a la métrica de recuento [de](#profile-count) perfiles, cuando la ingestión de registros en el almacén de Perfiles aumenta o disminuye el recuento en más de un 5 %, se activa un trabajo para actualizar las métricas de Área de nombres. Para los flujos de trabajo de datos de flujo continuo, se realiza una comprobación por hora para determinar si se ha alcanzado el umbral de aumento o reducción del 5 %. Si lo ha hecho, se activa automáticamente un trabajo para actualizar el recuento de perfiles. Para la ingestión por lotes, dentro de los 15 minutos posteriores a la ingestión satisfactoria de un lote en el almacén de Perfiles, si se alcanza el umbral de aumento o reducción del 5 %, se ejecuta un trabajo para actualizar las métricas.

### Combinar directiva

El selector de directivas **de** combinación selecciona automáticamente la directiva de combinación predeterminada para su organización. Si no desea utilizar esa política de combinación, puede seleccionar la opción `X` situada junto a la directiva de combinación predeterminada para abrir un cuadro de diálogo *Seleccionar directiva* de combinación donde puede elegir otra directiva de combinación. Para obtener más información sobre las directivas de combinación, consulte la guía [del usuario](merge-policies.md)Combinar directivas.

![](../images/user-guide/profiles-search-merge-policy.png)

### Área de nombres de identidad

El selector de Área de nombres **de** identidad abre un cuadro de diálogo en el que puede elegir la Área de nombres de identidad por la que desea buscar y puede personalizar los atributos que se muestran en la búsqueda seleccionando el icono de filtro y eligiendo los atributos que desea agregar o eliminar.

![](../images/user-guide/profiles-search-filter.png)

En el cuadro de diálogo *Seleccionar Área de nombres* de identidad, elija la Área de nombres por la que desea realizar la búsqueda o utilice la barra de **búsqueda** del cuadro de diálogo para empezar a escribir el nombre de una Área de nombres. Puede seleccionar una Área de nombres para vista de detalles adicionales, y una vez encontrada la Área de nombres que desea buscar puede seleccionar el botón de radio y pulsar **Seleccionar** para continuar.

![](../images/user-guide/profiles-select-identity-namespace.png)

### Valor de identidad

Después de seleccionar una Área de nombres **** de identidad, vuelva a la ficha *Examinar* , donde puede introducir un valor **** de identidad. Este valor es específico de un perfil de cliente individual y debe ser una entrada válida para la Área de nombres proporcionada. Por ejemplo, si selecciona la Área de nombres **de** identidad &quot;Correo electrónico&quot;, se requiere un valor **de** identidad en forma de una dirección de correo electrónico válida.

![](../images/user-guide/profiles-show-profile.png)

Una vez introducido un valor, seleccione **Mostrar perfil** y se devuelve un solo perfil que coincida con el valor. Seleccione el ID **de** Perfil para vista de los detalles de perfil.

![](../images/user-guide/profiles-display-profile.png)

### Detalles del Perfil

Al seleccionar el ID **de** Perfil, se abre la ficha _Detalle_ . Esta página muestra información sobre el perfil seleccionado, incluidos atributos básicos, identidades vinculadas y canales de contacto disponibles. La información de perfil mostrada se ha combinado desde varios fragmentos de perfil para formar una sola vista del cliente individual.

![](../images/user-guide/profiles-profile-detail.png)

Puede vista información adicional relacionada con el perfil, incluidos *Atributos*, *Eventos* y *Segmentos* a los que pertenece el perfil.

![](../images/user-guide/profiles-attributes-events-segments.png)

## Combinar directivas

Seleccione la ficha *Combinar políticas* para vista de una lista de directivas de combinación que pertenezcan a su organización. Cada directiva de la lista muestra su nombre, tanto si es la directiva de combinación predeterminada como si no, y el esquema al que se aplica.

Para obtener más información sobre las directivas de combinación, consulte la guía [del usuario Políticas de](merge-policies.md)combinación.

![](../images/user-guide/profiles-merge-policies.png)

## esquema de Unión

Seleccione la ficha Esquema *de* Unión para vista de los esquemas de unión de su almacén de Perfiles. Un esquema de unión es una combinación de todos los campos del Modelo de datos de experiencia (XDM) de la misma clase, cuyos esquemas se han habilitado para su uso en el Perfil del cliente en tiempo real. Seleccione una clase en la lista izquierda para vista de la estructura de su esquema de unión en el lienzo.

Por ejemplo, si selecciona &quot;Perfil XDM&quot;, se muestra el esquema de unión de la clase de Perfil individual XDM.

Consulte la sección sobre esquemas de unión en la guía [de composición de](../../xdm/schema/composition.md) esquemas para obtener más información sobre los esquemas de unión y su función en el Perfil de clientes en tiempo real.

![](../images/user-guide/profiles-union-schema.png)

## Pasos siguientes

Al leer esta guía, ahora sabe cómo realizar vistas y administrar los datos de Perfil mediante la interfaz de usuario del Experience Platform. Para obtener información sobre cómo aprovechar los datos de Perfil de clientes en tiempo real para generar segmentos de audiencia, consulte la documentación [de](../../segmentation/home.md)segmentación.