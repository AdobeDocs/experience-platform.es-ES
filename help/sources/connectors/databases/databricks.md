---
title: Azure Databricks
description: Obtenga información acerca de los pasos previos necesarios para conectar Azure Databricks a Experience Platform.
badgeUltimate: label="Ultimate" type="Positive"
badgeBeta: label="Beta" type="Informative"
last-substantial-update: 2025-04-29T00:00:00Z
exl-id: 2f082898-aa0e-47a1-a4bf-077c21afdfee
source-git-commit: 5637a12d5f9cc14b6cf3d88f018aa92de06ab739
workflow-type: tm+mt
source-wordcount: '593'
ht-degree: 3%

---

# [!DNL Azure Databricks]

>[!IMPORTANT]
>
>El origen [!DNL Azure Databricks] está disponible en el catálogo de orígenes para los usuarios que han adquirido Real-Time CDP Ultimate.

[!DNL Azure Databricks] es una plataforma basada en la nube diseñada para el análisis de datos, el aprendizaje automático y la IA. Puede usar [!DNL Databricks] para integrarse con [!DNL Azure] y proporcionar un entorno holístico para crear, implementar y administrar soluciones de datos a escala.

Puede usar el origen [!DNL Databricks] para conectar su cuenta e ingerir los datos de [!DNL Databricks] en Adobe Experience Platform.

## Requisitos previos

Complete los pasos previos para conectar correctamente su cuenta de [!DNL Databricks] a Experience Platform.

### Recuperar las credenciales del contenedor

Recupere sus credenciales de Experience Platform [!DNL Azure Blob Storage] para permitir que su cuenta de [!DNL Databricks] acceda a ella más tarde.

Para recuperar sus credenciales, realice una petición GET al extremo `/credentials` de la API [!DNL Connectors].

**Formato de API**

```http
GET /data/foundation/connectors/landingzone/credentials?type=dlz_databricks_source
```

**Solicitud**

La siguiente solicitud recupera las credenciales de su Experience Platform [!DNL Azure Blob Storage].

+++Ver ejemplo de solicitud

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/connectors/landingzone/credentials?type=dlz_databricks_source' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

+++

**Respuesta**

Una respuesta correcta proporciona sus credenciales (`containerName`, `SASToken`, `storageAccountName`) para su uso posterior en la configuración de [!DNL Apache Spark] para [!DNL Databricks].

+++Ver ejemplo de respuesta

```json
{
    "containerName": "dlz-databricks-container",
    "SASToken": "sv=2020-10-02&si=dlz-b1f4060b-6bbd-4043-9bd9-a5f5be72de30&sr=c&sp=racwdlm&sig=zVQfmuElZJzOKkUk8z5lChrJ3YQUE2h6EShDZOsVeMc%3D",
    "storageAccountName": "sndbxdtlndga8m7ajbvgc64k",
    "SASUri": "https://sndbxdtlndga8m7ajbvgc64k.blob.core.windows.net/dlz-databricks-container?sv=2020-10-02&si=dlz-b1f4060b-6bbd-4043-9bd9-a5f5be72de30&sr=c&sp=racwdlm&sig=zVQfmuElZJzOKkUk8z5lChrJ3YQUE2h6EShDZOsVeMc%3D",
    "expiryDate": "2025-07-05"
}
```

| Propiedad | Descripción |
| --- | --- |
| `containerName` | Nombre de su contenedor [!DNL Azure Blob Storage]. Utilizará este valor más adelante al completar la configuración de [!DNL Apache Spark] para [!DNL Databricks]. |
| `SASToken` | El token de firma de acceso compartido para su [!DNL Azure Blob Storage]. Esta cadena contiene toda la información necesaria para autorizar una solicitud. |
| `storageAccountName` | El nombre de su cuenta de almacenamiento. |
| `SASUri` | URI de firma de acceso compartido para su [!DNL Azure Blob Storage]. Esta cadena es una combinación del URI del [!DNL Azure Blob Storage] para el que se está autenticando y su token SAS correspondiente. |
| `expiryDate` | La fecha en la que caducará su token SAS. Debe actualizar el token antes de la fecha de caducidad para poder seguir usándolo en la aplicación para cargar datos en [!DNL Azure Blob Storage]. Si no actualiza manualmente el token antes de la fecha de caducidad indicada, se actualizará automáticamente y proporcionará un nuevo token cuando se realice la llamada de credenciales de GET. |

+++

### Actualizar las credenciales

>[!NOTE]
>
>Las credenciales existentes se revocarán una vez que las actualice. Por lo tanto, debe actualizar las configuraciones de [!DNL Spark] en consecuencia cada vez que actualice sus credenciales de almacenamiento. De lo contrario, el flujo de datos fallará.

Para actualizar sus credenciales, realice una petición POST e incluya `action=refresh` como parámetro de consulta.

**Formato de API**

```http
GET /data/foundation/connectors/landingzone/credentials?type=dlz_databricks_source&action=refresh
```

**Solicitud**

La siguiente solicitud actualiza las credenciales de su [!DNL Azure Blob Storage].

+++Ver ejemplo de solicitud

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/connectors/landingzone/credentials?type=dlz_databricks_source&action=refresh' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

+++

**Respuesta**

Una respuesta correcta devuelve sus nuevas credenciales.

+++Ver ejemplo de respuesta

```json
{
    "containerName": "dlz-databricks-container",
    "SASToken": "sv=2020-10-02&si=dlz-6e17e5d6-de18-4efc-88c7-45f37d242617&sr=c&sp=racwdlm&sig=wvA4K3fcEmqAA%2FPvcMhB%2FA8y8RLwVJ7zhdWbxvT1uFM%3D",
    "storageAccountName": "sndbxdtlndga8m7ajbvgc64k",
    "SASUri": "https://sndbxdtlndga8m7ajbvgc64k.blob.core.windows.net/dlz-databricks-container?sv=2020-10-02&si=dlz-6e17e5d6-de18-4efc-88c7-45f37d242617&sr=c&sp=racwdlm&sig=wvA4K3fcEmqAA%2FPvcMhB%2FA8y8RLwVJ7zhdWbxvT1uFM%3D",
    "expiryDate": "2025-07-20"
}
```

+++

### Configure el acceso a su [!DNL Azure Blob Storage]

>[!IMPORTANT]
>
>* Si el clúster ha finalizado, el servicio lo reiniciará automáticamente durante una ejecución de flujo. Sin embargo, debe asegurarse de que el clúster esté activo al crear una conexión o un flujo de datos. Además, el clúster debe estar activo si realiza acciones como la previsualización o exploración de datos, ya que estas acciones no pueden provocar el reinicio automático de un clúster finalizado.
>
>* Su contenedor [!DNL Azure] incluye una carpeta llamada `adobe-managed-staging`. Para garantizar la ingesta perfecta de datos, **no** modifique esta carpeta.


A continuación, debe asegurarse de que el clúster [!DNL Databricks] tenga acceso a la cuenta de Experience Platform [!DNL Azure Blob Storage]. Al hacerlo, puede usar [!DNL Azure Blob Storage] como ubicación provisional para escribir [!DNL delta lake] datos de tabla.

Para proporcionar acceso, debe configurar un token SAS en el clúster [!DNL Databricks] como parte de la configuración [!DNL Apache Spark].

En la interfaz [!DNL Databricks], seleccione **[!DNL Advanced options]** y, a continuación, escriba lo siguiente en el cuadro de entrada [!DNL Spark config].

```shell
fs.azure.sas.{CONTAINER_NAME}.{STORAGE-ACCOUNT}.blob.core.windows.net {SAS-TOKEN}
```

| Propiedad | Descripción |
| --- | --- |
| Nombre del contenedor | El nombre del contenedor. Puede obtener este valor si recupera sus credenciales de [!DNL Azure Blob Storage]. |
| Cuenta de almacenamiento | El nombre de su cuenta de almacenamiento. Puede obtener este valor si recupera sus credenciales de [!DNL Azure Blob Storage]. |
| Token de SAS | El token de firma de acceso compartido para su [!DNL Azure Blob Storage]. Puede obtener este valor si recupera sus credenciales de [!DNL Azure Blob Storage]. |

![Interfaz de usuario de Databricks en Azure.](../../images/tutorials/create/databricks/databricks-ui.png)

## Conectar [!DNL Databricks] a Experience Platform mediante API

Ahora que ha completado los pasos previos, puede continuar con la guía sobre [conectar su cuenta de  [!DNL Databricks] a Experience Platform mediante la API](../../tutorials/api/create/databases/databricks.md).
