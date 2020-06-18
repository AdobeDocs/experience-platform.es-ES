---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Creación de un conector de origen de Almacenamiento de archivos de Azure en la interfaz de usuario
topic: overview
translation-type: tm+mt
source-git-commit: ced839f64bea48703c530c83d8592f3842c17e53
workflow-type: tm+mt
source-wordcount: '522'
ht-degree: 0%

---


# Creación de un conector de origen de Almacenamiento de archivos de Azure en la interfaz de usuario

>[!NOTE]
>El conector del Almacenamiento de archivos de Azure está en versión beta. Consulte la descripción general [de](../../../../home.md#terms-and-conditions) Fuentes para obtener más información sobre el uso de conectores con etiquetas beta.

Los conectores de origen en Adobe Experience Platform permiten la ingesta de datos externos de forma programada. Este tutorial proporciona los pasos para autenticar un conector de origen de Almacenamiento de archivos de Azure mediante la interfaz de usuario de Platform.

## Primeros pasos

Este tutorial requiere un conocimiento práctico de los siguientes componentes del Adobe Experience Platform:

- [Sistema](../../../../../xdm/home.md)de modelo de datos de experiencia (XDM): El esquema estandarizado por el cual el Experience Platform organiza los datos de experiencia del cliente.
   - [Conceptos básicos de la composición](../../../../../xdm/schema/composition.md)de esquemas: Obtenga información sobre los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   - [Tutorial](../../../../../xdm/tutorials/create-schema-ui.md)del Editor de Esquemas: Obtenga información sobre cómo crear esquemas personalizados mediante la interfaz de usuario del Editor de Esquemas.
- [Perfil](../../../../../profile/home.md)del cliente en tiempo real: Proporciona un perfil de consumo unificado y en tiempo real basado en datos agregados de varias fuentes.

Si ya tiene una conexión de Almacenamiento de archivos, puede omitir el resto de este documento y continuar con el tutorial sobre la [configuración de un flujo de datos](../../dataflow/batch/cloud-storage.md).

### Recopilar las credenciales necesarias

Para autenticar el conector de origen del Almacenamiento de archivos de Azure, debe proporcionar valores para las siguientes propiedades de conexión:

| Credencial | Descripción |
| ---------- | ----------- |
| `host` | Extremo de la instancia de Almacenamiento de archivos de Azure a la que está accediendo. |
| `userId` | El usuario con acceso suficiente al extremo del Almacenamiento de archivos de Azure. |
| `password` | Clave de acceso del Almacenamiento de archivos de Azure. |

Para obtener más información sobre cómo empezar, consulte [este documento](https://docs.microsoft.com/en-us/azure/storage/files/storage-how-to-use-files-windows)de Almacenamiento de archivos de Azure.

## Conectar su cuenta de Almacenamiento de archivos de Azure

Una vez recopiladas las credenciales necesarias, puede seguir los pasos a continuación para crear una nueva cuenta de Almacenamiento de archivos de Azure para conectarse a Platform.

Inicie sesión en [Adobe Experience Platform](https://platform.adobe.com) y, a continuación, seleccione **[!UICONTROL Fuentes]** en la barra de navegación izquierda para acceder al espacio de trabajo *[!UICONTROL Fuentes]* . La pantalla *[!UICONTROL Catálogo]* muestra una serie de orígenes para los que puede crear una cuenta de entrada y cada origen muestra el número de cuentas existentes y flujos de datos asociados a ellas.

Puede seleccionar la categoría adecuada en el catálogo a la izquierda de la pantalla. También puede encontrar la fuente específica con la que desea trabajar mediante la opción de búsqueda.

En la categoría *[!UICONTROL Bases de datos]* , seleccione Almacenamiento **[!UICONTROL de archivos de]** Azure y haga clic **en el icono + (+)** para crear un nuevo conector de Almacenamiento de archivos de Azure.

![catálogo](../../../../images/tutorials/create/azure-file-storage/catalog.png)

Aparece la página *[!UICONTROL Conectar con el Almacenamiento]* de archivos de Azure. En esta página, puede usar credenciales nuevas o existentes.

### Nueva cuenta

Si está utilizando nuevas credenciales, seleccione **[!UICONTROL Nueva cuenta]**. En el formulario de entrada que aparece, proporcione la conexión con un nombre, una descripción opcional y las credenciales del Almacenamiento de archivos. Cuando termine, seleccione **[!UICONTROL Connect]** y, a continuación, espere un poco de tiempo para que se establezca la nueva cuenta.

![connect](../../../../images/tutorials/create/azure-file-storage/new.png)

### Cuenta existente

Para conectar una cuenta existente, seleccione la cuenta de Almacenamiento de archivos de Azure con la que desea conectarse y, a continuación, seleccione **[!UICONTROL Siguiente]** para continuar.

![existente](../../../../images/tutorials/create/azure-file-storage/existing.png)

## Pasos siguientes

Siguiendo este tutorial, ha establecido una conexión con su cuenta de Almacenamiento de archivos de Azure. Ahora puede continuar con el siguiente tutorial y [configurar un flujo de datos para traer datos de su almacenamiento de nube a Platform](../../dataflow/batch/cloud-storage.md).