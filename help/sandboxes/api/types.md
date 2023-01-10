---
keywords: Experience Platform;inicio;temas populares;entornos limitados de lista
solution: Experience Platform
title: Punto final de la API de tipos de Simulador para pruebas
description: Puede recuperar una lista de tipos de entornos limitados admitidos para su organización realizando una solicitud de GET al extremo /sandboxTypes .
exl-id: eb5e1b44-37f5-4ed5-98f5-ac8db8792c7d
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '162'
ht-degree: 3%

---

# Extremo de tipos de Simulador para pruebas

Puede recuperar una lista de tipos de entornos limitados admitidos para su organización realizando una solicitud de GET al `/sandboxTypes` punto final.

## Primeros pasos

El extremo de API utilizado en esta guía forma parte de la variable [[!DNL Sandbox] API](https://www.adobe.io/experience-platform-apis/references/sandbox). Antes de continuar, revise la [guía de introducción](./getting-started.md) para ver vínculos a documentación relacionada, una guía para leer las llamadas de API de ejemplo en este documento e información importante sobre los encabezados necesarios para realizar llamadas correctamente a cualquier API de Experience Platform.

## Recuperar una lista de tipos de entornos limitados admitidos

Puede recuperar una lista de tipos de entornos limitados admitidos para su organización realizando una solicitud de GET al `/sandboxTypes` punto final.

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
