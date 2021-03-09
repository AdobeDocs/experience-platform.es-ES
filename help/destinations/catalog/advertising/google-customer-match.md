---
keywords: coincidencia de clientes de google;coincidencia de clientes de Google;coincidencia de clientes de Google
title: Conexión de Google Customer Match
description: Google Customer Match le permite utilizar sus datos en línea y sin conexión para llegar a sus clientes y volver a interactuar con ellos en todas las propiedades de Google que usted posee y gestiona, como Search, Shopping, Gmail y YouTube.
translation-type: tm+mt
source-git-commit: 494b41265a0eec71ec15c7896eb8c652b3164e18
workflow-type: tm+mt
source-wordcount: '1420'
ht-degree: 0%

---


# [!DNL Google Customer Match] connection

[Las ](https://support.google.com/google-ads/answer/6379332?hl=en) coincidencias de clientes de Google le permiten usar sus datos en línea y sin conexión para llegar a sus clientes y volver a interactuar con ellos en todas las propiedades de Google y en las que opera, como:  [!DNL Search],  [!DNL Shopping],  [!DNL Gmail], y  [!DNL YouTube].

![Destino de Google Customer Match en la interfaz de usuario de Adobe Experience Platform](../../assets/catalog/advertising/google-customer-match/catalog.png)

## Casos de uso

Para ayudarle a comprender mejor cómo y cuándo debe utilizar el destino [!DNL Google Customer Match], estos son ejemplos de casos de uso que los clientes de Adobe Experience Platform pueden resolver utilizando esta función.

### Caso de uso n.º 1

Una marca de ropa deportiva quiere llegar a los clientes existentes a través de [!DNL Google Search] y [!DNL Google Shopping] para personalizar ofertas y artículos en función de sus compras anteriores y del historial de navegación. La marca de ropa puede introducir direcciones de correo electrónico desde su propio CRM a Experience Platform, generar segmentos a partir de sus propios datos sin conexión y enviar estos segmentos a [!DNL Google Customer Match] para que se utilicen en [!DNL Search] y [!DNL Shopping], lo que optimiza su gasto en publicidad.

### Caso de uso n.º 2

Una importante compañía tecnológica acaba de lanzar un nuevo teléfono. En un esfuerzo por promocionar este nuevo modelo de teléfono, buscan sensibilizar sobre las nuevas características y funcionalidades del teléfono a los clientes que poseen modelos anteriores de sus teléfonos.

Para promocionar la versión, cargan direcciones de correo electrónico de su base de datos CRM en Experience Platform, utilizando las direcciones de correo electrónico como identificadores. Los segmentos se crean en función de los clientes que son propietarios de modelos de teléfono antiguos y se envían a [!DNL Google Customer Match] para que puedan dirigirse a los clientes actuales, a los clientes que son propietarios de modelos de teléfono antiguos y a clientes similares en [!DNL YouTube].

## Detalles de destino {#destination-specs}

### Administración de datos para destinos [!DNL Google Customer Match] {#data-governance}

Los destinos de Experience Platform pueden tener ciertas reglas y obligaciones para los datos enviados a la plataforma de destino o recibidos de ella. Usted es el responsable de comprender las limitaciones y obligaciones de sus datos y cómo utiliza esos datos en Adobe Experience Platform y la plataforma de destino. Adobe Experience Platform proporciona herramientas de control de datos que le ayudan a administrar algunas de esas obligaciones de uso de datos. [Obtenga ](../../..//data-governance/labels/overview.md) más información sobre las herramientas y políticas de control de datos.

### Tipo de exportación e identidades {#export-type}

**Exportación de segmentos** : está exportando todos los miembros de un segmento (audiencia) con los identificadores (nombre, número de teléfono, etc.) se utiliza en el destino [!DNL Google Customer Match].

**Identidades** : puede usar correos electrónicos sin procesar o con hash como ID de cliente en Google.

### [!DNL Google Customer Match] requisitos previos de la cuenta  {#google-account-prerequisites}

Antes de configurar un destino [!DNL Google Customer Match] en Experience Platform, asegúrese de leer y adherirse a la directiva de Google para utilizar [!DNL Customer Match], que se describe en la [documentación de asistencia de Google](https://support.google.com/google-ads/answer/6299717).

### Permitir lista {#allowlist}

>[!NOTE]
>
>Es obligatorio añadirse a la lista de permitidos de Google antes de configurar su primer destino [!DNL Google Customer Match] en Experience Platform. Asegúrese de que Google haya completado el proceso de la lista de permitidos que se describe a continuación antes de crear un destino.

Antes de crear el destino [!DNL Google Customer Match] en Experience Platform, debe ponerse en contacto con Google y seguir las instrucciones de la lista de permitidos en [Use Customer Match partners para cargar los datos](https://support.google.com/google-ads/answer/7361372?hl=en&amp;ref_topic=6296507) en la documentación de Google.

Además, hay una segunda lista de permitidos de Google a la que debe agregar su cuenta si planea cargar datos mediante el [User_ID](https://developers.google.com/adwords/api/docs/guides/remarketing#customer_match_with_email_address_address_or_user_id) de Google. Póngase en contacto con el administrador de cuentas de Google para asegurarse de que se ha añadido a las listas de permitidos.

### Requisitos de coincidencia de ID {#id-matching-requirements}

[!DNL Google] exige que no se envíe con claridad ninguna información de identificación personal (PII). Por lo tanto, las audiencias activadas en [!DNL Google Customer Match] pueden desactivarse mediante identificadores *hash*, como direcciones de correo electrónico o números de teléfono.

En función del tipo de ID que incorpore en Adobe Experience Platform, debe cumplir sus requisitos correspondientes.

#### Requisitos de hash de números de teléfono {#phone-number-hashing-requirements}

Existen dos métodos para activar los números de teléfono en [!DNL Google Customer Match]:

* **Ingesta de números** de teléfono sin procesar: puede introducir números de teléfono sin procesar en el  [!DNL E.164] formato  [!DNL Platform], que se colocan automáticamente en hash tras la activación. Si elige esta opción, asegúrese de introducir siempre sus números de teléfono sin procesar en el espacio de nombres `Phone_E.164`.
* **Ingesta de números** de teléfono con hash: puede prehash sus números de teléfono antes de ingerirlos a  [!DNL Platform]. Si elige esta opción, asegúrese de introducir siempre los números de teléfono con hash en el espacio de nombres `PHONE_SHA256_E.164`.

>[!NOTE]
>
>Los números de teléfono introducidos en el espacio de nombres `Phone` no se pueden activar en [!DNL Google Customer Match].

#### Requisitos de hash de correo electrónico {#hashing-requirements}

Puede elegir hash de las direcciones de correo electrónico antes de ingerirlas en Adobe Experience Platform, o puede elegir trabajar con direcciones de correo electrónico claramente en Experience Platform y tener nuestro algoritmo hash en la activación.

Para obtener más información sobre los requisitos hash de Google y otras restricciones en la activación, consulte las siguientes secciones en la documentación de Google:

* [[!DNL Customer Match] con dirección de correo electrónico, dirección o ID de usuario](https://developers.google.com/adwords/api/docs/guides/remarketing#customer_match_with_email_address_address_or_user_id)
* [[!DNL Customer Match] consideraciones](https://developers.google.com/adwords/api/docs/guides/remarketing#customer_match_considerations)
* [Customer Match con número de teléfono](https://developers.google.com/adwords/api/docs/guides/remarketing#customer_match_with_phone_number)
* [Coincidencia de cliente con ID de dispositivos móviles](https://developers.google.com/adwords/api/docs/guides/remarketing#customer_match_with_mobile_device_ids)


Para obtener más información sobre la ingesta de direcciones de correo electrónico en Experience Platform, consulte la [información general sobre la ingesta por lotes](../../../ingestion/batch-ingestion/overview.md) y la [información general sobre la ingesta de flujo](../../../ingestion/streaming-ingestion/overview.md).

Si selecciona hash para las direcciones de correo electrónico usted mismo, asegúrese de cumplir con los requisitos de Google, descritos en los vínculos anteriores.

#### Uso de áreas de nombres personalizadas {#custom-namespaces}

Antes de utilizar el espacio de nombres `User_ID` para enviar datos a Google, asegúrese de sincronizar sus propios identificadores con [!DNL gTag]. Consulte la [documentación oficial de Google](https://support.google.com/google-ads/answer/9199250) para obtener información detallada.

<!-- Data from unhashed namespaces is automatically hashed by [!DNL Platform] upon activation.

Attribute source data is not automatically hashed. When your source field contains unhashed attributes, check the **[!UICONTROL Apply transformation]** option, to have [!DNL Platform] automatically hash the data on activation.
![Identity mapping transformation](../../assets/ui/activate-destinations/identity-mapping-transformation.png) -->

## Conectarse al destino {#connect-destination}

En **[!UICONTROL Destinations]** > **[!UICONTROL Catalog]**, desplácese hasta la categoría **[!UICONTROL Advertising]**. Seleccione [!DNL Google Customer Match] y, a continuación, seleccione **[!UICONTROL Configurar]**.

![Conectarse al destino de Google Customer Match](../../assets/catalog/advertising/google-customer-match/connect.png)

>[!NOTE]
>
>Si ya existe una conexión con este destino, puede ver un botón **[!UICONTROL Activate]** en la tarjeta de destino. Para obtener más información sobre la diferencia entre **[!UICONTROL Activate]** y **[!UICONTROL Configure]**, consulte la sección [Catalog](../../ui/destinations-workspace.md#catalog) de la documentación del espacio de trabajo de destino.

En el paso **Cuenta**, si anteriormente ha configurado una conexión con su destino [!DNL Google Customer Match], seleccione **[!UICONTROL Cuenta existente]** y seleccione la conexión existente. O bien, puede seleccionar **[!UICONTROL Nueva cuenta]** para configurar una nueva conexión a [!DNL Google Customer Match]. Seleccione **[!UICONTROL Connect to destination]** para iniciar sesión y conectar Adobe Experience Cloud a su cuenta [!DNL Google Ad].

>[!NOTE]
>
>Experience Platform admite la validación de credenciales en el proceso de autenticación y muestra un mensaje de error si se introducen credenciales incorrectas en la cuenta [!DNL Google Ad]. Esto garantiza que no complete el flujo de trabajo con credenciales incorrectas.

![Conectarse al destino de Google Customer Match: paso de autenticación](../../assets/catalog/advertising/google-customer-match/connection.png)

Una vez confirmadas las credenciales y conectada Adobe Experience Cloud a su cuenta de Google, puede seleccionar **[!UICONTROL Next]** para continuar con el paso **[!UICONTROL Authentication]**.

![Credenciales confirmadas](../../assets/catalog/advertising/google-customer-match/connection-success.png)

En el paso **[!UICONTROL Autenticación]**, introduzca un **[!UICONTROL Nombre]** y una **[!UICONTROL Descripción]** para el flujo de activación y rellene el **[!UICONTROL ID de cuenta]** de Google.

En este paso, también puede seleccionar cualquier **[!UICONTROL acción de marketing]** que deba aplicarse a este destino. Las acciones de marketing indican la intención para la que se exportarán los datos al destino. Puede seleccionar entre las acciones de marketing definidas por Adobe o crear su propia acción de marketing. Para obtener más información sobre las acciones de marketing, consulte [Información general sobre las políticas de uso de datos](../../../data-governance/policies/overview.md).

Seleccione **[!UICONTROL Crear destino]** después de rellenar los campos anteriores.

>[!IMPORTANT]
>
> * La acción de marketing **[!UICONTROL Combinar con PII]** está seleccionada de forma predeterminada para el destino [!DNL Google Customer Match] y no se puede eliminar.
> * Para destinos [!DNL Google Customer Match]. **[!UICONTROL El]** ID de cuenta es su ID de cliente de con Google. El formato del ID es xxx-xxx-xxxx.


![Conectar Google Customer Match: paso de autenticación](../../assets/catalog/advertising/google-customer-match/authentication.png)

Se ha creado el destino. Puede seleccionar **[!UICONTROL Guardar y salir]** si desea activar los segmentos más adelante o puede seleccionar **[!UICONTROL Siguiente]** para continuar con el flujo de trabajo y seleccionar los segmentos que desea activar. En cualquier caso, consulte la siguiente sección, [Activar segmentos en [!DNL Google Customer Match]](#activate-segments), para el resto del flujo de trabajo.

## Activar segmentos en [!DNL Google Customer Match] {#activate-segments}

Para obtener instrucciones sobre cómo activar segmentos en [!DNL Google Customer Match], consulte [Activar datos en destinos](../../ui/activate-destinations.md).


En el paso **[!UICONTROL Programación de segmentos]**, debe proporcionar el [!UICONTROL ID de aplicación] al enviar segmentos [!DNL IDFA] o [!DNL GAID] a [!DNL Google Customer Match].

![ID de aplicación de coincidencia de clientes de Google](../../assets/catalog/advertising/google-customer-match/gcm-destination-appid.png)

Para obtener más información sobre cómo encontrar el [!DNL App ID], consulte la [documentación oficial de Google](https://developers.google.com/adwords/api/docs/reference/v201809/AdwordsUserListService.CrmBasedUserList#appid).







<!-- 
To activate segments to [!DNL Google Customer Match], follow the steps below: 

In **[!UICONTROL Destinations > Browse]**, select the [!DNL Google Customer Match] destination where you want to activate your segments.

Click the name of the destination. This takes you to the Activate flow.

![activate-flow](../../assets/catalog/advertising/google-customer-match/activate-flow.png)

Note that if an activation flow already exists for a destination, you can see the segments that are currently being sent to the destination. Select **[!UICONTROL Edit activation]** in the right rail and follow the steps below to modify the activation details.

Select **[!UICONTROL Activate]**. In the **[!UICONTROL Activate destination]** workflow, on the **[!UICONTROL Select Segments]** page, select which segments to send to [!DNL Google Customer Match].

![segments-to-destination](../../assets/catalog/advertising/google-customer-match/activate-segments.png)

In the **[!UICONTROL Identity mapping]** step, select which attributes to be included as an identity in this destination. Select **[!UICONTROL Add new mapping]** and browse your schema, select email and/or hashed email, and map them to the corresponding target identity.

![identity mapping initial screen](../../assets/catalog/advertising/google-customer-match/identity-mapping.png) 

**Plain text email address as primary identity**: If you have plain text (unhashed) email addresses as primary identity in your schema, select the email field in your **[!UICONTROL Source Attributes]** and map to the Email field in the right column under **[!UICONTROL Target Identities]**, as shown below:

![select plain text emails identity](../../assets/catalog/advertising/google-customer-match/raw-email.gif) 

**Hashed email address as primary identity**: If you have hashed email addresses as primary identity in your schema, select the hashed email field in your **[!UICONTROL Source Attributes]** and map to the Email_LC_SHA256 field in the right column under **[!UICONTROL Target Identities]**, as shown below:

![select hashed emails identity](../../assets/catalog/advertising/google-customer-match/hashed-emails.gif)

On the **[!UICONTROL Segment schedule]** page, you can set the start date for sending data to the destination.

On the **[!UICONTROL Review]** page, you can see a summary of your selection. Select **[!UICONTROL Cancel]** to break up the flow, **[!UICONTROL Back]** to modify your settings, or **[!UICONTROL Finish]** to confirm your selection and start sending data to the destination.

>[!IMPORTANT]
>
>In this step, Real-time CDP checks for data usage policy violations. Shown below is an example where a policy is violated. You cannot complete the segment activation workflow until you have resolved the violation. For information on how to resolve policy violations, see [Policy enforcement](../../../rtcdp/privacy/data-governance-overview.md#enforcement) in the data governance documentation section.
 
![confirm-selection](../../assets/common/data-policy-violation.png)

If no policy violations have been detected, select **[!UICONTROL Finish]** to confirm your selection and start sending data to the destination.

![confirm-selection](../../assets/catalog/advertising/google-customer-match/review.png) -->

## Verifique que la activación del segmento se haya realizado correctamente {#verify-activation}

Después de completar el flujo de activación, cambie a su cuenta de **[!UICONTROL Google Ads]**. Los segmentos activados ahora aparecerán en su cuenta de Google como listas de clientes. Tenga en cuenta que, según el tamaño del segmento, algunas audiencias no se rellenarán a menos que haya más de 100 usuarios activos a los que atender.

Al asignar un segmento a [!DNL IDFA] e [!DNL GAID] ID móviles, [!DNL Google Customer Match] crea un segmento independiente para cada asignación de ID. Su cuenta [!DNL Google Ads] mostrará dos segmentos diferentes, uno para [!DNL IDFA] y otro para la asignación [!DNL GAID].

## Recursos adicionales {#additional-resources}

* [Integración de la coincidencia de clientes de Google: tutorial en vídeo](https://experienceleague.adobe.com/docs/platform-learn/tutorials/rtcdp/integrate-with-google-customer-match.html)