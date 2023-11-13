---
title: Información general sobre el conector de origen de Google BigQuery
description: Obtenga información sobre cómo conectar Google BigQuery a Adobe Experience Platform mediante API o la interfaz de usuario.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 35c61382-a909-47f4-a937-15cb725ecbe3
source-git-commit: 9a8139c26b5bb5ff937a51986967b57db58aab6c
workflow-type: tm+mt
source-wordcount: '396'
ht-degree: 0%

---

# [!DNL Google BigQuery] origen

>[!IMPORTANT]
>
>El [!DNL Google BigQuery] La fuente de está disponible en el catálogo de fuentes de para los usuarios que han adquirido Real-time Customer Data Platform Ultimate.

Adobe Experience Platform permite la ingesta de datos desde fuentes externas, al tiempo que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de Platform. Puede introducir datos de una variedad de fuentes, como aplicaciones de Adobe, almacenamiento basado en la nube, bases de datos y muchas otras.

[!DNL Experience Platform] proporciona compatibilidad con la ingesta de datos de una base de datos de terceros. Platform puede conectarse a diferentes tipos de bases de datos, como relacionales, NoSQL o almacenes de datos. Los proveedores de bases de datos admiten [!DNL Google BigQuery].

## LISTA DE PERMITIDOS de direcciones IP

Se debe agregar una lista de direcciones IP a una lista de permitidos antes de trabajar con conectores de origen. Si no se agregan las direcciones IP específicas de la región a la lista de permitidos, pueden producirse errores o no rendimiento al utilizar fuentes. Consulte la [LISTA DE PERMITIDOS de direcciones IP](../../ip-address-allow-list.md) para obtener más información.

## Requisitos previos

En la siguiente sección se proporciona más información sobre la configuración de requisitos previos necesaria para crear un [!DNL Google BigQuery] conexión de origen.

### Genere su [!DNL Google BigQuery] credenciales

Para conectar [!DNL Google BigQuery] En Platform, debe generar valores para las siguientes credenciales:

| Credencial | Descripción |
| ---------- | ----------- |
| `project` | El proyecto es la entidad organizadora de nivel base para su [!DNL Google Cloud] recursos, incluidos [!DNL Google BigQuery]. |
| `clientID` | El ID de cliente es la mitad de [!DNL Google BigQuery] Credenciales de OAuth 2.0 |
| `clientSecret` | El secreto del cliente es la otra mitad de su [!DNL Google BigQuery] Credenciales de OAuth 2.0 |
| `refreshToken` | El token de actualización le permite obtener nuevos tokens de acceso para su API. Los tokens de acceso tienen una duración limitada y pueden caducar durante el transcurso del proyecto. Puede utilizar el token de actualización para autenticar y solicitar tokens de acceso posteriores para su proyecto cuando sea necesario. |
| `largeResultsDataSetId` | El elemento creado previamente  [!DNL Google BigQuery] ID del conjunto de datos necesario para habilitar la compatibilidad con grandes conjuntos de resultados. |

Para obtener instrucciones detalladas sobre cómo generar credenciales de OAuth 2.0 para [!DNL Google] API, consulte lo siguiente [[!DNL Google] Guía de autenticación de OAuth 2.0](https://developers.google.com/identity/protocols/oauth2).

## Connect [!DNL Google BigQuery] a Platform

La siguiente documentación proporciona información sobre cómo conectarse [!DNL Google BigQuery] Vaya a Platform mediante las API o la interfaz de usuario de:

### Uso de API

- [Creación de una conexión base de Google BigQuery mediante la API de Flow Service](../../tutorials/api/create/databases/bigquery.md)
- [Exploración de tablas de datos mediante la API de Flow Service](../../tutorials/api/explore/tabular.md)
- [Crear un flujo de datos para un origen de base de datos mediante la API de Flow Service](../../tutorials/api/collect/database-nosql.md)

### Uso de la IU

- [Creación de una conexión de origen de Google BigQuery en la IU](../../tutorials/ui/create/databases/bigquery.md)
- [Crear un flujo de datos para una conexión de origen de base de datos en la IU](../../tutorials/ui/dataflow/databases.md)
