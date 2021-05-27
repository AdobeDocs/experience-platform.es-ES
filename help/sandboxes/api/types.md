---
keywords: Experience Platform;inicio;temas populares;entornos limitados de lista
solution: Experience Platform
title: Punto final de la API de tipos de Simulador para pruebas
topic-legacy: developer guide
description: Puede recuperar una lista de tipos de entornos limitados admitidos para su organización realizando una solicitud de GET al extremo /sandboxTypes .
exl-id: eb5e1b44-37f5-4ed5-98f5-ac8db8792c7d
source-git-commit: e644fe9a2faf8692617f6bbee2b91a52c323ff5d
workflow-type: tm+mt
source-wordcount: '166'
ht-degree: 2%

---

# Extremo de tipos de Simulador para pruebas

Puede recuperar una lista de tipos de entornos limitados admitidos para su organización realizando una solicitud de GET al extremo `/sandboxTypes` .

## Primeros pasos

El extremo de API utilizado en esta guía forma parte de la [[!DNL Sandbox] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sandbox-api.yaml). Antes de continuar, consulte la [guía de introducción](./getting-started.md) para ver los vínculos a la documentación relacionada, una guía para leer las llamadas de API de ejemplo en este documento e información importante sobre los encabezados necesarios que se necesitan para realizar llamadas correctamente a cualquier API de Experience Platform.

## Recuperar una lista de tipos de entornos limitados admitidos

Puede recuperar una lista de tipos de entornos limitados admitidos para su organización realizando una solicitud de GET al extremo `/sandboxTypes` .

**Formato de API**

```http
GET /sandboxTypes
```

**Solicitud**

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxTypes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

**Respuesta**

Una respuesta correcta devuelve una lista de tipos de entornos limitados compatibles con su organización.

```json
{
    "sandboxTypes": [
        "production",
        "development"
    ]
}
```
