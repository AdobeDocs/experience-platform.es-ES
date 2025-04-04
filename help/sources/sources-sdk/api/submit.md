---
keywords: Experience Platform;inicio;temas populares;fuentes;conectores;conectores de origen;fuentes sdk;sdk;SDK
title: Envíe su Source
description: El siguiente documento proporciona pasos sobre cómo probar y comprobar una nueva fuente mediante la API de Flow Service e integrar una nueva fuente mediante fuentes de autoservicio (SDK por lotes).
exl-id: 9e945ba1-51b6-40a9-b92f-e0a52b3f92fa
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '829'
ht-degree: 0%

---

# Enviar el origen

El paso final para integrar su nueva fuente en Adobe Experience Platform mediante fuentes de autoservicio (SDK por lotes) es probar la fuente para la verificación. Una vez realizado el proceso correctamente, puede enviar su nuevo origen poniéndose en contacto con su representante de Adobe.

El siguiente documento proporciona pasos sobre cómo probar y depurar el origen mediante la [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Introducción

* Para obtener información sobre cómo realizar llamadas correctamente a las API de Experience Platform, consulte la guía sobre [introducción a las API de Experience Platform](../../../landing/api-guide.md).
* Para obtener información sobre cómo generar tus credenciales para las API de Experience Platform, consulta el tutorial sobre [autenticación y acceso a las API de Experience Platform](../../../landing/api-authentication.md).
* Para obtener información sobre cómo configurar [!DNL Postman] para las API de Experience Platform, consulte el tutorial sobre [configuración de la consola para desarrolladores y [!DNL Postman]](../../../landing/postman.md).
* Para facilitar el proceso de prueba y depuración, descargue la colección de verificación de [fuentes de autoservicio y el entorno aquí](../assets/sdk-verification.zip) y siga los pasos descritos a continuación.

## Prueba del origen

Para probar el origen, debe ejecutar la [colección de verificación de fuentes de autoservicio y el entorno](../assets/sdk-verification.zip) en [!DNL Postman], al tiempo que proporciona las variables de entorno apropiadas que pertenecen al origen.

Para iniciar la prueba, primero debe configurar la colección y el entorno en [!DNL Postman]. A continuación, especifique el Id. de especificación de conexión que desea probar.

### Especificar `authSpecName`

Una vez que haya especificado el identificador de especificación de conexión, debe especificar el `authSpecName` que está usando para la conexión base. Según su elección, podría ser `OAuth 2 Refresh Code` o `Basic Authentication`. Una vez que especifique su `authSpecName`, debe incluir sus credenciales requeridas en el entorno. Por ejemplo, si especifica `authSpecName` como `OAuth 2 Refresh Code`, debe proporcionar las credenciales necesarias para OAuth 2, que son `host` y `accessToken`.

### Especificar `sourceSpec`

Con los parámetros de especificación de autenticación añadidos, a continuación debe añadir las propiedades necesarias desde la especificación de origen. Puede encontrar las propiedades requeridas en `sourceSpec.spec.properties`. En el caso del ejemplo [!DNL MailChimp Members] que se muestra a continuación, la única propiedad necesaria es `listId`, lo que significa `listId` y su valor de ID correspondiente a su entorno [!DNL Postman].

```json
"spec": {
  "$schema": "http://json-schema.org/draft-07/schema#",
  "type": "object",
  "description": "Define user input parameters to fetch resource values.",
  "properties": {
    "listId": {
      "type": "string",
      "description": "listId for which members need to fetch."
    }
  }
}
```

Una vez proporcionados los parámetros de autenticación y especificación de fuente, puede empezar a rellenar el resto de las variables de entorno; consulte la tabla siguiente para obtener una referencia:

>[!NOTE]
>
>Todas las variables de ejemplo siguientes son valores de marcador de posición que debe actualizar, excepto `flowSpecificationId` y `targetConnectionSpecId`, que son valores fijos.

| Parámetro | Descripción | Ejemplo |
| --- | --- | --- |
| `x-api-key` | Identificador único utilizado para autenticar llamadas a las API de Experience Platform. Consulte el tutorial sobre [autenticación y acceso a las API de Experience Platform](../../../landing/api-authentication.md) para obtener información sobre cómo recuperar su `x-api-key`. | `c8d9a2f5c1e03789bd22e8efdd1bdc1b` |
| `x-gw-ims-org-id` | Una entidad corporativa que puede poseer o licenciar productos y servicios y permitir el acceso a sus miembros. Consulte el tutorial sobre [configuración de la consola para desarrolladores y [!DNL Postman]](../../../landing/postman.md) para obtener instrucciones sobre cómo recuperar la información de `x-gw-ims-org-id`. | `ABCEH0D9KX6A7WA7ATQE0TE@adobeOrg` |
| `authorizationToken` | El token de autorización necesario para completar las llamadas a las API de Experience Platform. Consulte el tutorial sobre [autenticación y acceso a las API de Experience Platform](../../../landing/api-authentication.md) para obtener información sobre cómo recuperar su `authorizationToken`. | `Bearer authorizationToken` |
| `schemaId` | Para que los datos de origen se utilicen en Experience Platform, se debe crear un esquema de destino para estructurar los datos de origen según sus necesidades. Para ver los pasos detallados sobre cómo crear un esquema XDM de destino, consulte el tutorial de [creación de un esquema mediante la API](../../../xdm/api/schemas.md). | `https://ns.adobe.com/{TENANT_ID}.schemas.0ef4ce0d390f0809fad490802f53d30b` |
| `schemaVersion` | La versión única que se corresponde con el esquema. | `application/vnd.adobe.xed-full-notext+json; version=1` |
| `schemaAltId` | `meta:altId` que se devuelve junto con `schemaId` al crear un nuevo esquema. | `_{TENANT_ID}.schemas.0ef4ce0d390f0809fad490802f53d30b` |
| `dataSetId` | Para ver los pasos detallados sobre cómo crear un conjunto de datos de destino, consulte el tutorial de [creación de un conjunto de datos mediante la API](../../../catalog/api/create-dataset.md). | `5f3c3cedb2805c194ff0b69a` |
| `mappings` | Los conjuntos de asignaciones se pueden utilizar para definir cómo se asignan los datos de un esquema de origen al de un esquema de destino. Para ver los pasos detallados sobre cómo crear una asignación, consulte el tutorial sobre [creación de un conjunto de asignaciones mediante la API](../../../data-prep/api/mapping-set.md). | `[{"destinationXdmPath":"person.name.firstName","sourceAttribute":"email.email_id","identity":false,"version":0},{"destinationXdmPath":"person.name.lastName","sourceAttribute":"email.activity.action","identity":false,"version":0}]` |
| `mappingId` | ID único que corresponde al conjunto de asignaciones. | `bf5286a9c1ad4266baca76ba3adc9366` |
| `connectionSpecId` | El ID de especificación de conexión que corresponde con su origen. Este es el identificador que generó después de [crear una nueva especificación de conexión](./create.md). | `2e8580db-6489-4726-96de-e33f5f60295f` |
| `flowSpecificationId` | Identificador de especificación de flujo de `RestStorageToAEP`. **Este es un valor fijo**. | `6499120c-0b15-42dc-936e-847ea3c24d72` |
| `targetConnectionSpecId` | El ID de conexión de destino del lago de datos donde aterrizan los datos ingeridos. **Este es un valor fijo**. | `c604ff05-7f1a-43c0-8e18-33bf874cb11c` |
| `verifyWatTimeInSecond` | Intervalo de tiempo designado que se debe seguir al comprobar la finalización de una ejecución de flujo. | `40` |
| `startTime` | La hora de inicio designada para el flujo de datos. La hora de inicio debe tener el formato unix time. | `1597784298` |

Una vez que haya proporcionado todas las variables de entorno, puede comenzar a ejecutar la colección usando la interfaz [!DNL Postman]. En la interfaz [!DNL Postman], seleccione los puntos suspensivos (**...**) junto a [!DNL Sources SSSs Verification Collection] y, a continuación, seleccione **Ejecutar colección**.

![ejecutor](../assets/runner.png)

Aparecerá la interfaz [!DNL Runner], lo que le permitirá configurar el orden de ejecución del flujo de datos. Seleccione **Ejecutar colección de verificación de SMS** para ejecutar la colección.

>[!NOTE]
>
>Puede deshabilitar **Eliminar flujo** de la lista de comprobación del orden de ejecución si prefiere usar el panel de supervisión de orígenes en la interfaz de usuario de Experience Platform. Sin embargo, una vez que haya terminado con la prueba, debe asegurarse de que los flujos de prueba se eliminen.

![run-collection](../assets/run-collection.png)

## Enviar el origen

Una vez que el origen haya podido completar todo el flujo de trabajo, puede ponerse en contacto con el representante de Adobe y enviar el origen para que se integre.
