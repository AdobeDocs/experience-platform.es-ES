---
keywords: Experience Platform;inicio;temas populares;esquema;esquema;XDM;campos;esquemas;esquemas;detalles de página web;tipo de datos;tipo de datos;tipo de datos;página web
solution: Experience Platform
title: Tipo de datos del canal de experiencia
description: Este documento proporciona información general sobre el tipo de datos del Modelo de datos de experiencia de canal de experiencias (XDM).
exl-id: 209654f7-0bde-439a-989c-ce2e41599105
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '271'
ht-degree: 4%

---

# [!UICONTROL Canal de experiencia] tipo de datos

[!UICONTROL Canal de experiencia] es un tipo de datos estándar del Modelo de datos de experiencia (XDM) que describe un canal de experiencia. Un canal de experiencia representa un método o una ruta para el consumo de experiencias digitales.

Hay varios canales de experiencia, cada uno con diferentes restricciones en la forma en que se entrega el contenido, cómo se puede observar la interacción con los clientes y cómo se recopilan los datos. Dentro de un canal, las experiencias se pueden enviar a ubicaciones específicas. Las ubicaciones y los tipos de ubicaciones que existen en un canal difieren de un canal a otro.

![](../images/data-types/experience-channel.png)

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `_id` | Cadena | ID que identifica de forma exclusiva el canal. Cada canal de experiencia específico define una constante `@id`. |
| `_type` | Cadena | Proporciona una etiqueta de clasificación aproximada para canales con propiedades similares. |
| `contentTypes` | Matriz de cadenas | Los tipos de contenido que este canal puede entregar. |
| `locationTypes` | Matriz de cadenas | Tipos de ubicaciones (lugares virtuales) en las que está formado este canal y en las que se puede entregar contenido. |
| `mediaAction` | Cadena | Describe una acción multimedia de Evento de experiencia, si corresponde. |
| `mediaType` | Cadena | Describe si el tipo de medio es de pago, propio o ganado. |
| `metricTypes` | Matriz de cadenas | Las métricas que se pueden recopilar en este canal. |
| `mode` | Cadena | Cómo se entregan las experiencias en este canal. |
| `typeAtSource` | Cadena | Un nombre personalizado para el canal. |

{style=&quot;table-layout:auto&quot;}

Para obtener más información sobre el tipo de datos, consulte el repositorio XDM público:

* [Ejemplo rellenado](https://github.com/adobe/xdm/blob/master/components/datatypes/channels/channel.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/channels/channel.schema.json)
