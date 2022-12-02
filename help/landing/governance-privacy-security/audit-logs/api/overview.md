---
title: Guía de API de consulta de auditoría
description: La consulta de auditoría es una API de RESTful que permite a los desarrolladores ver quién realizó qué acciones en Adobe Experience Platform.
source-git-commit: 5b3459711f41430977f9d7b06f8b35801739207c
workflow-type: tm+mt
source-wordcount: '175'
ht-degree: 2%

---

# Guía de la API de [!DNL Audit Query]

La variable [!DNL Audit Query] La API proporciona extremos que le permiten recuperar y supervisar mediante programación los datos de evento de varias funciones de Adobe Experience Platform. Los extremos se describen a continuación. Visite el [guía de introducción](./getting-started.md) para obtener información importante sobre los encabezados necesarios, leer llamadas de API de ejemplo y más.

Para ver todos los extremos disponibles y las operaciones de CRUD, visite la [[!DNL Audit Query] Intercambio de API](https://www.adobe.io/experience-platform-apis/references/audit-query/).

## Eventos

Los eventos de auditoría proporcionan información sobre las acciones que realiza el usuario en Platform, incluido el tipo de acción, la fecha y la hora, el ID de correo electrónico del usuario que realizó la acción y atributos adicionales relevantes para el tipo de acción de varias funciones de Adobe Experience Platform. Para obtener información sobre cómo recuperar métricas mediante la API, consulte la [guía de extremo de eventos](./events.md).

## Exportar

La exportación de auditoría permite recuperar datos de eventos especificando los eventos que desea recuperar en la carga útil. Para obtener información sobre cómo recuperar métricas mediante la API, consulte la [exportar guía de extremo](./export.md).
