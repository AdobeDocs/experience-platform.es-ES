---
keywords: Experience Platform;inicio;temas populares;Apache HDFS;HDFS;hdfs
solution: Experience Platform
title: Crear una conexión de origen de Apache HDFS en la interfaz de usuario
type: Tutorial
description: Obtenga información sobre cómo crear una conexión de origen del sistema de archivos distribuido de Hadoop de Apache mediante la interfaz de usuario de Adobe Experience Platform.
exl-id: 3b8bf210-13b6-44e6-9090-152998f67452
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '492'
ht-degree: 1%

---

# Crear un [!DNL Apache] Conexión de origen de HDFS en la interfaz de usuario

>[!NOTE]
>
>El [!DNL Apache] El conector HDFS está en versión beta. Consulte la [Resumen de orígenes](../../../../home.md#terms-and-conditions) para obtener más información sobre el uso de conectores con etiqueta beta.

Conectores de origen en [!DNL Adobe Experience Platform] permite introducir datos de origen externo de forma programada. Este tutorial proporciona los pasos para autenticar un [!DNL Apache Hadoop Distributed File System] (en lo sucesivo, &quot;HDFS&quot;) que utiliza el conector de origen [!DNL Platform] interfaz de usuario.

## Primeros pasos

Este tutorial requiere una comprensión práctica de los siguientes componentes de [!DNL Platform]:

- [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): El marco estandarizado mediante el cual [!DNL Experience Platform] organiza los datos de experiencia del cliente.
   - [Conceptos básicos de composición de esquemas](../../../../../xdm/schema/composition.md): Obtenga información acerca de los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   - [Tutorial del Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): Aprenda a crear esquemas personalizados mediante la interfaz de usuario del Editor de esquemas.
- [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Proporciona un perfil de consumidor unificado y en tiempo real basado en los datos agregados de varias fuentes.

Si ya tiene una conexión HDFS válida, puede omitir el resto de este documento y continuar con el tutorial sobre [configuración de un flujo de datos](../../dataflow/batch/cloud-storage.md).

### Recopilar credenciales necesarias

Para autenticar el conector de origen de HDFS, debe proporcionar valores para la siguiente propiedad de conexión:

| Credencial | Descripción |
| ---------- | ----------- |
| `url` | La URL define los parámetros de autenticación necesarios para conectarse a HDFS de forma anónima. Para obtener más información sobre cómo obtener este valor, consulte el siguiente documento sobre [Autenticación HTTPS para HDFS](https://hadoop.apache.org/docs/r1.2.1/HttpAuthentication.html). |

## Conecte su cuenta de HDFS

Una vez que haya recopilado las credenciales requeridas, puede seguir los pasos a continuación para vincular su cuenta HDFS a [!DNL Platform].

Iniciar sesión en [Adobe Experience Platform](https://platform.adobe.com) y luego seleccione **[!UICONTROL Fuentes]** desde la barra de navegación izquierda para acceder a **[!UICONTROL Fuentes]** workspace. El **[!UICONTROL Catálogo]** La pantalla muestra una variedad de fuentes para las que puede crear una cuenta con.

Puede seleccionar la categoría adecuada del catálogo en la parte izquierda de la pantalla. También puede encontrar la fuente específica con la que desea trabajar utilizando la opción de búsqueda.

En el **[!UICONTROL Almacenamiento en la nube]** categoría, seleccionar **[!UICONTROL Apache HDFS]**. Si es la primera vez que utiliza este conector, seleccione **[!UICONTROL Configurar]**. De lo contrario, seleccione **[!UICONTROL Añadir datos]** para crear un nuevo conector HDFS.

![catalogar](../../../../images/tutorials/create/hdfs/catalog.png)

El **[!UICONTROL Conectar con HDFS]** página. En esta página, puede usar credenciales nuevas o existentes.

### Nueva cuenta

Si está usando credenciales nuevas, seleccione **[!UICONTROL Nueva cuenta]**. En el formulario de entrada que aparece, proporcione un nombre, una descripción opcional y sus credenciales de HDFS. Cuando termine, seleccione **[!UICONTROL Conectar con el origen]** y, a continuación, espere un poco para que se establezca la nueva conexión.

![conectar](../../../../images/tutorials/create/hdfs/new.png)

### Cuenta existente

Para conectar una cuenta existente, seleccione la cuenta HDFS con la que desee conectarse y, a continuación, seleccione **[!UICONTROL Siguiente]** para continuar.

![existente](../../../../images/tutorials/create/hdfs/existing.png)

## Pasos siguientes

Al seguir este tutorial, ha establecido una conexión con su cuenta de HDFS. Ahora puede continuar con el siguiente tutorial y [configure un flujo de datos para traer datos de su almacenamiento en la nube a [!DNL Platform]](../../dataflow/batch/cloud-storage.md).
