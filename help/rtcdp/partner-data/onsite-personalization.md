---
title: Utilice el reconocimiento de visitantes asistido por socios para personalizar experiencias in situ
description: Aprenda a utilizar el reconocimiento de visitantes asistido por socios para ofrecer experiencias personalizadas en el sitio a sus visitantes.
hide: true
hidefromtoc: true
source-git-commit: f63cddc1158e739ce26e0ce1d3d54b491bd80c06
workflow-type: tm+mt
source-wordcount: '2493'
ht-degree: 7%

---

# Utilice el reconocimiento de visitantes asistido por socios para personalizar las experiencias en el sitio

Aprenda a utilizar el reconocimiento asistido por socios para ofrecer experiencias personalizadas a los visitantes de su propiedad web. Utilice este tutorial para comprender la secuencia de implementación de varios elementos en Experience Platform y otras soluciones de Experience Cloud para mostrar una experiencia personalizada a los visitantes autenticados y no autenticados.

![Una infografía que describe cómo utilizar atributos proporcionados por el socio para ofrecer experiencias personalizadas a los visitantes.](/help/rtcdp/assets/partner-data/onsite-personalization/onsite-personalization-steps.png)

## Ejemplo del sector {#industry-example}

Por ejemplo, considere una marca de mejora del hogar con tasas de autenticación bajas. Esta marca desea ofrecer experiencias personalizadas a los visitantes nuevos, sin historial ni autenticación previos y sin la menor dependencia de cookies de terceros.

Esta marca elige aprovechar la tecnología de reconocimiento de socios para reconocer probabilísticamente al visitante y ofrecer una experiencia más personalizada. Esto ayuda a avanzar en la consideración, a medida que el visitante desciende por el canal de marketing. Por ejemplo, la marca podría utilizar señales demográficas proporcionadas por el socio para el contenido en el sitio que atraiga a las personas que se han mudado recientemente y ofrezcan un descuento en productos de bricolaje populares.

## Requisitos previos y planificación {#prerequisites-and-planning}

Cuando planee utilizar atributos proporcionados por el socio para ofrecer experiencias personalizadas a sus visitantes autenticados y no autenticados, tenga en cuenta los siguientes requisitos previos en el proceso de planificación:

* ¿Qué entradas espera la tecnología de reconocimiento de su socio para que puedan aprovechar atributos adicionales?
* ¿Hasta qué punto se siente cómodo al ofrecer personalización en diferentes canales y para diferentes casos de uso basados en atributos derivados probabilísticamente, en comparación con atributos confirmados determinísticamente?
* ¿Cómo debería cambiar la experiencia de un visitante previamente autenticado pero reconocido al autenticarse?

### Funcionalidad de la interfaz de usuario, componentes de Platform y productos de Experience Cloud que utilizará {#ui-functionality-and-elements}

Para implementar correctamente este caso de uso, debe utilizar varias áreas de Real-time Customer Data Platform y otras soluciones de Experience Cloud. Asegúrese de que dispone de lo necesario [permisos de control de acceso basados en atributos](/help/access-control/abac/overview.md) para todas estas áreas, o pídale al administrador del sistema que le conceda los permisos necesarios.

* Recopilación de datos
   * [SDK web de Adobe Experience Platform](/help/edge/home.md)
   * [Etiquetas](/help/tags/home.md)
   * [Corrientes de datos](/help/datastreams/overview.md)
* Administración de datos en Real-Time CDP
   * [Identidades](/help/identity-service/namespaces.md)
   * [Esquemas](/help/xdm/home.md)
   * [Etiquetas de uso de datos](/help/data-governance/labels/overview.md)
   * [Conjuntos de datos](/help/catalog/datasets/overview.md)
* Personalización de propiedades web
   * [Segmentación de Edge](/help/segmentation/ui/edge-segmentation.md)
   * [Destinos de personalización de Edge](/help/destinations/destination-types.md#edge-personalization-destinations)
   * [Adobe Target](/help/destinations/catalog/personalization/adobe-target-connection.md) (o una plataforma de personalización de su elección. Este tutorial de caso de uso resalta Adobe Target como motor de personalización)

## Cómo lograr el caso de uso: información general de alto nivel {#achieve-the-use-case-high-level}

![Una infografía que describe cómo utilizar atributos proporcionados por el socio para ofrecer experiencias personalizadas a los visitantes.](/help/rtcdp/assets/partner-data/onsite-personalization/onsite-personalization-steps.png)

1. As a **cliente**, su licencia de **socio de datos** la capacidad de obtener perspectivas en tiempo real en visitantes de sitios web que, de lo contrario, serían anónimos.
2. As a **cliente**, las bibliotecas del lado del cliente se implementan en las propiedades para llamar a **socio** Las API se configuran como SDK web o SDK móvil para enviar señales proporcionadas por el socio a Real-Time CDP.
3. Al navegar por su sitio web o aplicación, la variable **visitante** es reconocido probabilísticamente por el **socio**, que devuelve atributos junto con un ID.
4. Real-Time CDP ejecuta la segmentación de Edge para evaluar las visitas de eventos entrantes y mantiene los resultados con respecto al [Identificador de ECID](https://experienceleague.adobe.com/docs/id-service/using/home.html?lang=es).
5. Adobe Target utiliza la salida de segmentación de Edge para devolver la experiencia al **visitante** para la personalización en la sesión.
6. El evento se mantiene en su totalidad para flujos de trabajo descendentes como análisis y redireccionamiento.

## Cómo lograr el caso de uso: Instrucciones paso a paso {#step-by-step-instructions}

Lea las secciones siguientes, que incluyen vínculos a documentación adicional, para completar cada uno de los pasos de la información general de alto nivel anterior.

### Administración de datos: cree un área de nombres de identidad, un esquema y un conjunto de datos para administrar atributos de datos {#data-management}

Como preparación para conseguir que el caso de uso personalice la experiencia de los visitantes no autenticados, primero debe configurar la estructura de administración de datos en Real-Time CDP para recibir los datos entrantes de cualificación de audiencia y evento en tiempo real.

#### Crear área de nombres de identidad de ID de socio

En primer lugar, debe crear un área de nombres de identidad de ID de socio. Vaya a **[!UICONTROL Cliente]** > **[!UICONTROL Identidades]** en el carril izquierdo, y luego seleccione **[!UICONTROL Crear área de nombres de identidad]** en la esquina superior derecha de la pantalla.

![El cuadro de diálogo Crear área de nombres de identidad con ID de socio resaltado.](/help/rtcdp/assets/partner-data/onsite-personalization/create-identity-namespace.png)

Obtenga más información sobre cómo [crear un área de nombres de identidad de ID de socio](/help/rtcdp/partner-data/prospecting.md#create-partner-id-namespace).

#### Creación de un esquema

A continuación, cree un [!UICONTROL Evento de experiencia] para contener los datos de series temporales que más adelante recopilará de sus propiedades web y asegúrese de utilizar [!UICONTROL ExperienceEvent de XDM] como clase base para el esquema. Obtenga información sobre cómo [creación de un esquema con la interfaz de usuario de Experience Platform](/help/xdm/ui/resources/schemas.md#create).

![Espacio de trabajo de esquemas con Crear esquema y evento de experiencia XDM resaltado.](/help/rtcdp/assets/partner-data/onsite-personalization/create-experience-event-schema.png)

A medida que crea su esquema y [añadir grupos de campos al esquema](/help/xdm/ui/resources/schemas.md#add-field-groups), considere la posibilidad de añadir el [Visite la página web](/help/xdm/field-groups/event/web-details.md) y [Mapa de identidad](/help/xdm/field-groups/profile/identitymap.md) grupos de campos. Esto se suma a otros grupos de campos que se aplican a sus prácticas de propiedad digital y recopilación de datos.

Además, puede crear o reutilizar un grupo de campos existente y añadirlo a su esquema para capturar la información proporcionada por el socio sobre el visitante. Lea cómo [creación de un grupo de campos](/help/xdm/ui/resources/field-groups.md) y cómo [añadir campos](/help/xdm/ui/resources/field-groups.md) al grupo de campos. Por ejemplo, si espera personalizar con perspectivas proporcionadas por el socio, como el intervalo de edad, el estado laboral, el poder adquisitivo mensual o los comportamientos de compra, haga que su grupo de campo incluya campos adecuados.

Suponiendo que el socio de datos proporcione un identificador estable para el visitante y que desee introducir ese identificador en Real-Time CDP, asegúrese de tener un campo con el nombre adecuado para el identificador en el grupo de campos personalizados. También debe marcar el campo como una identidad en el área de nombres de identidad que creó anteriormente. Recuerde también [permitir que el esquema se incluya en el perfil](/help/xdm/ui/resources/schemas.md#profile).

#### Crear un conjunto de datos

A continuación, debe crear un conjunto de datos para contener los datos de series temporales que recopile de los visitantes de la propiedad web y que utilizará para la personalización en el sitio.

Lea el tutorial sobre [cómo crear un conjunto de datos](/help/catalog/datasets/user-guide.md#create) y recuerde seleccionar la opción para crear el conjunto de datos a partir de un esquema. Cree el conjunto de datos en función del esquema que creó en el paso anterior.

Similar al paso para crear un esquema, debe habilitar el conjunto de datos para que se incluya en el [!UICONTROL Perfil del cliente en tiempo real]. Para obtener más información sobre cómo habilitar el conjunto de datos para utilizarlo en [!UICONTROL Perfil del cliente en tiempo real], lea la [tutorial de creación de esquemas.](/help/xdm/tutorials/create-schema-ui.md#profile)

### Implementación de la recopilación de datos de evento en la propiedad web {#implement-data-collection}

Después de configurar la configuración de gestión de datos, ahora debe implementar un evento en tiempo real [recopilación de datos](/help/collection/home.md) en la propiedad web. Debe instrumentar la propiedad con la biblioteca de recopilación de datos de Adobe: [!UICONTROL SDK web] : para recopilar llamadas de evento en tiempo real y enviarlas de vuelta a Real-Time CDP. Este elemento consta de algunas tareas independientes entre varios componentes de recopilación de datos.

>[!IMPORTANT]
>
>Para recuperar los atributos proporcionados por el socio, también debe *integre su propiedad web con las API de socios u otros métodos para llamar y recuperar atributos de socios de datos en tiempo real*. Hable de este aspecto con su pareja preferida, ya que no es objeto de este tutorial.

En primer lugar, utilice el conmutador de aplicaciones en la esquina superior derecha de la pantalla para navegar hasta el **[!UICONTROL Recopilación de datos]** sección.

>[!TIP]
>
>Póngase en contacto con el administrador del sistema para solicitar acceso si no puede ver [!UICONTROL Recopilación de datos] en el conmutador de aplicaciones.

![Cambiar aplicación para llegar a la sección de recopilación de datos.](/help/rtcdp/assets/partner-data/onsite-personalization/app-switcher-data-collection.png)

El **[!UICONTROL Recopilación de datos]** de la interfaz de usuario tiene un aspecto similar al de la siguiente imagen.

![Sección de recopilación de datos de la IU de Platform.](/help/rtcdp/assets/partner-data/onsite-personalization/data-collection-home.png)

#### Crear secuencia de datos

Como primer paso en la sección de recopilación de datos, [crear una nueva secuencia de datos](/help/datastreams/configure.md). La secuencia de datos es la base de cómo se recopilan los datos y se enrutan correctamente a la aplicación de Adobe correcta, en este caso el Experience Platform.

A medida que crea el conjunto de datos, en la variable **[!UICONTROL Esquema del evento]** , seleccione el esquema que creó anteriormente.

![El selector de esquema de eventos se resalta al configurar una nueva secuencia de datos.](/help/rtcdp/assets/partner-data/onsite-personalization/event-schema-selector-datastream.png)

[Seleccione el conjunto de datos de evento](/help/datastreams/configure.md#aep) que ha creado anteriormente desde la lista desplegable, marque las casillas junto a **[!UICONTROL Segmentación de Edge]** y **[!UICONTROL Destinos de personalización]** y seleccione **[!UICONTROL Guardar]**.

Tenga en cuenta que no tiene que seleccionar un conjunto de datos de perfil en este escenario, ya que está trayendo datos de series temporales basados en eventos.

#### Crear propiedad de etiqueta

Considere una propiedad como un contenedor que se rellena con extensiones, reglas, elementos de datos y bibliotecas al implementar etiquetas en el sitio.

Vaya a **[!UICONTROL Etiquetas]** y seleccione **[!UICONTROL Nueva propiedad]**.

![Cree una nueva propiedad de etiqueta.](/help/rtcdp/assets/partner-data/onsite-personalization/create-tag-property.png)

Rellene los campos obligatorios y seleccione **[!UICONTROL Guardar]**.

![Rellene los campos obligatorios para la nueva propiedad.](/help/rtcdp/assets/partner-data/onsite-personalization/tag-property-fields.png)

Obtenga información completa sobre cómo [crear una propiedad de etiqueta](https://experienceleague.adobe.com/docs/platform-learn/implement-in-websites/configure-tags/create-a-property.html).

A continuación, debe instalar varias extensiones dentro de la propiedad. Seleccione la propiedad de etiquetas y vaya a [!UICONTROL Extensiones] sección.

![Seleccione la nueva propiedad de etiquetas.](/help/rtcdp/assets/partner-data/onsite-personalization/select-tag-property.png)

Observe que la variable [!UICONTROL Núcleo] La extensión de ya está instalada. Debe instalar dos extensiones adicionales, como se detalla en las secciones siguientes.

![Ver extensiones instaladas.](/help/rtcdp/assets/partner-data/onsite-personalization/view-existing-extensions.png)

#### Instalación de la extensión del SDK web

Tenga en cuenta que este tutorial indica cómo puede instrumentar el sitio web con el SDK web. También puede utilizar [Mobile SDK](https://developer.adobe.com/client-sdks/documentation/) en la aplicación para personalizar la experiencia a los visitantes de la aplicación.

![Vista de la extensión del SDK web en el catálogo de extensiones.](/help/rtcdp/assets/partner-data/onsite-personalization/web-sdk-extension.png)

En la pantalla para configurar el SDK web, vaya a **[!UICONTROL Datastreams]** y proporcione información sobre la zona protegida de Experience Platform que está utilizando. Seleccione el simulador para pruebas adecuado y la secuencia de datos creada en los pasos anteriores en el menú desplegable siguiente. Puede elegir los mismos valores de zona protegida y de secuencia de datos para todos los demás entornos. Deje el resto de configuraciones sin cambios y seleccione **[!UICONTROL Guardar]**.

Obtenga información completa sobre [cómo instalar el SDK web](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/tags-configuration/install-web-sdk.html).

#### Instalar extensión del servicio de ID

Utilice el [Extensión del servicio de ID de Experience Cloud](/help/tags/extensions/client/id-service/overview.md) para crear una identidad de origen única basada en dispositivos para los visitantes de todas las soluciones de Experience Cloud. Buscar por **[!UICONTROL Servicio de ID]** en el catálogo de extensiones e instálelo. Mantenga todos los ajustes predeterminados al instalar la extensión.

![Vista de la extensión del servicio de ID en el catálogo de extensiones.](/help/rtcdp/assets/partner-data/onsite-personalization/id-service-extension.png)

#### Configuración de entornos

A continuación, diríjase al **[!UICONTROL Entornos]** de la navegación por la izquierda. En este paso, debe conectar el sitio web a la red de Adobe Edge para recuperar y entregar la información del visitante en tiempo real.

Seleccione el icono de cuadro de la derecha para el entorno de desarrollo y copie la versión estándar del fragmento de código JavaScript que aparece en una ventana modal.

![Seleccione el icono de cuadro resaltado en la sección Entornos de la IU de recopilación de datos.](/help/rtcdp/assets/partner-data/onsite-personalization/select-box-icon.png)

Debe agregar este fragmento de código a la parte superior del sitio web. Como resultado, el sitio web realizará una llamada a la red de Adobe Edge para recuperar la lógica de JavaScript que se cargará y ejecutará en la página. Esto permite que funcionen funcionalidades como la generación de ID de visitante, la recopilación de datos y la personalización de experiencias en tiempo real.

#### Configuración de elementos de datos

Los Data Elements son los componentes básicos del diccionario de datos (o mapa de datos). Un solo elemento de datos es una variable cuyo valor puede asignarse a cadenas de consulta, URL, valores de cookies, variables JavaScript, etc. Más información sobre [elementos de datos](/help/tags/ui/managing-resources/data-elements.md).

Para los fines de este caso de uso, debe configurar dos elementos de datos.

En primer lugar, configure un `partnerData` Elemento. Vaya a **[!UICONTROL Elementos de datos]** y seleccione **[!UICONTROL Crear nuevo elemento de datos]**.

![Crear un nuevo elemento de datos.](/help/rtcdp/assets/partner-data/onsite-personalization/create-data-element.gif)

Asignar un nombre al elemento de datos `partnerData`, deje el [!UICONTROL extensión] valor como [!UICONTROL Núcleo]y establezca **[!UICONTROL Tipo de elemento de datos]** as **[!UICONTROL Variable JavaScript]**. Entrar `partnerData` en el campo titulado **[!UICONTROL Nombre de variable JavaScript]** y seleccione **[!UICONTROL Guardar]**.

![Selecciones resaltadas para configurar correctamente el elemento de datos partnerData.](/help/rtcdp/assets/partner-data/onsite-personalization/create-partnerdata-data-element.png)

Para configurar el segundo elemento de datos, asigne un nombre a la nueva variable `pageVisit`, configure el **[!UICONTROL Extensión]** hasta **[!UICONTROL Adobe Experience Platform]** y elija **[!UICONTROL Objeto XDM]** como el tipo de datos.

![Selecciones resaltadas para configurar correctamente el elemento de datos pageVisit.](/help/rtcdp/assets/partner-data/onsite-personalization/page-visit-data-element.png)

En el esquema, seleccione los atributos de terceros que corresponden a los valores que espera del socio de datos. A continuación, seleccione el botón de opción denominado **[!UICONTROL Proporcionar todo el objeto]**. Seleccione el icono que parece una base de datos y elija el `partnerData` Elemento de datos que ha creado anteriormente.

#### Configuración de reglas

En el **[!UICONTROL Reglas]** , puede configurar el sitio web para enviar una solicitud de personalización al Adobe con los atributos cargados en los elementos de datos que acaba de crear. Más información sobre [creación de reglas](/help/tags/ui/managing-resources/rules.md).

Seleccionar **[!UICONTROL Crear nueva regla]**. Asignar un nombre a esta regla **[!UICONTROL Personalizar]** y seleccione el signo + situado junto a **[!UICONTROL Eventos]**. Seleccionar **[!UICONTROL Page Bottom]** como el evento y guarde.

![Selecciones para la parte de tipo de evento de una regla.](/help/rtcdp/assets/partner-data/onsite-personalization/add-events-rule.png)

Seleccione el signo + situado junto a **[!UICONTROL Acciones]**. Actualice la extensión a **[!UICONTROL SDK web de Adobe Experience Platform]** y establecer **[!UICONTROL Tipo de acción]** hasta **[!UICONTROL Enviar evento]**.

![Selecciones para la parte de tipo de acción de una regla.](/help/rtcdp/assets/partner-data/onsite-personalization/add-action-rule.png)

Desde el **[!UICONTROL Tipo]** selector desplegable de la derecha, seleccione `web.webpagedetails.pageViews` como el tipo de evento.

![Seleccione el tipo de evento.](/help/rtcdp/assets/partner-data/onsite-personalization/add-pageview-type-rule.png)

Seleccione el icono de base de datos junto a los datos XDM y seleccione la opción `pageVisit` elemento de datos.

Desplácese hacia abajo por la lista de configuraciones de acción y asegúrese de marcar la casilla titulada **[!UICONTROL Procesar decisiones de personalización visuales]**. Esto es importante para permitir que las experiencias entregadas mediante Adobe Target u otros productos similares se representen visualmente en la página web. Seleccionar **[!UICONTROL Conservar cambios]**, y luego **[!UICONTROL Guardar]** la regla.

![Seleccione la casilla de verificación Procesar decisiones de personalización visual.](/help/rtcdp/assets/partner-data/onsite-personalization/render-visual-personalization-toggle.png)

#### Configurar el flujo de trabajo de publicación

Para implementar esta configuración en la página web, el siguiente paso es crear una biblioteca que incluya los recursos que acaba de crear. Más información sobre [configuración de un flujo de publicación](/help/tags/ui/publishing/publishing-flow.md).

Seleccionar **[!UICONTROL Flujo de publicación]** y luego **[!UICONTROL Añadir biblioteca]**.

Seleccionar **[!UICONTROL Añadir todos los recursos modificados]**, asigne un nombre a la biblioteca y establezca el entorno en **[!UICONTROL Desarrollo]** y seleccione **[!UICONTROL Guardar y generar en desarrollo]**.

![Crear biblioteca e implementar en el entorno de desarrollo](/help/rtcdp/assets/partner-data/onsite-personalization/create-publishing-workflow.gif)

#### Prueba del sitio web

En este punto, el sitio web debe estar completamente instrumentado con el SDK web. Para probar que la recopilación de datos funciona según lo esperado, puede navegar al sitio web y utilizar las herramientas para desarrolladores del explorador para inspeccionar el tráfico de red.

Entrada `interact` en el cuadro de búsqueda, actualice la página y debería ver las llamadas de red desde el sitio web a la red de Adobe Edge que se rellena.

![Vista de los eventos de red que se rellenan en las herramientas para desarrolladores.](/help/rtcdp/assets/partner-data/onsite-personalization/events-filtered.png)

### Personalización {#personalization}

Ya está listo para crear y activar audiencias para su personalización.

#### Configuración de la segmentación de Edge

Configuración de [segmentación de borde](/help/segmentation/ui/edge-segmentation.md) por lo tanto, la pertenencia a audiencias de los visitantes se evalúa en tiempo real a medida que visitan el dominio web.

Asegúrese de configurar también un [política de combinación activa en el perímetro](/help/destinations/ui/activate-edge-personalization-destinations.md#create-merge-policy) para las audiencias de edge.

#### Integración con Adobe Target u otro destino de personalización personalizado

Ya está listo para integrarse con un motor de personalización para mostrar contenido personalizado a los visitantes de su sitio web o aplicación. El Adobe recomienda utilizar la variable [Adobe Target destination](/help/destinations/catalog/personalization/adobe-target-connection.md) con este fin.

>[!IMPORTANT]
>
>Lea el tutorial sobre [activación de audiencias en destinos de personalización de edge](/help/destinations/ui/activate-edge-personalization-destinations.md) para obtener una vista completa de los pasos necesarios para activar las audiencias.

## Limitaciones y solución de problemas {#limitations-and-troubleshooting}

Tenga en cuenta las siguientes limitaciones a medida que explora el caso de uso descrito en esta página:

* Si utiliza ID de socio, tenga en cuenta que estos ID no se utilizan para crear su [gráfico de identidad](/help/identity-service/ui/identity-graph-viewer.md).

## Otros casos de uso obtenidos mediante la compatibilidad con datos de socios {#other-use-cases}

Explore más casos de uso habilitados a través de la compatibilidad con datos de socios en Real-Time CDP:

* [Complemente perfiles de origen con atributos de socios de datos de confianza para mejorar la base de datos, obtener nueva información sobre la base de clientes y optimizar mejor los públicos.](/help/rtcdp/partner-data/supplement-first-party-profiles.md)
* Utilice la compatibilidad con datos de terceros en Real-Time CDP para lo siguiente [amplíe su base de perfiles con perfiles potenciales de socios de datos y participe con ellos para adquirir o llegar a nuevos clientes](/help/rtcdp/partner-data/prospecting.md).
* (**Muy pronto**) [!BADGE Beta]{type=Informative}**Activación expandida** mediante ID de socios para ecosistemas de publicación que no aceptan PII o PII con hash.