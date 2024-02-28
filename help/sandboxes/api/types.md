---
keywords: Experience Platform;inicio;temas populares;zonas protegidas de lista
solution: Experience Platform
title: Punto final de API de tipos de zona protegida
description: Puede recuperar una lista de tipos de zonas protegidas admitidos para su organización realizando una solicitud de GET al extremo /sandboxTypes.
role: Developer
exl-id: eb5e1b44-37f5-4ed5-98f5-ac8db8792c7d
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '158'
ht-degree: 3%

---

# Extremo de tipos de zona protegida

Puede recuperar una lista de tipos de zonas protegidas compatibles con su organización realizando una solicitud de GET a la variable `/sandboxTypes` punto final.

## Introducción

El extremo de API utilizado en esta guía forma parte del [[!DNL Sandbox] API](https://www.adobe.io/experience-platform-apis/references/sandbox). Antes de continuar, consulte la [guía de introducción](./getting-started.md) para obtener vínculos a documentación relacionada, una guía para leer las llamadas de API de ejemplo en este documento e información importante sobre los encabezados necesarios para realizar correctamente llamadas a cualquier API de Experience Platform.

## Recuperación de una lista de tipos de zonas protegidas admitidos

Puede recuperar una lista de tipos de zonas protegidas compatibles con su organización realizando una solicitud de GET a la variable `/sandboxTypes` punto final.

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

Una respuesta correcta devuelve una lista de tipos de zonas protegidas compatibles con su organización.

```json
{
    "sandboxTypes": [
        "production",
        "development"
    ]
}
```
