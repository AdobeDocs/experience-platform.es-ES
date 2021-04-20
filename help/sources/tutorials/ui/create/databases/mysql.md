---
keywords: Experience Platform;inicio;temas populares;mysql;MySQL
solution: Experience Platform
title: Crear una conexión de origen MySQL en la interfaz de usuario
topic: overview
type: Tutorial
description: Aprenda a crear una conexión de origen MySQL utilizando la interfaz de usuario de Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: 8851e11e956b393e56714d4d48870b7f68947c18
workflow-type: tm+mt
source-wordcount: '404'
ht-degree: 1%

---


# Crear una conexión de origen [!DNL MySQL] en la interfaz de usuario

Los conectores de origen de Adobe Experience Platform permiten la ingesta de datos de origen externo de forma programada. Este tutorial proporciona los pasos para crear una conexión de origen [!DNL MySQL] mediante la interfaz de usuario de Adobe Experience Platform.

## Primeros pasos

Este tutorial requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): El marco estandarizado mediante el cual el Experience Platform organiza los datos de experiencia del cliente.
   * [Aspectos básicos de la composición](../../../../../xdm/schema/composition.md) del esquema: Obtenga información sobre los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   * [Tutorial del Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): Aprenda a crear esquemas personalizados mediante la interfaz de usuario del Editor de esquemas.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Proporciona un perfil de cliente unificado y en tiempo real basado en datos agregados de varias fuentes.

Si ya tiene una conexión [!DNL MySQL], puede omitir el resto de este documento y continuar con el tutorial sobre la [configuración de un flujo de datos](../../dataflow/databases.md).

### Recopilar las credenciales necesarias

Para acceder a su cuenta [!DNL MySQL] en [!DNL Platform], debe proporcionar el siguiente valor:

| Credencial | Descripción |
| ---------- | ----------- |
| `connectionString` | La cadena de conexión [!DNL MySQL] asociada a su cuenta. El patrón de cadena de conexión [!DNL MySQL] es: `Server={SERVER};Port={PORT};Database={DATABASE};UID={USERNAME};PWD={PASSWORD}`. Puede obtener más información sobre las cadenas de conexión y cómo obtenerlas leyendo el [[!DNL MySQL] documento](https://dev.mysql.com/doc/connector-net/en/connector-net-connections-string.html). |

## Conecte su cuenta [!DNL MySQL]

Una vez que haya reunido las credenciales necesarias, puede seguir los pasos a continuación para vincular su cuenta [!DNL MySQL] a [!DNL Platform].

Inicie sesión en [Adobe Experience Platform](https://platform.adobe.com) y, a continuación, seleccione **[!UICONTROL Sources]** en la barra de navegación izquierda para acceder al espacio de trabajo **[!UICONTROL Sources]**. La pantalla **[!UICONTROL Catalog]** muestra una variedad de fuentes para las que puede crear una cuenta.

En la categoría **[!UICONTROL Databases]**, seleccione **[!UICONTROL MySQL]**. Si es la primera vez que utiliza este conector, seleccione **[!UICONTROL Configure]**. De lo contrario, seleccione **[!UICONTROL Add data]** para crear un nuevo conector [!DNL MySQL].

![](../../../../images/tutorials/create/my-sql/catalog.png)

Aparece la página **[!UICONTROL Connect to MySQL]**. En esta página, puede usar credenciales nuevas o existentes.

### Nueva cuenta

Si está utilizando credenciales nuevas, seleccione **[!UICONTROL New account]**. En el formulario de entrada que aparece, indique un nombre, una descripción opcional y sus credenciales [!DNL MySQL]. Cuando termine, seleccione **[!UICONTROL Connect]** y, a continuación, deje que se establezca la nueva conexión.

![](../../../../images/tutorials/create/my-sql/new.png)

### Cuenta existente

Para conectar una cuenta existente, seleccione la cuenta [!DNL MySQL] con la que desea conectarse y, a continuación, seleccione **[!UICONTROL Next]** para continuar.

![](../../../../images/tutorials/create/my-sql/existing.png)

## Pasos siguientes

Siguiendo este tutorial, ha establecido una conexión con su cuenta MySQL. Ahora puede continuar con el siguiente tutorial y [configurar un flujo de datos para introducir datos en [!DNL Platform]](../../dataflow/databases.md).