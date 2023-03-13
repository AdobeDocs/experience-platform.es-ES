---
keywords: Experience Platform;inicio;temas populares;Azure File Storage;conector de Azure File Storage
solution: Experience Platform
title: Crear una conexión de origen de Azure File Storage en la interfaz de usuario
type: Tutorial
description: Obtenga información sobre cómo crear una conexión de origen de Azure File Storage mediante la interfaz de usuario de Adobe Experience Platform.
exl-id: 25d483b6-3975-4e80-9dbe-28b7b91cb063
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '470'
ht-degree: 1%

---

# Crear un [!DNL Azure File Storage] conexión de origen en la interfaz de usuario

Los conectores de origen en Adobe Experience Platform permiten introducir datos de origen externo de forma programada. Este tutorial proporciona los pasos para autenticar un [!DNL Azure File Storage] conector de origen mediante [!DNL Platform] interfaz de usuario.

## Primeros pasos

Este tutorial requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

- [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): El marco estandarizado mediante el cual [!DNL Experience Platform] organiza los datos de experiencia del cliente.
   - [Conceptos básicos de composición de esquemas](../../../../../xdm/schema/composition.md): Obtenga información acerca de los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   - [Tutorial del Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): Aprenda a crear esquemas personalizados mediante la interfaz de usuario del Editor de esquemas.
- [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Proporciona un perfil de consumidor unificado y en tiempo real basado en los datos agregados de varias fuentes.

Si ya tiene un válido [!DNL Azure File Storage] conexión, puede omitir el resto de este documento y continuar con el tutorial sobre [configuración de un flujo de datos](../../dataflow/batch/cloud-storage.md).

### Recopilar credenciales necesarias

Para autenticar su [!DNL Azure File Storage] conector de origen, debe proporcionar valores para las siguientes propiedades de conexión:

| Credencial | Descripción |
| ---------- | ----------- |
| `host` | El punto final del [!DNL Azure File Storage] instancia a la que accede. |
| `userId` | El usuario con acceso suficiente al [!DNL Azure File Storage] punto final. |
| `password` | El [!DNL Azure File Storage] clave de acceso. |

Para obtener más información sobre cómo empezar, consulte [esta [!DNL Azure File Storage] documento](https://docs.microsoft.com/en-us/azure/storage/files/storage-how-to-use-files-windows).

## Conecte su [!DNL Azure File Storage] account

Una vez que haya recopilado las credenciales necesarias, puede seguir los pasos a continuación para vincular su [!DNL Azure File Storage] cuenta a [!DNL Platform].

Iniciar sesión en [Adobe Experience Platform](https://platform.adobe.com) y luego seleccione **[!UICONTROL Fuentes]** desde la barra de navegación izquierda para acceder a **[!UICONTROL Fuentes]** workspace. El **[!UICONTROL Catálogo]** La pantalla muestra una variedad de fuentes para las que puede crear una cuenta con.

Puede seleccionar la categoría adecuada del catálogo en la parte izquierda de la pantalla. También puede encontrar la fuente específica con la que desea trabajar utilizando la opción de búsqueda.

En el **[!UICONTROL Bases de datos]** categoría, seleccionar **[!UICONTROL Azure File Storage]**. Si es la primera vez que utiliza este conector, seleccione **[!UICONTROL Configurar]**. De lo contrario, seleccione **[!UICONTROL Añadir datos]** para crear una nueva [!DNL Azure File Storage] conector.

![catalogar](../../../../images/tutorials/create/azure-file-storage/catalog.png)

El **[!UICONTROL Conectar con Azure File Storage]** página. En esta página, puede usar credenciales nuevas o existentes.

### Nueva cuenta

Si está usando credenciales nuevas, seleccione **[!UICONTROL Nueva cuenta]**. En el formulario de entrada que aparece, proporcione un nombre, una descripción opcional y su [!DNL Azure File Storage] credenciales. Cuando termine, seleccione **[!UICONTROL Connect]** y, a continuación, espere un poco para que se establezca la nueva conexión.

![conectar](../../../../images/tutorials/create/azure-file-storage/new.png)

### Cuenta existente

Para conectar una cuenta existente, seleccione la [!DNL Azure File Storage] cuenta con la que desea conectarse y, a continuación, seleccione **[!UICONTROL Siguiente]** para continuar.

![existente](../../../../images/tutorials/create/azure-file-storage/existing.png)

## Pasos siguientes

Al seguir este tutorial, ha establecido una conexión con su [!DNL Azure File Storage] cuenta. Ahora puede continuar con el siguiente tutorial y [configure un flujo de datos para traer datos de su almacenamiento en la nube a [!DNL Platform]](../../dataflow/batch/cloud-storage.md).
