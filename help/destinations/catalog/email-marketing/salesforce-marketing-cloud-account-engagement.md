---
title: Compromiso de cuenta de Marketing Cloud de Salesforce
description: Aprenda a utilizar el destino Compromiso de cuenta de Marketing Cloud de Salesforce (anteriormente conocido como Pardot) para exportar los datos de la cuenta y activarlos en Compromiso de cuenta de Marketing Cloud de Salesforce para sus necesidades comerciales.
last-substantial-update: 2023-04-14T00:00:00Z
exl-id: fca9d4f4-8717-4bfa-9992-5164ba98bea4
source-git-commit: e300e57df998836a8c388511b446e90499185705
workflow-type: tm+mt
source-wordcount: '1620'
ht-degree: 1%

---

# [!DNL Salesforce Marketing Cloud Account Engagement] conexión

Utilice el [[!DNL Salesforce Marketing Cloud Account Engagement]](https://www.salesforce.com/products/marketing-cloud/marketing-automation/) *(anteriormente conocido como [!DNL Pardot])* destino para capturar, rastrear, puntuar y calificar posibles clientes. También puede diseñar pistas de posibles clientes para todas las etapas de la canalización para audiencias de mercado objetivo y grupos de clientes a través de campañas de correo electrónico por goteo y administración de posibles clientes con nutrición, puntuación y segmentación de campañas.

Comparado con [!DNL Salesforce Marketing Cloud Engagement] que está más orientado hacia **B2C** marketing, [!DNL Marketing Cloud Account Engagement] es ideal para **B2B** casos de uso que implican varios departamentos y responsables de la toma de decisiones y que requieren ciclos de ventas y decisión más largos. Además, también mantiene una mayor proximidad e integración con su CRM para tomar las decisiones de ventas y marketing adecuadas. *Tenga en cuenta que Experience Platform también tiene conexiones para [!DNL Salesforce Marketing Cloud Engagement], puede comprobarlos en el [[!DNL Salesforce Marketing Cloud]](/help/destinations/catalog/email-marketing/salesforce-marketing-cloud.md) y [[!DNL (API) Salesforce Marketing Cloud]](/help/destinations/catalog/email-marketing/salesforce-marketing-cloud-exact-target.md) páginas.*

Esta [!DNL Adobe Experience Platform] [destino](/help/destinations/home.md) aprovecha el [[!DNL Salesforce Account Engagement API > Prospect Upsert by Email]](https://developer.salesforce.com/docs/marketing/pardot/guide/prospect-v5.html#prospect-upsert-by-email) extremo, a **añadir o actualizar los posibles clientes** después de activarlos en un nuevo [!DNL Marketing Cloud Account Engagement] segmento.

[!DNL Marketing Cloud Account Engagement] utiliza el protocolo OAuth 2 con código de autorización para autenticarse en [!DNL Account Engagement] API. Instrucciones para autenticarse en su [!DNL Marketing Cloud Account Engagement] más abajo, en la sección [Autenticar en el destino](#authenticate) sección.

## Casos de uso {#use-cases}

Para ayudarle a comprender mejor cómo y cuándo debe utilizar el [!DNL Marketing Cloud Account Engagement] Destino, este es un ejemplo de caso de uso que los clientes de Adobe Experience Platform pueden solucionar mediante este destino.

### Envío de correos electrónicos a contactos para campañas de marketing {#use-case-send-emails}

El departamento de marketing de una plataforma en línea desea difundir una campaña de marketing basada en correo electrónico a una audiencia seleccionada de posibles clientes B2B. El equipo de marketing de la plataforma puede agregar nuevos posibles clientes o actualizar la información de posibles clientes existente a través de Adobe Experience Platform, crear audiencias a partir de sus propios datos sin conexión y enviar estas audiencias a [!DNL Marketing Cloud Account Engagement], que se puede utilizar para enviar el correo electrónico de la campaña de marketing.

## Requisitos previos {#prerequisites}

Consulte las secciones siguientes para conocer todos los requisitos previos que debe configurar en Experience Platform y [!DNL Salesforce] y para obtener la información que necesita recopilar antes de trabajar con [!DNL Marketing Cloud Account Engagement] destino.

### Requisitos previos en Experience Platform {#prerequisites-in-experience-platform}

Antes de activar los datos en [!DNL Marketing Cloud Account Engagement] destino, debe tener un [esquema](/help/xdm/schema/composition.md), a [conjunto de datos](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=es), y [segmentos](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html) creado en [!DNL Experience Platform].

### Requisitos previos en [!DNL Marketing Cloud Account Engagement] {#prerequisites-destination}

Tenga en cuenta los siguientes requisitos previos para exportar datos de Platform a su [!DNL Marketing Cloud Account Engagement] cuenta:

#### Necesita tener un [!DNL Marketing Cloud Account Engagement] account {#prerequisites-account}

A [!DNL Marketing Cloud Account Engagement] cuenta con una suscripción a [Compromiso de cuenta Marketing Cloud](https://www.salesforce.com/products/marketing-cloud/marketing-automation/) el producto es obligatorio para continuar.

Su [!DNL Salesforce] La cuenta debe tener el [!DNL Salesforce] `Account Engagement Administrator role`. Esto es necesario para [crear campos de cliente prospecto personalizados](https://help.salesforce.com/s/articleView?id=sf.pardot_fields_create_custom_field.htm&amp;type=5).

Por último, su cuenta también debe poder acceder a [[!DNL Account Engagement Lightning App]](https://help.salesforce.com/s/articleView?id=sf.pardot_lightning_enable.htm&amp;type=5).

Póngase en contacto con [[!DNL Salesforce] Asistencia](https://www.salesforce.com/company/contact-us/?d=cta-glob-footer-10) o su [!DNL Salesforce] administrador de cuentas si no tiene una cuenta de o le falta el [!DNL Marketing Cloud Account Engagement] suscripción para la [!DNL Account Engagement Administrator role].

#### Reunir [!DNL Marketing Cloud Account Engagement] credenciales {#gather-credentials}

Tenga en cuenta los elementos siguientes antes de autenticarse en el [!DNL Marketing Cloud Account Engagement] destino.

| Credencial | Descripción |
| --- | --- |
| `Username` | Su [!DNL Marketing Cloud Account Engagement] nombre de usuario de cuenta. |
| `Password` | Su [!DNL Marketing Cloud Account Engagement] contraseña de la cuenta. |
| `Account Engagement Business Unit ID` | Para encontrar el ID de unidad de negocio de participación de cuenta, utilice Configuración en [!DNL Salesforce]. En Configuración, introduzca *Configuración de unidad de negocio* en el cuadro Búsqueda rápida. El ID de unidad de negocio de participación de cuenta comienza con `0Uv` y tiene 18 caracteres de longitud. Si no puede acceder a la información de configuración de la unidad de negocio, pregunte a su [!DNL Salesforce] Administrador de cuentas para proporcionarle el `Account Engagement Business Unit ID`. Si necesita más información, consulte la [[!DNL Salesforce] Autenticación](https://developer.salesforce.com/docs/marketing/pardot/guide/authentication) página de directrices. |

{style="table-layout:auto"}

### Mecanismos de protección {#guardrails}

Consulte la [!DNL Marketing Cloud Account Engagement] [límites de velocidad](https://developer.salesforce.com/docs/marketing/pardot/guide/overview.html#rate-limits) que detalla los límites impuestos por su plan y que también se aplicarían a las ejecuciones Experience Platform.

>[!IMPORTANT]
>
>Si su [!DNL Salesforce] El administrador de la cuenta ha restringido el acceso a rangos de IP de confianza. Debe ponerse en contacto con ellos para obtener [IP del Experience Platform](/help/destinations/catalog/streaming/ip-address-allow-list.md) incluido en la lista de permitidos. Consulte la [!DNL Salesforce] [Restringir el acceso a intervalos de IP fiables para una aplicación conectada](https://help.salesforce.com/s/articleView?id=sf.connected_app_edit_ip_ranges.htm&amp;type=5) documentación de si necesita instrucciones adicionales.

## Identidades admitidas {#supported-identities}

[!DNL Marketing Cloud Account Engagement] admite la activación de identidades descritas en la tabla siguiente. Más información sobre [identidades](/help/identity-service/namespaces.md).

| Identidad de destino | Descripción | Consideraciones |
|---|---|---|
| Correo electrónico | Dirección de correo electrónico del cliente potencial | Obligatorio |

{style="table-layout:auto"}

## Tipo y frecuencia de exportación {#export-type-frequency}

Consulte la tabla siguiente para obtener información sobre el tipo y la frecuencia de exportación de destino.

| Elemento | Tipo | Notas |
---------|----------|---------|
| Tipo de exportación | **[!UICONTROL Basado en perfiles]** | <ul><li>Está exportando todos los miembros de un segmento, junto con los campos de esquema deseados *(por ejemplo: dirección de correo electrónico, número de teléfono, apellidos)*, según la asignación de campo.</li><li> Para cada audiencia seleccionada en Platform, la correspondiente [!DNL Salesforce Marketing Cloud Account Engagement] El estado del segmento se actualiza con su estado de audiencia de Platform.</li></ul> |
| Frecuencia de exportación | **[!UICONTROL Transmisión]** | Los destinos de streaming son conexiones basadas en API &quot;siempre activadas&quot;. Tan pronto como se actualiza un perfil en Experience Platform según la evaluación de audiencias, el conector envía la actualización de forma descendente a la plataforma de destino. Más información sobre [destinos de streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Conectar con el destino {#connect}

>[!IMPORTANT]
>
>Para conectarse al destino, necesita el **[!UICONTROL Administrar destinos]** [permiso de control de acceso](/help/access-control/home.md#permissions). Lea el [información general de control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Para conectarse a este destino, siga los pasos descritos en la sección [tutorial de configuración de destino](../../ui/connect-destination.md). En el flujo de trabajo de configuración de destino, rellene los campos enumerados en las dos secciones siguientes.

En **[!UICONTROL Destinos]** > **[!UICONTROL Catálogo]**, buscar [!DNL Salesforce Marketing Cloud Account Engagement]. También puede encontrarlo en la sección **[!UICONTROL Marketing por email]** categoría.

### Autenticar en el destino {#authenticate}

Para autenticarse en el destino, seleccione **[!UICONTROL Conectar con destino]**. Se le dirigirá a la [!DNL Salesforce] página de inicio de sesión. Introduzca su [!DNL Marketing Cloud Account Engagement] credenciales de cuenta y seleccione [!DNL Log In].

![Captura de pantalla de la IU de Platform que muestra cómo autenticarse en la participación de la cuenta de Marketing Cloud.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-account-engagement/authenticate-destination.png)

A Continuación, Seleccione [!UICONTROL Permitir] en la ventana siguiente para conceder permisos al **Adobe Experience Platform** para acceder a su [!DNL Salesforce Marketing Cloud Account Engagement] cuenta. *Solo tendrá que hacer esto una vez*.

![Captura de pantalla emergente de confirmación de aplicación de Salesforce para dar permisos a la aplicación de Experience Platform para acceder a Participación de cuenta de Marketing Cloud.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-account-engagement/allow-app.png)

Si los detalles proporcionados son válidos, la interfaz de usuario muestra un mensaje: *Se ha conectado correctamente a la cuenta de participación de la cuenta de Marketing Cloud de Salesforce* message y una **[!UICONTROL Conectado]** estado con una marca de verificación verde, puede continuar con el siguiente paso.

### Rellenar detalles de destino {#destination-details}

Para configurar los detalles del destino, rellene los campos obligatorios y opcionales a continuación. Un asterisco junto a un campo en la interfaz de usuario indica que el campo es obligatorio. Consulte la [Reunir [!DNL Marketing Cloud Account Engagement] credenciales](#gather-credentials) para obtener cualquier guía.

![Captura de pantalla de la IU de Platform que muestra los detalles del destino.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-account-engagement/destination-details.png)

| Campo | Descripción |
| --- | --- |
| **[!UICONTROL Nombre]** | Un nombre con el que reconocerá este destino en el futuro. |
| **[!UICONTROL Descripción]** | Una descripción que le ayudará a identificar este destino en el futuro. |
| **[!UICONTROL ID de unidad de negocio de participación de cuenta]** | Su [!DNL Salesforce] `Account Engagement Business Unit ID`. |

{style="table-layout:auto"}

### Habilitar alertas {#enable-alerts}

Puede activar alertas para recibir notificaciones sobre el estado del flujo de datos a su destino. Seleccione una alerta de la lista a la que suscribirse para recibir notificaciones sobre el estado del flujo de datos. Para obtener más información sobre las alertas, consulte la guía de [suscripción a alertas de destinos mediante la IU](../../ui/alerts.md).

Cuando haya terminado de proporcionar detalles para la conexión de destino, seleccione **[!UICONTROL Siguiente]**.

## Activar audiencias en este destino {#activate}

>[!IMPORTANT]
> 
>* Para activar los datos, necesita el **[!UICONTROL Administrar destinos]**, **[!UICONTROL Activar destinos]**, **[!UICONTROL Ver perfiles]**, y **[!UICONTROL Ver segmentos]** [permisos de control de acceso](/help/access-control/home.md#permissions). Lea el [información general de control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.
>* Para exportar *identidades*, necesita el **[!UICONTROL Ver gráfico de identidad]** [permiso de control de acceso](/help/access-control/home.md#permissions). <br> ![Seleccione el área de nombres de identidad resaltada en el flujo de trabajo para activar audiencias en los destinos.](/help/destinations/assets/overview/export-identities-to-destination.png "Seleccione el área de nombres de identidad resaltada en el flujo de trabajo para activar audiencias en los destinos."){width="100" zoomable="yes"}

Leer [Activación de perfiles y audiencias en destinos de exportación de audiencia de streaming](/help/destinations/ui/activate-segment-streaming-destinations.md) para obtener instrucciones sobre cómo activar audiencias en este destino.

### Consideraciones sobre asignación y ejemplo {#mapping-considerations-example}

Para enviar correctamente los datos de audiencia de Adobe Experience Platform a [!DNL Marketing Cloud Account Engagement] destino, debe ir a través del paso de asignación de campos. La asignación consiste en crear un vínculo entre los campos de esquema del Modelo de datos de experiencia (XDM) en la cuenta de Platform y sus equivalentes correspondientes desde el destino de destino.

Para asignar correctamente los campos XDM a [!DNL Marketing Cloud Account Engagement] campos de destino, siga los pasos a continuación.

1. En el **[!UICONTROL Asignación]** paso, seleccione **[!UICONTROL Añadir nueva asignación]**. Verá una nueva fila de asignación en la pantalla.
1. En el **[!UICONTROL Seleccionar campo de origen]** , seleccione la **[!UICONTROL Seleccionar atributos]** y seleccione el atributo XDM o elija el **[!UICONTROL Seleccionar área de nombres de identidad]** y seleccione una identidad.
1. En el **[!UICONTROL Seleccionar campo de destino]** , seleccione la **[!UICONTROL Seleccionar área de nombres de identidad]** y seleccione una identidad o elija **[!UICONTROL Seleccionar atributos personalizados]** y especifique en la lista de [[!DNL Prospect API fields]](https://developer.salesforce.com/docs/marketing/pardot/guide/prospect-v5.html#fields) del esquema disponible.

   * Repita estos pasos para agregar cualquier asignación entre el esquema de perfil XDM y [!DNL Marketing Cloud Account Engagement]: | Campo de origen | Campo de destino | Obligatorio | | — | — | — | |`IdentityMap: Email`|`Identity: email`| Sí | |`xdm: MailingAddress.city`|`xdm: city`| | |`xdm: person.name.firstName`|`Attribute: firstName`| |

   * A continuación, se muestra un ejemplo con las asignaciones anteriores:
     ![Captura de pantalla de la IU de Platform que muestra asignaciones de Target.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-account-engagement/mappings.png)

Cuando haya terminado de proporcionar las asignaciones para la conexión de destino, seleccione **[!UICONTROL Siguiente]**.

## Validar exportación de datos {#exported-data}

Para comprobar que ha configurado correctamente el destino, siga los pasos a continuación:

1. Vaya a una de las audiencias que haya seleccionado. Seleccione la pestaña **[!DNL Activation data]** El **[!UICONTROL ID de asignación]** muestra el nombre del campo personalizado que se genera dentro de la columna [!DNL Marketing Cloud Account Engagement Prospects] página.
   ![Captura de pantalla de la IU de Platform que muestra el ID de asignación de un segmento seleccionado.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-account-engagement/selected-segment-mapping-id.png)

1. Inicie sesión en [[!DNL Salesforce]](https://login.salesforce.com/) sitio web. A continuación, vaya a **[!DNL Account Engagement]** > **[!DNL Prospects]** > **[!DNL Pardot Prospects]** y compruebe si se han añadido o actualizado los posibles clientes de la audiencia. También puede acceder a [[!DNL Salesforce Pardot]](https://pi.pardot.com/) y acceder a **[!DNL Prospects]** página.
   ![Captura de pantalla de la IU de Salesforce que muestra la página de clientes potenciales.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-account-engagement/prospects.png)

1. Para comprobar si se han actualizado los clientes potenciales, seleccione un cliente y verifique si el campo de cliente potencial personalizado se ha actualizado con el estado de audiencia del Experience Platform.
   ![Captura de pantalla de la interfaz de usuario de Salesforce que muestra la página de cliente potencial seleccionada, el campo de cliente potencial personalizado se actualiza con el estado de audiencia.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-account-engagement/prospect.png)

## Uso de datos y gobernanza {#data-usage-governance}

Todo [!DNL Adobe Experience Platform] Los destinos de cumplen con las políticas de uso de datos al gestionar los datos. Para obtener información detallada sobre cómo [!DNL Adobe Experience Platform] aplica la gobernanza de datos. Consulte la [Resumen de gobernanza de datos](/help/data-governance/home.md).

## Recursos adicionales {#additional-resources}

* [!DNL Marketing Cloud Account Engagement] [Documentación de API](https://developer.salesforce.com/docs/marketing/pardot/guide/overview.html).
