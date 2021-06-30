---
keywords: Experience Platform;inicio;temas populares;BigQuery;bigquery;Google BigQuery;google bigquery
solution: Experience Platform
title: Información general sobre el conector de origen BigQuery de Google
topic-legacy: overview
description: Obtenga información sobre cómo conectar Google BigQuery a Adobe Experience Platform mediante API o la interfaz de usuario.
exl-id: 35c61382-a909-47f4-a937-15cb725ecbe3
source-git-commit: 5821f9304a37c1a03d17f0113d09548799662a2e
workflow-type: tm+mt
source-wordcount: '395'
ht-degree: 0%

---

# Conector (Beta) [!DNL Google BigQuery]

>[!NOTE]
>
>El [!DNL Google BigQuery] está en versión beta. Consulte la [información general sobre fuentes](../../home.md#terms-and-conditions) para obtener más información sobre el uso de conectores con etiqueta beta.

Adobe Experience Platform permite la ingesta de datos de fuentes externas, al tiempo que permite estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de Platform. Puede ingerir datos de una variedad de fuentes, como aplicaciones de Adobe, almacenamiento basado en la nube, bases de datos y muchas otras.

[!DNL Experience Platform] permite la ingesta de datos desde una base de datos de terceros. Platform puede conectarse a diferentes tipos de bases de datos, como relacional, sinSQL o data warehouse. La compatibilidad con los proveedores de bases de datos incluye [!DNL Google BigQuery].

## LISTA DE PERMITIDOS de direcciones IP

Se debe agregar una lista de direcciones IP a una lista de permitidos antes de trabajar con conectores de origen. Si no agrega las direcciones IP específicas de su región a su lista de permitidos, puede que se produzcan errores o que no se produzca un rendimiento al utilizar fuentes. Consulte la página [lista de permitidos de direcciones IP](../../ip-address-allow-list.md) para obtener más información.

## Requisitos previos

La siguiente sección proporciona más información sobre la configuración previa necesaria para poder crear una conexión de origen [!DNL Google BigQuery].

### Generar sus [!DNL Google BigQuery] credenciales

Para conectar [!DNL Google BigQuery] a Platform, debe generar valores para las siguientes credenciales:

| Credencial | Descripción |
| ---------- | ----------- |
| `project` | El proyecto es la entidad organizadora de nivel base para sus [!DNL Google Cloud] recursos, incluido [!DNL Google BigQuery]. |
| `clientID` | El ID de cliente es la mitad de sus credenciales de [!DNL Google BigQuery] OAuth 2.0. |
| `clientSecret` | El secreto del cliente es la otra mitad de sus credenciales [!DNL Google BigQuery] de OAuth 2.0. |
| `refreshToken` | El token de actualización le permite obtener nuevos tokens de acceso para su API. Los tokens de acceso tienen una duración limitada y pueden caducar durante el curso del proyecto. Puede utilizar el token de actualización para autenticarse y solicitar los tokens de acceso subsiguientes para su proyecto cuando sea necesario. |

Para obtener instrucciones detalladas sobre cómo generar credenciales de OAuth 2.0 para API [!DNL Google], consulte la siguiente [[!DNL Google] Guía de autenticación de OAuth 2.0](https://developers.google.com/identity/protocols/oauth2).

## Conectar [!DNL Google BigQuery] a Platform

La documentación siguiente proporciona información sobre cómo conectar [!DNL Google BigQuery] a Platform mediante API o la interfaz de usuario:

### Uso de API

- [Creación de una conexión base de Google BigQuery mediante la API de servicio de flujo](../../tutorials/api/create/databases/bigquery.md)
- [Explorar la estructura de datos y el contenido de un origen de base de datos mediante la API de servicio de flujo](../../tutorials/api/explore/database-nosql.md)
- [Creación de un flujo de datos para un origen de base de datos mediante la API de servicio de flujo](../../tutorials/api/collect/database-nosql.md)

### Uso de la interfaz de usuario

- [Crear una conexión de origen de Google BigQuery en la interfaz de usuario](../../tutorials/ui/create/databases/bigquery.md)
- [Crear un flujo de datos para una conexión de origen de base de datos en la interfaz de usuario](../../tutorials/ui/dataflow/databases.md)
