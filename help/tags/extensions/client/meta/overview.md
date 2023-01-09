---
title: Información general sobre la extensión de Meta Pixel
description: Obtenga información sobre la extensión de la etiqueta Meta Pixel en Adobe Experience Platform.
exl-id: c5127bbc-6fe7-438f-99f1-6efdbe7d092e
source-git-commit: 24001da61306a00d295bf9441c55041e20f488c0
workflow-type: tm+mt
source-wordcount: '834'
ht-degree: 0%

---

# [!DNL Meta Pixel] información general de la extensión

[[!DNL Meta Pixel]](https://developers.facebook.com/docs/meta-pixel/) es una herramienta de análisis basada en JavaScript que le permite rastrear la actividad de los visitantes en su sitio web. Las acciones de visitante que rastrea (denominadas conversiones) se envían a [[!DNL Ads Manager]](https://www.facebook.com/business/tools/ads-manager) donde se pueden usar para medir la eficacia de sus anuncios, campañas, canales de conversión, etc.

La variable [!DNL Meta Pixel] la extensión de etiquetas le permite aprovechar [!DNL Pixel] en las bibliotecas de etiquetas del lado del cliente. Este documento explica cómo instalar la extensión y utilizar sus capacidades en una [regla](../../../ui/managing-resources/rules.md).

## Requisitos previos

Para utilizar la extensión de , debe tener una [!DNL Meta] cuenta con acceso a [!DNL Ads Manager]. Específicamente, debe [crear una nueva [!DNL Meta Pixel]](https://www.facebook.com/business/help/952192354843755) y copie su [!DNL Pixel ID] por lo tanto, la extensión se puede configurar en su cuenta de . Si ya tiene una [!DNL Meta Pixel], puede usar su ID en su lugar.

Se recomienda encarecidamente utilizar [!DNL Meta Pixel] en combinación con la variable [!DNL Meta Conversions API] para compartir y enviar los mismos eventos desde el lado del cliente y del servidor, respectivamente, ya que esto puede ayudar a recuperar eventos que no fueron recogidos por [!DNL Meta Pixel]. Consulte la guía de [[!DNL Meta Conversions API] extensión para el reenvío de eventos](../../client/meta/overview.md) para ver los pasos sobre cómo integrarlo en las implementaciones del lado del servidor. Tenga en cuenta que su organización debe tener acceso a [reenvío de eventos](../../../ui/event-forwarding/overview.md) para utilizar la extensión del lado del servidor.

## Instalación de la extensión

Para instalar el [!DNL Meta Pixel] , vaya a la IU de recopilación de datos o a la IU del Experience Platform y seleccione **[!UICONTROL Etiquetas]** desde el panel de navegación izquierdo. Desde aquí, seleccione una propiedad a la que añadir la extensión o cree una nueva propiedad.

Una vez seleccionada o creada la propiedad deseada, seleccione **[!UICONTROL Extensiones]** en el panel de navegación izquierdo, seleccione **[!UICONTROL Catálogo]** pestaña . Busque la variable [!UICONTROL Meta píxel] tarjeta y, a continuación, seleccione **[!UICONTROL Instalar]**.

![La variable [!UICONTROL Instalar] botón seleccionado para la variable [!UICONTROL Meta píxel] en la interfaz de usuario de la recopilación de datos.](../../../images/extensions/client/meta/install.png)

En la vista de configuración que aparece, debe proporcionar la variable [!DNL Pixel] ID que ha copiado anteriormente para vincular la extensión a su cuenta de . Puede pegar el ID directamente en la entrada o seleccionar un elemento de datos existente en su lugar.

>[!TIP]
>
>El uso de un elemento de datos le da la opción de cambiar dinámicamente el [!DNL Pixel] ID utilizado según otros factores, como el entorno de compilación. Consulte la sección del apéndice sobre [usar diferentes [!DNL Pixel] ID para diferentes entornos](#id-data-element) para obtener más información.

Si lo desea, también puede proporcionar un ID de evento para asociarlo a la extensión. Se utiliza para deduplicar eventos idénticos entre [!DNL Meta Pixel] y [!DNL Meta Conversions API]. Para obtener más información, consulte la sección sobre [deduplicación de eventos](../../server/meta/overview.md#event-deduplication) en la descripción general para la variable [!DNL Conversions API] extensión.

Cuando termine, seleccione **[!UICONTROL Guardar]**

![La variable [!DNL Pixel] ID proporcionado como elemento de datos en la vista de configuración de la extensión.](../../../images/extensions/client/meta/configure.png)

La extensión está instalada y ahora puede emplear sus distintas acciones en las reglas de etiquetas.

## Configuración de una regla de etiqueta {#rule}

[!DNL Meta Pixel] acepta un conjunto de [eventos estándar](https://www.facebook.com/business/help/402791146561655), cada uno con sus propios contextos y propiedades aceptadas. Las acciones de regla que proporciona el [!DNL Pixel] se correlaciona con estos tipos de eventos, lo que permite categorizar y configurar fácilmente el evento que se envía a [!DNL Meta] según su tipo.

Con fines de demostración, esta sección muestra cómo generar una regla que envíe un evento de vista de página a [!DNL Meta].

Comience a crear una nueva regla de etiqueta y configure sus condiciones como desee. Al seleccionar las acciones para la regla, seleccione **[!UICONTROL Meta píxel]** para la extensión, seleccione **[!UICONTROL Enviar vista de página]** para el tipo de acción.

![La variable [!UICONTROL Enviar vista de página] tipo de acción que se está seleccionando para una regla en la interfaz de usuario de la recopilación de datos.](../../../images/extensions/client/meta/select-action.png)

No se requiere ninguna configuración adicional para la variable [!UICONTROL Enviar vista de página] acción. Select **[!UICONTROL Conservar cambios]** para agregar la acción a la configuración de regla. Cuando esté satisfecho con la regla, seleccione **[!UICONTROL Guardar en biblioteca]**.

Finalmente, publicar una etiqueta nueva [versión](../../../ui/publishing/builds.md) para activar los cambios en la biblioteca.

## Confirme que [!DNL Meta] recibe datos

Una vez que la compilación actualizada se haya implementado en el sitio web, puede confirmar si los datos se envían según lo esperado mediante la generación de algunos eventos de conversión en el explorador y comprobar si dichos eventos aparecen en [[!DNL Meta Events Manager]](https://www.facebook.com/business/help/898185560232180).

## Pasos siguientes

Esta guía trata sobre cómo enviar datos a [!DNL Meta] usando la variable [!DNL Meta Pixel] extensión de etiqueta. Si también planea enviar eventos del lado del servidor a [!DNL Meta], ahora puede proceder a instalar y configurar el [[!DNL Conversions API] extensión de reenvío de eventos](../../server/meta/overview.md).

Para obtener más información sobre las etiquetas en el Experience Platform, consulte [información general sobre las etiquetas](../../../home.md).

## Apéndice: Usar diferentes [!DNL Pixel] ID para diferentes entornos {#id-data-element}

Si desea probar la implementación en entornos de desarrollo o ensayo y mantener la producción [!DNL Meta Pixel] analytics intacto, puede utilizar un elemento de datos para elegir dinámicamente una [!DNL Pixel] ID en función del entorno que se utilice.

Para conseguirlo, utilice un [!UICONTROL Código personalizado] elemento de datos (proporcionado por la variable [[!UICONTROL Principal] Extensión](../core/overview.md)) en combinación con la variable [`turbine` variable libre](../../../extension-dev/turbine.md). En el código JavaScript del elemento de datos, utilice la variable `turbine` para buscar el escenario de entorno actual y, a continuación, devolver un [!DNL Pixel] ID basado en el resultado.

El ejemplo siguiente devuelve un ID de producción falso `exampleProductionKey` cuando se utiliza en el entorno de producción y un ID diferente `exampleTestKey` cuando se utilice cualquier otro entorno. Al implementar este código, reemplace cada valor por su producción y prueba reales [!DNL Pixel] ID.

```js
return (turbine.environment.stage === "production" ? 'exampleProductionKey' : 'exampleTestKey');
```
