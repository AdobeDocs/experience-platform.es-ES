---
title: Guía de API de consulta de auditoría
description: La consulta de auditoría es una API de RESTful que permite a los desarrolladores ver quién realizó qué acciones en Adobe Experience Platform.
exl-id: 9ed291c6-ff8b-4d9b-9fed-d1e3fa8f92fb
source-git-commit: c2c5778e0a3fff7f488ad7a672123c813cca59f1
workflow-type: tm+mt
source-wordcount: '171'
ht-degree: 2%

---

# Guía de la API de [!DNL Audit Query]

La API [!DNL Audit Query] proporciona extremos que le permiten recuperar y supervisar mediante programación los datos de evento de varias características de Adobe Experience Platform. Los extremos se describen a continuación. Visite la [guía de introducción](./getting-started.md) para obtener información importante sobre los encabezados obligatorios, la lectura de llamadas de API de ejemplo y mucho más.

Para ver todos los extremos disponibles y las operaciones de CRUD, visita [[!DNL Audit Query] API swagger](https://www.adobe.io/experience-platform-apis/references/audit-query/).

## Eventos

Los eventos de auditoría proporcionan perspectivas sobre las acciones del usuario en Platform, incluido el tipo de acción, la fecha y la hora, el ID de correo electrónico del usuario que realizó la acción y los atributos adicionales relevantes del tipo de acción para varias funciones de Adobe Experience Platform. Para aprender a recuperar métricas mediante la API, consulte la [guía de extremo de eventos](./events.md).

## Exportar

La exportación de auditoría permite recuperar datos de eventos especificando los eventos que desea recuperar en la carga útil. Para aprender a recuperar métricas mediante la API, consulte la [guía de extremo de exportación](./export.md).
