---
keywords: Experience Platform;inicio;temas populares;Google PubSub;google pubsub
solution: Experience Platform
title: Creación de una conexión de origen PubSub de Google en la interfaz de usuario
topic: sobre validación
type: Tutorial
description: Obtenga información sobre cómo crear un conector de origen Google PubSub mediante la interfaz de usuario de la plataforma.
translation-type: tm+mt
source-git-commit: 0af90253f04377149986aedf2e9d3012ca06d4f8
workflow-type: tm+mt
source-wordcount: '445'
ht-degree: 1%

---


# Crear una conexión de origen [!DNL Google PubSub] en la interfaz de usuario

>[!NOTE]
>
> El conector [!DNL Google PubSub] está en versión beta. Consulte la [información general de las fuentes](../../../../home.md#terms-and-conditions) para obtener más información sobre el uso de conectores con etiquetas beta.

Este tutorial proporciona los pasos para crear un [!DNL Google PubSub] (en adelante denominado &quot;[!DNL PubSub]&quot;) mediante la interfaz de usuario de la plataforma.

## Primeros pasos

Este tutorial requiere un conocimiento práctico de los siguientes componentes de Adobe Experience Platform:

* [Fuentes](../../../../home.md): Experience Platform permite la ingesta de datos desde diversas fuentes, al tiempo que le permite estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de plataforma.
* [Simuladores](../../../../../sandboxes/home.md): Experience Platform proporciona entornos limitados virtuales que dividen una sola instancia de Plataforma en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

Si ya tiene una conexión [!DNL PubSub] válida, puede omitir el resto de este documento y continuar con el tutorial sobre [configuración de un flujo de datos](../../dataflow/batch/cloud-storage.md).

### Recopilar las credenciales necesarias

Para conectar [!DNL PubSub] a Platform, debe proporcionar un valor válido para las siguientes credenciales:

| Credencial | Descripción |
| ---------- | ----------- |
| `projectId` | ID de proyecto necesario para autenticar [!DNL PubSub]. |
| `credentials` | La credencial o clave necesaria para autenticar [!DNL PubSub]. |

Para obtener más información sobre estos valores, consulte el siguiente documento [de autenticación PubSub](https://cloud.google.com/pubsub/docs/authentication).

Una vez recopiladas las credenciales requeridas, puede seguir los pasos a continuación para vincular su cuenta [!DNL Blob] a la plataforma.

## Conectar su cuenta [!DNL PubSub]

En la [IU de la plataforma](https://platform.adobe.com), seleccione **[!UICONTROL Fuentes]** en la barra de navegación izquierda para acceder al espacio de trabajo [!UICONTROL Fuentes]. La pantalla [!UICONTROL Catálogo] muestra una variedad de fuentes con las que puede crear una cuenta.

Puede seleccionar la categoría adecuada en el catálogo a la izquierda de la pantalla. También puede encontrar la fuente específica con la que desea trabajar mediante la barra de búsqueda.

En la categoría [!UICONTROL Cloud almacenamiento], seleccione **[!UICONTROL Google PubSub]** y, a continuación, seleccione **[!UICONTROL Añadir datos]**.

![catálogo](../../../../images/tutorials/create/google-pubsub/catalog.png)

Aparece la página **[!UICONTROL Conectar con Google PubSub]**. En esta página, puede usar credenciales nuevas o existentes.

### Cuenta existente

Para utilizar una cuenta existente, seleccione la cuenta [!DNL PubSub] con la que desea crear un nuevo flujo de datos y, a continuación, seleccione **[!UICONTROL Siguiente]** para continuar.

![existente](../../../../images/tutorials/create/google-pubsub/existing.png)

### Nueva cuenta

Si va a crear una cuenta nueva, seleccione **[!UICONTROL Nueva cuenta]** y, a continuación, proporcione un nombre, una descripción opcional y las credenciales de autenticación [!DNL PubSub] en el formulario de entrada. Cuando termine, seleccione **[!UICONTROL Conectar con origen]** y, a continuación, deje transcurrir un tiempo para que se establezca la nueva conexión.

![new](../../../../images/tutorials/create/google-pubsub/new.png)

## Pasos siguientes

Siguiendo este tutorial, se ha creado una conexión entre la cuenta [!DNL PubSub] y la plataforma. Ahora puede continuar con el siguiente tutorial y [configurar un flujo de datos para que los datos de flujo continuo de su almacenamiento de nube pasen a la plataforma](../../dataflow/streaming/cloud-storage-streaming.md).
