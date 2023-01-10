---
keywords: Experience Platform;inicio;temas populares;api;API;Sandbox;Sandbox;Sandboxes;Sandboxes
solution: Experience Platform
title: Guía de la API de Sandbox
description: Este documento proporciona información complementaria relacionada con el trabajo con la API de espacio aislado.
exl-id: 48ffea01-f1b4-48c6-a6f5-c321074023d3
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '124'
ht-degree: 1%

---

# Apéndice de la guía de la API de Sandbox

Este documento proporciona información complementaria relacionada con el trabajo con la variable [!DNL Sandbox] API.

## Uso de parámetros de consulta {#query}

La variable [[!DNL Sandbox] API](https://www.adobe.io/experience-platform-apis/references/sandbox) admite el uso de parámetros de consulta en los resultados de filtro y página al enumerar entornos limitados.

>[!NOTE]
>
>La variable `limit` y `offset` los parámetros de consulta deben especificarse juntos. Si solo especifica uno, la API devolverá un error. Si no especifica ninguno, el límite predeterminado es 50 y el desplazamiento es 0.

| Parámetro | Descripción |
| --- | --- |
| `limit` | Número máximo de registros que se van a devolver en la respuesta. |
| `offset` | Número de entidades del primer registro desde el que se inicia (desplaza) la lista de respuestas. |
