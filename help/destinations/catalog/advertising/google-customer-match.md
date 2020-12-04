---
keywords: google customer match;Google customer match;Google Customer Match
title: Destino de coincidencia de clientes de Google
seo-title: Destino de coincidencia de clientes de Google
description: La coincidencia de clientes de Google le permite utilizar sus datos en línea y sin conexión para comunicarse con sus clientes y volver a interactuar con ellos en las propiedades que posee y opera Google, como Search, Shopping, Gmail y YouTube.
seo-description: La coincidencia de clientes de Google le permite utilizar sus datos en línea y sin conexión para comunicarse con sus clientes y volver a interactuar con ellos en las propiedades que posee y opera Google, como Search, Shopping, Gmail y YouTube.
translation-type: tm+mt
source-git-commit: f2fdc3b75d275698a4b1e4c8969b1b840429c919
workflow-type: tm+mt
source-wordcount: '1544'
ht-degree: 0%

---


# Destino de coincidencia de clientes de Google

## Información general {#overview}

[La coincidencia](https://support.google.com/google-ads/answer/6379332?hl=en) de clientes de Google le permite utilizar sus datos en línea y sin conexión para comunicarse con sus clientes y volver a interactuar con ellos en las propiedades que posee y opera Google, como: [!DNL Search], [!DNL Shopping], [!DNL Gmail], y [!DNL YouTube].

![Destino de Coincidencia de clientes de Google en la interfaz de usuario de CDP en tiempo real](../../assets/catalog/advertising/google-customer-match/catalog.png)

## Casos de uso

Para ayudarle a comprender mejor cómo y cuándo debe utilizar el destino, a continuación se muestran ejemplos de casos de uso que los clientes de la Plataforma de datos del cliente en tiempo real pueden resolver mediante esta función. [!DNL Google Customer Match]

### Caso de uso n.º 1

Una marca de ropa deportiva quiere llegar a los clientes actuales a través [!DNL Google Search] y [!DNL Google Shopping] para personalizar ofertas y artículos en función de sus compras anteriores y del historial de navegación. La marca de ropa puede ingerir direcciones de correo electrónico de su propio CRM a CDP en tiempo real, generar segmentos a partir de sus propios datos sin conexión y enviar estos segmentos para [!DNL Google Customer Match] que se utilicen en todo [!DNL Search] y [!DNL Shopping]optimizando el gasto en publicidad.

### Caso de uso n.º 2

Una destacada compañía tecnológica acaba de lanzar un nuevo teléfono. En un esfuerzo por promocionar este nuevo modelo de teléfono, buscan concienciar sobre las nuevas características y funcionalidades del teléfono a los clientes que poseen modelos anteriores de sus teléfonos.

Para promocionar la versión, cargan direcciones de correo electrónico de su base de datos CRM en CDP en tiempo real, usando las direcciones de correo electrónico como identificadores. Los segmentos se crean en función de los clientes que poseen modelos de teléfono antiguos y se envían a [!DNL Google Customer Match] para que puedan destinatario a los clientes actuales, a los clientes que poseen modelos de teléfono antiguos y a clientes similares en [!DNL YouTube].

## Administración de datos para [!DNL Google Customer Match] destinos {#data-governance}

Los destinos de CDP en tiempo real pueden tener ciertas reglas y obligaciones para los datos enviados o recibidos desde la plataforma de destino. Usted es el responsable de comprender las limitaciones y obligaciones de sus datos y de cómo los utiliza en Adobe Experience Platform y en la plataforma de destino. Adobe Experience Platform proporciona herramientas de administración de datos para ayudarle a administrar algunas de esas obligaciones de uso de datos. [Obtenga más](../../..//data-governance/labels/overview.md) información sobre las herramientas y políticas de administración de datos.

## Tipo de exportación e identidades {#export-type}

**Exportación** de segmentos: está exportando todos los miembros de un segmento (audiencia) con los identificadores (nombre, número de teléfono, etc.) en el [!DNL Google Customer Match] destino.

**Identidades** : puede usar correos electrónicos sin procesar o con hash como ID de cliente en Google

## [!DNL Google Customer Match] requisitos previos de cuenta {#google-account-prerequisites}

Antes de configurar un [!DNL Google Customer Match] destino en CDP en tiempo real, asegúrese de leer y cumplir la política de Google para el uso [!DNL Customer Match], que se describe en la documentación [de soporte de](https://support.google.com/google-ads/answer/6299717)Google.

### Lista de permitidos {#allowlist}

>[!NOTE]
>
>Es obligatorio agregarlo a la lista de permitidos de Google antes de configurar su primer [!DNL Google Customer Match] destino en CDP en tiempo real. Asegúrese de que Google haya completado el proceso de lista de permitidos que se describe a continuación antes de crear un destino.

Antes de crear el [!DNL Google Customer Match] destino en CDP en tiempo real, debe ponerse en contacto con Google y seguir las instrucciones de lista de permitidos en [Usar socios de coincidencia de cliente para cargar sus datos](https://support.google.com/google-ads/answer/7361372?hl=en&amp;ref_topic=6296507) en la documentación de Google.


### Requisitos de hash de correo electrónico {#hashing-requirements}

<!--

>[!IMPORTANT]
>
> When using mobile device IDs as identifiers, an AppId must be provided in the activation flow. For more information, see step 6 in the [Activate segments](#activate-segments) section of this page.

-->

Google exige que no se envíe información de identificación personal (PII) de manera clara. Por lo tanto, las audiencias activadas en [!DNL Google Customer Match] deben bloquearse las direcciones de correo electrónico con *hash* . Puede elegir hash las direcciones de correo electrónico antes de ingerirlas en Adobe Experience Platform, o puede elegir trabajar con las direcciones de correo electrónico de forma clara en Experience Platform y hacer que nuestro algoritmo las incluya en activación.

Para obtener más información sobre los requisitos de hash de Google y otras restricciones de activación, consulte las siguientes secciones en la documentación de Google:

* [[!DNL Customer Match] con dirección de correo electrónico, dirección o ID de usuario](https://developers.google.com/adwords/api/docs/guides/remarketing#customer_match_with_email_address_address_or_user_id)
* [[!DNL Customer Match] consideraciones](https://developers.google.com/adwords/api/docs/guides/remarketing#customer_match_considerations)

<!--

Links to be added when activation based on phone number and device IDs becomes available.

* [Customer Match with phone number](https://developers.google.com/adwords/api/docs/guides/remarketing#customer_match_with_phone_number)
* [Customer Match with mobile device IDs](https://developers.google.com/adwords/api/docs/guides/remarketing#customer_match_with_mobile_device_ids)

-->

Para obtener más información sobre la ingesta de direcciones de correo electrónico en Experience Platform, consulte la información general [sobre la ingestión de](../../../ingestion/batch-ingestion/overview.md) lotes y la información general [sobre la ingestión](../../../ingestion/streaming-ingestion/overview.md)por lotes.

Si selecciona hash para las direcciones de correo electrónico usted mismo, asegúrese de cumplir con los requisitos de Google, descritos en los vínculos anteriores.


>[!IMPORTANT]
>
>Si decide no usar hash en las direcciones de correo electrónico, CDP en tiempo real lo hará por usted cuando active segmentos en [!DNL Google Customer Match]. En el flujo de trabajo [de](#activate-segments) activación (consulte el paso 5), seleccione la `Email` opción como se muestra a continuación para las direcciones *de correo electrónico de texto* sin formato y `Email_LC_SHA256` para las direcciones *de correo electrónico* con hash.

![Hashing en activación](../../assets/catalog/advertising/google-customer-match/identity-mapping.png)

## Conectar al destino {#connect-destination}

En **[!UICONTROL Destinos]** > **[!UICONTROL Catálogo]**, desplácese hasta la categoría **[!UICONTROL Publicidad]** . Seleccione [!DNL Google Customer Match]y, a continuación, seleccione **[!UICONTROL Configurar]**.

![Conectar con el destino de Coincidencia de clientes de Google](../../assets/catalog/advertising/google-customer-match/connect.png)

>[!NOTE]
>
>Si ya existe una conexión con este destino, puede ver un botón **[!UICONTROL Activar]** en la tarjeta de destino. Para obtener más información sobre la diferencia entre **[!UICONTROL Activar]** y **[!UICONTROL Configurar]**, consulte la sección [Catálogo](../../ui/destinations-workspace.md#catalog) de la documentación del espacio de trabajo de destino.

En el paso **Cuenta** , si ha configurado anteriormente una conexión con su [!DNL Google Customer Match] destino, seleccione Cuenta **** existente y seleccione la conexión existente. O bien, puede seleccionar **[!UICONTROL Nueva cuenta]** para configurar una nueva conexión con [!DNL Google Customer Match]. Seleccione **[!UICONTROL Conectar al destino]** para iniciar sesión y conectar Adobe Experience Cloud a su [!DNL Google Ad] cuenta.

>[!NOTE]
>
>CDP en tiempo real admite la validación de credenciales en el proceso de autenticación y muestra un mensaje de error si se introducen credenciales incorrectas en la [!DNL Google Ad] cuenta. Esto garantiza que no se complete el flujo de trabajo con credenciales incorrectas.

![Conectar con el destino de Coincidencia de clientes de Google: paso de autenticación](../../assets/catalog/advertising/google-customer-match/connection.png)

Una vez confirmadas las credenciales y que Adobe Experience Cloud esté conectado a su cuenta de Google, puede seleccionar **[!UICONTROL Siguiente]** para continuar con el paso de **[!UICONTROL configuración]** .

![Credenciales confirmadas](../../assets/catalog/advertising/google-customer-match/connection-success.png)

En el paso **[!UICONTROL Autenticación]** , escriba un [!UICONTROL Nombre] y una [!UICONTROL Descripción] para el flujo de activación y rellene el ID [!UICONTROL de]cuenta de Google.

También en este paso, puede seleccionar cualquier caso **[!UICONTROL de uso de]** Marketing que deba aplicarse a este destino. Los casos de uso de mercadotecnia indican la intención para la cual se exportarán los datos al destino. Puede seleccionar entre los casos de uso de mercadotecnia definidos por el Adobe o puede crear su propio caso de uso de mercadotecnia. Para obtener más información sobre los casos de uso de mercadotecnia, consulte la página [Administración de datos en tiempo real de CDP](../../../rtcdp/privacy/data-governance-overview.md#destinations) . Para obtener información sobre los casos individuales de uso de mercadotecnia definidos por el Adobe, consulte la descripción general [de las políticas de uso de](../../../data-governance/policies/overview.md#core-actions)datos.

Seleccione **[!UICONTROL Crear destino]** después de completar los campos anteriores.

>[!IMPORTANT]
>
> * El caso de uso de la mercadotecnia **[!UICONTROL Combinar con PII]** está seleccionado de forma predeterminada para el [!DNL Google Customer Match] destino y no se puede eliminar.
> * Para [!DNL Google Customer Match] destinos. **[!UICONTROL El ID]** de cuenta es su ID de cliente con Google. El formato del ID es xxx-xxx-xxxx.


![Coincidencia de clientes de Connect Google: paso de autenticación](../../assets/catalog/advertising/google-customer-match/authentication.png)

Se ha creado el destino. Puede seleccionar **[!UICONTROL Guardar y salir]** si desea activar segmentos más adelante o puede seleccionar **[!UICONTROL Siguiente]** para continuar el flujo de trabajo y seleccionar los segmentos que desea activar. En cualquier caso, consulte la siguiente sección, [Activar segmentos en [!DNL Google Customer Match]](#activate-segments), para el resto del flujo de trabajo.

## Activar segmentos para [!DNL Google Customer Match] {#activate-segments}

Para activar segmentos en [!DNL Google Customer Match], siga los pasos a continuación:

En **[!UICONTROL Destinos > Examinar]**, seleccione el [!DNL Google Customer Match] destino en el que desea activar los segmentos.

Haga clic en el nombre del destino. Esto le lleva al flujo Activar.

![activate-flow](../../assets/catalog/advertising/google-customer-match/activate-flow.png)

Tenga en cuenta que si ya existe un flujo de activación para un destino, puede ver los segmentos que se están enviando al destino. Seleccione **[!UICONTROL Editar activación]** en el carril derecho y siga los pasos a continuación para modificar los detalles de la activación.

Seleccione **[!UICONTROL Activar]**. En el flujo de trabajo **[!UICONTROL Activar destino]** , en la página **[!UICONTROL Seleccionar segmentos]** , seleccione los segmentos a los que desea enviar [!DNL Google Customer Match].

![segmentos a destino](../../assets/catalog/advertising/google-customer-match/activate-segments.png)

En el paso Asignación **[!UICONTROL de]** identidad, seleccione qué atributos se incluirán como identidad en este destino. Seleccione **[!UICONTROL Añadir nueva asignación]** y examine el esquema, seleccione correo electrónico o correo electrónico con hash y asígneles a la identidad de destinatario correspondiente.

![pantalla inicial de asignación de identidad](../../assets/catalog/advertising/google-customer-match/identity-mapping.png)

**Dirección de correo electrónico de texto sin formato como identidad** principal: Si tiene direcciones de correo electrónico de texto sin formato (sin hash) como identidad principal en el esquema, seleccione el campo Correo electrónico en los atributos **** de origen y asígnelo al campo Correo electrónico de la columna derecha en Identidades **[!UICONTROL de]** Destinatario, como se muestra a continuación:

![seleccionar identidad de correos electrónicos de texto sin formato](../../assets/catalog/advertising/google-customer-match/raw-email.gif)

**Dirección de correo electrónico con hash como identidad** principal: Si tiene direcciones de correo electrónico con hash como identidad principal en el esquema, seleccione el campo de correo electrónico con hash en los atributos **** de origen y asígnelo al campo Email_LC_SHA256 en la columna derecha debajo de Identidades **[!UICONTROL de]** Destinatario, como se muestra a continuación:

![seleccionar identidad de correos electrónicos con hash](../../assets/catalog/advertising/google-customer-match/hashed-emails.gif)

En la página **[!UICONTROL Programación]** de segmentos, puede establecer la fecha de inicio para enviar datos al destino.

En la página **[!UICONTROL Revisar]** , puede ver un resumen de su selección. Seleccione **[!UICONTROL Cancelar]** para desglosar el flujo, **[!UICONTROL Atrás]** para modificar la configuración o **[!UICONTROL Finalizar]** para confirmar la selección y el inicio de envío de datos al destino.

>[!IMPORTANT]
>
>En este paso, CDP en tiempo real comprueba las infracciones de las políticas de uso de datos. A continuación se muestra un ejemplo de violación de una política. No puede completar el flujo de trabajo de activación de segmentos hasta que no haya resuelto la infracción. Para obtener información sobre cómo resolver las infracciones de políticas, consulte Aplicación de [políticas](../../../rtcdp/privacy/data-governance-overview.md#enforcement) en la sección de documentación de administración de datos.

![confirmación-selección](../../assets/common/data-policy-violation.png)

Si no se ha detectado ninguna infracción de directiva, seleccione **[!UICONTROL Finalizar]** para confirmar la selección y el inicio al enviar datos al destino.

![confirmación-selección](../../assets/catalog/advertising/google-customer-match/review.png)

## Verifique que la activación del segmento se haya realizado correctamente {#verify-activation}

Después de completar el flujo de activación, cambie a su cuenta de **[!UICONTROL Google Ads]** . Los segmentos activados ahora se mostrarán en su cuenta de Google como listas de clientes. Tenga en cuenta que, según el tamaño del segmento, algunas audiencias no se rellenarán a menos que haya más de 100 usuarios activos para servir.

## Recursos adicionales {#additional-resources}

* [Integrar la coincidencia de clientes de Google: tutorial de vídeo](https://experienceleague.adobe.com/docs/platform-learn/tutorials/rtcdp/integrate-with-google-customer-match.html)