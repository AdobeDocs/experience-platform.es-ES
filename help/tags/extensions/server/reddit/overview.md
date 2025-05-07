---
title: Extensión de API de conversiones de Reddit
description: Aprenda a utilizar la extensión de la API de conversiones de Reddit Ads para enviar eventos de interacción de usuarios a Reddit Ads para publicidad segmentada.
last-substantial-update: 2025-05-1
source-git-commit: 603cc86892f518852552eaa2fe1bdeaa296137cf
workflow-type: tm+mt
source-wordcount: '1022'
ht-degree: 1%

---

# Información general sobre la extensión API de conversiones [!DNL Reddit]

Reddit es una plataforma de medios sociales con una base de usuarios diversa, por lo que es ideal para anunciantes que se dirigen a audiencias específicas.

Use la extensión de la API [[!DNL Reddit] Conversiones](https://ads-api.reddit.com/docs/v2/#tag/Conversions-API) para enviar los eventos de interacción de usuarios capturados en Adobe Experience Platform Edge Network a [!DNL Reddit Ads]. Utilice esta extensión para ayudar a su marca a llegar a una audiencia de más de 379 millones de usuarios activos semanales, y comprender mejor el comportamiento del usuario y ejecutar anuncios dirigidos.

Lea esta guía para obtener información sobre cómo instalar, configurar y utilizar la extensión de API de conversiones [!DNL Reddit] en sus [reglas](https://experienceleague.adobe.com/en/docs/experience-platform/tags/ui/rules) de reenvío de eventos.

## Ventajas principales {#benefits}

Utilice la extensión de la API Reddit Conversions para lo siguiente:

- **Llega a tu audiencia**: interactúa con más de 379 millones de usuarios activos semanalmente en [!DNL Reddit].
- **Analizar el comportamiento del usuario**: aproveche los datos de interacción del usuario para comprender el comportamiento y optimizar las campañas.
- **Enviar anuncios de destino**: ejecute anuncios personalizados basados en las interacciones de los usuarios capturadas en Adobe Experience Platform.

## Requisitos previos {#prerequisites}

Debe tener una cuenta de Reddit Ads válida para utilizar esta extensión. Vaya a la [[!DNL Reddit Ads] página de registro](https://business.reddithelp.com/s/article/Create-and-manage-your-Reddit-Ads-account) para registrarse y crear una cuenta si todavía no la tiene. Una vez que haya configurado su cuenta, [solicite acceso a la API de anuncios](https://www.redditforbusiness.com/api-partnership).

### Recopilar detalles de configuración necesarios {#configuration-details}

Para conectar el Experience Platform a [!DNL Reddit], se requieren las siguientes entradas:

| Credencial | Descripción | Ejemplo |
| --- | --- | --- |
| ID de píxel | El ID de píxel es un identificador único asociado con su cuenta de [!DNL Reddit Ads]. Se utiliza para rastrear las interacciones del usuario y los eventos de conversión en el sitio web o la aplicación. Puedes encontrar tu ID de píxel en tu [!DNL Reddit Ads] [cuenta](https://ads.reddit.com/accounts). | 123456789012 |
| Token de acceso de conversión | Su token de acceso de conversión de [!DNL Reddit]. Consulte el documento [[!DNL Reddit] API de conversiones](https://business.reddithelp.com/s/article/conversion-access-token) para obtener instrucciones. <br> **Solo es necesario que realice este proceso una vez, ya que este token no caduca.** | {YOUR_REDDIT_BEARER_TOKEN} |

## Instalar y configurar la extensión [!DNL Reddit] {#install-configure}

Siga estos pasos para instalar y configurar la extensión de API [!DNL Reddit] Conversiones:

1. En la IU de recopilación de datos de Experience Platform, seleccione [!UICONTROL Extensiones] en el panel de navegación izquierdo para acceder al catálogo [!UICONTROL Extensiones]. A continuación [Cree una nueva propiedad de reenvío de eventos](https://experienceleague.adobe.com/en/docs/experience-platform/tags/event-forwarding/overview#properties) o seleccione una propiedad existente.
2. Vaya a **[!UICONTROL Extensiones]** en el panel de navegación izquierdo. Seleccione **[!UICONTROL Catálogo]** y luego seleccione la extensión **[!DNL Reddit]**.
   ![Catálogo de extensiones de Adobe Experience Platform con la extensión Reddit resaltada.](../../../images/extensions/server/reddit/reddit-extension.png)
3. Proporcione los siguientes detalles de configuración:
   - **ID de píxel**: escribe tu ID de píxel [!DNL Reddit Ads].
   - **Token de acceso de conversión**: escribe el token generado en tu cuenta de [!DNL Reddit Ads] y selecciona **[!UICONTROL Guardar]** cuando termines.
     ![Detalles de configuración para la extensión de la API de conversiones de Reddit, incluidos los campos de ID de píxel y Token de acceso de conversión.](../../../images/extensions/server/reddit/reddit-capi-details.png)

## Configuración de una regla de reenvío de eventos {#config-rule}

Después de configurar los elementos de datos, cree reglas de reenvío de eventos para determinar cuándo y cómo se enviarán los eventos a [!DNL Reddit Ads].

1. Vaya a **Reglas** en la propiedad de reenvío de eventos y cree una nueva [regla](https://experienceleague.adobe.com/en/docs/experience-platform/tags/ui/rules).
2. En **Acciones**, agregue una nueva acción y establezca la extensión en **[!DNL Reddit CAPI]**.
3. Establezca **Tipo de acción** en **Enviar evento**.
   ![Interfaz de configuración de reglas de reenvío de eventos para la extensión de API Reddit Conversions, con los campos de extensión y tipo de acción resaltados.](../../../images/extensions/server/reddit/reddit-rule.png)
4. Configure los controles adicionales para su evento como se muestra en la tabla siguiente:

   | Nombre del campo | Descripción | Ejemplo |
   | --- | --- | --- |
   | `Event Name` | Especifique el nombre del evento de conversión. | `Purchase` |
   | `Event Type` | Defina el tipo de evento que puede ser un [evento de conversión Reddit admitido](https://business.reddithelp.com/s/article/supported-conversion-events#supported-conversion-events) o uno personalizado. | `SignUp`, `MyCustomEvent` |
   | `Timestamp` | Proporcione la hora del evento en formato ISO o hora epoch. | `2025-04-15T16:01:00.000Z`, `1744742460000` |
   | `Client Dedupe ID` | Añada un ID único para la anulación de duplicación. | `abc123` |
   | `Match Keys` | Incluya identificadores de usuario y dispositivo para la atribución. | `{"email":"hashed_email@example.com", "phone":"hashed_phone"}` |
   | `Value` | Especifique el valor monetario del evento. | `99.99` |
   | `Currency Code` | Utilice el formato ISO-4217 para la moneda. | `USD` |
   | `Units Sold` | Introduzca la cantidad de artículos comprados. | `3` |
   | `Country Code` | Especifique el país donde se produjo el evento. | `US` |
   | `Data Processing Options` | Agregue indicadores de privacidad, como LDU (Uso de datos limitado). | `{"modes":["LDU"],"country":"US","region":"US-NY"}` |
   | `Consent` | Indique el consentimiento del usuario para el uso de datos publicitarios. | `true` |

5. Seleccione **Conservar cambios** para guardar la regla.

## Metadatos de eventos {#event-metadata}

Lea esta sección para obtener un desglose detallado de los campos de metadatos de evento y datos de usuario, lo que le garantiza que comprende los parámetros opcionales y requeridos para configurar los eventos. Los campos mostrados pueden variar según el tipo de evento seleccionado.

>[!NOTE]
>
>Para obtener los mejores resultados de los eventos de conversión, asegúrate de rellenar todos los campos al configurar [anuncios dinámicos de productos](https://business.reddithelp.com/s/article/dynamic-product-ads).

### Campos de metadatos de evento

![Detalles de configuración para la extensión de la API de conversiones de Reddit, incluidos los campos de ID de píxel y Token de acceso de conversión.](../../../images/extensions/server/reddit/reddit-event-metadata.png)

| Nombre del campo | Descripción | Ejemplo |
| --- | --- | --- |
| `Conversion ID` (obligatorio) | ID único del evento de conversión que se utiliza para la anulación de duplicación. | `abc123` |
| `Item Count` | Número total de elementos para el evento de conversión. | `6` |
| `Currency` | Se ha proporcionado la moneda del valor en formato [ISO-4217](https://www.iso.org/iso-4217-currency-codes.html). | `USD` |
| `Value` | El valor monetario total del evento de conversión, incluidos los decimales. | `1.23` |
| `Products` | Una matriz JSON de objetos con detalles sobre los productos asociados con el evento. Cada objeto debe incluir `id` como mínimo. | `[{"id":"SKU123","name":"ProductName","category":"CategoryName"},{"id":"SKU456","name":"ProductName","category":"CategoryName"}]` |

### Campos de datos de usuario

Los siguientes parámetros son opcionales pero se recomiendan:

| Nombre del campo | Descripción | Ejemplo |
| --- | --- | --- |
| `Email` (recomendado) | Un correo electrónico de usuario con hash o sin hash. | `example@email.com` |
| `External ID` | ID de usuario asignado por el anunciante con hash o sin hash. | `customer12345` |
| `UUID` (recomendado) | El ID generado por el píxel de Reddit en el sitio web. | `1677712978045.b8f7eb7d-b357-437b-8bd3-e1c8166c7132` |
| `IP Address` (recomendado) | La dirección IP del dispositivo del usuario. | `192.168.0.1` |
| `User Agent` (recomendado) | El explorador o la aplicación que utiliza el usuario. | `Chrome/98.0.4758.102` |
| `IDFA` | Identificador de Apple con hash o sin hash para anunciantes. | `8A2E4F6D-0852-4B2A-B9D5-79334DE14B16` |
| `AAID` | ID de Advertising de Android con o sin hash. | `38400000-8cf0-11bd-b23e-10b96e40000d` |
| `Screen Width` | Ancho de la pantalla del usuario. | `1920` |
| `Screen Height` | Altura de la visualización del usuario. | `1080` |
| `Data Processing Options` (formato JSON) | La configuración de privacidad del usuario. Solo admite LDU (uso de datos limitado). | `{"modes":["LDU"],"country":"US","region":"US-NY"}` |

### Consideraciones importantes

Antes de enviar datos a [!DNL Reddit Ads], la extensión almacena en hash y normaliza los valores de los campos siguientes: `Email`, `External ID`, `IDFA` y `AAID`. La extensión no vuelve a hash estos valores si ya se les ha pasado el hash en [!DNL SHA-256].

## Validación e implementación {#validate-deploy}

Después de configurar la extensión y las reglas, valide la integración comprobando los datos de evento en el [[!DNL Reddit Ads] Administrador de eventos](https://business.reddithelp.com/s/article/Events-Manager). Use la [Puntuación de calidad de coincidencia (MQS)](https://business.reddithelp.com/s/article/match-quality-score) para evaluar la precisión y confiabilidad de las integraciones de señal.

Para obtener más información sobre [!DNL Reddit Ads], visita la [documentación de Reddit Ads](https://ads.reddit.com/).

## Pasos siguientes {#next-steps}

Después de leer este documento, debería saber cómo configurar y utilizar la extensión de API de conversiones [!DNL Reddit]. Para obtener más información sobre las funcionalidades de reenvío de eventos en Adobe Experience Platform, consulte la [descripción general del reenvío de eventos](../../../ui/event-forwarding/overview.md) o los siguientes recursos:

- [Compartir claves de coincidencia](https://business.reddithelp.com/s/article/about-attribution-matching-signals) y [metadatos de evento](https://business.reddithelp.com/s/article/about-event-metadata): Aprenda a compartir de forma eficaz las claves de coincidencia y los metadatos de evento.
- [Deduplicar eventos](https://business.reddithelp.com/s/article/event-deduplication): garantice un seguimiento de eventos preciso mediante la deduplicación de eventos.
- [Crear un token de acceso de conversión](https://business.reddithelp.com/helpcenter/s/article/conversion-access-token): siga los pasos para crear un token de acceso de conversión para la autenticación de API segura.
