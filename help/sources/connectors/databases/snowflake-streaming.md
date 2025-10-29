---
title: Información general sobre el conector Source de Snowflake Streaming
description: Obtenga información sobre cómo crear una conexión de origen y un flujo de datos para introducir datos de flujo continuo de la instancia de Snowflake a Adobe Experience Platform
badgeUltimate: label="Ultimate" type="Positive"
exl-id: ed937689-e844-487e-85fb-e3536c851fe5
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '1510'
ht-degree: 3%

---

# [!DNL Snowflake] origen de flujo

>[!IMPORTANT]
>
>* El origen de flujo continuo [!DNL Snowflake] está disponible en la API para los usuarios que han adquirido Real-Time CDP Ultimate.
>
>* Ahora puede usar el origen de flujo continuo [!DNL Snowflake] al ejecutar Adobe Experience Platform en Amazon Web Service (AWS). Experience Platform que se ejecuta en AWS está disponible actualmente para un número limitado de clientes. Para obtener más información sobre la infraestructura de Experience Platform compatible, consulte la [descripción general de la nube múltiple de Experience Platform](../../../landing/multi-cloud.md).

Adobe Experience Platform permite la ingesta de datos desde fuentes externas, al tiempo que ofrece la posibilidad de estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de Experience Platform. Puede introducir datos de una variedad de fuentes, como aplicaciones de Adobe, almacenamiento basado en la nube, bases de datos y muchas otras.

Experience Platform proporciona compatibilidad para la transmisión de datos desde una base de datos de [!DNL Snowflake].

## Explicación del origen de flujo continuo [!DNL Snowflake]

El origen de flujo continuo [!DNL Snowflake] funciona cargando datos ejecutando periódicamente una consulta SQL y creando un registro de salida para cada fila del conjunto resultante.

Utilizando [!DNL Kafka Connect], el origen de flujo [!DNL Snowflake] realiza un seguimiento del último registro que recibe de cada tabla, de modo que pueda iniciarse en la ubicación correcta para la siguiente iteración. El origen utiliza esta funcionalidad para filtrar los datos y obtener solo las filas actualizadas de una tabla en cada iteración.

## Requisitos previos

En la siguiente sección se describen los pasos necesarios que se deben seguir para poder transmitir datos de la base de datos [!DNL Snowflake] a Experience Platform:

### LISTA DE PERMITIDOS de direcciones IP

Debe añadir direcciones IP específicas de la región a la lista de permitidos antes de conectar los orígenes a Experience Platform. Para obtener más información, lea la guía de [inclusión en la lista de permitidos de direcciones IP para conectarse a Experience Platform](../../ip-address-allow-list.md).

La siguiente documentación proporciona información sobre cómo conectar [!DNL Amazon Redshift] a Experience Platform mediante API o la interfaz de usuario:

### Recopilar credenciales necesarias

Para que [!DNL Flow Service] se conecte con [!DNL Snowflake], debe proporcionar las siguientes propiedades de conexión:

>[!BEGINTABS]

>[!TAB Autenticación básica]

| Credencial | Descripción |
| --- | --- |
| `account` | El identificador de cuenta completo (nombre de cuenta o localizador de cuentas) de su cuenta [!DNL Snowflake], anexado con el sufijo `snowflakecomputing.com`. El identificador de cuenta puede tener diferentes formatos: <ul><li>{ORG_NAME}-{ACCOUNT_NAME}.snowflakecomputing.com (p. ej. `acme-abc12345.snowflakecomputing.com`)</li><li>{ACCOUNT_LOCATOR}.{CLOUD_REGION_ID}.snowflakecomputing.com (p. ej. `acme12345.ap-southeast-1.snowflakecomputing.com`)</li><li>{ACCOUNT_LOCATOR}.{CLOUD_REGION_ID}.{CLOUD}.snowflakecomputing.com (p. ej. `acme12345.east-us-2.azure.snowflakecomputing.com`)</li></ul> Para obtener más información, lea [[!DNL Snowflake document on account identifiers]](<https://docs.snowflake.com/en/user-guide/admin-account-identifier.html>). |
| `warehouse` | El almacén [!DNL Snowflake] administra el proceso de ejecución de consultas para la aplicación. Cada almacén de [!DNL Snowflake] es independiente entre sí y se debe acceder a él de forma individual al llevar datos a Experience Platform. |
| `database` | La base de datos [!DNL Snowflake] contiene los datos que desea obtener de Experience Platform. |
| `username` | El nombre de usuario de la cuenta [!DNL Snowflake]. |
| `password` | Contraseña de la cuenta de usuario [!DNL Snowflake]. |
| `role` | (Opcional) Una función personalizada que se puede proporcionar a un usuario para una conexión determinada. Si no se proporciona, el valor predeterminado es `public`. |
| `connectionSpec.id` | La especificación de conexión devuelve las propiedades del conector de origen, incluidas las especificaciones de autenticación relacionadas con la creación de las conexiones base y origen. El id. de especificación de conexión para [!DNL Snowflake] es `51ae16c2-bdad-42fd-9fce-8d5dfddaf140`. |

>[!TAB Autenticación de par de claves]

Para utilizar la autenticación de par clave, debe generar un par clave RSA de 2048 bits y, a continuación, proporcionar los siguientes valores al crear una cuenta para el origen [!DNL Snowflake].

| Credencial | Descripción |
| --- | --- |
| `account` | Un nombre de cuenta identifica de forma exclusiva una cuenta de su organización. En este caso, debe identificar una cuenta de forma exclusiva en diferentes organizaciones de [!DNL Snowflake]. Para ello, debe anteponer el nombre de su organización al nombre de la cuenta. Por ejemplo: `orgname-account_name`. Lee la guía sobre [cómo recuperar tu [!DNL Snowflake] identificador de cuenta](./snowflake.md#retrieve-your-account-identifier) para obtener instrucciones adicionales. Para obtener más información, consulte la [[!DNL Snowflake] documentación](https://docs.snowflake.com/en/user-guide/admin-account-identifier#format-1-preferred-account-name-in-your-organization). |
| `username` | El nombre de usuario de su cuenta de [!DNL Snowflake]. |
| `privateKey` | La clave privada codificada [!DNL Base64-] de su cuenta de [!DNL Snowflake]. Puede generar claves privadas cifradas o no cifradas. Si utiliza una clave privada cifrada, también debe proporcionar una frase de contraseña de clave privada al autenticarse con Experience Platform. Lee la guía sobre [recuperar tu [!DNL Snowflake] clave privada](./snowflake.md) para obtener más información. |
| `passphrase` | La frase de contraseña es una capa adicional de seguridad que debe utilizar al autenticarse con una clave privada cifrada. No es necesario que proporcione la frase de contraseña si utiliza una clave privada no cifrada. |
| `database` | La base de datos [!DNL Snowflake] que contiene los datos que desea introducir en Experience Platform. |
| `warehouse` | El almacén [!DNL Snowflake] administra el proceso de ejecución de consultas para la aplicación. Cada almacén de [!DNL Snowflake] es independiente entre sí y se debe acceder a él de forma individual al llevar datos a Experience Platform. |

Para obtener más información sobre estos valores, consulte la [[!DNL Snowflake] guía de autenticación de par clave](https://docs.snowflake.com/en/user-guide/key-pair-auth.html).

>[!ENDTABS]

### Recuperación del identificador de cuenta {#retrieve-your-account-identifier}

Para autenticar su instancia de [!DNL Snowflake] con Experience Platform, debe obtener su identificador de cuenta del panel de interfaz de usuario de [!DNL Snowflake].

Siga estos pasos para encontrar el identificador de su cuenta:

* Vaya a su cuenta en [[!DNL Snowflake] panel de interfaz de usuario de la aplicación](https://app.snowflake.com/).
* En el panel de navegación izquierdo, seleccione **[!DNL Accounts]**, seguido de **[!DNL Active Accounts]** en el encabezado.
* A continuación, seleccione el icono de información y, luego, seleccione y copie el nombre de dominio de la dirección URL actual.

### Recuperación de la clave privada {#retrieve-your-private-key}

Si planea usar la autenticación de par de claves para su conexión [!DNL Snowflake], debe generar una clave privada antes de conectarse a Experience Platform.

>[!BEGINTABS]

>[!TAB Crear una clave privada cifrada]

Para generar su clave privada [!DNL Snowflake] cifrada, ejecute el siguiente comando en el terminal:

```shell
openssl genrsa 2048 | openssl pkcs8 -topk8 -v2 des3 -inform PEM -out rsa_key.p8
```

Si lo consigue, debería recibir su clave privada en formato PEM.

```shell
|-----BEGIN ENCRYPTED PRIVATE KEY-----
MIIE6T...
|-----END ENCRYPTED PRIVATE KEY-----
```

>[!TAB Crear una clave privada no cifrada]

Para generar la clave privada [!DNL Snowflake] sin cifrar, ejecute el siguiente comando en el terminal:

```shell
openssl genrsa 2048 | openssl pkcs8 -topk8 -inform PEM -out rsa_key.p8 -nocrypt
```

Si lo consigue, debería recibir su clave privada en formato PEM.

```shell
|-----BEGIN PRIVATE KEY-----
MIIE6T...
|-----END PRIVATE KEY-----
```

>[!ENDTABS]

Después de generar la clave privada, codifíquela directamente en [!DNL Base64] sin realizar cambios en el formato o el contenido. Antes de codificar, asegúrese de que no haya espacios adicionales ni líneas en blanco (incluidas las líneas nuevas finales) al final de la clave privada.

### Comprobar configuraciones

Para poder crear una conexión de origen para los datos de [!DNL Snowflake], también debe asegurarse de que se cumplan las siguientes configuraciones:

* El almacén predeterminado asignado a un usuario determinado debe ser el mismo que el almacén introducido al autenticarse en Experience Platform.
* La función predeterminada asignada a un usuario determinado debe tener acceso a la misma base de datos que especificó al autenticarse en Experience Platform.

Para verificar su rol y almacén:

* Seleccione **[!DNL Admin]** en el panel de navegación izquierdo y luego seleccione **[!DNL Users & Roles]**.
* Seleccione el usuario adecuado y, a continuación, seleccione los puntos suspensivos (`...`) en la esquina superior derecha.
* En la ventana [!DNL Edit user] que aparece, vaya a [!DNL Default Role] para ver la función asociada con el usuario determinado.
* En la misma ventana, vaya a [!DNL Default Warehouse] para ver el almacén asociado con el usuario determinado.

Una vez codificada correctamente, puede utilizar esa clave privada codificada con [!DNL Base64] en Experience Platform para autenticar su cuenta de [!DNL Snowflake].

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

## Convertir tiempo Unix en campos de fecha

[!DNL Snowflake Streaming] analiza y escribe ` DATE` campos como el número de días desde la época de Unix (1970-01-01). Por ejemplo, un valor `DATE` de 0 significa 1 de enero de 1970, mientras que un valor de 1 significa 2 de enero de 1970. Por lo tanto, cuando prepare el archivo para crear asignaciones en el origen [!DNL Snowflake Streaming], asegúrese de que la columna `DATE` se representa como un número entero.

Puede usar [funciones de datos y tiempo de la preparación de datos](../../../data-prep/functions.md#date-and-time-functions) para convertir la hora Unix en campos de fecha que se pueden ingerir en Experience Platform. Por ejemplo:

```shell
dformat({DATE_COLUMN} * 86400000, "yyyy-MM-dd")
```

En esta función:

* `{DATE_COLUMN}` es la columna de fecha que contiene el entero epoch day.
* Al multiplicar por 86400000, los días de la época se convierten en milisegundos.
* &#39;dd-MM-yyyy&#39; especifica el formato de fecha deseado.

Esta conversión garantiza que la fecha se represente correctamente en el conjunto de datos.


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

## Próximos pasos

>[!NOTE]
>
>Después de crear o actualizar un flujo de datos de flujo continuo, se requiere una breve pausa de 5 minutos en la ingesta de datos para evitar cualquier posible instancia de pérdida o caída de datos.

El siguiente tutorial proporciona pasos sobre cómo conectar el origen de flujo continuo de [!DNL Snowflake] a Experience Platform mediante la API:

* [Transmitir datos de una base de datos  [!DNL Snowflake] a Experience Platform mediante la API de Flow Service](../../tutorials/api/create/databases/snowflake-streaming.md)
* [Transmitir datos de una base de datos  [!DNL Snowflake] a Experience Platform mediante el área de trabajo de orígenes en la interfaz de usuario de Experience Platform](../../tutorials/ui/create/databases/snowflake-streaming.md)
