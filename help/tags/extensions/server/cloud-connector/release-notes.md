---
title: Notas de la versión de la extensión de Adobe Experience Platform Cloud Connector
description: Últimas notas de la versión de la extensión Cloud Connector en Adobe Experience Platform.
source-git-commit: e232ad7a9b581e65f7f4240bbc06155aec409eb7
workflow-type: tm+mt
source-wordcount: '128'
ht-degree: 22%

---

# Notas de la versión de la extensión del conector de Adobe Experience Platform Cloud

>[!NOTE]
>
>Adobe Experience Platform Launch se ha convertido en un conjunto de tecnologías de recopilación de datos en Adobe Experience Platform. Como resultado, se han implementado varios cambios terminológicos en la documentación del producto. Consulte el siguiente [documento](../../../term-updates.md) para obtener una referencia consolidada de los cambios terminológicos.

## 17 de enero de 2023

Versión 1.0.1

* Se ha corregido un problema por el que un JSON válido pegado en el área de texto de Body Raw se guardaba como una cadena en lugar de como un JSON.
* No permita que el Cuerpo se configure en solicitudes de GET o HEAD.
* Se ha corregido un error por el que, al guardar una respuesta mayor que 5 kb, se producía un error en la ejecución de la regla.

