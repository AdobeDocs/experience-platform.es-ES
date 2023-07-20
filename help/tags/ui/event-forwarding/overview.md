---
title: Información general sobre el reenvío de eventos
description: Obtenga información acerca del reenvío de eventos en Adobe Experience Platform, que le permite utilizar Platform Edge Network para ejecutar tareas sin cambiar la implementación de etiquetas.
feature: Event Forwarding
exl-id: 18e76b9c-4fdd-4eff-a515-a681bc78d37b
source-git-commit: 81f25e74931354003d89a57adedb578ddfe00704
workflow-type: tm+mt
source-wordcount: '1070'
ht-degree: 8%

---

# Información general sobre el reenvío de eventos

>[!NOTE]
>
>El reenvío de eventos es una función de pago que se incluye como parte de las ofertas de Adobe Real-time Customer Data Platform Connections, Prime o Ultimate.

>[!NOTE]
>
>Adobe Experience Platform Launch se ha convertido en un conjunto de tecnologías de recopilación de datos en Adobe Experience Platform. Como resultado, se han implementado varios cambios terminológicos en la documentación del producto. Consulte el siguiente [documento](../../term-updates.md) para obtener una referencia consolidada de los cambios terminológicos.

El reenvío de eventos en Adobe Experience Platform permite enviar datos de evento recopilados a un destino para el procesamiento en el servidor. El reenvío de eventos reduce el peso de páginas web y aplicaciones mediante Adobe Experience Platform Edge Network para ejecutar tareas que se realizan normalmente en el cliente. Las reglas de reenvío de eventos se implementan de forma similar a las etiquetas y pueden transformar y enviar datos a nuevos destinos, pero en lugar de enviar estos datos desde una aplicación cliente como un explorador web, se envían desde los servidores de Adobe.

Este documento proporciona información general de alto nivel sobre el reenvío de eventos en Platform.

![Reenvío de eventos en el ecosistema de recopilación de datos](../../../collection/images/home/event-forwarding.png)

>[!NOTE]
>
>Para obtener información sobre cómo encaja el reenvío de eventos en el ecosistema de recopilación de datos en Platform, consulte la [resumen de recopilación de datos](../../../collection/home.md).

Reenvío de eventos combinado con Adobe Experience Platform [SDK web](../../../edge/home.md) y [Mobile SDK](https://experienceleague.adobe.com/docs/platform-learn/data-collection/mobile-sdk/overview.html) ofrece las siguientes ventajas:

**Rendimiento**:

* Realizar una sola llamada desde una página que contenga una carga útil de datos que luego se federe en el servidor para reducir el tráfico de red del lado del cliente y ofrecer una experiencia más rápida a los clientes.
* Reducir la cantidad de tiempo que tardan las páginas web en cargarse para mejorar el rendimiento del sitio.
* Reduzca la cantidad de tecnologías del lado del cliente necesarias para ofrecer su experiencia y enviar datos a muchos destinos.

**Gobernanza de datos**:

* Aumentar la transparencia y el control sobre los datos que se envían a todas las propiedades.

## Diferencias entre el reenvío de eventos y las etiquetas {#differences-from-tags}

En cuanto a la configuración, el reenvío de eventos utiliza muchos de los mismos conceptos que las etiquetas, como [reglas](../managing-resources/rules.md), [elementos de datos](../managing-resources/data-elements.md), y [extensiones](../managing-resources/extensions/overview.md). La principal diferencia entre ambos puede resumirse de la siguiente manera:

* Etiquetas **recoge** datos de evento de un sitio web o una aplicación móvil nativa y los envía a Platform Edge Network.
* Reenvío de eventos **envía** datos de evento entrantes de Platform Edge Network a un extremo que representa un destino final o un extremo que proporciona datos con los que desea enriquecer la carga útil original.

Mientras que las etiquetas recopilan datos de evento directamente del sitio o de la aplicación móvil nativa mediante los SDK web y móvil de Platform, el reenvío de eventos requiere que los datos de evento ya se envíen a través de Platform Edge Network para reenviarlos a los destinos. En otras palabras, debe implementar el SDK web o móvil de Platform en su propiedad digital (mediante etiquetas o mediante código sin procesar) para utilizar el reenvío de eventos.

### Propiedades {#properties}

El reenvío de eventos mantiene su propio almacén de propiedades separadas de las etiquetas, que puede ver en la interfaz de usuario del Experience Platform o en la interfaz de usuario de recopilación de datos seleccionando **[!UICONTROL Reenvío de eventos]** en el panel de navegación izquierdo.

![Propiedades del reenvío de eventos en la IU de recopilación de datos](../../images/ui/event-forwarding/overview/properties.png)

Lista de todas las propiedades del reenvío de eventos **[!UICONTROL Edge]** como su plataforma. No distinguen entre web o móvil porque solo procesan los datos recibidos de Platform Edge Network, que a su vez puede recibir datos de eventos de plataformas web y móviles.

### Extensiones {#extensions}

El reenvío de eventos tiene su propio catálogo de extensiones compatibles, como [Núcleo](../../extensions/server/core/overview.md) extensión y [Conector de Adobe Cloud](../../extensions/server/cloud-connector/overview.md) extensión. Puede ver las extensiones disponibles para las propiedades de reenvío de eventos en la interfaz de usuario al seleccionar **[!UICONTROL Extensiones]** en el panel de navegación izquierdo, seguido de **[!UICONTROL Catálogo]**.

![Extensiones de reenvío de eventos en la IU de recopilación de datos](../../images/ui/event-forwarding/overview/extensions.png)

### Elementos de datos {#data-elements}

Los tipos de Data Elements disponibles en el reenvío de eventos se limitan al catálogo de [extensiones](#extensions) que los proporcionan.

Aunque los elementos de datos se crean y configuran del mismo modo en el reenvío de eventos que para las etiquetas, existen algunas diferencias de sintaxis importantes en cuanto a cómo hacen referencia a los datos de Platform Edge Network.

#### Referencia a datos de Platform Edge Network {#data-element-path}

Para hacer referencia a datos de Platform Edge Network, debe crear un elemento de datos que proporcione una ruta válida a esos datos. Al crear el elemento de datos en la interfaz de usuario, seleccione **[!UICONTROL Núcleo]** para la extensión y **[!UICONTROL Ruta]** para el tipo.

El **[!UICONTROL Ruta]** el valor del elemento de datos debe seguir el patrón `arc.event.{ELEMENT}` (por ejemplo: `arc.event.xdm.web.webPageDetails.URL`). Esta ruta debe especificarse correctamente para que se envíen los datos.

![Ejemplo de un elemento de datos de tipo de ruta para el reenvío de eventos](../../images/ui/event-forwarding/overview/data-reference.png)

### Reglas {#rules}

La creación de reglas en las propiedades del reenvío de eventos funciona de forma similar a las etiquetas, con la diferencia clave de que no se pueden seleccionar eventos como componentes de regla. En su lugar, una regla de reenvío de eventos procesa todos los eventos que recibe del [secuencia de datos](../../../edge/datastreams/overview.md) y reenvía esos eventos a destinos si se cumplen determinadas condiciones.

Además, se aplica un tiempo de espera de 30 segundos a un solo evento cuando se procesa en todas las reglas (y, por lo tanto, en todas las acciones) dentro de una propiedad de reenvío de eventos. Esto significa que todas las reglas y todas las acciones de un solo evento deben completarse en este lapso de tiempo.

![Reglas de reenvío de eventos en la IU de recopilación de datos](../../images/ui/event-forwarding/overview/rules.png)

#### Tokenización de elementos de datos {#tokenization}

En las reglas de etiquetas, los elementos de datos se identifican mediante token con un `%` al principio y al final del nombre del elemento de datos (por ejemplo: `%viewportHeight%`). En las reglas del reenvío de eventos, los elementos de datos se identifican mediante token con `{{` al principio y `}}` al final del nombre del elemento de datos (por ejemplo: `{{viewportHeight}}`).

![Ejemplo de un elemento de datos de tipo de ruta para el reenvío de eventos](../../images/ui/event-forwarding/overview/tokenization.png)

#### Secuencia de acciones de regla {#action-sequencing}

El [!UICONTROL Acciones] de una regla de reenvío de eventos siempre se ejecuta secuencialmente. Por ejemplo, si una regla tiene dos acciones, la segunda acción no comenzará a ejecutarse hasta que se complete la acción anterior (y en los casos en que se espere una respuesta de un extremo, ese extremo ha respondido). Asegúrese de que el orden de las acciones es correcto al guardar una regla. Esta secuencia de ejecución no se puede ejecutar de forma asíncrona como con las reglas de etiquetas.

## Secretos {#secrets}

El reenvío de eventos permite crear, administrar y almacenar secretos que se pueden utilizar para autenticarse en los servidores a los que envía datos. Consulte la guía de [secretos](./secrets.md) Obtenga información sobre los distintos tipos de tipos de secretos disponibles y cómo se implementan en la interfaz de usuario.

## Pasos siguientes

Este documento proporciona una introducción de alto nivel al reenvío de eventos. Para obtener más información sobre cómo configurar esta función para su organización, consulte la [guía de introducción](./getting-started.md).
