---
title: Información general sobre el conector de origen de flujo Snowflake
description: Obtenga información sobre cómo crear una conexión de origen y un flujo de datos para introducir datos de flujo continuo de la instancia de Snowflake a Adobe Experience Platform
badgeBeta: label="Beta" type="Informative"
badgeUltimate: label="Ultimate" type="Positive"
last-substantial-update: 2023-05-25T00:00:00Z
source-git-commit: 9a8139c26b5bb5ff937a51986967b57db58aab6c
workflow-type: tm+mt
source-wordcount: '686'
ht-degree: 1%

---

# [!DNL Snowflake] fuente de transmisión

>[!IMPORTANT]
>
>* El [!DNL Snowflake] la fuente de streaming está en versión beta. Lea el [Resumen de orígenes](../../home.md#terms-and-conditions) para obtener más información sobre el uso de fuentes etiquetadas como beta.
>* El [!DNL Snowflake] La fuente de streaming está disponible en la API para los usuarios que han adquirido Real-time Customer Data Platform Ultimate.

Adobe Experience Platform permite la ingesta de datos desde fuentes externas, al tiempo que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de Platform. Puede introducir datos de una variedad de fuentes, como aplicaciones de Adobe, almacenamiento basado en la nube, bases de datos y muchas otras.

El Experience Platform de proporciona asistencia para la transmisión de datos desde un [!DNL Snowflake] base de datos.

## Explicación de la [!DNL Snowflake] fuente de transmisión

El [!DNL Snowflake] El origen de flujo continuo funciona teniendo datos cargados ejecutando periódicamente una consulta SQL y creando un registro de salida para cada fila en el conjunto resultante.

Mediante [!DNL Kafka Connect], el [!DNL Snowflake] streaming source realiza el seguimiento del último registro que recibe de cada tabla, de modo que pueda comenzar en la ubicación correcta para la siguiente iteración. El origen utiliza esta funcionalidad para filtrar los datos y obtener solo las filas actualizadas de una tabla en cada iteración.

## Requisitos previos

En la siguiente sección se describen los pasos necesarios que deben seguirse para poder transmitir datos desde la [!DNL Snowflake] base de datos a Experience Platform:

### Recopilar credenciales necesarias

Para que [!DNL Flow Service] para conectar con [!DNL Snowflake], debe proporcionar las siguientes propiedades de conexión:

| Credencial | Descripción |
| --- | --- |
| `account` | El nombre completo de la cuenta asociado con su [!DNL Snowflake] cuenta. Un completo [!DNL Snowflake] nombre de cuenta incluye su nombre de cuenta, región y cloud platform. Por ejemplo, `cj12345.east-us-2.azure`. Para obtener más información sobre los nombres de cuenta, consulte esta sección [[!DNL Snowflake document on account identifiers]](<https://docs.snowflake.com/en/user-guide/admin-account-identifier.html>). |
| `warehouse` | El [!DNL Snowflake] data warehouse administra el proceso de ejecución de consultas de la aplicación. Cada [!DNL Snowflake] El almacén de datos es independiente entre sí y debe accederse a él de forma individual al llevar los datos a Platform. |
| `database` | El [!DNL Snowflake] La base de datos de contiene los datos que desea traer a Platform. |
| `username` | El nombre de usuario de [!DNL Snowflake] cuenta. |
| `password` | La contraseña para el [!DNL Snowflake] cuenta de usuario. |
| `role` | (Opcional) Una función personalizada que se puede proporcionar a un usuario para una conexión determinada. Si no se proporciona, el valor predeterminado es `public`. |
| `connectionSpec.id` | La especificación de conexión devuelve las propiedades del conector de origen, incluidas las especificaciones de autenticación relacionadas con la creación de las conexiones base y origen. Identificador de especificación de conexión para [!DNL Snowflake] es `51ae16c2-bdad-42fd-9fce-8d5dfddaf140`. |

Para obtener más información sobre la autenticación, consulte [[!DNL Snowflake] documento](<https://docs.snowflake.com/en/user-guide/key-pair-auth.html>).

### Configurar las opciones de rol {#configure-role-settings}

Debe configurar privilegios en un rol, incluso si se asigna el rol público predeterminado, para permitir que la conexión de origen acceda al correspondiente [!DNL Snowflake] base de datos, esquema y tabla. Los distintos privilegios para diferentes [!DNL Snowflake] entidades es la siguiente:

| [!DNL Snowflake] entidad | Requerir privilegio de rol |
| --- | --- |
| Almacén | FUNCIONAMIENTO, USO |
| Base de datos | USO |
| Esquema | USO |
| Tabla | SELECT |

>[!NOTE]
>
>La reanudación automática y la suspensión automática deben habilitarse en la configuración avanzada del almacén.

Para obtener más información sobre la administración de roles y privilegios, consulte la [[!DNL Snowflake] Referencia de API](<https://docs.snowflake.com/en/sql-reference/sql/grant-privilege>).

## Limitaciones y preguntas más frecuentes {#limitations-and-frequently-asked-questions}

* El rendimiento de los datos para [!DNL Snowflake] fuente: 2000 registros por segundo.
* Los precios pueden variar según la cantidad de tiempo que un almacén esté activo y el tamaño del almacén. Para el [!DNL Snowflake] integración fuente, el tamaño más pequeño, x-pequeño almacén es suficiente. Se recomienda habilitar la suspensión automática para que el almacén pueda suspender por sí solo cuando no esté en uso.
* El [!DNL Snowflake] El origen sondea la base de datos en busca de nuevos datos cada 10 segundos.
* Opciones de Configuration:
   * Puede activar un `backfill` indicador booleano para su [!DNL Snowflake] origen al crear una conexión de origen.
      * Si el relleno se establece en true, el valor de timestamp.initial se establece en 0. Esto significa que se recuperan los datos con una columna de marca de tiempo buena a 0 epoch time.
      * Si el relleno se establece en False, el valor de timestamp.initial se establece en -1. Esto significa que se recuperan los datos con una columna de marca de tiempo buena a la hora actual (la hora en la que el origen comienza a ingerir).
   * La columna de marca de tiempo debe tener el formato tipo: `TIMESTAMP_LTZ` o `TIMESTAMP_NTZ`. Si la columna de marca de tiempo se establece en `TIMESTAMP_NTZ`, los tipos deben almacenarse en hora UTC en la base de datos.

## Pasos siguientes

El siguiente tutorial proporciona pasos sobre cómo conectar su [!DNL Snowflake] fuente de streaming al Experience Platform mediante la API:

* [Transmita datos desde un [!DNL Snowflake] base de datos a Experience Platform mediante la API de Flow Service](../../tutorials/api/create/databases/snowflake-streaming.md)

