---
title: Tipo de datos de informes de detalles de metadatos personalizados
description: Obtenga información sobre el tipo de datos del Modelo de datos de experiencia (XDM) de creación de informes de detalles de metadatos personalizados.
exl-id: d82d42fb-c725-4a81-9b2a-f6434020ab49
source-git-commit: 799a384556b43bc844782d8b67416c7eea77fbf0
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 5%

---

# [!UICONTROL Detalles de metadatos personalizados] Tipo de datos de informe

[!UICONTROL Detalles de metadatos personalizados] La creación de informes es un tipo de datos estándar del Modelo de datos de experiencia (XDM) que define una estructura para almacenar metadatos personalizados. El tipo de datos de informe [!UICONTROL Detalles de metadatos personalizados] captura detalles como el nombre y el valor de los metadatos personalizados asociados con el contenido o las interacciones. Los servicios de Adobe utilizan los campos de creación de informes de contenidos para analizar los campos de recopilación de contenidos enviados por los usuarios. Estos datos, junto con otras métricas de usuario específicas, se calculan y se comunican.

![Un diagrama del tipo de datos del informe de detalles de metadatos personalizados.](../images/data-types/the-custom-metadata-reporting.png)

| Nombre para mostrar | Propiedad | Tipo de datos | Descripción |
|--------------------------------------------|------------------|-----------|-----------------------------------------|
| [!UICONTROL Nombre de campo de metadatos personalizado] | `name` | cadena | Nombre del campo personalizado. |
| [!UICONTROL Valor de campo de metadatos personalizado] | `value` | cadena | El valor del campo personalizado. |

{style="table-layout:auto"}
