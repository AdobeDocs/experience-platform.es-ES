---
keywords: Experience Platform;inicio;temas populares;esquema;Esquema;XDM;campos;esquemas;Esquemas;medida;tipo de datos;tipo de datos;tipo de datos;
solution: Experience Platform
title: Medir tipo de datos
topic: overview
description: Este documento proporciona una visión general del tipo de datos del Modelo de datos de experiencia de medición (XDM).
translation-type: tm+mt
source-git-commit: d282ea5526a05b28c6a82470eabf23e44d1fb420
workflow-type: tm+mt
source-wordcount: '227'
ht-degree: 1%

---


# [!UICONTROL Tipo ] de datos de medición

 Measurement es un tipo de datos estándar del Modelo de datos de experiencia (XDM) que contiene un punto de datos cuantificable concreto de una métrica en particular. Una medida se compone de un identificador único y un valor.

<img src="../images/data-types/measure.PNG" width="500" /><br />

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `id` | Cadena | Identificador único de esta medida. En los casos en que la recopilación de datos utiliza canales de comunicación con pérdida, como aplicaciones móviles o sitios web con funcionalidad sin conexión en los que no se puede garantizar la transmisión de medidas, esta propiedad contiene un ID exclusivo y generado por el cliente de la medida tomada. Se recomienda prolongar esto lo suficiente para garantizar un grado de aleatoriedad suficiente. <br><br> Si la información como la marca de tiempo, el ID del dispositivo, la IP, la dirección MAC u otros valores de identificación de usuarios potenciales se incorpora a la generación del  `id`, el resultado se debe hash. Esto garantiza que no se codifique ninguna PII en el valor, ya que el objetivo no es identificar un usuario o dispositivo, sino la medida específica a tiempo. |
| `value` | Duplicada | Valor cuantificable de esta medida. |

Para obtener más información sobre el tipo de datos, consulte el repositorio público XDM:

* [Ejemplo rellenado](https://github.com/adobe/xdm/blob/master/components/datatypes/data/measure.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/data/measure.schema.json)