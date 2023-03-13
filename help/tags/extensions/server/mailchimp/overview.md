---
title: Información general sobre la extensión Mailchimp
description: Utiliza el reenvío de eventos para déclencheur correos electrónicos de Mailchimp.
type: Documentation
feature: Data Collection, Event Forwarding
level: Beginner
role: User, Developer, Admin
topic: Integrations
exl-id: a52870c4-10e6-45a0-a502-f48da3398f3f
source-git-commit: bfbad3c11df64526627e4ce2d766b527df678bca
workflow-type: tm+mt
source-wordcount: '1303'
ht-degree: 5%

---

# Resumen de la extensión de reenvío de eventos Mailchimp

>[!NOTE]
>  
>Adobe Experience Platform Launch se ha convertido en un conjunto de tecnologías de recopilación de datos en Adobe Experience Platform. Como resultado, se han implementado varios cambios terminológicos en la documentación del producto. Consulte el siguiente [documento](https://experienceleague.adobe.com/docs/experience-platform/tags/term-updates.html) para obtener una referencia consolidada de los cambios terminológicos.

El Mailchimp [reenvío de eventos](../../../ui/event-forwarding/overview.md) Esta extensión envía eventos a la API de marketing de Mailchimp que pueden almacenar en déclencheur correos electrónicos para campañas de marketing, recorridos o transacciones de Mailchimp.

Este documento explica cómo configurar la extensión y las reglas mediante la acción Añadir evento.

## Requisitos previos

Este documento supone que está familiarizado con los productos de Mailchimp relevantes que aprovecha la extensión. Para obtener más información, consulte la documentación de ayuda de Mailchimp para [campañas](https://mailchimp.com/help/getting-started-with-campaigns/), [recorridos](https://mailchimp.com/help/about-customer-journeys/), y [transacciones](https://mailchimp.com/help/transactional/).

Se requiere una cuenta de Mailchimp para utilizar esta extensión. Puede registrarse para obtener una cuenta [aquí](https://login.mailchimp.com/signup/). En el panel de cuenta de Mailchimp, anote los siguientes valores para usarlos en esta guía:

- Prefijo de dominio de Mailchimp
- Su clave de API
- El ID de audiencia
- La dirección de correo electrónico predeterminada &quot;de&quot;

Según el plan de cuenta de Mailchimp, es posible que tengas acceso limitado a las herramientas de Recorrido del cliente de Mailchimp.

>[!TIP]
>  
>Si utilizas automatizaciones de Mailchimp como correos electrónicos transaccionales o Recorridos de clientes, los pasos y las pantallas pueden ser ligeramente diferentes de los que se enumeran aquí. Sin embargo, todavía necesita la misma información para utilizar esta extensión como se ha descrito anteriormente. Consulte la [Centro de ayuda de Mailchimp](https://mailchimp.com/help/) para obtener detalles sobre cada uno de estos valores para su cuenta y plan específicos.

### Prefijo de dominio

Después de iniciar sesión en Mailchimp y aterrizar en la vista del panel, la barra de direcciones del navegador debe mostrar una URL como `https://us11.admin.mailchimp.com` o simplemente `us11.admin.mailchimp.com`. En este ejemplo, el prefijo `us11` es solo un marcador de posición y su valor será diferente. Registre la dirección URL con el prefijo para un paso posterior.

### clave de API

Para buscar la clave API de tu cuenta, selecciona el icono de tu perfil en la interfaz de usuario de Mailchimp y luego selecciona **Perfil**. Debería ver una dirección URL como `https://us11.admin.mailchimp.com/account/profile/` pero con **su** prefijo en lugar de `us11`.

Seleccionar **Extras**, entonces **Claves de API**:

![Menú Extras, vínculo Claves de API](../../../images/extensions/server/mailchimp/menu-API-keys.png)

En **Sus claves API**, puede elegir una clave existente o puede seleccionar **Crear Una Clave** para crear uno nuevo. Puede crear una nueva clave para utilizarla específicamente con esta extensión. Copie la clave de API y guárdela para un paso posterior. Para obtener más información, consulte la documentación de Mailchimp sobre cómo [genere su clave de API](https://mailchimp.com/developer/marketing/guides/quick-start/#generate-your-api-key).

### ID de audiencia y dirección remitente

Seleccionar **Audiencia** en el panel de navegación izquierdo, **Tablero de audiencias**. A continuación, seleccione la audiencia que desee utilizar con esta extensión. Para obtener más información, consulte el documento de Mailchimp sobre [creación de una audiencia](https://mailchimp.com/help/create-audience/).

Con la audiencia creada y seleccionada, seleccione la **Administrar audiencia** y elija **Configuración**. Esta pantalla muestra varias configuraciones para la audiencia.

En la parte inferior de la pantalla Configuración, debería ver lo siguiente `Unique id for audience [audience name]` donde `[audience name]` es el nombre de la audiencia real. Copie el ID de audiencia y guárdelo para un paso posterior.

Seleccionar **Nombre de audiencia y valores predeterminados** y confirme que **Dirección de correo electrónico remitente predeterminada** tiene el valor correcto para sus campañas. Tenga en cuenta que el ID de audiencia también se muestra en la parte superior de esta página y es el mismo valor que copió en el último paso.

## Automatizaciones de Mailchimp

Dependiendo de tu plan de Mailchimp y de si utilizas correos electrónicos transaccionales, Recorridos del cliente u otras automatizaciones de Mailchimp, la configuración específica del recorrido puede variar.

>[!IMPORTANT]
>  
>El nombre del evento que elegiste para almacenar en déclencheur tu automatización o recorrido en Mailchimp es el mismo nombre de evento que debes enviar con esta extensión. Anote el nombre del evento en la automatización de Mailchimp y guárdelo para un paso posterior.

## Instalación y configuración

En esta sección se enumeran los pasos para instalar y configurar la extensión de. Para guardar de forma segura la clave API de Mailchimp, debes usar el reenvío de eventos [secretos](../../../ui/event-forwarding/secrets.md).

### Crear un secreto y un elemento de datos

En una propiedad de reenvío de eventos, [crear un [!UICONTROL Token] secreto](../../../ui/event-forwarding/secrets.md#token) llamado `Mailchimp API Key`.

Siguiente, [creación de un elemento de datos](../../../ui/managing-resources/data-elements.md#create-a-data-element) uso del [!UICONTROL Núcleo] extensión y a [!UICONTROL Secreto] tipo de elemento de datos para hacer referencia a `Mailchimp API Key` secreto que acaba de crear. Entrar `Mailchimp Token` como nombre del elemento de datos.

### Instale y configure la extensión de 

En la misma propiedad de reenvío de eventos, seleccione **[!UICONTROL Extensiones],** entonces **[!UICONTROL Catálogo]** para mostrar las extensiones disponibles para la instalación. Desde aquí, busque la extensión Mailchimp y seleccione **[!UICONTROL Instalar]**.

![Instalar la extensión Mailchimp](../../../images/extensions/server/mailchimp/install.png)

Aparece la pantalla de configuración. En **[!UICONTROL Nombre de dominio del prefijo del servidor Mailchimp]**, introduce el dominio que has copiado anteriormente desde tu cuenta de Mailchimp, incluido tu prefijo de dominio único.

>[!IMPORTANT]
>
>No incluir `http://` o `https://` en este campo.

![Configuración de extensión](../../../images/extensions/server/mailchimp/mailchimp-domain.png)

En **[!UICONTROL Token de Mailchimp]**, seleccione el icono de elemento de datos y elija el `Mailchimp Token` elemento de datos que ha creado anteriormente. Seleccionar **[!UICONTROL Guardar]** para guardar los cambios.

La extensión de ya está instalada y configurada para su uso en la propiedad.

## Recopilación de datos

Cuando se utiliza esta extensión en una [regla](../../../ui/managing-resources/rules.md)Sin embargo, hay varios valores de datos que la extensión envía a Mailchimp con cada evento. Para una implementación típica, puede configurar las variables [Extensión de SDK web de Adobe Experience Platform](../../client/sdk/overview.md) para enviar esos datos a [!DNL Platform Edge Network] para su uso por la extensión en la propiedad de reenvío de eventos.

Los datos requeridos por esta extensión se pueden enviar desde el SDK web como datos XDM o como datos no XDM. Consulte la documentación para obtener más información sobre [envío de datos XDM](../../../../edge/fundamentals/tracking-events.md#sending-non-xdm-data).

Por ejemplo, si un cliente realiza una compra o se registra para un evento en su sitio, puede enviar un correo electrónico de confirmación a través de Mailchimp con esta extensión. Una vez que envía la información necesaria desde el SDK web a la red perimetral, la extensión almacena en déclencheur el correo electrónico con Mailchimp.

![Añadir configuración de acción de evento](../../../images/extensions/server/mailchimp/action-configurations.png)

### Elementos de datos

La captura de pantalla de la sección anterior muestra los datos que puedes enviar con cada evento de esta extensión a Mailchimp. Una vez configurado el SDK web para enviar estos datos a la red perimetral, puede crear elementos de datos en la propiedad de reenvío de eventos para que la extensión pueda acceder a esos valores.

La tabla siguiente proporciona más detalles para cada valor posible.

| Nombre | Ruta de ejemplo | Tipo | Descripción | Requerido | Límites |
|:---|:---:|:---:|:---|:---:|:---|
| `email` | `arc.event.xdm._tenant.emailId`<br /> o<br /> `arc.event.data._tenant.emailId` | Cadena | La dirección que recibe el correo electrónico | **Sí** | Debe existir en la audiencia de Mailchimp |
| `listId` | `arc.event.xdm._tenant.listId`<br /> o<br /> `arc.event.data._tenant.listid` | Cadena | ID de audiencia | **Sí** | Debe coincidir con un ID de audiencia existente |
| `name` | `arc.event.xdm._tenant.name`<br /> o<br /> `arc.event.data._tenant.name` | Cadena | El nombre del evento | **Sí** | De 2 a 30 caracteres de longitud |
| `properties` | `arc.event.xdm._tenant.properties`<br /> o<br /> `arc.event.data._tenant.properties` | Objeto | Una lista opcional de propiedades en formato JSON con detalles sobre el evento | No |  |
| `isSyncing` | `arc.event.xdm._tenant.isSyncing`<br /> o<br /> `arc.event.data._tenant.isSyncing` | Booleano | Eventos creados con `is_syncing` establezca en `true` **no** Automatizaciones de déclencheur | No |  |
| `occurredAt` | `arc.event.xdm._tenant.occuredAt`<br /> o `arc.event.data._tenant.occuredAt` | Cadena | Una marca de tiempo ISO 8601 de cuándo se produjo el evento | No |  |

{style="table-layout:auto"}

>[!IMPORTANT]
>  
>El **Ruta de ejemplo** Los valores anteriores solo son ejemplos. Los nombres de campo y [rutas](../../../ui/event-forwarding/overview.md#data-element-path) Las referencias en esos elementos de datos pueden ser diferentes en la propiedad, según la forma en que haya asignado y configurado el SDK web en los pasos anteriores.

En la propiedad de reenvío de eventos puede crear un elemento de datos para cada uno de los campos descritos anteriormente. Una vez creada, puede hacer referencia a los elementos de datos en la variable [!UICONTROL Añadir evento] acción de esta extensión.

![Añadir configuración de acción de evento](../../../images/extensions/server/mailchimp/action-configurations.png)

Ahora puede utilizar esta extensión y la acción Añadir evento para almacenar en déclencheur correos electrónicos de Mailchimp para sus audiencias.

## Validación de datos

Al trabajar con extensiones de reenvío de eventos, la variable [Adobe Experience Platform Debugger](https://chrome.google.com/webstore/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob) es muy útil. En la sección Registros, en Registros de Edge puede ver las solicitudes realizadas por las reglas de reenvío de eventos una vez activadas. Las siguientes capturas de pantalla muestran una solicitud a la API de Mailchimp realizada por la extensión.

![Adobe Experience Platform Debugger](../../../images/extensions/server/mailchimp/debugger-edge-logs.png)

En el panel de Mailchimp, en la vista de Fuente de actividad de tu audiencia o miembro de audiencia, se proporciona una lista de eventos para ese audiencia o miembro de audiencia. Debe coincidir con los eventos enviados por la extensión y mostrar cualquier dato opcional enviado, junto con el correo electrónico o la campaña que recibieron. Consulte la [Guías de ayuda de Automatización Mailchimp](https://mailchimp.com/help/automation/) para obtener más información.
