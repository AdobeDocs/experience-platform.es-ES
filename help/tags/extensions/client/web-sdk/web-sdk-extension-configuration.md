---
title: Configurar la extensión de etiqueta del SDK web
description: Obtenga información sobre cómo configurar la extensión de etiquetas de SDK web de Experience Platform en la interfaz de usuario de etiquetas.
exl-id: 22425daa-10bd-4f06-92de-dff9f48ef16e
source-git-commit: 660d4e72bd93ca65001092520539a249eae23bfc
workflow-type: tm+mt
source-wordcount: '2012'
ht-degree: 5%

---

# Configurar la extensión de etiqueta del SDK web

El [!DNL Web SDK] la extensión de etiqueta envía datos a Adobe Experience Cloud desde las propiedades web a través del Edge Network del Experience Platform.

La extensión de le permite transmitir datos a Platform, sincronizar identidades, procesar señales de consentimiento de clientes y recopilar automáticamente datos de contexto.

En este documento se explica cómo configurar la extensión de etiqueta en la interfaz de usuario de Etiquetas.

## Instalación de la extensión de etiqueta del SDK web {#install}

La extensión de etiqueta del SDK web necesita que se instale una propiedad en. Si aún no lo ha hecho, consulte la documentación sobre [creación de una propiedad de etiqueta](https://experienceleague.adobe.com/docs/platform-learn/implement-in-websites/configure-tags/create-a-property.html).

Una vez creada una propiedad, ábrala y seleccione la opción **[!UICONTROL Extensiones]** en la barra lateral izquierda.

Seleccione el **[!UICONTROL Catálogo]** pestaña. En la lista de extensiones disponibles, busque [!DNL Web SDK] extensión y seleccione **[!UICONTROL Instalar]**.

![Imagen que muestra la IU de etiquetas con la extensión del SDK web seleccionada](assets/web-sdk-install.png)

Después de seleccionar **[!UICONTROL Instalar]**, debe configurar la extensión de etiqueta del SDK web y guardar la configuración.

>[!NOTE]
>
>La extensión de etiqueta solo se instala después de guardar la configuración. Consulte las secciones siguientes para obtener información sobre cómo configurar la extensión de etiqueta.

## Configuración de la instancia {#general}

Las opciones de configuración en la parte superior de la página indican a Adobe Experience Platform dónde enrutar los datos y qué configuraciones utilizar en el servidor.

![Imagen que muestra la configuración general de la extensión de etiqueta del SDK web en la interfaz de usuario de etiquetas](assets/web-sdk-ext-general.png)

* **[!UICONTROL Nombre]**: la extensión del SDK web de Adobe Experience Platform admite varias instancias en la página. El nombre se utiliza para enviar datos a varias organizaciones con una configuración de etiquetas. El nombre de instancia predeterminado es `alloy`. Sin embargo, puede cambiar el nombre de la instancia a cualquier nombre de objeto de JavaScript válido.
* **[!UICONTROL ID de organización IMS]**: ID de la organización a la que desea que se envíen los datos durante el Adobe. La mayoría de las veces, utilice el valor predeterminado que se rellena automáticamente. Cuando tenga varias instancias en la página, rellene este campo con el valor de la segunda organización a la que desee enviar datos.
* **[!UICONTROL dominio de Edge]**: Dominio desde el cual la extensión envía y recibe datos. El Adobe recomienda utilizar un dominio de origen (CNAME) para esta extensión. El dominio de terceros predeterminado funciona para entornos de desarrollo, pero no es adecuado para entornos de producción. Las instrucciones sobre cómo configurar un CNAME de origen se enumeran [aquí](https://experienceleague.adobe.com/docs/core-services/interface/ec-cookies/cookies-first-party.html?lang=es).

## Configuración del flujo de datos {#datastreams}

Esta sección le permite seleccionar los flujos de datos que deben utilizarse para cada uno de los tres entornos disponibles (producción, ensayo y desarrollo).

Cuando se envía una solicitud al Edge Network, se utiliza un ID de conjunto de datos para hacer referencia a la configuración del lado del servidor. Puede actualizar la configuración sin tener que realizar cambios en el código del sitio web.

Consulte la guía de [flujos de datos](../../../../datastreams/overview.md) para aprender a configurar una secuencia de datos.

Puede elegir una secuencia de datos de los menús desplegables disponibles o seleccionar **[!UICONTROL Introducir valores]** e introduzca un ID de flujo de datos personalizado para cada entorno.

![Imagen que muestra la configuración del flujo de datos de la extensión de etiqueta del SDK web en la interfaz de usuario de etiquetas](assets/web-sdk-ext-datastreams.png)

## Configuración de privacidad {#privacy}

Esta sección le permite configurar cómo el SDK web gestiona las señales de consentimiento de los usuarios desde el sitio web. En concreto, le permite seleccionar el nivel de consentimiento predeterminado que se supone de un usuario si no se ha proporcionado ninguna otra preferencia de consentimiento explícita.

El nivel de consentimiento predeterminado no se guarda en el perfil de usuario.

![Imagen que muestra la configuración de privacidad de la extensión de etiqueta del SDK web en la interfaz de usuario de etiquetas](assets/web-sdk-ext-privacy.png)

| [!UICONTROL Nivel de consentimiento predeterminado] | Descripción |
| --- | --- |
| [!UICONTROL Entrada] | Recopilar eventos que se producen antes de que el usuario proporcione preferencias de consentimiento. |
| [!UICONTROL Fuera] | Descartar los eventos que se producen antes de que el usuario proporcione preferencias de consentimiento. |
| [!UICONTROL Pendiente] | Eventos de cola que se producen antes de que el usuario proporcione preferencias de consentimiento. Cuando se proporcionan las preferencias de consentimiento, los eventos se recopilan o descartan según las preferencias proporcionadas. |
| [!UICONTROL Proporcionado por el elemento de datos] | El nivel de consentimiento predeterminado está determinado por un elemento de datos independiente que usted defina. Al utilizar esta opción, debe especificar el elemento de datos mediante el menú desplegable proporcionado. |

>[!TIP]
>
>Uso **[!UICONTROL Fuera]** o **[!UICONTROL Pendiente]** si necesita el consentimiento explícito del usuario para sus operaciones comerciales.

## Configuración de la identidad {#identity}

Esta sección le permite definir el comportamiento del SDK web en lo que respecta a la gestión de la identificación del usuario.

![Imagen que muestra la configuración de identidad de la extensión de etiqueta del SDK web en la interfaz de usuario de etiquetas](assets/web-sdk-ext-identity.png)

* **[!UICONTROL Migrar ECID desde VisitorAPI]**: Esta opción está habilitada de forma predeterminada. Cuando esta función está habilitada, el SDK puede leer el `AMCV` y `s_ecid` y configure las `AMCV` cookie utilizada por [!DNL Visitor.js]. Esta función es importante al migrar al SDK web, ya que algunas páginas pueden seguir utilizando [!DNL Visitor.js]. Esta opción permite que el SDK siga utilizando el mismo [!DNL ECID] para que los usuarios no se identifiquen como dos usuarios independientes.
* **[!UICONTROL Uso de cookies de terceros]**: cuando esta opción está habilitada, el SDK web intenta almacenar un identificador de usuario en una cookie de terceros. Si se realiza correctamente, el usuario se identifica como un solo usuario a medida que navega por varios dominios, en lugar de identificarse como un usuario independiente en cada dominio. Si esta opción está habilitada, es posible que el SDK aún no pueda almacenar el identificador de usuario en una cookie de terceros si el explorador no admite cookies de terceros o si el usuario lo ha configurado para no permitir cookies de terceros. En este caso, el SDK solo almacena el identificador en el dominio de origen.

  >[!IMPORTANT]
  >>Las cookies de terceros no son compatibles con [ID de dispositivo de origen](../../../../web-sdk/identity/first-party-device-ids.md) en el SDK web.
Puede usar ID de dispositivos de origen o cookies de terceros, pero no puede usar ambas funciones simultáneamente.
  >
## Configuración de la personalización {#personalization}

Esta sección le permite configurar cómo desea ocultar determinadas partes de una página mientras se carga contenido personalizado. Esto garantiza que los visitantes solo vean la página personalizada.

![Imagen que muestra la configuración de personalización de la extensión de etiqueta del SDK web en la interfaz de usuario de etiquetas](assets/web-sdk-ext-personalization.png)

* **[!UICONTROL Migración de Target de at.js al SDK web]**: utilice esta opción para habilitar [!DNL Web SDK] para leer y escribir el legado `mbox` y `mboxEdgeCluster` cookies que utiliza at.js `1.x` o `2.x` bibliotecas. Esto le ayuda a mantener el perfil del visitante mientras se desplaza de una página que utiliza el SDK web a una página que utiliza at.js `1.x` o `2.x` bibliotecas y viceversa.

### Estilo preocultado {#prehiding-style}

El editor de estilos preocultado permite definir reglas CSS personalizadas para ocultar secciones específicas de una página. Cuando se carga la página, el SDK web utiliza este estilo para ocultar las secciones que deben personalizarse, recupera la personalización y, a continuación, muestra las secciones de página personalizadas. De este modo, los visitantes ven las páginas ya personalizadas, sin ver el proceso de recuperación de la personalización.

### Preocultando fragmento {#prehiding-snippet}

El fragmento de preocultación resulta útil cuando la biblioteca del SDK web se carga asincrónicamente. En este caso, para evitar parpadeos, se recomienda ocultar el contenido antes de cargar la biblioteca del SDK web.

Para utilizar el fragmento preocultado, cópielo y péguelo dentro de `<head>` de la página.

>[!IMPORTANT]
>
Al utilizar el fragmento preocultado, Adobe recomienda utilizar el mismo [!DNL CSS] regla como la que usa el [estilo preocultado](#prehiding-style).

## Configuración de la recopilación de datos {#data-collection}

Administrar las opciones de configuración de recopilación de datos. Configuraciones similares en la biblioteca de JavaScript están disponibles mediante la variable [`configure`](/help/web-sdk/commands/configure/overview.md) comando.

![Imagen que muestra la configuración de recopilación de datos de la extensión de etiqueta del SDK web en la interfaz de usuario de etiquetas.](assets/web-sdk-ext-collection.png)

* **[!UICONTROL Activado antes de devolución de llamada de envío de evento]**: una función de llamada de retorno para evaluar y modificar la carga útil enviada al Adobe. Utilice el `content` dentro de la función de llamada de retorno para modificar la carga útil. Esta llamada de retorno es la etiqueta equivalente a [`onBeforeEventSend`](/help/web-sdk/commands/configure/onbeforeeventsend.md) en la biblioteca de JavaScript.
* **[!UICONTROL Recopilación de clics en vínculos internos]**: Casilla de verificación que permite recopilar datos de seguimiento de vínculos internos del sitio o la propiedad. Al activar esta casilla de verificación, aparecen las opciones de agrupación de eventos:
   * **[!UICONTROL Sin agrupación de eventos]**: Los datos de seguimiento de vínculos se envían al Adobe en eventos independientes. Los clics en vínculos enviados en eventos independientes pueden aumentar el uso contractual de los datos enviados a Adobe Experience Platform.
   * **[!UICONTROL Agrupación de eventos mediante el almacenamiento de sesión]**: almacena los datos de seguimiento de vínculos en el almacenamiento de la sesión hasta el evento de página siguiente. En la página siguiente, los datos de seguimiento de vínculos almacenados y los datos de vista de página se envían al Adobe al mismo tiempo. Adobe recomienda habilitar esta configuración al realizar el seguimiento de vínculos internos.
   * **[!UICONTROL Agrupación de eventos con objeto local]**: almacena los datos de seguimiento de vínculos en un objeto local hasta el evento de página siguiente. Si un visitante navega a una página nueva, se pierden los datos de seguimiento de vínculos. Esta configuración es más beneficiosa en el contexto de aplicaciones de una sola página.
* **[!UICONTROL Recopilación de clics en vínculos externos]**: Casilla de verificación que permite recopilar vínculos externos.
* **[!UICONTROL Recopilar clics en vínculos de descarga]**: Casilla de verificación que habilita la recopilación de vínculos de descarga.
* **[!UICONTROL Descargar calificador de vínculo]**: Expresión regular que califica una dirección URL de vínculo como vínculo de descarga.
* **[!UICONTROL Filtrar propiedades de clic]**: una función de llamada de retorno para evaluar y modificar las propiedades relacionadas con los clics antes de la colección. Esta función se ejecuta antes que [!UICONTROL Activado antes de devolución de llamada de envío de evento].
* **Configuración de contexto**: recopile automáticamente información del visitante que rellena automáticamente campos XDM específicos. Puede elegir **[!UICONTROL Toda la información de contexto predeterminada]** o **[!UICONTROL Información de contexto específica]**. Es la etiqueta equivalente a [`context`](/help/web-sdk/commands/configure/context.md) en la biblioteca de JavaScript.
   * **[!UICONTROL Web]**: Recopila información sobre la página actual.
   * **[!UICONTROL Dispositivo]**: recopila información sobre el dispositivo del usuario.
   * **[!UICONTROL Entorno]**: recopila información sobre el explorador del usuario.
   * **[!UICONTROL Contexto del lugar]**: recopila información sobre la ubicación del usuario.
   * **[!UICONTROL Sugerencias de agente de usuario de alta entropía]**: recopila información más detallada sobre el dispositivo del usuario.

>[!TIP]
>
El **[!UICONTROL Activado antes del envío de clics en vínculo]** Este campo es una llamada de retorno obsoleta que solo está visible para propiedades que ya lo tienen configurado. Es la etiqueta equivalente a [`onBeforeLinkClickSend`](/help/web-sdk/commands/configure/onbeforelinkclicksend.md) en la biblioteca de JavaScript. Utilice el **[!UICONTROL Filtrar propiedades de clic]** devolución de llamada para filtrar o ajustar datos de clics, o use **[!UICONTROL Activado antes de devolución de llamada de envío de evento]** para filtrar o ajustar la carga útil general enviada al Adobe. Si tanto la variable **[!UICONTROL Filtrar propiedades de clic]** callback y el **[!UICONTROL Activado antes del envío de clics en vínculo]** se establecen las llamadas de retorno, solo las **[!UICONTROL Filtrar propiedades de clic]** se ejecuta callback.

## Configuración de la colección de medios {#media-collection}

La función de recopilación de contenido le ayuda a recopilar datos relacionados con las sesiones de contenido del sitio web.

Los datos recopilados pueden incluir información sobre reproducciones de contenido, pausas, finalizaciones y otros eventos relacionados. Una vez recopilados, puede enviar estos datos a Adobe Experience Platform o Adobe Analytics para generar informes. Esta función proporciona una solución completa para realizar el seguimiento y comprender el comportamiento del consumo de medios en el sitio web.

![Imagen que muestra la configuración de recopilación de medios de la extensión de etiqueta del SDK web en la interfaz de usuario de etiquetas](assets/media-collection.png)


* **[!UICONTROL Canal]**: Nombre del canal en el que se produce la recopilación de medios. Ejemplo: `Video channel`.
* **[!UICONTROL Nombre del reproductor]**: Nombre del reproductor de contenidos.
* **[!UICONTROL Versión de aplicación]**: versión de la aplicación de reproducción de contenido.
* **[!UICONTROL Intervalo de ping principal]**: Frecuencia de pings para el contenido principal, en segundos. El valor predeterminado es `10`. Los valores pueden variar desde `10` hasta `50` segundos.  Si no se especifica ningún valor, se utiliza el valor predeterminado al utilizar [sesiones rastreadas automáticamente](../../../../web-sdk/commands/createmediasession.md#automatic).
* **[!UICONTROL Intervalo de ping de anuncio]**: Frecuencia de pings para el contenido del anuncio, en segundos. El valor predeterminado es `10`. Los valores pueden variar desde `1` hasta `10` segundos. Si no se especifica ningún valor, se utiliza el valor predeterminado al utilizar [sesiones rastreadas automáticamente](../../../../web-sdk/commands/createmediasession.md#automatic)

## Configurar anulaciones de secuencia de datos {#datastream-overrides}

Las anulaciones de las secuencias de datos permiten definir configuraciones adicionales para las secuencias de datos, que pasan a la red perimetral mediante el SDK web.

Esto le ayuda a activar comportamientos de secuencias de datos diferentes de los predeterminados, sin crear una nueva secuencia de datos ni modificar la configuración existente.

La anulación de la configuración de la secuencia de datos es un proceso de dos pasos:

1. En primer lugar, debe definir las anulaciones de configuración de la secuencia de datos en la [página de configuración de secuencia de datos](/help/datastreams/configure.md).
2. A continuación, debe enviar las invalidaciones al Edge Network a través de un comando del SDK web o mediante la extensión de etiqueta del SDK web.

Consulte la secuencia de datos [la configuración anula la documentación](/help/datastreams/overrides.md) para obtener instrucciones detalladas sobre cómo anular las configuraciones de secuencia de datos.

Como alternativa a pasar las invalidaciones a través de un comando del SDK web, puede configurarlas en la pantalla de extensión de etiquetas que se muestra a continuación.

>[!IMPORTANT]
>
Las anulaciones de flujos de datos deben configurarse por entorno. Los entornos de desarrollo, ensayo y producción tienen invalidaciones independientes. Puede copiar los ajustes entre ellos utilizando las opciones dedicadas que se muestran en la pantalla siguiente.

![Imagen que muestra las anulaciones de configuración de la secuencia de datos mediante la página de extensión de etiquetas del SDK web.](assets/datastream-overrides.png)

## Configuración avanzada

Utilice el **[!UICONTROL Ruta base de Edge]** campo si necesita cambiar la ruta base que se utiliza para interactuar con el Edge Network. Esto no debería requerir ninguna actualización, pero en caso de que participe en una versión beta o alfa, Adobe podría pedirle que cambie este campo.

![Imagen que muestra la configuración avanzada de mediante la página de extensión de etiquetas del SDK web.](assets/advanced-settings.png)
