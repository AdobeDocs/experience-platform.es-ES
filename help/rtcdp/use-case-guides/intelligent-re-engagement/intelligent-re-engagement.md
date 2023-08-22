---
title: Reparticipación inteligente
description: Ofrezca experiencias atractivas y conectadas durante los momentos clave de conversión para volver a atraer de forma inteligente a clientes poco frecuentes.
hide: true
hidefromtoc: true
source-git-commit: 69d83e0ca7530f09042e0740e3f25ba92ecb24e4
workflow-type: tm+mt
source-wordcount: '3395'
ht-degree: 4%

---

# Vuelva a atraer a sus clientes de forma inteligente para que regresen

Vuelva a atraer a los clientes que han abandonado una conversión antes de finalizarla de forma inteligente y responsable. Capte a los clientes caducados a través de experiencias en lugar de recordatorios para mejorar la conversión e impulsar el crecimiento del valor de duración del cliente.

Utilice consideraciones en tiempo real, tenga en cuenta todas las cualidades y comportamientos de los consumidores y ofrezca una reclasificación rápida basada en eventos en línea y sin conexión.

![Resumen visual de alto nivel de renovación inteligente de la participación paso a paso.](../intelligent-re-engagement/images/step-by-step.png)

## Resumen del caso de uso

Construirá esquemas, conjuntos de datos y audiencias a medida que trabaje con ejemplos de recorridos de renovación de la participación. También descubrirá las funciones necesarias para configurar los recorridos de ejemplo en [!DNL Adobe Journey Optimizer] y los necesarios para crear anuncios de medios de pago en los destinos. Esta guía utiliza ejemplos de renovación de la participación de los clientes en los recorridos de casos de uso que se describen a continuación:

* **Recorrido de renovación de participación** : Se dirige a los clientes que han abandonado la navegación de productos tanto en el sitio web como en la aplicación móvil.
* **Recorrido de carro abandonado** - Se dirige a los clientes que han colocado productos en el carro de compras, pero que aún no han sido comprados tanto en el sitio web como en la aplicación móvil.
* **Recorrido de confirmación de pedido** - Se centra en las compras de productos realizadas a través del sitio web y la aplicación móvil.

## Requisitos previos y planificación {#prerequisites-and-planning}

A medida que complete los pasos para implementar el caso de uso, utilizará las siguientes funciones y elementos de la interfaz de usuario de Real-Time CDP (enumerados en el orden en que los usará). Asegúrese de que dispone de los permisos de control de acceso basados en atributos necesarios para todas estas áreas o solicite al administrador del sistema que le conceda los permisos necesarios.

* [[!DNL Adobe Real-Time Customer Data Platform (Real-Time CDP)]](https://experienceleague.adobe.com/docs/platform-learn/tutorials/rtcdp/understanding-the-real-time-customer-data-platform.html) : integra datos en todas las fuentes de datos para impulsar la campaña. A continuación, estos datos se utilizan para crear las audiencias de campaña y los elementos de datos personalizados de superficie que se utilizan en los mosaicos de promo de correo electrónico y web (por ejemplo, nombre o información relacionada con la cuenta). El CDP también se utiliza para activar audiencias en el correo electrónico y la web (a través de [!DNL Adobe Target]).
   * [Esquemas](/help/xdm/home.md)
   * [Perfiles](/help/profile/home.md)
   * [Conjuntos de datos](/help/catalog/datasets/overview.md)
   * [Audiencias](/help/segmentation/home.md)
   * [[!DNL Adobe Journey Optimizer]](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/journey.html)
   * [Destinos](/help/destinations/home.md)
   * [Evento o Déclencheur de audiencia](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioning/collect-event-data/data-collection.html)
   * [Audiencias/ Eventos](https://experienceleague.adobe.com/docs/journey-optimizer/using/audiences-profiles-identities/audiences/about-audiences.html)
   * [Acciones de recorrido](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/journey.html)

### Cómo lograr el caso de uso: información general de alto nivel {#achieve-the-use-case-high-level}

A continuación se ofrece una descripción general de alto nivel de los tres recorridos de renovación de la participación.

>[!BEGINTABS]

>[!TAB Recorrido de renovación de participación]

El recorrido de renovación de la participación se dirige a la navegación de productos abandonados tanto en el sitio web como en la aplicación móvil. Este recorrido se activa cuando se ha visto un producto, pero no se ha comprado ni añadido al carro de compras. La participación de la marca se activa después de tres días si no se han realizado adiciones a la lista en las últimas 24 horas.<p>![Resumen visual de alto nivel del recorrido inteligente de renovación de la participación del cliente.](../intelligent-re-engagement/images/re-engagement-journey.png "Resumen visual de alto nivel del recorrido inteligente de renovación de la participación del cliente."){width="2560" zoomable="yes"}</p>

1. Puede crear esquemas y conjuntos de datos y luego marcar para [!UICONTROL Perfil].
2. Los datos se integran en Experience Platform mediante el SDK web, el SDK móvil de Edge o la API. El conector de datos de Analytics también se puede utilizar, pero puede provocar una latencia de recorrido.
3. Los perfiles se cargan en Real-Time CDP y se crean políticas de gobernanza para garantizar un uso responsable.
4. Las audiencias se generan centradas en la lista de perfiles para comprobar si **cliente** ha realizado un compromiso en los últimos tres días.
5. Puede crear un recorrido de renovación de participación en [!DNL Adobe Journey Optimizer].
6. Si es necesario, trabaje con **socio de datos** para la activación de audiencias en destinos de medios de pago deseados.
7. [!DNL Adobe Journey Optimizer] comprueba el consentimiento y envía las distintas acciones configuradas.

>[!TAB Recorrido de carro abandonado]

El recorrido de carrito abandonado se dirige a productos que se han incluido en el carrito, pero que aún no se han comprado ni en el sitio web ni en la aplicación móvil. Además, las campañas de medios de pago se inician y se detienen mediante este método.<p>![Resumen visual de alto nivel del recorrido del carro de compras abandonado por el cliente.](../intelligent-re-engagement/images/abandoned-cart-journey.png "Resumen visual de alto nivel del recorrido del carro de compras abandonado por el cliente."){width="2560" zoomable="yes"}</p>

1. Se crean esquemas y conjuntos de datos, la marca para [!UICONTROL Perfil].
2. Los datos se integran en Experience Platform mediante el SDK web, el SDK móvil de Edge o la API. El conector de datos de Analytics también se puede utilizar, pero puede provocar una latencia de recorrido.
3. Los perfiles se cargan en Real-Time CDP y se crean políticas de gobernanza para garantizar un uso responsable.
4. Las audiencias se generan centradas en la lista de perfiles para comprobar si **cliente** ha colocado un artículo en su carro de compras, pero no ha completado la compra. El **[!UICONTROL Añadir al carro de compras]** Este evento desencadena un temporizador que espera durante 30 minutos y, a continuación, comprueba la compra. Si no se ha realizado ninguna compra, la variable **cliente** se añade a **[!UICONTROL Abandonar carro]** audiencias.
5. Puede crear un recorrido de carro de compras abandonado en [!DNL Adobe Journey Optimizer].
6. Si es necesario, trabaje con **socio de datos** para la activación de audiencias en destinos de medios de pago deseados.
7. [!DNL Adobe Journey Optimizer] comprueba el consentimiento y envía las distintas acciones configuradas.

>[!TAB Recorrido de confirmación de pedido]

El recorrido de confirmación de pedido se centra en las compras de productos realizadas a través del sitio web y la aplicación móvil.<p>![Resumen visual de alto nivel del recorrido de confirmación de pedido del cliente.](../intelligent-re-engagement/images/order-confirmation-journey.png "Resumen visual de alto nivel del recorrido de confirmación de pedido del cliente."){width="2560" zoomable="yes"}</p>

1. Puede crear esquemas y conjuntos de datos y luego marcar para [!UICONTROL Perfil].
2. Los datos se integran en Experience Platform mediante el SDK web, el SDK móvil de Edge o la API. El conector de datos de Analytics también se puede utilizar, pero puede provocar una latencia de recorrido.
3. Los perfiles se cargan en Real-Time CDP y se crean políticas de gobernanza para garantizar un uso responsable.
4. Puede crear un recorrido de confirmación en [!DNL Adobe Journey Optimizer].
5. [!DNL Adobe Journey Optimizer] envía un mensaje de confirmación de pedido utilizando el canal preferido.

>[!ENDTABS]

## Cómo lograr el caso de uso: Instrucciones paso a paso {#step-by-step-instructions}

Para completar cada uno de los pasos de la información general de alto nivel anterior, lea las secciones siguientes, que ofrecen vínculos a más información e instrucciones más detalladas.

### Funcionalidad y elementos de la interfaz de usuario que utilizará {#ui-functionality-and-elements}

A medida que complete los pasos para implementar el caso de uso, utilizará la funcionalidad de Real-Time CDP y los elementos de la interfaz de usuario enumerados al principio de este documento. Asegúrese de que dispone de los permisos de control de acceso basados en atributos necesarios para todas estas áreas o solicite al administrador del sistema que le conceda los permisos necesarios.

### Crear un diseño de esquema y especificar grupos de campos

Los recursos del Modelo de datos de experiencia (XDM) se administran en la variable [!UICONTROL Esquemas] workspace en [!DNL Adobe Experience Platform]. Puede ver y explorar los recursos principales proporcionados por [!DNL Adobe] (por ejemplo, [!UICONTROL Grupos de campos]) y cree recursos y esquemas personalizados para su organización.

Para obtener más información sobre la creación de [esquemas](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html?lang=es), lea la [tutorial de creación de esquemas.](/help/xdm/tutorials/create-schema-ui.md)

Hay cuatro diseños de esquema que se utilizan para el caso de uso de renovación de la participación. Cada esquema requiere que se configuren campos específicos y algunos campos son muy recomendables.

#### Esquema de atributos del cliente

Este esquema se utiliza para estructurar y hacer referencia a los datos de perfil que conforman la información de clientes. Estos datos se suelen introducir en [!DNL Adobe Experience Platform] a través de su CRM o sistema similar, y es necesario para hacer referencia a los detalles del cliente que se utilizan para la personalización, el consentimiento de marketing y las funciones de segmentación mejoradas.

El esquema de atributos del cliente se representa mediante una variable [!UICONTROL Perfil individual de XDM] , que incluye los siguientes grupos de campos:

+++Datos personales de contacto (grupo de campos)

[Datos personales de contacto](/help/xdm/field-groups/profile/personal-contact-details.md) es un grupo de campos de esquema estándar para la clase de perfil individual de XDM que describe la información de contacto de una persona individual.

| Campos | Requisito | Descripción |
| --- | --- | --- |
| `mobilePhone.number` | Requerido | Número de teléfono móvil de la persona, que se utilizará para los SMS. |
| `personalEmail.address` | Requerido | La dirección de correo electrónico de la persona. |

+++

+++Datos demográficos (grupo de campos)

[Datos demográficos](/help/xdm/field-groups/profile/demographic-details.md) es un grupo de campos de esquema estándar para la clase de perfil individual de XDM. El grupo de campos proporciona un objeto person de nivel raíz, cuyos subcampos describen información sobre una persona individual.

| Campos | Requisito |
| --- | --- |
| `person.name.firstName` | Sugerido |
| `person.name.lastName` | Sugerido |

+++

+++Detalles de auditoría del sistema de origen externo (grupo de campos)

[Atributos de auditoría del sistema de origen externo](/help/xdm/data-types/external-source-system-audit-attributes.md) es un tipo de datos estándar del Modelo de datos de experiencia (XDM) que captura detalles de auditoría sobre un sistema de origen externo.

+++

+++Grupos de campos de consentimiento y preferencia (grupo de campos)

[Los consentimientos y preferencias](/help/xdm/field-groups//profile/consents.md) grupo de campos proporciona un único campo de tipo de objeto, consentimientos, para capturar información de consentimiento y preferencia.

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

Este grupo de campos se utiliza como práctica recomendada.

+++

#### Esquema de transacciones digitales del cliente

Este esquema se utiliza para estructurar y hacer referencia a los datos de evento que componen la actividad del cliente que se produce en el sitio web o en las plataformas digitales asociadas. Estos datos se suelen introducir en [!DNL Adobe Experience Platform] a través del SDK web y es necesario para hacer referencia a los distintos eventos de exploración y conversión que se utilizan para activar recorridos, análisis de clientes en línea detallado y funcionalidades de segmentación mejoradas.

El esquema de transacciones digitales del cliente se representa mediante una [!UICONTROL ExperienceEvent de XDM] , que incluye los siguientes grupos de campos:

+++ExperienceEvent del SDK web de Adobe Experience Platform (grupo de campos)

| Campos | Requisito |
| --- | --- |
| `device.model` | Sugerido |
| `environment.browserDetails.userAgent` | Sugerido |

+++

+++Detalles web (grupo de campos)

Detalles web es un grupo de campos de esquema estándar para la clase XDM ExperienceEvent, que se utiliza para describir información sobre los eventos de detalles web, como la interacción, los detalles de página y el referente.

| Campos | Requisito | Descripción |
| --- | --- | --- |
| `web.webInteraction.linkClicks.id` | Sugerido | ID del vínculo web o URL que corresponde a la interacción. |
| `web.webInteraction.linkClicks.value` | Sugerido | El número de clics para el vínculo web o la URL que corresponde a la interacción. |
| `web.webInteraction.name` | Sugerido | Nombre de la página web. |
| `web.webInteraction.URL` | Sugerido | Dirección URL de la página web. |
| `web.webPageDetails.name` | Sugerido | Nombre de la página web donde se produjo la interacción web. |
| `web.webPageDetails.URL` | Sugerido | Dirección URL de la página web donde se produjo la interacción web. |
| `web.webReferrer.URL` | Sugerido | Describe el referente de una interacción web, que es la URL de la que viene un visitante inmediatamente antes de que se registre la interacción web actual. |

+++

+++Evento de experiencia del consumidor (grupo de campos)

| Campos | Requisito |
| --- | --- |
| `commerce.cart.cartID` | Sugerido |
| `commerce.cart.cartSource` | Sugerido |
| `commerce.cartAbandons.id` | Sugerido |
| `commerce.cartAbandons.value` | Sugerido |
| `commerce.order.orderType` | Sugerido |
| `commerce.order.payments.paymentAmount` | Sugerido |
| `commerce.order.payments.paymentType` | Sugerido |
| `commerce.order.payments.transactionID` | Sugerido |
| `commerce.order.priceTotal` | Sugerido |
| `commerce.order.purchaseID` | Sugerido |
| `commerce.productListAdds.id` | Sugerido |
| `commerce.productListAdds.value` | Sugerido |
| `commerce.productListOpens.id` | Sugerido |
| `commerce.productListOpens.value` | Sugerido |
| `commerce.productListRemoval.id` | Sugerido |
| `commerce.productListRemoval.value` | Sugerido |
| `commerce.productListViews.id` | Sugerido |
| `commerce.productListViews.value` | Sugerido |
| `commerce.productViews.id` | Sugerido |
| `commerce.productViews.value` | Sugerido |
| `commerce.purchases.id` | Sugerido |
| `commerce.purchases.value` | Sugerido |
| `marketing.campaignGroup` | Sugerido |
| `marketing.campaignName` | Sugerido |
| `marketing.trackingCode` | Sugerido |
| `productListItems.name` | Sugerido |
| `productListItems.priceTotal` | Sugerido |
| `productListItems.product` | Sugerido |
| `productListItems.quantity` | Sugerido |

+++

+++Detalles del ID del usuario final (grupo de campos)

| Campos | Requisito | Descripción |
| --- | --- | --- |
| `endUserIDs._experience.emailid.authenticatedState` | Requerido | Estado autenticado de ID de dirección de correo electrónico del usuario final. |
| `endUserIDs._experience.emailid.id` | Requerido | ID de dirección de correo electrónico del usuario final. |
| `endUserIDs._experience.emailid.namespace.code` | Requerido | Código de área de nombres de ID de dirección de correo electrónico del usuario final. |
| `endUserIDs._experience.mcid.authenticatedState` | Requerido | [!DNL Adobe] Estado autenticado de ID de Marketing Cloud (ECID). El MCID ahora se conoce como ID de Experience Cloud (ECID). |
| `endUserIDs._experience.mcid.id` | Requerido | [!DNL Adobe] ID DE Marketing Cloud (MCID). El MCID ahora se conoce como ID de Experience Cloud (ECID). |
| `endUserIDs._experience.mcid.namespace.code` | Requerido | [!DNL Adobe] Código del área de nombres de ID de Marketing Cloud (MCID). |

+++

+++Detalles de auditoría del sistema de origen externo (grupo de campos)

Los atributos de auditoría del sistema de origen externo son un tipo de datos estándar del Modelo de datos de experiencia (XDM) que captura detalles de auditoría sobre un sistema de origen externo.

+++

#### Esquema de transacciones sin conexión del cliente

Este esquema se utiliza para estructurar y hacer referencia a los datos de evento que conforman la actividad de cliente que se produce en plataformas fuera del sitio web. Estos datos se suelen introducir en [!DNL Adobe Experience Platform] desde un POS (o sistema similar) y, con mayor frecuencia, se transmite a Platform a través de una conexión API. Su propósito es hacer referencia a los distintos eventos de conversión sin conexión que se utilizan para activar recorridos, realizar análisis de clientes en línea y sin conexión profundos y mejorar las capacidades de segmentación.

El esquema de transacciones sin conexión del cliente se representa mediante una [!UICONTROL ExperienceEvent de XDM] , que incluye los siguientes grupos de campos:

+++Detalles de comercio (grupo de campos)

| Campos | Requisito | Descripción |
| --- | --- | --- |
| `commerce.cart.cartID` | Requerido | ID del carro de compras. |
| `commerce.order.orderType` | Requerido | Un objeto que describe el tipo de pedido del producto. |
| `commerce.order.payments.paymentAmount` | Requerido | Un objeto que describe el importe de pago del pedido del producto. |
| `commerce.order.payments.paymentType` | Requerido | Un objeto que describe el tipo de pago de pedido de producto. |
| `commerce.order.payments.transactionID` | Requerido | Un ID de transacción de pedido de producto de objeto. |
| `commerce.order.purchaseID` | Requerido | ID de compra de pedido de producto de objeto. |
| `productListItems.name` | Requerido | Una lista de nombres de artículos que representa los productos seleccionados por un cliente. |
| `productListItems.priceTotal` | Requerido | El precio total de la lista de artículos que representan los productos seleccionados por un cliente. |
| `productListItems.product` | Requerido | El producto o los productos seleccionados. |
| `productListItems.quantity` | Requerido | La cantidad de artículos que representan los productos seleccionados por un cliente. |

+++

+++Datos personales de contacto (grupo de campos)

| Campos | Requisito | Descripción |
| --- | --- | --- |
| `mobilePhone.number` | Requerido | Número de teléfono móvil de la persona, que se utilizará para los SMS. |
| `personalEmail.address` | Requerido | La dirección de correo electrónico de la persona. |

+++

+++Detalles de auditoría del sistema de origen externo (grupo de campos)

Los atributos de auditoría del sistema de origen externo son un tipo de datos estándar del Modelo de datos de experiencia (XDM) que captura detalles de auditoría sobre un sistema de origen externo.

+++

#### esquema del conector web de Adobe

>[!NOTE]
>
>Esta es una implementación opcional si utiliza [!DNL Adobe Analytics Data Connector].

Este esquema se utiliza para estructurar y hacer referencia a los datos de evento que componen la actividad del cliente que se produce en el sitio web o en las plataformas digitales asociadas. Este esquema es similar al esquema de transacciones digitales del cliente, pero difiere en que está pensado para utilizarse cuando el SDK web no es una opción para la recopilación de datos; por lo tanto, este esquema es necesario cuando se utiliza el [!DNL Adobe Analytics Data Connector] para enviar los datos en línea a [!DNL Adobe Experience Platform] como conjunto de datos principal o secundario.

El [!DNL Adobe] el esquema del conector web se representa mediante una variable [!UICONTROL ExperienceEvent de XDM] , que incluye los siguientes grupos de campos:

Plantilla de ExperienceEvent de +++Adobe Analytics (grupo de campos)

| Campos | Requisito | Descripción |
| --- | --- | --- |
| `web.webInteraction.linkClicks.id` | Sugerido | ID del vínculo web o URL que corresponde a la interacción. |
| `web.webInteraction.linkClicks.value` | Sugerido | El número de clics para el vínculo web o la URL que corresponde a la interacción. |
| `web.webInteraction.name` | Sugerido | Nombre de la página web. |
| `web.webInteraction.URL` | Sugerido | Dirección URL de la página web. |
| `web.webPageDetails.name` | Sugerido | Nombre de la página web donde se produjo la interacción web. |
| `web.webPageDetails.URL` | Sugerido | Dirección URL de la página web donde se produjo la interacción web. |
| `web.webReferrer.URL` | Sugerido | Describe el referente de una interacción web, que es la URL de la que viene un visitante inmediatamente antes de que se registre la interacción web actual. |
| `commerce.cart.cartID` | Sugerido | |
| `commerce.cart.cartSource` | Sugerido | |
| `commerce.cartAbandons.id` | Sugerido | |
| `commerce.cartAbandons.value` | Sugerido | |
| `commerce.order.orderType` | Sugerido | |
| `commerce.order.payments.paymentAmount` | Sugerido | |
| `commerce.order.payments.paymentType` | Sugerido | |
| `commerce.order.payments.transactionID` | Sugerido | |
| `commerce.order.priceTotal` | Sugerido | |
| `commerce.order.purchaseID` | Sugerido | |
| `commerce.productListAdds.id` | Sugerido | |
| `commerce.productListAdds.value` | Sugerido | |
| `commerce.productListOpens.id` | Sugerido | |
| `commerce.productListOpens.value` | Sugerido | |
| `commerce.productListRemoval.id` | Sugerido | |
| `commerce.productListRemoval.value` | Sugerido | |
| `commerce.productListViews.id` | Sugerido | |
| `commerce.productListViews.value` | Sugerido | |
| `commerce.productViews.id` | Sugerido | |
| `commerce.productViews.value` | Sugerido | |
| `commerce.purchases.id` | Sugerido | |
| `commerce.purchases.value` | Sugerido | |
| `marketing.campaignGroup` | Sugerido | |
| `marketing.campaignName` | Sugerido | |
| `marketing.trackingCode` | Sugerido | |
| `productListItems.name` | Sugerido | |
| `productListItems.priceTotal` | Sugerido | |
| `productListItems.product` | Sugerido | |
| `productListItems.quantity` | Sugerido | |
| `endUserIDs._experience.emailid.authenticatedState` | Requerido | Estado autenticado de ID de dirección de correo electrónico del usuario final. |
| `endUserIDs._experience.emailid.id` | Requerido | ID de dirección de correo electrónico del usuario final. |
| `endUserIDs._experience.emailid.namespace.code` | Requerido | Código de área de nombres de ID de dirección de correo electrónico del usuario final. |
| `endUserIDs._experience.mcid.authenticatedState` | Requerido | [!DNL Adobe] Estado autenticado de ID de Marketing Cloud (ECID). El MCID ahora se conoce como ID de Experience Cloud (ECID). |
| `endUserIDs._experience.mcid.id` | Requerido | [!DNL Adobe] ID DE Marketing Cloud (MCID). El MCID ahora se conoce como ID de Experience Cloud (ECID). |
| `endUserIDs._experience.mcid.namespace.code` | Requerido | [!DNL Adobe] Código del área de nombres de ID de Marketing Cloud (MCID). |

+++

+++Valor de clase (grupo de campos)

| Campos | Requisito |
| --- | --- |
| `eventType` | Requerido |
| `timestamp` | Requerido |

+++

+++Detalles de auditoría del sistema de origen externo (grupo de campos)

Los atributos de auditoría del sistema de origen externo son un tipo de datos estándar del Modelo de datos de experiencia (XDM) que captura detalles de auditoría sobre un sistema de origen externo.

+++

### Creación de un conjunto de datos a partir de un esquema

Un conjunto de datos es una estructura de almacenamiento y administración para un grupo de datos. Cada esquema para los recorridos inteligentes de renovación de la participación tiene un único conjunto de datos.

Para obtener más información sobre cómo crear un [conjunto de datos](/help/catalog/datasets/overview.md) desde un esquema, lea la [Guía de IU de conjuntos de datos](/help/catalog/datasets/user-guide.md).

>[!NOTE]
>
>Similar al paso para crear un esquema, debe habilitar el conjunto de datos para que se incluya en el Perfil del cliente en tiempo real. Para obtener más información sobre la activación del conjunto de datos para su uso en el Perfil del cliente en tiempo real, lea la [tutorial de creación de esquemas.](/help/xdm/tutorials/create-schema-ui.md#profile).

### Privacidad, consentimiento y control de datos

#### Políticas de consentimiento

>[!IMPORTANT]
>
>Proporcionar a los clientes la capacidad de cancelar la suscripción a la recepción de comunicaciones de una marca es un requisito legal, así como garantizar que se cumpla esta opción. Obtenga más información acerca de la legislación aplicable en la [Documentación de Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/privacy/regulations/overview.html).

Al crear una ruta de renovación de la participación, se deben tener en cuenta las siguientes políticas de consentimiento:

* If `consents.marketing.email.val = "Y"` entonces Puede enviar por correo electrónico
* If `consents.marketing.sms.val = "Y"` entonces Puede SMS
* If `consents.marketing.push.val = "Y"` entonces Puede insertar
* If `consents.share.val = "Y"` Entonces puede anunciarse

#### Etiqueta y aplicación DULE

Al crear una ruta de renovación de la participación, se deben tener en cuenta las siguientes etiquetas DULE:

* Las direcciones de correo electrónico personales se utilizan como datos de identificación directa que se utilizan para identificar a una persona específica o ponerse en contacto con ella, en lugar de con un dispositivo.
   * `personalEmail.address = I1`

#### Políticas de marketing

No se requieren políticas de marketing para los recorridos de renovación de la participación; sin embargo, se debe tener en cuenta lo siguiente:

* Restringir datos confidenciales
* Restringir publicidad in situ
* Restringir direccionamiento de correo electrónico
* Restringir la segmentación entre sitios
* Restringir la combinación de datos directamente identificables con datos anónimos

### Crear una audiencia

#### Creación de audiencias para recorridos de renovación de la participación de la marca

Los recorridos de renovación de la participación utilizan audiencias para definir atributos o comportamientos específicos compartidos por un subconjunto de perfiles del almacén de perfiles para distinguir un grupo comercializable de personas de la base de clientes. Las audiencias se pueden crear de varias formas en [!DNL Adobe Experience Platform].

Para obtener más información sobre cómo componer directamente [Audiencias](/help/segmentation/home.md), lea la [Guía de IU de composición de audiencia](/help/segmentation/ui/audience-composition.md).

Para obtener más información sobre cómo crear audiencias a través de definiciones de segmentos derivadas de Platform, lea la [Guía de IU de Audience Builder](/help/segmentation/ui/segment-builder.md).

>[!BEGINTABS]

>[!TAB Recorrido de renovación de participación]

Esta audiencia se crea como una mejora del escenario clásico &quot;Abandono del carro de compras&quot;. Mientras que el abandono del carro de compras generalmente se centra en la adición de un carro de compras sin una compra posterior en un período de tiempo determinado, esta audiencia busca una participación anterior, específicamente aquellos que pueden haber explorado un producto en particular, pero no lo agregaron al carro de compras y no tuvieron actividad de seguimiento en el sitio dentro de un marco de tiempo determinado. Esta audiencia le ayuda a mantener su marca &quot;en la mente&quot; de los clientes que cumplen con estos criterios de inclusión y también se puede aprovechar para clientes cuyas propiedades digitales pueden diferir de un modelo de comercio electrónico tradicional.

Los siguientes eventos se utilizan para el recorrido de renovación de la participación, en el que los usuarios vieron los productos en línea y no agregaron al carro de compras en las siguientes 24 horas, seguido de sin participación de la marca en los 3 días siguientes.

Se requieren los campos y las condiciones siguientes al configurar esta audiencia:

* `EventType: commerce.productViews`
   * `Timestamp: <= 24 hours before now`
* `EventType is not: commerce.procuctListAdds`
   * `Timestamp: <= 24 hours before now, GAP(>= 3 days)`
* `EventType: application.launch or web.webpagedetails.pageViews or commerce.purchases`
   * `Timestamp: <= 2 days before now`

El descriptor del recorrido de renovación de participación aparece de la siguiente manera:

`Include audience who have at least 1 EventType = ProductViews event THEN have at least 1 Any event where (EventType does not equal commerce.productListAdds) and occurs in last 24 hour(s) then after 3 days do not have any Any event where (EventType = application.launch or web.webpagedetails.pageViews or commerce.purchases) and occurs in last 2 day(s).`

>[!TAB Recorrido de carro abandonado]

Esta audiencia se crea para admitir el escenario clásico &quot;Abandono del carro de compras&quot;. Su propósito es encontrar clientes que agregaron un producto al carro de compras, pero que finalmente no siguieron con una compra. Esta audiencia ayudará a mantener no solo su marca &quot;en mente&quot; para sus clientes, sino también los productos que dejaron atrás sin una compra posterior.

Los siguientes eventos se utilizan para el recorrido de carro de compras abandonado, en el que los usuarios agregaron un producto al carro de compras, pero no completaron la compra ni borraron el carro de compras en las últimas 24 horas.

Se requieren los campos y las condiciones siguientes al configurar esta audiencia:

* `EventType: commerce.productListAdds`
   * `Timestamp: >= 1 days before now and <= 4 days before now `
* `EventType: commerce.purchases`
   * `Timestamp: <= 4 days before now`
* `EventType: commerce.productListRemovals`
   * `Timestamp: <= 4 days before now`

El descriptor del recorrido de carro de compras abandonado aparece de la siguiente manera:

`Include EventType = commerce.productListAdds between 30 min and 1440 minutes before now. exclude EventType = commerce.purchases 30 minutes before now OR EventType = commerce.productListRemovals AND Cart ID equals Product List Adds1 Cart ID (the inclusion event).`

>[!ENDTABS]

### Configuración del recorrido en Adobe Journey Optimizer

>[!NOTE]
>
>[!DNL Adobe Journey Optimizer] no abarca todo lo que se muestra en los diagramas. Todos los anuncios de medios de pago se crean en [!UICONTROL Destinos].

[[!DNL Adobe Journey Optimizer]](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/journey.html) le ayuda a ofrecer experiencias conectadas, contextuales y personalizadas a sus clientes. El recorrido del cliente es todo el proceso de interacción de un cliente con la marca. Cada recorrido de caso de uso requiere información específica. A continuación se enumeran los datos precisos necesarios para cada rama de Recorrido.

>[!BEGINTABS]

>[!TAB Recorrido de renovación de participación]

El recorrido de renovación de la participación se dirige a la navegación de productos abandonados tanto en el sitio web como en la aplicación móvil.<p>![Resumen visual de alto nivel del recorrido inteligente de renovación de la participación del cliente.](../intelligent-re-engagement/images/re-engagement-journey.png "Resumen visual de alto nivel del recorrido inteligente de renovación de la participación del cliente."){width="2560" zoomable="yes"}</p>

+++Eventos

* Evento 1: Vistas del producto
   * Esquema: Transacciones digitales del cliente
   * Campos:
      * `EventType`
   * Condición:
      * `EventType = commerce.productViews`
      * Campos:
         * `Commerce.productViews.id`
         * `Commerce.productViews.value`
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

* Evento 2: Agregar al carro
   * Esquema: Transacciones digitales del cliente
   * Campos:
      * `EventType`
   * Condición:
      * `EventType = commerce.productListAdds`
      * Campos:
         * `Commerce.productListAdds.id`
         * `Commerce.productListAdds.value`
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
      * `EventType`
   * Condición:
      * `EventType in application.launch, commerce.purchases, web.webpagedetails.pageViews`
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
         * `Commerce.purchases.id`
         * `Commerce.purchases.value`
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

+++Lógica de Recorrido de claves

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

   * Personalización de canal
      * Contenido de canal personalizado basado en la vista del producto.

+++

>[!TAB Recorrido de carro abandonado]

El recorrido de carrito abandonado se dirige a productos que se han incluido en el carrito, pero que aún no se han comprado ni en el sitio web ni en la aplicación móvil.<p>![Resumen visual de alto nivel del recorrido del carro de compras abandonado por el cliente.](../intelligent-re-engagement/images/abandoned-cart-journey.png "Resumen visual de alto nivel del recorrido del carro de compras abandonado por el cliente."){width="2560" zoomable="yes"}</p>

+++Eventos

* Evento 2: Agregar al carro
   * Esquema: Transacciones digitales del cliente
   * Campos:
      * `EventType`
   * Condición:
      * `EventType = commerce.productListAdds`
      * Campos:
         * `Commerce.productListAdds.id`
         * `Commerce.productListAdds.value`
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
      * `EventType`
   * Condición:
      * `EventType = commerce.purchases`
      * Campos:
         * `Commerce.purchases.id`
         * `Commerce.purchases.value`
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
      * `EventType`
   * Condición:
      * `EventType in application.launch, commerce.purchases, web.webpagedetails.pageViews`
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
         * `Commerce.purchases.id`
         * `Commerce.purchases.value`
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

+++Lógica de Recorrido de claves

* Lógica de entrada de recorrido
   * `AddToCart` Evento

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
   * Personalización de canal
      * Muestra información detallada del carro de compras y puede mostrar varios productos en formato de tabla.

+++

>[!TAB Recorrido de confirmación de pedido]

El recorrido de confirmación de pedido se centra en las compras de productos realizadas a través del sitio web y la aplicación móvil.<p>![Resumen visual de alto nivel del recorrido de confirmación de pedido del cliente.](../intelligent-re-engagement/images/order-confirmation-journey.png "Resumen visual de alto nivel del recorrido de confirmación de pedido del cliente."){width="2560" zoomable="yes"}</p>

+++Eventos

* Evento 4: Compras en línea
   * Esquema: Transacciones digitales del cliente
   * Campos:
      * `EventType`
   * Condición:
      * `EventType = commerce.purchases`
      * Campos:
         * `Commerce.purchases.id`
         * `Commerce.purchases.value`
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

+++Lógica de Recorrido de claves

* Lógica de entrada de recorrido
   * Evento de pedido

* Condiciones
   * Seleccionar canal de destino (seleccione uno o varios canales para ampliar el alcance).
      * La confirmación de pedido se considera una prestación por naturaleza, por lo que la comprobación del consentimiento suele ser innecesaria.
      * Correo electrónico
      * Push
      * SMS

   * Personalización del contenido del canal
      * Muestra información detallada del pedido y puede mostrar una lista de productos con un formato de tabla.

+++

>[!ENDTABS]

Para obtener más información sobre la creación de recorridos en [!DNL Adobe Journey Optimizer], lea la [Guía de introducción a recorrido](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/journey.html).

### Configuración de anuncios de medios de pago en destinos

El marco de destinos se utiliza para anuncios de medios de pago. Una vez comprobado el consentimiento, se envía a los distintos destinos configurados. Para obtener más información sobre los destinos, lea la [Resumen de destinos](/help/destinations/home.md) documento.

#### Datos necesarios para los destinos

Los destinos de exportación de segmentos de streaming (como Facebook, Google Customer Match o Google DV360) admiten varias identidades a partir de los datos del cliente:

* `personalEmail.address`
* `ECID`
* `mobilePhone.number`

El segmento de carro de compras abandonado se está transmitiendo y, por lo tanto, el marco de trabajo de destino puede utilizarlo para este caso de uso.

* Transmisión/Activado
   * [Publicidad](/help/destinations/catalog/advertising/overview.md)/[Medios de pago y medios sociales](/help/destinations/catalog/social/overview.md)
   * [Dispositivo móvil](/help/destinations/catalog/mobile-engagement/overview.md)
   * [Destino de streaming](/help/destinations/catalog/streaming/http-destination.md)
   * [Destination SDK personalizado](/help/destinations/destination-sdk/overview.md)

* Archivo/Programado cada tres horas
   * [Marketing por correo electrónico](/help/destinations/catalog/email-marketing/overview.md)
