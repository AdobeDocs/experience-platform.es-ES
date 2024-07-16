---
keywords: extensión de reenvío de eventos;mixpanel;extensión de reenvío de eventos de mixpanel
title: Extensión de reenvío de eventos API de seguimiento de eventos de Mixpanel
description: Esta extensión de reenvío de eventos de Adobe Experience Platform envía eventos del Edge Network a Mixpanel.
last-substantial-update: 2023-03-29T00:00:00Z
exl-id: 21e2e0fa-4949-4be4-859f-d449d21d8f41
source-git-commit: 3272db15283d427eb4741708dffeb8141f61d5ff
workflow-type: tm+mt
source-wordcount: '892'
ht-degree: 1%

---

# Extensión de reenvío de eventos de API [!DNL Mixpanel Track Events]

[[!DNL Mixpanel]](https://www.mixpanel.com) es una herramienta de análisis de productos que le permite capturar datos sobre cómo los usuarios interactúan con un producto digital. Puede analizar los datos de los productos con informes sencillos e interactivos que le permiten consultar y visualizar los datos con solo unos clics. [!DNL Mixpanel] se diseñó para hacer que los equipos sean más eficientes, ya que permite que todos analicen los datos de los usuarios en tiempo real a fin de identificar tendencias, comprender el comportamiento de los usuarios y tomar decisiones acerca de su producto.

[!DNL Mixpanel] emplea un modelo centrado en el usuario y basado en eventos que conecta cada interacción con un solo usuario. El modelo de datos [!DNL Mixpanel] se basa en los conceptos de usuarios, eventos y propiedades.

>[!NOTE]
>
>Consulte la documentación de [!DNL Mixpanel] sobre [administración de identidades](https://help.mixpanel.com/hc/en-us/articles/360041039771-Getting-Started-with-Identity-Management) para comprender cómo [!DNL Mixpanel] combina eventos para crear clústeres de identidades. También se recomienda que revise el documento sobre [identificadores distintos](https://help.mixpanel.com/hc/en-us/articles/115004509426-Distinct-ID-Creation-JavaScript-iOS-Android-) para comprender cómo se utilizan para identificar a usuarios en los datos de evento.

## Casos de uso

Debe usar esta extensión si desea usar datos del Edge Network en [!DNL Mixpanel] para aprovechar las capacidades de análisis de productos.

Por ejemplo, considere una organización minorista que tenga presencia multicanal (sitio web y móvil). La organización captura los datos de entrada transaccionales o conversacionales como datos de evento de sus plataformas y los carga en [!DNL Mixpanel] mediante la extensión de reenvío de eventos.

Los equipos de análisis pueden aprovechar las capacidades de [!DNL Mixpanel's] para procesar los conjuntos de datos y obtener perspectivas comerciales, que se pueden usar para generar gráficos, paneles u otras visualizaciones para informar a las partes interesadas empresariales.

Para obtener más información sobre casos de uso específicos de [!DNL Mixpanel], consulte la siguiente documentación:

* [Nuevo en [!DNL Mixpanel]](https://docs.mixpanel.com/docs)
* [¿Qué es  [!DNL Mixpanel]?](https://developer.mixpanel.com/docs)
* [12  [!DNL Mixpanel] características](https://mixpanel.com/blog/12-things-you-probably-didnt-know-you-could-do-with-mixpanel/) que se deben probar

## [!DNL Mixpanel] requisitos previos {#prerequisites-mixpanel}

Debe tener una cuenta de [!DNL Mixpanel] válida para utilizar esta extensión. Vaya a la [[!DNL Mixpanel] página de registro](https://mixpanel.com/register/) para registrarse y crear una cuenta si todavía no la tiene.

Asegúrese de que la configuración [[!DNL Identity Merge]](https://help.mixpanel.com/hc/en-us/articles/9648680824852-ID-Merge-Implementation-Best-Practices) esté habilitada para su proyecto. Vaya a **[!DNL Settings]** > **[!DNL Project Setting]** > **[!DNL Identity Merge]** y cambie la configuración.

### Explicación de los clústeres de identidad en [!DNL Mixpanel]

En [!DNL Mixpanel], un clúster de identidad contiene una colección de `distinct_id` valores que se conectan a un usuario individual. [!DNL Mixpanel] administra el clúster de identidades de cada usuario, resolviendo un único `distinct_id` canónico de cada clúster que se utilizará en los informes. También puede incluir su propio identificador (denominado `distinct_id` local) para los eventos anónimos que ocurren antes de un evento de identificación de usuario.

[!DNL Mixpanel] resuelve los clústeres de identidad mediante dos métodos:

* **Identificar** : [!DNL Mixpanel] conecta el identificador seleccionado con un `distinct_id` anónimo. Si el sitio web tiene habilitado el SDK [!DNL Mixpanel], Platform usará el(la) `distinct_id` asignado(a) al usuario que ha iniciado sesión actualmente.
* **Alias**: [!DNL Mixpanel] combina dos `distinct id`s no anónimos si se cumplen criterios de combinación adicionales.

>[!NOTE]
>
>Consulte el documento [!DNL Mixpanel] sobre [administración de identidades](https://help.mixpanel.com/hc/en-us/articles/360041039771-Getting-Started-with-Identity-Management#user-identification) para obtener más información sobre estos métodos.
>
>Confirme que ha habilitado la [[!DNL Mixpanel] característica de combinación de identidades](#prerequisites-mixpanel) para asegurarse de que los clústeres de identidades se resuelven correctamente.

### Recopilar detalles de configuración necesarios {#configuration-details}

Para conectar el Experience Platform a [!DNL Mixpanel], debe tener las siguientes entradas:

| Tipo de clave | Descripción | Ejemplo |
| --- | --- | --- |
| Token de proyecto | El token de proyecto asociado con su cuenta de [!DNL Mixpanel]. Consulte la documentación de [!DNL Mixpanel] sobre [cómo encontrar el token de su proyecto](https://help.mixpanel.com/hc/en-us/articles/115004502806-Find-Project-Token-) para obtener instrucciones. | `25470xxxxxxxxxxxxxxxxxxx1289` |

## Instalar y configurar la extensión [!DNL Mixpanel] {#install}

Para instalar la extensión, [cree una propiedad de reenvío de eventos](../../../ui/event-forwarding/overview.md#properties) o elija una propiedad existente para editar en su lugar.

Seleccione **[!UICONTROL Extensiones]** en el panel de navegación izquierdo. En la ficha **[!UICONTROL Catálogo]**, seleccione **[!UICONTROL Instalar]** en la tarjeta de la extensión [!DNL Mixpanel].

![Instalando la extensión [!DNL Mixpanel].](../../../images/extensions/server/mixpanel/install-extension.png)

## Crear una regla [!DNL Send Event]

Comience a crear una nueva regla en la propiedad de reenvío de eventos. En **[!UICONTROL Acciones]**, agregue una nueva acción y establezca la extensión en **[!UICONTROL Mixpanel]**. A continuación, establezca el tipo de acción en **[!UICONTROL Rastrear evento]** para enviar eventos de Edge Network a [!DNL Mixpanel].

| Entrada | Descripción | Requerido |
| --- | --- | --- |
| [!UICONTROL Token de proyecto] | Este campo debe asignarse al token de proyecto asociado con su cuenta de [!DNL Mixpanel]. | Sí |
| [!UICONTROL Tipo de evento] | Nombre del evento. | Sí |
| [!UICONTROL Hora del evento] | La hora del evento. | |
| [!UICONTROL Id. distinto de Mixpanel] | El identificador único del usuario que realizó el evento. | |
| [!UICONTROL Insertar ID] | Identificador único del evento que se utiliza para la anulación de duplicación. | |
| [!UICONTROL Propiedades de evento] | Objeto JSON que contiene propiedades personalizadas del evento. Seleccione entre proporcionar JSON sin procesar o utilizar un conjunto simplificado de entradas de clave-valor. | |

>[!NOTE]
>
>Para obtener más información sobre los campos estándar para un evento [!DNL Mixpanel], consulte la [documentación oficial](https://developer.mixpanel.com/reference/import-events#event).

![Agregar una configuración de acción de regla de reenvío de eventos.](../../../images/extensions/server/mixpanel/track-event-action.png)

Una vez que la acción [!UICONTROL Track Event] se agregue a la regla, puede configurar las condiciones de la regla para que solo se active para determinados eventos o puede dejar vacía la sección de condiciones para que la regla se active para todos los eventos.

>[!IMPORTANT]
>
>Si su sitio web usa el SDK [!DNL Mixpanel], puede continuar con el siguiente paso de [validación de los datos en [!DNL Mixpanel]](#validate). Si no usa el SDK [!DNL Mixpanel], debe [crear una regla de seguimiento de identidad](#create-an-identity-tracking-rule) independiente para asegurarse de que los eventos apropiados y los valores de `distinct_id` se envíen a [!DNL Mixpanel] cuando se produzca un evento de identificación de usuario.

## Validar datos dentro de [!DNL Mixpanel] {#validate}

Si la implementación se realiza correctamente y se recopilan eventos, verá eventos dentro de la [[!DNL Mixpanel] consola](https://help.mixpanel.com/hc/en-us/articles/4402837164948).

Compruebe si [!DNL Mixpanel] ha combinado los eventos posteriores al inicio de sesión con los valores de correo electrónico y los eventos creados al usar **[!UICONTROL Enviar evento]**. Si se implementa correctamente, [!DNL Mixpanel] los asociará con un solo [perfil de usuario](https://help.mixpanel.com/hc/en-us/articles/115004501966).

## Pasos siguientes

En esta guía se explica cómo enviar eventos de conversión a [!DNL Mixpanel] mediante el reenvío de eventos. Esta extensión de reenvío de eventos aprovecha el SDK [!DNL Mixpanel] y la API de JavaScript. Para obtener más información sobre estas tecnologías subyacentes, consulte la documentación oficial:

* [[!DNL Mixpanel] SDK](https://developer.mixpanel.com/docs/nodejs)
* [[!DNL Mixpanel] API de JavaScript](https://developer.mixpanel.com/docs/javascript-full-api-reference#mixpanelidentify)

Para obtener más información sobre las funcionalidades de reenvío de eventos en Experience Platform, consulte la [descripción general del reenvío de eventos](../../../ui/event-forwarding/overview.md).
