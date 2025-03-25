---
title: Aplique etiquetas de acceso para administrar el acceso de los usuarios a los flujos de datos de origen mediante la API
description: Aprenda a utilizar la API de Flow Service para aplicar etiquetas de acceso y administrar el acceso de los usuarios a los flujos de datos de origen.
hide: true
hidefromtoc: true
source-git-commit: 80fb60abdf33eb2a7ca691a9a48a811c632b34fc
workflow-type: tm+mt
source-wordcount: '567'
ht-degree: 4%

---

# Aplique etiquetas de acceso para administrar el acceso de los usuarios a los flujos de datos de origen mediante la API

Puede utilizar las funcionalidades proporcionadas por [control de acceso basado en atributos](../../../access-control/abac/overview.md) en Real-Time CDP para aplicar etiquetas a los flujos de datos de origen. Con esta función, puede asegurarse de que solo un subconjunto de usuarios de su organización obtenga acceso a fuentes y flujos de datos específicos.

Cuando se agrega una etiqueta de acceso a un flujo de datos concreto, solo los usuarios que tienen acceso a una función a la que se les asigna esa etiqueta pueden ver y editar ese flujo de datos. Si un flujo de datos de origen no está marcado con ninguna etiqueta, es visible para todos los usuarios que pertenecen a su organización. Por ejemplo, si aplica la etiqueta C12 a un flujo de datos, los usuarios asignados a una función que no tiene la etiqueta C12 no podrán ver y editar el flujo de datos con la etiqueta C12.

Lea esta guía para obtener información sobre cómo aplicar etiquetas de acceso a los flujos de datos de origen mediante la [[!DNL Flow Service] API](https://developer.adobe.com/experience-platform-apis/references/flow-service/).

## Introducción 

Antes de trabajar con etiquetas de control de acceso, asegúrese de familiarizarse primero con las capacidades del control de acceso basado en atributos. Para obtener más información, lea la siguiente documentación:

* [Información general de control de acceso basado en atributos](../../../access-control/abac/overview.md)
* [Guía completa de control de acceso basado en atributos](../../../access-control/abac/end-to-end-guide.md)
* [Guía de API de control de acceso basado en atributos](../../../access-control/abac/api/overview.md)
* [Glosario de etiquetas de uso de datos](../../../data-governance/labels/reference.md)

## Aplicar etiquetas de acceso a flujos de datos de origen

>[!NOTE]
>
>* No puede aplicar etiquetas a una ejecución de flujo. Sin embargo, las ejecuciones de flujo heredan cualquier etiqueta que aplique al flujo de datos principal.
>
>* Si no tiene acceso de visualización a un flujo de datos, tampoco podrá ver sus ejecuciones de flujo correspondientes.

Para agregar una etiqueta a un flujo de datos, realice una petición PATCH al extremo `/flows` y proporcione el ID del flujo de datos que desea actualizar.

**Formato de API**

```http
PATCH /flows/{FLOW_ID}
```

| Parámetro | Descripción |
| --- | --- |
| `{FLOW_ID}` | El ID del flujo de datos que desea actualizar. |

**Solicitud**

>[!TIP]
>
>Para realizar una solicitud de PATCH, proporcione la versión o la etiqueta del flujo de datos que desea actualizar como parámetro de encabezado `if-match`.

La siguiente solicitud agrega la etiqueta C12 al flujo de datos con ID: `84224def-1e2a-4d95-9ea2-132d697ed2aa`.

```shell
curl -X PATCH \
  'https://platform.adobe.io/data/foundation/flowservice/flows/84224def-1e2a-4d95-9ea2-132d697ed2aa' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json' \
  -H 'if-match: "c5002e0e-0000-0200-0000-67a3c3b70000"'
  -d '[
    {
        "op": "add",
        "path": "/labels",
        "value": ["core/C12"]
    }
]'
```

| Propiedad | Descripción |
| --- | --- |
| `op` | La llamada de operación utilizada para definir la acción necesaria para actualizar el flujo de datos. Las operaciones incluyen: `add`, `replace` y `remove`. |
| `path` | La parte del flujo de datos que se va a actualizar. |
| `value` | El nuevo valor con el que desea actualizar la propiedad. |



**Respuesta**

Una respuesta correcta devuelve su ID de flujo y una etiqueta actualizada. Puede comprobar la actualización realizando una petición GET a la API [!DNL Flow Service], al tiempo que proporciona su ID de flujo.

```json
{
    "id": "84224def-1e2a-4d95-9ea2-132d697ed2aa",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

Una vez que haya configurado correctamente las etiquetas de acceso al flujo de datos, cualquier usuario que no tenga acceso a esa etiqueta ya no podrá recuperar el flujo de datos. Por ejemplo, si un usuario que no está aprovisionado con la etiqueta C12 realiza una petición GET para recuperar el flujo de datos con el ID: `84224def-1e2a-4d95-9ea2-132d697ed2aa`, recibirá la siguiente respuesta:

```json
{
    "type": "https://ns.adobe.com/aep/errors/FLOW-1439-404",
    "title": "Resource not found",
    "status": 404,
    "report": {
        "detailed-message": "The requested flows resource 84224def-1e2a-4d95-9ea2-132d697ed2aa is not found. Verify the resource ID before trying again.",
        "id": "84224def-1e2a-4d95-9ea2-132d697ed2aa",
        "request-id": "{REQUEST_ID}",
        "type": "flows"
    },
    "errorMessage": "The requested flows resource 84224def-1e2a-4d95-9ea2-132d697ed2aa is not found. Verify the resource ID before trying again.",
    "errorDetails": "The requested flows resource 84224def-1e2a-4d95-9ea2-132d697ed2aa is not found. Verify the resource ID before trying again."
}
```

Del mismo modo, los usuarios sin acceso a la etiqueta C12 no podrán realizar ninguna solicitud de PATCH o DELETE contra el flujo de datos actualizado y recibirán la siguiente respuesta:

```json
{
    "type": "https://ns.adobe.com/aep/errors/FLOW-2120-403",
    "title": "Forbidden",
    "status": 403,
    "report": {
        "detailed-message": "You do not have sufficient permissions to perform the operation. Please contact your administrator to resolve permissions and try again.",
        "request-id": "{REQUEST_ID}"
    },
    "errorMessage": "You do not have sufficient permissions to perform the operation. Please contact your administrator to resolve permissions and try again.",
    "errorDetails": "You do not have sufficient permissions to perform the operation. Please contact your administrator to resolve permissions and try again."
}
```

## Pasos siguientes

Ahora sabe cómo aplicar etiquetas de acceso a los flujos de datos de origen. Ahora puede asegurarse de que solo un grupo específico de usuarios de su organización pueda acceder a determinadas fuentes y flujos de datos. Lea la siguiente documentación para obtener más información:

* [Aplicar etiquetas de acceso a los flujos de datos de origen en la IU](../ui/labels.md)
* [Información general sobre el control de acceso](../../../access-control/home.md)