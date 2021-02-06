---
keywords: Experience Platform;inicio;temas populares;Apache HDFS;HDFS;hdfs
solution: Experience Platform
title: Creación de una conexión de origen HDFS de Apache en la interfaz de usuario
topic: overview
type: Tutorial
description: Aprenda a crear una conexión de origen de Apache Hadoop Distributed File System mediante la interfaz de usuario de Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: c7fb0d50761fa53c1fdf4dd70a63c62f2dcf6c85
workflow-type: tm+mt
source-wordcount: '492'
ht-degree: 1%

---


# Crear una conexión de origen [!DNL Apache] HDFS en la interfaz de usuario

>[!NOTE]
>
>El conector [!DNL Apache] HDFS está en versión beta. Consulte la [información general de las fuentes](../../../../home.md#terms-and-conditions) para obtener más información sobre el uso de conectores con etiquetas beta.

Los conectores de origen de [!DNL Adobe Experience Platform] permiten la ingesta de datos de origen externo de manera programada. Este tutorial proporciona pasos para autenticar un conector de origen [!DNL Apache Hadoop Distributed File System] (en adelante denominado &quot;HDFS&quot;) mediante la interfaz de usuario [!DNL Platform].

## Primeros pasos

Este tutorial requiere un conocimiento práctico de los siguientes componentes de [!DNL Platform]:

- [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): Marco normalizado por el cual se  [!DNL Experience Platform] organizan los datos de experiencia del cliente.
   - [Conceptos básicos de la composición](../../../../../xdm/schema/composition.md) de esquemas: Obtenga información sobre los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   - [Tutorial](../../../../../xdm/tutorials/create-schema-ui.md) del Editor de esquemas: Obtenga información sobre cómo crear esquemas personalizados mediante la interfaz de usuario del Editor de Esquemas.
- [[!DNL Real-time Customer Profile]](../../../../../profile/home.md):: Proporciona un perfil de consumo unificado y en tiempo real basado en datos agregados de varias fuentes.

Si ya tiene una conexión HDFS válida, puede omitir el resto de este documento y continuar con el tutorial sobre [configuración de un flujo de datos](../../dataflow/batch/cloud-storage.md).

### Recopilar las credenciales necesarias

Para autenticar el conector de origen HDFS, debe proporcionar valores para la siguiente propiedad de conexión:

| Credencial | Descripción |
| ---------- | ----------- |
| `url` | La URL define parámetros de autenticación necesarios para conectarse a HDFS de forma anónima. Para obtener más información sobre cómo obtener este valor, consulte el siguiente documento sobre [autenticación HTTPS para HDFS](https://hadoop.apache.org/docs/r1.2.1/HttpAuthentication.html). |

## Conectar la cuenta de HDFS

Una vez recopiladas las credenciales requeridas, puede seguir los pasos a continuación para vincular su cuenta de HDFS a [!DNL Platform].

Inicie sesión en [Adobe Experience Platform](https://platform.adobe.com) y, a continuación, seleccione **[!UICONTROL Fuentes]** en la barra de navegación izquierda para acceder al espacio de trabajo **[!UICONTROL Fuentes]**. La pantalla **[!UICONTROL Catálogo]** muestra una variedad de fuentes con las que puede crear una cuenta.

Puede seleccionar la categoría adecuada en el catálogo a la izquierda de la pantalla. También puede encontrar la fuente específica con la que desea trabajar mediante la opción de búsqueda.

En la categoría **[!UICONTROL Cloud almacenamiento]**, seleccione **[!UICONTROL Apache HDFS]**. Si es la primera vez que utiliza este conector, seleccione **[!UICONTROL Configurar]**. De lo contrario, seleccione **[!UICONTROL Añadir datos]** para crear un nuevo conector HDFS.

![catálogo](../../../../images/tutorials/create/hdfs/catalog.png)

Aparece la página **[!UICONTROL Conectar con HDFS]**. En esta página, puede usar credenciales nuevas o existentes.

### Nueva cuenta

Si está utilizando nuevas credenciales, seleccione **[!UICONTROL Nueva cuenta]**. En el formulario de entrada que aparece, especifique un nombre, una descripción opcional y sus credenciales de HDFS. Cuando termine, seleccione **[!UICONTROL Conectar con origen]** y, a continuación, deje transcurrir un tiempo para que se establezca la nueva conexión.

![connect](../../../../images/tutorials/create/hdfs/new.png)

### Cuenta existente

Para conectar una cuenta existente, seleccione la cuenta de HDFS con la que desea conectarse y, a continuación, seleccione **[!UICONTROL Siguiente]** para continuar.

![existente](../../../../images/tutorials/create/hdfs/existing.png)

## Pasos siguientes

Siguiendo este tutorial, ha establecido una conexión con su cuenta de HDFS. Ahora puede continuar con el siguiente tutorial y [configurar un flujo de datos para traer datos del almacenamiento de nube a [!DNL Platform]](../../dataflow/batch/cloud-storage.md).