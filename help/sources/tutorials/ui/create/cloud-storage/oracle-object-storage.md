---
keywords: Experience Platform;inicio;temas populares;Almacenamiento de objetos de Oracle;almacenamiento de objetos de oracle
solution: Experience Platform
title: Crear una conexión de origen de almacenamiento de objetos de Oracle en la interfaz de usuario
topic-legacy: overview
type: Tutorial
description: Aprenda a crear una conexión de origen de Almacenamiento de objetos de Oracle mediante la interfaz de usuario de Adobe Experience Platform.
exl-id: 32284163-5dde-4171-8977-f76ceeebcef2
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '446'
ht-degree: 1%

---

# Crear una conexión de origen [!DNL Oracle Object Storage] en la interfaz de usuario

Este tutorial proporciona los pasos para crear una conexión de origen [!DNL Oracle Object Storage] mediante la interfaz de usuario de Adobe Experience Platform.

## Primeros pasos

Este tutorial requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [Fuentes](../../../../home.md): Experience Platform permite la ingesta de datos de varias fuentes, al mismo tiempo que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de Platform.
* [Simuladores para pruebas](../../../../../sandboxes/home.md): Experience Platform proporciona entornos limitados virtuales que dividen una sola instancia de Platform en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

### Recopilar las credenciales necesarias

En para conectarse a [!DNL Oracle Object Storage], debe proporcionar valores para las siguientes propiedades de conexión:

| Credencial | Descripción |
| ---------- | ----------- |
| `serviceUrl` | El extremo [!DNL Oracle Object Storage] requerido para la autenticación. El formato del punto final es: `https://{OBJECT_STORAGE_NAMESPACE}.compat.objectstorage.eu-frankfurt-1.oraclecloud.com` |
| `accessKey` | El ID de clave de acceso [!DNL Oracle Object Storage] requerido para la autenticación. |
| `secretKey` | La contraseña [!DNL Oracle Object Storage] requerida para la autenticación. |
| `bucketName` | El nombre de bloque permitido requerido si el usuario tiene acceso restringido. El nombre del contenedor debe tener entre tres y 63 caracteres, debe comenzar y terminar con una letra o un número y solo puede contener letras minúsculas, números o guiones (`-`). No se puede dar formato al nombre del bloque como una dirección IP. |
| `folderPath` | La ruta de carpeta permitida necesaria si el usuario tiene acceso restringido. |

Para obtener más información sobre cómo obtener estos valores, consulte la [Guía de autenticación del Almacenamiento de objetos de Oracle](https://docs.oracle.com/en-us/iaas/Content/Identity/Concepts/usercredentials.htm#User_Credentials).

Una vez que haya recopilado las credenciales necesarias, puede seguir los pasos a continuación para crear una nueva cuenta de Oracle de almacenamiento de objetos para conectarse a Platform.

## Conexión al almacenamiento de objetos de Oracle

En la interfaz de usuario de Platform, seleccione **[!UICONTROL Sources]** en el panel de navegación izquierdo para acceder al espacio de trabajo [!UICONTROL Sources]. La pantalla [!UICONTROL Catalog] muestra una variedad de fuentes con las que puede crear una cuenta.

Puede seleccionar la categoría adecuada del catálogo en la parte izquierda de la pantalla. También puede encontrar la fuente específica con la que desea trabajar mediante la barra de búsqueda.

En la categoría [!UICONTROL Cloud storage], seleccione **[!UICONTROL Oracle Object Storage]** y luego seleccione **[!UICONTROL Add data]**.

![catálogo](../../../../images/tutorials/create/oracle-object-storage/catalog.png)

### Cuenta existente

Para utilizar una cuenta existente, seleccione la cuenta [!DNL Oracle Object Storage] con la que desea crear un nuevo flujo de datos y, a continuación, seleccione **[!UICONTROL Next]** para continuar.

![existente](../../../../images/tutorials/create/oracle-object-storage/existing.png)

### Nueva cuenta

Si está creando una cuenta nueva, seleccione **[!UICONTROL New account]** y, a continuación, proporcione un nombre, una descripción opcional y sus credenciales [!DNL Oracle Object Storage]. Cuando termine, seleccione **[!UICONTROL Connect to source]** y, a continuación, deje que se establezca la nueva conexión.

![new](../../../../images/tutorials/create/oracle-object-storage/new.png)

## Pasos siguientes

Al seguir este tutorial, ha establecido una conexión con su cuenta [!DNL Oracle Object Storage]. Ahora puede continuar con el siguiente tutorial sobre la [configuración de un flujo de datos para importar los datos del almacenamiento en la nube a Platform](../../dataflow/batch/cloud-storage.md).
