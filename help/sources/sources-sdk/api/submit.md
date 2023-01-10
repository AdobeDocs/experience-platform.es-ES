---
keywords: Experience Platform;inicio;temas populares;orígenes;conectores;conectores de origen;sdk de fuentes;sdk;SDK
title: Enviar el origen
description: En el siguiente documento se proporcionan pasos sobre cómo probar y verificar un nuevo origen mediante la API de servicio de flujo e integrar un nuevo origen a través de fuentes de autoservicio (SDK por lotes).
exl-id: 9e945ba1-51b6-40a9-b92f-e0a52b3f92fa
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '826'
ht-degree: 0%

---

# Enviar el origen

El paso final para integrar el nuevo origen en Adobe Experience Platform mediante fuentes de autoservicio (SDK por lotes) es probar el origen para verificarlo. Una vez realizada la operación, puede enviar la nueva fuente poniéndose en contacto con el representante de Adobe.

En el siguiente documento se proporcionan los pasos para probar y depurar el origen mediante el [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Primeros pasos

* Para obtener información sobre cómo realizar llamadas correctamente a las API de Platform, consulte la guía de [introducción a las API de Platform](../../../landing/api-guide.md).
* Para obtener información sobre cómo generar sus credenciales para las API de plataforma, consulte el tutorial sobre [autenticación y acceso a las API de Experience Platform](../../../landing/api-authentication.md).
* Para obtener información sobre cómo configurar [!DNL Postman] para las API de plataforma, consulte el tutorial en [configuración de la consola de desarrollador y [!DNL Postman]](../../../landing/postman.md).
* Para ayudarle con el proceso de prueba y depuración, descargue el [Entorno y recopilación de verificación de fuentes de autoservicio aquí](../assets/sdk-verification.zip) y siga los pasos descritos a continuación.

## Probar el origen

Para probar el origen, debe ejecutar el [Entorno y recopilación de verificación de fuentes autoservidas](../assets/sdk-verification.zip) en [!DNL Postman] proporciona las variables de entorno apropiadas que pertenecen a su origen.

Para iniciar las pruebas, primero debe configurar la colección y el entorno en [!DNL Postman]. A continuación, especifique el ID de especificación de conexión que desea probar.

### Especifique `authSpecName`

Una vez que haya introducido su ID de especificación de conexión, debe especificar la variable `authSpecName` que está utilizando para la conexión base. Dependiendo de su elección, esto podría ser `OAuth 2 Refresh Code` o  `Basic Authentication`. Una vez especificado el `authSpecName`, debe incluir las credenciales necesarias en su entorno. Por ejemplo, si especifica `authSpecName` como `OAuth 2 Refresh Code`, debe proporcionar las credenciales necesarias para OAuth 2, que son `host` y `accessToken`.

### Especifique `sourceSpec`

Con los parámetros de especificación de autenticación añadidos, debe añadir las propiedades requeridas desde la especificación de origen. Puede encontrar las propiedades necesarias en `sourceSpec.spec.properties`. En el caso del [!DNL MailChimp Members] Por ejemplo, a continuación, la única propiedad requerida es `listId`, que significa `listId` y su valor de ID correspondiente a su [!DNL Postman] entorno.

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

Una vez proporcionados los parámetros de especificación de origen y autenticación, puede empezar a rellenar el resto de las variables de entorno; consulte la tabla siguiente para obtener una referencia:

>[!NOTE]
>
>Todas las variables de ejemplo siguientes son valores de marcador de posición que debe actualizar, excepto para `flowSpecificationId` y `targetConnectionSpecId`, que son valores fijos.

| Parámetro | Descripción | Ejemplo |
| --- | --- | --- |
| `x-api-key` | Identificador único utilizado para autenticar llamadas a las API de Experience Platform. Consulte el tutorial en [autenticación y acceso a las API de Experience Platform](../../../landing/api-authentication.md) para obtener información sobre cómo recuperar su `x-api-key`. | `c8d9a2f5c1e03789bd22e8efdd1bdc1b` |
| `x-gw-ims-org-id` | Una entidad corporativa que puede ser propietaria o titular de licencias de productos y servicios y permitir el acceso a sus miembros. Consulte el tutorial en [configuración de la consola de desarrollador y [!DNL Postman]](../../../landing/postman.md) para obtener instrucciones sobre cómo recuperar su `x-gw-ims-org-id` información. | `ABCEH0D9KX6A7WA7ATQE0TE@adobeOrg` |
| `authorizationToken` | Token de autorización necesario para completar llamadas a las API de Experience Platform. Consulte el tutorial en [autenticación y acceso a las API de Experience Platform](../../../landing/api-authentication.md) para obtener información sobre cómo recuperar su `authorizationToken`. | `Bearer authorizationToken` |
| `schemaId` | Para que los datos de origen se utilicen en Platform, se debe crear un esquema de destino para estructurar los datos de origen según sus necesidades. Para ver los pasos detallados sobre cómo crear un esquema XDM de destino, consulte el tutorial sobre [creación de un esquema con la API](../../../xdm/api/schemas.md). | `https://ns.adobe.com/{TENANT_ID}.schemas.0ef4ce0d390f0809fad490802f53d30b` |
| `schemaVersion` | La versión única que corresponde al esquema. | `application/vnd.adobe.xed-full-notext+json; version=1` |
| `schemaAltId` | La variable `meta:altId` que se devuelve junto con la variable  `schemaId` al crear un nuevo esquema. | `_{TENANT_ID}.schemas.0ef4ce0d390f0809fad490802f53d30b` |
| `dataSetId` | Para ver los pasos detallados sobre cómo crear un conjunto de datos de destinatario, consulte el tutorial en [creación de un conjunto de datos mediante la API](../../../catalog/api/create-dataset.md). | `5f3c3cedb2805c194ff0b69a` |
| `mappings` | Los conjuntos de asignaciones se pueden utilizar para definir cómo se asignan los datos de un esquema de origen al de un esquema de destino. Para ver los pasos detallados sobre cómo crear una asignación, consulte el tutorial sobre [creación de un conjunto de asignaciones mediante la API](../../../data-prep/api/mapping-set.md). | `[{"destinationXdmPath":"person.name.firstName","sourceAttribute":"email.email_id","identity":false,"version":0},{"destinationXdmPath":"person.name.lastName","sourceAttribute":"email.activity.action","identity":false,"version":0}]` |
| `mappingId` | ID exclusivo que corresponde al conjunto de asignaciones. | `bf5286a9c1ad4266baca76ba3adc9366` |
| `connectionSpecId` | El ID de especificación de conexión que corresponde a su origen. Este es el ID que generó después de [creación de una nueva especificación de conexión](./create.md). | `2e8580db-6489-4726-96de-e33f5f60295f` |
| `flowSpecificationId` | El ID de especificación de flujo de `RestStorageToAEP`. **Este es un valor fijo**. | `6499120c-0b15-42dc-936e-847ea3c24d72` |
| `targetConnectionSpecId` | El ID de conexión de destino del lago de datos en el que llegan los datos ingestados. **Este es un valor fijo**. | `c604ff05-7f1a-43c0-8e18-33bf874cb11c` |
| `verifyWatTimeInSecond` | El intervalo de tiempo designado que debe seguirse al comprobar la finalización de una ejecución de flujo. | `40` |
| `startTime` | La hora de inicio designada para el flujo de datos. La hora de inicio debe tener un formato de tiempo Unix. | `1597784298` |

Una vez que haya proporcionado todas las variables de entorno, puede empezar a ejecutar la colección utilizando la variable [!DNL Postman] interfaz. En el [!DNL Postman] , seleccione los puntos suspensivos (**...**) al lado [!DNL Sources SSSs Verification Collection] y, a continuación, seleccione **Ejecutar colección**.

![runner](../assets/runner.png)

La variable [!DNL Runner] , lo que le permite configurar el orden de ejecución del flujo de datos. Select **Ejecutar la colección de verificación de SSS** para ejecutar la colección.

>[!NOTE]
>
>Puede desactivar **Eliminar flujo** de la lista de comprobación del orden de ejecución si prefiere usar el panel de control de fuentes en la interfaz de usuario de Platform. Sin embargo, una vez finalizada la prueba, debe asegurarse de que los flujos de prueba se eliminen.

![run-collection](../assets/run-collection.png)

## Enviar el origen

Una vez que la fuente pueda completar todo el flujo de trabajo, puede ponerse en contacto con el representante de Adobe y enviar la fuente para integrarla.
