---
title: Guía de API de higiene de datos
description: Aprenda a corregir o eliminar mediante programación los datos personales almacenados de sus clientes en Adobe Experience Platform.
exl-id: 78c8b15b-b433-4168-a1e8-c97b96e4bf85
hide: true
hidefromtoc: true
source-git-commit: c2e7cf1859f6a2b277783cdec535ecc208703fac
workflow-type: tm+mt
source-wordcount: '349'
ht-degree: 1%

---

# Guía de API de higiene de datos

>[!IMPORTANT]
>
>Actualmente, las funciones de higiene de datos de Adobe Experience Platform solo están disponibles para las organizaciones que han adquirido Escudo de Adobe para la atención médica.

La API de higiene de datos le permite corregir o eliminar mediante programación los datos personales almacenados de sus clientes en Adobe Experience Platform, así como programar protocolos de tiempo de vida (TTL) para conjuntos de datos. Esta guía trata los pasos previos para utilizar la API y proporciona vínculos a documentación más específica del extremo.

## Primeros pasos

Puede acceder a la API de higiene de datos a través de la siguiente ruta raíz: `https://platform.adobe.io/data/core/hygiene/`

Estas secciones describen los conceptos principales que debe conocer antes de intentar realizar llamadas a la API.

### Recopilar valores para encabezados necesarios

Para realizar llamadas a la API de higiene de datos, primero debe recopilar sus credenciales de autenticación. Siga las [Guía de autenticación de API](../../landing/api-authentication.md) para generar valores para cada uno de los encabezados requeridos para la API de higiene de datos, como se muestra a continuación:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Todas las solicitudes que contienen una carga útil (POST, PUT, PATCH) requieren un encabezado adicional:

* `Content-Type: application/json`

### Leer llamadas de API de ejemplo

Este documento proporciona una llamada API de ejemplo para demostrar cómo dar formato a las solicitudes. Para obtener información sobre las convenciones utilizadas en la documentación para las llamadas de API de ejemplo, consulte la sección sobre [cómo leer llamadas de API de ejemplo](../../landing/api-guide.md#sample-api) en la guía de introducción para las API de Experience Platform.

## Órdenes de trabajo

Una orden de trabajo es una representación de una tarea de higiene de datos que elimina las identidades de los consumidores de un conjunto de datos específico o de todos los conjuntos de datos. Consulte la [guía de extremo del orden de trabajo](./workorder.md) para obtener más información sobre cómo trabajar con órdenes de trabajo en la API.

## Tiempo de vida (TTL) para conjuntos de datos

Un TTL de conjunto de datos es una acción retrasada de &quot;eliminar un conjunto de datos&quot;. Al crear un TTL, está especificando un momento futuro en el que se debe eliminar ese conjunto de datos. Consulte la [guía de extremo de TTL del conjunto de datos](./ttl.md) para obtener más información sobre la programación de TTL de conjuntos de datos en la API.

## Pasos siguientes

Esta guía describe cómo administrar las solicitudes de higiene de datos mediante llamadas API. Para obtener información sobre cómo realizar estas acciones en la interfaz de usuario de Platform, consulte la [guía de interfaz de usuario sobre higiene de datos](../ui/overview.md).
