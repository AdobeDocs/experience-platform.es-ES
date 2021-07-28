---
title: Preguntas frecuentes
description: Obtenga respuestas a las preguntas más frecuentes sobre las etiquetas en Adobe Experience Platform.
source-git-commit: 7e27735697882065566ebdeccc36998ec368e404
workflow-type: tm+mt
source-wordcount: '904'
ht-degree: 30%

---

# Guía de solución de problemas de etiquetas

>[!NOTE]
>
>Adobe Experience Platform Launch se ha convertido en un conjunto de tecnologías de recopilación de datos en Adobe Experience Platform. Como resultado, se han implementado varios cambios terminológicos en la documentación del producto. Consulte el siguiente [documento](./term-updates.md) para obtener una referencia consolidada de los cambios terminológicos.

Este documento proporciona respuestas a las preguntas más frecuentes sobre las etiquetas en Adobe Experience Platform.

## ¿Qué son las etiquetas?

Las etiquetas son la función de administración de etiquetas de próxima generación que proporciona Adobe y que se integra en Adobe Experience Platform. Las etiquetas permiten a los clientes:

- Implementar productos web del lado del cliente mediante integraciones llamadas *extensiones*
- Distribuya de forma dinámica la configuración para actualizar las implementaciones de cliente en aplicaciones móviles nativas
- Capturar, definir, administrar y compartir datos de forma consistente entre productos de marketing y publicidad de otros proveedores y de Adobe

Las etiquetas son un sistema de entrega de configuración y código avanzado que evalúa las condiciones de las acciones ejecutadas para implementar de forma eficiente las bibliotecas y los productos en el lado del cliente. También proporcionan un enfoque altamente escalable para administrar y crear integraciones y cuentan con un robusto conjunto de API para la interacción mediante programación.

## ¿Cuánto cuestan las etiquetas?

Las etiquetas no suponen ningún coste adicional. Están disponibles para cualquier cliente [!DNL Adobe Experience Cloud].

## He oído que ahora hay complementos. ¿Qué significa eso?

Las etiquetas están integradas en Adobe Experience Platform y son totalmente ampliables. Los clientes, los socios de Adobe, las agencias y los proveedores de tecnología de publicidad o marketing pueden crear una extensión de etiqueta que añada nuevas funciones o modifique las funciones existentes. El sistema permite a socios y clientes crear, administrar y actualizar sus propias integraciones. Esto es solo una manera en que el Adobe abre Adobe Experience Platform para que los clientes y socios puedan crear productos y negocios en él. Esto ayuda a todos los usuarios a conectar la tecnología de Adobe con las tecnologías de marketing y publicidad de otros proveedores con mayor facilidad.

## ¿Todas las extensiones de terceros se ponen a disposición del usuario inmediatamente?

Ya hay extensiones disponibles para soluciones de Adobe y un gran número cada vez mayor de proveedores y tecnologías independientes de análisis, marketing, publicidad y consentimiento. Seguimos trabajando con nuestros asociados para ampliar el ecosistema. Debido a que los propietarios de tecnologías pueden crear, administrar y actualizar extensiones, los clientes no tienen que esperar a que los ingenieros de Adobe las creen.

## ¿Cuándo pueden los clientes o socios crear extensiones?

Las etiquetas han abierto su portal de autoservicio virtual, que los desarrolladores de extensiones pueden utilizar para crear sus propias integraciones con Adobe Cloud Platform.

Tenemos muchos clientes que también eligen construir sus propias extensiones privadas para usarlas solo dentro de sus propias compañías con los mismos métodos de desarrollo de extensiones.

## ¿Las etiquetas cumplen los estándares de seguridad de mi empresa?

Las etiquetas están listas para SOC-2 y la Ley GLBA. Las etiquetas también permiten el alojamiento propio. Las bibliotecas JavaScript y las configuraciones móviles se pueden servir desde sus propios servidores o desde la CDN que elija. Para los equipos de seguridad y de TI, esto le permite ejecutar pruebas automatizadas, comprobar los archivos en su propio sistema de control de versiones y cumplir todos los procesos de migración de producción interna, ya sean relacionados con la seguridad o de cualquier otro tipo.

## ¿Cuándo puedo pasar a las etiquetas?

Ahora es el mejor momento para pasar a las etiquetas . El proceso de migración facilita la copia de las propiedades de DTM en etiquetas. Recomendamos hacer pruebas exhaustivas, pero hemos automatizado todo lo posible (no se han realizado cambios en el código incrustado de la página ni se ha automatizado la migración de reglas y los elementos de datos).

## ¿Las etiquetas admiten aplicaciones de una sola página y mi marco favorito?

Sí. Las etiquetas tienen la capacidad de proporcionar a los usuarios y desarrolladores de extensiones flexibilidad para recopilar, administrar y distribuir datos dentro de experiencias de aplicación de una sola página o páginas o sitios con una gran presencia de Ajax. Esto se aplica independientemente de las preferencias del marco de desarrollo, ya sea Angular, React.js, Ember, Meteor, etc.

## ¿Las etiquetas admiten capas de datos dinámicas?

Sí. Las etiquetas incluyen una extensión que se especializa en detectar cambios en las capas de datos dinámicas.

## ¿Con qué tipos de eventos admiten las etiquetas?

Los tipos de eventos están disponibles a través de las extensiones. La cantidad de tipos de eventos admitidos varía según la extensión. Por ejemplo, la extensión de YouTube incluye cuatro tipos de eventos de vídeo: reproducción, pausa, finalización y tiempo de reproducción. A través de las extensiones, las etiquetas pueden admitir cualquier otro tipo de evento de explorador o tipo de evento sintético, como secuencias específicas de actividad del visitante.

## ¿Las etiquetas aceleran (o ralentizan) mi sitio web?

Las etiquetas están diseñadas para ofrecer y ejecutar tecnologías de marketing y publicidad en su sitio web de la manera más eficiente posible mediante las prácticas recomendadas actuales. Cuando se utilizan correctamente, se ha comprobado que las etiquetas mejoran el rendimiento de los sitios web sobre otros métodos que proporcionan una funcionalidad similar.

## ¿Con qué exploradores son compatibles las etiquetas?

Compatibilidad del explorador con etiquetas:

- [!DNL Chrome] (última versión)
- [!DNL Safari] (última versión)
- [!DNL Firefox] (última versión)
- [!DNL Microsoft Edge] (última versión)
- [!DNL Internet Explorer] (10 y posterior)
- [!DNL iOS Safari] (última versión)
- [!DNL Android Chrome] (última versión)

Compatibilidad del explorador con la interfaz de la aplicación de etiquetas:

- [!DNL Chrome] (última versión)
- [!DNL Safari] (última versión)
- [!DNL Firefox] (última versión)
- [!DNL Microsoft Edge] (última versión)

La mayoría de los clientes de Adobe utilizan funciones de plataforma web más modernas en los navegadores actuales para crear mejores experiencias de usuario, incluidas las aplicaciones de una sola página y las páginas y los sitios web con gran presencia de Ajax. A medida que la mayoría de los clientes avanzan hacia enfoques más modernos con sus sitios, exigen una solución como etiquetas que habiliten dichos enfoques.

## ¿Las etiquetas funcionan en aplicaciones móviles nativas?

¡Sí! Las etiquetas ahora admiten propiedades y configuración móviles para los nuevos SDK para móviles [Adobe Experience Platform](https://sdkdocs.com) para implementar la recopilación y el envío de datos en un entorno nativo de aplicaciones móviles. Acceda a [la documentación](https://sdkdocs.com) para obtener más información.

## ¿Y si tengo más preguntas?

Si tiene otras preguntas, consulte en la Comunidad de Adobe en la página de etiquetas principales que se encuentra en [https://adobe.com/go/launchme](https://adobe.com/go/launchme).

Las etiquetas son solo un ejemplo de hacia dónde se dirige nuestra plataforma: más abierto, más integrado y siempre dedicado al éxito de los clientes.
