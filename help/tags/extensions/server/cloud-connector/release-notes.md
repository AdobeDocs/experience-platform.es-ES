---
title: Notas de la versión para la extensión Cloud Connector de Adobe Experience Platform
description: Últimas notas de la versión de la extensión Cloud Connector en Adobe Experience Platform.
exl-id: 5ee85d9f-71f4-46ee-9064-4ceee1cf90e7
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: ht
source-wordcount: '128'
ht-degree: 100%

---

# Información general sobre la extensión Cloud Connector de Adobe Experience Platform

>[!NOTE]
>
>Adobe Experience Platform Launch se ha convertido en un grupo de tecnologías de recopilación de datos en Adobe Experience Platform. Como resultado, se han implementado varios cambios terminológicos en la documentación del producto. Consulte el siguiente [documento](../../../term-updates.md) para obtener una referencia consolidada de los cambios terminológicos.

## 17 de enero de 2023

Versión 1.0.1

* Se ha corregido un problema por el que un JSON válido pegado en el área de texto sin procesar del cuerpo se guardaba como una cadena en lugar de como un JSON.
* No permitir que el cuerpo se establezca en solicitudes de GET o HEAD.
* Se ha corregido un error por el que, al guardar una respuesta de más de 5 KB, se producía un error en la ejecución de la regla.
