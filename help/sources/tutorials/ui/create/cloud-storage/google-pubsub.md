---
title: Crear una conexión de Google PubSub Source en la interfaz de usuario
description: Obtenga información sobre cómo crear un conector de origen Google PubSub mediante la interfaz de usuario de Platform.
exl-id: fb8411f2-ccae-4bb5-b1bf-52b1144534ed
source-git-commit: 2b72d384e8edd91c662364dfac31ce4edff79172
workflow-type: tm+mt
source-wordcount: '658'
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
| Proyecto  ID | ID del proyecto necesario para la autenticación [!DNL PubSub]. |
| Credenciales | El ID de credencial o clave privada necesario para la autenticación [!DNL PubSub]. |
| ID del tema | El ID de la variable [!DNL PubSub] recurso que representa una fuente de mensajes. Debe especificar un ID de tema si desea proporcionar acceso a un flujo de datos específico de su [!DNL Google PubSub] fuente. |
| ID de suscripción | El ID de su [!DNL PubSub] suscripción. En [!DNL PubSub], las suscripciones le permiten recibir mensajes, suscribiéndose al tema en el que se han publicado los mensajes. |

Para obtener más información sobre estos valores, consulte [PubSub authentication](https://cloud.google.com/pubsub/docs/authentication) documento. Si utiliza la autenticación basada en cuentas de servicio, consulte lo siguiente [Guía de PubSub](https://cloud.google.com/docs/authentication/production#create_service_account) para ver los pasos sobre cómo generar sus credenciales.

>[!TIP]
>
>Si utiliza la autenticación basada en cuentas de servicio, asegúrese de que ha concedido suficiente acceso de usuario a su cuenta de servicio y de que no hay espacios en blanco adicionales en el JSON, al copiar y pegar sus credenciales.

Una vez que haya reunido las credenciales necesarias, puede seguir los pasos a continuación para vincular sus [!DNL PubSub] a Platform.

## Conecte su [!DNL PubSub] account

En la interfaz de usuario de Platform, seleccione **[!UICONTROL Fuentes]** en la barra de navegación izquierda para acceder a la [!UICONTROL Fuentes] espacio de trabajo. La variable [!UICONTROL Catálogo] muestra una variedad de fuentes con las que puede crear una cuenta.

Puede seleccionar la categoría adecuada del catálogo en la parte izquierda de la pantalla. Alternativamente, puede encontrar la fuente específica con la que desea trabajar usando la opción de búsqueda.

En el [!UICONTROL Almacenamiento en la nube] categoría, seleccione **[!UICONTROL Google PubSub]** y, a continuación, seleccione **[!UICONTROL Añadir datos]**.

![El catálogo de fuentes en la interfaz de usuario del Experience Platform.](../../../../images/tutorials/create/google-pubsub/catalog.png)

La variable **[!UICONTROL Conectarse a Google PubSub]** se abre. En esta página, puede usar credenciales nuevas o existentes.

### Cuenta existente

Para usar una cuenta existente, seleccione la opción [!DNL PubSub] cuenta con la que desee crear un nuevo flujo de datos y, a continuación, seleccione **[!UICONTROL Siguiente]** para continuar.

![La selección de cuenta existente en el flujo de trabajo de fuentes.](../../../../images/tutorials/create/google-pubsub/existing.png)

### Nueva cuenta

Si está creando una cuenta nueva, seleccione **[!UICONTROL Nueva cuenta]** y, a continuación, proporcione un nombre, una descripción opcional y su [!DNL PubSub] credenciales de autenticación en el formulario de entrada. Durante este paso, puede definir los datos a los que tiene acceso su cuenta proporcionando un ID de tema. Solo se puede acceder a las suscripciones asociadas a ese ID de tema.

>[!NOTE]
>
>El principal (funciones) asignado a un proyecto pubsub se hereda en todos los temas y suscripciones creados dentro de un [!DNL PubSub] proyecto. Si desea agregar una entidad de seguridad (función) para tener acceso a un tema específico, esa entidad de seguridad (función) también debe agregarse a la suscripción correspondiente del tema. Para obtener más información, lea la [[!DNL PubSub] documentación sobre control de acceso](https://cloud.google.com/pubsub/docs/access-control).

Cuando termine, seleccione **[!UICONTROL Conectar a origen]** y, a continuación, permita que la nueva conexión se establezca durante algún tiempo.

![La nueva interfaz de cuenta en el flujo de trabajo de fuentes.](../../../../images/tutorials/create/google-pubsub/new.png)

## Pasos siguientes

Al seguir este tutorial, ha creado una conexión entre sus [!DNL PubSub] cuenta y plataforma. Ahora puede continuar con el siguiente tutorial y [configure un flujo de datos para incorporar datos de flujo continuo desde el almacenamiento en la nube a Platform](../../dataflow/streaming/cloud-storage-streaming.md).
