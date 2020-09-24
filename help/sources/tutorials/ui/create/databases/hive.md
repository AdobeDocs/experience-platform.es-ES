---
keywords: Experience Platform;home;popular topics;Apache Hive;Azure HDInsights;azure hdinsights
solution: Experience Platform
title: Creación de un Apache Hive en el conector de origen de Azure HDInsights en la interfaz de usuario
topic: overview
type: Tutorial
description: Este tutorial proporciona los pasos para crear un Apache Hive en el conector de origen de Azure HDInsights mediante la interfaz de usuario de la plataforma.
translation-type: tm+mt
source-git-commit: 97dfd3a9a66fe2ae82cec8954066bdf3b6346830
workflow-type: tm+mt
source-wordcount: '481'
ht-degree: 1%

---


# Creación de un [!DNL Apache Hive] conector de origen [!DNL Azure HDInsights] en la interfaz de usuario

>[!NOTE]
>
> El [!DNL Apache Hive] conector on [!DNL Azure HDInsights] está en versión beta. Consulte la descripción general [de](../../../../home.md#terms-and-conditions) Fuentes para obtener más información sobre el uso de conectores con etiquetas beta.

Los conectores de origen de Adobe Experience Platform permiten la ingesta de datos externos de forma programada. Este tutorial proporciona los pasos para crear un conector [!DNL Apache Hive] en [!DNL Azure HDInsights] origen mediante la interfaz [!DNL Platform] de usuario.

## Primeros pasos

Este tutorial requiere un conocimiento práctico de los siguientes componentes de Adobe Experience Platform:

* [[!DNL Experience Data Model] (XDM) Sistema](../../../../../xdm/home.md): El marco normalizado por el cual [!DNL Experience Platform] organiza los datos de experiencia del cliente.
   * [Conceptos básicos de la composición](../../../../../xdm/schema/composition.md)de esquemas: Obtenga información sobre los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   * [Tutorial](../../../../../xdm/tutorials/create-schema-ui.md)del Editor de esquemas: Obtenga información sobre cómo crear esquemas personalizados mediante la interfaz de usuario del Editor de Esquemas.
* [[!Perfil del cliente en tiempo real de DNL]](../../../../../profile/home.md): Proporciona un perfil de consumo unificado y en tiempo real basado en datos agregados de varias fuentes.

Si ya tiene una conexión válida, puede omitir el resto de este documento y continuar con el tutorial sobre la [!DNL Hive] [configuración de un flujo de datos](../../dataflow/databases.md)

### Recopilar las credenciales necesarias

Para acceder a su [!DNL Hive] cuenta en [!DNL Platform], debe proporcionar los siguientes valores:

| Credencial | Descripción |
| ---------- | ----------- |
| `host` | La dirección IP o el nombre de host del [!DNL Hive] servidor. |
| `username` | El nombre de usuario que utiliza para acceder al [!DNL Hive] servidor. |
| `password` | La contraseña que corresponde al usuario. |

Para obtener más información sobre cómo empezar, consulte [ [!DNL Hive] este documento](https://cwiki.apache.org/confluence/display/Hive/Tutorial#Tutorial-GettingStarted).

## Conectar su [!DNL Hive] cuenta

Una vez recopiladas las credenciales necesarias, puede seguir los pasos a continuación para vincular su [!DNL Hive] cuenta a [!DNL Platform].

Inicie sesión en [Adobe Experience Platform](https://platform.adobe.com) y seleccione **[!UICONTROL Fuentes]** en la barra de navegación izquierda para acceder al espacio de trabajo **[!UICONTROL Fuentes]** . La pantalla **[!UICONTROL Catálogo]** muestra una serie de orígenes con los que puede crear una cuenta.

Puede seleccionar la categoría adecuada en el catálogo a la izquierda de la pantalla. También puede encontrar la fuente específica con la que desea trabajar mediante la opción de búsqueda.

En la categoría **[!UICONTROL Bases de datos]** , seleccione **[!UICONTROL Hive]**. Si es la primera vez que utiliza este conector, seleccione **[!UICONTROL Configurar]**. De lo contrario, seleccione **[!UICONTROL Añadir datos]** para crear un nuevo [!DNL Hive] conector.

![catálogo](../../../../images/tutorials/create/hive/catalog.png)

Aparece la página **[!UICONTROL Conectar con Hive]** . En esta página, puede usar credenciales nuevas o existentes.

### Nueva cuenta

Si está utilizando nuevas credenciales, seleccione **[!UICONTROL Nueva cuenta]**. En el formulario de entrada que aparece, especifique un nombre, una descripción opcional y sus [!DNL Hive] credenciales. Cuando termine, seleccione **[!UICONTROL Connect]** y, a continuación, espere un poco de tiempo para que se establezca la nueva conexión.

![connect](../../../../images/tutorials/create/hive/new.png)

### Cuenta existente

Para conectar una cuenta existente, seleccione la [!DNL Hive] cuenta con la que desea conectarse y, a continuación, seleccione **[!UICONTROL Siguiente]** para continuar.

![existente](../../../../images/tutorials/create/hive/existing.png)

## Pasos siguientes

Siguiendo este tutorial, ha establecido una conexión con su [!DNL Hive] cuenta. Ahora puede continuar con el siguiente tutorial y [configurar un flujo de datos para incluir [!DNL Platform]](../../dataflow/databases.md)datos.