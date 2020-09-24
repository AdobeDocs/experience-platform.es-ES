---
keywords: Experience Platform;home;popular topics;Amazon Kinesis;amazon kinesis;Kinesis;kinesis
solution: Experience Platform
title: Creación de un conector de origen de Amazon Kinesis en la interfaz de usuario
topic: overview
type: Tutorial
description: Este tutorial proporciona los pasos para autenticar un conector de origen de Amazon Kinesis (en adelante, "Kinesis") mediante la interfaz de usuario de la plataforma.
translation-type: tm+mt
source-git-commit: 97dfd3a9a66fe2ae82cec8954066bdf3b6346830
workflow-type: tm+mt
source-wordcount: '482'
ht-degree: 1%

---


# Creación de un conector [!DNL Amazon Kinesis] de origen en la interfaz de usuario

>[!NOTE]
>
>El [!DNL Amazon Kinesis] conector está en versión beta. Consulte la descripción general [de](../../../../home.md#terms-and-conditions) Fuentes para obtener más información sobre el uso de conectores con etiquetas beta.

Los conectores de origen de Adobe Experience Platform permiten la ingesta de datos externos de forma programada. Este tutorial proporciona los pasos para autenticar un conector de origen [!DNL Amazon Kinesis] (en lo sucesivo, [!DNL "Kinesis"]) mediante la interfaz [!DNL Platform] de usuario.

## Primeros pasos

Este tutorial requiere un conocimiento práctico de los siguientes componentes de Adobe Experience Platform:

- [[!DNL Experience Data Model] (XDM) Sistema](../../../../../xdm/home.md): El marco normalizado por el cual [!DNL Experience Platform] organiza los datos de experiencia del cliente.
   - [Conceptos básicos de la composición](../../../../../xdm/schema/composition.md)de esquemas: Obtenga información sobre los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   - [Tutorial](../../../../../xdm/tutorials/create-schema-ui.md)del Editor de esquemas: Obtenga información sobre cómo crear esquemas personalizados mediante la interfaz de usuario del Editor de Esquemas.
- [[!Perfil del cliente en tiempo real de DNL]](../../../../../profile/home.md): Proporciona un perfil de consumo unificado y en tiempo real basado en datos agregados de varias fuentes.

Si ya tiene una conexión válida, puede omitir el resto de este documento y continuar con el tutorial sobre la [!DNL Kinesis] configuración de un flujo de datos [](../../dataflow/streaming/cloud-storage-streaming.md).

### Recopilar las credenciales necesarias

Para autenticar el conector [!DNL Kinesis] de origen, debe proporcionar valores para las siguientes propiedades de conexión:

| Credencial | Descripción |
| ---------- | ----------- |
| `accessKeyId` | ID de la clave de acceso de su [!DNL Kinesis] cuenta. |
| `Secret access key` | Clave de acceso secreta de su [!DNL Kinesis] cuenta. |
| `region` | Región del servidor de AWS. |

Para obtener más información sobre estos valores, consulte [ [!DNL Kinesis] este documento](https://docs.aws.amazon.com/streams/latest/dev/getting-started.html).

## Conectar su [!DNL Kinesis] cuenta

Una vez recopiladas las credenciales necesarias, puede seguir los pasos a continuación para vincular su [!DNL Kinesis] cuenta a [!DNL Platform].

Inicie sesión en [Adobe Experience Platform](https://platform.adobe.com) y seleccione **[!UICONTROL Fuentes]** en la barra de navegación izquierda para acceder al espacio de trabajo **[!UICONTROL Fuentes]** . La pantalla **[!UICONTROL Catálogo]** muestra una serie de orígenes con los que puede crear una cuenta.

Puede seleccionar la categoría adecuada en el catálogo a la izquierda de la pantalla. También puede encontrar la fuente específica con la que desea trabajar mediante la opción de búsqueda.

En la categoría **[!UICONTROL Cloud Almacenamiento]** , seleccione **[!UICONTROL Amazon Kinesis]**. Si es la primera vez que utiliza este conector, seleccione **[!UICONTROL Configurar]**. De lo contrario, seleccione **[!UICONTROL Añadir datos]** para crear un nuevo [!DNL Kinesis] conector.

![](../../../../images/tutorials/create/kinesis/catalog.png)

Aparecerá el cuadro de diálogo **[!UICONTROL Conectar a Amazon Kinesis]** . En esta página, puede usar credenciales nuevas o existentes.

### Nueva cuenta

Si está utilizando nuevas credenciales, seleccione **[!UICONTROL Nueva cuenta]**. En el formulario de entrada que aparece, especifique un nombre, una descripción opcional y sus [!DNL Kinesis] credenciales. Cuando termine, seleccione **[!UICONTROL Connect]** y, a continuación, espere un poco de tiempo para que se establezca la nueva conexión.

![](../../../../images/tutorials/create/kinesis/new.png)

### Cuenta existente

Para conectar una cuenta existente, seleccione la [!DNL Kinesis] cuenta con la que desea conectarse y, a continuación, seleccione **[!UICONTROL Siguiente]** para continuar.

![](../../../../images/tutorials/create/kinesis/existing.png)

## Pasos siguientes

Siguiendo este tutorial, se ha conectado a su [!DNL Kinesis] cuenta a [!DNL Platform]. Ahora puede continuar con el siguiente tutorial y [configurar un flujo de datos para traer datos del almacenamiento de nube a [!DNL Platform]](../../dataflow/streaming/cloud-storage-streaming.md).