---
title: Redireccionamiento fuera del sitio de visitantes no autenticados
description: Obtenga información sobre cómo volver a dirigirse a usuarios no autenticados mediante los ID de cliente potencial para crear un atributo calculado que se pueda utilizar para crear una audiencia de usuarios no autenticados.
feature: Use Cases, Customer Acquisition
exl-id: cffa3873-d713-445a-a3e1-1edf1aa8eebb
source-git-commit: bb90bbddf33bc4b0557026a0f34965ac37475c65
workflow-type: tm+mt
source-wordcount: '1358'
ht-degree: 1%

---

# Redireccionamiento fuera del sitio de visitantes no autenticados

>[!AVAILABILITY]
>
>Esta funcionalidad está disponible para los clientes con licencia de Real-Time CDP (Servicio de aplicación), Adobe Experience Platform Activation, Real-Time CDP, Real-Time CDP Prime, Real-Time CDP Ultimate. Obtenga más información acerca de estos paquetes en las [descripciones de productos](https://helpx.adobe.com/es/legal/product-descriptions.html?lang=es) y póngase en contacto con el representante de Adobe para obtener más información.

Aprenda a crear una audiencia de visitantes no autenticados y a redirigirlos mediante los ID duraderos proporcionados por los socios.

![Infografía que muestra el flujo de datos del socio desde la ingesta en Adobe Experience Platform hasta la salida a través de audiencias a un destino descendente.](../assets/offsite-retargeting/header.png)

## Por qué considerar este caso de uso {#why-use-case}

Con la eliminación gradual de las cookies de terceros, los especialistas en marketing digital deben reimaginar sus estrategias para volver a interactuar con visitantes anónimos. Las marcas que optan por integrarse con proveedores de identidad para el reconocimiento de visitantes en tiempo real también pueden aprovechar los identificadores duraderos proporcionados por los socios para el retargeting de medios de pago fuera del sitio.

A pesar del alto volumen de tráfico, muchas marcas ven una caída significativa en la fase de conversión. Los visitantes participan con demostraciones de contenido y productos, pero se van sin registrarse ni realizar una compra.

No solo puede crear audiencias basadas en la participación en el sitio para personalizar los mensajes de marketing, sino que también puede utilizar la compatibilidad de Adobe con los ID de socio para volver a interactuar con los visitantes en destinos de medios de pago.

## Requisitos previos y planificación {#prerequisites-and-planning}

Cuando planee volver a dirigirse a visitantes no autenticados, tenga en cuenta los siguientes requisitos previos durante el proceso de planificación:

- ¿He configurado los ID de socio con las áreas de nombres de identidad adecuadas?

Además, para implementar el caso de uso, utilizará las siguientes funciones y elementos de la interfaz de usuario de Real-Time CDP. Asegúrese de que dispone de los permisos de control de acceso basados en atributos necesarios para todas estas áreas o pídale al administrador del sistema que le conceda los permisos necesarios.

- [Públicos](/help/segmentation/home.md)
- [Atributos calculados](/help/profile/computed-attributes/overview.md)
- [Destinos](/help/destinations/home.md)
- [Recopilación de datos](/help/collection/home.md)

## Obtención de datos de socios en Real-Time CDP {#get-data-in}

Para crear una audiencia de visitantes no autenticados, primero deberá introducir los datos de su socio en Real-Time CDP.

Para obtener información sobre la mejor manera de importar datos en Real-Time CDP mediante Web SDK, lea las [secciones de administración de datos y recopilación de datos de evento](./onsite-personalization.md#data-management) del caso de uso de personalización en el sitio.

## Reenvío de ID proporcionados por el socio {#bring-partner-ids-forward}

Después de importar los ID proporcionados por el socio en un conjunto de datos de evento, deberá obtener estos datos en los registros de perfil. Puede hacerlo utilizando atributos calculados.

Los atributos calculados permiten convertir rápidamente datos de comportamiento del perfil en valores agregados en el nivel de perfil. Como resultado, puede utilizar estas expresiones, como &quot;total de compra de por vida&quot; al perfil, lo que le permite utilizar fácilmente el atributo calculado dentro de sus audiencias. Encontrará más información sobre los atributos calculados en la [descripción general de los atributos calculados](/help/profile/computed-attributes/overview.md).

Para acceder a los atributos calculados, seleccione **[!UICONTROL Profiles]** seguido de **[!UICONTROL Computed attributes]** y **[!UICONTROL Create computed attribute]**.

![El botón [!UICONTROL Create computed attributes] está resaltado además de la ficha [!UICONTROL Computed attributes] en el área de trabajo [!UICONTROL Profiles].](../assets/offsite-retargeting/create-ca.png)

Aparecerá la página **[!UICONTROL Create computed attribute]**. En esta página, puede utilizar los componentes para crear el atributo calculado.

![Se muestra el área de trabajo Crear un atributo calculado.](../assets/offsite-retargeting/ca-page.png)

>[!NOTE]
>
>Para obtener información más detallada sobre la creación de atributos calculados, lea la [guía de la interfaz de usuario de atributos calculados](/help/profile/computed-attributes/ui.md).

Para este caso de uso, puede crear un atributo calculado que, si existe el ID del socio, obtenga el valor más reciente del ID del socio en las últimas 24 horas.

Con la barra de búsqueda, puede encontrar y agregar el evento &quot;Id. de socio&quot; que [creó durante el caso de uso de personalización en el sitio](#get-data-in) al lienzo de atributos calculado.

![La ficha [!UICONTROL Events] y la barra de búsqueda están resaltadas.](../assets/offsite-retargeting/ca-add-partner-id.png)

Después de agregar el evento &quot;ID de socio&quot; a la definición, establezca la condición de filtrado del evento en **[!UICONTROL Exists]**, establezca la condición de filtrado del evento en el valor **[!UICONTROL Most Recent]** del ID de socio agregado y con un período retroactivo de 24 horas.

![La definición del atributo calculado que desea crear está resaltada.](../assets/offsite-retargeting/ca-add-definition.png)

Asigne al atributo calculado un nombre adecuado (como &quot;ID de socio&quot;) y una descripción y, a continuación, seleccione **[!UICONTROL Publish]** para completar el proceso de creación del atributo calculado.

![La información básica del atributo calculado que desea crear está resaltada.](../assets/offsite-retargeting/ca-publish.png)

## Creación de una audiencia con el atributo calculado {#create-audience}

Ahora que ha creado el atributo calculado, puede utilizarlo para crear una audiencia. En este ejemplo, creará una audiencia compuesta por visitantes que visitaron su sitio web más de cinco veces este mes, pero que aún no se han registrado.

Para crear una audiencia, seleccione **[!UICONTROL Audiences]**, seguido de **[!UICONTROL Create audience]**.

![El botón [!UICONTROL Create audience] está resaltado.](../assets/offsite-retargeting/create-audience.png)

Aparece un cuadro de diálogo en el que se le pide que elija entre [!UICONTROL Compose audience] y [!UICONTROL Build rule]. Seleccione **[!UICONTROL Build rule]** seguido de **[!UICONTROL Create]**.

![El botón [!UICONTROL Build rule] está resaltado.](../assets/offsite-retargeting/select-build-rule.png)

Aparecerá la página Generador de segmentos. En esta página, puede utilizar los componentes para crear su audiencia.

![Se muestra el Generador de segmentos.](../assets/offsite-retargeting/segment-builder.png)

>[!NOTE]
>
>Para obtener información más detallada sobre el uso del Generador de segmentos, lea la [Guía de la interfaz de usuario del Generador de segmentos](/help/segmentation/ui/segment-builder.md).

Para lograr el objetivo de encontrar a estos visitantes, primero tendrá que agregar un evento **[!UICONTROL Page View]** a su audiencia. Seleccione la ficha **[!UICONTROL Events]** en **[!UICONTROL Fields]**, luego arrastre y suelte el evento **[!UICONTROL Page View]** y agréguelo al lienzo de sección de eventos.

![La ficha [!UICONTROL Events] de la sección [!UICONTROL Fields] está resaltada al mostrar el [!UICONTROL Page View]evento.](../assets/offsite-retargeting/add-page-view.png)

Seleccione el evento **[!UICONTROL Page View]** recién agregado. Cambie el período retrospectivo de **[!UICONTROL Any time]** a **[!UICONTROL This month]** y cambie la regla de evento para incluir **al menos 5**.

![Se muestran los detalles del evento [!UICONTROL Page View] agregado.](../assets/offsite-retargeting/edit-event.png)

Después de agregar el evento, debe agregar un atributo. Dado que está trabajando con visitantes no autenticados, puede agregar el atributo calculado que acaba de crear. Este atributo calculado recién creado le permite vincular ID de socios a una audiencia.

Para agregar el atributo calculado, en **[!UICONTROL Attributes]**, seleccione **[!UICONTROL XDM Individual Profile]**, seguido de **[el identificador de inquilino de su organización](/help/xdm/api/getting-started.md#know-your-tenant-id).**, **[!UICONTROL SystemComputedAttributes]** y **[!UICONTROL PartnerID]**. Ahora, agregue **[!UICONTROL Value]** del atributo calculado a la sección de atributos del lienzo.

![Se muestra la ruta de acceso a la carpeta para obtener acceso al atributo calculado.](../assets/offsite-retargeting/access-computed-attribute.png)

Además, busque **[!UICONTROL Personal Email]** y agregue el atributo **[!UICONTROL Address]** por debajo de **[!UICONTROL PartnerID]** a la sección de atributos del lienzo.

![El atributo calculado [!UICONTROL PartnerID] y el atributo [!UICONTROL Personal Email Address] aparecen resaltados en el lienzo del Generador de segmentos.](../assets/offsite-retargeting/added-attributes.png)

Ahora que ha añadido sus atributos, debe establecer sus criterios de evaluación. Para **[!UICONTROL PartnerID]**, establezca el criterio en **[!UICONTROL exists]** y para **[!UICONTROL Address]**, establezca el criterio en **[!UICONTROL does not exist]**.

![Se resaltan los valores correctos de los atributos.](../assets/offsite-retargeting/set-attribute-values.png)

Ahora ha creado correctamente una audiencia que busca visitantes de alta intensidad que tienen un ID proporcionado por el socio, pero que aún no se han registrado en el sitio. Asigne a la audiencia el nombre &quot;Redireccionamiento de usuarios no autenticados&quot; y seleccione **[!UICONTROL Save]** para terminar de crear la audiencia.

![Se resaltan las propiedades de la audiencia.](../assets/offsite-retargeting/save-audience-properties.png)

## Activación de la audiencia {#activate-audience}

Después de crear correctamente la audiencia, ahora puede activarla en destinos de flujo descendente. Seleccione **[!UICONTROL Audiences]** en el carril de navegación izquierdo, busque la audiencia recién creada, seleccione el icono de puntos suspensivos y seleccione **[!UICONTROL Activate to destination]**.

![El botón [!UICONTROL Activate to destination] está resaltado.](../assets/offsite-retargeting/activate-to-destination.png)

>[!NOTE]
>
>Todos los tipos de destino, incluidos los destinos basados en archivos, admiten la activación de audiencias con ID de socio.
>
>Para obtener más información sobre cómo activar audiencias en un destino, lea la [descripción general de la activación](/help/destinations/ui/activation-overview.md).

Aparecerá la página **[!UICONTROL Activate destination]**. En esta página, puede seleccionar a qué destino desea activar el destino. Después de seleccionar el destino elegido, seleccione **[!UICONTROL Next]**.

![El destino al que desea activar la audiencia está resaltado.](../assets/offsite-retargeting/select-destination.png)

Aparecerá la página **[!UICONTROL Scheduling]**. En esta página, puede crear una programación que determine la frecuencia con la que desea que se active la audiencia. Seleccione **[!UICONTROL Create schedule]** para crear una programación para la activación de audiencia.

![El botón [!UICONTROL Create schedule] está resaltado.](../assets/offsite-retargeting/select-create-schedule.png)

Aparece la ventana emergente [!UICONTROL Scheduling]. En esta página, puede crear la programación de activación de audiencia. Después de configurar la programación, seleccione **[!UICONTROL Create]** para continuar.

![Se muestra la ventana emergente de configuración de programación.](../assets/offsite-retargeting/configure-schedule.png)

Después de confirmar los detalles de la programación, seleccione **[!UICONTROL Next]**.

![Se muestran los detalles de la programación.](../assets/offsite-retargeting/created-schedule.png)

Aparecerá la página **[!UICONTROL Select attributes]**. En esta página, puede seleccionar qué atributos desea exportar junto con la audiencia activada. Como mínimo, debe incluir el ID de socio, ya que esto le permite identificar a los visitantes a los que planea redirigir. Seleccione **[!UICONTROL Add new mapping]** y busque el atributo calculado. Después de agregar los atributos necesarios, seleccione **[!UICONTROL Next]**.

![Tanto el botón [!UICONTROL Add new mapping] como el atributo calculado están resaltados.](../assets/offsite-retargeting/add-new-mapping.png)

Aparecerá la página **[!UICONTROL Review]**. En esta página, puede revisar los detalles de la activación de audiencia. Si está satisfecho con los detalles proporcionados, seleccione **[!UICONTROL Finish]**.

![Se muestra la página [!UICONTROL Review] con los detalles de la activación de audiencia.](../assets/offsite-retargeting/review-destination-activation.png)

Ahora ha activado una audiencia de usuarios no autenticados en un destino descendente para un nuevo objetivo.

## Otros casos de uso {#other-use-cases}

Puede explorar más casos de uso habilitados a través de la compatibilidad con datos de socios en Real-Time CDP:

- [Capte y adquiera nuevos clientes](./prospecting.md) mediante el uso de datos de socios.
- [Personalice experiencias en el sitio](./offsite-retargeting.md) con reconocimiento de visitantes ayudado por socios.
- [Complementar perfiles de origen](./supplement-first-party-profiles.md) con atributos proporcionados por el socio.
