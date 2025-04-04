---
title: Información general sobre el conector Snowflake Source
description: Obtenga información sobre cómo conectar Snowflake a Adobe Experience Platform mediante API o la interfaz de usuario.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: df066463-1ae6-4ecd-ae0e-fb291cec4bd5
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '694'
ht-degree: 0%

---

# [!DNL Snowflake] origen

>[!IMPORTANT]
>
>* El origen [!DNL Snowflake] está disponible en el catálogo de orígenes para los usuarios que han adquirido Real-Time Customer Data Platform Ultimate.
>* De manera predeterminada, el origen [!DNL Snowflake] interpreta `null` como una cadena vacía. Póngase en contacto con su representante de Adobe para asegurarse de que los valores de `null` se escriban correctamente como `null` en Adobe Experience Platform.
>* Para que Experience Platform pueda introducir datos, las zonas horarias de todos los orígenes de lotes basados en tablas deben configurarse en UTC. La única marca de tiempo compatible con el origen [!DNL Snowflake] es TIMESTAMP_NTZ con la hora UTC.

Adobe Experience Platform permite la ingesta de datos desde fuentes externas, al tiempo que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de Experience Platform. Puede introducir datos de una variedad de fuentes, como aplicaciones de Adobe, almacenamiento basado en la nube, bases de datos y muchas otras.

Experience Platform es compatible con la ingesta de datos desde una base de datos de terceros. Experience Platform puede conectarse a diferentes tipos de bases de datos, como relacionales, NoSQL o almacenes de datos. La compatibilidad con los proveedores de bases de datos incluye [!DNL Snowflake].

## Requisitos previos {#prerequisites}

En esta sección se describen las tareas de configuración que debe realizar para poder conectar el origen de [!DNL Snowflake] a Experience Platform.

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
-----BEGIN ENCRYPTED PRIVATE KEY-----
MIIE6T...
-----END ENCRYPTED PRIVATE KEY-----
```

>[!TAB Crear una clave privada no cifrada]

Para generar la clave privada [!DNL Snowflake] sin cifrar, ejecute el siguiente comando en el terminal:

```shell
openssl genrsa 2048 | openssl pkcs8 -topk8 -inform PEM -out rsa_key.p8 -nocrypt
```

Si lo consigue, debería recibir su clave privada en formato PEM.

```shell
-----BEGIN PRIVATE KEY-----
MIIE6T...
-----END PRIVATE KEY-----
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

## LISTA DE PERMITIDOS de direcciones IP

Se debe agregar una lista de direcciones IP a una lista de permitidos antes de trabajar con conectores de origen. Si no se agregan las direcciones IP específicas de la región a la lista de permitidos, pueden producirse errores o no rendimiento al utilizar fuentes. Consulte la página [lista de permitidos de direcciones IP](../../ip-address-allow-list.md) para obtener más información.

La siguiente documentación proporciona información sobre cómo conectar [!DNL Snowflake] a Experience Platform mediante API o la interfaz de usuario:

## Conectar [!DNL Snowflake] a Experience Platform mediante API

* [Crear una conexión base de Snowflake mediante la API de Flow Service](../../tutorials/api/create/databases/snowflake.md)
* [Exploración de tablas de datos mediante la API de Flow Service](../../tutorials/api/explore/tabular.md)
* [Crear un flujo de datos para un origen de base de datos mediante la API de Flow Service](../../tutorials/api/collect/database-nosql.md)

## Conectar [!DNL Snowflake] a Experience Platform mediante la interfaz de usuario

* [Crear una conexión de origen de Snowflake en la interfaz de usuario](../../tutorials/ui/create/databases/snowflake.md)
* [Crear un flujo de datos para una conexión de origen de base de datos en la IU](../../tutorials/ui/dataflow/databases.md)
