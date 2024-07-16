---
title: Información general sobre la extensión Meta Pixel
description: Obtenga información acerca de la extensión de etiqueta Meta Pixel en Adobe Experience Platform.
exl-id: c5127bbc-6fe7-438f-99f1-6efdbe7d092e
source-git-commit: 24001da61306a00d295bf9441c55041e20f488c0
workflow-type: tm+mt
source-wordcount: '818'
ht-degree: 0%

---

# Información general sobre la extensión [!DNL Meta Pixel]

[[!DNL Meta Pixel]](https://developers.facebook.com/docs/meta-pixel/) es una herramienta de análisis basada en JavaScript que le permite rastrear la actividad de los visitantes en su sitio web. Las acciones de visitante que rastrea (denominadas conversiones) se envían a [[!DNL Ads Manager]](https://www.facebook.com/business/tools/ads-manager), donde se pueden usar para medir la eficacia de sus anuncios, campañas, canales de conversión y más.

La extensión de etiquetas [!DNL Meta Pixel] le permite aprovechar las funcionalidades de [!DNL Pixel] en las bibliotecas de etiquetas del lado del cliente. Este documento explica cómo instalar la extensión y utilizar sus funcionalidades en una [regla](../../../ui/managing-resources/rules.md).

## Requisitos previos

Para usar la extensión, debe tener una cuenta de [!DNL Meta] válida con acceso a [!DNL Ads Manager]. Específicamente, debe [crear un nuevo [!DNL Meta Pixel]](https://www.facebook.com/business/help/952192354843755) y copiar su [!DNL Pixel ID] para que la extensión se pueda configurar en su cuenta. Si ya tiene un(a) [!DNL Meta Pixel], puede usar su ID en su lugar.

Se recomienda encarecidamente usar [!DNL Meta Pixel] en combinación con [!DNL Meta Conversions API] para compartir y enviar los mismos eventos del lado del cliente y del lado del servidor, respectivamente, ya que esto puede ayudar a recuperar eventos que [!DNL Meta Pixel] no captó. Consulte la guía de la extensión [[!DNL Meta Conversions API] para reenvío de eventos](../../client/meta/overview.md) para ver los pasos necesarios para integrarla en las implementaciones del lado del servidor. Tenga en cuenta que su organización debe tener acceso a [reenvío de eventos](../../../ui/event-forwarding/overview.md) para utilizar la extensión del lado del servidor.

## Instalación de la extensión

Para instalar la extensión [!DNL Meta Pixel], vaya a la IU de recopilación de datos o a la IU del Experience Platform y seleccione **[!UICONTROL Etiquetas]** en el panel de navegación izquierdo. Aquí, seleccione una propiedad a la que añadir la extensión o cree una nueva propiedad.

Una vez que haya seleccionado o creado la propiedad deseada, seleccione **[!UICONTROL Extensiones]** en el panel de navegación izquierdo y, a continuación, seleccione la pestaña **[!UICONTROL Catálogo]**. Busque la tarjeta [!UICONTROL Meta Pixel] y, a continuación, seleccione **[!UICONTROL Instalar]**.

![Se está seleccionando el botón [!UICONTROL Instalar] para la extensión [!UICONTROL Meta Pixel] en la IU de recopilación de datos.](../../../images/extensions/client/meta/install.png)

En la vista de configuración que aparece, debe proporcionar el ID de [!DNL Pixel] que copió anteriormente para vincular la extensión a su cuenta. Puede pegar el ID directamente en la entrada o seleccionar un elemento de datos existente en su lugar.

>[!TIP]
>
>El uso de un elemento de datos le da la opción de cambiar dinámicamente el ID de [!DNL Pixel] que se usa según otros factores, como el entorno de compilación. Consulte la sección del apéndice sobre [uso de [!DNL Pixel] ID diferentes para diferentes entornos](#id-data-element) para obtener más información.

Opcionalmente, también puede proporcionar un ID de evento para asociarlo a la extensión. Se usa para anular la duplicación de eventos idénticos entre [!DNL Meta Pixel] y [!DNL Meta Conversions API]. Para obtener más información, consulte la sección sobre [anulación de duplicación de eventos](../../server/meta/overview.md#event-deduplication) en Información general sobre la extensión [!DNL Conversions API].

Cuando termine, seleccione **[!UICONTROL Guardar]**

![El identificador [!DNL Pixel] proporcionado como elemento de datos en la vista de configuración de la extensión.](../../../images/extensions/client/meta/configure.png)

La extensión está instalada y ahora puede emplear sus distintas acciones en las reglas de etiquetas.

## Configuración de una regla de etiqueta {#rule}

[!DNL Meta Pixel] acepta un conjunto de [eventos estándar](https://www.facebook.com/business/help/402791146561655) predefinidos, cada uno con sus propios contextos y propiedades aceptadas. Las acciones de regla proporcionadas por la extensión [!DNL Pixel] se correlacionan con estos tipos de eventos, lo que permite clasificar y configurar fácilmente el evento que se envía a [!DNL Meta] según su tipo.

Para fines de demostración, esta sección muestra cómo generar una regla que envíe un evento de vista de página a [!DNL Meta].

Comience a crear una nueva regla de etiqueta y configure sus condiciones como desee. Al seleccionar las acciones de la regla, selecciona **[!UICONTROL Meta Pixel]** para la extensión y, a continuación, selecciona **[!UICONTROL Enviar vista de página]** para el tipo de acción.

![Se está seleccionando el tipo de acción [!UICONTROL Enviar vista de página] para una regla en la IU de recopilación de datos.](../../../images/extensions/client/meta/select-action.png)

No se requiere ninguna configuración adicional para la acción [!UICONTROL Enviar vista de página]. Seleccione **[!UICONTROL Conservar cambios]** para agregar la acción a la configuración de regla. Cuando esté satisfecho con la regla, seleccione **[!UICONTROL Guardar en biblioteca]**.

Finalmente, publique una nueva etiqueta [build](../../../ui/publishing/builds.md) para habilitar los cambios en la biblioteca.

## Confirmar que [!DNL Meta] está recibiendo datos

Una vez implementada la compilación actualizada en el sitio web, puede confirmar si los datos se envían según lo esperado generando algunos eventos de conversión en el explorador y comprobando si esos eventos aparecen en [[!DNL Meta Events Manager]](https://www.facebook.com/business/help/898185560232180).

## Pasos siguientes

En esta guía se explica cómo enviar datos a [!DNL Meta] mediante la extensión de etiqueta [!DNL Meta Pixel]. Si planea enviar también eventos del lado del servidor a [!DNL Meta], ahora puede continuar con la instalación y configuración de la [[!DNL Conversions API] extensión de reenvío de eventos](../../server/meta/overview.md).

Para obtener más información sobre las etiquetas en Experience Platform, consulte la [descripción general de las etiquetas](../../../home.md).

## Apéndice: Usar diferentes ID de [!DNL Pixel] para diferentes entornos {#id-data-element}

Si desea probar la implementación en entornos de ensayo o desarrollo mientras mantiene intactos los análisis de producción [!DNL Meta Pixel], puede utilizar un elemento de datos para elegir dinámicamente un ID de [!DNL Pixel] adecuado según el entorno que se utilice.

Puede conseguirlo utilizando un elemento de datos de [!UICONTROL Código personalizado] (proporcionado por la extensión [[!UICONTROL Core]](../core/overview.md)) en combinación con la variable gratuita [`turbine`](../../../extension-dev/turbine.md). En el código JavaScript del elemento de datos, use el objeto `turbine` para encontrar la fase de entorno actual y, a continuación, devuelva un identificador [!DNL Pixel] apropiado basado en el resultado.

El siguiente ejemplo devuelve un identificador de producción falso `exampleProductionKey` cuando se usa en el entorno de producción y un identificador diferente `exampleTestKey` cuando se usa cualquier otro entorno. Al implementar este código, reemplace cada valor por su producción real y pruebe [!DNL Pixel] ID.

```js
return (turbine.environment.stage === "production" ? 'exampleProductionKey' : 'exampleTestKey');
```
