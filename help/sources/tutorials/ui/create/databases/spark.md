---
keywords: Experience Platform;inicio;temas populares;Azure HDInsights;Apache Spark
solution: Experience Platform
title: Crear una conexión de origen de Apache Spark en Azure HDInsights en la interfaz de usuario
type: Tutorial
description: Obtenga información sobre cómo crear una conexión de origen de Apache Spark en Azure HDInsights mediante la interfaz de usuario de Adobe Experience Platform.
exl-id: 30d0b740-cec4-486f-9c9b-1579fd04f28b
source-git-commit: e37c00863249e677f1645266859bf40fe6451827
workflow-type: tm+mt
source-wordcount: '496'
ht-degree: 1%

---

# Crear un [!DNL Apache Spark] el [!DNL Azure HDInsights] conexión de origen en la interfaz de usuario

>[!NOTE]
>
> El [!DNL Apache Spark] el [!DNL Azure HDInsights] el conector está en versión beta. Consulte la [Resumen de orígenes](../../../../home.md#terms-and-conditions) para obtener más información sobre el uso de conectores etiquetados como beta.

Los conectores de origen en Adobe Experience Platform permiten introducir datos de origen externo de forma programada. Este tutorial proporciona los pasos para crear una [!DNL Apache Spark] el [!DNL Azure HDInsights] conector de origen mediante [!DNL Platform] interfaz de usuario.

## Introducción

Este tutorial requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [Sistema de modelo de datos de experiencia (XDM)](../../../../../xdm/home.md): El marco estandarizado mediante el cual Experience Platform organiza los datos de experiencia del cliente.
   * [Conceptos básicos de composición de esquemas](../../../../../xdm/schema/composition.md): Obtenga información acerca de los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   * [Tutorial del Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): Aprenda a crear esquemas personalizados mediante la interfaz de usuario del Editor de esquemas.
* [Perfil del cliente en tiempo real](../../../../../profile/home.md): Proporciona un perfil de consumidor unificado y en tiempo real basado en los datos agregados de varias fuentes.

Si ya tiene un válido [!DNL Spark] conexión, puede omitir el resto de este documento y continuar con el tutorial sobre [configuración de un flujo de datos](../../dataflow/databases.md)

### Recopilar credenciales necesarias

Para acceder a su [!DNL Spark] cuenta en [!DNL Platform], debe proporcionar los siguientes valores:

| Credencial | Descripción |
| ---------- | ----------- |
| `host` | La dirección IP o el nombre de host del [!DNL Spark] servidor. |
| `username` | El nombre de usuario que utiliza para acceder a [!DNL Spark] servidor. |
| `password` | La contraseña que corresponde al usuario. |

Para obtener más información sobre cómo empezar, consulte [este documento de Spark](https://docs.microsoft.com/en-us/azure/hdinsight/spark/apache-spark-overview).

## Conecte su [!DNL Spark] account

Una vez que haya recopilado las credenciales necesarias, puede seguir los pasos a continuación para vincular su [!DNL Spark] cuenta a la que conectarse [!DNL Platform].

Iniciar sesión en [Adobe Experience Platform](https://platform.adobe.com) y luego seleccione **[!UICONTROL Fuentes]** desde la barra de navegación izquierda para acceder a **[!UICONTROL Fuentes]** workspace. El **[!UICONTROL Catálogo]** La pantalla muestra una variedad de fuentes para las que puede crear una cuenta con.

Puede seleccionar la categoría adecuada del catálogo en la parte izquierda de la pantalla. También puede encontrar la fuente específica con la que desea trabajar utilizando la opción de búsqueda.

En el **[!UICONTROL Bases de datos]** categoría, seleccionar **[!UICONTROL Spark]**. Si es la primera vez que utiliza este conector, seleccione **[!UICONTROL Configurar]**. De lo contrario, seleccione **[!UICONTROL Añadir datos]** para crear una nueva [!DNL Spark] conector.

![catalogar](../../../../images/tutorials/create/spark/catalog.png)

El **[!UICONTROL Conectar con Spark]** página. En esta página, puede usar credenciales nuevas o existentes.

### Nueva cuenta

Si está usando credenciales nuevas, seleccione **[!UICONTROL Nueva cuenta]**. En el formulario de entrada que aparece, proporcione un nombre, una descripción opcional y su [!DNL Spark] credenciales. Cuando termine, seleccione **[!UICONTROL Connect]** y, a continuación, espere un poco para que se establezca la nueva conexión.

![nuevo](../../../../images/tutorials/create/spark/new.png)

### Cuenta existente

Para conectar una cuenta existente, seleccione la [!DNL Spark] cuenta con la que desea conectarse y, a continuación, seleccione **[!UICONTROL Siguiente]** para continuar.

![existente](../../../../images/tutorials/create/spark/existing.png)

## Pasos siguientes

Al seguir este tutorial, ha establecido una conexión con su [!DNL Spark] cuenta. Ahora puede continuar con el siguiente tutorial y [configuración de un flujo de datos para introducir datos en [!DNL Platform]](../../dataflow/databases.md).
