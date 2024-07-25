---
title: Extensión de reenvío de eventos de API de conversiones de LinkedIn
description: Esta extensión de reenvío de eventos de Adobe Experience Platform le permite medir el rendimiento de su campaña de marketing de LinkedIn.
last-substantial-update: 2023-10-25T00:00:00Z
exl-id: 411e7b77-081e-4139-ba34-04468e519ea5
source-git-commit: c2832821ea6f9f630e480c6412ca07af788efd66
workflow-type: tm+mt
source-wordcount: '790'
ht-degree: 2%

---

# Extensión de API de conversiones de [!DNL LinkedIn]

[[!DNL LinkedIn Conversions API]](https://learn.microsoft.com/en-us/linkedin/marketing/integrations/ads-reporting/conversions-api) es una herramienta de seguimiento de conversión que crea una conexión directa entre los datos de marketing del servidor de un anunciante y [!DNL LinkedIn]. Esto permite a los anunciantes evaluar la eficacia de sus [!DNL LinkedIn] campañas de marketing independientemente de la ubicación de la conversión y utilizar esta información para impulsar la optimización de la campaña. La extensión [!DNL LinkedIn Conversions API] puede ayudar a reforzar el rendimiento y reducir el coste por acción con una atribución más completa, una fiabilidad de los datos mejorada y una entrega mejor optimizada.

## Requisitos previos {#prerequisites}

Debe [crear una regla de conversión](https://www.linkedin.com/help/lms/answer/a1657171) en su cuenta de [!DNL LinkedIn Campaign Manager]. [!DNL Adobe] recomienda incluir &quot;CAPI&quot; al principio del nombre de la regla de conversación para separarla de otros tipos de reglas de conversión que pueda haber configurado.

### Creación de un secreto y un elemento de datos

Cree un nuevo [!DNL LinkedIn] [secreto de reenvío de eventos](../../../ui/event-forwarding/secrets.md) y asígnele un nombre único que signifique el miembro autenticador. Se utilizará para autenticar la conexión con su cuenta y mantener el valor seguro.

A continuación, [cree un elemento de datos](../../../ui/managing-resources/data-elements.md#create-a-data-element) con la extensión [!UICONTROL Core] y un tipo de elemento de datos [!UICONTROL Secret] para hacer referencia al secreto `LinkedIn` que acaba de crear.

## Instalar y configurar la extensión [!DNL LinkedIn] {#install}

Para instalar la extensión, [cree una propiedad de reenvío de eventos](../../../ui/event-forwarding/overview.md#properties) o seleccione una propiedad existente para editar.

Seleccione **[!UICONTROL Extensiones]** en el panel de navegación izquierdo. En la ficha **[!UICONTROL Catálogo]**, seleccione la extensión **[!UICONTROL LinkedIn]** y, a continuación, seleccione **[!UICONTROL Instalar]**.

![Catálogo de extensiones que muestra la tarjeta de extensión [!DNL LinkedIn] que resalta la instalación.](../../../images/extensions/server/linkedin/install-extension.png)

En la siguiente pantalla, escriba el secreto del elemento de datos que creó anteriormente en el campo `Access Token`. El secreto del elemento de datos contendrá su token de OAuth 2 [!DNL LinkedIn]. Seleccione **[!UICONTROL Guardar]** cuando haya terminado.

![La página de configuración de la extensión [!DNL LinkedIn] con el campo [!UICONTROL Token de acceso] y [!UICONTROL Guardar] resaltado.](../../../images/extensions/server/linkedin/configure-extension.png)

## Crear una regla [!DNL Send Conversion] {#tracking-rule}

Una vez configurados todos los elementos de datos, puede empezar a crear reglas de reenvío de eventos que determinan cuándo y cómo se enviarán los eventos a [!DNL LinkedIn].

Cree una nueva regla [rule](../../../ui/managing-resources/rules.md) de reenvío de eventos en su propiedad de reenvío de eventos. En **[!UICONTROL Acciones]**, agregue una nueva acción y establezca la extensión en **[!UICONTROL LinkedIn]**. A continuación, seleccione **[!UICONTROL Enviar conversión]** para el **[!UICONTROL Tipo de acción]**.

![La vista Reglas de propiedad de reenvío de eventos, con los campos necesarios para agregar una configuración de acción de regla de reenvío de eventos resaltada.](../../../images/extensions/server/linkedin/linkedin-event-action.png)

Después de la selección, aparecen controles adicionales para configurar aún más el evento. Seleccione **[!UICONTROL Conservar cambios]** para guardar la regla.

**[!UICONTROL Datos de usuario]**

| Entrada | Descripción |
| --- | --- |
| [!UICONTROL Correo electrónico] | Dirección de correo electrónico del contacto asociado con el evento de conversión. El código de extensión SHA256 codificará el valor de correo electrónico a menos que el valor proporcionado ya sea una cadena SHA256. |
| [!UICONTROL UUID de seguimiento de anuncios de origen de LinkedIn] | Este es un ID de cookie de origen. Los anunciantes deben habilitar el seguimiento de conversión mejorado desde [[!DNL LinkedIn Campaign Manager]](https://www.linkedin.com/help/lms/answer/a423304/enable-first-party-cookies-on-a-linkedin-insight-tag) para activar las cookies de origen que adjuntan un parámetro de ID de clic `li_fat_id` a las direcciones URL de clic. |
| [!UICONTROL Datos de información del cliente] | Este campo contiene un objeto JSON con atributos adicionales que se envían junto con el mensaje.<br><br>En la opción **[!UICONTROL Sin procesar]**, puede pegar el objeto JSON directamente en el campo de texto proporcionado o puede seleccionar el icono del elemento de datos (![Icono del conjunto de datos](/help/images/icons/database.png)) para seleccionarlo de una lista de elementos de datos existentes para representar los datos.<br><br>También puede usar la opción **[!UICONTROL Editor de pares clave-valor de JSON]** para agregar manualmente cada par clave-valor a través de un editor de interfaz de usuario. Cada valor se puede representar mediante una entrada sin procesar o se puede seleccionar un elemento de datos en su lugar. Los valores de clave aceptados son: `firstName`, `lastName`, `companyName`, `title` y `country`. |

{style="table-layout:auto"}

![La sección [!DNL User Data] muestra datos de ejemplo introducidos en los campos.](../../../images/extensions/server/linkedin/configure-extension-user-data.png)

**[!UICONTROL Datos de conversión]**

| Entrada | Descripción |
| --- | --- |
| [!UICONTROL Conversión] | El identificador de la regla de conversión creada en [LinkedIn Campaign Manager](https://www.linkedin.com/help/lms/answer/a1657171). Seleccione la regla de conversión para obtener el ID y copie el ID de la dirección URL del explorador (por ejemplo, `/campaignmanager/accounts/508111232/conversions/15588877`) como `/conversions/<id>`. |
| [!UICONTROL Tiempo de conversión] | Cada marca de tiempo en milisegundos a los que se produjo el evento de conversión. <br><br> Nota: si su origen registra la marca de tiempo de conversión en segundos, inserte 000 al final para transformarla a milisegundos. |
| [!UICONTROL Moneda] | Código de divisa en formato ISO. |
| [!UICONTROL Importe] | Valor de la conversión en una cadena decimal (por ejemplo, &quot;100.05&quot;). |
| [!UICONTROL ID de evento] | ID único generado por los anunciantes para indicar cada evento. Este es un campo opcional y se usa para [deduplication](https://learn.microsoft.com/en-us/linkedin/marketing/conversions/deduplication?view=li-lms-2024-02). |

{style="table-layout:auto"}

![La sección [!DNL Conversion Data] muestra datos de ejemplo en los campos.](../../../images/extensions/server/linkedin/configure-extension-conversions-data.png)

**[!UICONTROL Anulaciones de configuración]**

>NOTA
>
>El campo [!UICONTROL Anulaciones de configuración] permite que un usuario establezca un token de acceso de [!DNL LinkedIn] diferente en cada regla, lo que permite que cada regla use un token de acceso que puede tener acceso a diferentes cuentas de anuncios de [!DNL LinkedIn].

| Entrada | Descripción |
| --- | --- |
| [!UICONTROL Token de acceso] | El token de acceso de [!DNL LinkedIn]. |

![La sección [!DNL Configuration Overrides] muestra datos de ejemplo introducidos en el campo.](../../../images/extensions/server/linkedin/configure-extension-configuration-override.png)

## Pasos siguientes

Esta guía explica cómo enviar datos a [!DNL LinkedIn] mediante la extensión de reenvío de eventos [!DNL LinkedIn Conversions API]. Para obtener más información sobre las capacidades de reenvío de eventos en [!DNL Adobe Experience Platform], lea la [descripción general del reenvío de eventos](../../../ui/event-forwarding/overview.md).

Para obtener más información sobre cómo depurar la implementación con la herramienta de supervisión de Experience Platform Debugger y reenvío de eventos, lea la [descripción general del Adobe Experience Platform Debugger](../../../../debugger/home.md) y [Supervisar las actividades en el reenvío de eventos](../../../ui/event-forwarding/monitoring.md).
