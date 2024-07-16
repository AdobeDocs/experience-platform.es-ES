---
title: Personalice experiencias en el sitio para visitantes desconocidos mediante el reconocimiento de visitantes asistido por socios
description: Aprenda a utilizar el reconocimiento de visitantes asistido por socios para ofrecer experiencias personalizadas en el sitio a sus visitantes.
feature: Use Cases, Personalization, Customer Acquisition
exl-id: 99677988-1df8-47b1-96b1-0ef6db818a1d
source-git-commit: 5b37b51308dc2097c05b0e763293467eb12a2f21
workflow-type: tm+mt
source-wordcount: '2673'
ht-degree: 89%

---

# Personalice experiencias en el sitio para visitantes desconocidos mediante el reconocimiento de visitantes asistido por socios

>[!AVAILABILITY]
>
>Esta funcionalidad está disponible para los clientes con licencia de Real-Time CDP (servicio de aplicación), Adobe Experience Platform Activation, Real-Time CDP, Real-Time CDP Prime, Real-Time CDP Ultimate. Obtenga más información acerca de estos paquetes en las [descripciones de productos](https://helpx.adobe.com/legal/product-descriptions.html?lang=es) y póngase en contacto con el representante de Adobe para obtener más información.

Aprenda a utilizar el reconocimiento asistido por socios para ofrecer experiencias personalizadas a los visitantes de su propiedad web. Utilice este tutorial para comprender la secuencia de implementación de varios elementos en Experience Platform y otras soluciones de Experience Cloud para mostrar una experiencia personalizada a los visitantes autenticados y no autenticados.

![Una infografía que describe cómo utilizar atributos proporcionados por el socio para ofrecer experiencias personalizadas a los visitantes.](/help/rtcdp/assets/partner-data/onsite-personalization/onsite-personalization-overview.png)

## Por qué considerar este caso de uso {#why-this-use-case}

La fragmentación de experiencias digitales a medida que los consumidores interactúan con las marcas de innumerables maneras es muy real y cada vez es más difícil de resolver. Las mejores estrategias de participación del cliente para experiencias coherentes, recomendaciones segmentadas e interacciones personalizadas se ven limitadas por el reconocimiento del usuario.

Aquí es donde el reconocimiento en tiempo real asistido por socios puede marcar una diferencia significativa. El Adobe de permite a los socios de identidad conectarse a nuestra sofisticada recopilación de datos del lado del cliente y a nuestras ofertas de optimización de experiencias líderes en el mercado, para aumentar de forma eficaz el listón en la entrega de experiencias desde la primera visita en adelante, sin historial previo ni autenticación.

Esto resulta especialmente útil en verticales con tasas de autenticación bajas, como Bienes de Consumo Empaquetados, venta minorista en línea y mucho más.

## Ejemplo del sector {#industry-example}

Por ejemplo, considere una marca de mejora del hogar con tasas de autenticación bajas. Esta marca desea ofrecer experiencias personalizadas a los visitantes nuevos, sin historial ni autenticación previos y sin la menor dependencia de cookies de terceros.

Esta marca elige aprovechar la tecnología de reconocimiento de socios para reconocer probabilísticamente al visitante y ofrecer una experiencia más personalizada. Esto ayuda a avanzar en la consideración, a medida que el visitante desciende por el canal de marketing. Por ejemplo, la marca podría utilizar señales demográficas proporcionadas por el socio para el contenido en el sitio que atraiga a las personas que se han mudado recientemente y ofrezcan un descuento en productos de bricolaje populares.

## Requisitos previos y planificación {#prerequisites-and-planning}

Cuando planee utilizar atributos proporcionados por el socio para ofrecer experiencias personalizadas a sus visitantes autenticados y no autenticados, tenga en cuenta los siguientes requisitos previos en el proceso de planificación:

* ¿Qué entradas espera la tecnología de reconocimiento de su socio para que puedan aprovechar atributos adicionales?
* ¿Hasta qué punto se siente cómodo al ofrecer personalización en diferentes canales y para diferentes casos de uso basados en conjuntos de datos derivados probabilísticamente, en comparación con atributos confirmados determinísticamente?
* ¿Cómo debería cambiar la experiencia de un visitante previamente autenticado pero reconocido al autenticarse?

### Funcionalidad de la IU, componentes de Platform y productos de Experience Cloud que utilizará {#ui-functionality-and-elements}

Para implementar correctamente este caso de uso, debe utilizar varias áreas de Real-time Customer Data Platform y otras soluciones de Experience Cloud. Asegúrese de que dispone de los [permisos de control de acceso basados en atributos](/help/access-control/abac/overview.md) necesarios para todas estas áreas, o pídale al administrador del sistema que le conceda los permisos necesarios.

* Recopilación de datos
   * [SDK web de Adobe Experience Platform](/help/web-sdk/home.md)
   * [Etiquetas](/help/tags/home.md)
   * [Secuencias de datos](/help/datastreams/overview.md)
* Administración de datos en Real-Time CDP
   * [Identidades](/help/identity-service/features/namespaces.md)
   * [Esquemas](/help/xdm/home.md)
   * [Etiquetas de uso de datos](/help/data-governance/labels/overview.md)
   * [Conjuntos de datos](/help/catalog/datasets/overview.md)
* Personalización de propiedades web
   * [Segmentación de Edge](/help/segmentation/ui/edge-segmentation.md)
   * [Destinos de personalización de Edge](/help/destinations/destination-types.md#edge-personalization-destinations)
   * [Adobe Target](/help/destinations/catalog/personalization/adobe-target-connection.md) (o una plataforma de personalización de su elección. Este tutorial de caso de uso resalta Adobe Target como motor de personalización)

## Tutorial de vídeo {#video-walkthrough}

Vea el tutorial en vídeo a continuación para ver una introducción a cómo personalizar experiencias en el sitio para visitantes desconocidos:

>[!VIDEO](https://video.tv.adobe.com/v/3423076/?learn=on)

## Cómo lograr el caso de uso: información general de alto nivel {#achieve-the-use-case-high-level}

![Una infografía que describe cómo utilizar atributos proporcionados por el socio para ofrecer experiencias personalizadas a los visitantes.](/help/rtcdp/assets/partner-data/onsite-personalization/onsite-personalization-steps.png)

1. Como **cliente**, usted obtiene del **socio de datos** la capacidad de obtener perspectivas en tiempo real sobre visitantes de sitios web que, en otro caso, serían anónimos.
2. Como **cliente**, usted implementa las bibliotecas del lado del cliente en las propiedades para llamar a las API del **socio** y configura SDK web o SDK móvil para enviar señales proporcionadas por el socio a Real-Time CDP.
3. Al navegar por su sitio web o aplicación, el **visitante** es reconocido probabilísticamente por el **socio**, que devuelve atributos junto con un ID.
4. Real-Time CDP ejecuta la segmentación de Edge para evaluar las visitas de eventos entrantes y mantiene los resultados con respecto al [Identificador de ECID](https://experienceleague.adobe.com/docs/id-service/using/home.html?lang=es).
5. Adobe Target utiliza la salida de segmentación de Edge para devolver la experiencia al **visitante** para la personalización en la sesión.
6. El evento se mantiene en su totalidad para flujos de trabajo descendentes como análisis y redireccionamiento.

## Cómo lograr el caso de uso: Instrucciones paso a paso {#step-by-step-instructions}

Lea las secciones siguientes, que incluyen vínculos a documentación adicional, para completar cada uno de los pasos de la información general de alto nivel anterior.

### Administración de datos: cree un área de nombres de identidad, un esquema y un conjunto de datos para administrar atributos de datos {#data-management}

Como preparación para conseguir que el caso de uso personalice la experiencia de los visitantes no autenticados, primero debe configurar la estructura de administración de datos en Real-Time CDP para recibir los datos entrantes de cualificación de público y evento en tiempo real.

#### Crear área de nombres de identidad de ID de socio

En primer lugar, debe crear un área de nombres de identidad de ID de socio. Vaya a **[!UICONTROL Cliente]** > **[!UICONTROL Identidades]** en el carril izquierdo, y luego seleccione **[!UICONTROL Crear área de nombres de identidad]** en la esquina superior derecha de la pantalla.

![El cuadro de diálogo Crear área de nombres de identidad con ID de socio resaltado.](/help/rtcdp/assets/partner-data/onsite-personalization/create-identity-namespace.png)

Obtenga más información sobre cómo [crear un área de nombres de identidad de ID de socio](/help/rtcdp/partner-data/prospecting.md#create-partner-id-namespace).

#### Creación de un esquema

A continuación, cree un esquema de [!UICONTROL Evento de experiencia] para contener los datos de series temporales que más adelante recopilará de sus propiedades web y asegúrese de utilizar [!UICONTROL ExperienceEvent de XDM] como clase base para el esquema. Obtenga información sobre cómo [crear un esquema con la IU de Experience Platform](/help/xdm/ui/resources/schemas.md#create).

![Espacio de trabajo de esquemas con Crear esquema y evento de experiencia XDM resaltado.](/help/rtcdp/assets/partner-data/onsite-personalization/create-experience-event-schema.png)

A medida que crea su esquema y [añade grupos de campos al esquema](/help/xdm/ui/resources/schemas.md#add-field-groups), considere la posibilidad de añadir los grupos de campos [Visite la página web](/help/xdm/field-groups/event/web-details.md) y [Mapa de identidad](/help/xdm/field-groups/profile/identitymap.md). Esto se suma a otros grupos de campos que se aplican a sus prácticas de propiedad digital y recopilación de datos.

Además, puede crear o reutilizar un grupo de campos existente y añadirlo a su esquema, para capturar la información proporcionada por el socio sobre el visitante. Lea cómo [crear un grupo de campos](/help/xdm/ui/resources/field-groups.md) y cómo [añadir campos](/help/xdm/ui/resources/field-groups.md) al grupo de campos. Por ejemplo, si espera personalizar con perspectivas proporcionadas por el socio, como el intervalo de edad, el estado laboral, el poder adquisitivo mensual o los comportamientos de compra, haga que su grupo de campo incluya campos adecuados.

Suponiendo que el socio de datos proporcione un identificador estable para el visitante y que desee introducir ese identificador en Real-Time CDP, asegúrese de tener un campo con el nombre adecuado para el identificador en el grupo de campos personalizados. También debe marcar el campo como una identidad en el área de nombres de identidad que creó anteriormente. Recuerde también [permitir que el esquema se incluya en el perfil](/help/xdm/ui/resources/schemas.md#profile).

#### Crear un conjunto de datos

A continuación, debe crear un conjunto de datos para contener los datos de series temporales que recopile de los visitantes de la propiedad web y que utilizará para la personalización en el sitio.

Lea el tutorial sobre [cómo crear un conjunto de datos](/help/catalog/datasets/user-guide.md#create) y recuerde seleccionar la opción para crear el conjunto de datos a partir de un esquema. Cree el conjunto de datos en función del esquema que creó en el paso anterior.

Similar al paso para crear un esquema, debe habilitar el conjunto de datos para que se incluya en el [!UICONTROL Perfil del cliente en tiempo real]. Para obtener más información sobre cómo habilitar el conjunto de datos para utilizarlo en [!UICONTROL Perfil del cliente en tiempo real], lea el [tutorial de creación de esquemas.](/help/xdm/tutorials/create-schema-ui.md#profile)

### Implementación de la recopilación de datos de evento en la propiedad web {#implement-data-collection}

Después de ajustar la configuración de administración de datos, ahora debe implementar la [recopilación de datos](/help/collection/home.md) de evento en tiempo real en la propiedad web. Debe instrumentar la propiedad con la biblioteca de recopilación de datos de Adobe: [!UICONTROL SDK web]: para recopilar llamadas de evento en tiempo real y enviarlas de vuelta a Real-Time CDP. Este elemento consta de algunas tareas independientes entre varios componentes de recopilación de datos.

>[!IMPORTANT]
>
>Para recuperar los atributos proporcionados por el socio, también debe *integrar su propiedad web con las API de socios u otros métodos para llamar y recuperar atributos de socios de datos en tiempo real*. Hable de este aspecto con su socio preferido, ya que no es objeto de este tutorial.

En primer lugar, utilice el conmutador de aplicaciones en la esquina superior derecha de la pantalla para navegar hasta la sección **[!UICONTROL Recopilación de datos]**.

>[!TIP]
>
>Póngase en contacto con el administrador del sistema para solicitar acceso si no puede ver [!UICONTROL Recopilación de datos] en el conmutador de aplicaciones.

![Cambiar aplicación para llegar a la sección de recopilación de datos.](/help/rtcdp/assets/partner-data/onsite-personalization/app-switcher-data-collection.png)

La sección **[!UICONTROL Recopilación de datos]** de la interfaz de usuario tiene un aspecto similar al de la siguiente imagen.

![Sección de recopilación de datos de la IU de Platform.](/help/rtcdp/assets/partner-data/onsite-personalization/data-collection-home.png)

#### Crear secuencia de datos

Como primer paso en la sección de recopilación de datos, [cree una nueva secuencia de datos](/help/datastreams/configure.md). La secuencia de datos es la base de cómo se recopilan los datos y se enrutan correctamente a la aplicación de Adobe correcta, en este caso Experience Platform.

A medida que crea la secuencia de datos, en el campo **[!UICONTROL Esquema del evento]**, seleccione el esquema que creó anteriormente.

![El selector de esquema de eventos se resalta al configurar una nueva secuencia de datos.](/help/rtcdp/assets/partner-data/onsite-personalization/event-schema-selector-datastream.png)

[Seleccione el conjunto de datos de evento](/help/datastreams/configure.md#aep) que ha creado anteriormente desde la lista desplegable, marque las casillas junto a **[!UICONTROL Segmentación de Edge]** y **[!UICONTROL Destinos de personalización]** y seleccione **[!UICONTROL Guardar]**.

Tenga en cuenta que no tiene que seleccionar un conjunto de datos de perfil en este escenario, ya que está trayendo datos de series temporales basados en eventos.

#### Crear propiedad de etiqueta

Una propiedad es un contenedor que se rellena con extensiones, reglas, elementos de datos y bibliotecas mientras se implementan etiquetas en el sitio.

Vaya a **[!UICONTROL Etiquetas]** y seleccione **[!UICONTROL Nueva propiedad]**.

![Creación de una etiqueta nueva.](/help/rtcdp/assets/partner-data/onsite-personalization/create-tag-property.png)

Rellene los campos obligatorios y seleccione **[!UICONTROL Guardar]**.

![Rellene los campos obligatorios para la nueva propiedad.](/help/rtcdp/assets/partner-data/onsite-personalization/tag-property-fields.png)

Obtenga información completa sobre cómo [crear una propiedad de etiqueta](https://experienceleague.adobe.com/docs/platform-learn/implement-in-websites/configure-tags/create-a-property.html).

A continuación, debe instalar varias extensiones dentro de la propiedad. Seleccione la propiedad de etiquetas y vaya a la sección [!UICONTROL Extensiones].

![Seleccione la nueva propiedad de etiquetas.](/help/rtcdp/assets/partner-data/onsite-personalization/select-tag-property.png)

Observe que la extensión [!UICONTROL Núcleo] ya está instalada. Debe instalar dos extensiones adicionales, como se detalla en las secciones siguientes.

![Ver extensiones instaladas.](/help/rtcdp/assets/partner-data/onsite-personalization/view-existing-extensions.png)

#### Instalar extensión de SDK web

Tenga en cuenta que este tutorial indica cómo puede instrumentar el sitio web con el SDK web. También puede utilizar [SDK Mobile](https://developer.adobe.com/client-sdks/documentation/) en la aplicación para personalizar la experiencia de los visitantes de la aplicación.

![Vista de la extensión del SDK web en el catálogo de extensiones.](/help/rtcdp/assets/partner-data/onsite-personalization/web-sdk-extension.png)

En la pantalla para configurar el SDK web, vaya a la sección **[!UICONTROL Secuencias de datos]** y proporcione información sobre la zona protegida de Experience Platform que está utilizando. Seleccione la zona protegida adecuada y la secuencia de datos creada en los pasos anteriores en el menú desplegable siguiente. Puede elegir los mismos valores de zona protegida y de secuencia de datos para todos los demás entornos. Deje el resto de configuraciones sin cambios y seleccione **[!UICONTROL Guardar]**.

Obtenga información completa sobre [cómo instalar el SDK web](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/tags-configuration/install-web-sdk.html).

#### Instalar extensión del servicio de ID

Utilice la [Extensión del servicio de ID de Experience Cloud](/help/tags/extensions/client/id-service/overview.md) para crear una identidad de origen única basada en dispositivos para los visitantes de todas las soluciones de Experience Cloud. Busque **[!UICONTROL Servicio de ID]** en el catálogo de extensiones e instálelo. Mantenga todos los ajustes predeterminados al instalar la extensión.

![Vista de la extensión del servicio de ID en el catálogo de extensiones.](/help/rtcdp/assets/partner-data/onsite-personalization/id-service-extension.png)

#### Configuración de entornos

A continuación, diríjase a la sección **[!UICONTROL Entornos]** en la navegación a la izquierda. En este paso, debe conectar el sitio web a la red de Adobe Edge para recuperar y entregar la información del visitante en tiempo real.

Seleccione el icono de cuadro de la derecha para el entorno de desarrollo y copie la versión estándar del fragmento de código JavaScript que aparece en una ventana modal.

![Seleccione el icono de cuadro resaltado en la sección Entornos de la IU de recopilación de datos.](/help/rtcdp/assets/partner-data/onsite-personalization/select-box-icon.png)

Debe agregar este fragmento de código a la parte superior del sitio web. Como resultado, el sitio web realizará una llamada a la red de Adobe Edge para recuperar la lógica de JavaScript que se cargará y ejecutará en la página. Esto permite que funcionen funcionalidades como la generación de ID de visitante, la recopilación de datos y la personalización de experiencias en tiempo real.

#### Configuración de elementos de datos

Los elementos de datos son los componentes básicos del diccionario de datos (o mapa de datos). Un solo elemento de datos es una variable cuyo valor puede asignarse a cadenas de consulta, URL, valores de cookies, variables JavaScript, etc. Más información sobre [elementos de datos](/help/tags/ui/managing-resources/data-elements.md).

Para los fines de este caso de uso, debe configurar dos elementos de datos.

En primer lugar, configure un elemento `partnerData`. Vaya a la sección **[!UICONTROL Elementos de datos]** y seleccione **[!UICONTROL Crear nuevo elemento de datos]**.

![Crear un nuevo elemento de datos.](/help/rtcdp/assets/partner-data/onsite-personalization/create-data-element.gif)

Asigne un nombre al elemento de datos `partnerData`, deje el valor de la [!UICONTROL extensión] como [!UICONTROL núcleo], y establezca el **[!UICONTROL tipo de elemento de datos]** como **[!UICONTROL variable JavaScript]**. Introduzca `partnerData` en el campo titulado **[!UICONTROL Nombre de variable JavaScript]** y seleccione **[!UICONTROL Guardar]**.

![Selecciones resaltadas para configurar correctamente el elemento de datos partnerData.](/help/rtcdp/assets/partner-data/onsite-personalization/create-partnerdata-data-element.png)

Para configurar el segundo elemento de datos, asigne el nombre `pageVisit` a la nueva variable, configure la **[!UICONTROL Extensión]** en **[!UICONTROL Adobe Experience Platform]** y elija **[!UICONTROL Objeto XDM]** como el tipo de datos.

![Selecciones resaltadas para configurar correctamente el elemento de datos pageVisit.](/help/rtcdp/assets/partner-data/onsite-personalization/page-visit-data-element.png)

En el esquema, seleccione los atributos de terceros que corresponden a los valores que espera del socio de datos. A continuación, seleccione el botón de opción denominado **[!UICONTROL Proporcionar todo el objeto]**. Seleccione el icono que parece una base de datos y elija el elemento de datos `partnerData` que ha creado anteriormente.

#### Configuración de las reglas

En la sección **[!UICONTROL Reglas]**, puede configurar el sitio web para enviar una solicitud de personalización a Adobe con los atributos cargados en los elementos de datos que acaba de crear. Más información sobre [creación de reglas](/help/tags/ui/managing-resources/rules.md).

Seleccione **[!UICONTROL Crear nueva regla]**. Asigne un nombre a esta regla **[!UICONTROL Personalizar]** y seleccione el signo + situado junto a **[!UICONTROL Eventos]**. Seleccionar **[!UICONTROL Inferior de la página]** como el evento y guarde.

![Selecciones para la parte de tipo de evento de una regla.](/help/rtcdp/assets/partner-data/onsite-personalization/add-events-rule.png)

Seleccione el signo + situado junto a **[!UICONTROL Acciones]**. Actualice la extensión a **[!UICONTROL SDK web de Adobe Experience Platform]** y establezca **[!UICONTROL Tipo de acción]** en **[!UICONTROL Enviar evento]**.

![Selecciones para la parte de tipo de acción de una regla.](/help/rtcdp/assets/partner-data/onsite-personalization/add-action-rule.png)

Desde el selector desplegable **[!UICONTROL Tipo]** de la derecha, seleccione `web.webpagedetails.pageViews` como el tipo de evento.

![Seleccione tipo de evento.](/help/rtcdp/assets/partner-data/onsite-personalization/add-pageview-type-rule.png)

Seleccione el icono de base de datos junto a los datos XDM y el elemento de datos `pageVisit`.

Desplácese hacia abajo por la lista de configuraciones de acción y asegúrese de marcar la casilla titulada **[!UICONTROL Procesar decisiones de personalización visuales]**. Esto es importante para permitir que las experiencias entregadas mediante Adobe Target u otros productos similares se representen visualmente en la página web. Seleccione **[!UICONTROL Conservar cambios]** y luego **[!UICONTROL Guardar]** la regla.

![Seleccione la casilla de verificación Procesar decisiones de personalización visual.](/help/rtcdp/assets/partner-data/onsite-personalization/render-visual-personalization-toggle.png)

#### Configurar el flujo de trabajo de publicación

Para implementar esta configuración en la página web, el siguiente paso es crear una biblioteca que incluya los recursos que acaba de crear. Más información sobre [configuración de un flujo de publicaciones](/help/tags/ui/publishing/publishing-flow.md).

Seleccionar **[!UICONTROL Flujo de publicaciones]** y luego **[!UICONTROL Añadir biblioteca]**.

Seleccione **[!UICONTROL Añadir todos los recursos modificados]**, asigne un nombre a la biblioteca y establezca el entorno en **[!UICONTROL Desarrollo]** y seleccione **[!UICONTROL Guardar y generar en desarrollo]**.

![Crear biblioteca e implementarla en el entorno de desarrollo](/help/rtcdp/assets/partner-data/onsite-personalization/create-publishing-workflow.gif)

#### Prueba del sitio web

En este punto, el sitio web debe estar completamente instrumentado con el SDK web. Para probar que la recopilación de datos funciona según lo esperado, puede navegar al sitio web y utilizar las herramientas para desarrolladores del explorador para inspeccionar el tráfico de red.

Introduzca `interact` en el cuadro de búsqueda, actualice la página y debería ver las llamadas de red desde el sitio web a la red de Adobe Edge que se rellena.

![Vista de los eventos de red que se rellenan en las herramientas para desarrolladores.](/help/rtcdp/assets/partner-data/onsite-personalization/events-filtered.png)

### Personalización {#personalization}

Ya está listo para crear y activar públicos para su personalización.

#### Creación de audiencias y configuración de la segmentación de Edge

En la interfaz de usuario de Platform, vaya a **[!UICONTROL Cliente]** > **[!UICONTROL Audiencias]** y cree una audiencia para capturar a los visitantes del sitio web.

![Vista de cómo navegar a las audiencias.](/help/rtcdp/assets/partner-data/onsite-personalization/navigate-to-audiences.png)

Debe configurar su audiencia con [segmentación de Edge](/help/segmentation/ui/edge-segmentation.md) para que la pertenencia a audiencias de sus visitantes se evalúe en tiempo real cuando visiten su propiedad web.

Asegúrese de configurar también [políticas de combinación activas en el perímetro](/help/destinations/ui/activate-edge-personalization-destinations.md#create-merge-policy) para los públicos de perímetro.

#### Integración con Adobe Target u otro destino de personalización personalizado

Ya está listo para integrarse con un motor de personalización para mostrar contenido personalizado a los visitantes de su sitio web o aplicación. Adobe recomienda utilizar el destino [Adobe Target](/help/destinations/catalog/personalization/adobe-target-connection.md) con este fin.

>[!IMPORTANT]
>
>Lea el tutorial sobre [activación de públicos en destinos de personalización de perímetro](/help/destinations/ui/activate-edge-personalization-destinations.md) para obtener una vista completa de los pasos necesarios para activar los públicos.

## Limitaciones y solución de problemas {#limitations-and-troubleshooting}

Tenga en cuenta las siguientes limitaciones a medida que explora el caso de uso descrito en esta página:

* Si decide utilizar ID de socios, tenga en cuenta que estos no se utilizan para crear su [gráfico de identidad](/help/identity-service/features/identity-graph-viewer.md).

## Otros casos de uso obtenidos mediante la compatibilidad con datos de socios {#other-use-cases}

Explore más casos de uso habilitados a través de la compatibilidad con datos de socios en Real-Time CDP:

* [Complemente perfiles de origen con atributos de socios de datos de confianza para mejorar la base de datos, obtener nueva información sobre la base de clientes y optimizar mejor los públicos.](/help/rtcdp/partner-data/supplement-first-party-profiles.md)
* Utilice la compatibilidad con datos de terceros en Real-Time CDP para [ampliar su base de perfiles con perfiles potenciales de socios de datos y participe con ellos para adquirir o llegar a nuevos clientes](/help/rtcdp/partner-data/prospecting.md).
* [Se ha ampliado la activación de perfiles y audiencias de clientes potenciales](/help/destinations/ui/activate-prospect-audiences.md) para seleccionar destinos.
