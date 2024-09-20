---
title: Información general sobre el conector Source de Google BigQuery
description: Obtenga información sobre cómo conectar Google BigQuery a Adobe Experience Platform mediante API o la interfaz de usuario.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 35c61382-a909-47f4-a937-15cb725ecbe3
source-git-commit: 1fa79b31b5a257ebb3cbd60246b757d8a4a63d7c
workflow-type: tm+mt
source-wordcount: '529'
ht-degree: 0%

---

# [!DNL Google BigQuery] origen

>[!IMPORTANT]
>
>El origen [!DNL Google BigQuery] está disponible en el catálogo de orígenes para los usuarios que han adquirido Real-time Customer Data Platform Ultimate.

Adobe Experience Platform permite la ingesta de datos desde fuentes externas, al tiempo que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de Platform. Puede introducir datos de una variedad de fuentes, como aplicaciones de Adobe, almacenamiento basado en la nube, bases de datos y muchas otras.

Lea este documento para conocer los pasos necesarios que debe llevar a cabo para conectar correctamente su cuenta de [!DNL Google BigQuery] al Experience Platform.

## Requisitos previos {#prerequisites}

La siguiente sección proporciona más información sobre la configuración de requisitos previos necesaria para poder crear una conexión de origen de [!DNL Google BigQuery].

### LISTA DE PERMITIDOS de direcciones IP

Se debe agregar una lista de direcciones IP a una lista de permitidos antes de trabajar con conectores de origen. Si no se agregan las direcciones IP específicas de la región a la lista de permitidos, pueden producirse errores o no rendimiento al utilizar fuentes. Consulte la página [lista de permitidos de direcciones IP](../../ip-address-allow-list.md) para obtener más información.

### Generar sus credenciales de [!DNL Google BigQuery] {#credentials}

Para conectar [!DNL Google BigQuery] al Experience Platform, debe generar los valores de las siguientes credenciales:

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
| `keyFileContent` | El archivo de clave que se utiliza para autenticar la cuenta de servicio. Puede recuperar este valor del [[!DNL Google Cloud service accounts] tablero](https://console.cloud.google.com). El contenido del archivo de claves está en formato JSON. Debe codificar esto en [!DNL Base64] al autenticarse en el Experience Platform. |
| `largeResultsDataSetId` | (Opcional) El ID del conjunto de datos [!DNL Google BigQuery] creado previamente que es necesario para habilitar la compatibilidad con grandes conjuntos de resultados. |

Para obtener más información sobre cómo usar cuentas de servicio en [!DNL Google BigQuery], lea la guía sobre [usar cuentas de servicio en [!DNL Google BigQuery]](https://cloud.google.com/bigquery/docs/use-service-accounts).

>[!ENDTABS]

## Conectar [!DNL Google BigQuery] a Platform

La siguiente documentación proporciona información sobre cómo conectar [!DNL Google BigQuery] a Platform mediante API o la interfaz de usuario:

### Uso de API

- [Creación de una conexión base de Google BigQuery mediante la API de Flow Service](../../tutorials/api/create/databases/bigquery.md)
- [Exploración de tablas de datos mediante la API de Flow Service](../../tutorials/api/explore/tabular.md)
- [Crear un flujo de datos para un origen de base de datos mediante la API de Flow Service](../../tutorials/api/collect/database-nosql.md)

### Uso de la IU

- [Creación de una conexión de origen de Google BigQuery en la IU](../../tutorials/ui/create/databases/bigquery.md)
- [Crear un flujo de datos para una conexión de origen de base de datos en la IU](../../tutorials/ui/dataflow/databases.md)
