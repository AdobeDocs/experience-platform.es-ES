---
title: Información general sobre el conector Source de Snowflake Streaming
description: Obtenga información sobre cómo crear una conexión de origen y un flujo de datos para introducir datos de flujo continuo de la instancia de Snowflake a Adobe Experience Platform
badgeBeta: label="Beta" type="Informative"
badgeUltimate: label="Ultimate" type="Positive"
last-substantial-update: 2023-05-25T00:00:00Z
exl-id: ed937689-e844-487e-85fb-e3536c851fe5
source-git-commit: c80535cbb5dda55f1cf145f9f40bbcd40c78e63e
workflow-type: tm+mt
source-wordcount: '710'
ht-degree: 1%

---

# [!DNL Snowflake] origen de flujo

>[!IMPORTANT]
>
>* El origen de flujo continuo [!DNL Snowflake] está en fase beta. Lea [Resumen de fuentes](../../home.md#terms-and-conditions) para obtener más información sobre cómo usar fuentes con etiquetas beta.
>* El origen de flujo continuo [!DNL Snowflake] está disponible en la API para los usuarios que han adquirido Real-time Customer Data Platform Ultimate.

Adobe Experience Platform permite la ingesta de datos desde fuentes externas, al tiempo que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de Platform. Puede introducir datos de una variedad de fuentes, como aplicaciones de Adobe, almacenamiento basado en la nube, bases de datos y muchas otras.

El Experience Platform es compatible con la transmisión de datos desde una base de datos [!DNL Snowflake].

## Explicación del origen de flujo continuo [!DNL Snowflake]

El origen de flujo continuo [!DNL Snowflake] funciona cargando datos ejecutando periódicamente una consulta SQL y creando un registro de salida para cada fila del conjunto resultante.

Utilizando [!DNL Kafka Connect], el origen de flujo [!DNL Snowflake] realiza un seguimiento del último registro que recibe de cada tabla, de modo que pueda iniciarse en la ubicación correcta para la siguiente iteración. El origen utiliza esta funcionalidad para filtrar los datos y obtener solo las filas actualizadas de una tabla en cada iteración.

## Requisitos previos

En la siguiente sección se describen los pasos necesarios que se deben seguir para poder transmitir datos de la base de datos [!DNL Snowflake] al Experience Platform:

### Recopilar credenciales necesarias

Para que [!DNL Flow Service] se conecte con [!DNL Snowflake], debe proporcionar las siguientes propiedades de conexión:

| Credencial | Descripción |
| --- | --- |
| `account` | El nombre completo de la cuenta asociada con su cuenta de [!DNL Snowflake]. Un nombre de cuenta [!DNL Snowflake] completo incluye su nombre de cuenta, región y plataforma en la nube. Por ejemplo, `cj12345.east-us-2.azure`. Para obtener más información sobre los nombres de cuenta, consulte esta [[!DNL Snowflake document on account identifiers]](<https://docs.snowflake.com/en/user-guide/admin-account-identifier.html>). |
| `warehouse` | El almacén [!DNL Snowflake] administra el proceso de ejecución de consultas para la aplicación. Cada almacén de [!DNL Snowflake] es independiente entre sí y se debe acceder a él de forma individual al llevar datos a Platform. |
| `database` | La base de datos [!DNL Snowflake] contiene los datos que desea obtener de Platform. |
| `username` | El nombre de usuario de la cuenta [!DNL Snowflake]. |
| `password` | Contraseña de la cuenta de usuario [!DNL Snowflake]. |
| `role` | (Opcional) Una función personalizada que se puede proporcionar a un usuario para una conexión determinada. Si no se proporciona, el valor predeterminado es `public`. |
| `connectionSpec.id` | La especificación de conexión devuelve las propiedades del conector de origen, incluidas las especificaciones de autenticación relacionadas con la creación de las conexiones base y origen. El id. de especificación de conexión para [!DNL Snowflake] es `51ae16c2-bdad-42fd-9fce-8d5dfddaf140`. |


### Configurar las opciones de rol {#configure-role-settings}

Debe configurar privilegios en un rol, incluso si se asigna el rol público predeterminado, para permitir que la conexión de origen acceda a la base de datos, esquema y tabla [!DNL Snowflake] correspondiente. Los distintos privilegios para diferentes entidades de [!DNL Snowflake] son los siguientes:

| [!DNL Snowflake] entidad | Requerir privilegio de rol |
| --- | --- |
| Almacén | FUNCIONAMIENTO, USO |
| Base de datos | USO |
| Esquema | USO |
| Tabla | SELECT |

>[!NOTE]
>
>La reanudación automática y la suspensión automática deben habilitarse en la configuración avanzada del almacén.

Para obtener más información sobre la administración de roles y privilegios, consulte la [[!DNL Snowflake] referencia de API](<https://docs.snowflake.com/en/sql-reference/sql/grant-privilege>).

## Limitaciones y preguntas más frecuentes {#limitations-and-frequently-asked-questions}

* El rendimiento de datos para el origen de [!DNL Snowflake] es de 2000 registros por segundo.
* Los precios pueden variar según la cantidad de tiempo que un almacén esté activo y el tamaño del almacén. Para la integración de origen de [!DNL Snowflake], el almacén x-small de menor tamaño es suficiente. Se recomienda habilitar la suspensión automática para que el almacén pueda suspender por sí solo cuando no esté en uso.
* El origen [!DNL Snowflake] sondea la base de datos en busca de nuevos datos cada 10 segundos.
* Opciones de Configuration:
   * Puede habilitar un indicador booleano `backfill` para su origen [!DNL Snowflake] al crear una conexión de origen.
      * Si el relleno se establece en true, el valor de timestamp.initial se establece en 0. Esto significa que se recuperan los datos con una columna de marca de tiempo mayor que 0 epoch time.
      * Si el relleno se establece en False, el valor de timestamp.initial se establece en -1. Esto significa que se recuperan datos con una columna de marca de tiempo mayor que la hora actual (la hora en la que el origen comienza a ingerir).
   * La columna de marca de tiempo debe tener el formato de tipo: `TIMESTAMP_LTZ` o `TIMESTAMP_NTZ`. Si la columna de marca de tiempo se establece en `TIMESTAMP_NTZ`, la zona horaria correspondiente en la que se almacenan los valores se debe pasar a través del parámetro `timezoneValue`. Si no se proporciona, el valor predeterminado será UTC.
      * `TIMESTAMP_TZ` no se puede usar en una columna de marca de tiempo o en una asignación.

## Pasos siguientes

El siguiente tutorial proporciona pasos sobre cómo conectar el origen de flujo de [!DNL Snowflake] al Experience Platform mediante la API:

* [Transmitir datos de una base de datos  [!DNL Snowflake] al Experience Platform mediante la API de Flow Service](../../tutorials/api/create/databases/snowflake-streaming.md)
* [Transmitir datos de una base de datos  [!DNL Snowflake] al Experience Platform mediante el área de trabajo de orígenes en la interfaz de usuario del Experience Platform](../../tutorials/ui/create/databases/snowflake-streaming.md)
