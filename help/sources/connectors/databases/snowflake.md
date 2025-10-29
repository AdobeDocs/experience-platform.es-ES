---
title: Información general sobre el conector Snowflake Source
description: Obtenga información sobre cómo conectar Snowflake a Adobe Experience Platform mediante API o la interfaz de usuario.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: df066463-1ae6-4ecd-ae0e-fb291cec4bd5
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '1502'
ht-degree: 3%

---

# Fuente de [!DNL Snowflake] 

>[!IMPORTANT]
>
>* El origen [!DNL Snowflake] está disponible en el catálogo de orígenes para los usuarios que han adquirido Real-Time Customer Data Platform Ultimate.
>* De manera predeterminada, el origen [!DNL Snowflake] interpreta `null` como una cadena vacía. Póngase en contacto con su representante de Adobe para asegurarse de que los valores de `null` se escriban correctamente como `null` en Adobe Experience Platform.
>* Para que Experience Platform pueda introducir datos, las zonas horarias de todos los orígenes de lotes basados en tablas deben configurarse en UTC. La única marca de tiempo compatible con el origen [!DNL Snowflake] es TIMESTAMP_NTZ con la hora UTC.

Adobe Experience Platform permite la ingesta de datos desde fuentes externas, al tiempo que ofrece la posibilidad de estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de Experience Platform. Puede introducir datos de una variedad de fuentes, como aplicaciones de Adobe, almacenamiento basado en la nube, bases de datos y muchas otras.

Experience Platform es compatible con la ingesta de datos desde una base de datos de terceros. Experience Platform puede conectarse a diferentes tipos de bases de datos, como relacionales, NoSQL o almacenes de datos. La compatibilidad con los proveedores de bases de datos incluye [!DNL Snowflake].

## Requisitos previos {#prerequisites}

En esta sección se describen las tareas de configuración que debe realizar para poder conectar el origen de [!DNL Snowflake] a Experience Platform.

### LISTA DE PERMITIDOS de direcciones IP

Debe añadir direcciones IP específicas de la región a la lista de permitidos antes de conectar los orígenes a Experience Platform. Para obtener más información, lea la guía de [inclusión en la lista de permitidos de direcciones IP para conectarse a Experience Platform](../../ip-address-allow-list.md).

### Recopilar credenciales necesarias

Debe proporcionar valores para las siguientes propiedades de credenciales para autenticar el origen de [!DNL Snowflake].

>[!BEGINTABS]

>[!TAB Autenticación de clave de cuenta (Azure)]

Proporcione valores para las siguientes credenciales para conectar [!DNL Snowflake] a Experience Platform en Azure mediante la autenticación de clave de cuenta.

| Credencial | Descripción |
| ---------- | ----------- |
| `account` | Un nombre de cuenta identifica de forma exclusiva una cuenta de su organización. En este caso, debe identificar una cuenta de forma exclusiva en diferentes organizaciones de [!DNL Snowflake]. Para ello, debe anteponer el nombre de su organización al nombre de la cuenta. Por ejemplo: `orgname-account_name`. Lee la sección sobre [cómo recuperar tu [!DNL Snowflake] identificador de cuenta](#retrieve-your-account-identifier) para obtener más instrucciones. Para obtener más información, consulte la [[!DNL Snowflake] documentación](https://docs.snowflake.com/en/user-guide/admin-account-identifier#format-1-preferred-account-name-in-your-organization). |
| `warehouse` | El almacén [!DNL Snowflake] administra el proceso de ejecución de consultas para la aplicación. Cada almacén de [!DNL Snowflake] es independiente entre sí y se debe acceder a él de forma individual al llevar datos a Experience Platform. |
| `database` | La base de datos [!DNL Snowflake] contiene los datos que desea obtener de Experience Platform. |
| `username` | El nombre de usuario de la cuenta [!DNL Snowflake]. |
| `password` | Contraseña de la cuenta de usuario [!DNL Snowflake]. |
| `role` | La función de control de acceso predeterminada que se usará en la sesión [!DNL Snowflake]. La función debe ser una función existente que ya se haya asignado al usuario especificado. La función predeterminada es `PUBLIC`. |
| `connectionString` | Cadena de conexión utilizada para conectarse a la instancia [!DNL Snowflake]. El patrón de cadena de conexión de [!DNL Snowflake] es `jdbc:snowflake://{ACCOUNT_NAME}.snowflakecomputing.com/?user={USERNAME}&password={PASSWORD}&db={DATABASE}&warehouse={WAREHOUSE}`. |

>[!TAB Autenticación de par de claves (Azure)]

Para utilizar la autenticación de par clave, genere primero un par clave RSA de 2048 bits. A continuación, proporcione valores para las siguientes credenciales para conectarse a Experience Platform en Azure mediante la autenticación de par de claves.

| Credencial | Descripción |
| --- | --- |
| `account` | Un nombre de cuenta identifica de forma exclusiva una cuenta de su organización. En este caso, debe identificar una cuenta de forma exclusiva en diferentes organizaciones de [!DNL Snowflake]. Para ello, debe anteponer el nombre de su organización al nombre de la cuenta. Por ejemplo: `orgname-account_name`. Lee la sección sobre [cómo recuperar tu [!DNL Snowflake] identificador de cuenta](#retrieve-your-account-identifier) para obtener más instrucciones. Para obtener más información, consulte la [[!DNL Snowflake] documentación](https://docs.snowflake.com/en/user-guide/admin-account-identifier#format-1-preferred-account-name-in-your-organization). |
| `username` | El nombre de usuario de su cuenta de [!DNL Snowflake]. |
| `privateKey` | La clave privada codificada [!DNL Base64-] de su cuenta de [!DNL Snowflake]. Puede generar claves privadas cifradas o no cifradas. Si utiliza una clave privada cifrada, también debe proporcionar una frase de contraseña de clave privada al autenticarse con Experience Platform. Lea la sección sobre [recuperación de la clave privada](#retrieve-your-private-key) para obtener más información. |
| `privateKeyPassphrase` | La frase de contraseña de clave privada es una capa adicional de seguridad que debe utilizar al autenticarse con una clave privada cifrada. No es necesario que proporcione la frase de contraseña si utiliza una clave privada no cifrada. |
| `port` | Número de puerto que usa [!DNL Snowflake] al conectarse a un servidor a través de Internet. |
| `database` | La base de datos [!DNL Snowflake] que contiene los datos que desea introducir en Experience Platform. |
| `warehouse` | El almacén [!DNL Snowflake] administra el proceso de ejecución de consultas para la aplicación. Cada almacén de [!DNL Snowflake] es independiente entre sí y se debe acceder a él de forma individual al llevar datos a Experience Platform. |

Para obtener más información sobre estos valores, consulte la [[!DNL Snowflake] guía de autenticación de par clave](https://docs.snowflake.com/en/user-guide/key-pair-auth.html).

>[!TAB Autenticación básica (AWS)]

Proporcione valores para las siguientes credenciales a fin de conectar [!DNL Snowflake] a Experience Platform en AWS mediante autenticación básica.

>[!WARNING]
>
>La autenticación básica (o autenticación de clave de cuenta) para el origen [!DNL Snowflake] quedará obsoleta en noviembre de 2025. Debe pasar a la autenticación basada en pares de claves para seguir utilizando el origen e introduciendo datos de la base de datos en Experience Platform. Para obtener más información sobre la obsolescencia, lea la [[!DNL Snowflake] guía de prácticas recomendadas sobre cómo mitigar los riesgos de compromiso de credenciales](https://www.snowflake.com/en/resources/white-paper/best-practices-to-mitigate-the-risk-of-credential-compromise/).

| Credencial | Descripción |
| --- | --- |
| `host` | La URL de host a la que se conecta su cuenta de [!DNL Snowflake]. |
| `port` | Número de puerto que usa [!DNL Snowflake] al conectarse a un servidor a través de Internet. |
| `username` | El nombre de usuario asociado con su cuenta de [!DNL Snowflake]. |
| `password` | La contraseña asociada a su cuenta de [!DNL Snowflake]. |
| `database` | Base de datos [!DNL Snowflake] de la que se extraerán los datos. |
| `schema` | Nombre del esquema asociado con la base de datos [!DNL Snowflake]. Debe asegurarse de que el usuario al que desea otorgar acceso a la base de datos también tenga acceso a este esquema. |
| `warehouse` | El almacén de [!DNL Snowflake] que está utilizando. |

>[!TAB Autenticación de par de claves (AWS)]

Para utilizar la autenticación de par clave, genere primero un par clave RSA de 2048 bits. A continuación, proporcione valores para las siguientes credenciales para conectarse a Experience Platform en AWS mediante la autenticación de par de claves.

| Credencial | Descripción |
| --- | --- |
| `account` | Un nombre de cuenta identifica de forma exclusiva una cuenta de su organización. En este caso, debe identificar una cuenta de forma exclusiva en diferentes organizaciones de [!DNL Snowflake]. Para ello, debe anteponer el nombre de su organización al nombre de la cuenta. Por ejemplo: `orgname-account_name`. Lee la guía sobre [cómo recuperar tu [!DNL Snowflake] identificador de cuenta](#etrieve-your-account-identifier) para obtener instrucciones adicionales. Para obtener más información, consulte la [[!DNL Snowflake] documentación](https://docs.snowflake.com/en/user-guide/admin-account-identifier#format-1-preferred-account-name-in-your-organization). |
| `username` | El nombre de usuario de su cuenta de [!DNL Snowflake]. |
| `privateKey` | La clave privada del usuario [!DNL Snowflake], codificada en Base64 como una sola línea sin encabezados ni saltos de línea. Para prepararlo, copie el contenido del archivo PEM, quite las `BEGIN`/`END` líneas y todos los saltos de línea y, a continuación, codifique el resultado en base64. Lea la sección sobre [recuperación de la clave privada](#retrieve-your-private-key) para obtener más información. **Nota:** Actualmente no se admiten claves privadas cifradas para una conexión de AWS. |
| `port` | Número de puerto que usa [!DNL Snowflake] al conectarse a un servidor a través de Internet. |
| `database` | La base de datos [!DNL Snowflake] que contiene los datos que desea introducir en Experience Platform. |
| `warehouse` | El almacén [!DNL Snowflake] administra el proceso de ejecución de consultas para la aplicación. Cada almacén de [!DNL Snowflake] es independiente entre sí y se debe acceder a él de forma individual al llevar datos a Experience Platform. |

Para obtener más información sobre estos valores, consulte la [[!DNL Snowflake] guía de autenticación de par clave](https://docs.snowflake.com/en/user-guide/key-pair-auth.html).

>[!ENDTABS]

### Recuperación del identificador de cuenta {#retrieve-your-account-identifier}

Debe recuperar su identificador de cuenta del panel de interfaz de usuario de [!DNL Snowflake], ya que utilizará el identificador de cuenta para autenticar su instancia de [!DNL Snowflake] en Experience Platform.

Para recuperar el identificador de la cuenta:

* Vaya a su cuenta en [[!DNL Snowflake] panel de interfaz de usuario de la aplicación](https://app.snowflake.com/).
* En el panel de navegación izquierdo, seleccione **[!DNL Accounts]**, seguido de **[!DNL Active Accounts]** en el encabezado.
* A continuación, seleccione el icono de información y, luego, seleccione y copie el nombre de dominio de la dirección URL actual.

![Panel de interfaz de usuario de Snowflake con el nombre de dominio seleccionado.](../../images/tutorials/create/snowflake/snowflake-dashboard.png)

### Recuperación de la clave privada {#retrieve-your-private-key}

Si está usando autenticación de par clave para su conexión [!DNL Snowflake], también debe generar la clave privada antes de conectarse a Experience Platform.

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

A continuación, tome su clave privada y códiquela en [!DNL Base64]. Asegúrese de no realizar ninguna transformación ni conversión de formato en la clave privada [!DNL Snowflake]. Además, debe asegurarse de que no haya caracteres de línea nueva al final de la clave privada antes de codificarla en [!DNL Base64].

### Comprobar configuraciones

Para poder crear una conexión de origen para los datos de [!DNL Snowflake], también debe asegurarse de que se cumplan las siguientes configuraciones:

* El almacén predeterminado asignado a un usuario determinado debe ser el mismo que el almacén introducido al autenticarse en Experience Platform.
* La función predeterminada asignada a un usuario determinado debe tener acceso a la misma base de datos que especificó al autenticarse en Experience Platform.

Para verificar su rol y almacén:

* Seleccione **[!DNL Admin]** en el panel de navegación izquierdo y luego seleccione **[!DNL Users & Roles]**.
* Seleccione el usuario adecuado y, a continuación, seleccione los puntos suspensivos (`...`) en la esquina superior derecha.
* En la ventana [!DNL Edit user] que aparece, vaya a [!DNL Default Role] para ver la función asociada con el usuario determinado.
* En la misma ventana, vaya a [!DNL Default Warehouse] para ver el almacén asociado con el usuario determinado.

![Interfaz de usuario de Snowflake donde puede comprobar su rol y almacén.](../../images/tutorials/create/snowflake/snowflake-configs.png)

Una vez codificada correctamente, puede utilizar esa clave privada codificada con [!DNL Base64] en Experience Platform para autenticar su cuenta de [!DNL Snowflake].

La siguiente documentación proporciona información sobre cómo conectar [!DNL Snowflake] a Experience Platform mediante API o la interfaz de usuario:

## Conectar [!DNL Snowflake] a Experience Platform mediante API

* [Crear una conexión base de Snowflake mediante la API de Flow Service](../../tutorials/api/create/databases/snowflake.md)
* [Exploración de tablas de datos mediante la API de Flow Service](../../tutorials/api/explore/tabular.md)
* [Crear un flujo de datos para un origen de base de datos mediante la API de Flow Service](../../tutorials/api/collect/database-nosql.md)

## Conectar [!DNL Snowflake] a Experience Platform mediante la interfaz de usuario

* [Crear una conexión de origen de Snowflake en la interfaz de usuario](../../tutorials/ui/create/databases/snowflake.md)
* [Crear un flujo de datos para una conexión de origen de base de datos en la IU](../../tutorials/ui/dataflow/databases.md)
