---
title: Crear una conexión de origen Google PubSub en la interfaz de usuario de
description: Aprenda a crear un conector PubSub de Google mediante la interfaz de usuario de Platform.
exl-id: fb8411f2-ccae-4bb5-b1bf-52b1144534ed
source-git-commit: 79149274c28507041ad89be9d7afdefaedb6aaa0
workflow-type: tm+mt
source-wordcount: '1010'
ht-degree: 0%

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
| Nombre del tema | El nombre de su [!DNL PubSub] suscripción. Entrada [!DNL PubSub], las suscripciones le permiten recibir mensajes, suscribiéndose al tema en el que se han publicado los mensajes. **Nota**: Un solo [!DNL PubSub] la suscripción solo se puede utilizar para un flujo de datos. Para poder crear varios flujos de datos, debe tener varias suscripciones. |
| Nombre de suscripción | El nombre de su [!DNL PubSub] suscripción. Entrada [!DNL PubSub], las suscripciones le permiten recibir mensajes, suscribiéndose al tema en el que se han publicado los mensajes. |

Para obtener más información sobre estos valores, consulte lo siguiente [Autenticación PubSub](https://cloud.google.com/pubsub/docs/authentication) documento. Si utiliza la autenticación basada en cuentas de servicio, consulte lo siguiente [Guía de PubSub](https://cloud.google.com/docs/authentication/production#create_service_account) para ver los pasos sobre cómo generar las credenciales.

>[!TIP]
>
>Si utiliza la autenticación basada en cuentas de servicio, asegúrese de que ha concedido suficiente acceso de usuario a su cuenta de servicio y de que no hay espacios en blanco adicionales en el JSON al copiar y pegar las credenciales.

Una vez que haya recopilado las credenciales necesarias, puede seguir los pasos a continuación para vincular su [!DNL PubSub] a Platform.

## Conecte su [!DNL PubSub] account

En la IU de Platform, seleccione **[!UICONTROL Fuentes]** desde la navegación izquierda para acceder a [!UICONTROL Fuentes] workspace. El [!UICONTROL Catálogo] La pantalla de muestra una variedad de fuentes con las que puede crear una cuenta.

Puede seleccionar la categoría adecuada del catálogo en la parte izquierda de la pantalla. También puede encontrar la fuente específica con la que desea trabajar utilizando la opción de búsqueda.

En el [!UICONTROL Almacenamiento en la nube] categoría, seleccionar **[!UICONTROL Google PubSub]**, y luego seleccione **[!UICONTROL Añadir datos]**.

![El catálogo de fuentes de en la IU del Experience Platform.](../../../../images/tutorials/create/google-pubsub/catalog.png)

El **[!UICONTROL Conectar con Google PubSub]** página. En esta página, puede usar credenciales nuevas o existentes.

### Cuenta existente

Para utilizar una cuenta existente, seleccione la [!DNL PubSub] cuenta con la que desea crear un nuevo flujo de datos y seleccione **[!UICONTROL Siguiente]** para continuar.

![La selección de cuentas existente en el flujo de trabajo de orígenes.](../../../../images/tutorials/create/google-pubsub/existing.png)

### Nueva cuenta

>[!TIP]
>
>Al crear una cuenta con acceso restringido, debe proporcionar al menos uno de los nombres de tema o de suscripción. La autenticación fallará si faltan ambos valores.

Si está creando una cuenta nueva, seleccione **[!UICONTROL Nueva cuenta]** y, a continuación, proporcione un nombre y una descripción opcional para la nueva [!DNL PubSub] cuenta.

![La nueva interfaz de cuenta para el Google PubSub source en el flujo de trabajo de orígenes](../../../../images/tutorials/create/google-pubsub/new.png)

El [!DNL PubSub] fuente permite especificar el tipo de acceso que desea permitir durante la autenticación. Puede configurar su cuenta para que tenga autenticación basada en el proyecto o en temas y suscripciones. La autenticación basada en proyectos permite conceder acceso al proyecto de nivel raíz en la cuenta, mientras que la autenticación basada en temas y suscripciones permite restringir el acceso a un proyecto concreto [!DNL PubSub] tema y suscripción.

>[!BEGINTABS]

>[!TAB Autenticación basada en proyectos]

Para crear una cuenta con acceso a la raíz [!DNL PubSub] carpeta del proyecto. Seleccionar **[!UICONTROL Credenciales de autenticación de Google PubSub]** como su tipo de autenticación y proporcione su ID de proyecto y credenciales. Cuando termine, seleccione **[!UICONTROL Conectar con el origen]** y, a continuación, espere un poco para que se establezca la nueva conexión.

![La nueva interfaz de cuenta para el Google PubSub source con acceso raíz seleccionado.](../../../../images/tutorials/create/google-pubsub/root.png)

>[!TAB Autenticación por tema y por suscripción]

Para crear una cuenta con acceso restringido sólo a un [!DNL PubSub] tema y suscripción, seleccione **[!UICONTROL Credenciales de autenticación de Google PubSub Scoped]** y, a continuación, proporcione sus credenciales, el nombre del tema o el nombre de la suscripción. Cuando termine, seleccione **[!UICONTROL Conectar con el origen]** y, a continuación, espere un poco para que se establezca la nueva conexión.

![La nueva interfaz de cuenta para el origen Google PubSub con acceso de ámbito seleccionado.](../../../../images/tutorials/create/google-pubsub/scoped.png)

>[!ENDTABS]

>[!NOTE]
>
>Principal (funciones) asignado a [!DNL PubSub] Los proyectos de se heredan en todos los temas y suscripciones creados dentro de un [!DNL PubSub] proyecto. Si desea que una entidad de seguridad (función) tenga acceso a un tema específico, dicha entidad de seguridad (función) también debe agregarse a la suscripción correspondiente del tema. Para obtener más información, lea la [[!DNL PubSub] documentación sobre el control de acceso](<https://cloud.google.com/pubsub/docs/access-control>).

## Seleccionar datos

Una autenticación correcta le lleva a la [!UICONTROL Seleccionar datos] paso, donde puede navegar por su [!DNL PubSub] jerarquía de datos y seleccione los datos que desea llevar al Experience Platform.

>[!BEGINTABS]

>[!TAB Autenticación basada en proyectos]

Si se ha autenticado con acceso basado en proyectos, la variable [!UICONTROL Seleccionar datos] La interfaz de mostrará todas las suscripciones dentro del proyecto que tengan un tema adjunto.

![El paso Seleccionar datos del flujo de trabajo de fuentes con autenticación basada en el proyecto.](../../../../images/tutorials/create/google-pubsub/root-folders.png)

>[!TAB Autenticación por tema y por suscripción]

Si se ha autenticado con un tema y acceso basado en suscripción, la variable [!UICONTROL Seleccionar datos] La visualización de la interfaz puede variar según la información proporcionada.

* Si proporciona solo el nombre del tema, la interfaz muestra todos los pares de tema-suscripción que corresponden al tema proporcionado.
* Si solo proporciona el nombre de suscripción, la interfaz muestra todos los pares de tema-suscripción que corresponden al nombre de suscripción proporcionado.
* Si se proporcionan tanto el tema como los nombres de suscripción, la interfaz muestra el par tema-suscripción que corresponde con ambos valores proporcionados.

![El paso Seleccionar datos del flujo de trabajo de fuentes con autenticación por tema y por suscripción.](../../../../images/tutorials/create/google-pubsub/scoped-folders.png)

>[!ENDTABS]

## Pasos siguientes

Al seguir este tutorial, ha creado una conexión entre sus [!DNL PubSub] y Platform. Ahora puede continuar con el siguiente tutorial y [configure un flujo de datos para llevar los datos de streaming de su almacenamiento en la nube a Platform](../../dataflow/streaming/cloud-storage-streaming.md).
