---
title: Información general sobre el conector Snowflake Source
description: Obtenga información sobre cómo conectar Snowflake a Adobe Experience Platform mediante API o la interfaz de usuario.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: df066463-1ae6-4ecd-ae0e-fb291cec4bd5
source-git-commit: 687363ab664e43cc854b535760dfbfc55acefd2c
workflow-type: tm+mt
source-wordcount: '1570'
ht-degree: 2%

---

# Fuente de [!DNL Snowflake] 

>[!IMPORTANT]
>
>* El origen [!DNL Snowflake] está disponible en el catálogo de orígenes para los usuarios que han adquirido Real-Time Customer Data Platform Ultimate.
>* De manera predeterminada, el origen [!DNL Snowflake] interpreta `null` como una cadena vacía. Póngase en contacto con su representante de Adobe para asegurarse de que los valores de `null` se escriban correctamente como `null` en Adobe Experience Platform.
>* Para que Experience Platform pueda introducir datos, las zonas horarias de todos los orígenes de lotes basados en tablas deben configurarse en UTC. La única marca de tiempo compatible con el origen [!DNL Snowflake] es TIMESTAMP_NTZ con la hora UTC.

[!DNL Snowflake] es una plataforma de almacén de datos basada en la nube diseñada para permitir a las organizaciones almacenar, procesar y analizar grandes volúmenes de datos de forma eficaz. Creado para aprovechar la escalabilidad y flexibilidad de la nube, [!DNL Snowflake] admite la integración de datos, análisis avanzados y uso compartido fluido entre equipos. Como servicio totalmente administrado, [!DNL Snowflake] elimina las complejidades de mantenimiento comunes a las bases de datos tradicionales, lo que le permite centrarse en obtener información y valor de sus datos.

Puede usar el origen [!DNL Snowflake] para conectarse y llevar los datos de [!DNL Snowflake] a Adobe Experience Platform. Lea la siguiente documentación para aprender a configurar el origen de [!DNL Snowflake] y conectarse a Experience Platform.

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
| `account` | Un nombre de cuenta identifica de forma exclusiva una cuenta de su organización. En este caso, debe identificar una cuenta de forma exclusiva en diferentes organizaciones de [!DNL Snowflake]. Para ello, debe anteponer el nombre de su organización al nombre de la cuenta. Por ejemplo: `myorg-myaccount.snowflakecomputing.com`. Lee la sección sobre [cómo recuperar tu [!DNL Snowflake] identificador de cuenta](#retrieve-your-account-identifier) para obtener más instrucciones. Para obtener más información, consulte la [[!DNL Snowflake] documentación](https://docs.snowflake.com/en/user-guide/admin-account-identifier#format-1-preferred-account-name-in-your-organization). |
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
| `account` | Un nombre de cuenta identifica de forma exclusiva una cuenta de su organización. En este caso, debe identificar una cuenta de forma exclusiva en diferentes organizaciones de [!DNL Snowflake]. Para ello, debe anteponer el nombre de su organización al nombre de la cuenta. Por ejemplo: `myorg-myaccount.snowflakecomputing.com`. Lee la sección sobre [cómo recuperar tu [!DNL Snowflake] identificador de cuenta](#retrieve-your-account-identifier) para obtener más instrucciones. Para obtener más información, consulte la [[!DNL Snowflake] documentación](https://docs.snowflake.com/en/user-guide/admin-account-identifier#format-1-preferred-account-name-in-your-organization). |
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
| `account` | Un nombre de cuenta identifica de forma exclusiva una cuenta de su organización. En este caso, debe identificar una cuenta de forma exclusiva en diferentes organizaciones de [!DNL Snowflake]. Para ello, debe anteponer el nombre de su organización al nombre de la cuenta. Por ejemplo: `http://myorg-myaccount.snowflakecomputing.com/`. Lee la guía sobre [cómo recuperar tu [!DNL Snowflake] identificador de cuenta](#etrieve-your-account-identifier) para obtener instrucciones adicionales. Para obtener más información, consulte la [[!DNL Snowflake] documentación](https://docs.snowflake.com/en/user-guide/admin-account-identifier#format-1-preferred-account-name-in-your-organization). |
| `username` | El nombre de usuario de su cuenta de [!DNL Snowflake]. |
| `privateKey` | La clave privada del usuario [!DNL Snowflake], codificada en Base64 como una sola línea sin encabezados ni saltos de línea. Para prepararlo, copie el contenido del archivo PEM, quite las `BEGIN`/`END` líneas y todos los saltos de línea y, a continuación, codifique el resultado en base64. Lea la sección sobre [recuperación de la clave privada](#retrieve-your-private-key) para obtener más información. **Nota:** Actualmente no se admiten claves privadas cifradas para una conexión de AWS. |
| `port` | Número de puerto que usa [!DNL Snowflake] al conectarse a un servidor a través de Internet. |
| `database` | La base de datos [!DNL Snowflake] que contiene los datos que desea introducir en Experience Platform. |
| `warehouse` | El almacén [!DNL Snowflake] administra el proceso de ejecución de consultas para la aplicación. Cada almacén de [!DNL Snowflake] es independiente entre sí y se debe acceder a él de forma individual al llevar datos a Experience Platform. |

Para obtener más información sobre estos valores, consulte la [[!DNL Snowflake] guía de autenticación de par clave](https://docs.snowflake.com/en/user-guide/key-pair-auth.html).

>[!ENDTABS]

### Recuperación del identificador de cuenta {#retrieve-your-account-identifier}

Debe recuperar su identificador de cuenta del panel de interfaz de usuario de [!DNL Snowflake], ya que lo utilizará para autenticar su instancia de [!DNL Snowflake] en Experience Platform.

Para recuperar el identificador de la cuenta:

* Use el [[!DNL Snowflake] panel de interfaz de usuario de la aplicación](https://app.snowflake.com/) para acceder a su cuenta.
* En el panel de navegación izquierdo, seleccione **[!DNL Accounts]** y, a continuación, seleccione **[!DNL Active Accounts]** en el encabezado.
* A continuación, seleccione el icono de información y, luego, seleccione y copie el nombre de dominio de la dirección URL actual.

![Panel de interfaz de usuario de Snowflake con el nombre de dominio seleccionado.](../../images/tutorials/create/snowflake/snowflake-dashboard.png)

### Genere su par de claves RSA

Use OpenSSL en la interfaz de línea de comandos para generar un par de claves RSA de 2048 bits en formato PKCS#8. Se recomienda crear una clave privada cifrada para la seguridad, que requerirá una frase de contraseña.

>[!BEGINTABS]

>[!TAB Generar una clave privada cifrada]

Para generar su clave privada [!DNL Snowflake] cifrada, ejecute el siguiente comando en el terminal:

```bash
openssl genrsa 2048 | openssl pkcs8 -topk8 -v2 des3 -inform PEM -out rsa_key.p8# You will be prompted to enter a passphrase. Store this securely!
```

>[!TAB Generar una clave privada no cifrada]

Para generar la clave privada [!DNL Snowflake] sin cifrar, ejecute el siguiente comando en el terminal:

```bash
openssl genrsa 2048 | openssl pkcs8 -topk8 -inform PEM -out rsa_key.p8 -nocrypt
```

>[!ENDTABS]

### Genere una clave pública a partir de su clave privada

A continuación, ejecute el siguiente comando en la interfaz de la línea de comandos para crear una clave pública basada en la clave privada.

```bash
openssl rsa -in rsa_key.p8 -pubout -out rsa_key.pub# You will be prompted to enter the passphrase if the private key is encrypted.
```

### Asignar la clave pública al usuario [!DNL Snowflake]

Debe usar un rol de administrador de [!DNL Snowflake] (como **SECURITYADMIN**) para asociar la clave pública generada con el usuario de servicio [!DNL Snowflake] que usará Experience Platform. Para recuperar el contenido de clave pública, abra el archivo `rsa_key.pub` y copie todo el contenido, excluyendo las `-----BEGIN PUBLIC KEY----- and -----END PUBLIC KEY-----` líneas. A continuación, ejecute el siguiente SQL en [!DNL Snowflake]:

```sql
ALTER USER {YOUR_SNOWFLAKE_USERNAME}>SET RSA_PUBLIC_KEY='{PUBLIC_KEY_CONTENT}';
```

### Codifique la clave privada en [!DNL Base64]

Experience Platform requiere que la clave privada esté codificada en [!DNL Base64] y se proporcione como una cadena durante la configuración de la conexión. Use una herramienta o script adecuado para codificar el contenido del archivo `rsa_key.p8` en una sola cadena [!DNL Base64].

>[!TIP]
>
>Asegúrese de que no haya espacios ni saltos de línea adicionales, incluidas las líneas de encabezado/pie de página `(-----BEGIN ENCRYPTED PRIVATE KEY----- and -----END ENCRYPTED PRIVATE KEY-----)`, antes o después del proceso de codificación, ya que esto puede provocar errores de autenticación.

### Comprobar configuraciones

Antes de crear la conexión de origen de [!DNL Snowflake] en Experience Platform, debe asegurarse de que **[!DNL Default Role]** y **[!DNL Default Warehouse]** del usuario coincidan con los valores proporcionados en Experience Platform. Puede comprobar esta configuración en la interfaz de usuario de [!DNL Snowflake] mediante el comando SQL `DESCRIBE USER {USERNAME}`.

También puede seguir los pasos a continuación para comprobar la configuración:

* Seleccione **[!DNL Admin]** en el panel de navegación izquierdo y luego seleccione **[!DNL Users & Roles]**.
* Seleccione el usuario adecuado y, a continuación, seleccione los puntos suspensivos (`...`) en la esquina superior derecha.
* En la ventana [!DNL Edit user] que aparece, vaya a [!DNL Default Role] para ver la función asociada con el usuario determinado.
* En la misma ventana, vaya a [!DNL Default Warehouse] para ver el almacén asociado con el usuario determinado.

![Interfaz de usuario de Snowflake donde puede comprobar su rol y almacén.](../../images/tutorials/create/snowflake/snowflake-configs.png)

## Próximos pasos

Una vez completada la instalación, ahora puede continuar conectando su cuenta de [!DNL Snowflake] a Experience Platform. Lea la siguiente documentación para obtener más información:

### Conectar [!DNL Snowflake] a Experience Platform mediante API

* [Conectar  [!DNL Snowflake] a Experience Platform mediante la API](../../tutorials/api/create/databases/snowflake.md)
* [Exploración de tablas de datos mediante la API de Flow Service](../../tutorials/api/explore/tabular.md)
* [Crear un flujo de datos para un origen de base de datos mediante la API de Flow Service](../../tutorials/api/collect/database-nosql.md)

### Conectar [!DNL Snowflake] a Experience Platform mediante la interfaz de usuario

* [Conectar  [!DNL Snowflake] a Experience Platform mediante la interfaz de usuario](../../tutorials/ui/create/databases/snowflake.md)
* [Crear un flujo de datos para una conexión de origen de base de datos en la IU](../../tutorials/ui/dataflow/databases.md)
