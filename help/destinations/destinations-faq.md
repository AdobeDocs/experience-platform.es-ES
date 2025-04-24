---
keywords: destinos; preguntas; preguntas más frecuentes; faq; destinos faq
title: Preguntas frecuentes
description: Respuestas a las preguntas más frecuentes sobre destinos de Adobe Experience Platform
exl-id: 2c34ecd0-a6d0-48dd-86b0-a144a6acf61a
source-git-commit: 7f3459f678c74ead1d733304702309522dd0018b
workflow-type: tm+mt
source-wordcount: '1673'
ht-degree: 0%

---

# Preguntas frecuentes {#faq}

## Información general {#overview}

Este documento proporciona respuestas a las preguntas frecuentes acerca de los destinos de Adobe Experience Platform. Para preguntas y solucionar problemas relacionados con otros servicios de [!DNL Experience Platform], incluidos los que se encuentran en todas las API de [!DNL Experience Platform], consulte la [guía de solución de problemas de Experience Platform](../landing/troubleshooting.md).

## Preguntas sobre destinos generales {#general}

### ¿Por qué veo diferentes recuentos de perfiles en la interfaz de usuario de Experience Platform y en los archivos CSV exportados?

+++Respuesta
Se trata de un comportamiento normal debido al modo en que Experience Platform realiza la segmentación.

La segmentación por lotes actualiza el recuento de perfiles de las audiencias de streaming a lo largo del día, mientras que la segmentación por lotes actualiza el recuento de perfiles de las audiencias por lotes una vez cada 24 horas.

Cuando la programación de exportación de audiencias difiere de la programación de segmentación, los recuentos de perfiles entre la interfaz de usuario y el archivo [!DNL CSV] exportado serán diferentes, especialmente en lo que respecta a las audiencias de streaming.

Consulte la [documentación del servicio de segmentación](../segmentation/home.md) para obtener más información.
+++

### ¿Por qué veo tasas de coincidencia bajas al desactivar y reactivar una audiencia actualizada en el mismo destino?

+++Respuesta

La desactivación y eliminación de una audiencia desde un destino de flujo continuo no almacena en déclencheur un relleno tras la reactivación de la audiencia al mismo destino de flujo continuo.

**Ejemplo**

Ha activado una audiencia de 10 perfiles en un destino de flujo continuo.

Después de activar la audiencia, se da cuenta de que desea cambiar la configuración de la audiencia, por lo que desactiva la audiencia y cambia sus criterios de población, lo que da como resultado una población de audiencia de 100 perfiles.

La audiencia actualizada se vuelve a activar en el mismo destino, pero como no hay relleno activado, el destino no recibe los 90 perfiles adicionales.

**Solución**

Para asegurarse de que todos los perfiles se envían a su destino, debe crear una audiencia nueva con la nueva configuración y, a continuación, activarla en su destino.

+++

### Cuando se elimina una audiencia de un destino, ¿hay alguna señal que se envíe al destino que indique que se ha eliminado la audiencia?

+++Respuesta

No, no hay dependencia entre el destino de Experience Platform y la instancia de cliente del sistema de destino. En el lado receptor, la única indicación de que el sistema de destino vería es que dejó de recibir esos datos de audiencia.

+++

<!--
## [!DNL Experience Cloud Audiences] {#eca-faq}

### What are the differences between the Experience Cloud Audiences and Adobe Target destinations?

+++Answer

See the table below for a feature comparison between the Experience Cloud Audiences and Adobe Target destinations.

||Experience Cloud Audiences|Adobe Target|
|---|---|---|
| **Supported Experience Cloud apps** | Supports audience activation to Audience Manager, Adobe Target, Adobe Analytics, Advertising Cloud, Marketo, Adobe Campaign | Supports audience activation only to Adobe Target |
| **Supports audience activation** | ✓ | ✓ |
| **Supports attribute activation** | X | ✓ |
| **Latency** | Profiles begin activating in 6 hours. Full population is visible in 48 hours​. |Depends on implementation​ type. <ul><li>Web SDK enables same-page/next-page​ personalization.</li><li>AT.js enables next-session personalization.</li></ul> |
| **DULE support** | ✓ | ✓ |
| **Marketing actions support** | ✓ | ✓ |
| **Supported IDs** | [!DNL ECID], [!DNL GAID], [!DNL IDFA], [!DNL email_lc_sha256] | Any ID type |
| **Sandbox support** | One sandbox | Multiple sandboxes |
| **Consent support** | X | Yes. Requires Privacy & Security Shield. |
| **Edge segmentation support** | Supports activation of edge audiences. Does not support edge segmentation. | Supports edge segmentation and activation of edge audiences. |
| **Supported audiences** | All types of audiences  | Edge merge policy required for activation.|

+++

-->

## [!DNL Facebook Custom Audiences] {#facebook-faq}

### ¿Qué debo hacer para poder activar audiencias en [!DNL Facebook Custom Audiences]?

+++Respuesta
Antes de enviar las audiencias a [!DNL Facebook], asegúrese de cumplir con los siguientes requisitos:

* La cuenta de usuario [!DNL Facebook] debe tener habilitado el permiso **[!DNL Manage campaigns]** para la cuenta de publicidad que planea usar.
* La cuenta empresarial **Adobe Experience Cloud** debe agregarse como socio de publicidad en [!DNL Facebook Ad Account]. Usar `business ID=206617933627973`. Consulte [Agregar socios a su administrador comercial](https://www.facebook.com/business/help/1717412048538897) en la documentación de Facebook para obtener más información.

  >[!IMPORTANT]
  >
  > Al configurar los permisos para Adobe Experience Cloud, debe habilitar el permiso **Administrar campañas**. Esto es necesario para la integración de [!DNL Adobe Experience Platform].
* Lea y firme los términos de servicio de [!DNL Facebook Custom Audiences]. Para ello, vaya a `https://business.facebook.com/ads/manage/customaudiences/tos/?act=[accountID]`, donde `accountID` es su [!DNL Facebook Ad Account ID].
+++

### ¿Debo agregar aplicaciones o píxeles a mi cuenta de anunciante de [!DNL Facebook]?

+++Respuesta
No. Como no se trata de una integración basada en píxeles, no es necesario añadir píxeles a la cuenta del anunciante.
+++

### ¿Cuánto tiempo tarda Facebook en procesar la información de Adobe Experience Platform?

+++Respuesta
En marzo de 2021, [!DNL Facebook Custom Audiences] necesita hasta una hora para procesar la información recibida de [!DNL Experience Platform].
+++

### ¿Puedo usar [!DNL Facebook Custom Audiences] para segmentar audiencias en otras [!DNL Facebook] aplicaciones, como [!DNL Instagram]?

+++Amswer
Puede usar el destino [!DNL Facebook Custom Audiences] para la segmentación de audiencia en toda la familia de aplicaciones de Facebook compatibles con [!DNL Facebook Custom Audiences], entre ellas [!DNL Facebook], [!DNL Instagram], [!DNL Audience Network] y [!DNL Messenger]. La selección de la aplicación en la que los anunciantes desean ejecutar campañas se indica en el nivel de ubicación de [!DNL Facebook Ads Manager].
+++

### ¿Cuál es la diferencia entre la conexión [!DNL Facebook Custom Audiences] y la extensión [!DNL Facebook Pixel]?

+++Respuesta
La conexión [!DNL Facebook Custom Audiences] usa [!DNL Experience Platform] identidades al enviar audiencias a [!DNL Facebook], mientras que la conexión [[!DNL Facebook Pixel] connection](../destinations/catalog/advertising/facebook-pixel.md) usa los [!DNL Facebook] píxeles integrados en un sitio web.

Estas dos integraciones son complementarias; pueden utilizarse las dos para garantizar una mejor cobertura de audiencia. Por ejemplo, puede usar la extensión [!DNL Facebook Pixel] para la prospección de visitantes del sitio web que no hayan creado una cuenta, mientras que [!DNL Facebook Custom Audiences] puede ayudarle a dirigirse a los clientes existentes, según las identidades de [!DNL Experience Platform].
+++

### ¿Admite la integración de Adobe Experience Platform con [!DNL Facebook Custom Audiences] la descalificación de usuarios de una audiencia cuando ya no cumplen los requisitos para ella?**

+++Respuesta
Sí, la integración admite la eliminación de usuarios de [!DNL Facebook Custom Audiences] cuando ya no cumplen los requisitos.
+++

### ¿Cómo debo hash los datos de audiencia antes de enviarlos a [!DNL Facebook]?

+++Respuesta
[!DNL Facebook] requiere que no se envíe información de identificación personal (PII) de forma clara. Por lo tanto, las audiencias activadas en [!DNL Facebook] pueden tener claves de *identificadores hash*, como direcciones de correo electrónico o números de teléfono.

Para obtener explicaciones detalladas sobre los requisitos de coincidencia de ID, consulte [Requisitos de coincidencia de ID](catalog/social/facebook.md#id-matching-requirements).
+++

### ¿Qué tipo de identidades puedo activar en [!DNL Facebook Custom Audiences]?

+++Respuesta
[!DNL Facebook Custom Audiences] admite la activación de las siguientes identidades: correos electrónicos con hash, números de teléfono con hash, [!DNL GAID], [!DNL IDFA] e ID externos personalizados.
+++

### ¿Puedo crear varios destinos de Facebook en la interfaz de usuario de Experience Platform para cuentas de Facebook independientes?

+++Respuesta
Sí. Un destino de Facebook en Experience Platform es 1:1 en una cuenta de publicidad en Facebook. Puede crear un destino de Facebook independiente para cada cuenta de publicidad de Facebook de la compañía. Siga el [tutorial de conexión de destino](/help/destinations/ui/connect-destination.md) y conéctese a una cuenta de Facebook independiente para cada nuevo destino de Facebook en la interfaz de usuario de Experience Platform. No hay límite en el número de cuentas de anuncios de Facebook a las que puede conectarse.
+++

## Coincidencia de clientes de Google {#google-customer-match}

### Al exportar audiencias a Customer Match de Google, ¿por qué veo números adicionales anexados al final de los nombres de audiencia en la interfaz de Google?

+++Respuesta
Google requiere que los nombres de las audiencias sean únicos. Los números que está viendo son [marcas de tiempo UNIX](https://www.unixtimestamp.com/) y se anexan para mantener los nombres de audiencia únicos, si ha asignado la misma audiencia a varios destinos de Google.
+++

## Audiencias coincidentes de LinkedIn {#linkedin}

### ¿Debo agregar aplicaciones o píxeles a mi cuenta de anunciante de [!DNL LinkedIn]?

+++Respuesta
No. Como no se trata de una integración basada en píxeles, no es necesario añadir píxeles a la cuenta del anunciante.
+++

### ¿Qué debo hacer para poder activar audiencias en [!DNL LinkedIn Matched Audiences]?

+++Respuesta
Antes de usar el destino [!UICONTROL Audiencia coincidente de LinkedIn], asegúrate de que tu cuenta de [!DNL LinkedIn Campaign Manager] tenga el nivel de permiso de [!DNL Creative Manager] o superior.

Para obtener información sobre cómo editar los permisos de usuario de [!DNL LinkedIn Campaign Manager], consulte [Agregar, editar y quitar permisos de usuario en cuentas de Advertising](https://www.linkedin.com/help/lms/answer/5753) en la documentación de LinkedIn.
+++

### ¿Cómo debo hash los datos de audiencia antes de enviarlos a [!DNL LinkedIn]?

+++Respuesta
[!DNL LinkedIn] requiere que no se envíe información de identificación personal (PII) de forma clara. Por lo tanto, las audiencias activadas en [!DNL LinkedIn] pueden tener claves de *identificadores hash*, como direcciones de correo electrónico o números de teléfono.

Para obtener explicaciones detalladas sobre los requisitos de coincidencia de ID, consulte [Requisitos de coincidencia de ID](catalog/social/linkedin.md#id-matching-requirements).
+++

### ¿Qué tipo de identidades puedo activar en [!DNL LinkedIn]?

+++Respuesta
[!DNL LinkedIn Matched Audiences] admite la activación de las siguientes identidades: correos electrónicos con hash, [!DNL GAID] y [!DNL IDFA].

+++

## Personalización de la misma página y de la siguiente página mediante destinos Adobe Target y Personalization personalizados {#same-next-page-personalization}

### ¿Debo usar Experience Platform Web SDK para enviar audiencias y atributos a Adobe Target?

+++Respuesta
No, [Web SDK](../web-sdk/home.md) no es necesario para activar audiencias en [Adobe Target](catalog/personalization/adobe-target-connection.md).

Sin embargo, si se usa [[!DNL at.js]](https://experienceleague.adobe.com/docs/target-dev/developer/client-side/at-js-implementation/overview.html) en lugar de Web SDK, solo se admite la personalización de la sesión siguiente.

Para los casos de uso de [personalización de la misma página y de la siguiente](ui/activate-edge-personalization-destinations.md), debe usar [Web SDK](../web-sdk/home.md) o la [API de Edge Network](https://developer.adobe.com/data-collection-apis/docs/api/). Consulte la documentación sobre [activación de audiencias en destinos Edge](ui/activate-edge-personalization-destinations.md) para obtener más información sobre la implementación.
+++

### ¿Hay un límite en el número de atributos que puedo enviar desde Real-time Customer Data Platform a Adobe Target o a un destino personalizado de Personalization?

+++Respuesta
Sí, los casos de uso de personalización de la misma página y de la página siguiente admiten un máximo de 30 atributos por zona protegida al activar audiencias en destinos de Adobe Target o Personalization personalizados. Vea más información acerca de las protecciones de activación en la [documentación sobre las protecciones](guardrails.md#edge-destinations-activation).
+++

### ¿Qué tipos de atributos se admiten para la activación (por ejemplo, matrices, mapas, etc.)?

+++Respuesta
Actualmente, solo se admiten atributos estáticos de un solo valor, como `person.name.firstName`. Actualmente no se admiten atributos de matriz.
+++

<!-- **Is there a limit on the number of audiences that can be activated to Adobe Target and Custom Personalization destinations?**

Yes, you can activate a maximum of 150 edge audiences per sandbox.  For more information on activation guardrails, see the [default guardrails for activation](guardrails.md#edge-destinations-activation). -->

### Después de crear una audiencia en Experience Platform, ¿cuánto tiempo tardará esa audiencia en estar disponible para los casos de uso de segmentación de Edge?

+++Respuesta
Las definiciones de audiencia se propagan a [Edge Network](../web-sdk/home.md) en un máximo de una hora. Sin embargo, si se activa una audiencia en esta primera hora, se podrían perder algunos visitantes que habrían cumplido los requisitos para la audiencia.
+++

### ¿Dónde puedo ver los atributos activados en Adobe Target?

+++Respuesta
Los atributos estarán disponibles para usarlos en Target en las ofertas [JSON](https://experienceleague.adobe.com/docs/target/using/experiences/offers/create-json-offer.html) y [HTML](https://experienceleague.adobe.com/docs/target/using/experiences/offers/manage-content.html).
+++

### ¿Puedo crear un destino sin una secuencia de datos y luego agregar una secuencia de datos al mismo destino en un momento posterior?

+++Respuesta
Actualmente, esto no se admite en la IU de destinos. Si necesita ayuda en este caso, póngase en contacto con su representante de Adobe.
+++

### ¿Qué sucede si elimino un destino de Adobe Target?

+++Respuesta
Al eliminar un destino, todas las audiencias y atributos asignados en dicho destino se eliminan de Adobe Target y también se eliminan de Edge Network.
+++

### ¿Funciona la integración con la API de Edge Network?

+++Respuesta
Sí, la API de Edge Network funciona con el destino de Personalization personalizado. Dado que los atributos de perfil pueden contener datos confidenciales, para protegerlos, el destino de Personalization personalizado requiere que utilice la API de Edge Network para la recopilación de datos. Además, todas las llamadas de API deben realizarse en un [contexto autenticado](https://developer.adobe.com/data-collection-apis/docs/getting-started/authentication/).
+++

### Solo puedo tener una política de combinación activa en Edge. ¿Puedo crear audiencias que utilicen una política de combinación diferente y seguir enviándolas a Adobe Target como audiencias de streaming?

+++Respuesta
No. Todas las audiencias que desee activar en Adobe Target deben usar una [política de combinación](../profile/merge-policies/ui-guide.md) activa en el perímetro.
+++

### ¿Se aplican las políticas de etiquetado y aplicación del uso de datos (Data Usage Labeling and Enforcement, DULE) y de consentimiento?

+++Respuesta
Sí. Las [Políticas de consentimiento y control de datos](../data-governance/home.md) creadas y asociadas con las acciones de marketing seleccionadas regirán la activación de los atributos seleccionados.
+++

### ¿Son compatibles los destinos [!DNL Adobe Target] y [!DNL Custom Personalization] [!DNL HIPAA]?

+++Respuesta
[!DNL Adobe Target] no es compatible con [!DNL HIPPA] con [[!DNL Adobe Healthcare Shield]](https://business.adobe.com/solutions/industries/healthcare.html). Los clientes deben consultar con sus propios equipos legales la preparación de [!DNL HIPPA] para los canales de optimización personalizados antes de usar la personalización de Edge a través de [!DNL Adobe Target] o los destinos de [!DNL Custom Personalization].

Para los casos de uso en los que la administración de directivas de consentimiento debe aplicarse a escala, los clientes deben adquirir [!DNL Adobe Privacy & Security Shield]. Las características de [!DNL Adobe Privacy & Security Shield] se venden como un conjunto de funciones avanzadas y no se pueden comprar por separado.

Este servicio incluye claves administradas por el cliente y umbrales elevados para administrar el ciclo de vida de los datos del cliente.

Los destinos [!DNL Adobe Target] y [!DNL Custom Personalization] están integrados con las [etiquetas de uso de datos de Experience Platform](../data-governance/labels/overview.md) y el [servicio de aplicación de directivas de consentimiento](../data-governance/enforcement/overview.md). Estas funciones están disponibles para todos los clientes.




+++

