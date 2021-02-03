---
keywords: Experience Platform;inicio;temas populares;esquema;Esquema;XDM;campos;esquemas;Esquemas;aplicación;tipo de datos;tipo de datos;tipo de datos;
solution: Experience Platform
title: Tipo de datos de la aplicación
topic: overview
description: Este documento proporciona información general sobre el tipo de datos del Modelo de datos de experiencia de la aplicación (XDM).
translation-type: tm+mt
source-git-commit: d282ea5526a05b28c6a82470eabf23e44d1fb420
workflow-type: tm+mt
source-wordcount: '438'
ht-degree: 4%

---


# [!UICONTROL Tipo ] de datos de la aplicación

 Application es un tipo de datos estándar del Modelo de datos de experiencia (XDM) que describe detalles relacionados con las interacciones generadas por la aplicación. Una aplicación hace referencia a una experiencia de software, como una aplicación móvil o de escritorio, que un usuario final puede instalar, ejecutar, cerrar o desinstalar. Las propiedades de este tipo de datos no pretenden describir agentes como chats, complementos basados en explorador u otras experiencias que no se apliquen a las aplicaciones.

<img src="../images/data-types/application.PNG" width="500" /><br />

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `applicationCloses` | [[!UICONTROL Medida]](./measure.md) | Describe los detalles sobre la finalización de una aplicación. |
| `crashes` | [[!UICONTROL Medida]](./measure.md) | Esta propiedad déclencheur cuando la aplicación no sale del modo previsto. |
| `featureUsages` | [[!UICONTROL Medida]](./measure.md) | Describe cualquier dato de la activación de una función de aplicación que se esté midiendo. |
| `firstLaunches` | [[!UICONTROL Medida]](./measure.md) | Contiene datos del primer inicio. Esta propiedad se activa la primera vez que se inicia después de una instalación. |
| `installs` | [[!UICONTROL Medida]](./measure.md) | Registra la instalación de una aplicación en un dispositivo cuando hay un evento de instalación específico disponible. |
| `launches` | [[!UICONTROL Medida]](./measure.md) | Describe un valor asociado al inicio de una aplicación. Esto se activa en cada ejecución, incluidos los bloqueos, las instalaciones y la reanudación desde segundo plano cuando se ha superado el tiempo de espera de sesión. |
| `upgrades` | [[!UICONTROL Medida]](./measure.md) | Contiene datos sobre la actualización de una aplicación que se ha instalado anteriormente. Esto se activa el primer inicio después de una actualización. |
| `id` | Cadena | Identificador único de la aplicación. |
| `name` | Cadena | Nombre de la aplicación  |
| `userPerspective` | Cadena | Perspectiva o relación física entre el usuario y la aplicación o marca en el momento en que se produjo un evento. El comprender la perspectiva del usuario en relación con la aplicación ayuda a generar sesiones de forma precisa, ya que la mayoría de las veces no querrá incluir eventos `background` y `detached` como parte de una sesión &quot;activa&quot;. El valor de esta propiedad debe ser igual a uno de los valores enum que se enumeran a continuación. <li> `foreground`:: El usuario y la aplicación están interactuando directamente entre sí. </li> <li> `background`:: La aplicación y el usuario están interactuando indirectamente entre sí. Por ejemplo, la aplicación podría medir un valor y actualizarse mientras la pantalla está bloqueada o se está utilizando otra aplicación en primer plano.  </li> <li> `detached`:: Desconectado significa que el evento estaba relacionado con la aplicación pero no procedía directamente de la aplicación, como el envío de un correo electrónico o una notificación push desde un sistema externo. |
| `version` | Cadena | Versión de la aplicación. |

Para obtener más información sobre el tipo de datos, consulte el repositorio público XDM:

* [Ejemplo rellenado](https://github.com/adobe/xdm/blob/master/components/datatypes/channels/application.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/channels/application.schema.json)