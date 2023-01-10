---
keywords: Experience Platform;inicio;temas populares;Almacenamiento de objetos de Oracle;almacenamiento de objetos de oracle
solution: Experience Platform
title: Crear una conexión de origen de almacenamiento de objetos de Oracle en la interfaz de usuario
type: Tutorial
description: Aprenda a crear una conexión de origen de Almacenamiento de objetos de Oracle mediante la interfaz de usuario de Adobe Experience Platform.
exl-id: 32284163-5dde-4171-8977-f76ceeebcef2
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '462'
ht-degree: 1%

---

# Cree un [!DNL Oracle Object Storage] Conexión de origen en la interfaz de usuario

Este tutorial proporciona los pasos para crear un [!DNL Oracle Object Storage] conexión de origen mediante la interfaz de usuario de Adobe Experience Platform.

## Primeros pasos

Este tutorial requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [Fuentes](../../../../home.md): Experience Platform permite la ingesta de datos de varias fuentes, al mismo tiempo que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de Platform.
* [Sandboxes](../../../../../sandboxes/home.md): Experience Platform proporciona entornos limitados virtuales que dividen una sola instancia de Platform en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

### Recopilar las credenciales necesarias

En para conectarse a [!DNL Oracle Object Storage], debe proporcionar valores para las siguientes propiedades de conexión:

| Credencial | Descripción |
| ---------- | ----------- |
| `serviceUrl` | La variable [!DNL Oracle Object Storage] extremo requerido para la autenticación. El formato del punto final es: `https://{OBJECT_STORAGE_NAMESPACE}.compat.objectstorage.eu-frankfurt-1.oraclecloud.com` |
| `accessKey` | La variable [!DNL Oracle Object Storage] se requiere el ID de clave de acceso para la autenticación. |
| `secretKey` | La variable [!DNL Oracle Object Storage] contraseña necesaria para la autenticación. |
| `bucketName` | El nombre de bloque permitido requerido si el usuario tiene acceso restringido. El nombre del contenedor debe tener entre tres y 63 caracteres, debe comenzar y terminar con una letra o un número y solo puede contener letras minúsculas, números o guiones (`-`). No se puede dar formato al nombre del bloque como una dirección IP. |
| `folderPath` | La ruta de carpeta permitida necesaria si el usuario tiene acceso restringido. |

Para obtener más información sobre cómo obtener estos valores, consulte la [Guía de autenticación de almacenamiento de objetos oracle](https://docs.oracle.com/en-us/iaas/Content/Identity/Concepts/usercredentials.htm#User_Credentials).

Una vez que haya recopilado las credenciales necesarias, puede seguir los pasos a continuación para crear una nueva cuenta de Oracle de almacenamiento de objetos para conectarse a Platform.

## Conexión al almacenamiento de objetos de Oracle

En la interfaz de usuario de Platform, seleccione **[!UICONTROL Fuentes]** desde el panel de navegación izquierdo para acceder a la [!UICONTROL Fuentes] espacio de trabajo. La variable [!UICONTROL Catálogo] muestra una variedad de fuentes con las que puede crear una cuenta.

Puede seleccionar la categoría adecuada del catálogo en la parte izquierda de la pantalla. También puede encontrar la fuente específica con la que desea trabajar mediante la barra de búsqueda.

En el [!UICONTROL Almacenamiento en la nube] categoría, seleccione **[!UICONTROL Almacenamiento de objetos de oracle]** y, a continuación, seleccione **[!UICONTROL Añadir datos]**.

![catálogo](../../../../images/tutorials/create/oracle-object-storage/catalog.png)

### Cuenta existente

Para usar una cuenta existente, seleccione la opción [!DNL Oracle Object Storage] cuenta con la que desee crear un nuevo flujo de datos y, a continuación, seleccione **[!UICONTROL Siguiente]** para continuar.

![existente](../../../../images/tutorials/create/oracle-object-storage/existing.png)

### Nueva cuenta

Si está creando una cuenta nueva, seleccione **[!UICONTROL Nueva cuenta]** y, a continuación, proporcione un nombre, una descripción opcional y su [!DNL Oracle Object Storage] credenciales. Cuando termine, seleccione **[!UICONTROL Conectar a origen]** y, a continuación, permita que la nueva conexión se establezca durante algún tiempo.

![new](../../../../images/tutorials/create/oracle-object-storage/new.png)

## Pasos siguientes

Al seguir este tutorial, ha establecido una conexión con su [!DNL Oracle Object Storage] cuenta. Ahora puede continuar con el siguiente tutorial en [configuración de un flujo de datos para incorporar datos del almacenamiento en la nube a Platform](../../dataflow/batch/cloud-storage.md).
