---
title: Reparticipación inteligente
description: Ofrezca experiencias atractivas y conectadas durante los momentos clave de conversión para volver a atraer de forma inteligente a los clientes poco frecuentes.
feature: Use Cases
exl-id: 13f6dbc9-7471-40bf-824d-27922be0d879
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '3896'
ht-degree: 4%

---

# Vuelva a atraer a sus clientes de forma inteligente para que regresen

>[!NOTE]
>
>Esta es una implementación de muestra y los ejemplos de esta página, como la sintaxis de segmentos, son solo ejemplos. Debe usar los ejemplos como guía, ya que la implementación puede diferir.

Vuelva a atraer a los clientes que han abandonado una conversión de forma inteligente y responsable. Capte a los clientes caducados con experiencias para aumentar la conversión y aumentar el valor de duración del cliente.

Utilice consideraciones en tiempo real, tenga en cuenta todas las cualidades y comportamientos de los consumidores y ofrezca una reclasificación rápida basada en eventos en línea y sin conexión.

A continuación se muestra una vista de arquitectura de alto nivel de los distintos componentes de Real-Time CDP y Journey Optimizer. Este diagrama muestra cómo fluyen los datos entre las dos aplicaciones de Experience Platform desde la recopilación de datos hasta el punto en que se activan mediante recorridos o campañas hasta los destinos, para lograr el caso de uso descrito en esta página.

![Información general visual de alto nivel sobre la renovación inteligente de la participación.](../intelligent-re-engagement/images/step-by-step.png)

## Resumen del caso de uso {#overview}

Construirá esquemas, conjuntos de datos y audiencias a medida que trabaje con ejemplos de escenarios de renovación de participación. También descubrirá las características necesarias para configurar los recorridos de ejemplo en [!DNL Adobe Journey Optimizer] y las necesarias para crear anuncios multimedia de pago en destinos. Esta guía utiliza ejemplos de renovación de la participación de los clientes en los recorridos de casos de uso que se describen a continuación:

* **Escenario de exploración de productos abandonados**: Clientes de Target que han abandonado la exploración de productos en el sitio web y en la aplicación móvil.
* **Escenario de carro de compras abandonado**: Segmente a los clientes que han colocado productos en el carro de compras, pero que aún no han sido comprados tanto en el sitio web como en la aplicación móvil.
* **Escenario de confirmación de pedido**: céntrese en las compras de productos realizadas a través del sitio web y la aplicación móvil.

## Requisitos previos y planificación {#prerequisites-and-planning}

A medida que complete los pasos para implementar el caso de uso, utilizará las siguientes funcionalidades de Real-Time CDP y Adobe Journey Optimizer (enumeradas en el orden en que las utilizará). Asegúrese de que dispone de los [permisos de control de acceso basados en atributos](/help/access-control/home.md) necesarios para todas estas áreas, o pídale al administrador del sistema que le conceda los permisos necesarios.

* [[!DNL Adobe Real-Time Customer Data Platform (Real-Time CDP)]](https://experienceleague.adobe.com/docs/platform-learn/tutorials/rtcdp/understanding-the-real-time-customer-data-platform.html?lang=es) - Integra datos entre orígenes de datos para impulsar la campaña. A continuación, estos datos se utilizan para crear las audiencias de campaña y los elementos de datos personalizados de superficie que se utilizan en los mosaicos de promo de correo electrónico y web (por ejemplo, nombre o información relacionada con la cuenta). CDP también se usa para activar audiencias en el correo electrónico y la web (a través de [!DNL Adobe Target]).
   * [Esquemas](/help/xdm/home.md)
   * [Perfiles](/help/profile/home.md)
   * [Conjuntos de datos](/help/catalog/datasets/overview.md)
   * [Públicos](/help/segmentation/home.md)
   * [[!DNL Adobe Journey Optimizer]](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/journey.html?lang=es)
   * [Destinos](/help/destinations/home.md)

* [[!DNL Adobe Journey Optimizer]](https://experienceleague.adobe.com/docs/journey-optimizer-learn/tutorials/introduction-to-journey-optimizer/introduction.html?lang=es): ayuda a ofrecer a los clientes experiencias conectadas, contextuales y personalizadas.
   * [Evento o Déclencheur de audiencia](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioning/collect-event-data/data-collection.html?lang=es)
   * [Audiencias/ Eventos](https://experienceleague.adobe.com/docs/journey-optimizer/using/audiences-profiles-identities/audiences/about-audiences.html?lang=es)
   * [Acciones de Recorrido](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/journey.html?lang=es)

## Cómo lograr el caso de uso {#achieve-use-case-instruction}

A continuación se ofrece una descripción general de alto nivel de los tres ejemplos de escenarios de renovación de la participación.

>[!BEGINTABS]

>[!TAB Escenario de exploración de productos abandonado]

El escenario de exploración de productos abandonados se dirige a la exploración de productos abandonados tanto en el sitio web como en la aplicación móvil. Este escenario se activa cuando se ha visto un producto, pero no se ha comprado ni agregado al carro de compras. En este ejemplo, la participación de la marca se activa después de tres días si no hay adiciones de lista en las últimas 24 horas.<p>![Resumen visual de alto nivel del escenario de exploración de productos abandonados inteligente del cliente.](../intelligent-re-engagement/images/re-engagement-journey.png "Resumen visual de alto nivel del escenario de exploración de productos abandonados inteligente del cliente."){width="1920" zoomable="yes"}</p>

1. Usted crea esquemas y conjuntos de datos y luego habilita para [!UICONTROL Perfil].
2. Los datos se introducen en Experience Platform mediante SDK web, SDK móvil o API. El conector Source de Analytics también se puede utilizar, pero puede provocar una latencia de recorrido.
3. Los datos adicionales habilitados para perfiles se introducen y se pueden vincular al visitante de la aplicación móvil y web autenticado mediante gráficos de identidad.
4. Usted genera audiencias centradas a partir de la lista de perfiles para comprobar si un **cliente** ha realizado una participación en los últimos tres días.
5. Crea un recorrido de exploración de producto abandonado en [!DNL Adobe Journey Optimizer].
6. Si es necesario, trabaje con el **socio de datos** para la activación de audiencias en los destinos de medios de pago deseados.
7. [!DNL Adobe Journey Optimizer] comprueba el consentimiento y envía las diversas acciones configuradas.

>[!TAB Escenario de carro abandonado]

El escenario de carro de compras abandonado se aplica cuando los productos se han colocado en el carro de compras, pero aún no se han comprado tanto en el sitio web como en la aplicación móvil. Además, las campañas de medios de pago se inician y se detienen mediante este método.<p>![Resumen visual de alto nivel del escenario de carro de compras abandonado por el cliente.](../intelligent-re-engagement/images/abandoned-cart-journey.png "Resumen visual de alto nivel del escenario de carro de compras abandonado por el cliente."){width="1920" zoomable="yes"}</p>

1. Usted crea esquemas y conjuntos de datos, y habilita para [!UICONTROL Perfil].
2. Los datos se introducen en Experience Platform mediante SDK web, SDK móvil o API. El conector Source de Analytics también se puede utilizar, pero puede provocar una latencia de recorrido.
3. Los datos adicionales habilitados para perfiles se introducen y se pueden vincular al visitante de la aplicación móvil y web autenticado mediante gráficos de identidad.
4. Puede generar audiencias enfocadas a partir de la lista de perfiles para comprobar si un **cliente** ha puesto un artículo en su carro de compras, pero no ha completado la compra. El evento **[!UICONTROL Agregar al carro]** inicia un temporizador que espera 30 minutos y luego comprueba la compra. Si no se ha realizado ninguna compra, entonces el **cliente** se agrega a las audiencias de **[!UICONTROL Abandonar carro]**.
5. Usted crea un recorrido de carro de compras abandonado en [!DNL Adobe Journey Optimizer].
6. Si es necesario, trabaje con el **socio de datos** para la activación de audiencias en los destinos de medios de pago deseados.
7. [!DNL Adobe Journey Optimizer] comprueba el consentimiento y envía las diversas acciones configuradas.

>[!TAB Escenario de confirmación de pedido]

El escenario de confirmación de pedido se centra en las compras de productos realizadas a través del sitio web y la aplicación móvil.<p>![Resumen visual de alto nivel del escenario de confirmación de pedido del cliente.](../intelligent-re-engagement/images/order-confirmation-journey.png "Resumen visual de alto nivel del escenario de confirmación de pedido de cliente."){width="1920" zoomable="yes"}</p>

1. Usted crea esquemas y conjuntos de datos y luego habilita para [!UICONTROL Perfil].
2. Los datos se introducen en Experience Platform mediante SDK web, SDK móvil o API. El conector Source de Analytics también se puede utilizar, pero puede provocar una latencia de recorrido.
3. Los datos adicionales habilitados para perfiles se introducen y se pueden vincular al visitante de la aplicación móvil y web autenticado mediante gráficos de identidad.
4. Usted crea un recorrido de confirmación en [!DNL Adobe Journey Optimizer].
5. [!DNL Adobe Journey Optimizer] envía un mensaje de confirmación de pedido mediante el canal preferido.

>[!ENDTABS]

Para completar cada uno de los pasos de la información general de alto nivel anterior, lea las secciones siguientes, que ofrecen vínculos a más información e instrucciones más detalladas.

### Crear esquemas y especificar grupos de campos {#schema-design}

Los recursos del modelo de datos de experiencia (XDM) se administran en el área de trabajo [!UICONTROL Esquemas] de [!DNL Adobe Experience Platform]. Puede ver y explorar los recursos principales proporcionados por [!DNL Adobe] (por ejemplo, los grupos de campos) y crear recursos y esquemas personalizados para su organización.

Para obtener más información sobre la creación de [esquemas](/help/xdm/home.md), consulte el tutorial [crear esquema.](/help/xdm/tutorials/create-schema-ui.md) y [Modele sus datos de experiencia del cliente con XDM](https://experienceleague.adobe.com/docs/courses/using/experienceplatform-d-1-2021-1-xdm.html?lang=es).

Hay cuatro diseños de esquema que se utilizan para el caso de uso de renovación de la participación. Cada esquema requiere que se configuren campos específicos. Debe habilitar el esquema para que se incluya en el perfil del cliente en tiempo real. Para obtener más información sobre cómo habilitar el esquema para utilizarlo en el perfil del cliente en tiempo real, lea [habilitar un esquema para el perfil del cliente en tiempo real](/help/xdm/ui/resources/schemas.md#enable-a-schema-for-real-time-customer-profile).

#### Esquema de atributos del cliente

Este esquema se utiliza para estructurar y hacer referencia a los datos de perfil que conforman la información de clientes. Estos datos generalmente se incorporan a [!DNL Adobe Experience Platform] a través de su CRM o sistema similar y son necesarios para hacer referencia a los detalles del cliente que se utilizan para la personalización, el consentimiento de marketing y las capacidades de audiencia mejoradas.

El esquema de atributos del cliente está representado por una clase [[!UICONTROL XDM Individual Profile]](/help/xdm/classes/individual-profile.md), que incluye los siguientes grupos de campos:

+++Datos personales de contacto (grupo de campos)

[Datos de contacto personal](/help/xdm/field-groups/profile/personal-contact-details.md) es un grupo de campos de esquema estándar para la clase de perfil individual de XDM que describe la información de contacto de una persona individual.

| Campos | Descripción |
| --- | --- |
| `mobilePhone.number` | Número de teléfono móvil de la persona, que se utilizará para los SMS. |
| `personalEmail.address` | La dirección de correo electrónico de la persona. |

+++

+++Detalles de auditoría del sistema de Source externo (grupo de campos)

[Atributos de auditoría del sistema de Source externo](/help/xdm/data-types/external-source-system-audit-attributes.md) es un tipo de datos estándar del Modelo de datos de experiencia (XDM) que captura detalles de auditoría sobre un sistema de origen externo.

+++

+++Grupos de campos de consentimiento y preferencia (grupo de campos)

El grupo de campos [Consentimientos y preferencias](/help/xdm/field-groups//profile/consents.md) proporciona un único campo de tipo de objeto, consentimientos, para capturar información de consentimiento y preferencia.

| Campos | Requisito |
| --- | --- |
| `consents.marketing.email.val` | Requerido |
| `consents.marketing.preferred` | Requerido |
| `consents.marketing.push.val` | Requerido |
| `consents.marketing.sms.val` | Requerido |
| `consents.personalize.content.val` | Requerido |
| `consents.share.val` | Requerido |

+++

+++Detalles de prueba de perfil (grupo de campos)

Este grupo de campos le permite probar el recorrido antes de publicarlo, mediante perfiles de prueba. Para obtener más información acerca de la creación de perfiles de prueba, lea el [tutorial Crear perfiles de prueba](https://experienceleague.adobe.com/docs/journeys/using/building-journeys/about-journey-building/creating-test-profiles.html?lang=es) y [tutorial Prueba del recorrido](https://experienceleague.adobe.com/docs/journeys/using/building-journeys/testing-the-journey.html?lang=es).

+++

#### Esquema de transacciones digitales del cliente

Este esquema se utiliza para estructurar y hacer referencia a los datos de evento que conforman la actividad de cliente que se produce en el sitio web o en las plataformas digitales asociadas. Estos datos generalmente se incorporan a [!DNL Adobe Experience Platform] a través de [Web SDK](/help/web-sdk/home.md) y son necesarios para hacer referencia a los distintos eventos de exploración y conversión que se utilizan para activar recorridos, análisis detallado de clientes en línea, funcionalidades de audiencia mejoradas y mensajes personalizados.

El esquema de transacciones digitales del cliente está representado por una clase [[!UICONTROL XDM ExperienceEvent]](/help/xdm/classes/experienceevent.md).

+++ExperienceEvent de XDM (clase)

La clase [[!UICONTROL XDM ExperienceEvent]](/help/xdm/classes/experienceevent.md) incluye los siguientes grupos de campos:

| Campos | Descripción |
| --- | --- |
| `_id` | Identifica de forma exclusiva los eventos individuales que se incorporan a [!DNL Adobe Experience Platform]. |
| `timestamp` | Una marca de tiempo ISO 8601 de cuándo se produjo el evento, con formato según RFC 3339, sección 5.6. Esta marca de tiempo debe pertenecer al pasado. |
| `eventType` | Cadena que indica el tipo de categoría del evento. |

+++

+++Detalles del ID del usuario final (grupo de campos)

El grupo de campos [Detalles del identificador de usuario final](/help/xdm/field-groups/event/enduserids.md) se usa para describir la información de identidad de un individuo en varias aplicaciones de Adobe.

| Campos | Descripción |
| --- | --- |
| `endUserIDs._experience.emailid.authenticatedState` | Estado autenticado de ID de dirección de correo electrónico del usuario final. |
| `endUserIDs._experience.emailid.id` | ID de dirección de correo electrónico del usuario final. |
| `endUserIDs._experience.emailid.namespace.code` | Código de área de nombres de ID de dirección de correo electrónico del usuario final. |
| `endUserIDs._experience.mcid.authenticatedState` | [!DNL Adobe] estado autenticado de Marketing Cloud ID (MCID). El MCID ahora se conoce como Experience Cloud ID (ECID). |
| `endUserIDs._experience.mcid.id` | [!DNL Adobe] Marketing Cloud ID (MCID). El MCID ahora se conoce como Experience Cloud ID (ECID). |
| `endUserIDs._experience.mcid.namespace.code` | [!DNL Adobe] código de área de nombres de Marketing Cloud ID (MCID). |

+++

+++Detalles de Commerce (grupo de campos)

El grupo de campos [Detalles de Commerce](/help/xdm/field-groups/event/commerce-details.md) se usa para describir datos comerciales, como información de productos (SKU, nombre y cantidad) y operaciones estándar del carro de compras (pedidos, pagos y abandonos).

| Campos | Descripción |
| --- | --- |
| `commerce.cart.cartID` | ID del carro de compras. |
| `commerce.order.orderType` | Un objeto que describe el tipo de pedido del producto. |
| `commerce.order.payments.paymentAmount` | Un objeto que describe el importe de pago del pedido del producto. |
| `commerce.order.payments.paymentType` | Un objeto que describe el tipo de pago de pedido de producto. |
| `commerce.order.payments.transactionID` | Un ID de transacción de pedido de producto de objeto. |
| `commerce.order.purchaseID` | ID de compra de pedido de producto de objeto. |
| `productListItems.name` | Una lista de nombres de artículos que representa los productos seleccionados por un cliente. |
| `productListItems.priceTotal` | El precio total de la lista de artículos que representan los productos seleccionados por un cliente. |
| `productListItems.product` | El producto o los productos seleccionados. |
| `productListItems.quantity` | La cantidad de artículos que representan los productos seleccionados por un cliente. |

+++

+++Detalles de auditoría del sistema de Source externo (grupo de campos)

Los atributos de auditoría del sistema de Source externo son un tipo de datos estándar del Modelo de datos de experiencia (XDM) que captura detalles de auditoría sobre un sistema de origen externo.

+++

#### Esquema de transacciones sin conexión del cliente

Este esquema se utiliza para estructurar y hacer referencia a los datos de evento que conforman la actividad de cliente que se produce en plataformas fuera del sitio web. Estos datos generalmente se incorporan a [!DNL Adobe Experience Platform] desde un POS (o sistema similar) y, con mayor frecuencia, se transmiten a Experience Platform a través de una conexión API. Su propósito es hacer referencia a los distintos eventos de conversión sin conexión que se utilizan para activar recorridos, análisis de clientes en línea y sin conexión profundos, funcionalidades de audiencia mejoradas y mensajería personalizada.

El esquema de transacciones sin conexión de cliente está representado por una clase [[!UICONTROL XDM ExperienceEvent]](/help/xdm/classes/experienceevent.md).

+++ExperienceEvent de XDM (clase)

La clase [[!UICONTROL XDM ExperienceEvent]](/help/xdm/classes/experienceevent.md) incluye los siguientes grupos de campos:

| Campos | Descripción |
| --- | --- |
| `_id` | Identifica de forma exclusiva los eventos individuales que se incorporan a [!DNL Adobe Experience Platform]. |
| `timestamp` | Una marca de tiempo ISO 8601 de cuándo se produjo el evento, con formato según RFC 3339, sección 5.6. Esta marca de tiempo debe pertenecer al pasado. |
| `eventType` | Cadena que indica el tipo de categoría del evento. |

+++

+++Detalles de Commerce (grupo de campos)

El grupo de campos [Detalles de Commerce](/help/xdm/field-groups/event/commerce-details.md) se usa para describir datos comerciales, como información de productos (SKU, nombre y cantidad) y operaciones estándar del carro de compras (pedidos, pagos y abandonos).

| Campos | Descripción |
| --- | --- |
| `commerce.cart.cartID` | ID del carro de compras. |
| `commerce.order.orderType` | Un objeto que describe el tipo de pedido del producto. |
| `commerce.order.payments.paymentAmount` | Un objeto que describe el importe de pago del pedido del producto. |
| `commerce.order.payments.paymentType` | Un objeto que describe el tipo de pago de pedido de producto. |
| `commerce.order.payments.transactionID` | Un ID de transacción de pedido de producto de objeto. |
| `commerce.order.purchaseID` | ID de compra de pedido de producto de objeto. |
| `productListItems.name` | Una lista de nombres de artículos que representa los productos seleccionados por un cliente. |
| `productListItems.priceTotal` | El precio total de la lista de artículos que representan los productos seleccionados por un cliente. |
| `productListItems.product` | El producto o los productos seleccionados. |
| `productListItems.quantity` | La cantidad de artículos que representan los productos seleccionados por un cliente. |

+++

+++Datos personales de contacto (grupo de campos)

[Datos de contacto personal](/help/xdm/field-groups/profile/personal-contact-details.md) es un grupo de campos de esquema estándar para la clase de perfil individual de XDM que describe la información de contacto de una persona individual.

| Campos | Descripción |
| --- | --- |
| `mobilePhone.number` | Número de teléfono móvil de la persona, que se utilizará para los SMS. |
| `personalEmail.address` | La dirección de correo electrónico de la persona. |

+++

+++Detalles de auditoría del sistema de Source externo (grupo de campos)

Los atributos de auditoría del sistema de Source externo son un tipo de datos estándar del Modelo de datos de experiencia (XDM) que captura detalles de auditoría sobre un sistema de origen externo.

+++

#### Esquema del conector web de Adobe

>[!NOTE]
>
>Esta es una implementación opcional si está usando [[!DNL Adobe Analytics Source Connector]](/help/sources/connectors/adobe-applications/analytics.md).

Este esquema se utiliza para estructurar y hacer referencia a los datos de evento que conforman la actividad de cliente que se produce en el sitio web o en las plataformas digitales asociadas. Este esquema es similar al esquema de transacciones digitales del cliente, pero difiere en que está pensado para utilizarse cuando [Web SDK](/help/web-sdk/home.md) no es una opción para la recopilación de datos; por lo tanto, este esquema es necesario cuando se utiliza [!DNL Adobe Analytics Source Connector] para enviar los datos en línea a [!DNL Adobe Experience Platform] como un conjunto de datos principal o secundario.

El esquema del conector web [!DNL Adobe] está representado por una clase [[!UICONTROL XDM ExperienceEvent]](/help/xdm/classes/experienceevent.md).

+++ExperienceEvent de XDM (clase)

La clase [[!UICONTROL XDM ExperienceEvent]](/help/xdm/classes/experienceevent.md) incluye los siguientes grupos de campos:

| Campos | Descripción |
| --- | --- |
| `_id` | Identifica de forma exclusiva los eventos individuales que se incorporan a [!DNL Adobe Experience Platform]. |
| `timestamp` | Una marca de tiempo ISO 8601 de cuándo se produjo el evento, con formato según RFC 3339, sección 5.6. Esta marca de tiempo debe pertenecer al pasado. |
| `eventType` | Cadena que indica el tipo de categoría del evento. |

+++

+++Plantilla de ExperienceEvent de Adobe Analytics (grupo de campos)

El grupo de campos [Adobe Analytics ExperienceEvent](/help/xdm/field-groups/event/analytics-full-extension.md) captura métricas comunes que recopila Adobe Analytics.

| Campos | Descripción |
| --- | --- |
| `endUserIDs._experience.emailid.authenticatedState` | Estado autenticado de ID de dirección de correo electrónico del usuario final. |
| `endUserIDs._experience.emailid.id` | ID de dirección de correo electrónico del usuario final. |
| `endUserIDs._experience.emailid.namespace.code` | Código de área de nombres de ID de dirección de correo electrónico del usuario final. |
| `endUserIDs._experience.mcid.authenticatedState` | [!DNL Adobe] estado autenticado de Marketing Cloud ID (MCID). El MCID ahora se conoce como Experience Cloud ID (ECID). |
| `endUserIDs._experience.mcid.id` | [!DNL Adobe] Marketing Cloud ID (MCID). El MCID ahora se conoce como Experience Cloud ID (ECID). |
| `endUserIDs._experience.mcid.namespace.code` | [!DNL Adobe] código de área de nombres de Marketing Cloud ID (MCID). |

+++

+++Detalles de auditoría del sistema de Source externo (grupo de campos)

Los atributos de auditoría del sistema de Source externo son un tipo de datos estándar del Modelo de datos de experiencia (XDM) que captura detalles de auditoría sobre un sistema de origen externo.

+++

### Creación de un conjunto de datos a partir de un esquema {#create-datasets}

Un conjunto de datos es una estructura de almacenamiento y administración para un grupo de datos. Cada esquema para escenarios inteligentes de renovación de la participación debe tener su propio conjunto de datos.

Para obtener más información sobre cómo crear un [conjunto de datos](/help/catalog/datasets/overview.md) a partir de un esquema, lea la [Guía de IU de conjuntos de datos](/help/catalog/datasets/user-guide.md).

>[!NOTE]
>
>Similar al paso para crear un esquema, debe habilitar el conjunto de datos para que se incluya en el Perfil del cliente en tiempo real. Para obtener más información sobre cómo habilitar el conjunto de datos para utilizarlo en el perfil del cliente en tiempo real, consulte el tutorial sobre [introducción de datos en el perfil del cliente en tiempo real](https://experienceleague.adobe.com/docs/platform-learn/tutorials/profiles/bring-data-into-the-real-time-customer-profile.html?lang=es).

### Consentimiento y control de datos {#privacy-consent}

>[!IMPORTANT]
>
>Proporcionar a los clientes la capacidad de cancelar la suscripción a la recepción de comunicaciones de una marca, así como garantizar que se cumpla esta opción, es un requisito legal. Obtenga más información acerca de la legislación aplicable en la [descripción general de las normas de privacidad](https://experienceleague.adobe.com/docs/experience-platform/privacy/regulations/overview.html?lang=es).

#### Políticas de consentimiento

Al crear una ruta de participación, considere la posibilidad de agregar las [políticas de consentimiento](https://experienceleague.adobe.com/docs/platform-learn/data-collection/web-sdk/consent/overview.html?lang=es) siguientes:

* Si `consents.marketing.email.val = "Y"`, entonces puede enviar un correo electrónico
* Si `consents.marketing.sms.val = "Y"`, entonces puede enviar un SMS
* Si `consents.marketing.push.val = "Y"`, entonces puede insertar
* Si `consents.share.val = "Y"`, entonces Puede anunciar

#### Etiquetado y aplicación de gobernanza de datos

Al crear una ruta de participación, considere la posibilidad de agregar las siguientes [etiquetas de control de datos](/help/data-governance/labels/overview.md):

* Las direcciones de correo electrónico personales se utilizan como datos de identificación directa que se utilizan para identificar a una persona específica o ponerse en contacto con ella, en lugar de con un dispositivo.
   * `personalEmail.address = I1`

#### Políticas de uso de datos

No se requieren [políticas de uso de datos](/help/data-governance/policies/overview.md) para el escenario de exploración de productos abandonados. Sin embargo, debe tener en cuenta lo siguiente:

* Restringir datos confidenciales
* Restringir Advertising in situ
* Restringir direccionamiento de correo electrónico
* Restringir la segmentación entre sitios
* Restringir la combinación de datos directamente identificables con datos anónimos

### Creación de públicos {#create-audience}

Los escenarios de renovación de participación utilizan audiencias para definir atributos o comportamientos específicos compartidos por un subconjunto de perfiles del almacén de perfiles con el fin de distinguir un grupo comercializable de personas de la base de clientes. Las audiencias se pueden crear de varias maneras en [!DNL Adobe Experience Platform].

Para obtener más información sobre cómo crear una audiencia, lea la [guía de la interfaz de usuario del servicio de audiencia](https://experienceleague.adobe.com/docs/experience-platform/segmentation/ui/overview.html?lang=es#create-audience).

Para obtener más información sobre cómo componer directamente [Audiencias](/help/segmentation/home.md), lea la [guía de la interfaz de usuario de la composición de audiencias](/help/segmentation/ui/audience-composition.md).

Para obtener más información sobre cómo crear audiencias mediante definiciones de audiencia derivadas de Experience Platform, lea la [guía de la interfaz de usuario de Audience Builder](/help/segmentation/ui/segment-builder.md).

>[!BEGINTABS]

>[!TAB Escenario de exploración de productos abandonado]

Esta audiencia se crea como una mejora del escenario clásico &quot;Abandono del carro de compras&quot;. Mientras que el abandono del carro de compras generalmente se centra en la adición de un carro de compras sin una compra posterior en un período de tiempo determinado, esta audiencia busca una participación anterior, específicamente aquellos que pueden haber explorado un producto en particular, pero no lo agregaron al carro de compras y no tuvieron actividad de seguimiento en el sitio dentro de un marco de tiempo determinado. Esta audiencia le ayuda a mantener su marca &quot;en la mente&quot; de los clientes que cumplen con estos criterios de inclusión y también se puede aprovechar para clientes cuyas propiedades digitales pueden diferir de un modelo de comercio electrónico tradicional.

+++Vista de producto abandonado sin participación en los últimos tres días

El siguiente evento se utiliza para el escenario de exploración de productos abandonados en el que los usuarios vieron los productos en línea y no interactuaron (visitas al sitio, visitas a la aplicación, compras en línea, compras sin conexión y eventos de adición al carro de compras) en los 3 días siguientes.

Se requieren los campos y las condiciones siguientes al configurar esta audiencia:

* `eventType: commerce.productViews`
* Y `THEN` (evento secuencial) excluyen `eventType: commerce.productListAdds` AND `application.launch` AND `web.webpagedetails.pageViews` AND `commerce.purchases` (esto incluye tanto en línea como sin conexión)
   * `Timestamp: > 3 days after productView`
* `Timestamp: > 4 days`

+++

+++Vista del producto con participación en los últimos tres días

El siguiente evento se utiliza en el escenario de navegación de productos abandonados en el que los usuarios vieron los productos en línea y participaron (visitas al sitio, visitas a la aplicación, compras en línea, compras sin conexión y eventos de adición al carro de compras) en los 3 días siguientes.

Se requieren los campos y las condiciones siguientes al configurar esta audiencia:

* `eventType: commerce.productViews`
* Y `THEN` (evento secuencial) incluye `eventType: commerce.productListAdds` O `application.launch` O `web.webpagedetails.pageViews` O `commerce.purchases` (esto incluye tanto en línea como sin conexión)
   * `Timestamp: > 3 days after productView`
* `Timestamp: > 4 days`
+++

+++Flujo de participación en el último día

El siguiente evento se utiliza para el escenario de exploración de productos abandonados en el que los usuarios han participado (visitas al sitio, visitas a la aplicación, compras en línea, compras sin conexión y eventos de agregar al carro de compras) en el último día.

Se requieren los campos y las condiciones siguientes al configurar esta audiencia:

* `eventType: commerce.productListAdds OR application.launch OR web.webpagedetails.pageViews OR commerce.purchases`
   * `Timestamp: in last 1 day` (Transmisión)

+++

+++Lote de participación en los últimos tres días

El siguiente evento se utiliza para el escenario de exploración de productos abandonados en el que los usuarios han participado (visitas al sitio, visitas a la aplicación, compras en línea, compras sin conexión y eventos de agregar al carro de compras) en los últimos 3 días.

Se requieren los campos y las condiciones siguientes al configurar esta audiencia:

* `EventType: commerce.productListAdds OR application.launch OR web.webpagedetails.pageViews OR commerce.purchases`
   * `Timestamp: in last 3 days` (Lote)

+++

>[!TAB Escenario de carro abandonado]

Esta audiencia se crea para admitir el escenario clásico &quot;Abandono del carro de compras&quot;. Su propósito es encontrar clientes que agregaron un producto al carro de compras, pero que finalmente no siguieron con una compra. Esta audiencia ayudará a mantener no solo su marca &quot;en mente&quot; para sus clientes, sino también los productos que dejaron atrás sin una compra posterior.

Los siguientes eventos se utilizan en el escenario de carro de compras abandonado, en el que los usuarios agregaron un producto al carro de compras hace entre 1 y 4 días, pero no completaron la compra ni borraron el carro de compras.

Se requieren los campos y las condiciones siguientes al configurar esta audiencia:

* `eventType: commerce.productListAdds`
   * `Timestamp: >= 1 days before now AND <= 4 days before now `
* `eventType: commerce.purchases`
   * `Timestamp: <= 4 days before now`
* `eventType: commerce.productListRemovals`
   * `Timestamp: <= 4 days before now`

El descriptor para el escenario de carro de compras abandonado aparece de la siguiente manera:

`Include eventType = commerce.productListAdds between 30 min and 1440 minutes before now. exclude eventType = commerce.purchases 30 minutes before now OR eventType = commerce.productListRemovals AND Cart ID equals Product List Adds1 Cart ID (the inclusion event).`

>[!TAB Escenario de confirmación de pedido]

Este recorrido no requiere que se creen audiencias.

>[!ENDTABS]

### Configuración del recorrido en Adobe Journey Optimizer {#journey-setup}

>[!NOTE]
>
>[!DNL Adobe Journey Optimizer] no abarca todo lo que se muestra en los diagramas. Todos los [anuncios multimedia pagados](/help/destinations/catalog/social/overview.md) se crean en [!UICONTROL Destinos].

[[!DNL Adobe Journey Optimizer]](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/journey.html?lang=es) le ayuda a ofrecer a sus clientes experiencias conectadas, contextuales y personalizadas. El recorrido del cliente es todo el proceso de interacción de un cliente con la marca. Cada recorrido de caso de uso requiere información específica. A continuación se enumeran los datos precisos necesarios para cada recorrido.

>[!BEGINTABS]

>[!TAB Escenario de exploración de productos abandonado]

El escenario de exploración de productos abandonados se dirige a la exploración de productos abandonados tanto en el sitio web como en la aplicación móvil.<p>![Resumen visual de alto nivel del escenario de exploración de productos abandonados por el cliente.](../intelligent-re-engagement/images/re-engagement-journey.png "Resumen visual de alto nivel del escenario de exploración de productos abandonados por el cliente."){width="1920" zoomable="yes"}</p>

+++Eventos

Los eventos permiten activar sus recorridos de forma unitaria para enviar mensajes, en tiempo real, al particular que entra en el recorrido. Para obtener más información sobre los eventos, lea la [guía general de eventos](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/general-events.html?lang=es).

* Evento 1: Vistas del producto
   * Esquema: Transacciones digitales del cliente
   * Campos:
      * `eventType`
   * Condición:
      * `eventType = commerce.productViews`
      * Campos:
         * `eventType`
         * `productListItems.name`
         * `productListItems.priceTotal`
         * `productListItems.product`
         * `productListItems.productImageUrl`
         * `productListItems.quantity`
         * `timestamp`
         * `endUserIDs._experience.emailid.authenticatedState`
         * `endUserIDs._experience.emailid.id`
         * `endUserIDs._experience.emailid.namespace.code`
         * `_id`

* Evento 2: Agregar al carro
   * Esquema: Transacciones digitales del cliente
   * Campos:
      * `eventType`
   * Condición:
      * `eventType = commerce.productListAdds`
      * Campos:
         * `commerce.productListAdds.id`
         * `commerce.productListAdds.value`
         * `eventType`
         * `identityMap.authenticatedState`
         * `identityMap.id`
         * `identityMap.primary`
         * `productListItems.SKU`
         * `productListItems.currencyCode`
         * `productListItems.name`
         * `productListItems.priceTotal`
         * `productListItems.product`
         * `productListItems.productImageUrl`
         * `productListItems.quantity`
         * `timestamp`
         * `commerce.cart.cartID`
         * `endUserIDs._experience.emailid.authenticatedState`
         * `endUserIDs._experience.emailid.id`
         * `endUserIDs._experience.emailid.namespace.code`
         * `_id`

* Evento 3: Compromiso de marca
   * Esquema: Transacciones digitales del cliente
   * Campos:
      * `eventType`
   * Condición:
      * `eventType in application.launch, commerce.purchases, web.webpagedetails.pageViews`
      * Campos:
         * `eventType`
         * `identityMap.authenticatedState`
         * `identityMap.id`
         * `identityMap.primary`
         * `productListItems.SKU`
         * `productListItems.currencyCode`
         * `productListItems.name`
         * `productListItems.priceTotal`
         * `productListItems.product`
         * `productListItems.productImageUrl`
         * `productListItems.quantity`
         * `timestamp`
         * `web.webpagedetails.URL`
         * `web.webpagedetails.isHomePage`
         * `web.webpagedetails.name`
         * `endUserIDs._experience.emailid.authenticatedState`
         * `endUserIDs._experience.emailid.id`
         * `endUserIDs._experience.emailid.namespace.code`
         * `_id`
         * `commerce.purchases.id`
         * `commerce.purchases.value`
         * `shipping.address.city`
         * `shipping.address.countryCode`
         * `shipping.address.postalCode`
         * `shipping.address.state`
         * `shipping.address.street1`
         * `shipping.address.street2`
         * `shipping.shipDate`
         * `shipping.trackingNumber`
         * `shipping.trackingURL`

+++

+++Lógica clave del lienzo Recorrido

La lógica de clave de lienzo de recorrido requiere que identifique eventos específicos y que configure las acciones que deben realizarse después de que se produzca el evento.

* Lógica de entrada de recorrido
   * Evento de vista de producto

* Condiciones
   * Compruebe si hay al menos un evento de compra en línea o sin conexión desde la última vez que se vio el producto.
      * Esquema: Transacciones digitales del cliente
      * `eventType = commerce.purchases`
      * `timestamp > timestamp of product last viewed`

   * Compruebe si hay al menos una compra sin conexión desde la última vez que vio el producto:
      * Esquema: Transacciones sin conexión del cliente
      * `eventType = commerce.purchases`
      * `timestamp > timestamp of product last viewed`

   * Condiciones: Seleccione el canal de Target
      * Correo electrónico
         * `consents.marketing.email.val = y`
      * Push
         * `consents.marketing.push.val=y`
      * SMS
         * `consents.marketing.sms.val = y`

   * Channel Personalization
      * Contenido de canal personalizado basado en la vista del producto.

+++

>[!TAB Escenario de carro abandonado]

El escenario de carro de compras abandonado se dirige a productos que se han colocado en el carro de compras, pero que aún no se han comprado tanto en el sitio web como en la aplicación móvil.<p>![Resumen visual de alto nivel del escenario de carro de compras abandonado por el cliente.](../intelligent-re-engagement/images/abandoned-cart-journey.png "Resumen visual de alto nivel del escenario de carro de compras abandonado por el cliente."){width="1920" zoomable="yes"}</p>

+++Eventos

Los eventos permiten activar sus recorridos de forma unitaria para enviar mensajes, en tiempo real, al particular que entra en el recorrido. Para obtener más información sobre los eventos, lea la [guía general de eventos](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/general-events.html?lang=es).

* Evento 2: Agregar al carro
   * Esquema: Transacciones digitales del cliente
   * Campos:
      * `eventType`
   * Condición:
      * `eventType = commerce.productListAdds`
      * Campos:
         * `commerce.productListAdds.id`
         * `commerce.productListAdds.value`
         * `eventType`
         * `identityMap.authenticatedState`
         * `identityMap.id`
         * `identityMap.primary`
         * `productListItems.SKU`
         * `productListItems.currencyCode`
         * `productListItems.name`
         * `productListItems.priceTotal`
         * `productListItems.product`
         * `productListItems.productImageUrl`
         * `productListItems.quantity`
         * `timestamp`
         * `commerce.cart.cartID`
         * `endUserIDs._experience.emailid.authenticatedState`
         * `endUserIDs._experience.emailid.id`
         * `endUserIDs._experience.emailid.namespace.code`
         * `_id`

* Evento 4: Compras en línea
   * Esquema: Transacciones digitales del cliente
   * Campos:
      * `eventType`
   * Condición:
      * `eventType = commerce.purchases`
      * Campos:
         * `commerce.purchases.id`
         * `commerce.purchases.value`
         * `eventType`
         * `identityMap.authenticatedState`
         * `identityMap.id`
         * `identityMap.primary`
         * `productListItems.SKU`
         * `productListItems.currencyCode`
         * `productListItems.name`
         * `productListItems.priceTotal`
         * `productListItems.product`
         * `productListItems.productImageUrl`
         * `productListItems.quantity`
         * `timestamp`
         * `endUserIDs._experience.emailid.authenticatedState`
         * `endUserIDs._experience.emailid.id`
         * `endUserIDs._experience.emailid.namespace.code`
         * `_id`

* Evento 3: Compromiso de marca
   * Esquema: Transacciones digitales del cliente
   * Campos:
      * `eventType`
   * Condición:
      * `eventType in application.launch, commerce.purchases, web.webpagedetails.pageViews`
      * Campos:
         * `eventType`
         * `identityMap.authenticatedState`
         * `identityMap.id`
         * `identityMap.primary`
         * `productListItems.SKU`
         * `productListItems.currencyCode`
         * `productListItems.name`
         * `productListItems.priceTotal`
         * `productListItems.product`
         * `productListItems.productImageUrl`
         * `productListItems.quantity`
         * `timestamp`
         * `web.webpagedetails.URL`
         * `web.webpagedetails.isHomePage`
         * `web.webpagedetails.name`
         * `endUserIDs._experience.emailid.authenticatedState`
         * `endUserIDs._experience.emailid.id`
         * `endUserIDs._experience.emailid.namespace.code`
         * `_id`
         * `commerce.purchases.id`
         * `commerce.purchases.value`
         * `shipping.address.city`
         * `shipping.address.countryCode`
         * `shipping.address.postalCode`
         * `shipping.address.state`
         * `shipping.address.street1`
         * `shipping.address.street2`
         * `shipping.shipDate`
         * `shipping.trackingNumber`
         * `shipping.trackingURL`

+++

+++Lógica clave del lienzo Recorrido

La lógica de clave de lienzo de recorrido requiere que identifique eventos específicos y que configure las acciones que deben realizarse después de que se produzca el evento.

* Lógica de entrada de recorrido
   * `AddToCart` evento

* AuthenticatedState en autenticado

* Condición: compras sin conexión desde que se abandonó el carro por última vez:
   * Esquema: Transacciones sin conexión del cliente
   * `eventType = commerce.purchases`
   * `timestamp > timestamp of cart was last abandoned`

* Condición: carro de compras borrado desde la última vez que se abandonó:
   * Esquema: Transacciones digitales del cliente
   * `eventType = commerce.cartCleared`
   * `cartID` (ID del carro de compras)
   * `timestamp > timestamp of cart was last abandoned`

* Seleccionar canal de destino (seleccione uno o varios canales para ampliar el alcance)
   * Correo electrónico
      * `consents.marketing.email.val = y`
   * Push
      * `consents.marketing.push.val = y`
   * SMS
      * `consents.marketing.sms.val = y`
   * Channel Personalization
      * Muestra información detallada del carro de compras y puede mostrar varios productos en formato de tabla.

+++

>[!TAB Escenario de confirmación de pedido]

El escenario de confirmación de pedido se centra en las compras de productos realizadas a través del sitio web y la aplicación móvil.<p>![Resumen visual de alto nivel del escenario de confirmación de pedido del cliente.](../intelligent-re-engagement/images/order-confirmation-journey.png "Resumen visual de alto nivel del escenario de confirmación de pedido de cliente."){width="1920" zoomable="yes"}</p>

+++Eventos

Los eventos permiten activar sus recorridos de forma unitaria para enviar mensajes, en tiempo real, al particular que entra en el recorrido. Para obtener más información sobre los eventos, lea la [guía general de eventos](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/general-events.html?lang=es).

* Evento 4: Compras en línea
   * Esquema: Transacciones digitales del cliente
   * Campos:
      * `eventType`
   * Condición:
      * `eventType = commerce.purchases`
      * Campos:
         * `commerce.purchases.id`
         * `commerce.purchases.value`
         * `eventType`
         * `identityMap.authenticatedState`
         * `identityMap.id`
         * `identityMap.primary`
         * `productListItems.SKU`
         * `productListItems.currencyCode`
         * `productListItems.name`
         * `productListItems.priceTotal`
         * `productListItems.product`
         * `productListItems.productImageUrl`
         * `productListItems.quantity`
         * `timestamp`
         * `endUserIDs._experience.emailid.authenticatedState`
         * `endUserIDs._experience.emailid.id`
         * `endUserIDs._experience.emailid.namespace.code`
         * `_id`

+++

+++Lógica clave del lienzo Recorrido

La lógica de clave de lienzo de recorrido requiere que identifique eventos específicos y que configure las acciones que deben realizarse después de que se produzca el evento.

* Lógica de entrada de recorrido
   * Evento de pedido

* Condiciones
   * Seleccionar canal de destino (seleccione uno o varios canales para ampliar el alcance).
      * La confirmación de pedido se considera una prestación por naturaleza, por lo que la comprobación del consentimiento suele ser innecesaria.
      * Correo electrónico
      * Push
      * SMS

   * Personalization de contenido de canal
      * Muestra información detallada del pedido y puede mostrar una lista de productos con un formato de tabla.

+++

>[!ENDTABS]

Para obtener más información acerca de cómo crear recorridos en [!DNL Adobe Journey Optimizer], lea la [Guía de introducción a los recorridos](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/journey.html?lang=es).

### Configuración de anuncios de medios de pago en destinos {#paid-media-ads}

El marco de destinos se utiliza para anuncios de medios de pago. Una vez comprobado el consentimiento, se envía a los distintos destinos configurados. Para obtener más información sobre los destinos, lea el documento [Información general sobre destinos](/help/destinations/home.md).

#### Datos necesarios para los destinos

Los destinos de exportación de audiencias de streaming (como Facebook, Google Customer Match o Google DV360) admiten varias identidades a partir de los datos del cliente:

* `personalEmail.address`
* `ECID`
* `mobilePhone.number`

Puede activar la exploración de productos abandonados y las audiencias de abandono del carro de compras para los anuncios de medios de pago.

* Transmisión/Activado
   * [Advertising](/help/destinations/catalog/advertising/overview.md)/[Medios de pago y medios sociales](/help/destinations/catalog/social/overview.md)
   * [Dispositivo móvil](/help/destinations/catalog/mobile-engagement/overview.md)
   * [Destino de streaming](/help/destinations/catalog/streaming/http-destination.md)
   * [Destino personalizado creado mediante Destination SDK.](/help/destinations/destination-sdk/overview.md). Si es cliente de Real-Time CDP Ultimate, también puede crear un [destino personalizado con Destination SDK](/help/destinations/destination-sdk/overview.md#productized-and-custom-integrations)

## Pasos siguientes {#next-steps}

Al volver a atraer a los clientes que abandonaron una conversión de una manera inteligente y responsable, esperamos que haya aumentado las conversiones y el valor de duración del cliente.

A continuación, puede explorar otros casos de uso admitidos por Real-Time CDP, como [mostrar contenido personalizado a usuarios no autenticados](/help/rtcdp/partner-data/onsite-personalization.md) en sus propiedades web.
