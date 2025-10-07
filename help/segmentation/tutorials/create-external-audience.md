---
title: Creación y activación de una audiencia externa
type: Tutorial
description: Obtenga información sobre cómo crear una audiencia externa en Adobe Experience Platform mediante las API de Experience Platform.
source-git-commit: 0a37ef2f5fc08eb515c7c5056936fd904ea6d360
workflow-type: tm+mt
source-wordcount: '892'
ht-degree: 3%

---


# Creación y activación de una audiencia externa mediante la API

Este tutorial muestra los pasos necesarios para crear una audiencia externa mediante las API de Adobe Experience Platform.

## Introducción

Este tutorial requiere una comprensión práctica de los distintos servicios de Experience Platform implicados en la creación de una audiencia externa. Antes de comenzar este tutorial, lea la documentación de los siguientes servicios:

- [Fuentes](../../sources/home.md): Experience Platform permite la ingesta de datos de varias fuentes al tiempo que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de Experience Platform.
- [[!DNL Adobe Experience Platform Segmentation Service]](../home.md): permite crear audiencias a partir de los datos externos.
- [Destinos](../../destinations/home.md): los destinos son integraciones prediseñadas con aplicaciones de uso común que permiten la activación perfecta de datos de Experience Platform para campañas de marketing entre canales, campañas por correo electrónico, publicidad segmentada y mucho más.

### Encabezados obligatorios

Este tutorial también requiere que haya completado el [tutorial de autenticación](https://www.adobe.com/go/platform-api-authentication-en) para realizar correctamente llamadas a las API de [!DNL Experience Platform]. Al completar el tutorial de autenticación, se proporcionan los valores para cada uno de los encabezados obligatorios en todas las llamadas de API de [!DNL Experience Platform], como se muestra a continuación:

- Autorización: Portador `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

Todos los recursos de [!DNL Experience Platform] están aislados en zonas protegidas virtuales específicas. Las solicitudes a las API [!DNL Experience Platform] requieren un encabezado que especifique el nombre de la zona protegida en la que se realizará la operación:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Para obtener más información sobre las zonas protegidas en [!DNL Experience Platform], consulte la [documentación de información general sobre las zonas protegidas](../../sandboxes/home.md).

Todas las solicitudes de POST, PUT y PATCH requieren un encabezado adicional:

- Content-Type: application/json

## Preparación de la audiencia externa {#prepare}

Para poder crear una audiencia externa dentro de Experience Platform, debe preparar un archivo que contenga los datos de audiencia.

Para este ejemplo, debe utilizar un archivo CSV. Asegúrese de que el archivo CSV contenga **al menos** una columna con un valor de identidad como un ECID, un ID de correo electrónico o un ID de CRM. Además, asegúrese de que contiene todos los atributos de enriquecimiento que necesitará para la segmentación y activación.

También debe asegurarse de que el archivo se ajuste a los requisitos del esquema de Experience Platform. Para obtener más información sobre cómo crear un esquema, lea el [tutorial sobre cómo crear un esquema con la API](/help/xdm/tutorials/create-schema-api.md) o el [tutorial sobre cómo crear un esquema con la interfaz de usuario](/help/xdm/tutorials/create-schema-ui.md).

Una vez que haya confirmado que el archivo CSV contiene toda la información necesaria y se ajusta al esquema, deberá cargar el archivo CSV a su proveedor de almacenamiento en la nube para poder utilizar fuentes e introducir los datos en Experience Platform. Para obtener más información sobre cómo usar una fuente de almacenamiento en la nube, lea el [tutorial sobre cómo explorar las opciones de almacenamiento en la nube mediante la API](/help/sources/tutorials/api/explore/cloud-storage.md) o la [descripción general de las fuentes](/help/sources/home.md#cloud-storage).

## Creación de una audiencia externa {#create}

Después de preparar el archivo CSV, ahora puede iniciar el proceso de creación de la audiencia externa.

Puede crear una audiencia externa realizando una petición POST al extremo `/external-audience/`.

Al realizar esta solicitud, debe especificar la siguiente información:

- Nombre de la audiencia
- Una descripción para la audiencia
- Los campos correspondientes entre el CSV y el esquema
- La información de especificación de origen
   - Esto incluye la ruta del archivo CSV para la ingesta
      - La ruta de acceso de archivo **no puede** contener espacios. Por ejemplo, si la ruta es `activation/sample-source/Example CSV File.csv`, establezca la ruta en `activation/sample-source/ExampleCSVFile.csv`.

Para obtener información más detallada sobre cómo usar este extremo, lea la [guía de extremo de audiencias externas](/help/segmentation/api/external-audiences.md#create-audience).

+++Solicitud

```shell
curl -X POST https://platform.adobe.io/data/core/ais/external-audience/ \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
        "name": "Sample external audience",
        "description": "A sample version of an external audience",
        "fields": [
            {
                "name": "ppid",
                "type": "string",
                "identityNs": "email"
            },
            {
                "name": "list_id",
                "type": "string",
                "labels": ["core/C2", "custom/deep"]
            },
            {
                "name": "delete",
                "type": "number"
            },
            {
                "name": "process_consent",
                "type": "string"
            }
        ],
        "sourceSpec": {
            "params": {
                "path": "activation/sample-source/example.csv",
                "type": "file",
                "sourceType": "Cloud Storage",
                "baseConnectionId": "1d1d4bc5-b527-46a3-9863-530246a61b2b"
            }
        },
        "ttlInDays": "40",
        "labels": ["core/C1"],
        "audienceType": "people",
        "originName": "CUSTOM_UPLOAD"
    }'
```

+++

Después de realizar esta solicitud, asegúrese de tomar nota de `operationId` que recibe de la respuesta para poder recuperar el ID de audiencia.

## Recuperar ID de audiencia {#retrieve-audience-id}

Ahora que ha creado la audiencia externa, debe obtener el ID de audiencia para poder introducir la audiencia en Experience Platform.

Puede recuperar el ID de audiencia realizando una petición GET al extremo `/external-audiences/operations` y proporcionando el ID de la operación que recibió anteriormente de la respuesta Crear audiencia externa.

Para obtener información más detallada sobre cómo usar este extremo, lea la [guía de extremo de audiencia externa](/help/segmentation/api/external-audiences.md#retrieve-status).

+++ Solicitud

```shell
curl -X GET https://platform.adobe.io/data/core/ais/external-audience/operations/{OPERATION_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

Después de realizar esta solicitud, asegúrese de anotar `audienceId` que recibe de la respuesta para poder almacenar en déclencheur el trabajo de ingesta para la audiencia.

## Iniciar ingesta de audiencia {#start-ingestion}

Dado que tiene su `audienceId`, ahora puede almacenar en déclencheur la ingesta de la audiencia externa en Experience Platform.

Puede iniciar una ingesta de audiencia realizando una petición POST al siguiente punto de conexión, proporcionando al mismo tiempo el ID de audiencia. Además, tendrá que especificar la hora de inicio para determinar qué archivos se procesarán.

Para obtener información más detallada sobre cómo usar este extremo, lea la [guía de extremo de audiencias externas](/help/segmentation/api/external-audiences.md#start-audience-ingestion)

+++ Solicitud

```shell
curl -X POST https://platform.adobe.io/data/core/ais/external-audience/{AUDIENCE_ID}/runs \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
    "dataFilterStartTime": 764245635
 }' 
```

+++

Después de realizar esta solicitud, asegúrese de anotar `runId` que recibe de la respuesta para poder supervisar el estado de la ingesta.

## Monitorizar estado de ingesta {#monitor-ingestion}

Después de activar la ingesta de audiencia, ahora puede monitorizar el progreso de la ingesta para confirmar que sea correcta y validar la disponibilidad de la audiencia para la activación descendente.

Puede recuperar el estado de una ingesta de audiencia realizando una petición GET al siguiente extremo, proporcionando al mismo tiempo la audiencia y los ID de ejecución.

Para obtener información más detallada sobre cómo usar este extremo, lea la [guía de extremo de audiencia externa](/help/segmentation/api/external-audiences.md#retrieve-ingestion-status).

+++ Solicitud

```shell
curl -X GET https://platform.adobe.io/data/core/ais/external-audience/{AUDIENCE_ID}/runs/{RUN_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

## Próximos pasos {#next-steps}

>[!IMPORTANT]
>
>Para usar la audiencia generada externamente, **debe** esperar hasta que se complete el trabajo de segmentación diaria.

Una vez que haya confirmado que la audiencia externa se ha introducido correctamente, puede verla en Audience Portal y utilizarla en servicios descendentes como destinos.

Para obtener más información acerca de Audience Portal, lea la [Guía de la interfaz de usuario de Audience Portal](/help/segmentation/ui/audience-portal.md). Para obtener más información sobre los destinos, lea la [descripción general de los destinos](/help/destinations/home.md).

