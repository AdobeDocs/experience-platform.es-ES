---
keywords: Experience Platform;inicio;temas populares;esquema;XDM;esquemas;esquemas;Detalles de página web;tipo de datos;tipo de datos;tipo de datos;página web
solution: Experience Platform
title: Tipo de datos del canal de experiencia
description: Obtenga información acerca del tipo de datos del Modelo de datos de experiencia (XDM) del canal de experiencia.
exl-id: 209654f7-0bde-439a-989c-ce2e41599105
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '244'
ht-degree: 24%

---

# [!UICONTROL Tipo de datos del canal de experiencia]

[!UICONTROL Canal de experiencia] es un tipo de datos estándar del Modelo de datos de experiencia (XDM) que describe un canal de experiencia. Un canal de experiencia representa un método o una ruta para el modo en que se consumen las experiencias digitales.

Existen varios canales de experiencia, cada uno con diferentes restricciones sobre cómo se entrega el contenido, y cómo se puede observar la interacción del cliente y cómo se recopilan los datos. Dentro de un canal, las experiencias se pueden entregar a ubicaciones específicas. Las ubicaciones y los tipos de ubicaciones que existen en un canal difieren de uno a otro.

![](../images/data-types/experience-channel.png)

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `_id` | Cadena | ID que identifica de forma exclusiva el canal. Cada canal de experiencia específico define una constante `@id`. |
| `_type` | Cadena | Proporciona una etiqueta de clasificación aproximada para canales con propiedades similares. |
| `contentTypes` | Matriz de cadenas | Los tipos de contenido que este canal puede entregar. |
| `locationTypes` | Matriz de cadenas | Los tipos de ubicaciones (lugares virtuales) en los que se compone este canal y en los que puede entregar contenido. |
| `mediaAction` | Cadena | Describe una acción multimedia de Evento de experiencia, si corresponde. |
| `mediaType` | Cadena | Describe si el tipo de medios es de pago, se posee o se obtiene. |
| `metricTypes` | Matriz de cadenas | Las métricas que se pueden recopilar en este canal. |
| `mode` | Cadena | Cómo se entregan las experiencias en este canal. |
| `typeAtSource` | Cadena | Un nombre personalizado para el canal. |

{style="table-layout:auto"}

Para obtener más información sobre el tipo de datos, consulte el repositorio XDM público:

* [Ejemplo completado](https://github.com/adobe/xdm/blob/master/components/datatypes/channels/channel.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/channels/channel.schema.json)
