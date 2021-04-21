---
keywords: Experience Platform;inicio;temas populares;esquema;esquema;XDM;campos;esquemas;esquemas;aplicación;tipo de datos;tipo de datos;tipo de datos;
solution: Experience Platform
title: Tipo de datos de aplicación
topic-legacy: overview
description: Este documento proporciona información general sobre el tipo de datos del Modelo de datos de experiencia de la aplicación (XDM).
exl-id: ac7d6761-7b58-4e0d-85e7-6f157fb2eea5
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '429'
ht-degree: 2%

---

# [!UICONTROL Application] tipo de datos

[!UICONTROL Application] es un tipo de datos estándar del Modelo de datos de experiencia (XDM) que describe detalles relacionados con las interacciones generadas por la aplicación. Una aplicación hace referencia a una experiencia de software, como una aplicación móvil o de escritorio que un usuario final puede instalar, ejecutar, cerrar o desinstalar. Las propiedades de este tipo de datos no están pensadas para describir agentes como bots de chat, complementos basados en navegador u otras experiencias que no se aplican a aplicaciones.

<img src="../images/data-types/application.PNG" width="500" /><br />

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `applicationCloses` | [[!UICONTROL Measure]](./measure.md) | Describe los detalles sobre la finalización de una aplicación. |
| `crashes` | [[!UICONTROL Measure]](./measure.md) | Esta propiedad se déclencheur cuando la aplicación no se cierra como está previsto. |
| `featureUsages` | [[!UICONTROL Measure]](./measure.md) | Describe cualquier dato de la activación de una función de aplicación que se esté midiendo. |
| `firstLaunches` | [[!UICONTROL Measure]](./measure.md) | Contiene datos del primer inicio. Esta propiedad se activa al iniciarse por primera vez después de una instalación. |
| `installs` | [[!UICONTROL Measure]](./measure.md) | Registra la instalación de una aplicación en un dispositivo cuando hay disponible un evento de instalación específico. |
| `launches` | [[!UICONTROL Measure]](./measure.md) | Describe un valor asociado con el inicio de una aplicación. Esto se activa en cada ejecución, incluidos los bloqueos, las instalaciones y la reanudación desde segundo plano cuando se supera el tiempo de espera de la sesión. |
| `upgrades` | [[!UICONTROL Measure]](./measure.md) | Contiene datos sobre la actualización de una aplicación que se ha instalado anteriormente. Esto se activa en el primer inicio después de una actualización. |
| `id` | Cadena | Identificador único de la aplicación. |
| `name` | Cadena | Nombre de la aplicación  |
| `userPerspective` | Cadena | Perspectiva o relación física entre el usuario y la aplicación o marca en el momento en que se produjo un evento. Comprender la perspectiva del usuario en relación con la aplicación le ayuda a generar sesiones de forma precisa, ya que la mayoría de las veces no querrá incluir eventos `background` y `detached` como parte de una sesión &quot;activa&quot;. El valor de esta propiedad debe ser igual a uno de los valores de enumeración enumerados a continuación. <li> `foreground`: El usuario y la aplicación están interactuando directamente entre sí. </li> <li> `background`: La aplicación y el usuario están interactuando de forma indirecta entre sí. Por ejemplo, la aplicación podría medir un valor y actualizarse mientras la pantalla está bloqueada o se está utilizando otra aplicación en primer plano.  </li> <li> `detached`: Desconectado significa que el evento estaba relacionado con la aplicación, pero no provino directamente de la aplicación, como el envío de un correo electrónico o una notificación push desde un sistema externo. |
| `version` | Cadena | Versión de la aplicación. |

Para obtener más información sobre el tipo de datos, consulte el repositorio XDM público:

* [Ejemplo rellenado](https://github.com/adobe/xdm/blob/master/components/datatypes/channels/application.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/channels/application.schema.json)
