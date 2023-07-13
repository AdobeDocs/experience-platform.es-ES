---
keywords: Experience Platform;perfil;perfil de cliente en tiempo real;interfaz de usuario;IU;personalización;tablero de perfiles;tablero
title: Guía del panel Destinos
description: Adobe Experience Platform proporciona un panel a través del cual puede ver información importante acerca de los destinos activos de su organización.
type: Documentation
exl-id: 6a34a796-24a1-450a-af39-60113928873e
source-git-commit: f4f4deda02c96e567cbd0815783f192d1c54096c
workflow-type: tm+mt
source-wordcount: '3031'
ht-degree: 9%

---

# [!UICONTROL Destinos] tablero

La interfaz de usuario (IU) de Adobe Experience Platform proporciona un panel a través del cual puede ver información importante acerca de los destinos activos de su organización, tal como se capturan durante una instantánea diaria. Esta guía describe cómo acceder al panel de destinos de la interfaz de usuario y trabajar con él, y proporciona más información sobre las métricas que se muestran en el panel.

Para obtener una descripción general de los destinos, así como un catálogo de todos los destinos disponibles dentro de Experience Platform, visite el [documentación de destinos](../../destinations/home.md).

## [!UICONTROL Destinos] datos del panel {#destinations-dashboard-data}

El panel Destinos muestra una instantánea de los destinos que su organización ha activado en Experience Platform. Los datos de la instantánea muestran los datos exactamente como aparecen en el momento específico en el que se tomó. En otras palabras, la instantánea no es una aproximación o una muestra de los datos y el panel de destinos no se actualiza en tiempo real.

>[!NOTE]
>
>Los cambios o actualizaciones realizados en los datos desde que se tomó la instantánea no se reflejarán en el tablero hasta que se tome la siguiente instantánea.

## Explore la [!UICONTROL Destinos] tablero {#explore}

Para navegar al panel de destinos dentro de la IU de Platform, seleccione **[!UICONTROL Destinos]** en el carril izquierdo, seleccione **[!UICONTROL Información general]** para mostrar el tablero.

La fecha y la hora de la instantánea más reciente se muestran en la parte superior de la [!UICONTROL Información general] junto al menú desplegable de destino. Todos los datos del widget son precisos a partir de esa fecha y hora. La marca de tiempo de la instantánea se proporciona en formato UTC; no se encuentra en la zona horaria del usuario u organización individual.

>[!NOTE]
>
>Si su organización es nueva en Experience Platform y aún no tiene destinos activos, el panel Destinos y [!UICONTROL Información general] no son visibles. En su lugar, seleccione [!UICONTROL Destinos] desde la navegación izquierda se muestra el [!UICONTROL Catálogo] pestaña. Para obtener más información sobre [!UICONTROL Catálogo] , consulte la [[!UICONTROL Destinos] guía de workspace](../../destinations/ui/destinations-workspace.md).

![Información general sobre los destinos de la interfaz de usuario de Platform con la instantánea más reciente resaltada.](../images/destinations/snapshot-timestamp.png)

### Modifique la [!UICONTROL Destinos] tablero {#modify}

Seleccionar **[!UICONTROL Modificar tablero]** para cambiar el aspecto del panel destinos. Esto permite mover, añadir y eliminar widgets del tablero, así como acceder a la biblioteca de widgets. Desde la biblioteca de widgets, puede explorar los widgets disponibles y crear widgets personalizados para su organización.

Consulte la [modificación de paneles](../customize/modify.md) y [introducción a la biblioteca de widgets](../customize/widget-library.md) para obtener más información.

### Añadir widgets {#add-widget}

Seleccionar **[!UICONTROL Agregar widget]** para desplazarse a la biblioteca de widgets y ver una lista de los widgets disponibles para agregarlos al tablero.

![Información general del panel Destinos con el widget Agregar resaltado.](../images/destinations/destinations-overview-add-widget.png)

Desde la biblioteca de widgets, puede examinar la selección de widgets de audiencia estándar y personalizados. Para obtener información sobre cómo añadir widgets, consulte la documentación de la biblioteca de widgets sobre cómo [añadir un widget](../customize/widget-library.md#add-widgets).

## Widgets estándar {#standard-widgets}

Adobe proporciona varios widgets estándar que puede utilizar para visualizar diferentes métricas relacionadas con los  y evaluar la integridad de las audiencias disponibles para el análisis de datos. También puede crear widgets personalizados para compartirlos con su organización mediante el [!UICONTROL Biblioteca de widgets]. Para obtener más información sobre la creación de widgets personalizados, comience por leer el [Resumen de biblioteca de widgets](../customize/widget-library.md).

### Requisitos previos {#prerequisites}

Antes de continuar con las descripciones de los widgets estándar, asegúrese de estar familiarizado con las definiciones de los siguientes términos clave utilizados en la documentación:

* **Definición del segmento:** Una definición de segmento es una **conjunto de reglas** se utiliza para describir las características clave o el comportamiento de una audiencia objetivo. Estas reglas incluyen datos de atributos y eventos que clasifican los perfiles como parte de una audiencia.
* **Audiencia**: conjunto de personas, cuentas, hogares u otras entidades que comparten características y comportamientos comunes.
* **Asignado/asignación**: la asignación de datos es el proceso de asignación de campos de datos de origen a campos de destino relacionados en un destino.
* **Identidad**: una identidad es un identificador que representa de forma exclusiva a un cliente individual, como un ID de cookie, un ID de dispositivo o un ID de correo electrónico.
* **Activar**: Activar es la acción realizada por un usuario para asignar una audiencia o perfiles a un destino como Oracle Eloqua, Google o Marketing Cloud de Salesforce.

Para obtener más información sobre cada uno de los widgets estándar disponibles, seleccione el nombre de un widget en la siguiente lista:

* [[!UICONTROL Destinos más utilizados]](#most-used-destinations)
* [[!UICONTROL Destinos creados recientemente]](#recently-created-destinations)
* [[!UICONTROL Audiencias activadas recientemente]](#recently-activated-audiences)
* [[!UICONTROL Audiencias activadas recientemente por destino]](#recently-activated-audiences-by-destination)
* [[!UICONTROL Tendencia de tamaño de audiencia]](#audience-size-trend)
* [[!UICONTROL Audiencias no asignadas por identidad]](#unmapped-audiences-by-identity)
* [[!UICONTROL Audiencias asignadas por identidad]](#mapped-audiences-by-identity)
* [[!UICONTROL Audiencias comunes]](#common-audiences)
* [[!UICONTROL Audiencias asignadas]](#mapped-audiences)
* [[!UICONTROL Estado de audiencia asignado]](#mapped-audience-health)
* [[!UICONTROL Recuento de destinos]](#destinations-count)
* [[!UICONTROL Estado del destino]](#destination-status)
* [[!UICONTROL Destinos activos por plataforma de destino]](#active-destinations-by-destination-platform)
* [[!UICONTROL Audiencias activadas en todos los destinos]](#activated-audiences-across-all-destinations)
* [[!UICONTROL Audiencias activadas]](#activated-audiences)

### [!UICONTROL Destinos más utilizados] {#most-used-destinations}

>[!CONTEXTUALHELP]
>id="platform_dashboards_destinations_mostuseddestinations"
>title="Destinos más utilizados"
>abstract="Este widget muestra los destinos más activos de su organización según el número de audiencias asignadas. Estos números son precisos en el momento de la última instantánea. Esta clasificación proporciona una perspectiva sobre los destinos que se utilizan más actualmente, al tiempo que resalta los que pueden estar infrautilizados."

El **[!UICONTROL Destinos más utilizados]** widget muestra los principales destinos de su organización según el número de audiencias asignadas, a partir de la última instantánea. Esta clasificación proporciona una perspectiva de los destinos que se están utilizando, pero también muestra potencialmente aquellos que pueden estar infrautilizados.

Por ejemplo, si configuró un destino ayer pero no le ha asignado ninguna audiencia, podrá ver que el destino está actualmente infrautilizado.

El número de audiencias asignadas que se muestran en la [!UICONTROL Recuento de audiencias] es precisa a partir de la última instantánea diaria. La asignación de una nueva audiencia al destino no actualiza el recuento hasta que se produce la siguiente instantánea.

Seleccione el nombre de un destino en la lista que aparece en el widget para navegar hasta los detalles de destino de ese destino en particular. También puede seleccionar **[!UICONTROL Ver todo]** para ir al **[!UICONTROL Examinar]** y, a continuación, seleccione el nombre de un destino para ver sus detalles.

![La pestaña Información general del panel Destinos con el widget Destinos más utilizados resaltado.](../images/destinations/most-used-destinations.png)

### [!UICONTROL Destinos creados recientemente] {#recently-created-destinations}

>[!CONTEXTUALHELP]
>id="platform_dashboards_destinations_recentlycreateddestinations"
>title="Destinos creados recientemente"
>abstract="Este widget muestra una lista de los destinos configurados más recientemente dentro de su organización."

El **[!UICONTROL Destinos creados recientemente]** Este widget le permite ver una lista de los destinos configurados más recientemente para su organización.

La fecha de creación que se muestra es la exacta de la última instantánea diaria. En otras palabras, si crea un nuevo destino, no aparecerá en la lista hasta que se tome la siguiente instantánea.

Al seleccionar el nombre de un destino en la lista que se muestra en el widget, se le dirigirán a los detalles de destino como vinculados desde el **[!UICONTROL Examinar]** pestaña. También puede seleccionar **[!UICONTROL Ver todo]** para ir al **[!UICONTROL Examinar]** y, a continuación, seleccione el nombre de un destino para ver sus detalles.

Para obtener más información sobre cómo configurar tipos específicos de destinos, visite la [documentación de destinos](../../destinations/home.md).

![La pestaña Información general del panel Destinos con el widget de destinos creados recientemente resaltado.](../images/destinations/recently-created-destinations.png)

### [!UICONTROL Audiencias activadas recientemente] {#recently-activated-audiences}

>[!CONTEXTUALHELP]
>id="platform_dashboards_destinations_recentlyactivatedsegments"
>title="Audiencias activadas recientemente"
>abstract="Este widget proporciona una lista de las audiencias asignadas más recientemente a un destino. Esta lista proporciona una instantánea de las audiencias y los destinos que se utilizan de forma activa en el sistema y puede ayudar a solucionar cualquier asignación errónea."

El **[!UICONTROL Audiencias activadas recientemente]** widget proporciona una lista de las audiencias asignadas más recientemente a un destino. Esta lista proporciona una instantánea de las audiencias y los destinos que se utilizan de forma activa en el sistema y puede ayudar a solucionar cualquier asignación errónea.

El [!UICONTROL Actualizado] la fecha mostrada muestra la última vez que la audiencia se activó en el destino y es precisa hasta la última instantánea diaria. En otras palabras, si activa una audiencia en el destino, la fecha de actualización no cambia hasta que se tome la siguiente instantánea.

Al seleccionar el nombre de una audiencia en la lista que se muestra en el widget, se accede a los detalles de la audiencia. También puede seleccionar **[!UICONTROL Ver todo]** para ir al [!UICONTROL Audiencias] [!UICONTROL Examinar] y, a continuación, seleccione el nombre de una audiencia para ver sus detalles.

Para obtener más información sobre cómo trabajar con audiencias en Experience Platform, consulte la [Resumen del servicio de segmentación](../../segmentation/home.md).

![La pestaña Información general del panel Destinos con el widget de audiencias activadas recientemente resaltado.](../images/destinations/recently-activated-audiences.png)

### [!UICONTROL Audiencias activadas recientemente por destino] {#recently-activated-audiences-by-destination}

>[!CONTEXTUALHELP]
>id="platform_dashboards_destinations_recentlyactivatedsegmentsbydestination"
>title="Audiencias activadas recientemente por destino"
>abstract="Este widget muestra las cinco audiencias activadas más recientemente en orden descendente según el destino elegido en la lista desplegable de información general."

El **[!UICONTROL Audiencias activadas recientemente por destino]** widget muestra las cinco audiencias activadas más recientemente en orden descendente según el destino elegido en la lista desplegable de información general. Es similar a la [!UICONTROL Audiencias activadas recientemente] widget, pero se muestran los datos **solamente** se aplica al destino seleccionado.

Este widget contiene dos métricas: el nombre de las audiencias y la fecha en que se activaron por última vez en el destino. Los datos mostrados son correctos desde la última instantánea diaria.

Para ver los detalles de una audiencia, seleccione el nombre de la audiencia en la lista que se muestra.

![El widget Audiencias activadas recientemente por destino.](../images/destinations/recently-activated-audiences-by-destination.png)

Consulte la sección de requisitos previos para obtener la [definiciones de los términos utilizados](#prerequisites) en esta descripción.

### [!UICONTROL Tendencia de tamaño de audiencia] {#audience-size-trend}

>[!CONTEXTUALHELP]
>id="platform_dashboards_destinations_audiencesizetrend"
>title="Tendencia de tamaño de audiencia"
>abstract="Este widget ilustra el número de perfiles que contiene la audiencia, que se envían diariamente a la cuenta de destino. El primer menú desplegable ajusta el período de tiempo de la tendencia de audiencia. El segundo menú desplegable de widgets selecciona la audiencia para su análisis. El destino se elige en el menú desplegable Información general."

El **[!UICONTROL Tendencia de tamaño de audiencia]** widget muestra la relación del recuento de perfiles durante un período de tiempo para una audiencia que se ha asignado a esa cuenta de destino. El widget utiliza un gráfico de líneas para ilustrar el número de perfiles contenidos en la audiencia que se envían diariamente a la cuenta de destino.

Se puede ajustar un periodo de tiempo para la tendencia de la audiencia en los últimos 30 días, 90 días o 12 meses mediante el primer menú desplegable.

El segundo menú desplegable enumera todas las audiencias disponibles que se pueden enviar a la cuenta de destino elegida en la parte superior del panel.

![El widget de tendencia Tamaño de audiencia.](../images/destinations/audience-size-trend.png)

El **[!UICONTROL Tendencia de tamaño de audiencia]** El widget proporciona un [!UICONTROL Subtítulos] en la parte superior derecha del widget. Seleccionar **[!UICONTROL Subtítulos]** para abrir el diálogo subtítulos automáticos. Un modelo de aprendizaje automático genera automáticamente subtítulos para describir las tendencias clave y los eventos importantes mediante el análisis del gráfico y los datos de audiencia.

![Cuadro de diálogo de subtítulos automáticos para el widget de tendencia de tamaño de audiencia.](../images/destinations/audience-size-trend-captions.png)

### [!UICONTROL Audiencias no asignadas por identidad] {#unmapped-audiences-by-identity}

>[!CONTEXTUALHELP]
>id="platform_dashboards_destinations_unmappedsegmentsbyidentity"
>title="Audiencias no asignadas por identidad"
>abstract="Este widget enumera los cinco principales **sin asignar** las audiencias clasificadas por recuento de identidad descendente para un destino e identidad determinados. Los ID de filtro enumerados en el menú desplegable del widget cambian según la cuenta de destino seleccionada en la parte superior de la página de información general."

El **[!UICONTROL Audiencias no asignadas por identidad]** widget enumera los cinco principales **sin asignar** las audiencias clasificadas por recuento de identidad descendente para un destino e identidad determinados. Resalta las audiencias que son más beneficiosas para asignar a la cuenta de destino elegida en función del ID elegido.

El menú desplegable de ID de destino filtra las audiencias disponibles. Los ID de filtro enumerados en el menú desplegable del cambian según la cuenta de destino seleccionada en la parte superior de la página de información general.

La columna de identidades cuenta el número de ID de origen dentro de la audiencia que podrían asignarse al ID elegido en la lista desplegable ID del widget.

![Widget de audiencias no asignadas por identidad.](../images/destinations/unmapped-audiences-by-identity.png)

Consulte la sección de requisitos previos para obtener la [definiciones de los términos utilizados](#prerequisites) en esta descripción.

### [!UICONTROL Audiencias asignadas por identidad] {#mapped-audiences-by-identity}

>[!CONTEXTUALHELP]
>id="platform_dashboards_destinations_mappedsegmentsbyidentity"
>title="Audiencias asignadas por identidad"
>abstract="Este widget proporciona una lista de los cinco principales **asignado** audiencias. La lista se ordena de alta a baja según el número de ID de origen contenidos dentro de las audiencias. El ID de destino que se va a contar se selecciona en el menú desplegable situado debajo del título del widget. Los ID de destino disponibles en el menú desplegable del widget dependen del destino elegido en la parte superior del panel de información general."

Este widget proporciona una lista de los cinco principales **asignado** audiencias. La lista se ordena de alta a baja según el número de ID de origen contenidos dentro de las audiencias. El ID de destino que se va a contar se selecciona en el menú desplegable situado debajo del título del widget. Los ID de destino disponibles en la lista desplegable del widget cambiarán según el filtro de cuenta de destino elegido en la parte superior del panel de información general.

![El widget Audiencias asignadas por identidad.](../images/destinations/mapped-audiences-by-identity.png)

El **[!UICONTROL Audiencias asignadas por identidad]** de un vistazo, el widget resalta la probabilidad de segmentar correctamente las oportunidades de perfil para una campaña dentro del destino elegido. Una campaña objetivo eficaz no depende del número de perfiles enviados al destino, sino del número de ID de origen que es probable que coincidan con los ID de destino para proporcionar datos útiles y procesables.

### Audiencias comunes {#common-audiences}

>[!CONTEXTUALHELP]
>id="platform_dashboards_destinations_commonaudiences"
>title="Audiencias comunes"
>abstract="Este widget proporciona una lista de las cinco audiencias principales activadas en la cuenta de destino elegida en la parte superior de la página y el destino seleccionado en la lista desplegable del widget. La lista de audiencias se ordena según la fecha de activación. La audiencia activada más recientemente se muestra en la parte superior."

El **[!UICONTROL Audiencias comunes]** widget proporciona una lista de las cinco audiencias principales activadas en la cuenta de destino elegida en la parte superior de la página y el destino seleccionado en la lista desplegable del widget. La lista de audiencias se ordena según la fecha de activación. La audiencia activada más recientemente se muestra en la parte superior.

El [!UICONTROL TAMAÑO DE AUDIENCIA] proporciona el recuento total de perfiles de cada audiencia enumerada.

![El widget de audiencias comunes.](../images/destinations/common-audiences.png)

### Audiencias asignadas {#mapped-audiences}

El [!UICONTROL Audiencias asignadas] widget muestra el número total de audiencias asignadas que se pueden activar al destino seleccionado en la parte superior de la página.

Seleccionar **[!UICONTROL Audiencias]** para ir al panel Audiencias [!UICONTROL Examinar] pestaña. Este espacio de trabajo muestra una lista de todas las definiciones de segmentos de su organización.

![El widget Audiencias asignadas.](../images/destinations/mapped-audiences.png)

### Estado de audiencia asignado {#mapped-audience-health}

>[!CONTEXTUALHELP]
>id="platform_dashboards_destinations_mappedaudiencehealth"
>title="Estado de audiencia asignado"
>abstract="Este widget proporciona una lista de hasta 20 audiencias asignadas cuyos recuentos de perfiles totales se desvían por un factor de al menos una desviación estándar del tamaño de audiencia promedio de 30 días asignado a ese destino. Proporciona una métrica calculada para la dispersión de los tamaños de audiencia de la media durante los últimos 30 días. Los tamaños de audiencia se ordenan de mayor a menor."

El widget proporciona una lista de hasta 20 audiencias asignadas cuyo recuento total de perfiles, a partir de la última instantánea diaria, se desvía por un factor de al menos una desviación estándar del tamaño medio de audiencia asignado a ese destino a los 30 días.

En resumen, proporciona una métrica calculada para la dispersión de los tamaños de audiencia desde la media de los últimos 30 días. Compara si el tamaño de la audiencia actual está fuera de la desviación estándar histórica vista en los datos de los últimos 30 días.

Todos los tamaños de audiencia del sistema se ordenan de alto a bajo, tal como se indica en la [!UICONTROL ÚLTIMO TAMAÑO] columna.

Si el recuento de perfiles de audiencia asignados está fuera de una desviación estándar del tamaño promedio de perfil asignado en los últimos 30 días, esto indica una anomalía en el sistema y debe investigarse.

Si una audiencia dentro de [!UICONTROL Estado de audiencia asignado] Si un widget se desvía por un amplio margen, debe consultar el gráfico de tendencias del tamaño de la audiencia y localizar la audiencia anómala. La tendencia puede proporcionar más información sobre el estado de la audiencia.

>[!NOTE]
>
>El tamaño predeterminado del widget de estado de audiencia asignado puede obstruir la información de la tabla. Modifique el tamaño del widget para mejorar la legibilidad de los nombres de audiencia y títulos de columna asignados. Consulte la documentación de modificación de paneles para obtener instrucciones sobre [cómo cambiar el tamaño de un widget](../customize/modify.md).

![El widget de estado de audiencia asignado.](../images/destinations/mapped-audience-health.png)

### [!UICONTROL Recuento de destinos] {#destinations-count}

>[!CONTEXTUALHELP]
>id="platform_dashboards_destinations_destinationscount"
>title="Recuento de destinos"
>abstract="Este widget proporciona el número total de puntos finales disponibles en los que se puede activar y enviar una audiencia dentro del sistema. Este número incluye destinos tanto activos como inactivos."

El [!UICONTROL Recuento de destinos] widget proporciona el número total de puntos de conexión disponibles donde se puede activar y enviar una audiencia dentro del sistema. Este número incluye destinos tanto activos como inactivos.

Debajo del recuento total, seleccione **[!UICONTROL Destinos]** para ir a la pestaña destinos examinar. Esta página lista todos los destinos con los que ha establecido una conexión hasta la fecha.

![El widget Recuento de destinos.](../images/destinations/destinations-count.png)

### [!UICONTROL Estado del destino] {#destination-status}

El [!UICONTROL Estado del destino] widget muestra el número total de destinos habilitados como una sola métrica y utiliza un gráfico de anillo para ilustrar la diferencia proporcional entre los destinos habilitados y deshabilitados.

Los recuentos individuales de los destinos habilitados o deshabilitados se muestran en un cuadro de diálogo cuando el cursor se pasa por encima de la sección correspondiente del gráfico circular.

![El widget de estado de destino.](../images/destinations/destination-status.png)

### [!UICONTROL Destinos activos por plataforma de destino] {#active-destinations-by-destination-platform}

El widget proporciona una tabla de dos columnas para mostrar una lista de las plataformas de destino activas y el número total de destinos activos para cada plataforma de destino. La lista de plataformas de destino se ordena de alta a baja.

![El widget Destinos activos por plataforma de destino.](../images/destinations/active-destinations-by-destination-platform.png)

### [!UICONTROL Audiencias activadas en todos los destinos] {#activated-audiences-across-all-destinations}

El [!UICONTROL Audiencias activadas en todos los destinos] widget proporciona el número total de audiencias activadas en todos los destinos en una sola métrica. Este número corresponde a la instantánea más reciente.

![El widget Audiencias activadas en todos los destinos.](../images/destinations/activated-audiences-across-all-destinations.png)

Seleccionar **[!UICONTROL Audiencias]** para ir a los destinos [!UICONTROL Examinar] pestaña. Esta página proporciona una lista de todos los destinos habilitados y una variedad de métricas relevantes. Consulte la documentación para obtener más información sobre [[!UICONTROL Examinar] pestaña](../../destinations/ui/destinations-workspace.md#browse).

Consulte la sección de requisitos previos para obtener la [definiciones de los términos utilizados](#prerequisites) en esta descripción.

### [!UICONTROL Audiencias activadas] {#activated-audiences}

Este widget proporciona una sola métrica para el número total de audiencias activadas en un destino.

![El widget Audiencias activadas.](../images/destinations/activated-audiences.png)

Seleccionar **[!UICONTROL Audiencias]** para ir a la página de detalles del panel destinos. El [!UICONTROL Datos de activación] La pestaña muestra una lista de audiencias que se han asignado al destino, incluida su fecha de inicio y finalización (si corresponde) y otra información relevante para la exportación de datos, como el tipo de exportación, la programación y la frecuencia. Para ver los detalles de una audiencia en particular, seleccione su nombre en la [!UICONTROL Nombre de audiencia] columna.

![La página de detalles del panel de destinos con la pestaña de datos de activación resaltada.](../images/destinations/activation-data-tab.png)

Este widget le ayuda a comprender el valor de sus destinos en función del número de audiencias activadas de un vistazo. También facilita el acceso a información más detallada para un análisis más detallado.

Consulte la sección de requisitos previos para obtener la [definiciones de los términos utilizados](#prerequisites) en esta descripción.

## Pasos siguientes

Al seguir este documento, ahora debería poder localizar el panel de destinos y comprender las métricas mostradas en los widgets disponibles. Para obtener más información sobre cómo trabajar con destinos en Experience Platform, consulte la [documentación de destinos](../../destinations/home.md).
