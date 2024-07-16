---
keywords: Experience Platform;inicio;temas populares;Almacenamiento de objetos de Oracle;almacenamiento de objetos de oracle
solution: Experience Platform
title: Creación de una conexión de Source de almacenamiento de objetos de Oracle en la IU
type: Tutorial
description: Obtenga información sobre cómo crear una conexión de origen de Almacenamiento de objetos de Oracle mediante la interfaz de usuario de Adobe Experience Platform.
exl-id: 32284163-5dde-4171-8977-f76ceeebcef2
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '454'
ht-degree: 1%

---

# Crear una conexión de Source [!DNL Oracle Object Storage] en la interfaz de usuario

Este tutorial proporciona los pasos para crear una conexión de origen [!DNL Oracle Object Storage] mediante la interfaz de usuario de Adobe Experience Platform.

## Introducción

Este tutorial requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [Fuentes](../../../../home.md): El Experience Platform permite la ingesta de datos de varias fuentes, al tiempo que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de Platform.
* [Zonas protegidas](../../../../../sandboxes/home.md): El Experience Platform proporciona zonas protegidas virtuales que dividen una sola instancia de Platform en entornos virtuales independientes para ayudar a desarrollar y evolucionar aplicaciones de experiencia digital.

### Recopilar credenciales necesarias

Para conectarse a [!DNL Oracle Object Storage], debe proporcionar valores para las siguientes propiedades de conexión:

| Credencial | Descripción |
| ---------- | ----------- |
| `serviceUrl` | Extremo [!DNL Oracle Object Storage] necesario para la autenticación. El formato del extremo es: `https://{OBJECT_STORAGE_NAMESPACE}.compat.objectstorage.eu-frankfurt-1.oraclecloud.com` |
| `accessKey` | La clave de acceso [!DNL Oracle Object Storage] necesaria para la autenticación. |
| `secretKey` | Se requiere la contraseña [!DNL Oracle Object Storage] para la autenticación. |
| `bucketName` | Se requiere el nombre de contenedor permitido si el usuario tiene acceso restringido. El nombre del contenedor debe tener entre tres y 63 caracteres, debe comenzar y finalizar con una letra o un número, y solo puede contener letras minúsculas, números o guiones (`-`). El nombre del contenedor no puede tener el formato de una dirección IP. |
| `folderPath` | La ruta de carpeta permitida requerida si el usuario tiene acceso restringido. |

Para obtener más información sobre cómo obtener estos valores, consulte la [guía de autenticación de almacenamiento de objetos de Oracle](https://docs.oracle.com/en-us/iaas/Content/Identity/Concepts/usercredentials.htm#User_Credentials).

Una vez que haya recopilado las credenciales necesarias, puede seguir los pasos a continuación para crear una nueva cuenta de almacenamiento de objetos de Oracle para conectarse a Platform.

## Conectar con almacenamiento de objetos de Oracle

En la interfaz de usuario de Platform, seleccione **[!UICONTROL Sources]** en el panel de navegación izquierdo para acceder al área de trabajo [!UICONTROL Sources]. La pantalla [!UICONTROL Catálogo] muestra una variedad de orígenes con los que puede crear una cuenta.

Puede seleccionar la categoría adecuada del catálogo en la parte izquierda de la pantalla. También puede encontrar la fuente específica con la que desea trabajar en la barra de búsqueda.

En la categoría [!UICONTROL Almacenamiento en la nube], seleccione **[!UICONTROL Almacenamiento de objetos de Oracle]** y, a continuación, seleccione **[!UICONTROL Agregar datos]**.

![catálogo](../../../../images/tutorials/create/oracle-object-storage/catalog.png)

### Cuenta existente

Para usar una cuenta existente, seleccione la cuenta de [!DNL Oracle Object Storage] con la que desee crear un nuevo flujo de datos y, a continuación, seleccione **[!UICONTROL Siguiente]** para continuar.

![existente](../../../../images/tutorials/create/oracle-object-storage/existing.png)

### Nueva cuenta

Si va a crear una cuenta nueva, seleccione **[!UICONTROL Cuenta nueva]** y, a continuación, proporcione un nombre, una descripción opcional y sus credenciales de [!DNL Oracle Object Storage]. Cuando termine, seleccione **[!UICONTROL Conectarse al origen]** y deje pasar un tiempo para que se establezca la nueva conexión.

![nuevo](../../../../images/tutorials/create/oracle-object-storage/new.png)

## Pasos siguientes

Al seguir este tutorial, ha establecido una conexión con su cuenta de [!DNL Oracle Object Storage]. Ahora puede continuar con el siguiente tutorial sobre [configuración de un flujo de datos para traer datos de su almacenamiento en la nube a Platform](../../dataflow/batch/cloud-storage.md).
