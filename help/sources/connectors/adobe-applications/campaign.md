---
keywords: Experience Platform;inicio;temas populares;Adobe Campaign Managed Cloud Services;campaña;servicios administrados de campaña
title: Adobe Campaign Managed Cloud Services
description: Obtenga información sobre cómo conectar los Cloud Service administrados de Campaign a Platform mediante la interfaz de usuario
exl-id: 8f18bf73-ebf1-4b4e-a12b-964faa0e24cc
source-git-commit: e300e57df998836a8c388511b446e90499185705
workflow-type: tm+mt
source-wordcount: '753'
ht-degree: 2%

---

# Adobe Campaign Managed Cloud Services

Adobe Experience Platform permite la ingesta de datos desde fuentes externas, al tiempo que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de Platform. Puede introducir datos de una variedad de fuentes, como aplicaciones de Adobe, almacenamiento basado en la nube, bases de datos y muchas otras.

Adobe Campaign Managed Cloud Services ofrece una plataforma Managed Services para diseñar experiencias multicanal para los clientes y proporciona un entorno para la organización visual de la campaña, la administración de interacciones en tiempo real y la ejecución multicanal. Visite la [Documentación de Adobe Campaign v8](https://experienceleague.adobe.com/docs/campaign/campaign-v8/campaign-home.html?lang=es) para obtener más información.

La fuente de Adobe Campaign Managed Cloud Services le permite llevar los datos de registros de envío y de seguimiento de Adobe Campaign v8 a Adobe Experience Platform.

## Requisitos previos

Antes de poder crear una conexión de origen para llevar la versión 8 de Campaign al Experience Platform, primero debe completar los siguientes requisitos previos:

* [Configure la importación del registro de eventos mediante la consola del cliente de Adobe Campaign](#view-delivery-and-tracking-log-data)
* [Creación de un esquema XDM ExperienceEvent](#create-a-schema)
* [Crear un conjunto de datos](#create-a-dataset)

### Visualización de datos de registro de envío y seguimiento {#view-delivery-and-tracking-log-data}

>[!IMPORTANT]
>
>Debe tener acceso a la consola del cliente de Adobe Campaign v8 para ver los datos de registro en Campaign. Visite la [Documentación de Campaign v8](https://experienceleague.adobe.com/docs/campaign/campaign-v8/deploy/connect.html) para obtener información sobre cómo descargar e instalar la consola de cliente.

Inicie sesión en la instancia de Campaign v8 a través de la consola del cliente. En el [!DNL Explorer] pestaña, seleccione [!DNL Administration] y luego seleccione [!DNL Configuration]. A continuación, seleccione [!DNL Data schemas] y, a continuación, aplique el `broadLog` filtre por nombre o etiqueta. En la lista que aparece, seleccione el esquema de origen recipient delivery logs con el nombre `broadLogRcp`.

![La consola del cliente de Adobe Campaign v8 con la pestaña Explorer seleccionada, los nodos Administration, Configuration y Data schemas expandidos y el filtrado establecido en &quot;broad&quot;.](./images/campaign/explorer.png)

A continuación, seleccione la **Datos** pestaña.

![La consola del cliente de Adobe Campaign v8 con la pestaña de datos seleccionada.](./images/campaign/data.png)

Haga clic con el botón derecho/pulsación de tecla en el panel de datos para abrir el menú contextual. Desde aquí, seleccione **Configurar lista...**

![La consola del cliente de Adobe Campaign v8 con el menú contextual abierto y la opción Configure list seleccionada.](./images/campaign/configure.png)

Aparecerá la ventana de configuración de la lista, que le proporcionará una interfaz en la que puede añadir los campos deseados a la lista preexistente para ver los datos en el panel de datos.

![Una lista de configuraciones para los registros de envío de los destinatarios que se pueden añadir para su visualización.](./images/campaign/list-configuration.png)

Ahora puede ver los registros de envío de los destinatarios, incluidos los campos de configuración añadidos en el paso anterior.

>[!TIP]
>
>Puede repetir los mismos pasos, pero filtrar por `tracking` para ver los datos del registro de seguimiento.

![Los registros de envío de los destinatarios mostrados con información sobre su último nombre modificado, canal de envío, nombre de envío interno y etiqueta.](./images/campaign/recipient-delivery-logs.png)

### Creación de un esquema {#create-a-schema}

A continuación, cree un esquema XDM ExperienceEvent para los registros de envío y de seguimiento. Debe aplicar el grupo de campos Registros de envío de Campaign al esquema de registros de envío y el grupo de campos Registros de seguimiento de Campaign al esquema de registros de seguimiento. También debe definir la variable `externalID` como la identidad principal del esquema.

>[!NOTE]
>
>El esquema XDM ExperienceEvent debe estar habilitado para el perfil para poder introducir los datos de Campaign en [!DNL Real-Time Customer Profile].

Para obtener instrucciones detalladas sobre cómo crear un esquema, lea la guía de [creación de un esquema XDM en la IU](../../../xdm/tutorials/create-schema-ui.md).

### Crear un conjunto de datos {#create-a-dataset}

Finalmente, debe crear un conjunto de datos para los esquemas. Para obtener instrucciones detalladas sobre cómo crear un conjunto de datos, lea la guía sobre [creación de un conjunto de datos en la IU](../../../catalog/datasets/user-guide.md).

## Creación de una conexión de origen de Adobe Campaign Managed Cloud Services mediante la IU de Platform

Ahora que ha accedido a los registros de datos en la consola del cliente de Campaign, ha creado un esquema y un conjunto de datos, puede continuar con la creación de una conexión de origen para llevar los datos de Campaign Managed Services a Platform.

Para obtener instrucciones detalladas sobre cómo llevar los datos de registros de envío y registros de seguimiento de Campaign v8 a Experience Platform, lea la guía sobre [creación de una conexión de origen de Managed Services en Campaign en la IU](../../tutorials/ui/create/adobe-applications/campaign.md).

>[!IMPORTANT]
>
>Existe un caso límite en el que la interacción de un destinatario de correo electrónico eliminado recientemente con un correo electrónico podría volver a introducir información personal en Experience Platform. En algunos casos, esto podría volver a habilitar el marketing para ese usuario.
>
>* Este escenario solo está activo entre el momento en que se ha ejecutado una solicitud de privacidad en Experience Platform y el momento en que se ha ejecutado en Adobe Campaign Classic. Una vez que la solicitud se ejecuta en Campaign, se realiza una comprobación para asegurarse de que el registro no se exporta a Campaign. Vuelva a emitir una solicitud RGPD después de 72 horas de ejecución para resolverlo.