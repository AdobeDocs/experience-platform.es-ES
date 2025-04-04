---
keywords: Experience Platform;inicio;temas populares;FTP;ftp
solution: Experience Platform
title: Creación de una conexión FTP-Source en la interfaz de usuario
type: Tutorial
description: Obtenga información sobre cómo crear una conexión de origen FTP mediante la interfaz de usuario de Adobe Experience Platform.
exl-id: 8e505ead-4bae-43fe-830b-75620e8fba28
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '464'
ht-degree: 2%

---

# Creación de una conexión de origen FTP en la interfaz de usuario

>[!NOTE]
>
>El conector FTP está en versión beta. Consulte [Resumen de fuentes](../../../../home.md#terms-and-conditions) para obtener más información sobre el uso de conectores con etiqueta beta.

En este tutorial se proporcionan los pasos para crear una conexión de origen FTP mediante la interfaz de usuario de Adobe Experience Platform.

## Introducción

Este tutorial requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): El marco estandarizado mediante el cual Experience Platform organiza los datos de experiencia del cliente.
   * [Aspectos básicos de la composición de esquemas](../../../../../xdm/schema/composition.md): obtenga información sobre los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   * [Tutorial del editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): Aprenda a crear esquemas personalizados mediante la interfaz de usuario del editor de esquemas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): proporciona un perfil de consumidor unificado y en tiempo real basado en los datos agregados de varias fuentes.

Si ya tiene una conexión FTP válida, puede omitir el resto de este documento y continuar con el tutorial sobre [configuración de un flujo de datos](../../dataflow/batch/cloud-storage.md).

### Recopilar credenciales necesarias

Para conectarse a FTP, debe proporcionar valores para las siguientes propiedades de conexión:

| Credencial | Descripción |
| ---------- | ----------- |
| `host` | El nombre o la dirección IP asociados con el servidor FTP. |
| `username` | El nombre de usuario con acceso a su servidor FTP. |
| `password` | Contraseña del servidor FTP. |

## Conexión a su servidor FTP

Una vez que haya recopilado las credenciales necesarias, puede seguir los pasos a continuación para crear una nueva cuenta de FTP y conectarse a Experience Platform.

Inicie sesión en [Adobe Experience Platform](https://platform.adobe.com) y, a continuación, seleccione **[!UICONTROL Fuentes]** en la barra de navegación izquierda para acceder al área de trabajo de [!UICONTROL Fuentes]. La pantalla [!UICONTROL Catálogo] muestra una variedad de orígenes con los que puede crear una cuenta entrante.

Puede seleccionar la categoría adecuada del catálogo en la parte izquierda de la pantalla. También puede encontrar la fuente específica con la que desea trabajar utilizando la opción de búsqueda.

En la categoría [!UICONTROL Almacenamiento en la nube], seleccione **[!UICONTROL FTP]**. Si es la primera vez que usa este conector, seleccione **[!UICONTROL Configurar]**. De lo contrario, seleccione **[!UICONTROL Agregar datos]** para crear una nueva conexión FTP.

![catálogo](../../../../images/tutorials/create/ftp/catalog.png)

Aparecerá la página **[!UICONTROL Conectarse a FTP]**. En esta página, puede usar credenciales nuevas o existentes.

### Nueva cuenta

Si está usando credenciales nuevas, seleccione **[!UICONTROL Nueva cuenta]**. En el formulario de entrada que aparece, proporcione un nombre, una descripción opcional y sus credenciales. Cuando termine, seleccione **[!UICONTROL Conectar]** y deje pasar un tiempo para que se establezca la nueva conexión.

![nuevo](../../../../images/tutorials/create/ftp/new.png)

### Cuenta existente

Para conectar una cuenta existente, selecciona la cuenta de FTP con la que deseas conectarte y, a continuación, selecciona **[!UICONTROL Siguiente]** para continuar.

![existente](../../../../images/tutorials/create/ftp/existing.png)

## Pasos siguientes

Con este tutorial ha establecido una conexión con su cuenta de FTP. Ahora puede continuar con el siguiente tutorial y [configurar un flujo de datos para traer datos de su almacenamiento en la nube a Experience Platform](../../dataflow/batch/cloud-storage.md).
