---
keywords: Experience Platform;inicio;temas populares;Almacenamiento de archivos de Azure;Conector de almacenamiento de archivos de Azure
solution: Experience Platform
title: Crear una conexión de origen de almacenamiento de archivos de Azure en la interfaz de usuario
topic-legacy: overview
type: Tutorial
description: Obtenga información sobre cómo crear una conexión de origen de almacenamiento de archivos de Azure mediante la interfaz de usuario de Adobe Experience Platform.
exl-id: 25d483b6-3975-4e80-9dbe-28b7b91cb063
source-git-commit: e150f05df2107d7b3a2e95a55dc4ad072294279e
workflow-type: tm+mt
source-wordcount: '470'
ht-degree: 1%

---

# Crear una conexión de origen [!DNL Azure File Storage] en la interfaz de usuario

Los conectores de origen de Adobe Experience Platform permiten la ingesta de datos de origen externo de forma programada. Este tutorial proporciona pasos para autenticar un conector de origen [!DNL Azure File Storage] mediante la interfaz de usuario [!DNL Platform].

## Primeros pasos

Este tutorial requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

- [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): El marco estandarizado mediante el cual se  [!DNL Experience Platform] organizan los datos de experiencia del cliente.
   - [Aspectos básicos de la composición](../../../../../xdm/schema/composition.md) del esquema: Obtenga información sobre los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   - [Tutorial del Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): Aprenda a crear esquemas personalizados mediante la interfaz de usuario del Editor de esquemas.
- [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Proporciona un perfil de cliente unificado y en tiempo real basado en datos agregados de varias fuentes.

Si ya tiene una conexión [!DNL Azure File Storage] válida, puede omitir el resto de este documento y continuar con el tutorial sobre la [configuración de un flujo de datos](../../dataflow/batch/cloud-storage.md).

### Recopilar las credenciales necesarias

Para autenticar el conector de origen [!DNL Azure File Storage], debe proporcionar valores para las siguientes propiedades de conexión:

| Credencial | Descripción |
| ---------- | ----------- |
| `host` | El extremo de la instancia [!DNL Azure File Storage] a la que está accediendo. |
| `userId` | El usuario con acceso suficiente al extremo [!DNL Azure File Storage]. |
| `password` | La clave de acceso [!DNL Azure File Storage]. |

Para obtener más información sobre cómo empezar, consulte [este [!DNL Azure File Storage] documento](https://docs.microsoft.com/en-us/azure/storage/files/storage-how-to-use-files-windows).

## Conecte su cuenta [!DNL Azure File Storage]

Una vez que haya reunido las credenciales necesarias, puede seguir los pasos a continuación para vincular su cuenta [!DNL Azure File Storage] a [!DNL Platform].

Inicie sesión en [Adobe Experience Platform](https://platform.adobe.com) y, a continuación, seleccione **[!UICONTROL Orígenes]** en la barra de navegación izquierda para acceder al espacio de trabajo **[!UICONTROL Orígenes]**. La pantalla **[!UICONTROL Catalog]** muestra una variedad de fuentes con las que puede crear una cuenta.

Puede seleccionar la categoría adecuada del catálogo en la parte izquierda de la pantalla. Alternativamente, puede encontrar la fuente específica con la que desea trabajar usando la opción de búsqueda.

En la categoría **[!UICONTROL Bases de datos]**, seleccione **[!UICONTROL Almacenamiento de archivos de Azure]**. Si es la primera vez que utiliza este conector, seleccione **[!UICONTROL Configurar]**. De lo contrario, seleccione **[!UICONTROL Add data]** para crear un nuevo conector [!DNL Azure File Storage].

![catálogo](../../../../images/tutorials/create/azure-file-storage/catalog.png)

Aparece la página **[!UICONTROL Connect to Azure File Storage]**. En esta página, puede usar credenciales nuevas o existentes.

### Nueva cuenta

Si está utilizando credenciales nuevas, seleccione **[!UICONTROL New account]**. En el formulario de entrada que aparece, indique un nombre, una descripción opcional y sus credenciales [!DNL Azure File Storage]. Cuando termine, seleccione **[!UICONTROL Connect]** y, a continuación, deje que se establezca la nueva conexión.

![connect](../../../../images/tutorials/create/azure-file-storage/new.png)

### Cuenta existente

Para conectar una cuenta existente, seleccione la cuenta [!DNL Azure File Storage] con la que desea conectarse y, a continuación, seleccione **[!UICONTROL Siguiente]** para continuar.

![existente](../../../../images/tutorials/create/azure-file-storage/existing.png)

## Pasos siguientes

Al seguir este tutorial, ha establecido una conexión con su cuenta [!DNL Azure File Storage]. Ahora puede continuar con el siguiente tutorial y [configurar un flujo de datos para incorporar datos del almacenamiento en la nube a [!DNL Platform]](../../dataflow/batch/cloud-storage.md).
