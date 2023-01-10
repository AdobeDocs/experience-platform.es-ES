---
keywords: Experience Platform;inicio;temas populares
solution: Experience Platform
title: Punto final de la API de consentimiento
description: Obtenga información sobre cómo administrar las solicitudes de consentimiento del cliente para aplicaciones de Experience Cloud mediante la API de Privacy Service.
exl-id: ec505749-c0a9-4050-be56-4c0657807ec7
source-git-commit: 0f7ef438db5e7141197fb860a5814883d31ca545
workflow-type: tm+mt
source-wordcount: '247'
ht-degree: 3%

---

# Punto final de consentimiento

Algunas regulaciones requieren el consentimiento explícito del cliente antes de que se puedan recopilar sus datos personales. La variable `/consent` en la variable [!DNL Privacy Service] La API de le permite procesar solicitudes de consentimiento del cliente e integrarlas en su flujo de trabajo de privacidad.

Antes de utilizar esta guía, consulte la [introducción](./getting-started.md) guía para obtener información sobre los encabezados de autenticación requeridos que se presentan en la llamada de API de ejemplo a continuación.

## Procesamiento de una solicitud de consentimiento del cliente

Las solicitudes de consentimiento se procesan realizando una solicitud del POST al `/consent` punto final.

**Formato de API**

```http
POST /consent
```

**Solicitud**

La siguiente solicitud crea un nuevo trabajo de consentimiento para los ID de usuario proporcionados en la variable `entities` matriz.

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
| `optOutOfSale` | Cuando se establece en true, indica que los usuarios proporcionados en `entities` desean excluir la venta o el uso compartido de sus datos personales. |
| `entities` | Matriz de objetos que indica los usuarios a los que se aplica la solicitud de consentimiento. Cada objeto contiene un `namespace` y una matriz de `values` para hacer coincidir usuarios individuales con ese espacio de nombres. |
| `nameSpace` | Cada objeto del `entities` la matriz debe contener uno de los [áreas de nombres de identidad estándar](./appendix.md#standard-namespaces) reconocido por la API de Privacy Service. |
| `values` | Una matriz de valores para cada usuario, correspondiente con los valores proporcionados `nameSpace`. |

{style=&quot;table-layout:auto&quot;}

>[!NOTE]
>
>Para obtener más información sobre cómo determinar a qué valores de identidad de cliente enviar [!DNL Privacy Service], consulte la guía de [proporcionar datos de identidad](../identity-data.md).

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 202 (aceptado) sin carga útil, lo que indica que la solicitud fue aceptada por [!DNL Privacy Service] y se está procesando.
