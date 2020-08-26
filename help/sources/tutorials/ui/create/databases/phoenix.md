---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Creación de un conector de origen Phoenix en la interfaz de usuario
topic: overview
translation-type: tm+mt
source-git-commit: 690ddbd92f0a2e4e06b988e761dabff399cd2367
workflow-type: tm+mt
source-wordcount: '504'
ht-degree: 0%

---


# Creación de un conector [!DNL Phoenix] de origen en la interfaz de usuario

>[!NOTE]
>
> El [!DNL Phoenix] conector está en versión beta. Consulte la descripción general [de](../../../../home.md#terms-and-conditions) Fuentes para obtener más información sobre el uso de conectores con etiquetas beta.

Los conectores de origen de Adobe Experience Platform permiten la ingesta de datos externos de forma programada. Este tutorial proporciona los pasos para crear un conector de [!DNL Phoenix] origen mediante la interfaz [!DNL Platform] de usuario.

## Primeros pasos

Este tutorial requiere un conocimiento práctico de los siguientes componentes de Adobe Experience Platform:

* [[!DNL Experience Data Model] (XDM) Sistema](../../../../../xdm/home.md): El marco normalizado por el cual [!DNL Experience Platform] organiza los datos de experiencia del cliente.
   * [Conceptos básicos de la composición](../../../../../xdm/schema/composition.md)de esquemas: Obtenga información sobre los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   * [Tutorial](../../../../../xdm/tutorials/create-schema-ui.md)del Editor de esquemas: Obtenga información sobre cómo crear esquemas personalizados mediante la interfaz de usuario del Editor de Esquemas.
* [[!Perfil del cliente en tiempo real de DNL]](../../../../../profile/home.md): Proporciona un perfil de consumo unificado y en tiempo real basado en datos agregados de varias fuentes.

Si ya tiene una conexión válida, puede omitir el resto de este documento y continuar con el tutorial sobre la [!DNL Phoenix] [configuración de un flujo de datos](../../dataflow/databases.md)

### Recopilar las credenciales necesarias

Para acceder a su [!DNL Phoenix] cuenta en [!DNL Platform], debe proporcionar los siguientes valores:

| Credencial | Descripción |
| ---------- | ----------- |
| `host` | La dirección IP o el nombre de host del [!DNL Phoenix] servidor. |
| `port` | El puerto TCP que utiliza el [!DNL Phoenix] servidor para detectar conexiones de cliente. Si se conecta a [!DNL Azure HDInsights], especifique el puerto como 443. |
| `httpPath` | La URL parcial correspondiente al [!DNL Phoenix] servidor. Especifique /hbasephoenix0 si está utilizando el [!DNL Azure HDInsights] clúster. |
| `username` | El nombre de usuario que utiliza para acceder al [!DNL Phoenix] servidor. |
| `password` | La contraseña que corresponde al usuario. |
| `enableSsl` | Un conmutador que especifica si las conexiones al servidor se cifran mediante SSL. |

Para obtener más información sobre cómo empezar, consulte [ [!DNL Phoenix] este documento](https://python-phoenixdb.readthedocs.io/en/latest/api.html).

## Conectar su [!DNL Phoenix] cuenta

Una vez que haya recopilado las credenciales necesarias, puede seguir los pasos a continuación para vincular su [!DNL Phoenix] cuenta a [!DNL Platform].

Inicie sesión en [Adobe Experience Platform](https://platform.adobe.com) y seleccione **[!UICONTROL Fuentes]** en la barra de navegación izquierda para acceder al espacio de trabajo **[!UICONTROL Fuentes]** . La pantalla **[!UICONTROL Catálogo]** muestra una serie de orígenes con los que puede crear una cuenta.

Puede seleccionar la categoría adecuada en el catálogo a la izquierda de la pantalla. También puede encontrar la fuente específica con la que desea trabajar mediante la opción de búsqueda.

En la categoría **[!UICONTROL Bases]** de datos, seleccione **[!UICONTROL Fénix]**. Si es la primera vez que utiliza este conector, seleccione **[!UICONTROL Configurar]**. De lo contrario, seleccione **[!UICONTROL Añadir datos]** para crear una nueva [!DNL Phoenix] cuenta.

![catálogo](../../../../images/tutorials/create/phoenix/catalog.png)

Aparece la página **[!UICONTROL Conectar con Phoenix]** . En esta página, puede usar credenciales nuevas o existentes.

### Nueva cuenta

Si está utilizando nuevas credenciales, seleccione **[!UICONTROL Nueva cuenta]**. En el formulario de entrada que aparece, especifique un nombre, una descripción opcional y sus [!DNL Phoenix] credenciales. Cuando termine, seleccione **[!UICONTROL Connect]** y, a continuación, espere un poco de tiempo para que se establezca la nueva conexión.

![connect](../../../../images/tutorials/create/phoenix/new.png)

### Cuenta existente

Para conectar una cuenta existente, seleccione la [!DNL Phoenix] cuenta con la que desea conectarse y, a continuación, seleccione **[!UICONTROL Siguiente]** para continuar.

![existente](../../../../images/tutorials/create/phoenix/existing.png)

## Pasos siguientes

Siguiendo este tutorial, ha establecido una conexión con su [!DNL Phoenix] cuenta. Ahora puede continuar con el siguiente tutorial y [configurar un flujo de datos para incluir [!DNL Platform]](../../dataflow/databases.md)datos.