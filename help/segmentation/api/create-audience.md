---
title: Crear extremo de API de Audience
description: Obtenga información sobre cómo crear los metadatos para una audiencia externa mediante la API.
hide: true
hidefromtoc: true
source-git-commit: 74fa66e78ac36c8007eb89e8c271d989845c96f0
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 7%

---


# Crear extremo de audiencia

Se puede usar el extremo POST `/audiences` para crear los metadatos de una audiencia externa. Debe utilizar este punto final si la ingesta de audiencias se va a administrar en un servicio independiente, como la ingesta por lotes.

## Introducción

>[!IMPORTANT]
>
>Los extremos de esta guía llevan el prefijo `/core/ais`, a diferencia de `/core/ups`.

Para usar las API de Experience Platform, debe haber completado el [tutorial de autenticación](https://www.adobe.com/go/platform-api-authentication-en). Al completar el tutorial de autenticación, se proporcionan los valores para cada uno de los encabezados necesarios en las llamadas a la API de Experience Platform, como se muestra a continuación:

- Autorización: `Bearer {ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

Todos los recursos de [!DNL Experience Platform] están aislados en zonas protegidas virtuales específicas. Todas las solicitudes a las API de [!DNL Experience Platform] requieren un encabezado que especifica el nombre de la zona protegida en la que se realizará la operación:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Para obtener más información sobre cómo trabajar con zonas protegidas en [!DNL Experience Platform], consulte la [documentación general sobre las zonas protegidas](../../sandboxes/home.md).

**Formato de API**

>[!IMPORTANT]
>
>Usted **debe** incluir el parámetro de consulta `createAudienceMetaOnly=true` como parte de la solicitud.

```http
POST /audiences?createAudienceMetaOnly=true
```

**Solicitud**

>[!IMPORTANT]
>
>Usted **debe** incluir el encabezado `Accept: application/vnd.adobe.external.audiences+json; version=2` como parte de la solicitud de API.

```shell
curl -X POST https://platform.adobe.io/core/ais/audiences?createAudienceMetaOnly=true \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'\
 -H 'Accept: application/vnd.adobe.external.audiences+json; version=2'
 -d '{
    "name": "Sample audience name",
    "description" "A sample description for the audience.",
    "namespace": "agora",
    "originName": "Agora_Collaboration"
 }'
```

| Propiedad | Tipo | Descripción |
| -------- | ---- | ----------- |
| `name` | Cadena | Nombre de la audiencia. |
| `description` | Cadena | Una descripción opcional para la audiencia. |
| `namespace` | Cadena | El área de nombres de la audiencia. |
| `originName` | Cadena | Nombre del origen de la audiencia. |

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 con información sobre la audiencia recién creada.

```json
{
    "name": "Sample audience name",
    "audienceId": "4a815904-f2f9-4237-82fb-55605bcc2ad7"
}
```

| Propiedad | Tipo | Descripción |
| -------- | ---- | ----------- |
| `name` | Cadena | Nombre de la audiencia que ha creado. |
| `audienceId` | Cadena | El ID de la audiencia que ha creado. |
