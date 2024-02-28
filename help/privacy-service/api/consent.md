---
keywords: Experience Platform;inicio;temas populares
solution: Experience Platform
title: Punto final de API de consentimiento
description: Obtenga información sobre cómo administrar las solicitudes de consentimiento de los clientes para aplicaciones de Experience Cloud mediante la API de Privacy Service.
role: Developer
exl-id: ec505749-c0a9-4050-be56-4c0657807ec7
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '245'
ht-degree: 2%

---

# Extremo de consentimiento

Ciertas regulaciones requieren el consentimiento explícito del cliente antes de que se puedan recopilar sus datos personales. El `/consent` punto final en la [!DNL Privacy Service] La API permite procesar las solicitudes de consentimiento de los clientes e integrarlas en el flujo de trabajo de privacidad.

Antes de utilizar esta guía, consulte la [introducción](./getting-started.md) para obtener información sobre los encabezados de autenticación requeridos que se presentan en el ejemplo de llamada de API a continuación.

## Procesamiento de una solicitud de consentimiento de cliente

Las solicitudes de consentimiento se procesan realizando una solicitud de POST a `/consent` punto final.

**Formato de API**

```http
POST /consent
```

**Solicitud**

La siguiente solicitud crea un nuevo trabajo de consentimiento para los ID de usuario proporcionados en el `entities` matriz.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/privacy/consent \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -d '{
        "optOutOfSale": true,
        "entities": [
          {
            "nameSpace": "email",
            "values": [
              "dsmith@acme.com",
              "ajones@acme.com"
            ]
          },
          {
            "nameSpace": "ECID",
            "values": [
              "443636576799758681021090721276"
            ]
          }
        ]
      }'
```

| Propiedad | Descripción |
| --- | --- |
| `optOutOfSale` | Cuando se establece en true, indica que los usuarios proporcionados en `entities` desea excluirse de la venta o del uso compartido de sus datos personales. |
| `entities` | Matriz de objetos que indica los usuarios a los que se aplica la solicitud de consentimiento. Cada objeto contiene un `namespace` y una matriz de `values` para hacer coincidir usuarios individuales con ese área de nombres. |
| `nameSpace` | Cada objeto de la `entities` la matriz debe contener uno de los [áreas de nombres de identidad estándar](./appendix.md#standard-namespaces) reconocido por la API de Privacy Service. |
| `values` | Una matriz de valores para cada usuario, correspondiente al proporcionado `nameSpace`. |

{style="table-layout:auto"}

>[!NOTE]
>
>Para obtener más información sobre cómo determinar qué valores de identidad de cliente enviar a [!DNL Privacy Service], consulte la guía de [proporcionar datos de identidad](../identity-data.md).

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 202 (Aceptado) sin carga útil, lo que indica que aceptó la solicitud [!DNL Privacy Service] y se está procesando.
