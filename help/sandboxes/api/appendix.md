---
keywords: Experience Platform;inicio;temas populares;api;API;Sandbox;Sandbox;Sandboxes;Sandboxes
solution: Experience Platform
title: Guía de la API de Sandbox
description: Este documento proporciona información complementaria relacionada con el trabajo con la API de espacio aislado.
topic-legacy: developer guide
source-git-commit: f5ce7b7f09c624c53065757bb8a9b09f989dce0a
workflow-type: tm+mt
source-wordcount: '124'
ht-degree: 1%

---

# Apéndice de la guía de la API de Sandbox

Este documento proporciona información complementaria relacionada con el trabajo con la API [!DNL Sandbox].

## Uso de parámetros de consulta {#query}

La [[!DNL Sandbox] API](https://www.adobe.io/experience-platform-apis/references/sandbox) admite el uso de parámetros de consulta en la página y filtrar los resultados al enumerar entornos limitados.

>[!NOTE]
>
>Los parámetros de consulta `limit` y `offset` deben especificarse juntos. Si solo especifica uno, la API devolverá un error. Si no especifica ninguno, el límite predeterminado es 50 y el desplazamiento es 0.

| Parámetro | Descripción |
| --- | --- |
| `limit` | Número máximo de registros que se van a devolver en la respuesta. |
| `offset` | Número de entidades del primer registro desde el que se inicia (desplaza) la lista de respuestas. |
