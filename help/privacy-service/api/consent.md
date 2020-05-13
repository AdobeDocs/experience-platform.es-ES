---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Consentimiento
topic: developer guide
translation-type: tm+mt
source-git-commit: a3178ab54a7ab5eacd6c5f605b8bd894779f9e85
workflow-type: tm+mt
source-wordcount: '226'
ht-degree: 1%

---


# Consentimiento

Ciertas regulaciones requieren el consentimiento explícito del cliente antes de que se puedan recopilar sus datos personales. El punto final de la API de Privacy Service le permite procesar las solicitudes de consentimiento del cliente e integrarlas en su flujo de trabajo de privacidad. `/consent`

Antes de utilizar esta guía, consulte la sección [Introducción](./getting-started.md) para obtener información sobre los encabezados de autenticación requeridos que se presentan en la llamada de API de ejemplo siguiente.

## Procesar una solicitud de consentimiento del cliente

Las solicitudes de consentimiento se procesan realizando una solicitud POST al `/consent` extremo.

**Formato API**

```http
POST /consent
```

**Solicitud**

La siguiente solicitud crea un nuevo trabajo de consentimiento para los ID de usuario proporcionados en la `entities` matriz.

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
| `optOutOfSale` | Cuando se establece en true, indica que los usuarios incluidos en `entities` desean excluirse de la venta o el uso compartido de sus datos personales. |
| `entities` | Matriz de objetos que indica a los usuarios a los que se aplica la solicitud de consentimiento. Cada objeto contiene una `namespace` y una matriz de `values` para que los usuarios individuales coincidan con esa Área de nombres. |
| `nameSpace` | Cada objeto de la `entities` matriz debe contener una de las Áreas de nombres [de identidad](./appendix.md#standard-namespaces) estándar reconocidas por la API de Privacy Service. |
| `values` | Matriz de valores para cada usuario, correspondiente con el valor proporcionado `nameSpace`. |

>[!NOTE] Para obtener más información sobre cómo determinar qué valores de identidad del cliente se enviarán a Privacy Service, consulte la guía sobre el [suministro de datos](../identity-data.md)de identidad.

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 202 (Aceptado) sin carga útil, lo que indica que Privacy Service ha aceptado la solicitud y que se está procesando.