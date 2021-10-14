---
keywords: Experience Platform;guía del usuario;ai del cliente;temas populares;configurar instancia;crear instancia;
solution: Experience Platform, Intelligent Services, Real-time Customer Data Platform
feature: Customer AI
title: Configuración de una instancia de AI del cliente
topic-legacy: Instance creation
description: Los servicios inteligentes proporcionan Customer AI como un servicio de Adobe Sensei fácil de usar que se puede configurar para diferentes casos de uso. Las secciones siguientes proporcionan los pasos para configurar una instancia de Customer AI.
exl-id: 78353dab-ccb5-4692-81f6-3fb3f6eca886
source-git-commit: c3320f040383980448135371ad9fae583cfca344
workflow-type: tm+mt
source-wordcount: '1549'
ht-degree: 0%

---

# Configuración de una instancia de Customer AI

Customer AI, como parte de Servicios inteligentes, le permite generar puntuaciones de tendencia personalizadas sin tener que preocuparse por el aprendizaje automático.

Los servicios inteligentes proporcionan Customer AI como un servicio de Adobe Sensei fácil de usar que se puede configurar para diferentes casos de uso. Las secciones siguientes proporcionan los pasos para configurar una instancia de Customer AI.

## Configurar la instancia {#set-up-your-instance}

En la interfaz de usuario de Platform, seleccione **[!UICONTROL Services]** en el panel de navegación izquierdo. Aparece el explorador **[!UICONTROL Services]** y muestra todos los servicios disponibles. En el contenedor para Customer AI, seleccione **[!UICONTROL Open]**.

![](../images/user-guide/navigate-to-service.png)

La interfaz de usuario **Customer AI** aparece y muestra todas las instancias de servicio.

- Puede encontrar la métrica **[!UICONTROL Perfiles totales marcados]** ubicada en la parte inferior derecha del contenedor **[!UICONTROL Crear instancia]**. Esta métrica rastrea el número total de perfiles marcados por Customer AI durante el año natural actual, incluidos todos los entornos de espacio aislado y las instancias de servicio eliminadas.

![](../images/user-guide/total-profiles.png)

Las instancias de servicio se pueden editar, clonar y eliminar utilizando los controles del lado derecho de la interfaz de usuario. Para mostrar estos controles, seleccione una instancia de las **[!UICONTROL instancias de servicio]** existentes. Los controles contienen lo siguiente:

- **[!UICONTROL Editar]**: La selección de  **** Editar permite modificar una instancia de servicio existente. Puede editar el nombre, la descripción y la frecuencia de puntuación de la instancia.
- **[!UICONTROL Clonar]**: Si selecciona  **** Clonecopies, se configurará la instancia de servicio seleccionada actualmente. A continuación, puede modificar el flujo de trabajo para realizar ajustes menores y cambiarle el nombre como una nueva instancia.
- **[!UICONTROL Eliminar]**: Puede eliminar una instancia de servicio, incluidas las ejecuciones históricas.
- **[!UICONTROL Fuente]** de datos: Un vínculo al conjunto de datos utilizado por esta instancia.
- **[!UICONTROL Detalles]** de la última ejecución: Esto solo se muestra cuando falla una ejecución. Aquí se muestra información sobre por qué se ha producido un error en la ejecución, como códigos de error.
- **[!UICONTROL Definición]** de puntuación: Información general rápida sobre el objetivo que configuró para esta instancia.

![](../images/user-guide/service-instance-panel.png)

Para crear una nueva instancia, seleccione **[!UICONTROL Crear instancia]**.

![](../images/user-guide/dashboard.png)

Aparece el flujo de trabajo de creación de instancias, comenzando en el paso **[!UICONTROL Configuración]**.

A continuación se proporciona información importante sobre los valores con los que debe proporcionar a la instancia:

- El nombre de la instancia se utiliza en todos los lugares donde se muestran las puntuaciones de Customer AI. Por lo tanto, los nombres deberían describir lo que representan las puntuaciones de predicción, por ejemplo, &quot;Probabilidad de cancelar la suscripción a la revista&quot;.

- El tipo de tendencia determina la intención de la puntuación y la polaridad de la métrica. Puede elegir **[!UICONTROL Conversión]** o **[!UICONTROL Conversión]**. Consulte la nota en [resumen de puntuación](./discover-insights.md#scoring-summary) en el documento de perspectivas de descubrimiento para obtener más información sobre cómo afecta el tipo de tendencia a su instancia.

- La fuente de datos es donde se ubican los datos. El conjunto de datos es el conjunto de datos de entrada que se utiliza para predecir puntuaciones. Por diseño, la Customer AI utiliza datos de Evento de experiencia del consumidor, Adobe Analytics y Adobe Audience Manager para calcular las puntuaciones de tendencia. Al seleccionar un conjunto de datos en el selector desplegable, solo se muestran los que son compatibles con la API del cliente.

- De forma predeterminada, se generan puntuaciones de tendencia para todos los perfiles a menos que se especifique una población apta. Puede especificar una población apta definiendo condiciones para incluir o excluir perfiles según eventos.

Proporcione los valores necesarios y seleccione **[!UICONTROL Next]**.

![](../images/user-guide/setup.png)

### Definir un objetivo {#define-a-goal}

Aparece el paso **[!UICONTROL Definir objetivo]** y proporciona un entorno interactivo para que usted defina visualmente un objetivo de predicción. Un objetivo está compuesto por uno o más eventos, donde la ocurrencia de cada evento se basa en la condición que contiene. El objetivo de una instancia de Customer AI es determinar la probabilidad de alcanzar su objetivo en un lapso de tiempo determinado.

Para crear un objetivo, seleccione **[!UICONTROL Enter Field Name]** y seleccione un campo en la lista desplegable. Seleccione la segunda entrada y seleccione una cláusula para la condición del evento. A continuación, proporcione el valor objetivo para completar el evento. Se pueden configurar eventos adicionales seleccionando **[!UICONTROL Agregar evento]**. Por último, complete el objetivo aplicando un intervalo de tiempo de predicción en cantidad de días y, a continuación, seleccione **[!UICONTROL Siguiente]**.

![](../images/user-guide/goal.png)

#### Ocurrirá y no ocurrirá

Al definir el objetivo, tiene la opción de seleccionar **[!UICONTROL Se producirá]** o **[!UICONTROL No se producirá]**. Seleccionar **[!UICONTROL Se producirá]** significa que las condiciones de evento que defina deben cumplirse para que los datos de evento de un cliente se incluyan en la interfaz de usuario de perspectivas.

Por ejemplo, si desea configurar una aplicación para predecir si un cliente realizará una compra, puede seleccionar **[!UICONTROL Will occur]** seguido de **[!UICONTROL All of]** y luego introducir **commerce.purchases.id** y **exists** como operador.

![ocurrirá](../images/user-guide/occur.png)

Sin embargo, puede haber casos en los que le interese predecir si algún evento no se producirá en un intervalo de tiempo determinado. Para configurar un objetivo con esta opción, seleccione **[!UICONTROL No se producirá]** en la lista desplegable de nivel superior.

Por ejemplo, si le interesa predecir qué clientes participan menos y no visitan la página de inicio de sesión de su cuenta en el mes siguiente. Seleccione **[!UICONTROL No ocurrirá]** seguido de **[!UICONTROL Todos los]** y, a continuación, introduzca **web.webInteraction.URL** y **[!UICONTROL es igual a]** como operador con **inicio de sesión en la cuenta** como valor.

![no se producirá](../images/user-guide/not-occur.png)

#### Todos y cualquiera de

En algunos casos, es posible que desee predecir si se producirá una combinación de eventos y, en otros, es posible que desee predecir la aparición de cualquier evento de un conjunto predefinido. Para predecir si un cliente tendrá una combinación de eventos, seleccione la opción **[!UICONTROL Todos los]** en la lista desplegable de segundo nivel de la página **[!UICONTROL Definir objetivo]**.

Por ejemplo, es posible que desee predecir si un cliente compra un producto en particular. Este objetivo de predicción se define mediante dos condiciones: a `commerce.order.purchaseID` **existe** y `productListItems.SKU` **es igual a** un valor específico.

![Todos los ejemplos](../images/user-guide/all-of.png)

Para predecir si un cliente tendrá algún evento de un conjunto determinado, puede utilizar la opción **[!UICONTROL Cualquiera de]**.

Por ejemplo, es posible que desee predecir si un cliente visita una determinada dirección URL o una página web con un nombre determinado. Este objetivo de predicción se define mediante dos condiciones: `web.webPageDetails.URL` **comienza con** un valor en particular y `web.webPageDetails.name` **comienza con** un valor en particular.

![Cualquiera de los ejemplos](../images/user-guide/any-of.png)

### Eventos personalizados (*opcional*) {#custom-events}

Si tiene información adicional además de los [campos de evento estándar](../input-output.md#standard-events) utilizados por Customer AI para generar puntuaciones de tendencia, se proporciona una opción de eventos personalizada. Si el conjunto de datos seleccionado incluye eventos personalizados definidos en el esquema, puede agregarlos a la instancia.

![función de evento](../images/user-guide/event-feature.png)

Para agregar un evento personalizado, seleccione **[!UICONTROL Agregar evento personalizado]**. A continuación, introduzca un nombre de evento personalizado y asígnelo al campo de evento del esquema. Los nombres de evento personalizados se muestran en lugar del valor de los campos al consultar factores influyentes y otras perspectivas. Esto significa que los ID de usuario, los ID de reserva, la información del dispositivo y otros valores personalizados se enumeran con el nombre del evento personalizado en lugar del ID/valor del evento. La Customer AI utiliza estos eventos personalizados adicionales para mejorar la calidad del modelo y ofrecer resultados más precisos.

![Campo Evento personalizado](../images/user-guide/custom-event.png)

A continuación, seleccione el operador que desee utilizar en la lista desplegable de operadores disponibles. Solo se muestran los operadores compatibles con el evento.

![Operador de eventos personalizados](../images/user-guide/custom-operator.png)

Por último, introduzca los valores de campo si el operador seleccionado requiere uno. En este ejemplo, solo necesitamos ver si existe una reserva de hotel o restaurante. Sin embargo, si queremos ser más exactos, podemos usar el operador equals e introducir un valor exacto en el símbolo del sistema.

![Valor del campo Evento personalizado](../images/user-guide/custom-value.png)

Una vez finalizado, seleccione **[!UICONTROL Next]** en la parte superior derecha para continuar.

### Configurar una programación *(opcional)* {#configure-a-schedule}

Aparece el paso **[!UICONTROL Avanzado]**. Este paso opcional le permite configurar una programación para automatizar las ejecuciones de predicción, definir las exclusiones de predicción para filtrar ciertos eventos o seleccionar **[!UICONTROL Finish]** si no se necesita nada.

Configure una programación de puntuación configurando la **[!UICONTROL Frecuencia de puntuación]**. Las ejecuciones de predicciones automatizadas se pueden programar para que se ejecuten de forma semanal o mensual.

![](../images/user-guide/schedule.png)

### Exclusiones de predicción

Si el conjunto de datos contiene columnas agregadas como datos de prueba, puede agregar esa columna o evento a una lista de exclusión seleccionando **Agregar exclusión** seguido del campo que desea excluir. Esto evita que los eventos que cumplen determinadas condiciones se evalúen al generar puntuaciones. Esta función se puede usar para filtrar entradas de datos irrelevantes o ciertas promociones.

Para excluir un evento, seleccione **[!UICONTROL Add exclude]** y defina el evento. Para eliminar una exclusión, seleccione los puntos suspensivos (**[!UICONTROL ...]**) en la parte superior derecha del contenedor de eventos y, a continuación, seleccione **[!UICONTROL Quitar contenedor]**.

![](../images/user-guide/exclusion.png)

Excluya eventos según sea necesario y luego seleccione **[!UICONTROL Finish]** para crear la instancia.

![](../images/user-guide/advanced.png)

Si la instancia se crea correctamente, se activa inmediatamente una ejecución de predicción y las ejecuciones posteriores se ejecutan según la programación definida.

>[!NOTE]
>
>Según el tamaño de los datos de entrada, las ejecuciones de predicciones pueden tardar hasta 24 horas en completarse.

Al seguir esta sección, ha configurado una instancia de Customer AI y se ejecutó una ejecución de predicción. Una vez finalizada correctamente la ejecución, las perspectivas puntuadas rellenan automáticamente los perfiles con puntuaciones predichas. Espere hasta 24 horas antes de continuar con la siguiente sección de este tutorial.

## Pasos siguientes {#next-steps}

Al seguir este tutorial, ha configurado correctamente una instancia de Customer AI y ha generado puntuaciones de tendencia. Ahora puede elegir usar el Generador de segmentos para [crear segmentos de clientes con puntuaciones predichas](./create-segment.md) o [descubrir perspectivas con Customer AI](./discover-insights.md).

## Recursos adicionales

El siguiente vídeo está diseñado para comprender el flujo de trabajo de configuración de Customer AI. Además, se proporcionan prácticas recomendadas y ejemplos de casos de uso.

>[!VIDEO](https://video.tv.adobe.com/v/32665?learn=on&quality=12)
