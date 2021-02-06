---
keywords: Experience Platform;inicio;temas populares
solution: Experience Platform
title: Extremo de la API de consentimiento
topic: developer guide
description: Obtenga información sobre cómo administrar las solicitudes de consentimiento del cliente para aplicaciones Experience Cloud mediante la API de Privacy Service.
translation-type: tm+mt
source-git-commit: 698639d6c2f7897f0eb4cce2a1f265a0f7bb57c9
workflow-type: tm+mt
source-wordcount: '244'
ht-degree: 1%

---


# Extremo de consentimiento

Algunas regulaciones requieren el consentimiento explícito del cliente antes de que se puedan recopilar sus datos personales. El extremo `/consent` de la API [!DNL Privacy Service] le permite procesar solicitudes de consentimiento del cliente e integrarlas en su flujo de trabajo de privacidad.

Antes de utilizar esta guía, consulte la sección [introducción](./getting-started.md) para obtener información sobre los encabezados de autenticación requeridos que se presentan en la llamada de API de ejemplo siguiente.

## Procesar una solicitud de consentimiento del cliente

Las solicitudes de consentimiento se procesan realizando una solicitud de POST al extremo `/consent`.

**Formato API**

```http
POST /consent
```

**Solicitud**

La siguiente solicitud crea un nuevo trabajo de consentimiento para los ID de usuario proporcionados en la matriz `entities`.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/privacy/consent \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `optOutOfSale` | Cuando se establece en true, indica que los usuarios que se proporcionan en `entities` desean excluirse de la venta o compartir sus datos personales. |
| `entities` | Matriz de objetos que indica a los usuarios a los que se aplica la solicitud de consentimiento. Cada objeto contiene un `namespace` y una matriz de `values` para hacer coincidir usuarios individuales con esa Área de nombres. |
| `nameSpace` | Cada objeto de la matriz `entities` debe contener una de las [Áreas de nombres de identidad estándar](./appendix.md#standard-namespaces) reconocidas por la API de Privacy Service. |
| `values` | Matriz de valores para cada usuario, correspondiente a la `nameSpace` proporcionada. |

>[!NOTE]
>
>Para obtener más información sobre cómo determinar a qué valores de identidad del cliente se enviarán [!DNL Privacy Service], consulte la guía sobre [cómo proporcionar datos de identidad](../identity-data.md).

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 202 (Aceptado) sin carga útil, lo que indica que la solicitud fue aceptada por [!DNL Privacy Service] y se está procesando.