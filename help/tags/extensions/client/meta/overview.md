---
title: Información general sobre la extensión Meta Pixel
description: Obtenga información acerca de la extensión de etiqueta Meta Pixel en Adobe Experience Platform.
exl-id: c5127bbc-6fe7-438f-99f1-6efdbe7d092e
source-git-commit: 24001da61306a00d295bf9441c55041e20f488c0
workflow-type: tm+mt
source-wordcount: '834'
ht-degree: 0%

---

# [!DNL Meta Pixel] información general sobre extensiones

[[!DNL Meta Pixel]](https://developers.facebook.com/docs/meta-pixel/) es una herramienta de análisis basada en JavaScript que le permite rastrear la actividad de los visitantes en su sitio web. Las acciones de visitante que rastrea (denominadas conversiones) se envían a [[!DNL Ads Manager]](https://www.facebook.com/business/tools/ads-manager) donde se pueden utilizar para medir la eficacia de los anuncios, campañas, canales de conversión y mucho más.

El [!DNL Meta Pixel] la extensión de etiquetas le permite aprovechar [!DNL Pixel] funcionalidades en las bibliotecas de etiquetas del lado del cliente. Este documento explica cómo instalar la extensión y utilizar sus funcionalidades en una [regla](../../../ui/managing-resources/rules.md).

## Requisitos previos

Para utilizar la extensión de, debe tener un válido [!DNL Meta] cuenta con acceso a [!DNL Ads Manager]. Específicamente, debe [crear un nuevo [!DNL Meta Pixel]](https://www.facebook.com/business/help/952192354843755) y copie sus [!DNL Pixel ID] para que la extensión se pueda configurar en su cuenta de. Si ya tiene un [!DNL Meta Pixel], puede utilizar su ID en su lugar.

Se recomienda encarecidamente utilizar [!DNL Meta Pixel] en combinación con el [!DNL Meta Conversions API] para compartir y enviar los mismos eventos del lado del cliente y del lado del servidor, respectivamente, ya que esto puede ayudar a recuperar eventos que no recogieron [!DNL Meta Pixel]. Consulte la guía en la [[!DNL Meta Conversions API] extensión para reenvío de eventos](../../client/meta/overview.md) para ver los pasos necesarios para integrarlo en las implementaciones del lado del servidor. Tenga en cuenta que su organización debe tener acceso a [reenvío de eventos](../../../ui/event-forwarding/overview.md) para utilizar la extensión del lado del servidor.

## Instalación de la extensión

Para instalar el [!DNL Meta Pixel] extensión, vaya a la IU de recopilación de datos o a la IU del Experience Platform y seleccione **[!UICONTROL Etiquetas]** en el panel de navegación izquierdo. Aquí, seleccione una propiedad a la que añadir la extensión o cree una nueva propiedad.

Una vez seleccionada o creada la propiedad deseada, seleccione **[!UICONTROL Extensiones]** en el panel de navegación izquierdo, seleccione la opción **[!UICONTROL Catálogo]** pestaña. Busque la variable [!UICONTROL Meta píxel] y, a continuación, seleccione **[!UICONTROL Instalar]**.

![El [!UICONTROL Instalar] botón seleccionado para la [!UICONTROL Meta píxel] en la IU de recopilación de datos.](../../../images/extensions/client/meta/install.png)

En la vista de configuración que aparece, debe proporcionar el [!DNL Pixel] ID que copió anteriormente para vincular la extensión a su cuenta. Puede pegar el ID directamente en la entrada o seleccionar un elemento de datos existente en su lugar.

>[!TIP]
>
>El uso de un elemento de datos le da la opción de cambiar dinámicamente la variable [!DNL Pixel] El ID utilizado depende de otros factores, como el entorno de compilación. Consulte la sección del apéndice sobre [uso de diferentes [!DNL Pixel] ID para diferentes entornos](#id-data-element) para obtener más información.

Opcionalmente, también puede proporcionar un ID de evento para asociarlo a la extensión. Se utiliza para deduplicar eventos idénticos entre [!DNL Meta Pixel] y el [!DNL Meta Conversions API]. Para obtener más información, consulte la sección sobre [deduplicación de eventos](../../server/meta/overview.md#event-deduplication) en información general de [!DNL Conversions API] extensión.

Cuando termine, seleccione **[!UICONTROL Guardar]**

![El [!DNL Pixel] El ID proporcionado como elemento de datos en la vista de configuración de la extensión.](../../../images/extensions/client/meta/configure.png)

La extensión está instalada y ahora puede emplear sus distintas acciones en las reglas de etiquetas.

## Configuración de una regla de etiqueta {#rule}

[!DNL Meta Pixel] acepta un conjunto de [eventos estándar](https://www.facebook.com/business/help/402791146561655), cada uno con sus propios contextos y propiedades aceptadas. Las acciones de regla proporcionadas por [!DNL Pixel] Las extensiones de se correlacionan con estos tipos de eventos, lo que permite categorizar y configurar fácilmente el evento que se envía a [!DNL Meta] según su tipo.

Para fines de demostración, esta sección muestra cómo crear una regla que envíe un evento de vista de página a [!DNL Meta].

Comience a crear una nueva regla de etiqueta y configure sus condiciones como desee. Al seleccionar las acciones para la regla, seleccione **[!UICONTROL Meta píxel]** para la extensión, seleccione **[!UICONTROL Enviar vista de página]** para el tipo de acción.

![El [!UICONTROL Enviar vista de página] Tipo de acción seleccionado para una regla de la IU de recopilación de datos.](../../../images/extensions/client/meta/select-action.png)

No se requiere ninguna configuración adicional para el [!UICONTROL Enviar vista de página] acción. Seleccionar **[!UICONTROL Conservar cambios]** para añadir la acción a la configuración de regla. Cuando esté satisfecho con la regla, seleccione **[!UICONTROL Guardar en biblioteca]**.

Por último, publique una etiqueta nueva [generar](../../../ui/publishing/builds.md) para habilitar los cambios en la biblioteca.

## Confirme que [!DNL Meta] está recibiendo datos

Una vez implementada la compilación actualizada en el sitio web, puede confirmar si los datos se envían según lo esperado generando algunos eventos de conversión en el explorador y comprobando si esos eventos aparecen en [[!DNL Meta Events Manager]](https://www.facebook.com/business/help/898185560232180).

## Pasos siguientes

En esta guía se explica cómo enviar datos a [!DNL Meta] uso del [!DNL Meta Pixel] extensión de etiqueta. Si planea enviar también eventos del lado del servidor a [!DNL Meta], ahora puede continuar con la instalación y configuración de [[!DNL Conversions API] extensión de reenvío de eventos](../../server/meta/overview.md).

Para obtener más información sobre las etiquetas en Experience Platform, consulte la [información general sobre etiquetas](../../../home.md).

## Apéndice: usar diferentes [!DNL Pixel] ID para diferentes entornos {#id-data-element}

Si desea probar la implementación en entornos de desarrollo o ensayo mientras mantiene la producción [!DNL Meta Pixel] analytics intacto, puede utilizar un elemento de datos para elegir dinámicamente un [!DNL Pixel] El ID depende del entorno que se utilice.

Puede conseguirlo utilizando una variable [!UICONTROL Código personalizado] elemento de datos (proporcionado por el [[!UICONTROL Núcleo] extensión](../core/overview.md)) en combinación con el [`turbine` variable gratuita](../../../extension-dev/turbine.md). En el código JavaScript del elemento de datos, utilice el `turbine` objeto para buscar el escenario del entorno actual y, a continuación, devolver un [!DNL Pixel] ID basado en el resultado.

El siguiente ejemplo devuelve un ID de producción falso `exampleProductionKey` cuando se utiliza en el entorno de producción y un ID diferente `exampleTestKey` cuando se utiliza cualquier otro entorno. Al implementar este código, reemplace cada valor por su producción y prueba reales [!DNL Pixel] ID.

```js
return (turbine.environment.stage === "production" ? 'exampleProductionKey' : 'exampleTestKey');
```
