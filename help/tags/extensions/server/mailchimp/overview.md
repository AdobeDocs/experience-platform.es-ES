---
title: Información general sobre la extensión Mailchimp
description: Utiliza el reenvío de eventos para déclencheur correos electrónicos de Mailchimp.
type: Documentation
feature: Data Collection, Event Forwarding
level: Beginner
role: User, Developer, Admin
topic: Integrations
exl-id: a52870c4-10e6-45a0-a502-f48da3398f3f
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1267'
ht-degree: 5%

---

# Resumen de la extensión de reenvío de eventos Mailchimp

>[!NOTE]
>  
>Adobe Experience Platform Launch se ha convertido en un grupo de tecnologías de recopilación de datos en Adobe Experience Platform. Como resultado, se han implementado varios cambios terminológicos en la documentación del producto. Consulte el siguiente [documento](https://experienceleague.adobe.com/docs/experience-platform/tags/term-updates.html?lang=es) para obtener una referencia consolidada de los cambios terminológicos.

La extensión de Mailchimp [reenvío de eventos](../../../ui/event-forwarding/overview.md) envía eventos a la API de marketing de Mailchimp que puede almacenar en déclencheur correos electrónicos para campañas, recorridos o transacciones de marketing de Mailchimp.

Este documento explica cómo configurar la extensión y las reglas mediante la acción Añadir evento.

## Requisitos previos

Este documento supone que está familiarizado con los productos de Mailchimp relevantes que aprovecha la extensión. Para obtener más información, consulta la documentación de ayuda de Mailchimp para [campañas](https://mailchimp.com/help/getting-started-with-campaigns/), [recorridos](https://mailchimp.com/help/about-customer-journeys/) y [transacciones](https://mailchimp.com/help/transactional/).

Se requiere una cuenta de Mailchimp para utilizar esta extensión. Puede registrarse para obtener una cuenta [aquí](https://login.mailchimp.com/signup/). En el panel de cuenta de Mailchimp, anote los siguientes valores para usarlos en esta guía:

- Prefijo de dominio de Mailchimp
- Su clave de API
- El ID de audiencia
- La dirección de correo electrónico predeterminada &quot;de&quot;

Según el plan de cuenta de Mailchimp, es posible que tengas acceso limitado a las herramientas de Recorrido del cliente de Mailchimp.

>[!TIP]
>  
>Si utilizas automatizaciones de Mailchimp como correos electrónicos transaccionales o Recorridos de clientes, los pasos y las pantallas pueden ser ligeramente diferentes de los que se enumeran aquí. Sin embargo, todavía necesita la misma información para utilizar esta extensión como se ha descrito anteriormente. Consulta el [Centro de ayuda de Mailchimp](https://mailchimp.com/help/) para obtener detalles sobre cada uno de estos valores para tu cuenta y plan específicos.

### Prefijo de dominio

Después de iniciar sesión en Mailchimp y de aterrizar en la vista del panel, la barra de direcciones del navegador debe mostrar una URL como `https://us11.admin.mailchimp.com` o solo `us11.admin.mailchimp.com`. En este ejemplo, el prefijo `us11` es solo un marcador de posición y el valor será diferente. Registre la dirección URL con el prefijo para un paso posterior.

### Clave de API

Para encontrar la clave API de tu cuenta, selecciona el icono de perfil en la interfaz de usuario de Mailchimp y, a continuación, selecciona **Perfil**. Debería ver una dirección URL como `https://us11.admin.mailchimp.com/account/profile/`, pero con el prefijo **your** en lugar de `us11`.

Seleccione **Extras** y luego **claves API**:

![Menú Extras, vínculo de claves API](../../../images/extensions/server/mailchimp/menu-API-keys.png)

En **Sus claves API**, puede elegir una clave existente o seleccionar **Crear una clave** para crear una nueva. Puede crear una nueva clave para utilizarla específicamente con esta extensión. Copie la clave de API y guárdela para un paso posterior. Para obtener más información, consulta la documentación de Mailchimp sobre cómo [generar tu clave de API](https://mailchimp.com/developer/marketing/guides/quick-start/#generate-your-api-key).

### ID de audiencia y dirección remitente

Seleccione **Audiencia** en el panel de navegación izquierdo, luego **Panel de audiencias**. A continuación, seleccione la audiencia que desee utilizar con esta extensión. Para obtener más información, consulta el documento de Mailchimp sobre [creación de una audiencia](https://mailchimp.com/help/create-audience/).

Con la audiencia creada y seleccionada, selecciona el menú desplegable **Administrar audiencia** y elige **Configuración**. Esta pantalla muestra varias configuraciones para la audiencia.

En la parte inferior de la pantalla Configuración, debería ver `Unique id for audience [audience name]`, donde `[audience name]` es el nombre de la audiencia real. Copie el ID de audiencia y guárdelo para un paso posterior.

Seleccione **Nombre de audiencia y valores predeterminados** y confirme que **Dirección de correo electrónico remitente predeterminada** tiene el valor correcto para sus campañas. Tenga en cuenta que el ID de audiencia también se muestra en la parte superior de esta página y es el mismo valor que copió en el último paso.

## Automatizaciones de Mailchimp

Dependiendo de tu plan de Mailchimp y de si utilizas correos electrónicos transaccionales, Recorridos del cliente u otras automatizaciones de Mailchimp, la configuración específica del recorrido puede variar.

>[!IMPORTANT]
>  
>El nombre del evento que elegiste para almacenar en déclencheur tu automatización o recorrido en Mailchimp es el mismo nombre de evento que debes enviar con esta extensión. Anote el nombre del evento en la automatización de Mailchimp y guárdelo para un paso posterior.

## Instalación y configuración

En esta sección se enumeran los pasos para instalar y configurar la extensión de. Para guardar de forma segura la clave de API de Mailchimp, debes usar el reenvío de eventos [secret](../../../ui/event-forwarding/secrets.md).

### Crear un secreto y un elemento de datos

En una propiedad de reenvío de eventos, [cree un [!UICONTROL token] secreto](../../../ui/event-forwarding/secrets.md#token) llamado `Mailchimp API Key`.

A continuación, [cree un elemento de datos](../../../ui/managing-resources/data-elements.md#create-a-data-element) con la extensión [!UICONTROL Core] y un tipo de elemento de datos [!UICONTROL Secret] para hacer referencia al secreto `Mailchimp API Key` que acaba de crear. Escriba `Mailchimp Token` como nombre del elemento de datos.

### Instalación y configuración de la extensión de

En la misma propiedad de reenvío de eventos, seleccione **[!UICONTROL Extensiones],** y **[!UICONTROL Catálogo]** para mostrar las extensiones disponibles para la instalación. Aquí, busca la extensión Mailchimp y selecciona **[!UICONTROL Instalar]**.

![Instalar la extensión de Mailchimp](../../../images/extensions/server/mailchimp/install.png)

Aparece la pantalla de configuración. En **[!UICONTROL Nombre de dominio del prefijo del servidor de Mailchimp]**, escribe el dominio que copiaste anteriormente desde tu cuenta de Mailchimp, incluido tu prefijo de dominio único.

>[!IMPORTANT]
>
>No incluya `http://` o `https://` en este campo.

![Configuración de extensión](../../../images/extensions/server/mailchimp/mailchimp-domain.png)

En **[!UICONTROL Token de Mailchimp]**, seleccione el icono del elemento de datos y elija el elemento de datos `Mailchimp Token` que creó anteriormente. Seleccione **[!UICONTROL Guardar]** para guardar los cambios.

La extensión de ya está instalada y configurada para su uso en la propiedad.

## Recopilación de datos

Al usar esta extensión en una [regla](../../../ui/managing-resources/rules.md), hay varios valores de datos que la extensión envía a Mailchimp con cada evento. Para una implementación típica, puede configurar la [extensión de Adobe Experience Platform Web SDK](../../client/web-sdk/overview.md) para enviar esos datos a [!DNL Experience Platform Edge Network] para que la utilice la extensión en la propiedad de reenvío de eventos.

Los datos requeridos por esta extensión se pueden enviar desde Web SDK como datos XDM (con el objeto [`xdm`](/help/web-sdk/commands/sendevent/xdm.md)) o como datos que no sean XDM (con el objeto [`data`](/help/web-sdk/commands/sendevent/data.md)).

Por ejemplo, si un cliente realiza una compra o se registra para un evento en su sitio, puede enviar un correo electrónico de confirmación a través de Mailchimp con esta extensión. Una vez que envía la información necesaria desde Web SDK a Edge Network, la extensión almacena en déclencheur el correo electrónico con Mailchimp.

![Agregar configuración de acción de evento](../../../images/extensions/server/mailchimp/action-configurations.png)

### Elementos de datos

La captura de pantalla de la sección anterior muestra los datos que puedes enviar con cada evento de esta extensión a Mailchimp. Una vez configurado Web SDK para enviar estos datos a Edge Network, puede crear elementos de datos en la propiedad de reenvío de eventos para que la extensión pueda acceder a esos valores.

La tabla siguiente proporciona más detalles para cada valor posible.

| Nombre | Ruta de ejemplo | Tipo | Descripción | Requerido | Límites |
|:---|:---:|:---:|:---|:---:|:---|
| `email` | `arc.event.xdm._tenant.emailId`<br /> o <br /> `arc.event.data._tenant.emailId` | Cadena | La dirección que recibe el correo electrónico | **Sí** | Debe existir en la audiencia de Mailchimp |
| `listId` | `arc.event.xdm._tenant.listId`<br /> o <br /> `arc.event.data._tenant.listid` | Cadena | ID de público | **Sí** | Debe coincidir con un ID de audiencia existente |
| `name` | `arc.event.xdm._tenant.name`<br /> o <br /> `arc.event.data._tenant.name` | Cadena | El nombre del evento | **Sí** | De 2 a 30 caracteres de longitud |
| `properties` | `arc.event.xdm._tenant.properties`<br /> o <br /> `arc.event.data._tenant.properties` | Objeto | Una lista opcional de propiedades en formato JSON con detalles sobre el evento | No |  |
| `isSyncing` | `arc.event.xdm._tenant.isSyncing`<br /> o <br /> `arc.event.data._tenant.isSyncing` | Booleano | Los eventos creados con `is_syncing` establecido en `true` **no** automatizaciones de déclencheur | No |  |
| `occurredAt` | `arc.event.xdm._tenant.occuredAt`<br /> o `arc.event.data._tenant.occuredAt` | Cadena | Una marca de tiempo ISO 8601 de cuándo se produjo el evento | No |  |

{style="table-layout:auto"}

>[!IMPORTANT]
>  
>Los valores de **Ejemplo de ruta** anteriores son solo ejemplos. Los nombres de campo y las [rutas](../../../ui/event-forwarding/overview.md#data-element-path) a las que se hace referencia en esos elementos de datos pueden ser diferentes en su propiedad, según cómo haya asignado nombre y configurado Web SDK en los pasos anteriores.

En la propiedad de reenvío de eventos puede crear un elemento de datos para cada uno de los campos descritos anteriormente. Una vez creada, puede hacer referencia a los elementos de datos en la acción [!UICONTROL Agregar evento] de esta extensión.

![Agregar configuración de acción de evento](../../../images/extensions/server/mailchimp/action-configurations.png)

Ahora puede utilizar esta extensión y la acción Añadir evento para almacenar en déclencheur correos electrónicos de Mailchimp para sus audiencias.

## Validación de datos

Al trabajar con extensiones de reenvío de eventos, [Adobe Experience Platform Debugger](https://chrome.google.com/webstore/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob) resulta muy útil. En la sección Registros, en Registros de Edge puede ver las solicitudes realizadas por las reglas de reenvío de eventos una vez activadas. Las siguientes capturas de pantalla muestran una solicitud a la API de Mailchimp realizada por la extensión.

![Adobe Experience Platform Debugger](../../../images/extensions/server/mailchimp/debugger-edge-logs.png)

En el panel de Mailchimp, en la vista de Fuente de actividad de tu audiencia o miembro de audiencia, se proporciona una lista de eventos para ese audiencia o miembro de audiencia. Debe coincidir con los eventos enviados por la extensión y mostrar cualquier dato opcional enviado, junto con el correo electrónico o la campaña que recibieron. Consulte las [guías de ayuda de automatización de Mailchimp](https://mailchimp.com/help/automation/) para obtener más información.
