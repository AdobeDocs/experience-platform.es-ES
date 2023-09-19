---
keywords: extensión de reenvío de eventos;mixpanel;extensión de reenvío de eventos de mixpanel
title: Extensión de reenvío de eventos API de seguimiento de eventos de Mixpanel
description: Esta extensión de reenvío de eventos de Adobe Experience Platform envía eventos de red perimetral a Mixpanel.
last-substantial-update: 2023-03-29T00:00:00Z
exl-id: 21e2e0fa-4949-4be4-859f-d449d21d8f41
source-git-commit: 3272db15283d427eb4741708dffeb8141f61d5ff
workflow-type: tm+mt
source-wordcount: '946'
ht-degree: 1%

---

# [!DNL Mixpanel Track Events] Extensión de reenvío de eventos API

[[!DNL Mixpanel]](https://www.mixpanel.com) es una herramienta de análisis de productos que le permite capturar datos sobre cómo los usuarios interactúan con un producto digital. Puede analizar los datos de los productos con informes sencillos e interactivos que le permiten consultar y visualizar los datos con solo unos clics. [!DNL Mixpanel] diseñado para que los equipos sean más eficientes, ya que permite a todos analizar los datos de usuario en tiempo real para identificar tendencias, comprender el comportamiento del usuario y tomar decisiones sobre el producto.

[!DNL Mixpanel] emplea un modelo centrado en el usuario y basado en eventos que conecta cada interacción con un solo usuario. El [!DNL Mixpanel] El modelo de datos de se basa en los conceptos de usuarios, eventos y propiedades.

>[!NOTE]
>
>Consulte la [!DNL Mixpanel] documentación sobre [administración de identidades](https://help.mixpanel.com/hc/en-us/articles/360041039771-Getting-Started-with-Identity-Management) para comprender cómo [!DNL Mixpanel] combina eventos para crear clústeres de identidad. También se recomienda revisar el documento en [ID distintos](https://help.mixpanel.com/hc/en-us/articles/115004509426-Distinct-ID-Creation-JavaScript-iOS-Android-) para comprender cómo se utilizan para identificar a los usuarios en los datos de evento.

## Casos de uso

Debe usar esta extensión si desea usar datos de la red perimetral en [!DNL Mixpanel] para aprovechar sus capacidades de análisis de productos.

Por ejemplo, considere una organización minorista que tenga presencia multicanal (sitio web y móvil). La organización captura los datos de transacción o conversacionales como datos de evento de sus plataformas y los carga en [!DNL Mixpanel] uso de la extensión de reenvío de eventos.

Los equipos de análisis pueden aprovechar [!DNL Mixpanel's] capacidades para procesar los conjuntos de datos y derivar perspectivas comerciales, que se pueden utilizar para generar gráficos, tableros u otras visualizaciones para informar a las partes interesadas empresariales.

Para obtener más información sobre casos de uso específicos de [!DNL Mixpanel], consulte la siguiente documentación:

* [Nuevo en [!DNL Mixpanel]](https://docs.mixpanel.com/docs)
* [¿Qué es  [!DNL Mixpanel]?](https://developer.mixpanel.com/docs)
* [12 intentos obligatorios [!DNL Mixpanel] características](https://mixpanel.com/blog/12-things-you-probably-didnt-know-you-could-do-with-mixpanel/)

## [!DNL Mixpanel] requisitos previos {#prerequisites-mixpanel}

Debe tener un válido [!DNL Mixpanel] para utilizar esta extensión. Vaya a la [[!DNL Mixpanel] página de registro](https://mixpanel.com/register/) para registrarse y crear una cuenta si aún no la tiene.

Asegúrese de que la variable [[!DNL Identity Merge]](https://help.mixpanel.com/hc/en-us/articles/9648680824852-ID-Merge-Implementation-Best-Practices) La configuración está habilitada para su proyecto. Vaya a **[!DNL Settings]** > **[!DNL Project Setting]** > **[!DNL Identity Merge]** y alternar el ajuste.

### Explicación de los clústeres de identidad en [!DNL Mixpanel]

Entrada [!DNL Mixpanel], un clúster de identidad contiene una colección de `distinct_id` valores que se conectan a un usuario individual. [!DNL Mixpanel] administra el grupo de identidades de cada usuario, resolviendo un único problema canónico `distinct_id` de cada clúster que se utilizará en los informes. También puede incluir su propio identificador (denominado local `distinct_id`) para eventos anónimos que se producen antes de un evento de identificación de usuario.

[!DNL Mixpanel] resuelve los clústeres de identidad mediante dos métodos:

* **Identificar** : [!DNL Mixpanel] conecta el identificador seleccionado con un anónimo `distinct_id`. Si su sitio web tiene [!DNL Mixpanel] SDK habilitado, Platform utilizará el `distinct_id` asignado al usuario que ha iniciado sesión actualmente.
* **Alias**: [!DNL Mixpanel] combina dos no anónimos `distinct id`&quot;s&quot; juntos si se cumplen criterios de combinación adicionales.

>[!NOTE]
>
>Consulte la [!DNL Mixpanel] documento en [administración de identidades](https://help.mixpanel.com/hc/en-us/articles/360041039771-Getting-Started-with-Identity-Management#user-identification) para obtener más información sobre estos métodos.
>
>Confirme que ha habilitado la variable [[!DNL Mixpanel] función de combinación de identidades](#prerequisites-mixpanel) para garantizar que los clústeres de identidad se resuelven correctamente.

### Recopilar detalles de configuración necesarios {#configuration-details}

Para conectar el Experience Platform a [!DNL Mixpanel] debe tener las siguientes entradas:

| Tipo de clave | Descripción | Ejemplo |
| --- | --- | --- |
| Token de proyecto | El token de proyecto asociado con su [!DNL Mixpanel] cuenta. Consulte la [!DNL Mixpanel] documentación sobre [búsqueda del token de proyecto](https://help.mixpanel.com/hc/en-us/articles/115004502806-Find-Project-Token-) para obtener orientación. | `25470xxxxxxxxxxxxxxxxxxx1289` |

## Instalación y configuración de [!DNL Mixpanel] extensión {#install}

Para instalar la extensión de, [crear una propiedad de reenvío de eventos](../../../ui/event-forwarding/overview.md#properties) o elija una propiedad existente para editar en su lugar.

Seleccionar **[!UICONTROL Extensiones]** en el panel de navegación izquierdo. En el **[!UICONTROL Catálogo]** pestaña, seleccione **[!UICONTROL Instalar]** en la tarjeta de [!DNL Mixpanel] extensión.

![Instalación del [!DNL Mixpanel] extensión.](../../../images/extensions/server/mixpanel/install-extension.png)

## Crear un [!DNL Send Event] regla

Comience a crear una nueva regla en la propiedad de reenvío de eventos. En **[!UICONTROL Acciones]**, añada una nueva acción y establezca la extensión en **[!UICONTROL Mixpanel]**. A continuación, establezca el tipo de acción en **[!UICONTROL Rastrear evento]** para enviar eventos de Edge Network a [!DNL Mixpanel].

| Entrada | Descripción | Requerido |
| --- | --- | --- |
| [!UICONTROL Token de proyecto] | Este campo debe asignarse al token de proyecto asociado a su [!DNL Mixpanel] cuenta. | Sí |
| [!UICONTROL Tipo de evento] | Nombre del evento. | Sí |
| [!UICONTROL Hora del evento] | La hora del evento. | |
| [!UICONTROL ID distinto de Mixpanel] | El identificador único del usuario que realizó el evento. | |
| [!UICONTROL Insertar ID] | Identificador único del evento que se utiliza para la anulación de duplicación. | |
| [!UICONTROL Propiedades del evento] | Objeto JSON que contiene propiedades personalizadas del evento. Seleccione entre proporcionar JSON sin procesar o utilizar un conjunto simplificado de entradas de clave-valor. | |

>[!NOTE]
>
>Para obtener más información sobre los campos estándar de una [!DNL Mixpanel] , consulte la [documentación oficial](https://developer.mixpanel.com/reference/import-events#event).

![Añada una configuración de acción de regla de reenvío de eventos.](../../../images/extensions/server/mixpanel/track-event-action.png)

Una vez que [!UICONTROL Rastrear evento] acción se añade a la regla, puede configurar las condiciones de la regla para que solo se active para determinados eventos o puede dejar vacía la sección condiciones para que la regla se active para todos los eventos.

>[!IMPORTANT]
>
>Si su sitio web utiliza [!DNL Mixpanel] SDK, puede continuar con el siguiente paso de [validación de los datos en [!DNL Mixpanel]](#validate). Si no utiliza el [!DNL Mixpanel] SDK, debe [crear una regla de seguimiento de identidad independiente](#create-an-identity-tracking-rule) para garantizar que los eventos y `distinct_id` Los valores de se envían a [!DNL Mixpanel] cuando se produce un evento de identificación de usuario.

## Validación de datos dentro de [!DNL Mixpanel] {#validate}

Si la implementación se realiza correctamente y se recopilan eventos, verá eventos dentro de la variable [[!DNL Mixpanel] consolar](https://help.mixpanel.com/hc/en-us/articles/4402837164948).

Comprobar si [!DNL Mixpanel] ha combinado los eventos posteriores al inicio de sesión rellenados con valores de correo electrónico y los eventos creados al utilizar **[!UICONTROL Enviar evento]**. Si se implementa correctamente, [!DNL Mixpanel] los asociará con un único [perfil de usuario](https://help.mixpanel.com/hc/en-us/articles/115004501966).

## Pasos siguientes

En esta guía se explica cómo enviar eventos de conversión a [!DNL Mixpanel] uso del reenvío de eventos. Esta extensión de reenvío de eventos aprovecha el [!DNL Mixpanel] SDK y API de JavaScript. Para obtener más información sobre estas tecnologías subyacentes, consulte la documentación oficial:

* [[!DNL Mixpanel] SDK](https://developer.mixpanel.com/docs/nodejs)
* [[!DNL Mixpanel] API de JavaScript](https://developer.mixpanel.com/docs/javascript-full-api-reference#mixpanelidentify)

Para obtener más información sobre las funcionalidades de reenvío de eventos en Experience Platform, consulte la [resumen del reenvío de eventos](../../../ui/event-forwarding/overview.md).
