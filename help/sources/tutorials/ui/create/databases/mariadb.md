---
keywords: Experience Platform;inicio;temas populares;Maria DB;maria db
solution: Experience Platform
title: Crear una conexión de origen de MariaDB en la interfaz de usuario
topic-legacy: overview
type: Tutorial
description: Aprenda a crear una conexión de origen de Maria DB mediante la interfaz de usuario de Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '415'
ht-degree: 1%

---


# Crear una conexión de origen [!DNL MariaDB] en la interfaz de usuario

>[!NOTE]
>
> El conector [!DNL MariaDB] está en versión beta. Consulte la [información general sobre fuentes](../../../../home.md#terms-and-conditions) para obtener más información sobre el uso de conectores con etiqueta beta.

Los conectores de origen de Adobe Experience Platform permiten la ingesta de datos de origen externo de forma programada. Este tutorial proporciona los pasos para crear un conector de origen de Maria DB utilizando la interfaz de usuario [!DNL Platform].

## Primeros pasos

Este tutorial requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): El marco estandarizado mediante el cual se  [!DNL Experience Platform] organizan los datos de experiencia del cliente.
   * [Aspectos básicos de la composición](../../../../../xdm/schema/composition.md) del esquema: Obtenga información sobre los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   * [Tutorial del Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): Aprenda a crear esquemas personalizados mediante la interfaz de usuario del Editor de esquemas.
* [Perfil](../../../../../profile/home.md) del cliente en tiempo real: Proporciona un perfil de cliente unificado y en tiempo real basado en datos agregados de varias fuentes.

Si ya tiene una conexión [!DNL MariaDB], puede omitir el resto de este documento y continuar con el tutorial sobre la [configuración de un flujo de datos](../../dataflow/databases.md).

### Recopilar las credenciales necesarias

Para acceder a su cuenta [!DNL MariaDB] en [!DNL Platform], debe proporcionar el siguiente valor:

| Credencial | Descripción |
| ---------- | ----------- |
| `connectionString` | La cadena de conexión asociada con la autenticación de MariaDB. El patrón de cadena de conexión [!DNL MariaDB] es: `Server={HOST};Port={PORT};Database={DATABASE};UID={USERNAME};PWD={PASSWORD}`. |

Para obtener más información sobre cómo empezar, consulte este [[!DNL MariaDB] documento](https://mariadb.com/kb/en/about-mariadb-connector-odbc/).

## Conecte su cuenta [!DNL Maria DB]

Una vez que haya reunido las credenciales necesarias, puede seguir los pasos a continuación para vincular su cuenta [!DNL Maria DB] a [!DNL Platform].

Inicie sesión en [Adobe Experience Platform](https://platform.adobe.com) y, a continuación, seleccione **[!UICONTROL Sources]** en la barra de navegación izquierda para acceder al espacio de trabajo **[!UICONTROL Sources]**. La pantalla **[!UICONTROL Catalog]** muestra una variedad de fuentes para las que puede crear una cuenta.

En la categoría **[!UICONTROL Databases]**, seleccione **[!UICONTROL Maria DB]**. Si es la primera vez que utiliza este conector, seleccione **[!UICONTROL Configure]**. De lo contrario, seleccione **[!UICONTROL Add data]** para crear un nuevo conector [!DNL Maria DB].

![](../../../../images/tutorials/create/maria-db/catalog.png)

Aparece la página **[!UICONTROL Connect to Maria DB]**. En esta página, puede usar credenciales nuevas o existentes.

### Nueva cuenta

Si está utilizando credenciales nuevas, seleccione **[!UICONTROL New account]**. En el formulario de entrada que aparece, indique un nombre, una descripción opcional y sus credenciales [!DNL MariaDB]. Cuando termine, seleccione **[!UICONTROL Connect]** y, a continuación, deje que se establezca la nueva conexión.

![](../../../../images/tutorials/create/maria-db/new.png)

### Cuenta existente

Para conectar una cuenta existente, seleccione la cuenta [!DNL MariaDB] con la que desea conectarse y, a continuación, seleccione **[!UICONTROL Next]** para continuar.

![](../../../../images/tutorials/create/maria-db/existing.png)

## Pasos siguientes

Al seguir este tutorial, ha establecido una conexión con su cuenta [!DNL MariaDB]. Ahora puede continuar con el siguiente tutorial y [configurar un flujo de datos para introducir datos en [!DNL Platform]](../../dataflow/databases.md).