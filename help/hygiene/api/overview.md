---
title: Guía de API de higiene de datos
description: Aprenda a corregir o eliminar mediante programación los datos personales almacenados de sus clientes en Adobe Experience Platform.
exl-id: 78c8b15b-b433-4168-a1e8-c97b96e4bf85
source-git-commit: 566f1b6478cd0de0691cfb2301d5b86fbbfece52
workflow-type: tm+mt
source-wordcount: '445'
ht-degree: 0%

---

# Guía de API de higiene de datos

La API de higiene de datos le permite corregir o eliminar mediante programación los datos personales almacenados de sus clientes en Adobe Experience Platform, así como programar fechas de caducidad para conjuntos de datos. Esta guía describe los pasos previos para utilizar la API y proporciona vínculos a documentación más específica del extremo.

## Introducción

Puede acceder a la API de higiene de datos a través de la siguiente ruta raíz: `https://platform.adobe.io/data/core/hygiene/`

Las secciones siguientes describen los conceptos principales que debe conocer antes de intentar realizar llamadas a la API.

### Recopilar valores para los encabezados obligatorios

Para realizar llamadas a la API de higiene de datos, primero debe recopilar sus credenciales de autenticación. Siga las [Guía de autenticación de API](../../landing/api-authentication.md) para generar valores para cada uno de los encabezados requeridos para la API de higiene de datos, como se muestra a continuación:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Todas las solicitudes que contienen una carga útil (POST, PUT, PATCH) requieren un encabezado adicional:

* `Content-Type: application/json`

### Leer llamadas de API de muestra

Este documento proporciona una llamada de API de ejemplo para demostrar cómo dar formato a sus solicitudes. Para obtener información sobre las convenciones utilizadas en la documentación de las llamadas de API de ejemplo, consulte la sección sobre [cómo leer llamadas de API de ejemplo](../../landing/api-guide.md#sample-api) en la guía de introducción para las API de Experience Platform.

## Caducidad de conjuntos de datos

Una caducidad del conjunto de datos es una acción &quot;eliminar un conjunto de datos&quot; con tiempo de espera. Al crear una caducidad del conjunto de datos, está especificando un momento futuro en el que se debe eliminar ese conjunto de datos. Consulte la [guía de extremo de caducidad del conjunto de datos](./dataset-expiration.md) para obtener más información sobre la programación de caducidades del conjunto de datos en la API.

## Eliminaciones de registros

>[!IMPORTANT]
>
>Las solicitudes de eliminación de registros solo están disponibles para organizaciones que han realizado compras **Adobe Healthcare Shield**.
>
>
>Las eliminaciones de registros están pensadas para utilizarse para limpiar, eliminar datos anónimos o minimizar datos. Lo son **no** para su uso en solicitudes de derechos de titulares de los datos (cumplimiento) relacionadas con regulaciones de privacidad como el Reglamento General de Protección de Datos (RGPD). Para todos los casos de uso de conformidad, utilice [Adobe Experience Platform Privacy Service](../../privacy-service/home.md) en su lugar.

La API de higiene de datos permite eliminar todos los registros asociados con una identidad en uno o todos los conjuntos de datos. Todas las tareas del ciclo de vida de datos que eliminan identidades están representadas por una construcción denominada orden de trabajo. Consulte la [guía de extremo de pedido de trabajo](./workorder.md) para obtener más información sobre cómo trabajar con las eliminaciones de registros en la API.

## Cuota

Su organización se limita a una cuota de trabajo mensual predeterminada para cada tipo de operación del ciclo vital de datos, que puede variar según la licencia. Consulte la [guía de extremo de cuota](./quota.md) para obtener más información sobre cómo ver el estado de cuota actual de los procesos del ciclo vital de datos.

## Pasos siguientes

En esta guía se explica cómo administrar las solicitudes del ciclo vital de datos mediante llamadas a la API. Para obtener información sobre cómo realizar estas acciones en la interfaz de usuario de Platform, consulte [guía de IU del ciclo vital de datos](../ui/overview.md).
