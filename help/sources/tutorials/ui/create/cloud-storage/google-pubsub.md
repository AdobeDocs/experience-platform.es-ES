---
title: Crear una conexión de origen Google PubSub en la interfaz de usuario de
description: Aprenda a crear un conector PubSub de Google mediante la interfaz de usuario de Platform.
exl-id: fb8411f2-ccae-4bb5-b1bf-52b1144534ed
source-git-commit: 2b72d384e8edd91c662364dfac31ce4edff79172
workflow-type: tm+mt
source-wordcount: '658'
ht-degree: 1%

---

# Crear un [!DNL Google PubSub] conexión de origen en la interfaz de usuario

Este tutorial proporciona los pasos para crear una [!DNL Google PubSub] (en lo sucesivo, &quot;[!DNL PubSub]&quot;) mediante la interfaz de usuario de Platform.

## Primeros pasos

Este tutorial requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [Fuentes](../../../../home.md): Experience Platform permite la ingesta de datos desde varias fuentes y, al mismo tiempo, le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de Platform.
* [Zonas protegidas](../../../../../sandboxes/home.md): El Experience Platform proporciona entornos limitados virtuales que dividen una sola instancia de Platform en entornos virtuales independientes para ayudar a desarrollar y evolucionar aplicaciones de experiencia digital.

Si ya tiene un válido [!DNL PubSub] conexión, puede omitir el resto de este documento y continuar con el tutorial sobre [configuración de un flujo de datos](../../dataflow/batch/cloud-storage.md).

### Recopilar credenciales necesarias

Para poder conectarse [!DNL PubSub] En Platform, debe proporcionar un valor válido para las siguientes credenciales:

| Credencial | Descripción |
| ---------- | ----------- |
| Proyecto  ID | El ID de proyecto necesario para la autenticación [!DNL PubSub]. |
| Credenciales | La credencial o el ID de clave privada necesarios para la autenticación [!DNL PubSub]. |
| ID de tema | El ID de [!DNL PubSub] que representa una fuente de mensajes. Debe especificar un ID de tema si desea proporcionar acceso a un flujo de datos específico en su [!DNL Google PubSub] origen. |
| ID de suscripción | El ID de su [!DNL PubSub] suscripción. Entrada [!DNL PubSub], las suscripciones le permiten recibir mensajes, suscribiéndose al tema en el que se han publicado los mensajes. |

Para obtener más información sobre estos valores, consulte lo siguiente [Autenticación PubSub](https://cloud.google.com/pubsub/docs/authentication) documento. Si utiliza la autenticación basada en cuentas de servicio, consulte lo siguiente [Guía de PubSub](https://cloud.google.com/docs/authentication/production#create_service_account) para ver los pasos sobre cómo generar las credenciales.

>[!TIP]
>
>Si utiliza la autenticación basada en cuentas de servicio, asegúrese de que ha concedido suficiente acceso de usuario a su cuenta de servicio y de que no hay espacios en blanco adicionales en el JSON al copiar y pegar las credenciales.

Una vez que haya recopilado las credenciales necesarias, puede seguir los pasos a continuación para vincular su [!DNL PubSub] a Platform.

## Conecte su [!DNL PubSub] account

En la IU de Platform, seleccione **[!UICONTROL Fuentes]** desde la barra de navegación izquierda para acceder a [!UICONTROL Fuentes] workspace. El [!UICONTROL Catálogo] La pantalla muestra una variedad de fuentes con las que puede crear una cuenta.

Puede seleccionar la categoría adecuada del catálogo en la parte izquierda de la pantalla. También puede encontrar la fuente específica con la que desea trabajar utilizando la opción de búsqueda.

En el [!UICONTROL Almacenamiento en la nube] categoría, seleccionar **[!UICONTROL Google PubSub]**, y luego seleccione **[!UICONTROL Añadir datos]**.

![El catálogo de fuentes de en la IU del Experience Platform.](../../../../images/tutorials/create/google-pubsub/catalog.png)

El **[!UICONTROL Conectar con Google PubSub]** página. En esta página, puede usar credenciales nuevas o existentes.

### Cuenta existente

Para utilizar una cuenta existente, seleccione la [!DNL PubSub] cuenta con la que desea crear un nuevo flujo de datos y seleccione **[!UICONTROL Siguiente]** para continuar.

![La selección de cuentas existente en el flujo de trabajo de orígenes.](../../../../images/tutorials/create/google-pubsub/existing.png)

### Nueva cuenta

Si está creando una cuenta nueva, seleccione **[!UICONTROL Nueva cuenta]** y, a continuación, proporcione un nombre, una descripción opcional y su [!DNL PubSub] credenciales de autenticación en el formulario de entrada. Durante este paso, puede definir los datos a los que tiene acceso su cuenta proporcionando un ID de tema. Solo se puede acceder a las suscripciones asociadas con ese ID de tema.

>[!NOTE]
>
>Las principales (funciones) asignadas a un subproyecto público se heredan en todos los temas y suscripciones creados dentro de un [!DNL PubSub] proyecto. Si desea agregar un principal (función) para tener acceso a un tema específico, ese principal (función) también debe agregarse a la suscripción correspondiente del tema. Para obtener más información, lea la [[!DNL PubSub] documentación sobre el control de acceso](https://cloud.google.com/pubsub/docs/access-control).

Cuando termine, seleccione **[!UICONTROL Conectar con el origen]** y, a continuación, espere un poco para que se establezca la nueva conexión.

![La nueva interfaz de cuenta en el flujo de trabajo de orígenes.](../../../../images/tutorials/create/google-pubsub/new.png)

## Pasos siguientes

Al seguir este tutorial, ha creado una conexión entre sus [!DNL PubSub] y Platform. Ahora puede continuar con el siguiente tutorial y [configure un flujo de datos para llevar los datos de streaming de su almacenamiento en la nube a Platform](../../dataflow/streaming/cloud-storage-streaming.md).
