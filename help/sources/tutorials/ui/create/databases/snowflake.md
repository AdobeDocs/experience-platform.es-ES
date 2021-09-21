---
keywords: Experience Platform;inicio;temas populares;Snowflake
title: Crear una conexión de origen de Snowflake en la interfaz de usuario
topic-legacy: overview
type: Tutorial
description: Obtenga información sobre cómo crear una conexión de origen de Snowflake mediante la interfaz de usuario de Adobe Experience Platform.
source-git-commit: 2e717f33b487430220bd3bb7812558cde81d8852
workflow-type: tm+mt
source-wordcount: '431'
ht-degree: 1%

---

# Crear una conexión de origen [!DNL Snowflake] en la interfaz de usuario

>[!NOTE]
>
> El conector [!DNL Snowflake] está en versión beta. Consulte la [información general sobre fuentes](../../../../home.md#terms-and-conditions) para obtener más información sobre el uso de conectores con etiqueta beta.

Este tutorial proporciona los pasos para crear un conector de origen [!DNL Snowflake] mediante la interfaz de usuario de Adobe Experience Platform.

## Primeros pasos

Este tutorial requiere una comprensión práctica de los siguientes componentes de Platform:

* [Fuentes](../../../../home.md):  [!DNL Experience Platform] permite la ingesta de datos de varias fuentes, al mismo tiempo que permite estructurar, etiquetar y mejorar los datos entrantes mediante  [!DNL Platform] servicios.
* [Simuladores para pruebas](../../../../../sandboxes/home.md):  [!DNL Experience Platform] proporciona entornos limitados virtuales que dividen una sola  [!DNL Platform] instancia en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

### Recopilar las credenciales necesarias

Para acceder a su cuenta de Snowflake en [!DNL Platform], debe proporcionar el siguiente valor de autenticación:

| Credencial | Descripción |
| ---------- | ----------- |
| Cuenta | La cuenta [!DNL Snowflake] que desea conectar con Platform. |
| Almacén | El almacén [!DNL Snowflake] administra el proceso de ejecución de consultas para la aplicación. Cada [!DNL Snowflake] almacén es independiente entre sí y se debe acceder a él de forma individual al llevar los datos a Platform. |
| Database | El [!DNL Snowflake] contiene los datos que desea que traigan a la plataforma. |
| Nombre de usuario | El nombre de usuario de la cuenta [!DNL Snowflake]. |
| Contraseña | La contraseña de la cuenta de usuario [!DNL Snowflake]. |
| Cadena de conexión | La cadena de conexión utilizada para conectarse a la instancia [!DNL Snowflake]. El patrón de cadena de conexión para [!DNL Snowflake] es `jdbc:snowflake://{ACCOUNT_NAME}.snowflakecomputing.com/?user={USERNAME}&password={PASSWORD}&db={DATABASE}&warehouse={WAREHOUSE}`. |

Para obtener más información sobre estos valores, consulte [este documento del Snowflake](https://docs.snowflake.com/en/user-guide/oauth-custom.html).

## Conecte su cuenta de Snowflake

En la interfaz de usuario de Platform, seleccione **[!UICONTROL Sources]** en el panel de navegación izquierdo para acceder al espacio de trabajo [!UICONTROL Sources]. La pantalla [!UICONTROL Catalog] muestra una variedad de fuentes con las que puede crear una cuenta.

Puede seleccionar la categoría adecuada del catálogo en la parte izquierda de la pantalla. También puede encontrar la fuente específica con la que desea trabajar mediante la barra de búsqueda.

En la categoría [!UICONTROL Bases de datos], seleccione **[!UICONTROL Snowflake]** y, a continuación, seleccione **[!UICONTROL Agregar datos]**.

![](../../../../images/tutorials/create/snowflake/catalog.png)

Aparece la página **[!UICONTROL Connect to Snowflake]**. En esta página, puede usar credenciales nuevas o existentes.

### Cuenta existente

Para conectar una cuenta existente, seleccione la cuenta de Snowflake con la que desee conectarse y, a continuación, seleccione **[!UICONTROL Next]** para continuar.

![](../../../../images/tutorials/create/snowflake/existing.png)

### Nueva cuenta

Si está utilizando credenciales nuevas, seleccione **[!UICONTROL New account]**. En el formulario de entrada que aparece, indique un nombre, una descripción opcional y las credenciales del Snowflake. Cuando termine, seleccione **[!UICONTROL Connect]** y, a continuación, deje que se establezca la nueva conexión.

![](../../../../images/tutorials/create/snowflake/new.png)

## Pasos siguientes

Siguiendo este tutorial, ha establecido una conexión con su cuenta de Snowflake. Ahora puede continuar con el siguiente tutorial y [configurar un flujo de datos para introducir datos en [!DNL Platform]](../../dataflow/databases.md).
