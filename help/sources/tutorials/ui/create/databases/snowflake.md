---
title: Creación de una conexión de Snowflake Source en la interfaz de usuario
type: Tutorial
description: Obtenga información sobre cómo crear una conexión de origen de Snowflake mediante la interfaz de usuario de Adobe Experience Platform.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: fb2038b9-7f27-4818-b5de-cc8072122127
source-git-commit: 4de2193a45fc2925af310b5e2475eabe26d13adc
workflow-type: tm+mt
source-wordcount: '786'
ht-degree: 2%

---

# Crear una conexión de origen [!DNL Snowflake] en la interfaz de usuario

>[!IMPORTANT]
>
>El origen [!DNL Snowflake] está disponible en el catálogo de orígenes para los usuarios que han adquirido Real-time Customer Data Platform Ultimate.

Este tutorial proporciona los pasos para crear un conector de origen [!DNL Snowflake] mediante la interfaz de usuario de Adobe Experience Platform.

## Introducción

Este tutorial requiere una comprensión práctica de los siguientes componentes de Experience Platform:

* [Fuentes](../../../../home.md): [!DNL Experience Platform] permite la ingesta de datos de varias fuentes al tiempo que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de [!DNL Platform].
* [Zonas protegidas](../../../../../sandboxes/home.md): [!DNL Experience Platform] proporciona zonas protegidas virtuales que dividen una sola instancia de [!DNL Platform] en entornos virtuales independientes para ayudar a desarrollar y evolucionar aplicaciones de experiencia digital.

### Recopilar credenciales necesarias

Debe proporcionar valores para las siguientes propiedades de credenciales para autenticar el origen de [!DNL Snowflake].

>[!BEGINTABS]

>[!TAB Autenticación de clave de cuenta]

| Credencial | Descripción |
| ---------- | ----------- |
| Cuenta | Un nombre de cuenta identifica de forma exclusiva una cuenta de su organización. En este caso, debe identificar una cuenta de forma exclusiva en diferentes organizaciones de [!DNL Snowflake]. Para ello, debe anteponer el nombre de su organización al nombre de la cuenta. Por ejemplo: `orgname-account_name`. Para obtener más información sobre los nombres de cuenta, lea la documentación de [!DNL Snowflake] sobre [identificadores de cuenta](https://docs.snowflake.com/en/user-guide/admin-account-identifier#format-1-preferred-account-name-in-your-organization). |
| Almacén | El almacén [!DNL Snowflake] administra el proceso de ejecución de consultas para la aplicación. Cada almacén de [!DNL Snowflake] es independiente entre sí y se debe acceder a él de forma individual al llevar datos a Platform. |
| Base de datos | La base de datos [!DNL Snowflake] contiene los datos que desea obtener de Platform. |
| Nombre de usuario | El nombre de usuario de la cuenta [!DNL Snowflake]. |
| Contraseña | Contraseña de la cuenta de usuario [!DNL Snowflake]. |
| Función | La función de control de acceso predeterminada que se usará en la sesión [!DNL Snowflake]. La función debe ser una función existente que ya se haya asignado al usuario especificado. La función predeterminada es `PUBLIC`. |
| Cadena de conexión | Cadena de conexión utilizada para conectarse a la instancia [!DNL Snowflake]. El patrón de cadena de conexión de [!DNL Snowflake] es `jdbc:snowflake://{ACCOUNT_NAME}.snowflakecomputing.com/?user={USERNAME}&password={PASSWORD}&db={DATABASE}&warehouse={WAREHOUSE}` |

>[!TAB Autenticación de par de claves]

Para utilizar la autenticación de par clave, debe generar un par clave RSA de 2048 bits y, a continuación, proporcionar los siguientes valores al crear una cuenta para el origen [!DNL Snowflake].

| Credencial | Descripción |
| --- | --- |
| Cuenta | Un nombre de cuenta identifica de forma exclusiva una cuenta de su organización. En este caso, debe identificar una cuenta de forma exclusiva en diferentes organizaciones de [!DNL Snowflake]. Para ello, debe anteponer el nombre de su organización al nombre de la cuenta. Por ejemplo: `orgname-account_name`. Para obtener más información sobre los nombres de cuenta, lea la documentación de [!DNL Snowflake] sobre [identificadores de cuenta](https://docs.snowflake.com/en/user-guide/admin-account-identifier#format-1-preferred-account-name-in-your-organization). |
| Nombre de usuario | El nombre de usuario de su cuenta de [!DNL Snowflake]. |
| Clave privada | La clave privada codificada [!DNL Base64-] de su cuenta de [!DNL Snowflake]. Puede generar claves privadas cifradas o no cifradas. Si utiliza una clave privada cifrada, también debe proporcionar una frase de contraseña de clave privada al autenticarse con el Experience Platform. |
| Frase de contraseña de clave privada | La frase de contraseña de clave privada es una capa adicional de seguridad que debe utilizar al autenticarse con una clave privada cifrada. No es necesario que proporcione la frase de contraseña si utiliza una clave privada no cifrada. |
| Base de datos | La base de datos [!DNL Snowflake] que contiene los datos que desea introducir al Experience Platform. |
| Almacén | El almacén [!DNL Snowflake] administra el proceso de ejecución de consultas para la aplicación. Cada almacén de [!DNL Snowflake] es independiente entre sí y se debe acceder a él de forma individual al llevar datos a Platform. |

Para obtener más información sobre estos valores, consulte [este documento de Snowflake](https://docs.snowflake.com/en/user-guide/key-pair-auth.html).

>[!ENDTABS]

Para acceder a su cuenta de Snowflake en Experience Platform, debe proporcionar el siguiente valor de autenticación:

>[!NOTE]
>
>Debe establecer el indicador `PREVENT_UNLOAD_TO_INLINE_URL` en `FALSE` para permitir la descarga de datos de la base de datos [!DNL Snowflake] al Experience Platform.

## Conecte su cuenta de Snowflake

En la interfaz de usuario de Platform, seleccione **[!UICONTROL Sources]** en el panel de navegación izquierdo para acceder al área de trabajo [!UICONTROL Sources].

Puede seleccionar la categoría adecuada del catálogo en la parte izquierda de la pantalla. También puede encontrar la fuente específica con la que desea trabajar en la barra de búsqueda.

En la categoría [!UICONTROL Bases de datos], seleccione **[!UICONTROL Snowflake]** y, a continuación, seleccione **[!UICONTROL Agregar datos]**.

![El catálogo de orígenes con [!DNL Snowflake] resaltado.](../../../../images/tutorials/create/snowflake/catalog.png)

Aparecerá la página **[!UICONTROL Conectarse al Snowflake]**. En esta página, puede usar credenciales nuevas o existentes.

### Cuenta existente

Para usar una cuenta existente, seleccione la cuenta de [!DNL Snowflake] con la que desee conectarse y, a continuación, seleccione **[!UICONTROL Siguiente]** para continuar.

![Interfaz de cuenta existente en el flujo de trabajo de orígenes.](../../../../images/tutorials/create/snowflake/existing.png)

### Nueva cuenta

Para crear una nueva cuenta, selecciona **[!UICONTROL Nueva cuenta]** y, a continuación, proporciona un nombre y una descripción opcional para la nueva cuenta de [!DNL Snowflake].

![La nueva interfaz de cuenta en el flujo de trabajo de orígenes.](../../../../images/tutorials/create/snowflake/new.png)

>[!BEGINTABS]

>[!TAB Autenticación de clave de cuenta]

Para usar la autenticación de clave de cuenta, proporciona la cadena de conexión en el formulario de entrada y, a continuación, selecciona **[!UICONTROL Conectar con el origen]**.

![Interfaz de autenticación de clave de cuenta.](../../../../images/tutorials/create/snowflake/connection-string.png)

>[!TAB Autenticación de par de claves]

Para usar la autenticación de par clave, proporciona valores para tu cuenta, nombre de usuario, clave privada, frase de contraseña de clave privada, base de datos y almacén y, a continuación, selecciona **[!UICONTROL Conectarse al origen]**.

![Interfaz de autenticación de par de claves de cuenta.](../../../../images/tutorials/create/snowflake/key-pair.png)

>[!ENDTABS]

## Pasos siguientes

Al seguir este tutorial, ha establecido una conexión con su cuenta de Snowflake. Ahora puede continuar con el siguiente tutorial y [configurar un flujo de datos para introducir datos en [!DNL Platform]](../../dataflow/databases.md).
