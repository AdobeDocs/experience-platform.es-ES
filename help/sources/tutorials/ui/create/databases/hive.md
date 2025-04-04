---
keywords: Experience Platform;inicio;temas populares;Apache Hive;Azure HDInsights;azure hdinsights
solution: Experience Platform
title: Crear un Apache Hive en Azure HDInsights Source Connection en la interfaz de usuario
type: Tutorial
description: Obtenga información sobre cómo crear una conexión de origen de Apache Hive en Azure HDInsights mediante la interfaz de usuario de Adobe Experience Platform.
exl-id: 3eb3cb02-9867-451a-b847-ab895310eedf
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '479'
ht-degree: 2%

---

# Crear un(a) [!DNL Apache Hive] en la conexión de origen [!DNL Azure HDInsights] en la interfaz de usuario

>[!NOTE]
>
> El conector [!DNL Apache Hive] de [!DNL Azure HDInsights] está en versión beta. Consulte [Resumen de fuentes](../../../../home.md#terms-and-conditions) para obtener más información sobre el uso de conectores con etiqueta beta.

Los conectores de Source en Adobe Experience Platform permiten introducir datos de origen externo de forma programada. Este tutorial proporciona los pasos para crear un [!DNL Apache Hive] en el conector de origen [!DNL Azure HDInsights] mediante la interfaz de usuario [!DNL Experience Platform].

## Introducción

Este tutorial requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): El marco de trabajo estandarizado mediante el cual [!DNL Experience Platform] organiza los datos de la experiencia del cliente.
   * [Aspectos básicos de la composición de esquemas](../../../../../xdm/schema/composition.md): obtenga información sobre los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   * [Tutorial del editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): Aprenda a crear esquemas personalizados mediante la interfaz de usuario del editor de esquemas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): proporciona un perfil de consumidor unificado y en tiempo real basado en los datos agregados de varias fuentes.

Si ya tiene una conexión [!DNL Hive] válida, puede omitir el resto de este documento y continuar con el tutorial sobre [configuración de un flujo de datos](../../dataflow/databases.md)

### Recopilar credenciales necesarias

Para tener acceso a su cuenta de [!DNL Hive] en [!DNL Experience Platform], debe proporcionar los siguientes valores:

| Credencial | Descripción |
| ---------- | ----------- |
| `host` | La dirección IP o el nombre de host del servidor [!DNL Hive]. |
| `username` | Nombre de usuario que utiliza para obtener acceso al servidor [!DNL Hive]. |
| `password` | La contraseña que corresponde al usuario. |

Para obtener más información sobre cómo empezar, consulte [este [!DNL Hive] documento](https://cwiki.apache.org/confluence/display/Hive/Tutorial#Tutorial-GettingStarted).

## Conectar su cuenta de [!DNL Hive]

Una vez que haya recopilado las credenciales requeridas, puede seguir los pasos a continuación para vincular su cuenta de [!DNL Hive] a [!DNL Experience Platform].

Inicie sesión en [Adobe Experience Platform](https://platform.adobe.com) y, a continuación, seleccione **[!UICONTROL Fuentes]** en la barra de navegación izquierda para acceder al área de trabajo de **[!UICONTROL Fuentes]**. La pantalla **[!UICONTROL Catálogo]** muestra una variedad de orígenes con los que puede crear una cuenta.

Puede seleccionar la categoría adecuada del catálogo en la parte izquierda de la pantalla. También puede encontrar la fuente específica con la que desea trabajar utilizando la opción de búsqueda.

En la categoría **[!UICONTROL Bases de datos]**, seleccione **[!UICONTROL Hive]**. Si es la primera vez que usa este conector, seleccione **[!UICONTROL Configurar]**. De lo contrario, seleccione **[!UICONTROL Agregar datos]** para crear un nuevo conector [!DNL Hive].

![catálogo](../../../../images/tutorials/create/hive/catalog.png)

Aparecerá la página **[!UICONTROL Conectarse a Hive]**. En esta página, puede usar credenciales nuevas o existentes.

### Nueva cuenta

Si está usando credenciales nuevas, seleccione **[!UICONTROL Nueva cuenta]**. En el formulario de entrada que aparece, proporcione un nombre, una descripción opcional y sus credenciales de [!DNL Hive]. Cuando termine, seleccione **[!UICONTROL Conectar]** y deje pasar un tiempo para que se establezca la nueva conexión.

![conectar](../../../../images/tutorials/create/hive/new.png)

### Cuenta existente

Para conectar una cuenta existente, seleccione la cuenta de [!DNL Hive] con la que desee conectarse y, a continuación, seleccione **[!UICONTROL Siguiente]** para continuar.

![existente](../../../../images/tutorials/create/hive/existing.png)

## Pasos siguientes

Al seguir este tutorial, ha establecido una conexión con su cuenta de [!DNL Hive]. Ahora puede continuar con el siguiente tutorial y [configurar un flujo de datos para introducir datos en [!DNL Experience Platform]](../../dataflow/databases.md).
