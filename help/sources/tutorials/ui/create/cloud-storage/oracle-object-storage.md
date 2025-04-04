---
keywords: Experience Platform;inicio;temas populares;Oracle Object Storage;oracle object storage
solution: Experience Platform
title: Creación de una conexión de Source de Oracle Object Storage en la interfaz de usuario de
type: Tutorial
description: Obtenga información sobre cómo crear una conexión de origen de Oracle Object Storage mediante la interfaz de usuario de Adobe Experience Platform.
exl-id: 32284163-5dde-4171-8977-f76ceeebcef2
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '459'
ht-degree: 1%

---

# Crear una conexión de Source [!DNL Oracle Object Storage] en la interfaz de usuario

Este tutorial proporciona los pasos para crear una conexión de origen [!DNL Oracle Object Storage] mediante la interfaz de usuario de Adobe Experience Platform.

## Introducción

Este tutorial requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [Fuentes](../../../../home.md): Experience Platform permite la ingesta de datos de varias fuentes al tiempo que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de Experience Platform.
* [Zonas protegidas](../../../../../sandboxes/home.md): Experience Platform proporciona zonas protegidas virtuales que dividen una sola instancia de Experience Platform en entornos virtuales independientes para ayudar a desarrollar y evolucionar aplicaciones de experiencia digital.

### Recopilar credenciales necesarias

Para conectarse a [!DNL Oracle Object Storage], debe proporcionar valores para las siguientes propiedades de conexión:

| Credencial | Descripción |
| ---------- | ----------- |
| `serviceUrl` | Extremo [!DNL Oracle Object Storage] necesario para la autenticación. El formato del extremo es: `https://{OBJECT_STORAGE_NAMESPACE}.compat.objectstorage.eu-frankfurt-1.oraclecloud.com` |
| `accessKey` | La clave de acceso [!DNL Oracle Object Storage] necesaria para la autenticación. |
| `secretKey` | Se requiere la contraseña [!DNL Oracle Object Storage] para la autenticación. |
| `bucketName` | Se requiere el nombre de contenedor permitido si el usuario tiene acceso restringido. El nombre del contenedor debe tener entre tres y 63 caracteres, debe comenzar y finalizar con una letra o un número, y solo puede contener letras minúsculas, números o guiones (`-`). El nombre del contenedor no puede tener el formato de una dirección IP. |
| `folderPath` | La ruta de carpeta permitida requerida si el usuario tiene acceso restringido. |

Para obtener más información sobre cómo obtener estos valores, consulte la [guía de autenticación de Oracle Object Storage](https://docs.oracle.com/en-us/iaas/Content/Identity/Concepts/usercredentials.htm#User_Credentials).

Una vez que haya recopilado las credenciales necesarias, puede seguir los pasos a continuación para crear una nueva cuenta de Oracle Object Storage para conectarse a Experience Platform.

## Conectar con Oracle Object Storage

En la interfaz de usuario de Experience Platform, seleccione **[!UICONTROL Fuentes]** en el panel de navegación izquierdo para acceder al área de trabajo [!UICONTROL Fuentes]. La pantalla [!UICONTROL Catálogo] muestra una variedad de orígenes con los que puede crear una cuenta.

Puede seleccionar la categoría adecuada del catálogo en la parte izquierda de la pantalla. También puede encontrar la fuente específica con la que desea trabajar en la barra de búsqueda.

En la categoría [!UICONTROL Almacenamiento en la nube], seleccione **[!UICONTROL Almacenamiento de objetos de Oracle]** y luego seleccione **[!UICONTROL Agregar datos]**.

![catálogo](../../../../images/tutorials/create/oracle-object-storage/catalog.png)

### Cuenta existente

Para usar una cuenta existente, seleccione la cuenta de [!DNL Oracle Object Storage] con la que desee crear un nuevo flujo de datos y, a continuación, seleccione **[!UICONTROL Siguiente]** para continuar.

![existente](../../../../images/tutorials/create/oracle-object-storage/existing.png)

### Nueva cuenta

Si va a crear una cuenta nueva, seleccione **[!UICONTROL Cuenta nueva]** y, a continuación, proporcione un nombre, una descripción opcional y sus credenciales de [!DNL Oracle Object Storage]. Cuando termine, seleccione **[!UICONTROL Conectarse al origen]** y deje pasar un tiempo para que se establezca la nueva conexión.

![nuevo](../../../../images/tutorials/create/oracle-object-storage/new.png)

## Pasos siguientes

Al seguir este tutorial, ha establecido una conexión con su cuenta de [!DNL Oracle Object Storage]. Ahora puede continuar con el siguiente tutorial sobre [configuración de un flujo de datos para traer datos de su almacenamiento en la nube a Experience Platform](../../dataflow/batch/cloud-storage.md).
