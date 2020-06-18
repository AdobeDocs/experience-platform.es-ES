---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Creación de un conector de origen de Amazon Kinesis en la interfaz de usuario
topic: overview
translation-type: tm+mt
source-git-commit: 855f543a1cef394d121502f03471a60b97eae256
workflow-type: tm+mt
source-wordcount: '454'
ht-degree: 1%

---


# Creación de un conector de origen de Amazon Kinesis en la interfaz de usuario

>[!NOTE]
>El conector de Amazon Kinesis está en versión beta. Consulte la descripción general [de](../../../../home.md#terms-and-conditions) Fuentes para obtener más información sobre el uso de conectores con etiquetas beta.

Los conectores de origen en Adobe Experience Platform permiten la ingesta de datos externos de forma programada. Este tutorial proporciona los pasos para autenticar un conector de origen de Amazon Kinesis (en adelante, &quot;Kinesis&quot;) mediante la interfaz de usuario de Platform.

## Primeros pasos

Este tutorial requiere un conocimiento práctico de los siguientes componentes del Adobe Experience Platform:

- [Sistema](../../../../../xdm/home.md)de modelo de datos de experiencia (XDM): El esquema estandarizado por el cual el Experience Platform organiza los datos de experiencia del cliente.
   - [Conceptos básicos de la composición](../../../../../xdm/schema/composition.md)de esquemas: Obtenga información sobre los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   - [Tutorial](../../../../../xdm/tutorials/create-schema-ui.md)del Editor de Esquemas: Obtenga información sobre cómo crear esquemas personalizados mediante la interfaz de usuario del Editor de Esquemas.
- [Perfil](../../../../../profile/home.md)del cliente en tiempo real: Proporciona un perfil de consumo unificado y en tiempo real basado en datos agregados de varias fuentes.

Si ya tiene una cuenta de Kinesis, puede omitir el resto de este documento y continuar con el tutorial sobre la [configuración de un flujo de datos](../../dataflow/streaming/cloud-storage.md).

### Recopilar las credenciales necesarias

Para autenticar el conector de origen de Kinesis, debe proporcionar valores para las siguientes propiedades de conexión:

| Credencial | Descripción |
| ---------- | ----------- |
| `accessKeyId` | ID de la clave de acceso de su cuenta de Kinesis. |
| `Secret access key` | Clave de acceso secreta para su cuenta de Kinesis. |
| `region` | Región del servidor de AWS. |

Para obtener más información sobre estos valores, consulte [este documento](https://docs.aws.amazon.com/streams/latest/dev/getting-started.html)de Kinesis.

## Conectar la cuenta de Kinesis

Una vez recopiladas las credenciales necesarias, puede seguir los pasos a continuación para vincular su cuenta de Kinesis a Platform.

Inicie sesión en [Adobe Experience Platform](https://platform.adobe.com) y seleccione **Fuentes** en la barra de navegación izquierda para acceder al espacio de trabajo *Fuentes* . La ficha *Catálogo* muestra una serie de orígenes para los que se puede conectar a Platform. Cada origen muestra el número de cuentas existentes asociadas a ellas.

En la categoría *Cloud Almacenamiento* , seleccione **Amazon Kinesis** y haga clic **en el icono + (+)** para crear un nuevo conector Kinesis.

![](../../../../images/tutorials/create/kinesis/catalog.png)

Aparecerá el cuadro de diálogo *Conectar con Amazon Kinesis* . En esta página, puede usar credenciales nuevas o existentes.

### Nueva cuenta

Si está utilizando nuevas credenciales, seleccione **Nueva cuenta**. En el formulario de entrada que aparece, especifique un nombre, una descripción opcional y las credenciales de Kinesis. Cuando termine, seleccione **Connect** y, a continuación, espere un poco de tiempo para que se establezca la nueva conexión.

![](../../../../images/tutorials/create/kinesis/new.png)

### Cuenta existente

Para conectar una cuenta existente, seleccione la cuenta de Kinesis con la que desea conectarse y, a continuación, seleccione **Siguiente** para continuar.

![](../../../../images/tutorials/create/kinesis/existing.png)

## Pasos siguientes

Siguiendo este tutorial, se ha conectado a su cuenta de Kinesis a Platform. Ahora puede continuar con el siguiente tutorial y [configurar un flujo de datos para traer datos de su almacenamiento de nube a Platform](../../dataflow/streaming/cloud-storage.md).