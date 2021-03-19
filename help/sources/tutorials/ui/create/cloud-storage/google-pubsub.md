---
keywords: Experience Platform;inicio;temas populares;Google PubSub;google pubsub
solution: Experience Platform
title: Crear una conexión de Google PubSub Source en la interfaz de usuario
topic: sobre validación
type: Tutorial
description: Aprenda a crear un conector de origen Google PubSub utilizando la interfaz de usuario de Platform.
translation-type: tm+mt
source-git-commit: b5358ce206888c413035b46fe751520fd9aefb14
workflow-type: tm+mt
source-wordcount: '492'
ht-degree: 1%

---


# Crear una conexión de origen [!DNL Google PubSub] en la interfaz de usuario

>[!NOTE]
>
> El conector [!DNL Google PubSub] está en versión beta. Consulte la [información general sobre fuentes](../../../../home.md#terms-and-conditions) para obtener más información sobre el uso de conectores con etiqueta beta.

Este tutorial proporciona los pasos para crear un [!DNL Google PubSub] (en adelante denominado &quot;[!DNL PubSub]&quot;) mediante la interfaz de usuario de Platform.

## Primeros pasos

Este tutorial requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [Fuentes](../../../../home.md): Experience Platform permite la ingesta de datos de varias fuentes, al mismo tiempo que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de Platform.
* [Simuladores para pruebas](../../../../../sandboxes/home.md): Experience Platform proporciona entornos limitados virtuales que dividen una sola instancia de Platform en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

Si ya tiene una conexión [!DNL PubSub] válida, puede omitir el resto de este documento y continuar con el tutorial sobre la [configuración de un flujo de datos](../../dataflow/batch/cloud-storage.md).

### Recopilar las credenciales necesarias

Para conectar [!DNL PubSub] a Platform, debe proporcionar un valor válido para las siguientes credenciales:

| Credencial | Descripción |
| ---------- | ----------- |
| `projectId` | El ID de proyecto necesario para autenticarse [!DNL PubSub]. |
| `credentials` | El ID de credencial o clave privada necesario para autenticar [!DNL PubSub]. |

Para obtener más información sobre estos valores, consulte el siguiente documento [PubSub authentication](https://cloud.google.com/pubsub/docs/authentication). Si utiliza la autenticación basada en cuentas de servicio, consulte la siguiente [guía de PubSub](https://cloud.google.com/docs/authentication/production#create_service_account) para ver los pasos sobre cómo generar sus credenciales.

>[!TIP]
>
>Si utiliza la autenticación basada en cuentas de servicio, asegúrese de que ha concedido suficiente acceso de usuario a su cuenta de servicio y de que no hay espacios en blanco adicionales en el JSON, al copiar y pegar sus credenciales.

Una vez que haya reunido las credenciales necesarias, puede seguir los pasos a continuación para vincular su cuenta [!DNL PubSub] a Platform.

## Conecte su cuenta [!DNL PubSub]

En la [Platform UI](https://platform.adobe.com), seleccione **[!UICONTROL Sources]** en la barra de navegación izquierda para acceder al espacio de trabajo [!UICONTROL Sources]. La pantalla [!UICONTROL Catalog] muestra una variedad de fuentes para las que puede crear una cuenta.

Puede seleccionar la categoría adecuada del catálogo en la parte izquierda de la pantalla. También puede encontrar la fuente específica con la que desea trabajar mediante la barra de búsqueda.

En la categoría [!UICONTROL Cloud storage], seleccione **[!UICONTROL Google PubSub]** y, a continuación, seleccione **[!UICONTROL Add data]**.

![catálogo](../../../../images/tutorials/create/google-pubsub/catalog.png)

Aparece la página **[!UICONTROL Connect to Google PubSub]**. En esta página, puede usar credenciales nuevas o existentes.

### Cuenta existente

Para utilizar una cuenta existente, seleccione la cuenta [!DNL PubSub] con la que desea crear un nuevo flujo de datos y, a continuación, seleccione **[!UICONTROL Next]** para continuar.

![existente](../../../../images/tutorials/create/google-pubsub/existing.png)

### Nueva cuenta

Si va a crear una cuenta nueva, seleccione **[!UICONTROL New account]** y, a continuación, proporcione un nombre, una descripción opcional y las credenciales de autenticación [!DNL PubSub] en el formulario de entrada. Cuando termine, seleccione **[!UICONTROL Connect to source]** y, a continuación, deje que se establezca la nueva conexión.

![new](../../../../images/tutorials/create/google-pubsub/new.png)

## Pasos siguientes

Al seguir este tutorial, ha creado una conexión entre su cuenta [!DNL PubSub] y Platform. Ahora puede continuar con el siguiente tutorial y [configurar un flujo de datos para incorporar datos de flujo continuo del almacenamiento en la nube a Platform](../../dataflow/streaming/cloud-storage-streaming.md).
