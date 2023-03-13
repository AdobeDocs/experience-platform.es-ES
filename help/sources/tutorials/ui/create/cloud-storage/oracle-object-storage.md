---
keywords: Experience Platform;inicio;temas populares;Almacenamiento de objetos de Oracle;almacenamiento de objetos de oracle
solution: Experience Platform
title: Crear una conexión de origen de almacenamiento de objetos de Oracle en la interfaz de usuario
type: Tutorial
description: Obtenga información sobre cómo crear una conexión de origen de Almacenamiento de objetos de Oracle mediante la interfaz de usuario de Adobe Experience Platform.
exl-id: 32284163-5dde-4171-8977-f76ceeebcef2
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '462'
ht-degree: 1%

---

# Crear un [!DNL Oracle Object Storage] Conexión de origen en la IU

Este tutorial proporciona los pasos para crear una [!DNL Oracle Object Storage] conexión de origen mediante la IU de Adobe Experience Platform.

## Primeros pasos

Este tutorial requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [Fuentes](../../../../home.md): Experience Platform permite la ingesta de datos desde varias fuentes y, al mismo tiempo, le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de Platform.
* [Zonas protegidas](../../../../../sandboxes/home.md): El Experience Platform proporciona entornos limitados virtuales que dividen una sola instancia de Platform en entornos virtuales independientes para ayudar a desarrollar y evolucionar aplicaciones de experiencia digital.

### Recopilar credenciales necesarias

En para conectarse a [!DNL Oracle Object Storage], debe proporcionar valores para las siguientes propiedades de conexión:

| Credencial | Descripción |
| ---------- | ----------- |
| `serviceUrl` | El [!DNL Oracle Object Storage] extremo requerido para la autenticación. El formato del punto de conexión es: `https://{OBJECT_STORAGE_NAMESPACE}.compat.objectstorage.eu-frankfurt-1.oraclecloud.com` |
| `accessKey` | El [!DNL Oracle Object Storage] identificador de clave de acceso necesario para la autenticación. |
| `secretKey` | El [!DNL Oracle Object Storage] contraseña necesaria para la autenticación. |
| `bucketName` | Se requiere el nombre de contenedor permitido si el usuario tiene acceso restringido. El nombre del contenedor debe tener entre tres y 63 caracteres, debe comenzar y finalizar con una letra o un número, y solo puede contener letras minúsculas, números o guiones (`-`). El nombre del contenedor no puede tener el formato de una dirección IP. |
| `folderPath` | La ruta de carpeta permitida requerida si el usuario tiene acceso restringido. |

Para obtener más información sobre cómo obtener estos valores, consulte la [Guía de autenticación de oracle Object Storage](https://docs.oracle.com/en-us/iaas/Content/Identity/Concepts/usercredentials.htm#User_Credentials).

Una vez que haya recopilado las credenciales necesarias, puede seguir los pasos a continuación para crear una nueva cuenta de almacenamiento de objetos de Oracle para conectarse a Platform.

## Conectar con almacenamiento de objetos de Oracle

En la IU de Platform, seleccione **[!UICONTROL Fuentes]** desde la navegación izquierda para acceder a [!UICONTROL Fuentes] workspace. El [!UICONTROL Catálogo] La pantalla muestra una variedad de fuentes con las que puede crear una cuenta.

Puede seleccionar la categoría adecuada del catálogo en la parte izquierda de la pantalla. También puede encontrar la fuente específica con la que desea trabajar en la barra de búsqueda.

En el [!UICONTROL Almacenamiento en la nube] categoría, seleccionar **[!UICONTROL Almacenamiento de objetos de oracle]** y luego seleccione **[!UICONTROL Añadir datos]**.

![catalogar](../../../../images/tutorials/create/oracle-object-storage/catalog.png)

### Cuenta existente

Para utilizar una cuenta existente, seleccione la [!DNL Oracle Object Storage] cuenta con la que desea crear un nuevo flujo de datos y seleccione **[!UICONTROL Siguiente]** para continuar.

![existente](../../../../images/tutorials/create/oracle-object-storage/existing.png)

### Nueva cuenta

Si está creando una cuenta nueva, seleccione **[!UICONTROL Nueva cuenta]** y, a continuación, proporcione un nombre, una descripción opcional y su [!DNL Oracle Object Storage] credenciales. Cuando termine, seleccione **[!UICONTROL Conectar con el origen]** y, a continuación, espere un poco para que se establezca la nueva conexión.

![nuevo](../../../../images/tutorials/create/oracle-object-storage/new.png)

## Pasos siguientes

Al seguir este tutorial, ha establecido una conexión con su [!DNL Oracle Object Storage] cuenta. Ahora puede continuar con el siguiente tutorial sobre [configuración de un flujo de datos para llevar datos del almacenamiento en la nube a Platform](../../dataflow/batch/cloud-storage.md).
