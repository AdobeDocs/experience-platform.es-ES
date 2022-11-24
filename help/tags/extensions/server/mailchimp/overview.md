---
title: Información general de la extensión Mailchimp
description: Utilice el reenvío de eventos para los correos electrónicos de déclencheur Mailchimp.
type: Documentation
feature: Data Collection, Event Forwarding
level: Beginner
role: User, Developer, Admin
topic: Integrations
exl-id: a52870c4-10e6-45a0-a502-f48da3398f3f
source-git-commit: bfbad3c11df64526627e4ce2d766b527df678bca
workflow-type: tm+mt
source-wordcount: '1306'
ht-degree: 5%

---

# Descripción general de la extensión de reenvío de eventos Mailchimp

>[!NOTE]
>  
>Adobe Experience Platform Launch se ha convertido en un conjunto de tecnologías de recopilación de datos en Adobe Experience Platform. Como resultado, se han implementado varios cambios terminológicos en la documentación del producto. Consulte el siguiente [documento](https://experienceleague.adobe.com/docs/experience-platform/tags/term-updates.html) para obtener una referencia consolidada de los cambios terminológicos.

Mailchimp [reenvío de eventos](../../../ui/event-forwarding/overview.md) envía eventos a la API de marketing de Mailchimp que pueden enviar correos electrónicos de déclencheur para campañas de marketing de Mailchimp, recorridos o transacciones.

Este documento explica cómo configurar la extensión y configurar reglas mediante la acción Añadir evento .

## Requisitos previos

Este documento supone que está familiarizado con los productos Mailchimp relevantes aprovechados por la extensión. Para obtener más información, consulte la documentación de ayuda de Mailchimp para [campañas](https://mailchimp.com/help/getting-started-with-campaigns/), [recorridos](https://mailchimp.com/help/about-customer-journeys/)y [transacciones](https://mailchimp.com/help/transactional/).

Se requiere una cuenta Mailchimp para utilizar esta extensión. Puede registrarse en una cuenta [here](https://login.mailchimp.com/signup/). En el panel de cuentas de Mailchimp, tome nota de los siguientes valores para usarlos en esta guía:

- El prefijo de dominio Mailchimp
- La clave de API
- El ID de audiencia
- La dirección de correo electrónico predeterminada &quot;de&quot;

Según el plan de cuenta de Mailchimp, es posible que tenga acceso limitado a las herramientas de Recorrido del cliente de Mailchimp.

>[!TIP]
>  
>Si utiliza automatizaciones Mailchimp como correos electrónicos transaccionales o Recorridos de cliente, los pasos y las pantallas pueden ser ligeramente diferentes a los que se enumeran aquí. Sin embargo, sigue necesitando la misma información para utilizar esta extensión como se describe anteriormente. Consulte la [Centro de ayuda de Mailchimp](https://mailchimp.com/help/) para obtener detalles sobre cada uno de estos valores para su cuenta y plan específicos.

### Prefijo de dominio

Después de iniciar sesión en Mailchimp y aterrizar en la vista Tablero, la barra de direcciones del explorador debería mostrar una dirección URL como `https://us11.admin.mailchimp.com` o solo `us11.admin.mailchimp.com`. En este ejemplo, el prefijo `us11` es solo un marcador de posición y su valor será diferente. Registre la dirección URL con el prefijo para un paso posterior.

### clave de API

Para buscar la clave de API para la cuenta, seleccione el icono de perfil en la interfaz de usuario de Mailchimp y, a continuación, seleccione **Perfil**. Debería ver una URL como `https://us11.admin.mailchimp.com/account/profile/` pero con **your** prefijo en lugar de `us11`.

Select **Extras**, luego **Claves de API**:

![Menú Extras, vínculo de claves de API](../../../images/extensions/server/mailchimp/menu-API-keys.png)

En **Sus claves de API**, puede elegir una clave existente o seleccionar **Crear Una Clave** para crear uno nuevo. Puede crear una nueva clave para utilizarla específicamente con esta extensión. Copie la clave de API y guárdela para un paso posterior. Para obtener más información, consulte la documentación de Mailchimp sobre cómo [generar la clave de API](https://mailchimp.com/developer/marketing/guides/quick-start/#generate-your-api-key).

### ID de audiencia y dirección de origen

Select **Audiencia** en la navegación izquierda, **Panel de audiencia**. A continuación, seleccione la audiencia que desea utilizar con esta extensión. Para obtener más información, consulte el documento Mailchimp en [creación de una audiencia](https://mailchimp.com/help/create-audience/).

Con la audiencia creada y seleccionada, seleccione la opción **Administrar audiencia** lista desplegable y elija **Configuración**. Esta pantalla muestra varias configuraciones para la audiencia.

En la parte inferior de la pantalla Configuración, debería ver `Unique id for audience [audience name]` donde `[audience name]` es el nombre de la audiencia real. Copie el ID de audiencia y guárdelo para un paso posterior.

Select **Nombre de audiencia y valores predeterminados** y confirme que **Dirección predeterminada de correo electrónico** tiene el valor correcto para sus campañas. Tenga en cuenta que el ID de audiencia también se muestra en la parte superior de esta página y es el mismo valor que copió en el último paso.

## Automatización de Mailchimp

Dependiendo de su plan Mailchimp y de si utiliza correos electrónicos transaccionales, Recorridos del cliente u otras automatizaciones de Mailchimp, la configuración específica del recorrido puede variar.

>[!IMPORTANT]
>  
>El nombre del evento que eligió para almacenar en déclencheur la automatización o el recorrido en Mailchimp es el mismo nombre de evento que debe enviar con esta extensión. Observe el nombre del evento en la automatización de Mailchimp y guárdelo para un paso posterior.

## Instalación y configuración

Esta sección enumera los pasos para instalar y configurar la extensión. Para guardar de forma segura la clave de API Mailchimp, debe utilizar el reenvío de eventos [secretos](../../../ui/event-forwarding/secrets.md).

### Crear un secreto y un elemento de datos

En una propiedad de reenvío de eventos, [cree un [!UICONTROL Token] secreto](../../../ui/event-forwarding/secrets.md#token) llamado `Mailchimp API Key`.

Siguiente, [crear un elemento de datos](../../../ui/managing-resources/data-elements.md#create-a-data-element) usando la variable [!UICONTROL Principal] extensión y [!UICONTROL Secreto] tipo de elemento de datos para hacer referencia a la variable `Mailchimp API Key` secreto que acaba de crear. Entrar `Mailchimp Token` como nombre del elemento de datos.

### Instale y configure la extensión de 

En la misma propiedad de reenvío de eventos, seleccione **[!UICONTROL Extensiones],** then **[!UICONTROL Catálogo]** para mostrar las extensiones disponibles para la instalación. Desde aquí, busque la extensión Mailchimp y seleccione **[!UICONTROL Instalar]**.

![Instalación de la extensión Mailchimp](../../../images/extensions/server/mailchimp/install.png)

Aparecerá la pantalla de configuración. En **[!UICONTROL Nombre de dominio de prefijo del servidor Mailchimp]**, introduzca el dominio que ha copiado anteriormente desde su cuenta de Mailchimp, incluido su prefijo de dominio único.

>[!IMPORTANT]
>
>No incluir `http://` o `https://` en este campo.

![Configuración de extensión](../../../images/extensions/server/mailchimp/mailchimp-domain.png)

En **[!UICONTROL Token de Mailchimp]**, seleccione el icono de elemento de datos y elija la opción `Mailchimp Token` elemento de datos creado anteriormente. Select **[!UICONTROL Guardar]** para guardar los cambios.

La extensión de ahora está instalada y configurada para su uso en la propiedad de .

## Recopilación de datos

Al utilizar esta extensión en un [regla](../../../ui/managing-resources/rules.md), hay varios valores de datos que la extensión envía a Mailchimp con cada evento. Para una implementación típica, puede configurar la variable [Extensión de Adobe Experience Platform Web SDK](../../client/sdk/overview.md) para enviar esos datos a [!DNL Platform Edge Network] para su uso por la extensión en la propiedad de reenvío de eventos.

Los datos requeridos por esta extensión pueden enviarse desde el SDK web como datos XDM o no XDM. Consulte la documentación para obtener más información [envío de datos XDM](../../../../edge/fundamentals/tracking-events.md#sending-non-xdm-data).

Por ejemplo, si un cliente realiza una compra o se registra en un evento de su sitio, puede enviar un correo electrónico de confirmación a través de Mailchimp con esta extensión. Una vez que envíe la información necesaria desde el SDK web a la red perimetral, la extensión déclencheur el correo electrónico con Mailchimp.

![Añadir configuración de acción de evento](../../../images/extensions/server/mailchimp/action-configurations.png)

### Elementos de datos

La captura de pantalla de la sección anterior muestra los datos que se pueden enviar con cada evento desde esta extensión a Mailchimp. Una vez configurado el SDK web para enviar estos datos a la red perimetral, puede crear elementos de datos en la propiedad de reenvío de eventos para que la extensión pueda acceder a esos valores.

La tabla siguiente proporciona más detalles para cada valor posible.

| Nombre | Ruta de ejemplo | Tipo | Descripción | Requerido | Límites |
|:---|:---:|:---:|:---|:---:|:---|
| `email` | `arc.event.xdm._tenant.emailId`<br /> o<br /> `arc.event.data._tenant.emailId` | Cadena | La dirección que recibe el correo electrónico | **Sí** | Debe existir en la audiencia de Mailchimp |
| `listId` | `arc.event.xdm._tenant.listId`<br /> o<br /> `arc.event.data._tenant.listid` | Cadena | ID de audiencia | **Sí** | Debe coincidir con un ID de audiencia existente |
| `name` | `arc.event.xdm._tenant.name`<br /> o<br /> `arc.event.data._tenant.name` | Cadena | El nombre del evento | **Sí** | De 2 a 30 caracteres de longitud |
| `properties` | `arc.event.xdm._tenant.properties`<br /> o<br /> `arc.event.data._tenant.properties` | Objeto | Una lista opcional de propiedades en formato JSON con detalles sobre el evento | No |  |
| `isSyncing` | `arc.event.xdm._tenant.isSyncing`<br /> o<br /> `arc.event.data._tenant.isSyncing` | Booleano | Eventos creados con `is_syncing` configure como `true` **will not** Automatización de déclencheur | No |  |
| `occurredAt` | `arc.event.xdm._tenant.occuredAt`<br /> o `arc.event.data._tenant.occuredAt` | Cadena | Marca de tiempo ISO 8601 del momento en que se produjo el evento | No |  |

{style=&quot;table-layout:auto&quot;}

>[!IMPORTANT]
>  
>La variable **Ruta de ejemplo** los valores anteriores son solo ejemplos. Los nombres de campo y [rutas](../../../ui/event-forwarding/overview.md#data-element-path) en esos elementos de datos puede haber una referencia diferente en su propiedad, según el nombre y la configuración del SDK web en los pasos anteriores.

En la propiedad de reenvío de eventos, puede crear un elemento de datos para cada uno de los campos descritos anteriormente. Una vez creados, puede hacer referencia a los elementos de datos en la variable [!UICONTROL Agregar evento] acción de esta extensión.

![Añadir configuración de acción de evento](../../../images/extensions/server/mailchimp/action-configurations.png)

Ahora puede utilizar esta extensión y la acción Añadir evento para almacenar en déclencheur los correos electrónicos de Mailchimp para las audiencias.

## Validación de datos

Al trabajar con extensiones de reenvío de eventos, la variable [Adobe Experience Platform Debugger](https://chrome.google.com/webstore/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob) es muy útil. En la sección Registros , en Registros de Edge , puede ver las solicitudes realizadas por las reglas de reenvío de eventos después de activarse. Las siguientes capturas de pantalla muestran una solicitud que la extensión está realizando a la API Mailchimp.

![Adobe Experience Platform Debugger](../../../images/extensions/server/mailchimp/debugger-edge-logs.png)

En el panel Mailchimp, en la vista Fuente de actividad de su Audiencia o Miembro de audiencia, se proporciona una lista de eventos para esa Audiencia o Miembro de audiencia. Esto debe coincidir con los eventos enviados por la extensión y mostrar los datos opcionales enviados, junto con el correo electrónico o la campaña que recibieron. Consulte la [Guías de ayuda de la automatización de Mailchimp](https://mailchimp.com/help/automation/) para obtener más información.
