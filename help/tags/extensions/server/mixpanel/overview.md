---
keywords: extensión de reenvío de eventos;mixpanel;extensión de reenvío de eventos de panel mixto
title: Extensión de reenvío de eventos de API de seguimiento de eventos de Mixpanel
description: Esta extensión de reenvío de eventos de Adobe Experience Platform envía eventos de Adobe Experience Edge Network a Mixpanel.
source-git-commit: 8538e3a2899c3e2451519996cabeffc4b42d706c
workflow-type: tm+mt
source-wordcount: '953'
ht-degree: 1%

---

# [!DNL Mixpanel Track Events] Extensión de reenvío de eventos de API

[[!DNL Mixpanel]](https://www.mixpanel.com) es una herramienta de análisis de producto que le permite capturar datos sobre cómo interactúan los usuarios con un producto digital. Puede analizar los datos del producto con informes interactivos y simples que le permiten consultar y visualizar los datos con solo unos clics. [!DNL Mixpanel] diseñado para que los equipos sean más eficientes, ya que permite a todos analizar los datos de los usuarios en tiempo real para identificar tendencias, comprender el comportamiento de los usuarios y tomar decisiones sobre su producto.

[!DNL Mixpanel] emplea un modelo basado en eventos y centrado en el usuario que conecta cada interacción con un único usuario. La variable [!DNL Mixpanel] el modelo de datos se basa en los conceptos de usuarios, eventos y propiedades.

>[!NOTE]
>
>Consulte la [!DNL Mixpanel] documentación sobre [administración de identidades](https://help.mixpanel.com/hc/en-us/articles/360041039771-Getting-Started-with-Identity-Management) para comprender cómo [!DNL Mixpanel] combina eventos para crear clústeres de identidad. También se recomienda revisar el documento en [ID distintos](https://help.mixpanel.com/hc/en-us/articles/115004509426-Distinct-ID-Creation-JavaScript-iOS-Android-) para comprender cómo se utilizan para identificar a los usuarios en los datos de evento.

## Casos de uso

Esta extensión debe usarse si desea utilizar datos de la red perimetral en [!DNL Mixpanel] para aprovechar las funciones de análisis de productos.

Por ejemplo, considere una organización minorista que tiene una presencia multicanal (sitio web y móvil). La organización captura la entrada transaccional o de conversación como datos de evento de sus plataformas y lo carga en [!DNL Mixpanel] uso de la extensión de reenvío de eventos.

Los equipos de análisis pueden aprovechar [!DNL Mixpanel's] capacidades para procesar los conjuntos de datos y derivar perspectivas empresariales, que pueden utilizarse para generar gráficos, tableros u otras visualizaciones para informar a las partes interesadas del negocio.

Para obtener más información sobre casos de uso específicos de [!DNL Mixpanel], consulte la siguiente documentación:

* [Nuevo en [!DNL Mixpanel]](https://help.mixpanel.com/hc/en-us/sections/360008533532-New-to-Mixpanel)
* [¿Qué es  [!DNL Mixpanel]?](https://developer.mixpanel.com/docs)
* [12 prueba obligatoria [!DNL Mixpanel] características](https://mixpanel.com/blog/12-things-you-probably-didnt-know-you-could-do-with-mixpanel/)

## [!DNL Mixpanel] requisitos previos {#prerequisites-mixpanel}

Debe tener una [!DNL Mixpanel] para utilizar esta extensión. Vaya a la [[!DNL Mixpanel] página de registro](https://mixpanel.com/register/) para registrar y crear una cuenta si todavía no la tiene.

Asegúrese de que la variable [[!DNL Identity Merge]](https://help.mixpanel.com/hc/en-us/articles/9648680824852-ID-Merge-Implementation-Best-Practices) está habilitado para el proyecto. Vaya a **[!DNL Settings]** > **[!DNL Project Setting]** > **[!DNL Identity Merge]** y alterne la configuración .

### Explicación de los clústeres de identidad en [!DNL Mixpanel]

En [!DNL Mixpanel], un clúster de identidad contiene una colección de `distinct_id` valores que se conectan a un usuario individual. [!DNL Mixpanel] gestiona el clúster de identidades de cada usuario, resolviendo un solo canónico `distinct_id` de cada clúster que se utilizará en los informes. También puede incluir su propio identificador (denominado `distinct_id`) para eventos anónimos que se producen antes de un evento de identificación de usuario.

[!DNL Mixpanel] resuelve los clústeres de identidad mediante dos métodos:

* **Identificar** : [!DNL Mixpanel] conecta el identificador seleccionado con un `distinct_id`. Si el sitio web tiene la variable [!DNL Mixpanel] SDK habilitado, Platform utilizará el `distinct_id` se asigna al usuario que ha iniciado sesión en ese momento.
* **Alias**: [!DNL Mixpanel] combina dos no anónimos `distinct id`s juntos si se cumplen criterios de combinación adicionales.

>[!NOTE]
>
>Consulte la [!DNL Mixpanel] documento en [administración de identidades](https://help.mixpanel.com/hc/en-us/articles/360041039771-Getting-Started-with-Identity-Management#user-identification) para obtener más información sobre estos métodos.
>
>Confirme que ha habilitado la variable [[!DNL Mixpanel] característica de combinación de identidades](#prerequisites-mixpanel) para garantizar que los clústeres de identidad se resuelvan adecuadamente.

### Recopilar los detalles de configuración necesarios {#configuration-details}

Para conectar el Experience Platform a [!DNL Mixpanel] debe tener las siguientes entradas:

| Tipo de clave | Descripción | Ejemplo |
| --- | --- | --- |
| Token del proyecto | El token de proyecto asociado con su [!DNL Mixpanel] cuenta. Consulte la [!DNL Mixpanel] documentación sobre [búsqueda del token del proyecto](https://help.mixpanel.com/hc/en-us/articles/115004502806-Find-Project-Token-) para obtener más información. | `25470xxxxxxxxxxxxxxxxxxx1289` |

## Instale y configure el [!DNL Mixpanel] Extensión {#install}

Para instalar la extensión, [crear una propiedad de reenvío de eventos](../../../ui/event-forwarding/overview.md#properties) o elija una propiedad existente para editarla en su lugar.

Select **[!UICONTROL Extensiones]** en el panel de navegación izquierdo. En el **[!UICONTROL Catálogo]** , seleccione **[!UICONTROL Instalar]** en la tarjeta para la variable [!DNL Mixpanel] extensión.

![La instalación del [!DNL Mixpanel] extensión.](../../../images/extensions/server/mixpanel/install-extension.png)

## Cree un [!DNL Send Event] regla

Comience a crear una regla nueva en la propiedad de reenvío de eventos. En **[!UICONTROL Acciones]**, agregue una nueva acción y establezca la extensión en **[!UICONTROL Panel de mezcla]**. A continuación, establezca el tipo de acción en **[!UICONTROL Rastrear evento]** para enviar eventos de Adobe Experience Edge Network a [!DNL Mixpanel].

| Entrada | Descripción | Requerido |
| --- | --- | --- |
| [!UICONTROL Token del proyecto] | Este campo debe asignarse al token de proyecto asociado con su [!DNL Mixpanel] cuenta. | Sí |
| [!UICONTROL Tipo de evento] | El nombre del evento. | Sí |
| [!UICONTROL Hora del evento] | La hora del evento. |  |
| [!UICONTROL ID distintivo de panel mixto] | Identificador único del usuario que realizó el evento. |  |
| [!UICONTROL Insertar ID] | Identificador único del evento, utilizado para la deduplicación. |  |
| [!UICONTROL Propiedades del evento] | Un objeto JSON que contiene propiedades personalizadas del evento. Seleccione esta opción para proporcionar JSON sin procesar o utilizar un conjunto simplificado de entradas de valor clave. |  |

>[!NOTE]
>
>Para obtener más información sobre los campos estándar de un [!DNL Mixpanel] , consulte la [documentación oficial](https://developer.mixpanel.com/reference/import-events#event).

![Agregue una configuración de acción de regla de reenvío de eventos.](../../../images/extensions/server/mixpanel/track-event-action.png)

Una vez que la variable [!UICONTROL Rastrear evento] se agrega a la regla, puede configurar las condiciones de la regla para que solo se active para ciertos eventos o puede dejar vacía la sección condiciones para que la regla se active para todos los eventos.

>[!IMPORTANT]
>
>Si el sitio web está usando la variable [!DNL Mixpanel] SDK, puede continuar con el siguiente paso de [validar los datos en [!DNL Mixpanel]](#validate). Si no usa la variable [!DNL Mixpanel] SDK, debe [crear una regla de seguimiento de identidad independiente](#create-an-identity-tracking-rule) para garantizar que los eventos y `distinct_id` se envían a [!DNL Mixpanel] cuando se produce un evento de identificación de usuario.

## Validar datos en [!DNL Mixpanel] {#validate}

Si la implementación se realiza correctamente y se recopilan eventos, verá eventos dentro de la variable [[!DNL Mixpanel] consola](https://help.mixpanel.com/hc/en-us/articles/4402837164948).

Compruebe si [!DNL Mixpanel] ha combinado los eventos posteriores al inicio de sesión rellenados con valores de correo electrónico y los eventos creados al usar **[!UICONTROL Enviar evento]**. Si se implementa correctamente, [!DNL Mixpanel] los asociará con un solo [perfil de usuario](https://help.mixpanel.com/hc/en-us/articles/115004501966).

## Pasos siguientes

Esta guía explica cómo enviar eventos de conversión a [!DNL Mixpanel] uso del reenvío de eventos. Esta extensión de reenvío de eventos aprovecha la variable [!DNL Mixpanel] SDK y API de JavaScript. Para obtener más información sobre estas tecnologías subyacentes, consulte la documentación oficial:

* [[!DNL Mixpanel] SDK](https://developer.mixpanel.com/docs/nodejs)
* [[!DNL Mixpanel] API de JavaScript](https://developer.mixpanel.com/docs/javascript-full-api-reference#mixpanelidentify)

Para obtener más información sobre las funcionalidades de reenvío de eventos en Experience Platform, consulte la [información general sobre el reenvío de eventos](../../../ui/event-forwarding/overview.md).
