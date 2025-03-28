---
title: Información general sobre el conector Source de Google BigQuery
description: Obtenga información sobre cómo conectar Google BigQuery a Adobe Experience Platform mediante API o la interfaz de usuario.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 35c61382-a909-47f4-a937-15cb725ecbe3
source-git-commit: 1900a8c6a3f3119c8b9049b12f5660cc9fd181a2
workflow-type: tm+mt
source-wordcount: '582'
ht-degree: 0%

---

# [!DNL Google BigQuery] origen

>[!IMPORTANT]
>
>El origen [!DNL Google BigQuery] está disponible en el catálogo de orígenes para los usuarios que han adquirido Real-Time Customer Data Platform Ultimate.

Lea este documento para conocer los pasos necesarios que debe seguir para conectar correctamente su cuenta de [!DNL Google BigQuery] a Adobe Experience Platform en Azure o Amazon Web Service (AWS).

## Requisitos previos {#prerequisites}

Lea las siguientes secciones para la configuración de requisitos previos que debe completar antes de poder conectar su cuenta de [!DNL Google BigQuery] a Experience Platform.

### LISTA DE PERMITIDOS de direcciones IP

Debe agregar direcciones IP específicas de la región a la lista de permitidos antes de conectar las fuentes a Experience Platform en Azure o Amazon Web Service (AWS). Para obtener más información, lea la guía de [inclusión en la lista de permitidos de direcciones IP para conectarse a Experience Platform en Azure y AWS](../../ip-address-allow-list.md).

### Autenticar en Experience Platform en Azure {#azure}

Debe proporcionar las siguientes credenciales para conectar su cuenta de [!DNL Google BigQuery] a Experience Platform en Azure.

>[!BEGINTABS]

>[!TAB Autenticación básica]

Para autenticarse con una combinación de OAuth 2.0 y autenticación básica, proporcione los valores adecuados para las siguientes credenciales.

| Credencial | Descripción |
| --- | --- |
| `project` | El proyecto es la entidad organizadora de nivel base para los recursos de [!DNL Google Cloud], entre ellos [!DNL Google BigQuery]. |
| `clientID` | El ID de cliente es la mitad de sus credenciales de [!DNL Google BigQuery] OAuth 2.0. |
| `clientSecret` | El secreto de cliente es la otra mitad de sus credenciales de OAuth 2.0 de [!DNL Google BigQuery]. |
| `refreshToken` | El token de actualización le permite obtener nuevos tokens de acceso para su API. Los tokens de acceso tienen una duración limitada y pueden caducar durante el transcurso del proyecto. Puede utilizar el token de actualización para autenticar y solicitar tokens de acceso posteriores para su proyecto cuando sea necesario. |
| `largeResultsDataSetId` | (Opcional) El ID del conjunto de datos [!DNL Google BigQuery] creado previamente que es necesario para habilitar la compatibilidad con grandes conjuntos de resultados. |

Para obtener instrucciones detalladas sobre cómo generar credenciales de OAuth 2.0 para API [!DNL Google], consulte la siguiente [[!DNL Google] guía de autenticación OAuth 2.0](https://developers.google.com/identity/protocols/oauth2).

>[!TAB Autenticación de servicio]

Para autenticarse mediante la autenticación del servicio, proporcione los valores adecuados para las siguientes credenciales.

**Nota**: su cuenta de servicio debe tener permisos suficientes, como: **[!DNL BigQuery Job User]**, **[!DNL BigQuery Data Viewer]**, **[!DNL BigQuery Read Session User]** y **[!DNL BigQuery Data Owner]** para autenticarse correctamente con la autenticación de servicio.

| Credencial | Descripción |
| --- | --- |
| `projectId` | El identificador de [!DNL Google BigQuery] con el que desea realizar la consulta. |
| `keyFileContent` | El archivo de clave que se utiliza para autenticar la cuenta de servicio. Puede recuperar este valor del [[!DNL Google Cloud service accounts] tablero](https://console.cloud.google.com). El contenido del archivo de claves está en formato JSON. Debe codificar esto en [!DNL Base64] al autenticarse en Experience Platform. |
| `largeResultsDataSetId` | (Opcional) El ID del conjunto de datos [!DNL Google BigQuery] creado previamente que es necesario para habilitar la compatibilidad con grandes conjuntos de resultados. |

Para obtener más información sobre cómo usar cuentas de servicio en [!DNL Google BigQuery], lea la guía sobre [usar cuentas de servicio en [!DNL Google BigQuery]](https://cloud.google.com/bigquery/docs/use-service-accounts).

>[!ENDTABS]

### Autenticar en Experience Platform en AWS {#aws}

Debe proporcionar las siguientes credenciales para conectar su cuenta de [!DNL Google BigQuery] a Experience Platform en AWS.

| Credencial | Descripción |
| --- | --- |
| `projectId` | El identificador de [!DNL Google BigQuery] con el que desea realizar la consulta. |
| `keyFileContent` | El archivo de clave que se utiliza para autenticar la cuenta de servicio. Puede recuperar este valor del [[!DNL Google Cloud service accounts] tablero](https://console.cloud.google.com). El contenido del archivo de claves está en formato JSON. Debe codificar esto en [!DNL Base64] al autenticarse en Experience Platform. |
| `datasetId` | Identificador del conjunto de datos [!DNL Google BigQuery]. Este ID representa dónde se encuentran las tablas de datos. |

## Conectar [!DNL Google BigQuery] a Experience Platform

La siguiente documentación proporciona información sobre cómo conectar [!DNL Google BigQuery] a Experience Platform mediante API o la interfaz de usuario:

### Uso de API

- [Creación de una conexión base de Google BigQuery mediante la API de Flow Service](../../tutorials/api/create/databases/bigquery.md)
- [Exploración de tablas de datos mediante la API de Flow Service](../../tutorials/api/explore/tabular.md)
- [Crear un flujo de datos para un origen de base de datos mediante la API de Flow Service](../../tutorials/api/collect/database-nosql.md)

### Uso de la IU

- [Creación de una conexión de origen de Google BigQuery en la IU](../../tutorials/ui/create/databases/bigquery.md)
- [Crear un flujo de datos para una conexión de origen de base de datos en la IU](../../tutorials/ui/dataflow/databases.md)
