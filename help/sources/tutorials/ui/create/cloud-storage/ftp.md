---
keywords: Experience Platform;inicio;temas populares;FTP;ftp
solution: Experience Platform
title: Crear una conexión de origen de FTP en la interfaz de usuario
topic-legacy: overview
type: Tutorial
description: Obtenga información sobre cómo crear una conexión de origen FTP mediante la interfaz de usuario de Adobe Experience Platform.
exl-id: 8e505ead-4bae-43fe-830b-75620e8fba28
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '447'
ht-degree: 1%

---

# Crear una conexión de origen FTP en la interfaz de usuario

>[!NOTE]
>
>El conector FTP está en versión beta. Consulte la [información general sobre fuentes](../../../../home.md#terms-and-conditions) para obtener más información sobre el uso de conectores con etiqueta beta.

Este tutorial proporciona los pasos para crear una conexión de origen FTP mediante la interfaz de usuario de Adobe Experience Platform.

## Primeros pasos

Este tutorial requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): El marco estandarizado mediante el cual el Experience Platform organiza los datos de experiencia del cliente.
   * [Aspectos básicos de la composición](../../../../../xdm/schema/composition.md) del esquema: Obtenga información sobre los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   * [Tutorial del Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): Aprenda a crear esquemas personalizados mediante la interfaz de usuario del Editor de esquemas.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Proporciona un perfil de cliente unificado y en tiempo real basado en datos agregados de varias fuentes.

Si ya tiene una conexión FTP válida, puede omitir el resto de este documento y continuar con el tutorial sobre la [configuración de un flujo de datos](../../dataflow/batch/cloud-storage.md).

### Recopilar las credenciales necesarias

Para conectarse a FTP, debe proporcionar valores para las siguientes propiedades de conexión:

| Credencial | Descripción |
| ---------- | ----------- |
| `host` | El nombre o la dirección IP asociados con su servidor FTP. |
| `username` | El nombre de usuario con acceso a su servidor FTP. |
| `password` | La contraseña del servidor FTP. |

## Conectarse al servidor FTP

Una vez que haya recopilado las credenciales necesarias, puede seguir los pasos a continuación para crear una nueva cuenta de FTP que se conecte a Platform.

Inicie sesión en [Adobe Experience Platform](https://platform.adobe.com) y, a continuación, seleccione **[!UICONTROL Sources]** en la barra de navegación izquierda para acceder al espacio de trabajo [!UICONTROL Sources]. La pantalla [!UICONTROL Catalog] muestra una variedad de fuentes para las que puede crear una cuenta de entrada.

Puede seleccionar la categoría adecuada del catálogo en la parte izquierda de la pantalla. Alternativamente, puede encontrar la fuente específica con la que desea trabajar usando la opción de búsqueda.

En la categoría [!UICONTROL Cloud storage], seleccione **[!UICONTROL FTP]**. Si es la primera vez que utiliza este conector, seleccione **[!UICONTROL Configure]**. De lo contrario, seleccione **[!UICONTROL Add data]** para crear una nueva conexión FTP.

![catálogo](../../../../images/tutorials/create/ftp/catalog.png)

Aparece la página **[!UICONTROL Connect to FTP]**. En esta página, puede usar credenciales nuevas o existentes.

### Nueva cuenta

Si está utilizando credenciales nuevas, seleccione **[!UICONTROL New account]**. En el formulario de entrada que aparece, indique un nombre, una descripción opcional y sus credenciales. Cuando termine, seleccione **[!UICONTROL Connect]** y, a continuación, deje que se establezca la nueva conexión.

![new](../../../../images/tutorials/create/ftp/new.png)

### Cuenta existente

Para conectar una cuenta existente, seleccione la cuenta de FTP con la que desee conectarse y, a continuación, seleccione **[!UICONTROL Next]** para continuar.

![existente](../../../../images/tutorials/create/ftp/existing.png)

## Pasos siguientes

Siguiendo este tutorial, ha establecido una conexión con su cuenta de FTP. Ahora puede continuar con el siguiente tutorial y [configurar un flujo de datos para importar los datos del almacenamiento en la nube a Platform](../../dataflow/batch/cloud-storage.md).
