---
keywords: Experience Platform;inicio;temas populares;api;API;zona protegida;zona protegida;zonas protegidas;zonas protegidas;zonas protegidas
solution: Experience Platform
title: Apéndice de guía de API de zona protegida
description: Este documento proporciona información complementaria relacionada con el trabajo con la API de zona protegida.
role: Developer
exl-id: 48ffea01-f1b4-48c6-a6f5-c321074023d3
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '122'
ht-degree: 1%

---

# Apéndice de guía de API de zona protegida

Este documento proporciona información complementaria relacionada con el trabajo con [!DNL Sandbox] API.

## Uso de parámetros de consulta {#query}

El [[!DNL Sandbox] API](https://www.adobe.io/experience-platform-apis/references/sandbox) admite el uso de parámetros de consulta para paginar y filtrar los resultados al enumerar zonas protegidas.

>[!NOTE]
>
>El `limit` y `offset` los parámetros de consulta deben especificarse juntos. Si especifica solo uno, la API devolverá un error. Si especifica none, el límite predeterminado es 50 y el desplazamiento es 0.

| Parámetro | Descripción |
| --- | --- |
| `limit` | Número máximo de registros que se devolverán en la respuesta. |
| `offset` | El número de entidades desde el primer registro desde el que se inicia (desplaza) la lista de respuestas. |
