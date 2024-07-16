---
keywords: Experience Platform;inicio;temas populares;esquema;XDM;esquemas;esquemas;aplicación;tipo de datos;tipo de datos;tipo de datos;
solution: Experience Platform
title: Tipo de datos de aplicación
description: Obtenga información sobre el tipo de datos del Modelo de datos de experiencia de aplicación (XDM).
exl-id: ac7d6761-7b58-4e0d-85e7-6f157fb2eea5
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '416'
ht-degree: 1%

---

# Tipo de datos [!UICONTROL Aplicación]

[!UICONTROL Aplicación] es un tipo de datos estándar del Modelo de datos de experiencia (XDM) que describe detalles relacionados con las interacciones generadas por una aplicación. Una aplicación hace referencia a una experiencia de software, como una aplicación móvil o de escritorio que un usuario final puede instalar, ejecutar, cerrar o desinstalar. Las propiedades de este tipo de datos no están pensadas para describir agentes como bots de chat, complementos basados en explorador u otras experiencias que no se aplican a las aplicaciones.

<img src="../images/data-types/application.PNG" width="500" /><br />

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `applicationCloses` | [[!UICONTROL Medida]](./measure.md) | Describe los detalles de la finalización de una aplicación. |
| `crashes` | [[!UICONTROL Medida]](./measure.md) | Esta propiedad entra en déclencheur cuando la aplicación no se cierra como estaba previsto. |
| `featureUsages` | [[!UICONTROL Medida]](./measure.md) | Describe cualquier dato de la activación de una característica de la aplicación que se esté midiendo. |
| `firstLaunches` | [[!UICONTROL Medida]](./measure.md) | Contiene datos sobre el primer inicio. Esta propiedad se activa en el primer inicio después de una instalación. |
| `installs` | [[!UICONTROL Medida]](./measure.md) | Registra la instalación de una aplicación en un dispositivo cuando hay un evento de instalación específico disponible. |
| `launches` | [[!UICONTROL Medida]](./measure.md) | Describe un valor asociado con el inicio de una aplicación. Se activa en cada ejecución, incluidos los bloqueos, las instalaciones y la reanudación desde segundo plano cuando se ha superado el tiempo de espera de sesión. |
| `upgrades` | [[!UICONTROL Medida]](./measure.md) | Contiene datos sobre la actualización de una aplicación previamente instalada. Se activa en el primer inicio después de una actualización. |
| `id` | Cadena | Un identificador único de la aplicación. |
| `name` | Cadena | Nombre de la aplicación. |
| `userPerspective` | Cadena | La perspectiva o relación física entre el usuario y la aplicación o marca en el momento en que se produjo un evento. Comprender la perspectiva del usuario en relación con la aplicación ayuda a generar sesiones con precisión, ya que la mayoría de las veces no se desean incluir `background` y `detached` eventos como parte de una sesión &quot;activa&quot;. El valor de esta propiedad debe ser igual a uno de los valores de enumeración enumerados a continuación. <li> `foreground`: el usuario y la aplicación están interactuando directamente entre sí. </li> <li> `background`: la aplicación y el usuario están interactuando indirectamente entre sí. Por ejemplo, la aplicación podría medir un valor y actualizarse mientras la pantalla está bloqueada o se está utilizando otra aplicación en primer plano.  </li> <li> `detached`: independiente significa que el evento estaba relacionado con la aplicación, pero no provenía directamente de la aplicación, como el envío de un correo electrónico o una notificación push desde un sistema externo. |
| `version` | Cadena | La versión de la aplicación. |

{style="table-layout:auto"}

Para obtener más información sobre el tipo de datos, consulte el repositorio XDM público:

* [Ejemplo completado](https://github.com/adobe/xdm/blob/master/components/datatypes/channels/application.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/channels/application.schema.json)
