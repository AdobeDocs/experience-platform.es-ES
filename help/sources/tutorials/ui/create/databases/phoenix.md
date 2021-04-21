---
keywords: Experience Platform;inicio;temas populares;Phoenix;phoenix
solution: Experience Platform
title: Crear una conexión de origen de Phoenix en la interfaz de usuario
topic-legacy: overview
type: Tutorial
description: Aprenda a crear una conexión de origen de Phoenix utilizando la interfaz de usuario de Adobe Experience Platform.
exl-id: 2ed469bc-1c72-4f04-a5f0-6a0bb519a6c2
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '505'
ht-degree: 0%

---

# Crear una conexión de origen [!DNL Phoenix] en la interfaz de usuario

>[!NOTE]
>
> El conector [!DNL Phoenix] está en versión beta. Consulte la [información general sobre fuentes](../../../../home.md#terms-and-conditions) para obtener más información sobre el uso de conectores con etiqueta beta.

Los conectores de origen de Adobe Experience Platform permiten la ingesta de datos de origen externo de forma programada. Este tutorial proporciona los pasos para crear un conector de origen [!DNL Phoenix] mediante la interfaz de usuario [!DNL Platform].

## Primeros pasos

Este tutorial requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): El marco estandarizado mediante el cual se  [!DNL Experience Platform] organizan los datos de experiencia del cliente.
   * [Aspectos básicos de la composición](../../../../../xdm/schema/composition.md) del esquema: Obtenga información sobre los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   * [Tutorial del Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): Aprenda a crear esquemas personalizados mediante la interfaz de usuario del Editor de esquemas.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Proporciona un perfil de cliente unificado y en tiempo real basado en datos agregados de varias fuentes.

Si ya tiene una conexión [!DNL Phoenix] válida, puede omitir el resto de este documento y continuar con el tutorial sobre la [configuración de un flujo de datos](../../dataflow/databases.md)

### Recopilar las credenciales necesarias

Para acceder a su cuenta [!DNL Phoenix] en [!DNL Platform], debe proporcionar los siguientes valores:

| Credencial | Descripción |
| ---------- | ----------- |
| `host` | La dirección IP o el nombre de host del servidor [!DNL Phoenix]. |
| `port` | Puerto TCP que utiliza el servidor [!DNL Phoenix] para detectar conexiones de cliente. Si se conecta a [!DNL Azure HDInsights], especifique el puerto como 443. |
| `httpPath` | La URL parcial correspondiente al servidor [!DNL Phoenix]. Especifique /basephoenix0 si está utilizando el clúster [!DNL Azure HDInsights]. |
| `username` | El nombre de usuario que utiliza para acceder al servidor [!DNL Phoenix]. |
| `password` | La contraseña que corresponde al usuario. |
| `enableSsl` | Un conmutador que especifica si las conexiones al servidor se cifran mediante SSL. |

Para obtener más información sobre cómo empezar, consulte [este [!DNL Phoenix] documento](https://python-phoenixdb.readthedocs.io/en/latest/api.html).

## Conecte su cuenta [!DNL Phoenix]

Una vez que haya reunido las credenciales necesarias, puede seguir los pasos a continuación para vincular su cuenta [!DNL Phoenix] para conectarse a [!DNL Platform].

Inicie sesión en [Adobe Experience Platform](https://platform.adobe.com) y, a continuación, seleccione **[!UICONTROL Sources]** en la barra de navegación izquierda para acceder al espacio de trabajo **[!UICONTROL Sources]**. La pantalla **[!UICONTROL Catalog]** muestra una variedad de fuentes para las que puede crear una cuenta.

Puede seleccionar la categoría adecuada del catálogo en la parte izquierda de la pantalla. Alternativamente, puede encontrar la fuente específica con la que desea trabajar usando la opción de búsqueda.

En la categoría **[!UICONTROL Databases]**, seleccione **[!UICONTROL Phoenix]**. Si es la primera vez que utiliza este conector, seleccione **[!UICONTROL Configure]**. De lo contrario, seleccione **[!UICONTROL Add data]** para crear una nueva cuenta [!DNL Phoenix].

![catálogo](../../../../images/tutorials/create/phoenix/catalog.png)

Aparece la página **[!UICONTROL Connect to Phoenix]**. En esta página, puede usar credenciales nuevas o existentes.

### Nueva cuenta

Si está utilizando credenciales nuevas, seleccione **[!UICONTROL New account]**. En el formulario de entrada que aparece, indique un nombre, una descripción opcional y sus credenciales [!DNL Phoenix]. Cuando termine, seleccione **[!UICONTROL Connect]** y, a continuación, deje que se establezca la nueva conexión.

![connect](../../../../images/tutorials/create/phoenix/new.png)

### Cuenta existente

Para conectar una cuenta existente, seleccione la cuenta [!DNL Phoenix] con la que desea conectarse y, a continuación, seleccione **[!UICONTROL Next]** para continuar.

![existente](../../../../images/tutorials/create/phoenix/existing.png)

## Pasos siguientes

Al seguir este tutorial, ha establecido una conexión con su cuenta [!DNL Phoenix]. Ahora puede continuar con el siguiente tutorial y [configurar un flujo de datos para introducir datos en [!DNL Platform]](../../dataflow/databases.md).
