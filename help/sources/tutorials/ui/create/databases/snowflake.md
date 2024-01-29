---
title: Crear una conexión de origen de Snowflake en la interfaz de usuario
type: Tutorial
description: Obtenga información sobre cómo crear una conexión de origen de Snowflake mediante la interfaz de usuario de Adobe Experience Platform.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: fb2038b9-7f27-4818-b5de-cc8072122127
source-git-commit: 4de2193a45fc2925af310b5e2475eabe26d13adc
workflow-type: tm+mt
source-wordcount: '786'
ht-degree: 2%

---

# Crear un [!DNL Snowflake] conexión de origen en la interfaz de usuario

>[!IMPORTANT]
>
>El [!DNL Snowflake] La fuente de está disponible en el catálogo de fuentes de para los usuarios que han adquirido Real-time Customer Data Platform Ultimate.

Este tutorial proporciona los pasos para crear una [!DNL Snowflake] conector de origen mediante la interfaz de usuario de Adobe Experience Platform.

## Introducción

Este tutorial requiere una comprensión práctica de los siguientes componentes de Experience Platform:

* [Fuentes](../../../../home.md): [!DNL Experience Platform] permite la ingesta de datos desde varias fuentes, al tiempo que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante [!DNL Platform] servicios.
* [Zonas protegidas](../../../../../sandboxes/home.md): [!DNL Experience Platform] proporciona zonas protegidas virtuales que dividen una sola [!DNL Platform] en entornos virtuales independientes para ayudar a desarrollar y evolucionar aplicaciones de experiencia digital.

### Recopilar credenciales necesarias

Debe proporcionar valores para las siguientes propiedades de credenciales para autenticar su [!DNL Snowflake] origen.

>[!BEGINTABS]

>[!TAB Autenticación de clave de cuenta]

| Credencial | Descripción |
| ---------- | ----------- |
| Cuenta | Un nombre de cuenta identifica de forma exclusiva una cuenta de su organización. En este caso, debe identificar una cuenta de forma exclusiva en diferentes [!DNL Snowflake] organizaciones. Para ello, debe anteponer el nombre de su organización al nombre de la cuenta. Por ejemplo: `orgname-account_name`. Para obtener más información sobre los nombres de cuenta, lea la [!DNL Snowflake] documentación sobre [identificadores de cuenta](https://docs.snowflake.com/en/user-guide/admin-account-identifier#format-1-preferred-account-name-in-your-organization). |
| Almacén | El [!DNL Snowflake] data warehouse administra el proceso de ejecución de consultas de la aplicación. Cada [!DNL Snowflake] El almacén es independiente entre sí y debe accederse a él de forma individual al llevar los datos a Platform. |
| Base de datos | El [!DNL Snowflake] La base de datos de contiene los datos que desea traer a Platform. |
| Nombre de usuario | El nombre de usuario de [!DNL Snowflake] cuenta. |
| Una contraseña | La contraseña para el [!DNL Snowflake] cuenta de usuario. |
| Función | La función de control de acceso predeterminada que se utilizará en [!DNL Snowflake] sesión. La función debe ser una función existente que ya se haya asignado al usuario especificado. La función predeterminada es `PUBLIC`. |
| Cadena de conexión | La cadena de conexión utilizada para conectarse a su [!DNL Snowflake] ejemplo. El patrón de cadena de conexión para [!DNL Snowflake] es `jdbc:snowflake://{ACCOUNT_NAME}.snowflakecomputing.com/?user={USERNAME}&password={PASSWORD}&db={DATABASE}&warehouse={WAREHOUSE}` |

>[!TAB Autenticación de par de claves]

Para utilizar la autenticación de par clave, debe generar un par clave RSA de 2048 bits y, a continuación, proporcionar los siguientes valores al crear una cuenta para su [!DNL Snowflake] origen.

| Credencial | Descripción |
| --- | --- |
| Cuenta | Un nombre de cuenta identifica de forma exclusiva una cuenta de su organización. En este caso, debe identificar una cuenta de forma exclusiva en diferentes [!DNL Snowflake] organizaciones. Para ello, debe anteponer el nombre de su organización al nombre de la cuenta. Por ejemplo: `orgname-account_name`. Para obtener más información sobre los nombres de cuenta, lea la [!DNL Snowflake] documentación sobre [identificadores de cuenta](https://docs.snowflake.com/en/user-guide/admin-account-identifier#format-1-preferred-account-name-in-your-organization). |
| Nombre de usuario | El nombre de usuario de su [!DNL Snowflake] cuenta. |
| Clave privada | El [!DNL Base64-]clave privada codificada de su [!DNL Snowflake] cuenta. Puede generar claves privadas cifradas o no cifradas. Si utiliza una clave privada cifrada, también debe proporcionar una frase de contraseña de clave privada al autenticarse con el Experience Platform. |
| Frase de contraseña de clave privada | La frase de contraseña de clave privada es una capa adicional de seguridad que debe utilizar al autenticarse con una clave privada cifrada. No es necesario que proporcione la frase de contraseña si utiliza una clave privada no cifrada. |
| Base de datos | El [!DNL Snowflake] base de datos que contiene los datos que desea introducir en Experience Platform. |
| Almacén | El [!DNL Snowflake] data warehouse administra el proceso de ejecución de consultas de la aplicación. Cada [!DNL Snowflake] El almacén es independiente entre sí y debe accederse a él de forma individual al llevar los datos a Platform. |

Para obtener más información, consulte [este documento de Snowflake](https://docs.snowflake.com/en/user-guide/key-pair-auth.html).

>[!ENDTABS]

Para acceder a su cuenta de Snowflake en Experience Platform, debe proporcionar el siguiente valor de autenticación:

>[!NOTE]
>
>Debe configurar la variable `PREVENT_UNLOAD_TO_INLINE_URL` marcar como `FALSE` para permitir la descarga de datos desde [!DNL Snowflake] base de datos a Experience Platform.

## Conecte su cuenta de Snowflake

En la IU de Platform, seleccione **[!UICONTROL Fuentes]** desde la navegación izquierda para acceder a [!UICONTROL Fuentes] workspace.

Puede seleccionar la categoría adecuada del catálogo en la parte izquierda de la pantalla. También puede encontrar la fuente específica con la que desea trabajar en la barra de búsqueda.

En el [!UICONTROL Bases de datos] categoría, seleccionar **[!UICONTROL Snowflake]** y luego seleccione **[!UICONTROL Añadir datos]**.

![El catálogo de fuentes con [!DNL Snowflake] resaltado.](../../../../images/tutorials/create/snowflake/catalog.png)

El **[!UICONTROL Conectar con el Snowflake]** página. En esta página, puede usar credenciales nuevas o existentes.

### Cuenta existente

Para utilizar una cuenta existente, seleccione la [!DNL Snowflake] cuenta con la que desea conectarse y, a continuación, seleccione **[!UICONTROL Siguiente]** para continuar.

![Interfaz de cuenta existente en el flujo de trabajo de orígenes.](../../../../images/tutorials/create/snowflake/existing.png)

### Nueva cuenta

Para crear una nueva cuenta, seleccione **[!UICONTROL Nueva cuenta]** y, a continuación, proporcione un nombre y una descripción opcional para la nueva [!DNL Snowflake] cuenta.

![La nueva interfaz de cuenta en el flujo de trabajo de orígenes.](../../../../images/tutorials/create/snowflake/new.png)

>[!BEGINTABS]

>[!TAB Autenticación de clave de cuenta]

Para utilizar la autenticación de clave de cuenta, proporcione la cadena de conexión en el formulario de entrada y, a continuación, seleccione **[!UICONTROL Conectar con el origen]**.

![Interfaz de autenticación de clave de cuenta.](../../../../images/tutorials/create/snowflake/connection-string.png)

>[!TAB Autenticación de par de claves]

Para utilizar la autenticación de par clave, proporcione valores para su cuenta, nombre de usuario, clave privada, frase de contraseña de clave privada, base de datos y almacén y, a continuación, seleccione **[!UICONTROL Conectar con el origen]**.

![Interfaz de autenticación de par de claves de cuenta.](../../../../images/tutorials/create/snowflake/key-pair.png)

>[!ENDTABS]

## Pasos siguientes

Al seguir este tutorial, ha establecido una conexión con su cuenta de Snowflake. Ahora puede continuar con el siguiente tutorial y [configuración de un flujo de datos para introducir datos en [!DNL Platform]](../../dataflow/databases.md).
