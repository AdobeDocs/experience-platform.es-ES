---
title: Tipo de datos del informe de estado del reproductor
description: Obtenga información acerca del tipo de datos del Modelo de datos de experiencia (XDM) de creación de informes de datos de estado del reproductor.
source-git-commit: b6b916c76d1b2babb673d419ab69ae414dd42f20
workflow-type: tm+mt
source-wordcount: '189'
ht-degree: 4%

---

# [!UICONTROL Informes de datos de estado del reproductor] tipo de datos

[!UICONTROL Informes de datos de estado del reproductor] es un tipo de datos estándar del Modelo de datos de experiencia (XDM) que describe los distintos estados y sus ocurrencias dentro de un reproductor de contenido. Utilice el [!UICONTROL Informes de datos de estado del reproductor] tipo de datos para capturar diferentes estados del reproductor, como pantalla completa, silencio, subtítulos, imagen en imagen y estados de enfoque. Para cada estado, registra si se establece el estado, el recuento de ocurrencias y la duración total que permanece activa durante la reproducción del contenido.

![Diagrama del tipo de datos de informes de datos de estado del reproductor.](../images/data-types/player-state-data-information.png)

| Nombre para mostrar | Propiedad | Tipo de datos | Descripción |
|-------------------|----------------|-----------|----------------------------------------------|
| [!UICONTROL Nombre del estado del reproductor] | `name` | string | Nombre del estado del reproductor. Enumerado: &quot;pantalla completa&quot;, &quot;silenciar&quot;, &quot;closedCaptioning&quot;, &quot;pictureInPicture&quot;, &quot;inFocus&quot; con los significados respectivos. |
| [!UICONTROL Conjunto de estado del reproductor] | `isSet` | Booleano | Si el estado del reproductor está en ese estado o no. |
| [!UICONTROL Recuento de estados del reproductor] | `count` | entero | La cantidad de veces que se estableció el estado del reproductor en el flujo. |
| [!UICONTROL Hora de estado del reproductor] | `time` | entero | La duración total del estado del reproductor. |

{style="table-layout:auto"}

Para obtener más información sobre el grupo de campos, consulte la [repositorio XDM público](https://github.com/adobe/xdm/blob/master/components/datatypes/playerstatedata.schema.json)
