---
title: Guía de resolución de problemas de etiquetas
description: Obtenga respuestas a las preguntas frecuentes sobre Adobe Experience Platform.
exl-id: c06b8e25-4d79-4a11-94da-94ac096b5e33
source-git-commit: 9701a14dc2915e0d6dcc6051c15d5113f305487f
workflow-type: tm+mt
source-wordcount: '1032'
ht-degree: 78%

---

# Guía de solución de problemas con etiquetas

>[!NOTE]
>
>Adobe Experience Platform Launch se ha convertido en un conjunto de tecnologías de recopilación de datos en Adobe Experience Platform. Como resultado, se han implementado varios cambios terminológicos en la documentación del producto. Consulte el siguiente [documento](./term-updates.md) para obtener una referencia consolidada de los cambios terminológicos.

Este documento proporciona respuestas a las preguntas frecuentes acerca de Adobe Experience Platform.

## ¿Qué son las etiquetas?

Las etiquetas son la función de administración de etiquetas de próxima generación que proporciona Adobe y que se integra en Adobe Experience Platform. Las etiquetas permiten a los clientes:

- Implementar productos web del lado del cliente mediante integraciones llamadas *extensiones*
- Distribuya de forma dinámica la configuración para actualizar las implementaciones de cliente en aplicaciones móviles nativas
- Capturar, definir, administrar y compartir datos de forma consistente entre productos de marketing y publicidad de otros proveedores y de Adobe

Las etiquetas son un sistema de entrega de configuración y código avanzado que evalúa las condiciones de las acciones ejecutadas para implementar de forma eficiente las bibliotecas y los productos en el lado del cliente. También ofrece un enfoque altamente escalable para administrar y crear integraciones, y cuenta con un sólido conjunto de API para la interacción programática.

## ¿Cuánto cuestan las etiquetas?

Las etiquetas no suponen ningún coste adicional. Están disponibles para cualquier cliente de [!DNL Adobe Experience Cloud].

## He oído que ahora hay complementos. ¿Qué significa eso?

Las etiquetas están integradas en Adobe Experience Platform y son totalmente ampliables. Los clientes, los socios de Adobe, las agencias y los proveedores de tecnología de publicidad o marketing pueden crear una extensión de etiqueta que añada nuevas funciones o modifique las funciones existentes. El sistema permite a socios y clientes crear, administrar y actualizar sus propias integraciones. Esta es solo una manera en que Adobe abre Adobe Experience Platform para que los clientes y socios puedan crear productos y negocios en él. Esto ayuda a todos los usuarios a conectar la tecnología de Adobe con las tecnologías de marketing y publicidad de otros proveedores con mayor facilidad.

## ¿Todas las extensiones de terceros se ponen a disposición del usuario inmediatamente?

Ya hay extensiones disponibles para soluciones de Adobe y una gran cantidad de proveedores y tecnologías independientes de análisis, marketing, publicidad y consentimiento. Seguimos trabajando con nuestros asociados para ampliar el ecosistema. Debido a que las extensiones pueden crearlas, administrarlas y actualizarlas los propietarios de tecnologías, los clientes no tienen que esperar a que el equipo de ingeniería de Adobe las creen.

## ¿Cuándo pueden los clientes o socios crear extensiones?

Las etiquetas han abierto su portal de autoservicio virtual, que los desarrolladores de extensiones pueden utilizar para construir sus propias integraciones con Adobe Cloud Platform.

Tenemos muchos clientes que también eligen construir sus propias extensiones privadas para usarlas solo dentro de sus propias compañías con los mismos métodos de desarrollo de extensiones.

Para desarrollar una extensión, consulte la página [Información general sobre el desarrollo de extensiones](./extension-dev/overview.md).

## ¿Cumplen las etiquetas con los estándares de seguridad de mi compañía?

Las etiquetas están listas para SOC-2 y la Ley GLBA. Las etiquetas también permiten el alojamiento propio. Las bibliotecas de JavaScript y las configuraciones móviles se pueden reparar desde sus propios servidores o desde la red de distribución de contenido (CDN) que elija. Para los equipos de seguridad y de TI, esto le permite ejecutar pruebas automatizadas, comprobar los archivos en su propio sistema de control de versiones y cumplir todos los procesos de migración de producción interna, ya sean relacionados con la seguridad o de cualquier otro tipo.

## ¿Cuándo puedo pasarme a las etiquetas?

Ahora es el mejor momento para pasar a las etiquetas. El proceso de migración facilita la copia de las propiedades de DTM en las etiquetas. Recomendamos hacer pruebas exhaustivas, pero hemos automatizado todo lo posible (no se han realizado cambios en el código incrustado de la página ni se ha automatizado la migración de reglas y los elementos de datos).

## ¿Admiten las etiquetas aplicaciones de una sola página y mi marco de trabajo favorito?

Sí. Las etiquetas disponen de funcionalidades que permiten flexibilidad a los usuarios y a los desarrolladores de extensiones a la hora de recopilar, gestionar y distribuir datos dentro de experiencias de aplicación de una sola página o páginas o sitios con una gran presencia de Ajax. Esto se aplica independientemente de las preferencias del marco de desarrollo, ya sea Angular, React.js, Ember, Meteor, etc.

## ¿Admiten las etiquetas capas de datos dinámicas?

Sí. Las etiquetas incluyen una extensión que se especializa en detectar cambios en las capas de datos dinámicas.

## ¿Con qué tipos de eventos admiten las etiquetas?

Los tipos de eventos están disponibles a través de las extensiones. La cantidad de tipos de eventos admitidos varía según la extensión. Por ejemplo, la extensión de YouTube incluye cuatro tipos de eventos de vídeo: reproducción, pausa, finalización y tiempo de reproducción. A través de las extensiones, las etiquetas ofrecen compatibilidad con cualquier otro tipo de evento de explorador o tipo de evento sintético, como las secuencias específicas de actividad del visitante.

## ¿Aceleran (o ralentizan) las etiquetas mi sitio web?

Las etiquetas están diseñadas para proporcionar y ejecutar tecnologías de marketing y publicidad en su sitio web de la forma más eficiente posible mediante las prácticas recomendadas actuales. Cuando se utilizan correctamente, se ha comprobado que las etiquetas mejoran el rendimiento de los sitios web sobre otros métodos que proporcionan una funcionalidad similar.

## ¿Con qué exploradores son compatibles las etiquetas?

Consulte los exploradores compatibles [aquí](./extension-dev/browsers.md).

La mayoría de clientes de Adobe ahora aprovecha las funciones más modernas de plataforma web en los exploradores actuales y crean mejores experiencias de usuario, incluidas las aplicaciones de una sola página y las páginas y los sitios web con gran presencia de Ajax. A medida que la mayoría de los clientes avanzan hacia enfoques más modernos con sus sitios, exigen soluciones como etiquetas, que permiten dichos enfoques.

## ¿Las etiquetas funcionan en aplicaciones móviles nativas?

¡Sí! Las etiquetas ahora admiten propiedades y configuración móviles para los nuevos [SDK de dispositivos móviles](https://sdkdocs.com) de Adobe Experience Platform para implementar la recopilación y entrega de datos en un entorno de aplicación móvil nativa. Acceda a [la documentación](https://sdkdocs.com) para obtener más información.

## ¿Por qué la interfaz de usuario indica que se ha producido un error al cargar mi cuenta?

Si recibe un mensaje que indica que se ha producido un error al cargar la cuenta, significa que la cuenta no pertenece a ningún perfil de producto para etiquetas. Consulte la guía sobre [administración de permisos](../collection/permissions.md) para obtener información sobre cómo configurar un perfil de producto en Adobe Admin Console para conceder acceso a las funciones de recopilación de datos en la interfaz de usuario.

## ¿Por qué no se puede agregar ninguna propiedad en la interfaz de usuario?

Si no puede crear ninguna propiedad nueva al iniciar sesión en la interfaz de usuario, significa que su cuenta no pertenece a un perfil de producto que tenga derechos de administración de propiedades.

Consulte la guía sobre [administración de permisos](../collection/permissions.md) para obtener información sobre cómo configurar un perfil de producto en Adobe Admin Console para conceder el derecho Administrar propiedades. Para obtener más información sobre los diferentes derechos de las etiquetas, consulte la descripción general de [permisos de usuario para etiquetas](./ui/administration/user-permissions.md).

## ¿Y si tengo más preguntas?

Si tiene otras preguntas, puede preguntar en la [página de la comunidad de recopilación de datos de Adobe Experience Platform](https://adobe.com/go/launchme) en Experience League o unirse al [espacio de trabajo de Slack de la comunidad](https://docs.google.com/forms/d/e/1FAIpQLScq1m63YkDrRpvPLhzUqtfoleWiDDTTXZsSivIXRfFdlSMzpQ/viewform) para desarrolladores y temas de implementación técnica.
