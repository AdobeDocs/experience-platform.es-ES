---
title: Tipo de datos de informes de detalles de metadatos personalizados
description: Obtenga información sobre el tipo de datos del Modelo de datos de experiencia (XDM) de creación de informes de detalles de metadatos personalizados.
source-git-commit: a604dc8b541784ace8aedef42030e5bd8b646c28
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 4%

---

# [!UICONTROL Detalles de metadatos personalizados] Tipo de datos de informes

[!UICONTROL Detalles de metadatos personalizados] Los informes son un tipo de datos estándar del Modelo de datos de experiencia (XDM) que define una estructura para almacenar metadatos personalizados. El [!UICONTROL Detalles de metadatos personalizados] El tipo de datos de creación de informes captura detalles como el nombre y el valor de los metadatos personalizados asociados al contenido o a las interacciones. Los servicios de Adobe utilizan los campos de creación de informes de contenidos para analizar los campos de recopilación de contenidos enviados por los usuarios. Estos datos, junto con otras métricas de usuario específicas, se calculan y se comunican.

![Un diagrama del tipo de datos del informe de detalles de metadatos personalizados.](../images/data-types/the-custom-metadata-reporting.png)

| Nombre para mostrar | Propiedad | Tipo de datos | Descripción |
|--------------------------------------------|------------------|-----------|-----------------------------------------|
| [!UICONTROL Nombre del campo de metadatos personalizado] | `name` | string | Nombre del campo personalizado. |
| [!UICONTROL Valor del campo de metadatos personalizado] | `value` | string | El valor del campo personalizado. |

{style="table-layout:auto"}
