---
title: Información general sobre la extensión API de conversiones Amazon
description: Comparta interacciones con sitios web directamente con Amazon mediante la API de eventos web de Adobe Experience Platform
last-substantial-update: 2025-04-17T00:00:00Z
exl-id: 20339b6e-15e3-4d0e-8870-a3a85b7e66fd
source-git-commit: 306795c0fdd665b1813c70c41bd9b5d58f5507e6
workflow-type: tm+mt
source-wordcount: '957'
ht-degree: 2%

---

# Información general sobre la extensión API de eventos web [!DNL Amazon]

La extensión de la API de conversiones [!DNL Amazon] crea una conexión directa entre los datos de marketing del servidor de un anunciante y [!DNL Amazon]. Permite a los anunciantes evaluar la eficacia de la campaña independientemente de la ubicación de conversión y optimizar las campañas en consecuencia. Esta extensión proporciona atribución completa, fiabilidad de los datos y una entrega optimizada.

## [!DNL Amazon] requisitos previos {#prerequisites}

Antes de instalar y configurar la extensión de API Conversiones [!DNL Amazon], complete los siguientes pasos previos para garantizar la autenticación y el acceso a datos adecuados:

### Crear un secreto y un elemento de datos {#secret}

Cree un nuevo [!DNL Amazon] [secreto de reenvío de eventos](../../../ui/event-forwarding/secrets.md) y asígnele un nombre único que signifique el miembro autenticador. Se utilizará para autenticar la conexión con su cuenta y mantener el valor seguro.

A continuación, [cree un elemento de datos](../../../ui/managing-resources/data-elements.md#create-a-data-element) con la extensión [!UICONTROL Core] y un tipo de elemento de datos [!UICONTROL Secret] para hacer referencia al secreto `Amazon` que acaba de crear.

### Recopilar detalles de configuración necesarios {#configuration-details}

Para conectar Experience Platform a [!DNL Amazon], escriba los siguientes detalles:

| Tipo de clave | Descripción |
| --- | --- |
| ID de cuenta | El identificador único de la cuenta de [!DNL Amazon]. |
| ID de entidad | El identificador de un perfil asociado a la cuenta del anunciante. Se encuentra en la dirección URL del portal del Administrador de campañas, con el prefijo `entity`. |
| Token de acceso | El token de acceso de su aplicación, que no caduca y que se usa para autenticarse en la API [!DNL Amazon] a través de OAuth. Consulte la [documentación de la API de Amazon sobre autenticación](https://developer.amazon.com/docs/app-porting/device-messaging-fit-obtain-api-key.html) para obtener instrucciones. |

## Instalar y configurar la extensión [!DNL Amazon] {#install-configure}

Siga estos pasos para instalar y configurar la extensión de API [!DNL Amazon] Conversiones:

1. Cree o edite una propiedad de reenvío de eventos.
2. Vaya a **Extensiones** en el panel de navegación izquierdo y, a continuación, seleccione la extensión [!DNL Amazon] en la pestaña Catálogo.
3. Seleccione **Instalar**.

   ![Tarjeta de extensión de Amazon resaltada en el catálogo de extensiones de Adobe Experience Platform.](../../../images/extensions/server/amazon/amazon-extension.png)

4. Configure la extensión con los siguientes detalles:
   - **Token de acceso**: El secreto del elemento de datos que contiene el token de OAuth 2.

     ![Interfaz de configuración que resalta el campo para introducir el secreto del elemento de datos para el token de OAuth 2.](../../../images/extensions/server/amazon/amazon-oauth2-token-field.png)

   - **ID de entidad**: su ID de entidad (que se encuentra en la URL del portal de Campaign Manager con el prefijo &quot;entity&quot;).

     ![Interfaz de portal de Campaign Manager con el campo Identificador de entidad resaltado.](../../../images/extensions/server/amazon/campaign-manager-entity-id.png)

5. Seleccione **Guardar** para completar la configuración.

## Configuración de una regla de reenvío de eventos {#config-rule}

Una vez configurados todos los elementos de datos, cree reglas de reenvío de eventos para determinar cuándo y cómo se enviarán los eventos a [!DNL Amazon].

1. Vaya a **Reglas** y cree una nueva regla de reenvío de eventos.
2. En **Acciones**, seleccione **Extensión de la API de conversiones de Amazon**.
3. Establezca **Tipo de acción** en **Importar eventos de conversión**.

   ![Interfaz de configuración de regla de reenvío de eventos con el tipo de acción establecido en Importar eventos de conversión.](../../../images/extensions/server/amazon/amazon-import-conversion-events.png)

### Configuración de datos de evento de conversión {#conversion-event-data}

Los datos de eventos de conversión son esenciales para realizar un seguimiento de las interacciones de los usuarios y medir la eficacia de las campañas. Al reenviar estos datos a [!DNL Amazon], puede obtener información sobre el comportamiento del usuario, optimizar las campañas y garantizar una atribución precisa para las conversiones.

En la tabla siguiente se describen las propiedades clave necesarias para configurar y reenviar los datos de evento de conversión:

| Entrada | Descripción | Requerido | Ejemplo |
| --- | --- | --- | --- |
| `name` | Nombre del evento importado. | Sí | `My Event Name` |
| `eventType` | El tipo de evento estándar de Amazon asociado al evento y utilizado para el sistema de informes. | Sí | `Add to Shopping Cart` |
| `eventActionSource` | La plataforma desde la que se originó el evento. | Sí | `WEBSITE` |
| `clientDedupeId` | `id` especificado por el anunciante para el evento de conversión. En el caso de los eventos con el mismo `clientDedupeId`, solo se conservará el primer evento y se perderán todos los eventos subsiguientes. | Opcional | `3234A398932` |
| `timestamp` | La marca de tiempo del informe de cuándo se produjo el evento. La marca de tiempo puede ser de hasta 7 días antes de enviar un evento. No se procesarán los datos con más de 7 días. | Sí | `2023-05-08T14:04:28Z` |
| `matchKeys` | Matriz que representa los tipos/valores de identificador de cliente y dispositivo que se utilizarán para la atribución a eventos de tráfico. | Sí | — |
| `matchKeys > type` | El tipo de identificador utilizado para la atribución. | Sí | — |
| `matchKeys > value` | El valor de identificador utilizado para la atribución. | Sí | Lista de valores de identificador con hash SHA-256 del cliente que realizó el evento. |
| `value` | El valor del evento. | Opcional | `5` o `0.99` |
| `currencyCode` | El código de moneda asociado con el `value` del evento en formato ISO-4217. Solo se aplica al tipo de evento de Compras Off Amazon. Si no se proporciona, se utilizará la configuración del código de moneda de la definición de conversión. | Opcional | `USD`, `EUR`, `GBP`, etc. |
| `unitsSold` | Número de artículos comprados. Solo se aplica al tipo de evento de Compras Off Amazon. Si no se proporciona en el evento de conversión, se aplicará un valor predeterminado de `1`. | Opcional | — |
| `countryCode` | Este valor se basa en los códigos de país ISO 3166-1 alpha-2 de dos letras definidos en la norma ISO 3166-1, que forma parte de la norma ISO 3166 publicada por la Organización Internacional de Normalización (ISO), para representar países, territorios dependientes y áreas especiales de interés geográfico. | Sí | — |
| `dataProcessingOptions` | Indica el consentimiento del usuario para el uso de datos publicitarios. | Opcional | LIMITED_DATA_USE |

- Seleccione **[!UICONTROL Conservar cambios]** para guardar la regla.

![Interfaz de configuración de parámetros de evento con el botón Conservar cambios resaltado.](../../../images/extensions/server/amazon/event-parameters.png)

![Interfaz de configuración de parámetros de evento adicionales con el botón Conservar cambios resaltado.](../../../images/extensions/server/amazon/additional-event-parameters.png)

## Deduplicación de eventos {#deduplication}

La deduplicación es esencial para garantizar unos informes precisos y evitar recuentos de conversiones inflados al utilizar la etiqueta Advertising (AAT) [!DNL Amazon] y la extensión de la API de conversiones [!DNL Amazon] para rastrear los mismos eventos.

### ¿Cuándo se requiere la deduplicación?

- **Obligatorio**: Si se envía el mismo evento desde el cliente (AAT) y el servidor (API de conversiones).
- **No se requiere**: Si se envían distintos tipos de eventos desde el cliente y el servidor sin ninguna superposición.

### Activación de la deduplicación

Para habilitar la anulación de duplicación, incluya el campo `clientDedupeId` en cada evento compartido. Este identificador único permite a [!DNL Amazon] distinguir entre eventos del lado del cliente y del lado del servidor, así como evitar entradas duplicadas.

Al configurar correctamente la deduplicación, puede asegurarse de que los datos de optimización sigan siendo precisos y de que los informes no se vean afectados negativamente.

Para obtener más información, consulte la [Guía de anulación de duplicación de eventos de Amazon](https://advertising.amazon.com/).

## Pasos siguientes {#next-steps}

En esta guía se explica cómo configurar y enviar eventos de conversión a [!DNL Amazon] mediante la extensión de API de conversiones [!DNL Amazon]. Para obtener más información sobre las capacidades de reenvío de eventos en [!DNL Adobe Experience Platform], consulte la [descripción general del reenvío de eventos](../../../ui/event-forwarding/overview.md).

Para obtener más información sobre cómo depurar la implementación con la herramienta de supervisión de Experience Platform Debugger y reenvío de eventos, lea la [descripción general de Adobe Experience Platform Debugger](/help/debugger/home.md) y [Supervisar actividades](../../../ui/event-forwarding/monitoring.md) en el reenvío de eventos.
