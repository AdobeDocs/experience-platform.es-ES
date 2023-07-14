---
keywords: destinos; preguntas; preguntas más frecuentes; faq; destinos faq
title: Preguntas frecuentes
description: Respuestas a las preguntas más frecuentes sobre destinos de Adobe Experience Platform
exl-id: 2c34ecd0-a6d0-48dd-86b0-a144a6acf61a
source-git-commit: 165793619437f403045b9301ca6fa5389d55db31
workflow-type: tm+mt
source-wordcount: '1395'
ht-degree: 4%

---

# Preguntas frecuentes {#faq}

## Información general {#overview}

Este documento proporciona respuestas a las preguntas frecuentes acerca de los destinos de Adobe Experience Platform. Para preguntas y resolución de problemas relacionados con otros [!DNL Platform] servicios, incluidos los que se encuentran en todos los [!DNL Platform] API, consulte la [guía de solución de problemas del Experience Platform](../landing/troubleshooting.md).

## Preguntas sobre destinos generales {#general}

### ¿Por qué veo diferentes recuentos de perfiles en la interfaz de usuario de Experience Platform y en los archivos CSV exportados?

+++Respuesta: Se trata de un comportamiento normal debido a la forma en que el Experience Platform realiza la segmentación.

La segmentación por lotes actualiza el recuento de perfiles de las audiencias de streaming a lo largo del día, mientras que la segmentación por lotes actualiza el recuento de perfiles de las audiencias por lotes una vez cada 24 horas.

Cuando la programación de exportación de la audiencia difiere de la programación de segmentación, el perfil cuenta entre la interfaz de usuario y el contenido exportado [!DNL CSV] El archivo será diferente, especialmente cuando se trata de audiencias de streaming.

Consulte la [Documentación del Servicio de segmentación](../segmentation/home.md) para obtener más información.
+++

## [!DNL Facebook Custom Audiences] {#facebook-faq}

### ¿Qué debo hacer antes de poder activar audiencias en? [!DNL Facebook Custom Audiences]?

+++Responda Antes de enviar sus audiencias a [!DNL Facebook], asegúrese de cumplir los siguientes requisitos:

* Su [!DNL Facebook] la cuenta de usuario debe tener el **[!DNL Manage campaigns]** permiso habilitado para la cuenta de Ad que planea usar.
* El **Adobe Experience Cloud** La cuenta comercial de debe añadirse como socio de publicidad en su [!DNL Facebook Ad Account]. En su lugar, utilice `business ID=206617933627973`. Consulte [Añadir socios a su administrador comercial](https://www.facebook.com/business/help/1717412048538897) en la documentación de Facebook para obtener más información.
  >[!IMPORTANT]
  >
  > Al configurar los permisos para Adobe Experience Cloud, debe habilitar la variable **Administración de campañas** permiso. Es necesario para la integración de [!DNL Adobe Experience Platform].
* Lea y firme el [!DNL Facebook Custom Audiences] Condiciones del servicio. Para ello, vaya a `https://business.facebook.com/ads/manage/customaudiences/tos/?act=[accountID]`, donde `accountID` es su [!DNL Facebook Ad Account ID].
+++

### ¿Debo agregar aplicaciones o píxeles a mi [!DNL Facebook] ¿cuenta del anunciante?

+++Nº de respuesta Como no se trata de una integración basada en píxeles, no es necesario añadir píxeles a la cuenta del anunciante.
+++

### ¿Cuánto tiempo tarda Facebook en procesar la información de Adobe Experience Platform?

+++Respuesta A partir de marzo de 2021, [!DNL Facebook Custom Audiences] necesita hasta una hora para procesar la información recibida de [!DNL Platform].
+++

### ¿Puedo usar [!DNL Facebook Custom Audiences] para la segmentación de audiencias en otros [!DNL Facebook] aplicaciones, como [!DNL Instagram]?

+++Respuesta Puede utilizar el [!DNL Facebook Custom Audiences] destino para la segmentación de audiencias en toda la familia de aplicaciones de Facebook compatibles con [!DNL Facebook Custom Audiences], incluido [!DNL Facebook], [!DNL Instagram], [!DNL Audience Network], y [!DNL Messenger]. La selección de la aplicación en la que los anunciantes desean ejecutar campañas se indica en el nivel de ubicación en [!DNL Facebook Ads Manager].
+++

### ¿Cuál es la diferencia entre las [!DNL Facebook Custom Audiences] conexión y [!DNL Facebook Pixel] ¿Extensión?

+++Responda Al [!DNL Facebook Custom Audiences] la conexión utiliza [!DNL Platform] identidades al enviar audiencias a [!DNL Facebook], mientras que el [[!DNL Facebook Pixel] conexión](../destinations/catalog/advertising/facebook-pixel.md) utiliza el [!DNL Facebook] píxel integrado en un sitio web.

Estas dos integraciones son complementarias; pueden utilizarse las dos para garantizar una mejor cobertura de audiencia. Por ejemplo, puede utilizar la variable [!DNL Facebook Pixel] extensión para la prospección de visitantes de sitios web que no hayan creado una cuenta, mientras que [!DNL Facebook Custom Audiences] puede ayudarle a segmentar clientes existentes según lo siguiente [!DNL Platform] identidades.
+++

### ¿La integración de Adobe Experience Platform con [!DNL Facebook Custom Audiences] admitir la descalificación de usuarios de una audiencia cuando ya no cumplen los requisitos para ella?**

+++Responda Sí, la integración admite la eliminación de usuarios de [!DNL Facebook Custom Audiences] cuando ya no cumplan los requisitos.
+++

### ¿Cómo debo hash los datos de audiencia antes de enviarlos a? [!DNL Facebook]?

+++Respuesta
[!DNL Facebook] requiere que no se envíe información de identificación personal (PII) de forma clara. Por lo tanto, las audiencias se activan para [!DNL Facebook] se puede cerrar con llave *con hash* identificadores, como direcciones de correo electrónico o números de teléfono.

Para obtener explicaciones detalladas sobre los requisitos de coincidencia de ID, consulte [Requisitos de coincidencia de ID](catalog/social/facebook.md#id-matching-requirements).
+++

### Qué tipo de identidades puedo activar en [!DNL Facebook Custom Audiences]?

+++Respuesta
[!DNL Facebook Custom Audiences] admite la activación de las siguientes identidades: correos electrónicos con hash, números de teléfono con hash, [!DNL GAID], [!DNL IDFA]y los ID externos personalizados.
+++

### ¿Puedo crear varios destinos de Facebook en la interfaz de usuario de Platform para cuentas de Facebook independientes?

+++Conteste Sí. Un destino de Facebook en Experience Platform es 1:1 en una cuenta de publicidad en Facebook. Puede crear un destino de Facebook independiente para cada cuenta de publicidad de Facebook de su compañía. Siga las [tutorial de conexión de destino](/help/destinations/ui/connect-destination.md) y conectarse a una cuenta de Facebook independiente para cada nuevo destino de Facebook en la interfaz de usuario de Platform. No hay límite en el número de cuentas de publicidad de Facebook a las que puede conectarse.
+++

## Coincidencia de clientes de Google {#google-customer-match}

### Al exportar audiencias a Customer Match de Google, ¿por qué veo números adicionales anexados al final de los nombres de audiencia en la interfaz de Google?

+++Answer Google requiere que los nombres de audiencia sean únicos. Los números que está viendo son [Marcas de tiempo UNIX](https://www.unixtimestamp.com/) y se anexan para mantener los nombres de audiencia únicos, si ha asignado la misma audiencia a varios destinos de Google.
+++

## Audiencias coincidentes de linkedIn {#linkedin}

### ¿Debo agregar aplicaciones o píxeles a mi [!DNL LinkedIn] ¿cuenta del anunciante?

+++Nº de respuesta Como no se trata de una integración basada en píxeles, no es necesario añadir píxeles a la cuenta del anunciante.
+++

### ¿Qué debo hacer antes de poder activar audiencias en? [!DNL LinkedIn Matched Audiences]?

+++Respuesta Antes de poder usar el [!UICONTROL Audiencia coincidente de linkedIn] destino, asegúrese de que su [!DNL LinkedIn Campaign Manager] La cuenta tiene el [!DNL Creative Manager] nivel de permiso o superior.

Para obtener información sobre cómo editar su [!DNL LinkedIn Campaign Manager] permisos de usuario, consulte [Agregar, editar y quitar permisos de usuario en cuentas publicitarias](https://www.linkedin.com/help/lms/answer/5753) en la documentación de LinkedIn.
+++

### ¿Cómo debo hash los datos de audiencia antes de enviarlos a? [!DNL LinkedIn]?

+++Respuesta
[!DNL LinkedIn] requiere que no se envíe información de identificación personal (PII) de forma clara. Por lo tanto, las audiencias se activan para [!DNL LinkedIn] se puede cerrar con llave *con hash* identificadores, como direcciones de correo electrónico o números de teléfono.

Para obtener explicaciones detalladas sobre los requisitos de coincidencia de ID, consulte [Requisitos de coincidencia de ID](catalog/social/linkedin.md#id-matching-requirements).
+++

### Qué tipo de identidades puedo activar en [!DNL LinkedIn]?

+++Respuesta
[!DNL LinkedIn Matched Audiences] admite la activación de las siguientes identidades: correos electrónicos con hash, [!DNL GAID], y [!DNL IDFA].
+++

## Personalización de la misma página y de la página siguiente mediante Adobe Target y destinos de Personalización personalizados {#same-next-page-personalization}

### ¿Debo utilizar el SDK web de Experience Platform para enviar audiencias y atributos a Adobe Target?

+++No de respuesta, [SDK web](../edge/home.md) no es necesario para activar audiencias en [Adobe Target](catalog/personalization/adobe-target-connection.md).

Sin embargo, si [[!DNL at.js]](https://experienceleague.adobe.com/docs/target-dev/developer/client-side/at-js-implementation/overview.html?lang=es) se utiliza en lugar del SDK web, solo se admite la personalización de la sesión siguiente.

Para [personalización de la misma página y de la página siguiente](ui/activate-edge-personalization-destinations.md) Casos de uso de, debe utilizar cualquiera de los siguientes [SDK web](../edge/home.md) o el [API del servidor de red perimetral](../server-api/overview.md). Consulte la documentación sobre [activación de audiencias en destinos Edge](ui/activate-edge-personalization-destinations.md) para obtener más información sobre la implementación.
+++

### ¿Hay un límite en el número de atributos que puedo enviar desde Real-time Customer Data Platform a Adobe Target o a un destino de personalización personalizado?

+++Responda Sí, los casos de uso de personalización de la misma página y de la siguiente página admiten un máximo de 30 atributos por zona protegida al activar audiencias en destinos de Adobe Target o Personalización personalizada. Consulte más información sobre las protecciones de activación en la [documentación sobre protecciones](guardrails.md#edge-destinations-activation).
+++

### ¿Qué tipos de atributos se admiten para la activación (por ejemplo, matrices, mapas, etc.)?

+++Responder Actualmente, solo se admiten atributos estáticos de un solo valor, como `person.name.firstName`. Actualmente no se admiten atributos de matriz.
+++

<!-- **Is there a limit on the number of audiences that can be activated to Adobe Target and Custom Personalization destinations?**

Yes, you can activate a maximum of 150 edge audiences per sandbox.  For more information on activation guardrails, see the [default guardrails for activation](guardrails.md#edge-destinations-activation). -->

### Después de crear una audiencia en Experience Platform, ¿cuánto tiempo tardará esa audiencia en estar disponible para los casos de uso de segmentación de Edge?

+++Las definiciones de audiencia de respuesta se propagan a [Red perimetral](../edge/home.md) hasta en una hora. Sin embargo, si se activa una audiencia en esta primera hora, se podrían perder algunos visitantes que habrían cumplido los requisitos para la audiencia.
+++

### ¿Dónde puedo ver los atributos activados en Adobe Target?

+++Los atributos de respuesta estarán disponibles para usarlos en Target en [JSON](https://experienceleague.adobe.com/docs/target/using/experiences/offers/create-json-offer.html) y [HTML](https://experienceleague.adobe.com/docs/target/using/experiences/offers/manage-content.html?lang=es) ofertas.
+++

### ¿Puedo crear un destino sin una secuencia de datos y luego agregar una secuencia de datos al mismo destino en un momento posterior?

+++Respuesta Actualmente, esto no es compatible con la interfaz de usuario de destinos. Si necesita ayuda en este caso, póngase en contacto con su representante del Adobe.
+++

### ¿Qué sucede si elimino un destino de Adobe Target?

+++Respuesta Cuando elimina un destino, todas las audiencias y atributos asignados bajo el destino se eliminan de Adobe Target y también se eliminan de la red perimetral.
+++

### ¿Funciona la integración con la API del servidor de red perimetral?

+++Responda Sí, la API del servidor de red perimetral funciona con el destino de Personalización personalizada. Dado que los atributos de perfil pueden contener datos confidenciales, para protegerlos, el destino de Personalización personalizada requiere que utilice la API del servidor de red perimetral para la recopilación de datos. Además, todas las llamadas de API deben realizarse en un [contexto autenticado](../server-api/authentication.md).
+++

### Solo puedo tener una política de combinación activa en Edge. ¿Puedo crear audiencias que utilicen una política de combinación diferente y seguir enviándolas a Adobe Target como audiencias de streaming?

+++Nº de respuesta Todas las audiencias que desee activar en Adobe Target deben utilizar un perfil activo en Edge [política de combinación](../profile/merge-policies/ui-guide.md).
+++

### ¿Se aplican las políticas de etiquetado y aplicación del uso de datos (Data Usage Labeling and Enforcement, DULE) y de consentimiento?

+++Conteste Sí. El [Gobernanza de datos y políticas de consentimiento](../data-governance/home.md) Las acciones de marketing creadas y asociadas con las seleccionadas rigen la activación de los atributos seleccionados.
+++
