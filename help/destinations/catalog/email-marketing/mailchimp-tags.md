---
title: Etiquetas de Mailchimp
description: El destino de Etiquetas de Mailchimp te permite exportar los datos de tu cuenta y activarlos dentro de Mailchimp para interactuar con tus contactos.
source-git-commit: b32d619b78502e38e98a410bd14379992543c63c
workflow-type: tm+mt
source-wordcount: '1646'
ht-degree: 2%

---

# [!DNL Mailchimp Tags] conexión

[[!DNL Mailchimp]](https://mailchimp.com) *(también conocido como [!DNL Intuit Mailchimp])* es una popular plataforma de automatización de marketing y servicio de marketing por correo electrónico que utilizan las empresas para administrar y hablar con los contactos *(clientes, clientes u otras partes interesadas)* uso de listas de correo y campañas de marketing por correo electrónico.

[!DNL Mailchimp Tags] utiliza [audiencias](https://mailchimp.com/help/getting-started-audience/) y [etiquetas](https://mailchimp.com/help/getting-started-tags/) para administrar su información de contacto. Las etiquetas son etiquetas que permiten organizar los contactos y etiquetarlos para la categorización interna en [!DNL Mailchimp].

Comparado con [!DNL Mailchimp Interest Categories] que utilizaría para ordenar sus contactos según sus intereses y preferencias, [!DNL Mailchimp Tags] está diseñado para administrar suscripciones a temas de interés que puedan interesar a sus contactos. *Tenga en cuenta que Experience Platform también tiene una conexión para [!DNL Mailchimp Interest Categories], puede comprobarlo en la página [[!DNL Mailchimp Interest Categories]](/help/destinations/catalog/email-marketing/mailchimp-interest-categories.md) página.*

Esta [!DNL Adobe Experience Platform] [destino](/help/destinations/home.md) aprovecha el [[!DNL Mailchimp batch subscribe or unsubscribe API]](https://mailchimp.com/developer/marketing/api/lists/batch-subscribe-or-unsubscribe/) punto final. Puede **añadir nuevos contactos** o **actualizar etiquetas de [!DNL Mailchimp] contactos** dentro de un existente [!DNL Mailchimp] después de activarlos en una nueva audiencia. [!DNL Mailchimp Tags] utiliza los nombres de audiencia seleccionados de Platform como nombres de etiqueta dentro de [!DNL Mailchimp].

## Casos de uso {#use-cases}

Para ayudarle a comprender mejor cómo y cuándo debe utilizar el [!DNL Mailchimp Tags] Destino, este es un ejemplo de caso de uso que los clientes de Adobe Experience Platform pueden solucionar mediante este destino.

### Envío de correos electrónicos a contactos para campañas de marketing {#use-case-send-emails}

El departamento de ventas de una organización desea difundir una campaña de marketing basada en correo electrónico a una lista revisada de contactos. Las listas de contactos se reciben por lotes desde diferentes fuentes sin conexión y, por lo tanto, deben rastrearse. El equipo identifica un existente [!DNL Mailchimp] y comienza a crear las audiencias de Experience Platform a las que se añaden los contactos de cada lista. Después de enviar estas audiencias a [!DNL Mailchimp Tags], si hay contactos que no existen en el seleccionado [!DNL Mailchimp] a la audiencia, se les agrega una etiqueta asociada que incluye el nombre de la audiencia a la que pertenece el contacto. Si ya existe algún contacto en [!DNL Mailchimp] audiencia se añade una nueva etiqueta con el nombre de la audiencia. Como las etiquetas son visibles en [!DNL Mailchimp] las fuentes sin conexión se pueden identificar fácilmente. Una vez que los datos se hayan enviado a [!DNL Mailchimp] envían el correo electrónico de la campaña de marketing a la audiencia.

## Requisitos previos {#prerequisites}

Consulte las secciones siguientes para conocer todos los requisitos previos que debe configurar en Experience Platform y [!DNL Mailchimp] y para obtener la información que necesita recopilar antes de trabajar con [!DNL Mailchimp Tags] destino.

### Requisitos previos en Experience Platform {#prerequisites-in-experience-platform}

Antes de activar los datos en [!DNL Mailchimp Tags] destino, debe tener un [esquema](/help/xdm/schema/composition.md), a [conjunto de datos](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=en), y [audiencias](https://experienceleague.adobe.com/docs/platform-learn/tutorials/audiences/create-audiences.html) creado en [!DNL Experience Platform].

### Requisitos previos para la [!DNL Mailchimp Tags] destino {#prerequisites-destination}

Tenga en cuenta los siguientes requisitos previos para exportar datos de Platform a su [!DNL Mailchimp Tags] cuenta:

#### Necesita tener un [!DNL Mailchimp] account {#prerequisites-account}

Antes de crear un [!DNL Mailchimp Tags] destino, primero debe asegurarse de que dispone de un [!DNL Mailchimp] cuenta. Si todavía no dispone de una, visite la [[!DNL Mailchimp] página de suscripción](https://login.mailchimp.com/signup/) para registrarse y crear su cuenta.

#### Reunir [!DNL Mailchimp] Clave de API {#gather-credentials}

Necesita su [!DNL Mailchimp] **Clave de API** para autenticar el [!DNL Mailchimp Interest Categories] destino frente a su [!DNL Mailchimp] cuenta. El **Clave de API** sirve como **Contraseña** cuando usted [autenticar el destino](#authenticate).

Si no tiene su **Clave de API**, inicie sesión en su [!DNL Mailchimp] y consulte la [!DNL Mailchimp] documentación sobre [Cómo generar la clave de API](https://mailchimp.com/developer/marketing/guides/quick-start/#generate-your-api-key).

Un ejemplo de clave de API es `0123456789abcdef0123456789abcde-us14`.

>[!IMPORTANT]
>
>Si genera el **Clave de API**, anótelo, ya que no podrá acceder a él después de la generación.

#### Identifique su [!DNL Mailchimp] centro de datos {#identify-data-center}

A continuación, debe identificar su [!DNL Mailchimp] centro de datos. Para ello, inicie sesión en su [!DNL Mailchimp] y vaya a la **sección de claves API** de su cuenta.

El ID del centro de datos es la primera sección de la dirección URL que ve en el explorador. Si la dirección URL es *https://`us14`.mailchimp.com/account/api/*, el centro de datos es `us14`.

El ID del centro de datos también se adjunta a la clave de API en el formulario *key-dc*; Por ejemplo, si la clave de API es `0123456789abcdef0123456789abcde-us14`, el centro de datos es `us14`.

Anote el valor del centro de datos *(`us14` en este ejemplo)*. Necesitará este valor cuando [rellene los detalles de destino](#destination-details).

Si necesita más información, consulte la [[!DNL Mailchimp] Documentación de fundamentos](https://mailchimp.com/developer/marketing/docs/fundamentals/#api-structure).

### Mecanismos de protección {#guardrails}

Consulte la [!DNL Mailchimp] [límites de velocidad](https://mailchimp.com/developer/marketing/docs/fundamentals/#api-limits) para obtener información detallada sobre los límites impuestos por la [!DNL Mailchimp] API.

## Identidades admitidas {#supported-identities}

[!DNL Mailchimp] admite la activación de identidades descritas en la tabla siguiente. Más información sobre [identidades](/help/identity-service/features/namespaces.md).

| Identidad de destino | Descripción | Consideraciones |
|---|---|---|
| Correo electrónico | La dirección de correo electrónico del contacto. | Obligatorio |

{style="table-layout:auto"}

## Audiencias compatibles {#supported-audiences}

Esta sección describe qué tipo de audiencias puede exportar a este destino.

| Origen de audiencia | Admitido | Descripción |
---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Audiencias generadas mediante el Experience Platform [Servicio de segmentación](../../../segmentation/home.md). |
| Cargas personalizadas | ✓ | Audiencias [importado](../../../segmentation/ui/overview.md#import-audience) en el Experience Platform desde archivos CSV. |

{style="table-layout:auto"}

## Tipo y frecuencia de exportación {#export-type-frequency}

Consulte la tabla siguiente para obtener información sobre el tipo y la frecuencia de exportación de destino.

| Elemento | Tipo | Notas |
---------|----------|---------|
| Tipo de exportación | **[!UICONTROL Basado en perfiles]** | <ul><li>Está exportando todos los miembros de una audiencia, junto con los campos de esquema deseados *(por ejemplo: dirección de correo electrónico, número de teléfono, apellidos)*, según la asignación de campo.</li><li> Para cada audiencia seleccionada en Platform, la correspondiente [!DNL Mailchimp Tags] El estado del segmento se actualiza con el estado de audiencia de Platform.</li></ul> |
| Frecuencia de exportación | **[!UICONTROL Transmisión]** | Los destinos de streaming son conexiones basadas en API &quot;siempre activadas&quot;. Tan pronto como se actualiza un perfil en Experience Platform según la evaluación de audiencias, el conector envía la actualización de forma descendente a la plataforma de destino. Más información sobre [destinos de streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Conexión al destino {#connect}

>[!IMPORTANT]
>
>Para conectarse al destino, necesita el **[!UICONTROL Administrar destinos]** [permiso de control de acceso](/help/access-control/home.md#permissions). Lea el [información general de control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Para conectarse a este destino, siga los pasos descritos en la sección [tutorial de configuración de destino](../../ui/connect-destination.md). En el flujo de trabajo de configuración de destino, rellene los campos enumerados en las dos secciones siguientes.

En **[!UICONTROL Destinos]** > **[!UICONTROL Catálogo]**, buscar [!DNL Mailchimp Tags]. También puede encontrarlo en la sección **[!UICONTROL Marketing por email]** categoría.

### Autenticarse en el destino {#authenticate}

Para autenticarse en el destino, rellene los campos obligatorios a continuación y seleccione **[!UICONTROL Conectar con destino]**.

| Campo | Descripción |
| --- | --- |
| **[!UICONTROL Nombre de usuario]** | Su [!DNL Mailchimp] nombre de usuario. |
| **[!UICONTROL Contraseña]** | Su [!DNL Mailchimp] **Clave de API**, que había anotado en el [Reunir [!DNL Mailchimp] credenciales](#gather-credentials) sección.<br> La clave de API adopta la forma de `{KEY}-{DC}`, donde la variable `{KEY}` hace referencia al valor anotado en la sección [[!DNL Mailchimp] Clave de API](#gather-credentials) y la sección `{DC}` La parte hace referencia a [[!DNL Mailchimp] centro de datos](#identify-data-center). <br>Puede proporcionar cualquiera de las `{KEY}` parte o todo el formulario.<br> Por ejemplo, si la clave de API es <br>*`0123456789abcdef0123456789abcde-us14`*,<br> puede proporcionar lo siguiente *`0123456789abcdef0123456789abcde`*o *`0123456789abcdef0123456789abcde-us14`*como el valor. |

{style="table-layout:auto"}

![Captura de pantalla de la IU de Platform que muestra cómo autenticarse.](../../assets/catalog/email-marketing/mailchimp-tags/authenticate-destination.png)

Si los detalles proporcionados son válidos, la interfaz de usuario muestra un **[!UICONTROL Conectado]** estado con una marca de verificación verde. A continuación, puede continuar con el paso siguiente.

### Rellenar detalles de destino {#destination-details}

Para configurar los detalles del destino, rellene los campos obligatorios y opcionales a continuación. Un asterisco junto a un campo en la interfaz de usuario indica que el campo es obligatorio.

![Captura de pantalla de la IU de Platform que muestra los detalles del destino.](../../assets/catalog/email-marketing/mailchimp-tags/destination-details.png)

| Campo | Descripción |
| --- | --- |
| **[!UICONTROL Nombre]** | Un nombre con el que reconocerá este destino en el futuro. |
| **[!UICONTROL Descripción]** | Una descripción que le ayudará a identificar este destino en el futuro. |
| **[!UICONTROL Centro de datos]** | Su [!DNL Mailchimp] account `data center`. Consulte la [Identificar [!DNL Mailchimp] centro de datos](#identify-data-center) para obtener cualquier guía. |
| **[!UICONTROL Nombre de audiencia (introduzca primero el centro de datos)]** | Después de introducir su **[!UICONTROL Centro de datos]**, esta lista desplegable se rellena automáticamente con los nombres de audiencia de su [!DNL Mailchimp] cuenta. Seleccione la audiencia que desee actualizar con los datos de Platform. |

{style="table-layout:auto"}

### Habilitar alertas {#enable-alerts}

Puede activar alertas para recibir notificaciones sobre el estado del flujo de datos a su destino. Seleccione una alerta de la lista a la que suscribirse para recibir notificaciones sobre el estado del flujo de datos. Para obtener más información sobre las alertas, consulte la guía de [suscripción a alertas de destinos mediante la IU](../../ui/alerts.md).

Cuando haya terminado de proporcionar detalles para la conexión de destino, seleccione **[!UICONTROL Siguiente]**.

## Activar públicos en este destino {#activate}

>[!IMPORTANT]
> 
>* Para activar los datos, necesita el **[!UICONTROL Ver destinos]**, **[!UICONTROL Activar destinos]**, **[!UICONTROL Ver perfiles]**, y **[!UICONTROL Ver segmentos]** [permisos de control de acceso](/help/access-control/home.md#permissions). Lea el [información general de control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.
>* Para exportar *identidades*, necesita el **[!UICONTROL Ver gráfico de identidad]** [permiso de control de acceso](/help/access-control/home.md#permissions). <br> ![Seleccione el área de nombres de identidad resaltada en el flujo de trabajo para activar audiencias en los destinos.](/help/destinations/assets/overview/export-identities-to-destination.png "Seleccione el área de nombres de identidad resaltada en el flujo de trabajo para activar audiencias en los destinos."){width="100" zoomable="yes"}

Leer [Activar audiencias en destinos de flujo continuo](/help/destinations/ui/activate-segment-streaming-destinations.md) para obtener instrucciones sobre cómo activar audiencias en este destino.

### Consideraciones sobre asignación y ejemplo {#mapping-considerations-example}

Para enviar correctamente los datos de audiencia de Adobe Experience Platform a [!DNL Mailchimp Tags] destino, debe ir a través del paso de asignación de campos. La asignación consiste en crear un vínculo entre los campos de esquema del Modelo de datos de experiencia (XDM) en la cuenta de Platform y sus equivalentes correspondientes desde el destino de destino.

Para asignar correctamente los campos XDM a [!DNL Mailchimp Tags] campos de destino, siga los pasos a continuación:

1. En el **[!UICONTROL Asignación]** paso, seleccione **[!UICONTROL Añadir nueva asignación]**. Verá una nueva fila de asignación en la pantalla.
1. En el **[!UICONTROL Seleccionar campo de origen]** ventana, elija **[!UICONTROL Seleccionar área de nombres de identidad]** y seleccione la `Email` área de nombres de identidad.

   ![Captura de pantalla de la IU de Platform con el campo Fuente como Correo electrónico desde el área de nombres de identidad.](../../assets/catalog/email-marketing/mailchimp-tags/source-field.png)

1. En el **[!UICONTROL Seleccionar campo de destino]** ventana, elija **[!UICONTROL Seleccionar área de nombres de identidad]** y seleccione la `Email` área de nombres de identidad.

   ![Captura de pantalla de la IU de Platform con el campo de Destino como Correo electrónico desde el área de nombres de identidad.](../../assets/catalog/email-marketing/mailchimp-tags/target-field.png)

   Las asignaciones entre el esquema de perfil XDM y [!DNL Mailchimp Tags] será el siguiente: | Campo de origen | Campo de destino | Obligatorio | | — | — | — | |`IdentityMap: Email`|`Identity: Email`| Sí |

   A continuación, se muestra un ejemplo con las asignaciones completadas:
   ![Ejemplo de captura de pantalla de la IU de Platform que muestra asignaciones de campos.](../../assets/catalog/email-marketing/mailchimp-tags/mappings.png)

Cuando haya terminado de proporcionar las asignaciones para la conexión de destino, seleccione **[!UICONTROL Siguiente]**.

## Validar exportación de datos {#exported-data}

Para comprobar que ha configurado correctamente el destino, siga los pasos a continuación:

1. Inicie sesión en su [[!DNL Mailchimp]](https://login.mailchimp.com/) cuenta. A continuación, vaya a **[!DNL Audience]** > **[!DNL All Contacts]** y compruebe si se han añadido los contactos de la audiencia y si los contactos de la audiencia se han actualizado con el nombre de la audiencia.
   ![Captura de pantalla de IU de Mailchimp que muestra la página Audience.](../../assets/catalog/email-marketing/mailchimp-tags/contacts.png)

## Uso de datos y gobernanza {#data-usage-governance}

Todo [!DNL Adobe Experience Platform] Los destinos de cumplen con las políticas de uso de datos al gestionar los datos. Para obtener información detallada sobre cómo [!DNL Adobe Experience Platform] aplica la gobernanza de datos. Consulte la [Resumen de gobernanza de datos](/help/data-governance/home.md).

## Errores y solución de problemas {#errors-and-troubleshooting}

Consulte la [[!DNL Mailchimp] página de errores](https://mailchimp.com/developer/marketing/docs/errors/) para obtener una lista completa de estados y códigos de error con explicaciones.

## Recursos adicionales {#additional-resources}

Información útil adicional del [!DNL Mailchimp] Esta documentación es:
* [Introducción a [!DNL Mailchimp]](https://mailchimp.com/help/getting-started-with-mailchimp/)
* [Introducción a Audiences](https://mailchimp.com/help/getting-started-audience/)
* [Crear una audiencia](https://mailchimp.com/help/create-audience/)
* [Introducción a las etiquetas](https://mailchimp.com/help/getting-started-tags/)
* [API de marketing](https://mailchimp.com/developer/marketing/api/)
