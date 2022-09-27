---
title: Guía de API de higiene de datos
description: Aprenda a corregir o eliminar mediante programación los datos personales almacenados de sus clientes en Adobe Experience Platform.
exl-id: 78c8b15b-b433-4168-a1e8-c97b96e4bf85
source-git-commit: 724852c63886ea8761b177c4351cca8a6fe748c3
workflow-type: tm+mt
source-wordcount: '345'
ht-degree: 1%

---

# Guía de API de higiene de datos

>[!IMPORTANT]
>
>Actualmente, las funciones de higiene de datos de Adobe Experience Platform solo están disponibles para las organizaciones que han adquirido el Escudo de la salud.

La API de higiene de datos le permite corregir o eliminar mediante programación los datos personales almacenados de sus clientes en Adobe Experience Platform, así como programar fechas de caducidad para conjuntos de datos. Esta guía trata los pasos previos para utilizar la API y proporciona vínculos a documentación más específica del extremo.

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

<!-- ## Work orders

A work order is a representation of a data hygiene task that deletes consumer identities from a specific dataset or all datasets. See the [work order endpoint guide](./workorder.md) for details on working with work orders in the API. -->

## Caducidad de conjuntos de datos

Una caducidad del conjunto de datos es una acción &quot;eliminar un conjunto de datos&quot; con retraso temporal. Al crear una caducidad del conjunto de datos, se especifica un momento futuro en el que ese conjunto de datos debe eliminarse. Consulte la [guía de extremo de caducidad del conjunto de datos](./dataset-expiration.md) para obtener más información sobre la programación de caducidades de conjuntos de datos en la API.

## Cuota

Su organización está limitada a una cuota de trabajo mensual predeterminada para cada tipo de operación de higiene de datos, que puede variar según la licencia. Consulte la [guía de extremo de cuota](./quota.md) para obtener más información sobre la visualización del estado de cuota actual de sus procesos de higiene de datos.

## Pasos siguientes

Esta guía describe cómo administrar las solicitudes de higiene de datos mediante llamadas API. Para obtener información sobre cómo realizar estas acciones en la interfaz de usuario de Platform, consulte la [guía de interfaz de usuario sobre higiene de datos](../ui/overview.md).
