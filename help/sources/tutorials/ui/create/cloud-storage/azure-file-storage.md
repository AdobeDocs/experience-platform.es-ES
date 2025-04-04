---
keywords: Experience Platform;inicio;temas populares;Azure File Storage;conector de Azure File Storage
solution: Experience Platform
title: Crear una conexión de Azure File Storage Source en la interfaz de usuario
type: Tutorial
description: Obtenga información sobre cómo crear una conexión de origen de Azure File Storage mediante la interfaz de usuario de Adobe Experience Platform.
exl-id: 25d483b6-3975-4e80-9dbe-28b7b91cb063
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '463'
ht-degree: 2%

---

# Crear una conexión de origen [!DNL Azure File Storage] en la interfaz de usuario

Los conectores de Source en Adobe Experience Platform permiten introducir datos de origen externo de forma programada. Este tutorial proporciona los pasos para autenticar un conector de origen [!DNL Azure File Storage] mediante la interfaz de usuario [!DNL Experience Platform].

## Introducción

Este tutorial requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

- [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): El marco de trabajo estandarizado mediante el cual [!DNL Experience Platform] organiza los datos de la experiencia del cliente.
   - [Aspectos básicos de la composición de esquemas](../../../../../xdm/schema/composition.md): obtenga información sobre los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   - [Tutorial del editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): Aprenda a crear esquemas personalizados mediante la interfaz de usuario del editor de esquemas.
- [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): proporciona un perfil de consumidor unificado y en tiempo real basado en los datos agregados de varias fuentes.

Si ya tiene una conexión [!DNL Azure File Storage] válida, puede omitir el resto de este documento y continuar con el tutorial sobre [configuración de un flujo de datos](../../dataflow/batch/cloud-storage.md).

### Recopilar credenciales necesarias

Para autenticar el conector de origen [!DNL Azure File Storage], debe proporcionar valores para las siguientes propiedades de conexión:

| Credencial | Descripción |
| ---------- | ----------- |
| `host` | Extremo de la instancia [!DNL Azure File Storage] a la que está accediendo. |
| `userId` | El usuario con acceso suficiente al extremo [!DNL Azure File Storage]. |
| `password` | La clave de acceso [!DNL Azure File Storage]. |

Para obtener más información sobre cómo empezar, consulte [este [!DNL Azure File Storage] documento](https://docs.microsoft.com/en-us/azure/storage/files/storage-how-to-use-files-windows).

## Conectar su cuenta de [!DNL Azure File Storage]

Una vez que haya recopilado las credenciales requeridas, puede seguir los pasos a continuación para vincular su cuenta de [!DNL Azure File Storage] a [!DNL Experience Platform].

Inicie sesión en [Adobe Experience Platform](https://platform.adobe.com) y, a continuación, seleccione **[!UICONTROL Fuentes]** en la barra de navegación izquierda para acceder al área de trabajo de **[!UICONTROL Fuentes]**. La pantalla **[!UICONTROL Catálogo]** muestra una variedad de orígenes con los que puede crear una cuenta.

Puede seleccionar la categoría adecuada del catálogo en la parte izquierda de la pantalla. También puede encontrar la fuente específica con la que desea trabajar utilizando la opción de búsqueda.

En la categoría **[!UICONTROL Bases de datos]**, seleccione **[!UICONTROL Azure File Storage]**. Si es la primera vez que usa este conector, seleccione **[!UICONTROL Configurar]**. De lo contrario, seleccione **[!UICONTROL Agregar datos]** para crear un nuevo conector [!DNL Azure File Storage].

![catálogo](../../../../images/tutorials/create/azure-file-storage/catalog.png)

Aparecerá la página **[!UICONTROL Conectar con Azure File Storage]**. En esta página, puede usar credenciales nuevas o existentes.

### Nueva cuenta

Si está usando credenciales nuevas, seleccione **[!UICONTROL Nueva cuenta]**. En el formulario de entrada que aparece, proporcione un nombre, una descripción opcional y sus credenciales de [!DNL Azure File Storage]. Cuando termine, seleccione **[!UICONTROL Conectar]** y deje pasar un tiempo para que se establezca la nueva conexión.

![conectar](../../../../images/tutorials/create/azure-file-storage/new.png)

### Cuenta existente

Para conectar una cuenta existente, seleccione la cuenta de [!DNL Azure File Storage] con la que desee conectarse y, a continuación, seleccione **[!UICONTROL Siguiente]** para continuar.

![existente](../../../../images/tutorials/create/azure-file-storage/existing.png)

## Pasos siguientes

Al seguir este tutorial, ha establecido una conexión con su cuenta de [!DNL Azure File Storage]. Ahora puede continuar con el siguiente tutorial y [configurar un flujo de datos para traer datos de su almacenamiento en la nube a [!DNL Experience Platform]](../../dataflow/batch/cloud-storage.md).
