---
keywords: Experience Platform;inicio;temas populares;esquema;XDM;esquemas;esquemas;medida;tipo de datos;tipo de datos;tipo de datos;
solution: Experience Platform
title: Tipo de datos de medida
description: Obtenga información acerca del tipo de datos del Modelo de datos de experiencia de medida (XDM).
exl-id: 5d6cc15d-63cf-4af5-9ae9-12c886dd6735
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '204'
ht-degree: 5%

---

# Tipo de datos [!UICONTROL Measure]

[!UICONTROL Measure] es un tipo de datos XDM (Experience Data Model) estándar que contiene un punto de datos cuantificable concreto de una métrica en particular. Una medida está compuesta por un identificador único y un valor.

<img src="../images/data-types/measure.PNG" width="500" /><br />

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `id` | Cadena | El identificador único de esta medida. En casos de recopilación de datos mediante canales de comunicación con pérdidas, como aplicaciones móviles o sitios web con funcionalidad sin conexión en los que no se puede garantizar la transmisión de medidas, esta propiedad contiene un ID único generado por el cliente de la medida tomada. Se recomienda prolongar esto lo suficiente como para garantizar una aleatoriedad suficiente. <br><br> Si la información como la marca de tiempo, el identificador de dispositivo, la dirección IP, la dirección MAC u otros valores que puedan identificar al usuario se incorporan en la generación de `id`, el resultado debería tener un cifrado hash. Esto garantiza que no se codifique ninguna PII en el valor, ya que el objetivo no es identificar a un usuario o dispositivo, sino la medida específica en el tiempo. |
| `value` | Duplicada | El valor cuantificable de esta medida. |

{style="table-layout:auto"}

Para obtener más información sobre el tipo de datos, consulte el repositorio XDM público:

* [Ejemplo completado](https://github.com/adobe/xdm/blob/master/components/datatypes/data/measure.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/data/measure.schema.json)
