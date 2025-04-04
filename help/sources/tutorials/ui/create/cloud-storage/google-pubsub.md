---
title: Crear una conexión de Google PubSub Source en la interfaz de usuario de
description: Aprenda a crear un conector PubSub de Google mediante la interfaz de usuario de Experience Platform.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: fb8411f2-ccae-4bb5-b1bf-52b1144534ed
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1106'
ht-degree: 1%

---

# Crear una conexión de origen [!DNL Google PubSub] en la interfaz de usuario

>[!IMPORTANT]
>
>El origen [!DNL Google PubSub] está disponible en el catálogo de orígenes para los usuarios que han adquirido Real-Time Customer Data Platform Ultimate.

Este tutorial proporciona los pasos para crear un(a) [!DNL Google PubSub] (denominado(a) &quot;[!DNL PubSub]&quot;) mediante la interfaz de usuario de Experience Platform.

## Introducción 

Este tutorial requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [Fuentes](../../../../home.md): Experience Platform permite la ingesta de datos de varias fuentes al tiempo que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de Experience Platform.
* [Zonas protegidas](../../../../../sandboxes/home.md): Experience Platform proporciona zonas protegidas virtuales que dividen una sola instancia de Experience Platform en entornos virtuales independientes para ayudar a desarrollar y evolucionar aplicaciones de experiencia digital.

Si ya tiene una conexión [!DNL PubSub] válida, puede omitir el resto de este documento y continuar con el tutorial sobre [configuración de un flujo de datos](../../dataflow/batch/cloud-storage.md).

### Recopilar credenciales necesarias

Debe proporcionar valores para las propiedades de conexión que se indican a continuación a fin de conectar su cuenta de [!DNL PubSub] a Experience Platform. Para obtener más información sobre la autenticación y la configuración de requisitos previos, lea la [[!DNL PubSub source] descripción general](../../../../connectors/cloud-storage/google-pubsub.md#prerequisites).


>[!BEGINTABS]

>[!TAB Autenticación basada en proyecto]

| Credencial | Descripción |
| --- | --- |
| Identificador de proyecto | Identificador de proyecto necesario para autenticar [!DNL PubSub]. |
| Credenciales | Credencial necesaria para autenticar [!DNL PubSub]. Debe asegurarse de colocar el archivo JSON completo después de eliminar los espacios en blanco de las credenciales. |

>[!TAB Autenticación basada en temas y suscripciones]

| Credencial | Descripción |
| --- | --- |
| Credenciales | Credencial necesaria para autenticar [!DNL PubSub]. Debe asegurarse de colocar el archivo JSON completo después de eliminar los espacios en blanco de las credenciales. |
| Nombre del tema | Nombre de su suscripción a [!DNL PubSub]. En [!DNL PubSub], las suscripciones le permiten recibir mensajes, mediante suscripción al tema en el que se han publicado los mensajes. **Nota**: una sola suscripción de [!DNL PubSub] solo se puede usar para un flujo de datos. Para poder crear varios flujos de datos, debe tener varias suscripciones. |
| Nombre de suscripción | Nombre de su suscripción a [!DNL PubSub]. En [!DNL PubSub], las suscripciones le permiten recibir mensajes, mediante suscripción al tema en el que se han publicado los mensajes. |

>[!ENDTABS]

Para obtener más información sobre estos valores, consulte el siguiente documento [Autenticación PubSub](https://cloud.google.com/pubsub/docs/authentication). Si está usando autenticación basada en cuentas de servicio, consulte la siguiente [guía de PubSub](https://cloud.google.com/docs/authentication/production#create_service_account) para ver los pasos sobre cómo generar sus credenciales.

>[!TIP]
>
>Si utiliza la autenticación basada en cuentas de servicio, asegúrese de que ha concedido suficiente acceso de usuario a su cuenta de servicio y de que no hay espacios en blanco adicionales en el JSON al copiar y pegar las credenciales.

Una vez que haya recopilado las credenciales necesarias, puede seguir los pasos a continuación para vincular su cuenta de [!DNL PubSub] a Experience Platform.

## Conectar su cuenta de [!DNL PubSub]

En la interfaz de usuario de Experience Platform, seleccione **[!UICONTROL Fuentes]** en el panel de navegación izquierdo para acceder al área de trabajo [!UICONTROL Fuentes]. La pantalla [!UICONTROL Catálogo] muestra una variedad de orígenes con los que puede crear una cuenta.

Puede seleccionar la categoría adecuada del catálogo en la parte izquierda de la pantalla. También puede encontrar la fuente específica con la que desea trabajar utilizando la opción de búsqueda.

En la categoría [!UICONTROL Almacenamiento en la nube], seleccione **[!UICONTROL Google PubSub]** y, a continuación, seleccione **[!UICONTROL Agregar datos]**.

![El catálogo de orígenes en la interfaz de usuario de Experience Platform.](../../../../images/tutorials/create/google-pubsub/catalog.png)

Aparecerá la página **[!UICONTROL Conectarse a Google PubSub]**. En esta página, puede usar credenciales nuevas o existentes.

### Cuenta existente

Para usar una cuenta existente, seleccione la cuenta de [!DNL PubSub] con la que desee crear un nuevo flujo de datos y, a continuación, seleccione **[!UICONTROL Siguiente]** para continuar.

![Selección de cuenta existente en el flujo de trabajo de orígenes.](../../../../images/tutorials/create/google-pubsub/existing.png)

### Nueva cuenta

>[!TIP]
>
>* Al crear una cuenta con acceso restringido, debe proporcionar al menos uno de los nombres de tema o de suscripción. La autenticación fallará si faltan ambos valores.
>* Una vez creada, no se puede cambiar el tipo de autenticación de una conexión base de [!DNL Google PubSub]. Para cambiar el tipo de autenticación, debe crear una nueva conexión base.

Si va a crear una cuenta nueva, seleccione **[!UICONTROL Nueva cuenta]** y, a continuación, proporcione un nombre y una descripción opcional para la nueva cuenta de [!DNL PubSub].

![La nueva interfaz de cuenta para el origen Google PubSub en el flujo de trabajo de orígenes](../../../../images/tutorials/create/google-pubsub/new.png)

El origen [!DNL PubSub] le permite especificar el tipo de acceso que desea permitir durante la autenticación. Puede configurar su cuenta para que tenga autenticación basada en el proyecto o en temas y suscripciones. La autenticación basada en proyectos le permite conceder acceso al proyecto de nivel raíz en su cuenta, mientras que la autenticación basada en temas y suscripciones le permite restringir el acceso a un tema y suscripción de [!DNL PubSub] en particular.

>[!BEGINTABS]

>[!TAB Autenticación basada en proyecto]

Para crear una cuenta con acceso a la carpeta raíz del proyecto [!DNL PubSub]. Seleccione **[!UICONTROL Credenciales de autenticación de Google PubSub]** como tipo de autenticación y proporcione su ID de proyecto y credenciales. Cuando termine, seleccione **[!UICONTROL Conectarse al origen]** y deje pasar un tiempo para que se establezca la nueva conexión.

![Interfaz de la nueva cuenta para el origen PubSub de Google con acceso raíz seleccionado.](../../../../images/tutorials/create/google-pubsub/root.png)

>[!TAB Autenticación basada en temas y suscripciones]

Para crear una cuenta con acceso restringido solo a un tema y suscripción de [!DNL PubSub] en particular, seleccione **[!UICONTROL Credenciales de autenticación de ámbito PubSub de Google]** y, a continuación, proporcione sus credenciales, nombre del tema y/o nombre de suscripción. Cuando termine, seleccione **[!UICONTROL Conectarse al origen]** y deje pasar un tiempo para que se establezca la nueva conexión.

![Interfaz de la nueva cuenta para el origen PubSub de Google con acceso de ámbito seleccionado.](../../../../images/tutorials/create/google-pubsub/scoped.png)

>[!ENDTABS]

>[!NOTE]
>
>El principal (funciones) asignado a un proyecto [!DNL PubSub] se hereda en todos los temas y suscripciones creados dentro de un proyecto [!DNL PubSub]. Si desea que una entidad de seguridad (función) tenga acceso a un tema específico, dicha entidad de seguridad (función) también debe agregarse a la suscripción correspondiente del tema. Para obtener más información, lea la [[!DNL PubSub] documentación sobre el control de acceso](<https://cloud.google.com/pubsub/docs/access-control>).

## Seleccionar datos

Una autenticación correcta le lleva al paso [!UICONTROL Seleccionar datos], donde puede navegar por la jerarquía de datos de [!DNL PubSub] y seleccionar los datos que desea llevar a Experience Platform.

>[!BEGINTABS]

>[!TAB Autenticación basada en proyecto]

Si se ha autenticado con acceso basado en proyectos, la interfaz [!UICONTROL Select data] mostrará todas las suscripciones dentro del proyecto que tengan un tema adjunto a ellas.

![Paso de selección de datos del flujo de trabajo de orígenes con autenticación basada en proyecto.](../../../../images/tutorials/create/google-pubsub/root-folders.png)

>[!TAB Autenticación basada en temas y suscripciones]

Si se ha autenticado con un tema y acceso basado en suscripción, la visualización de la interfaz [!UICONTROL Seleccionar datos] puede variar según la información que haya proporcionado.

* Si proporciona solo el nombre del tema, la interfaz muestra todos los pares de tema-suscripción que corresponden al tema proporcionado.
* Si solo proporciona el nombre de suscripción, la interfaz muestra todos los pares de tema-suscripción que corresponden al nombre de suscripción proporcionado.
* Si se proporcionan tanto el tema como los nombres de suscripción, la interfaz muestra el par tema-suscripción que corresponde con ambos valores proporcionados.

![Paso de selección de datos del flujo de trabajo de orígenes con autenticación por tema y por suscripción.](../../../../images/tutorials/create/google-pubsub/scoped-folders.png)

>[!ENDTABS]

## Pasos siguientes

Al seguir este tutorial, ha creado una conexión entre su cuenta de [!DNL PubSub] y Experience Platform. Ahora puede continuar con el siguiente tutorial y [configurar un flujo de datos para traer los datos de streaming de su almacenamiento en la nube a Experience Platform](../../dataflow/streaming/cloud-storage-streaming.md).
