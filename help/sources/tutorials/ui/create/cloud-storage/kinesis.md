---
keywords: Experience Platform;inicio;temas populares;Amazon Kinesis;amazon kinesis;Kinesis;kinesis
solution: Experience Platform
title: Crear una conexión de origen de Amazon Kinesis en la interfaz de usuario
topic-legacy: overview
type: Tutorial
description: Obtenga información sobre cómo crear una conexión de origen de Amazon Kinesis mediante la interfaz de usuario de Adobe Experience Platform.
exl-id: 4152e48b-bec7-4b05-a172-eea71c9d9880
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '464'
ht-degree: 1%

---

# Crear una conexión de origen [!DNL Amazon Kinesis] en la interfaz de usuario

>[!NOTE]
>
>El conector [!DNL Amazon Kinesis] está en versión beta. Consulte la [información general sobre fuentes](../../../../home.md#terms-and-conditions) para obtener más información sobre el uso de conectores con etiqueta beta.

Los conectores de origen de Adobe Experience Platform permiten la ingesta de datos de origen externo de forma programada. Este tutorial proporciona pasos para autenticar un conector de origen [!DNL Amazon Kinesis] (en adelante denominado [!DNL "Kinesis"]) mediante la interfaz de usuario [!DNL Platform].

## Primeros pasos

Este tutorial requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

- [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): El marco estandarizado mediante el cual se  [!DNL Experience Platform] organizan los datos de experiencia del cliente.
   - [Aspectos básicos de la composición](../../../../../xdm/schema/composition.md) del esquema: Obtenga información sobre los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   - [Tutorial del Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): Aprenda a crear esquemas personalizados mediante la interfaz de usuario del Editor de esquemas.
- [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Proporciona un perfil de cliente unificado y en tiempo real basado en datos agregados de varias fuentes.

Si ya tiene una conexión [!DNL Kinesis] válida, puede omitir el resto de este documento y continuar con el tutorial sobre la [configuración de un flujo de datos](../../dataflow/streaming/cloud-storage-streaming.md).

### Recopilar las credenciales necesarias

Para autenticar el conector de origen [!DNL Kinesis], debe proporcionar valores para las siguientes propiedades de conexión:

| Credencial | Descripción |
| ---------- | ----------- |
| `accessKeyId` | El ID de clave de acceso para su cuenta [!DNL Kinesis]. |
| `Secret access key` | La clave de acceso secreta para su cuenta [!DNL Kinesis]. |
| `region` | Región del servidor AWS. |

Para obtener más información sobre estos valores, consulte [this [!DNL Kinesis] document](https://docs.aws.amazon.com/streams/latest/dev/getting-started.html).

## Conecte su cuenta [!DNL Kinesis]

Una vez que haya reunido las credenciales necesarias, puede seguir los pasos a continuación para vincular su cuenta [!DNL Kinesis] a [!DNL Platform].

Inicie sesión en [Adobe Experience Platform](https://platform.adobe.com) y, a continuación, seleccione **[!UICONTROL Sources]** en la barra de navegación izquierda para acceder al espacio de trabajo **[!UICONTROL Sources]**. La pantalla **[!UICONTROL Catalog]** muestra una variedad de fuentes para las que puede crear una cuenta.

Puede seleccionar la categoría adecuada del catálogo en la parte izquierda de la pantalla. Alternativamente, puede encontrar la fuente específica con la que desea trabajar usando la opción de búsqueda.

En la categoría **[!UICONTROL Cloud Storage]**, seleccione **[!UICONTROL Amazon Kinesis]**. Si es la primera vez que utiliza este conector, seleccione **[!UICONTROL Configure]**. De lo contrario, seleccione **[!UICONTROL Add data]** para crear un nuevo conector [!DNL Kinesis].

![](../../../../images/tutorials/create/kinesis/catalog.png)

Aparece el cuadro de diálogo **[!UICONTROL Connect to Amazon Kinesis]**. En esta página, puede usar credenciales nuevas o existentes.

### Nueva cuenta

Si está utilizando credenciales nuevas, seleccione **[!UICONTROL New Account]**. En el formulario de entrada que aparece, indique un nombre, una descripción opcional y sus credenciales [!DNL Kinesis]. Cuando termine, seleccione **[!UICONTROL Connect]** y, a continuación, deje que se establezca la nueva conexión.

![](../../../../images/tutorials/create/kinesis/new.png)

### Cuenta existente

Para conectar una cuenta existente, seleccione la cuenta [!DNL Kinesis] con la que desea conectarse y, a continuación, seleccione **[!UICONTROL Next]** para continuar.

![](../../../../images/tutorials/create/kinesis/existing.png)

## Pasos siguientes

Al seguir este tutorial, se ha conectado a su cuenta [!DNL Kinesis] a [!DNL Platform]. Ahora puede continuar con el siguiente tutorial y [configurar un flujo de datos para incorporar datos del almacenamiento en la nube a [!DNL Platform]](../../dataflow/streaming/cloud-storage-streaming.md).
