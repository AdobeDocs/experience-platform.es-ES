---
keywords: Experience Platform;inicio;temas populares;Google PubSub;google pubsub
solution: Experience Platform
title: Crear una conexión de Google PubSub Source en la interfaz de usuario
type: Tutorial
description: Obtenga información sobre cómo crear un conector de origen Google PubSub mediante la interfaz de usuario de Platform.
exl-id: fb8411f2-ccae-4bb5-b1bf-52b1144534ed
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '493'
ht-degree: 1%

---

# Cree un [!DNL Google PubSub] conexión de origen en la interfaz de usuario

Este tutorial proporciona los pasos para crear un [!DNL Google PubSub] (en lo sucesivo, &quot;el[!DNL PubSub]&quot;) utilizando la interfaz de usuario de Platform.

## Primeros pasos

Este tutorial requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [Fuentes](../../../../home.md): Experience Platform permite la ingesta de datos de varias fuentes, al mismo tiempo que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de Platform.
* [Sandboxes](../../../../../sandboxes/home.md): Experience Platform proporciona entornos limitados virtuales que dividen una sola instancia de Platform en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

Si ya tiene una [!DNL PubSub] conexión, puede omitir el resto de este documento y continuar con el tutorial en [configuración de un flujo de datos](../../dataflow/batch/cloud-storage.md).

### Recopilar las credenciales necesarias

Para conectarse [!DNL PubSub] para Platform, debe proporcionar un valor válido para las siguientes credenciales:

| Credencial | Descripción |
| ---------- | ----------- |
| `projectId` | ID del proyecto necesario para la autenticación [!DNL PubSub]. |
| `credentials` | El ID de credencial o clave privada necesario para la autenticación [!DNL PubSub]. |

Para obtener más información sobre estos valores, consulte [PubSub authentication](https://cloud.google.com/pubsub/docs/authentication) documento. Si utiliza la autenticación basada en cuentas de servicio, consulte lo siguiente [Guía de PubSub](https://cloud.google.com/docs/authentication/production#create_service_account) para ver los pasos sobre cómo generar sus credenciales.

>[!TIP]
>
>Si utiliza la autenticación basada en cuentas de servicio, asegúrese de que ha concedido suficiente acceso de usuario a su cuenta de servicio y de que no hay espacios en blanco adicionales en el JSON, al copiar y pegar sus credenciales.

Una vez que haya reunido las credenciales necesarias, puede seguir los pasos a continuación para vincular sus [!DNL PubSub] a Platform.

## Conecte su [!DNL PubSub] account

En el [Interfaz de usuario de Platform](https://platform.adobe.com), seleccione **[!UICONTROL Fuentes]** en la barra de navegación izquierda para acceder a la [!UICONTROL Fuentes] espacio de trabajo. La variable [!UICONTROL Catálogo] muestra una variedad de fuentes para las que puede crear una cuenta.

Puede seleccionar la categoría adecuada del catálogo en la parte izquierda de la pantalla. También puede encontrar la fuente específica con la que desea trabajar mediante la barra de búsqueda.

En el [!UICONTROL Almacenamiento en la nube] categoría, seleccione **[!UICONTROL Google PubSub]** y, a continuación, seleccione **[!UICONTROL Añadir datos]**.

![catálogo](../../../../images/tutorials/create/google-pubsub/catalog.png)

La variable **[!UICONTROL Conectarse a Google PubSub]** se abre. En esta página, puede usar credenciales nuevas o existentes.

### Cuenta existente

Para usar una cuenta existente, seleccione la opción [!DNL PubSub] cuenta con la que desee crear un nuevo flujo de datos y, a continuación, seleccione **[!UICONTROL Siguiente]** para continuar.

![existente](../../../../images/tutorials/create/google-pubsub/existing.png)

### Nueva cuenta

Si está creando una cuenta nueva, seleccione **[!UICONTROL Nueva cuenta]** y, a continuación, proporcione un nombre, una descripción opcional y su [!DNL PubSub] credenciales de autenticación en el formulario de entrada. Cuando termine, seleccione **[!UICONTROL Conectar a origen]** y, a continuación, permita que la nueva conexión se establezca durante algún tiempo.

![new](../../../../images/tutorials/create/google-pubsub/new.png)

## Pasos siguientes

Al seguir este tutorial, ha creado una conexión entre sus [!DNL PubSub] cuenta y plataforma. Ahora puede continuar con el siguiente tutorial y [configure un flujo de datos para incorporar datos de flujo continuo desde el almacenamiento en la nube a Platform](../../dataflow/streaming/cloud-storage-streaming.md).
