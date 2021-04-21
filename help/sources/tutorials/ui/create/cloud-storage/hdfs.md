---
keywords: Experience Platform;inicio;temas populares;HDFS de Apache;HDFS;hdfs
solution: Experience Platform
title: Crear una conexión de origen de HDFS de Apache en la interfaz de usuario
topic-legacy: overview
type: Tutorial
description: Aprenda a crear una conexión de origen del sistema de archivos distribuido de Hadoop Apache utilizando la interfaz de usuario de Adobe Experience Platform.
exl-id: 3b8bf210-13b6-44e6-9090-152998f67452
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '473'
ht-degree: 1%

---

# Crear una conexión de origen [!DNL Apache] HDFS en la interfaz de usuario

>[!NOTE]
>
>El conector [!DNL Apache] HDFS está en versión beta. Consulte la [información general sobre fuentes](../../../../home.md#terms-and-conditions) para obtener más información sobre el uso de conectores con etiqueta beta.

Los conectores de origen en [!DNL Adobe Experience Platform] permiten ingerir datos de origen externo de forma programada. Este tutorial proporciona los pasos para autenticar un conector de origen [!DNL Apache Hadoop Distributed File System] (en adelante denominado &quot;HDFS&quot;) mediante la interfaz de usuario [!DNL Platform].

## Primeros pasos

Este tutorial requiere una comprensión práctica de los siguientes componentes de [!DNL Platform]:

- [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): El marco estandarizado mediante el cual se  [!DNL Experience Platform] organizan los datos de experiencia del cliente.
   - [Aspectos básicos de la composición](../../../../../xdm/schema/composition.md) del esquema: Obtenga información sobre los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   - [Tutorial del Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): Aprenda a crear esquemas personalizados mediante la interfaz de usuario del Editor de esquemas.
- [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Proporciona un perfil de cliente unificado y en tiempo real basado en datos agregados de varias fuentes.

Si ya tiene una conexión HDFS válida, puede omitir el resto de este documento y continuar con el tutorial sobre la [configuración de un flujo de datos](../../dataflow/batch/cloud-storage.md).

### Recopilar las credenciales necesarias

Para autenticar el conector de origen HDFS, debe proporcionar valores para la siguiente propiedad de conexión:

| Credencial | Descripción |
| ---------- | ----------- |
| `url` | La URL define parámetros de autenticación necesarios para conectarse a HDFS de forma anónima. Para obtener más información sobre cómo obtener este valor, consulte el siguiente documento sobre [autenticación HTTPS para HDFS](https://hadoop.apache.org/docs/r1.2.1/HttpAuthentication.html). |

## Conecte su cuenta de HDFS

Una vez que haya reunido las credenciales requeridas, puede seguir los pasos a continuación para vincular su cuenta de HDFS a [!DNL Platform].

Inicie sesión en [Adobe Experience Platform](https://platform.adobe.com) y, a continuación, seleccione **[!UICONTROL Sources]** en la barra de navegación izquierda para acceder al espacio de trabajo **[!UICONTROL Sources]**. La pantalla **[!UICONTROL Catalog]** muestra una variedad de fuentes para las que puede crear una cuenta.

Puede seleccionar la categoría adecuada del catálogo en la parte izquierda de la pantalla. Alternativamente, puede encontrar la fuente específica con la que desea trabajar usando la opción de búsqueda.

En la categoría **[!UICONTROL Cloud storage]**, seleccione **[!UICONTROL Apache HDFS]**. Si es la primera vez que utiliza este conector, seleccione **[!UICONTROL Configure]**. De lo contrario, seleccione **[!UICONTROL Add data]** para crear un nuevo conector HDFS.

![catálogo](../../../../images/tutorials/create/hdfs/catalog.png)

Aparece la página **[!UICONTROL Connect to HDFS]**. En esta página, puede usar credenciales nuevas o existentes.

### Nueva cuenta

Si está utilizando credenciales nuevas, seleccione **[!UICONTROL New account]**. En el formulario de entrada que aparece, indique un nombre, una descripción opcional y sus credenciales de HDFS. Cuando termine, seleccione **[!UICONTROL Connect to source]** y, a continuación, deje que se establezca la nueva conexión.

![connect](../../../../images/tutorials/create/hdfs/new.png)

### Cuenta existente

Para conectar una cuenta existente, seleccione la cuenta de HDFS con la que desee conectarse y, a continuación, seleccione **[!UICONTROL Next]** para continuar.

![existente](../../../../images/tutorials/create/hdfs/existing.png)

## Pasos siguientes

Siguiendo este tutorial, ha establecido una conexión con su cuenta de HDFS. Ahora puede continuar con el siguiente tutorial y [configurar un flujo de datos para incorporar datos del almacenamiento en la nube a [!DNL Platform]](../../dataflow/batch/cloud-storage.md).
