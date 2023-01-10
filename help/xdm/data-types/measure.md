---
keywords: Experience Platform;inicio;temas populares;esquema;esquema;XDM;campos;esquemas;esquemas;medida;tipo de datos;tipo de datos;tipo de datos;
solution: Experience Platform
title: Tipo de datos de medida
description: Este documento proporciona información general sobre el tipo de datos del Modelo de datos de experiencia de medición (XDM).
exl-id: 5d6cc15d-63cf-4af5-9ae9-12c886dd6735
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '230'
ht-degree: 3%

---

# [!UICONTROL Medida] tipo de datos

[!UICONTROL Medida] es un tipo de datos estándar del Modelo de datos de experiencia (XDM) que contiene un punto de datos cuantificable concreto de una métrica en particular. Una medida está compuesta por un identificador único y un valor.

<img src="../images/data-types/measure.PNG" width="500" /><br />

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `id` | Cadena | Identificador único de esta medida. En casos de recopilación de datos que utilizan canales de comunicación con pérdidas, como aplicaciones móviles o sitios web con funcionalidad sin conexión en los que no se puede garantizar la transmisión de medidas, esta propiedad contiene un ID único y generado por el cliente de la medida adoptada. Se recomienda hacer esto lo suficientemente largo como para asegurar suficiente aleatoriedad. <br><br> Si la información como la marca de tiempo, el ID del dispositivo, la IP, la dirección MAC u otros valores que puedan identificar al usuario se incorpora en la generación de la variable `id`, el resultado debe tener un cifrado hash. Esto garantiza que no se codifique ningún PII en el valor, ya que el objetivo no es identificar un usuario o dispositivo, sino la medida específica a tiempo. |
| `value` | Doble | El valor cuantificable de esta medida. |

{style=&quot;table-layout:auto&quot;}

Para obtener más información sobre el tipo de datos, consulte el repositorio XDM público:

* [Ejemplo rellenado](https://github.com/adobe/xdm/blob/master/components/datatypes/data/measure.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/data/measure.schema.json)
