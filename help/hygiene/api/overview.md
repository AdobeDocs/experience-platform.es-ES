---
title: Guía de API de higiene de datos
description: Aprenda a corregir o eliminar mediante programación los datos personales almacenados de sus clientes en Adobe Experience Platform.
role: Developer
exl-id: 78c8b15b-b433-4168-a1e8-c97b96e4bf85
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '446'
ht-degree: 6%

---

# Guía de API de higiene de datos

La API de higiene de datos le permite corregir o eliminar mediante programación los datos personales almacenados de sus clientes en Adobe Experience Platform, así como programar fechas de caducidad para conjuntos de datos. Esta guía describe los pasos previos para utilizar la API y proporciona vínculos a documentación más específica del extremo.

## Introducción

Puede acceder a la API de higiene de datos a través de la siguiente ruta raíz: `https://platform.adobe.io/data/core/hygiene/`

Las secciones siguientes describen los conceptos principales que debe conocer antes de intentar realizar llamadas a la API.

### Recopilación de valores para los encabezados obligatorios

Para realizar llamadas a la API de higiene de datos, primero debe recopilar sus credenciales de autenticación. Siga la [guía de autenticación de API](../../landing/api-authentication.md) para generar valores para cada uno de los encabezados necesarios para la API de higiene de datos, como se muestra a continuación:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Todas las solicitudes que contienen una carga útil (POST, PUT, PATCH) requieren un encabezado adicional:

* `Content-Type: application/json`

### Lectura de llamadas de API de muestra

Este documento proporciona una llamada de API de ejemplo para demostrar cómo dar formato a sus solicitudes. Para obtener información sobre las convenciones utilizadas en la documentación de las llamadas de API de ejemplo, consulte la sección sobre [cómo leer las llamadas de API de ejemplo](../../landing/api-guide.md#sample-api) en la guía de introducción a las API de Experience Platform.

## Caducidades de los conjuntos de datos

Una caducidad del conjunto de datos es una acción &quot;eliminar un conjunto de datos&quot; con tiempo de espera. Al crear una caducidad del conjunto de datos, está especificando un momento futuro en el que se debe eliminar ese conjunto de datos. Consulte la [guía de extremo de caducidad del conjunto de datos](./dataset-expiration.md) para obtener detalles sobre la programación de caducidades del conjunto de datos en la API.

## Eliminaciones de registros

>[!IMPORTANT]
>
>Las solicitudes de eliminación de registros solo están disponibles para las organizaciones que han adquirido **Adobe Healthcare Shield**.
>
>
>Las eliminaciones de registros están pensadas para utilizarse para limpiar, eliminar datos anónimos o minimizar datos. Son **no** para usar en solicitudes de derechos de titulares de datos (cumplimiento) relacionadas con normas de privacidad como el Reglamento General de Protección de Datos (RGPD). Para todos los casos de uso de cumplimiento, usa [Adobe Experience Platform Privacy Service](../../privacy-service/home.md) en su lugar.

La API de higiene de datos permite eliminar todos los registros asociados con una identidad en uno o todos los conjuntos de datos. Todas las tareas del ciclo de vida de datos que eliminan identidades están representadas por una construcción denominada orden de trabajo. Consulte la [guía de extremo de orden de trabajo](./workorder.md) para obtener detalles sobre cómo trabajar con eliminaciones de registros en la API.

## Cuota

Su organización se limita a una cuota de trabajo mensual predeterminada para cada tipo de operación del ciclo vital de datos, que puede variar según la licencia. Consulte la [guía de extremo de cuota](./quota.md) para obtener más información sobre cómo ver el estado de cuota actual de los procesos del ciclo de vida de datos.

## Pasos siguientes

En esta guía se explica cómo administrar las solicitudes del ciclo vital de datos mediante llamadas a la API. Para obtener información sobre cómo realizar estas acciones en la interfaz de usuario de Experience Platform, consulte la [guía de la interfaz de usuario del ciclo vital de datos](../ui/overview.md).
