---
keywords: Experience Platform;inicio;temas populares;Azure HDInsights;Apache Spark
solution: Experience Platform
title: Creación de una conexión de Apache Spark en Azure HDInsights Source en la interfaz de usuario
type: Tutorial
description: Obtenga información sobre cómo crear una conexión de origen de Apache Spark en Azure HDInsights mediante la interfaz de usuario de Adobe Experience Platform.
exl-id: 30d0b740-cec4-486f-9c9b-1579fd04f28b
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '489'
ht-degree: 2%

---

# Crear un(a) [!DNL Apache Spark] en la conexión de origen [!DNL Azure HDInsights] en la interfaz de usuario

>[!NOTE]
>
> El conector [!DNL Apache Spark] de [!DNL Azure HDInsights] está en versión beta. Consulte [Resumen de fuentes](../../../../home.md#terms-and-conditions) para obtener más información sobre el uso de conectores con etiqueta beta.

Los conectores de Source en Adobe Experience Platform permiten introducir datos de origen externo de forma programada. Este tutorial proporciona los pasos para crear un [!DNL Apache Spark] en el conector de origen [!DNL Azure HDInsights] mediante la interfaz de usuario [!DNL Experience Platform].

## Introducción

Este tutorial requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* Sistema [Experience Data Model (XDM)](../../../../../xdm/home.md): El marco de trabajo estandarizado mediante el cual Experience Platform organiza los datos de experiencia del cliente.
   * [Aspectos básicos de la composición de esquemas](../../../../../xdm/schema/composition.md): obtenga información sobre los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   * [Tutorial del editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): Aprenda a crear esquemas personalizados mediante la interfaz de usuario del editor de esquemas.
* [Perfil del cliente en tiempo real](../../../../../profile/home.md): Proporciona un perfil de consumidor unificado en tiempo real basado en datos agregados de múltiples fuentes.

Si ya tiene una conexión [!DNL Spark] válida, puede omitir el resto de este documento y continuar con el tutorial sobre [configuración de un flujo de datos](../../dataflow/databases.md)

### Recopilar credenciales necesarias

Para tener acceso a su cuenta de [!DNL Spark] en [!DNL Experience Platform], debe proporcionar los siguientes valores:

| Credencial | Descripción |
| ---------- | ----------- |
| `host` | La dirección IP o el nombre de host del servidor [!DNL Spark]. |
| `username` | Nombre de usuario que utiliza para obtener acceso al servidor [!DNL Spark]. |
| `password` | La contraseña que corresponde al usuario. |

Para obtener más información sobre cómo empezar, consulte [este documento de Spark](https://docs.microsoft.com/en-us/azure/hdinsight/spark/apache-spark-overview).

## Conectar su cuenta de [!DNL Spark]

Una vez que haya recopilado las credenciales requeridas, puede seguir los pasos a continuación para vincular su cuenta de [!DNL Spark] y conectarse a [!DNL Experience Platform].

Inicie sesión en [Adobe Experience Platform](https://platform.adobe.com) y, a continuación, seleccione **[!UICONTROL Fuentes]** en la barra de navegación izquierda para acceder al área de trabajo de **[!UICONTROL Fuentes]**. La pantalla **[!UICONTROL Catálogo]** muestra una variedad de orígenes con los que puede crear una cuenta.

Puede seleccionar la categoría adecuada del catálogo en la parte izquierda de la pantalla. También puede encontrar la fuente específica con la que desea trabajar utilizando la opción de búsqueda.

En la categoría **[!UICONTROL Bases de datos]**, seleccione **[!UICONTROL Spark]**. Si es la primera vez que usa este conector, seleccione **[!UICONTROL Configurar]**. De lo contrario, seleccione **[!UICONTROL Agregar datos]** para crear un nuevo conector [!DNL Spark].

![catálogo](../../../../images/tutorials/create/spark/catalog.png)

Aparecerá la página **[!UICONTROL Conectar con Spark]**. En esta página, puede usar credenciales nuevas o existentes.

### Nueva cuenta

Si está usando credenciales nuevas, seleccione **[!UICONTROL Nueva cuenta]**. En el formulario de entrada que aparece, proporcione un nombre, una descripción opcional y sus credenciales de [!DNL Spark]. Cuando termine, seleccione **[!UICONTROL Conectar]** y deje pasar un tiempo para que se establezca la nueva conexión.

![nuevo](../../../../images/tutorials/create/spark/new.png)

### Cuenta existente

Para conectar una cuenta existente, seleccione la cuenta de [!DNL Spark] con la que desee conectarse y, a continuación, seleccione **[!UICONTROL Siguiente]** para continuar.

![existente](../../../../images/tutorials/create/spark/existing.png)

## Pasos siguientes

Al seguir este tutorial, ha establecido una conexión con su cuenta de [!DNL Spark]. Ahora puede continuar con el siguiente tutorial y [configurar un flujo de datos para introducir datos en [!DNL Experience Platform]](../../dataflow/databases.md).
