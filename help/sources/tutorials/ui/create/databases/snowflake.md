---
title: Crear una conexión de origen de Snowflake en la interfaz de usuario
type: Tutorial
description: Obtenga información sobre cómo crear una conexión de origen de Snowflake mediante la interfaz de usuario de Adobe Experience Platform.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: fb2038b9-7f27-4818-b5de-cc8072122127
source-git-commit: 669b47753a9c9400f22aa81d08a4d25bb5e414c5
workflow-type: tm+mt
source-wordcount: '505'
ht-degree: 2%

---

# Crear un [!DNL Snowflake] conexión de origen en la interfaz de usuario

>[!IMPORTANT]
>
>El [!DNL Snowflake] La fuente de está disponible en el catálogo de fuentes de para los usuarios que han adquirido Real-time Customer Data Platform Ultimate.

Este tutorial proporciona los pasos para crear una [!DNL Snowflake] conector de origen mediante la interfaz de usuario de Adobe Experience Platform.

## Introducción

Este tutorial requiere una comprensión práctica de los siguientes componentes de Platform:

* [Fuentes](../../../../home.md): [!DNL Experience Platform] permite la ingesta de datos desde varias fuentes, al tiempo que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante [!DNL Platform] servicios.
* [Zonas protegidas](../../../../../sandboxes/home.md): [!DNL Experience Platform] proporciona zonas protegidas virtuales que dividen una sola [!DNL Platform] en entornos virtuales independientes para ayudar a desarrollar y evolucionar aplicaciones de experiencia digital.

### Recopilar credenciales necesarias

Para acceder a su cuenta de Snowflake en [!DNL Platform], debe proporcionar el siguiente valor de autenticación:

| Credencial | Descripción |
| ---------- | ----------- |
| Cuenta | El nombre completo de la cuenta asociado con su [!DNL Snowflake] cuenta. Un completo [!DNL Snowflake] nombre de cuenta incluye su nombre de cuenta, región y cloud platform. Por ejemplo, `cj12345.east-us-2.azure`. Para obtener más información sobre los nombres de cuenta, consulte esta sección [[!DNL Snowflake document on account identifiers]](https://docs.snowflake.com/en/user-guide/admin-account-identifier.html). |
| Almacén | El [!DNL Snowflake] data warehouse administra el proceso de ejecución de consultas de la aplicación. Cada [!DNL Snowflake] El almacén es independiente entre sí y debe accederse a él de forma individual al llevar los datos a Platform. |
| Base de datos | El [!DNL Snowflake] La base de datos de contiene los datos que desea traer a Platform. |
| Nombre de usuario | El nombre de usuario de [!DNL Snowflake] cuenta. |
| Una contraseña | La contraseña para el [!DNL Snowflake] cuenta de usuario. |
| Función | La función de control de acceso predeterminada que se utilizará en [!DNL Snowflake] sesión. La función debe ser una función existente que ya se haya asignado al usuario especificado. La función predeterminada es `PUBLIC`. |
| Cadena de conexión | La cadena de conexión utilizada para conectarse a su [!DNL Snowflake] ejemplo. El patrón de cadena de conexión para [!DNL Snowflake] es `jdbc:snowflake://{ACCOUNT_NAME}.snowflakecomputing.com/?user={USERNAME}&password={PASSWORD}&db={DATABASE}&warehouse={WAREHOUSE}` |

Para obtener más información, consulte [este documento de Snowflake](https://docs.snowflake.com/en/user-guide/key-pair-auth.html).

>[!NOTE]
>
>Debe configurar la variable `PREVENT_UNLOAD_TO_INLINE_URL` marcar como `FALSE` para permitir la descarga de datos desde [!DNL Snowflake] base de datos a Experience Platform.

## Conecte su cuenta de Snowflake

En la IU de Platform, seleccione **[!UICONTROL Fuentes]** desde la navegación izquierda para acceder a [!UICONTROL Fuentes] workspace. El [!UICONTROL Catálogo] La pantalla muestra una variedad de fuentes con las que puede crear una cuenta.

Puede seleccionar la categoría adecuada del catálogo en la parte izquierda de la pantalla. También puede encontrar la fuente específica con la que desea trabajar en la barra de búsqueda.

En el [!UICONTROL Bases de datos] categoría, seleccionar **[!UICONTROL Snowflake]** y luego seleccione **[!UICONTROL Añadir datos]**.

![](../../../../images/tutorials/create/snowflake/catalog.png)

El **[!UICONTROL Conectar con el Snowflake]** página. En esta página, puede usar credenciales nuevas o existentes.

### Cuenta existente

Para conectar una cuenta existente, seleccione la cuenta de Snowflake con la que desee conectarse y, a continuación, seleccione **[!UICONTROL Siguiente]** para continuar.

![](../../../../images/tutorials/create/snowflake/existing.png)

### Nueva cuenta

Si está usando credenciales nuevas, seleccione **[!UICONTROL Nueva cuenta]**. En el formulario de entrada que aparece, proporcione un nombre, una descripción opcional y las credenciales de Snowflake. Cuando termine, seleccione **[!UICONTROL Connect]** y, a continuación, espere un poco para que se establezca la nueva conexión.

![](../../../../images/tutorials/create/snowflake/new.png)

## Pasos siguientes

Al seguir este tutorial, ha establecido una conexión con su cuenta de Snowflake. Ahora puede continuar con el siguiente tutorial y [configuración de un flujo de datos para introducir datos en [!DNL Platform]](../../dataflow/databases.md).
