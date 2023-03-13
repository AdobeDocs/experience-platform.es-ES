---
keywords: Experience Platform;inicio;temas populares;Amazon Kinesis;amazon kinesis;Kinesis;kinesis
solution: Experience Platform
title: Creación de una conexión de origen de Amazon Kinesis en la IU
type: Tutorial
description: Obtenga información sobre cómo crear una conexión de origen de Amazon Kinesis mediante la interfaz de usuario de Adobe Experience Platform.
exl-id: 4152e48b-bec7-4b05-a172-eea71c9d9880
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '466'
ht-degree: 1%

---

# Crear un [!DNL Amazon Kinesis] conexión de origen en la interfaz de usuario

Los conectores de origen en Adobe Experience Platform permiten introducir datos de origen externo de forma programada. Este tutorial proporciona los pasos para autenticar un [!DNL Amazon Kinesis] (en lo sucesivo denominados [!DNL "Kinesis"]) conector de origen utilizando [!DNL Platform] interfaz de usuario.

## Primeros pasos

Este tutorial requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

- [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): El marco estandarizado mediante el cual [!DNL Experience Platform] organiza los datos de experiencia del cliente.
   - [Conceptos básicos de composición de esquemas](../../../../../xdm/schema/composition.md): Obtenga información acerca de los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   - [Tutorial del Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): Aprenda a crear esquemas personalizados mediante la interfaz de usuario del Editor de esquemas.
- [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Proporciona un perfil de consumidor unificado y en tiempo real basado en los datos agregados de varias fuentes.

Si ya tiene un válido [!DNL Kinesis] conexión, puede omitir el resto de este documento y continuar con el tutorial sobre [configuración de un flujo de datos](../../dataflow/streaming/cloud-storage-streaming.md).

### Recopilar credenciales necesarias

Para autenticar su [!DNL Kinesis] conector de origen, debe proporcionar valores para las siguientes propiedades de conexión:

| Credencial | Descripción |
| ---------- | ----------- |
| `accessKeyId` | El ID de la clave de acceso de su [!DNL Kinesis] cuenta. |
| `Secret access key` | La clave secreta de acceso para su [!DNL Kinesis] cuenta. |
| `region` | La región del servidor de AWS. |

Para obtener más información, consulte [esta [!DNL Kinesis] documento](https://docs.aws.amazon.com/streams/latest/dev/getting-started.html).

## Conecte su [!DNL Kinesis] account

Una vez que haya recopilado las credenciales necesarias, puede seguir los pasos a continuación para vincular su [!DNL Kinesis] cuenta a [!DNL Platform].

Iniciar sesión en [Adobe Experience Platform](https://platform.adobe.com) y luego seleccione **[!UICONTROL Fuentes]** desde la barra de navegación izquierda para acceder a **[!UICONTROL Fuentes]** workspace. El **[!UICONTROL Catálogo]** La pantalla muestra una variedad de fuentes para las que puede crear una cuenta con.

Puede seleccionar la categoría adecuada del catálogo en la parte izquierda de la pantalla. También puede encontrar la fuente específica con la que desea trabajar utilizando la opción de búsqueda.

En el **[!UICONTROL Almacenamiento en la nube]** categoría, seleccionar **[!UICONTROL Amazon Kinesis]**. Si es la primera vez que utiliza este conector, seleccione **[!UICONTROL Configurar]**. De lo contrario, seleccione **[!UICONTROL Añadir datos]** para crear una nueva [!DNL Kinesis] conector.

![](../../../../images/tutorials/create/kinesis/catalog.png)

El **[!UICONTROL Conectar con Amazon Kinesis]** aparece el cuadro de diálogo. En esta página, puede usar credenciales nuevas o existentes.

### Nueva cuenta

Si está usando credenciales nuevas, seleccione **[!UICONTROL Nueva cuenta]**. En el formulario de entrada que aparece, proporcione un nombre, una descripción opcional y su [!DNL Kinesis] credenciales. Cuando termine, seleccione **[!UICONTROL Connect]** y, a continuación, espere un poco para que se establezca la nueva conexión.

![](../../../../images/tutorials/create/kinesis/new.png)

### Cuenta existente

Para conectar una cuenta existente, seleccione la [!DNL Kinesis] cuenta con la que desea conectarse y, a continuación, seleccione **[!UICONTROL Siguiente]** para continuar.

![](../../../../images/tutorials/create/kinesis/existing.png)

## Pasos siguientes

Al seguir este tutorial, se ha conectado a su [!DNL Kinesis] cuenta a [!DNL Platform]. Ahora puede continuar con el siguiente tutorial y [configure un flujo de datos para traer datos de su almacenamiento en la nube a [!DNL Platform]](../../dataflow/streaming/cloud-storage-streaming.md).
