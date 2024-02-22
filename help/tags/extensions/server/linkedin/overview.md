---
title: Extensión de reenvío de eventos de API de conversiones de LinkedIn
description: Esta extensión de reenvío de eventos de Adobe Experience Platform le permite medir el rendimiento de su campaña de marketing de LinkedIn.
last-substantial-update: 2023-10-25T00:00:00Z
exl-id: 411e7b77-081e-4139-ba34-04468e519ea5
source-git-commit: 0d6ade1a0b6c00a4f87395d476dd7e7915489ea5
workflow-type: tm+mt
source-wordcount: '790'
ht-degree: 2%

---

# Extensión de API de conversiones de [!DNL LinkedIn]

[[!DNL LinkedIn Conversions API]](https://learn.microsoft.com/en-us/linkedin/marketing/integrations/ads-reporting/conversions-api) es una herramienta de seguimiento de conversión que crea una conexión directa entre los datos de marketing del servidor de un anunciante y [!DNL LinkedIn]. Esto permite a los anunciantes evaluar la eficacia de su [!DNL LinkedIn] campañas de marketing independientemente de la ubicación de la conversión y utilice esta información para impulsar la optimización de campañas. El [!DNL LinkedIn Conversions API] La extensión de puede ayudar a reforzar el rendimiento y reducir el coste por acción con una atribución más completa, una fiabilidad de los datos mejorada y una entrega optimizada mejor.

## Requisitos previos {#prerequisites}

Usted debe [crear una regla de conversión](https://www.linkedin.com/help/lms/answer/a1657171) en su [!DNL LinkedIn Campaign Manager] cuenta. [!DNL Adobe] recomienda incluir &quot;CAPI&quot; al principio del nombre de la regla de conversación para diferenciarla de otros tipos de reglas de conversión que pueda haber configurado.

### Creación de un secreto y un elemento de datos

Crear un nuevo [!DNL LinkedIn] [secreto de reenvío de eventos](../../../ui/event-forwarding/secrets.md) y asígnele un nombre único que signifique el miembro autenticador. Se utilizará para autenticar la conexión con su cuenta y mantener el valor seguro.

Siguiente, [creación de un elemento de datos](../../../ui/managing-resources/data-elements.md#create-a-data-element) uso del [!UICONTROL Núcleo] extensión y a [!UICONTROL Secreto] tipo de elemento de datos para hacer referencia a `LinkedIn` secreto que acaba de crear.

## Instalación y configuración de [!DNL LinkedIn] extensión {#install}

Para instalar la extensión de, [crear una propiedad de reenvío de eventos](../../../ui/event-forwarding/overview.md#properties) o seleccione una propiedad existente para editarla.

Seleccionar **[!UICONTROL Extensiones]** en el panel de navegación izquierdo. En el **[!UICONTROL Catálogo]** , seleccione la pestaña **[!UICONTROL LinkedIn]** extensión y, a continuación, seleccione **[!UICONTROL Instalar]**.

![El catálogo de extensiones que muestra [!DNL LinkedIn] instalación de resalte de tarjeta de extensión.](../../../images/extensions/server/linkedin/install-extension.png)

En la siguiente pantalla, introduzca el secreto del elemento de datos creado anteriormente en `Access Token` field. El secreto del elemento de datos contendrá su [!DNL LinkedIn] Token de OAuth 2. Seleccione **[!UICONTROL Guardar]** cuando haya terminado.

![El [!DNL LinkedIn] página de configuración de la extensión con [!UICONTROL Token de acceso] field y [!UICONTROL Guardar] resaltado.](../../../images/extensions/server/linkedin/configure-extension.png)

## Crear un [!DNL Send Conversion] regla {#tracking-rule}

Una vez configurados todos los elementos de datos, puede empezar a crear reglas de reenvío de eventos que determinen cuándo y cómo se enviarán los eventos a [!DNL LinkedIn].

Crear un nuevo reenvío de eventos [regla](../../../ui/managing-resources/rules.md) en la propiedad de reenvío de eventos. En **[!UICONTROL Acciones]**, añada una nueva acción y establezca la extensión en **[!UICONTROL LinkedIn]**. A continuación, seleccione **[!UICONTROL Enviar conversión]** para el **[!UICONTROL Tipo de acción]**.

![La vista Reglas de propiedad de reenvío de eventos, con los campos necesarios para agregar una configuración de acción de regla de reenvío de eventos resaltados.](../../../images/extensions/server/linkedin/linkedin-event-action.png)

Después de la selección, aparecen controles adicionales para configurar aún más el evento. Seleccionar **[!UICONTROL Conservar cambios]** para guardar la regla.

**[!UICONTROL Datos de usuario]**

| Entrada | Descripción |
| --- | --- |
| [!UICONTROL Correo electrónico] | Dirección de correo electrónico del contacto asociado con el evento de conversión. El código de extensión SHA256 codificará el valor de correo electrónico a menos que el valor proporcionado ya sea una cadena SHA256. |
| [!UICONTROL UUID de seguimiento de anuncios de origen de linkedIn] | Este es un ID de cookie de origen. Los anunciantes deben habilitar un seguimiento de conversión mejorado desde [[!DNL LinkedIn Campaign Manager]](https://www.linkedin.com/help/lms/answer/a423304/enable-first-party-cookies-on-a-linkedin-insight-tag) para activar cookies de origen que adjunten un parámetro de ID de clic `li_fat_id` Vaya a las direcciones URL de clic. |
| [!UICONTROL Datos de información del cliente] | Este campo contiene un objeto JSON con atributos adicionales que se envían junto con el mensaje.<br><br>En el **[!UICONTROL Raw]** , puede pegar el objeto JSON directamente en el campo de texto proporcionado o puede seleccionar el icono de elemento de datos (![Icono de conjunto de datos](../../../images/extensions/server/aws/data-element-icon.png)) para seleccionar de una lista de elementos de datos existentes para representar los datos.<br><br>También puede utilizar la variable **[!UICONTROL Editor de pares de clave-valor JSON]** para agregar manualmente cada par clave-valor a través de un editor de interfaz de usuario. Cada valor se puede representar mediante una entrada sin procesar o se puede seleccionar un elemento de datos en su lugar. Los valores de clave aceptados son: `firstName`, `lastName`, `companyName`, `title` y `country`. |

{style="table-layout:auto"}

![El [!DNL User Data] sección que muestra la entrada de datos de ejemplo en los campos.](../../../images/extensions/server/linkedin/configure-extension-user-data.png)

**[!UICONTROL Datos de conversión]**

| Entrada | Descripción |
| --- | --- |
| [!UICONTROL Conversión] | El ID de la regla de conversión creada en [Administrador de linkedIn Campaign](https://www.linkedin.com/help/lms/answer/a1657171). Seleccione la regla de conversión para obtener el ID y copie el ID desde la dirección URL del explorador (por ejemplo, `/campaignmanager/accounts/508111232/conversions/15588877`) como `/conversions/<id>`. |
| [!UICONTROL Tiempo de conversión] | Cada marca de tiempo en milisegundos a los que se produjo el evento de conversión. <br><br> Nota: Si la fuente registra la marca de tiempo de conversión en segundos, inserte 000 al final para transformarla a milisegundos. |
| [!UICONTROL Moneda] | Código de divisa en formato ISO. |
| [!UICONTROL Cantidad] | Valor de la conversión en una cadena decimal (por ejemplo, &quot;100.05&quot;). |
| [!UICONTROL ID de evento] | ID único generado por los anunciantes para indicar cada evento. Este es un campo opcional y se utiliza para lo siguiente [deduplicación](https://learn.microsoft.com/en-us/linkedin/marketing/conversions/deduplication?view=li-lms-2024-02). |

{style="table-layout:auto"}

![El [!DNL Conversion Data] que muestra datos de ejemplo en los campos.](../../../images/extensions/server/linkedin/configure-extension-conversions-data.png)

**[!UICONTROL Anulaciones de configuración]**

>NOTA
>
>El [!UICONTROL Anulaciones de configuración] permite al usuario establecer un campo diferente [!DNL LinkedIn] token de acceso en cada regla, permitiendo que cada regla utilice un token de acceso que puede tener acceso a diferentes [!DNL LinkedIn] cuentas de publicidad.

| Entrada | Descripción |
| --- | --- |
| [!UICONTROL Token de acceso] | El [!DNL LinkedIn] token de acceso. |

![El [!DNL Configuration Overrides] sección que muestra la entrada de datos de ejemplo en el campo.](../../../images/extensions/server/linkedin/configure-extension-configuration-override.png)

## Pasos siguientes

En esta guía se explica cómo enviar datos a [!DNL LinkedIn] uso del [!DNL LinkedIn Conversions API] extensión de reenvío de eventos. Para obtener más información sobre las funcionalidades de reenvío de eventos en [!DNL Adobe Experience Platform], lea la [resumen del reenvío de eventos](../../../ui/event-forwarding/overview.md).

Para obtener más información sobre cómo depurar la implementación con la herramienta Experience Platform Debugger y la herramienta de monitorización del reenvío de eventos, lea la [información general de Adobe Experience Platform Debugger](../../../../debugger/home.md) y [Monitorización de actividades en el reenvío de eventos](../../../ui/event-forwarding/monitoring.md).
