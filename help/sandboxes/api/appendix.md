---
keywords: Experience Platform;inicio;temas populares;api;API;Sandbox;Sandbox;Sandboxes;Sandboxes
solution: Experience Platform
title: Guía de la API de Sandbox
description: Este documento proporciona información complementaria relacionada con el trabajo con la API de espacio aislado.
topic-legacy: developer guide
source-git-commit: e4067f79e9da106fe2d2a86fa0024c2e5fe5d0ba
workflow-type: tm+mt
source-wordcount: '128'
ht-degree: 1%

---

# Apéndice de la guía de la API de Sandbox

Este documento proporciona información complementaria relacionada con el trabajo con la API [!DNL Sandbox].

## Uso de parámetros de consulta {#query}

La [[!DNL Sandbox] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sandbox-api.yaml) admite el uso de parámetros de consulta en la página y filtrar los resultados al enumerar entornos limitados.

>[!NOTE]
>
>Los parámetros de consulta `limit` y `offset` deben especificarse juntos. Si solo especifica uno, la API devolverá un error. Si no especifica ninguno, el límite predeterminado es 50 y el desplazamiento es 0.

| Parámetro | Descripción |
| --- | --- |
| `limit` | Número máximo de registros que se van a devolver en la respuesta. |
| `offset` | Número de entidades del primer registro desde el que se inicia (desplaza) la lista de respuestas. |
