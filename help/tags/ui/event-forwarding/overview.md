---
title: Información general sobre el reenvío de eventos
description: Obtenga información acerca del reenvío de eventos en Adobe Experience Platform, que le permite utilizar Platform Edge Network para ejecutar tareas sin cambiar la implementación de etiquetas.
feature: Event Forwarding
exl-id: 18e76b9c-4fdd-4eff-a515-a681bc78d37b
source-git-commit: f3c23665229a83d6c63c7d6026ebf463069d8ad9
workflow-type: tm+mt
source-wordcount: '533'
ht-degree: 96%

---

# Información general sobre el reenvío de eventos

>[!NOTE]
>
>Adobe Experience Platform Launch se ha convertido en un conjunto de tecnologías de recopilación de datos en Adobe Experience Platform. Como resultado, se han implementado varios cambios terminológicos en la documentación del producto. Consulte el siguiente [documento](../../term-updates.md) para obtener una referencia consolidada de los cambios terminológicos.

El reenvío de eventos en Adobe Experience Platform reduce el peso de páginas web y aplicaciones mediante Adobe Experience Platform Edge Network para ejecutar tareas que se realizan normalmente en el cliente. Las reglas de reenvío de eventos pueden transformar y enviar datos a nuevos destinos sin cambiar las implementaciones del lado del cliente.

El reenvío de eventos, junto con los SDK móviles y web de Adobe Experience Platform, permite:

* Realizar una sola llamada desde la página que contiene una carga útil de datos. A continuación, los datos se federan del lado del servidor para reducir el tráfico de red del lado del cliente y ofrecer una experiencia más rápida para los clientes.
* Reducir la cantidad de tiempo que tardan las páginas web en cargarse para que el sitio se ajuste a las prácticas recomendadas del sector en cuanto a rendimiento.
* Aumentar la transparencia y el control sobre los tipos de datos que se envían a todas las propiedades de etiquetas.
* Crear una regla de reenvío de eventos para enviar los datos rastreados anteriormente a un nuevo destino.

## Rendimiento mejorado

En un entorno cada vez más competitivo, las empresas deben priorizar el rendimiento para mantener y ampliar la cuota de mercado. El reenvío de eventos mejora el rendimiento del sitio web y la aplicación en los dispositivos móviles, IoT y OTT. Las tasas de conversión del sitio web pueden aumentar debido a los tiempos de carga más rápidos, las aplicaciones móviles no agotan las baterías tan rápido y las aplicaciones OTT ofrecen una sensación tan adaptable como las mismas aplicaciones que se ejecutan en dispositivos móviles. A medida que aumenta el rendimiento, también es común que aumenten las tasas de conversión.

## Mejor gobernanza de datos

A medida que la pila de tecnología crece y los datos se envían a más y más destinos, el desafío de controlar qué datos se envían allí se hace más difícil. La normalización de regulaciones como el RGPD y la CCPA obliga a las compañías a ejercer más control sobre un problema de datos que se está tornando cada vez más difícil.

El reenvío de eventos ayuda a los equipos de marketing a desarrollar su negocio mientras controlan los datos. Eso hace disminuir el número de tecnologías de lado del cliente que los especialistas en marketing necesitan utilizar para llegar a su mercado objetivo y enviar datos a destinos que no sean de Adobe. Esto les facilita a los equipos de implementación la administración de los datos que fluyen desde el cliente a distintos destinos.

## Diferencias entre el reenvío de eventos y las etiquetas

Es importante tener en cuenta las siguientes diferencias entre el reenvío de eventos y las etiquetas:

* Tokenización de elementos de datos

   * Etiquetas: En una regla, los elementos de datos se tokenizan con `%` al principio y al final del nombre del elemento de datos. Por ejemplo, `%viewportHeight%`.

   * Reenvío de eventos: En una regla, los elementos de datos se tokenizan con `{{` al principio y `}}` al final del nombre del elemento de datos. Por ejemplo, `{{viewportHeight}}`.

* Cómo se hace referencia a los datos

   Para hacer referencia a datos de la red de Edge, la ruta del elemento de datos debe ser `arc.event._<element>_`.

   `arc` significa contexto de respuesta de Adobe.

   Por ejemplo: `arc.event.xdm.web.webPageDetails.URL`

   >[!IMPORTANT]
   >
   >Si esta ruta de acceso no se especifica correctamente, no se recopilarán datos.


* Secuencia de acciones de regla

   En la sección Acción de una regla, las reglas del reenvío de eventos siempre se ejecutan secuencialmente. Asegúrese de que el orden de las acciones es correcto al guardar una regla. Esta secuencia de ejecución no se puede elegir como con las etiquetas.

<!--doc Adobe Cloud Connector extension, get from Jon-->
