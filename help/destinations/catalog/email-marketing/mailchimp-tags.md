---
title: Etiquetas de Mailchimp
description: El destino de Etiquetas de Mailchimp te permite exportar los datos de tu cuenta y activarlos dentro de Mailchimp para interactuar con tus contactos.
last-substantial-update: 2024-02-20T00:00:00Z
exl-id: 0f278ca8-4fcf-4c47-b538-9cffa45a3d90
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1657'
ht-degree: 2%

---

# [!DNL Mailchimp Tags] conexión

[[!DNL Mailchimp]](https://mailchimp.com) *(también conocido como [!DNL Intuit Mailchimp])* es una popular plataforma de automatización de marketing y un servicio de marketing por correo electrónico que utilizan las empresas para administrar y hablar con los contactos *(clientes, clientes u otras partes interesadas)* mediante listas de correo y campañas de marketing por correo electrónico.

[!DNL Mailchimp Tags] usa [audiencias](https://mailchimp.com/help/getting-started-audience/) y [etiquetas](https://mailchimp.com/help/getting-started-tags/) para administrar tu información de contacto. Las etiquetas son etiquetas que permiten organizar los contactos y etiquetarlos para la categorización interna dentro de [!DNL Mailchimp].

En comparación con [!DNL Mailchimp Interest Categories], que utilizaría para ordenar los contactos según sus intereses y preferencias, [!DNL Mailchimp Tags] está pensado para administrar suscripciones a temas de interés que puedan interesar a sus contactos. *Tenga en cuenta que Experience Platform también tiene una conexión para [!DNL Mailchimp Interest Categories], puede desprotegerla en la página [[!DNL Mailchimp Interest Categories]](/help/destinations/catalog/email-marketing/mailchimp-interest-categories.md).*

Este [!DNL Adobe Experience Platform] [destino](/help/destinations/home.md) aprovecha el extremo [[!DNL Mailchimp batch subscribe or unsubscribe API]](https://mailchimp.com/developer/marketing/api/lists/batch-subscribe-or-unsubscribe/). Puede **agregar nuevos contactos** o **actualizar las etiquetas de [!DNL Mailchimp] contactos** existentes dentro de una audiencia [!DNL Mailchimp] existente después de activarlos dentro de una audiencia nueva. [!DNL Mailchimp Tags] usa los nombres de audiencia seleccionados de Experience Platform como nombres de etiqueta dentro de [!DNL Mailchimp].

## Casos de uso {#use-cases}

Para ayudarle a comprender mejor cómo y cuándo debe utilizar el destino [!DNL Mailchimp Tags], aquí tiene un ejemplo de uso que los clientes de Adobe Experience Platform pueden solucionar mediante este destino.

### Envío de correos electrónicos a contactos para campañas de marketing {#use-case-send-emails}

El departamento de ventas de una organización desea difundir una campaña de marketing basada en correo electrónico a una lista revisada de contactos. Las listas de contactos se reciben por lotes desde diferentes fuentes sin conexión y, por lo tanto, deben rastrearse. El equipo identifica una audiencia [!DNL Mailchimp] existente y comienza a crear las audiencias de Experience Platform a las que se agregan los contactos de cada lista. Después de enviar estas audiencias a [!DNL Mailchimp Tags], si algún contacto no existe en la audiencia [!DNL Mailchimp] seleccionada, se agrega con una etiqueta asociada que incluye el nombre de audiencia al que pertenece el contacto. Si ya existen contactos en la audiencia [!DNL Mailchimp], se agrega una nueva etiqueta con el nombre de la audiencia. Como las etiquetas son visibles en [!DNL Mailchimp], los orígenes sin conexión se pueden identificar fácilmente. Una vez que los datos se envían a [!DNL Mailchimp], envían el correo electrónico de la campaña de marketing a la audiencia.

## Requisitos previos {#prerequisites}

Consulte las secciones siguientes para conocer los requisitos previos que debe configurar en Experience Platform y [!DNL Mailchimp] y para obtener la información que necesita recopilar antes de trabajar con el destino [!DNL Mailchimp Tags].

### Requisitos previos en Experience Platform {#prerequisites-in-experience-platform}

Antes de activar datos en el destino [!DNL Mailchimp Tags], debe tener un [esquema](/help/xdm/schema/composition.md), un [conjunto de datos](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=es) y [audiencias](https://experienceleague.adobe.com/docs/platform-learn/tutorials/audiences/create-audiences.html?lang=es) creados en [!DNL Experience Platform].

### Requisitos previos para el destino [!DNL Mailchimp Tags] {#prerequisites-destination}

Tenga en cuenta los siguientes requisitos previos para exportar datos de Experience Platform a su cuenta de [!DNL Mailchimp Tags]:

#### Necesita tener una cuenta de [!DNL Mailchimp] {#prerequisites-account}

Para poder crear un destino de [!DNL Mailchimp Tags], primero debe asegurarse de que tiene una cuenta de [!DNL Mailchimp]. Si todavía no tiene una, visite la [[!DNL Mailchimp] página de suscripción](https://login.mailchimp.com/signup/) para registrarse y crear su cuenta.

#### Recopilar clave de API [!DNL Mailchimp] {#gather-credentials}

Necesita su [!DNL Mailchimp] **clave de API** para autenticar el destino [!DNL Mailchimp Interest Categories] con su cuenta de [!DNL Mailchimp]. La **clave API** sirve como **contraseña** al [autenticar el destino](#authenticate).

Si no tiene su **clave de API**, inicie sesión en su cuenta de [!DNL Mailchimp] y consulte la documentación de [!DNL Mailchimp] sobre [cómo generar su clave de API](https://mailchimp.com/developer/marketing/guides/quick-start/#generate-your-api-key).

Un ejemplo de clave de API es `0123456789abcdef0123456789abcde-us14`.

>[!IMPORTANT]
>
>Si genera la **clave API**, anótela, ya que no podrá obtener acceso a ella después de la generación.

#### Identificar su centro de datos [!DNL Mailchimp] {#identify-data-center}

A continuación, debe identificar su centro de datos [!DNL Mailchimp]. Para ello, inicia sesión en tu cuenta de [!DNL Mailchimp] y navega a la **sección de claves API** de tu cuenta.

El ID del centro de datos es la primera sección de la dirección URL que ve en el explorador. Si la dirección URL es *https://`us14`.mailchimp.com/account/api/*, el centro de datos es `us14`.

La ID del centro de datos también se anexa a la clave de API con el formato *key-dc*; por ejemplo, si la clave de API es `0123456789abcdef0123456789abcde-us14`, el centro de datos es `us14`.

Anote el valor del centro de datos *(`us14` en este ejemplo)*. Necesitará este valor cuando [rellene los detalles de destino](#destination-details).

Si necesita más orientación, consulte la [[!DNL Mailchimp] documentación de aspectos básicos](https://mailchimp.com/developer/marketing/docs/fundamentals/#api-structure).

### Mecanismos de protección {#guardrails}

Consulte [!DNL Mailchimp] [límites de tarifa](https://mailchimp.com/developer/marketing/docs/fundamentals/#api-limits) para obtener información detallada sobre los límites impuestos por la API [!DNL Mailchimp].

## Identidades admitidas {#supported-identities}

[!DNL Mailchimp] admite la activación de las identidades descritas en la tabla siguiente. Más información sobre [identidades](/help/identity-service/features/namespaces.md).

| Identidad de destino | Descripción | Consideraciones |
|---|---|---|
| Correo electrónico | La dirección de correo electrónico del contacto. | Obligatorio |

{style="table-layout:auto"}

## Audiencias compatibles {#supported-audiences}

Esta sección describe qué tipo de audiencias puede exportar a este destino.

| Origen de audiencia | Admitido | Descripción |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Audiencias generadas a través del [servicio de segmentación](../../../segmentation/home.md) de Experience Platform. |
| Cargas personalizadas | ✓ | Las audiencias [importadas](../../../segmentation/ui/audience-portal.md#import-audience) en Experience Platform desde archivos CSV. |

{style="table-layout:auto"}

## Tipo y frecuencia de exportación {#export-type-frequency}

Consulte la tabla siguiente para obtener información sobre el tipo y la frecuencia de exportación de destino.

| Elemento | Tipo | Notas |
---------|----------|---------|
| Tipo de exportación | **[!UICONTROL Basado en perfil]** | <ul><li>Va a exportar todos los miembros de una audiencia, junto con los campos de esquema deseados *(por ejemplo: dirección de correo electrónico, número de teléfono, apellidos)*, según la asignación de campos.</li><li> Para cada audiencia seleccionada en Experience Platform, el estado del segmento [!DNL Mailchimp Tags] correspondiente se actualiza con el estado de audiencia de Experience Platform.</li></ul> |
| Frecuencia de exportación | **[!UICONTROL Transmisión]** | Los destinos de streaming son conexiones basadas en API &quot;siempre activadas&quot;. Tan pronto como se actualiza un perfil en Experience Platform basado en la evaluación de audiencias, el conector envía la actualización de forma descendente a la plataforma de destino. Más información sobre [destinos de streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Conexión al destino {#connect}

>[!IMPORTANT]
>
>Para conectarse al destino, necesita el **[!UICONTROL permiso Administrar destinos]** [control de acceso](/help/access-control/home.md#permissions). Lea la [descripción general del control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Para conectarse a este destino, siga los pasos descritos en el [tutorial de configuración de destino](../../ui/connect-destination.md). En el flujo de trabajo de configuración de destino, rellene los campos enumerados en las dos secciones siguientes.

En **[!UICONTROL destinos]** > **[!UICONTROL catálogo]**, busque [!DNL Mailchimp Tags]. También puede ubicarlo en la categoría **[!UICONTROL Marketing por correo electrónico]**.

### Autenticarse en el destino {#authenticate}

Para autenticarte en el destino, rellena los campos obligatorios a continuación y selecciona **[!UICONTROL Conectarse al destino]**.

| Campo | Descripción |
| --- | --- |
| **[!UICONTROL Nombre de usuario]** | Su nombre de usuario [!DNL Mailchimp]. |
| **[!UICONTROL Contraseña]** | Su [!DNL Mailchimp] **clave de API**, que había anotado en la sección [Recopilar [!DNL Mailchimp] credenciales](#gather-credentials).<br> Su clave de API adopta la forma de `{KEY}-{DC}`, donde la parte `{KEY}` hace referencia al valor anotado en la sección [[!DNL Mailchimp] clave de API](#gather-credentials) y la parte `{DC}` hace referencia al [[!DNL Mailchimp] centro de datos](#identify-data-center). <br>Puede proporcionar la parte `{KEY}` o todo el formulario.<br> Por ejemplo, si su clave de API es <br>*`0123456789abcdef0123456789abcde-us14`*,<br>, puede proporcionar *`0123456789abcdef0123456789abcde`*o *`0123456789abcdef0123456789abcde-us14`*como valor. |

{style="table-layout:auto"}

![Captura de pantalla de la interfaz de usuario de Experience Platform que muestra cómo autenticarse.](../../assets/catalog/email-marketing/mailchimp-tags/authenticate-destination.png)

Si los detalles proporcionados son válidos, la interfaz de usuario mostrará el estado **[!UICONTROL Conectado]** con una marca de verificación verde. A continuación, puede continuar con el paso siguiente.

### Rellenar detalles de destino {#destination-details}

Para configurar los detalles del destino, rellene los campos obligatorios y opcionales a continuación. Un asterisco junto a un campo en la interfaz de usuario indica que el campo es obligatorio.

![Captura de pantalla de la interfaz de usuario de Experience Platform que muestra los detalles del destino.](../../assets/catalog/email-marketing/mailchimp-tags/destination-details.png)

| Campo | Descripción |
| --- | --- |
| **[!UICONTROL Nombre]** | Un nombre con el que reconocerá este destino en el futuro. |
| **[!UICONTROL Descripción]** | Una descripción que le ayudará a identificar este destino en el futuro. |
| **[!UICONTROL Centro de datos]** | Su cuenta [!DNL Mailchimp] `data center`. Consulte la sección [Identificar [!DNL Mailchimp] centro de datos](#identify-data-center) para obtener instrucciones. |
| **[!UICONTROL Nombre de audiencia (primero ingrese el centro de datos)]** | Una vez que ingrese su **[!UICONTROL Centro de datos]**, este menú desplegable se rellenará automáticamente con los nombres de audiencia de su cuenta de [!DNL Mailchimp]. Seleccione la audiencia que desea actualizar con los datos de Experience Platform. |

{style="table-layout:auto"}

### Habilitar alertas {#enable-alerts}

Puede activar alertas para recibir notificaciones sobre el estado del flujo de datos a su destino. Seleccione una alerta de la lista a la que suscribirse para recibir notificaciones sobre el estado del flujo de datos. Para obtener más información sobre las alertas, consulte la guía sobre [suscripción a alertas de destinos mediante la interfaz de usuario](../../ui/alerts.md).

Cuando termine de proporcionar detalles para la conexión de destino, seleccione **[!UICONTROL Siguiente]**.

## Activar públicos en este destino {#activate}

>[!IMPORTANT]
> 
>* Para activar los datos, necesita los **[!UICONTROL permisos de control de acceso]**, **[!UICONTROL Activar destinos]**, **[!UICONTROL Ver perfiles]** y **[!UICONTROL Ver segmentos]**&#x200B;[para ](/help/access-control/home.md#permissions). Lea la [descripción general del control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.
>* Para exportar *identidades*, necesita el **[[!UICONTROL permiso de control de acceso]](/help/access-control/home.md#permissions) de&rbrack;** Ver gráfico de identidad&lbrack;. <br> ![Seleccione el área de nombres de identidad resaltada en el flujo de trabajo para activar audiencias en los destinos.](/help/destinations/assets/overview/export-identities-to-destination.png "Seleccione el área de nombres de identidad resaltada en el flujo de trabajo para activar audiencias en los destinos."){width="100" zoomable="yes"}

Lea [Activar audiencias en destinos de flujo continuo](/help/destinations/ui/activate-segment-streaming-destinations.md) para obtener instrucciones sobre cómo activar audiencias en este destino.

### Consideraciones sobre asignación y ejemplo {#mapping-considerations-example}

Para enviar correctamente los datos de audiencia de Adobe Experience Platform al destino [!DNL Mailchimp Tags], debe pasar por el paso de asignación de campos. La asignación consiste en crear un vínculo entre los campos de esquema del Modelo de datos de experiencia (XDM) en la cuenta de Experience Platform y sus equivalentes correspondientes desde el destino de destino.

Para asignar correctamente los campos XDM a los campos de destino [!DNL Mailchimp Tags], siga los pasos a continuación:

1. En el paso **[!UICONTROL Asignación]**, seleccione **[!UICONTROL Agregar nueva asignación]**. Verá una nueva fila de asignación en la pantalla.
1. En la ventana **[!UICONTROL Seleccionar campo de origen]**, elija **[!UICONTROL Seleccionar área de nombres de identidad]** y seleccione el área de nombres de identidad `Email`.

   ![Captura de pantalla de la interfaz de usuario de Experience Platform con el campo Source como correo electrónico del área de nombres de identidad.](../../assets/catalog/email-marketing/mailchimp-tags/source-field.png)

1. En la ventana **[!UICONTROL Seleccionar campo de destino]**, elija **[!UICONTROL Seleccionar área de nombres de identidad]** y seleccione el área de nombres de identidad `Email`.

   ![Captura de pantalla de la interfaz de usuario de Experience Platform con el campo de destino como correo electrónico del área de nombres de identidad.](../../assets/catalog/email-marketing/mailchimp-tags/target-field.png)

   Las asignaciones entre su esquema de perfil XDM y [!DNL Mailchimp Tags] serán las siguientes:

   | Campo de origen | Campo de destino | Obligatorio |
   | --- | --- | --- |
   | `IdentityMap: Email` | `Identity: Email` | Sí |

   A continuación, se muestra un ejemplo con las asignaciones completadas:
   ![Ejemplo de captura de pantalla de IU de Experience Platform que muestra asignaciones de campos.](../../assets/catalog/email-marketing/mailchimp-tags/mappings.png)

Cuando haya terminado de proporcionar las asignaciones para la conexión de destino, seleccione **[!UICONTROL Siguiente]**.

## Validar exportación de datos {#exported-data}

Para comprobar que ha configurado correctamente el destino, siga los pasos a continuación:

1. Inicie sesión en su cuenta de [[!DNL Mailchimp]](https://login.mailchimp.com/). A continuación, vaya a la página **[!DNL Audience]** > **[!DNL All Contacts]** y compruebe si los contactos de la audiencia se han agregado y si los contactos de la audiencia se han actualizado con el nombre de la audiencia.
   ![Captura de pantalla de IU de Mailchimp que muestra la página Audiencia.](../../assets/catalog/email-marketing/mailchimp-tags/contacts.png)

## Uso de datos y gobernanza {#data-usage-governance}

Todos los destinos de [!DNL Adobe Experience Platform] cumplen con las políticas de uso de datos al administrar los datos. Para obtener información detallada sobre cómo [!DNL Adobe Experience Platform] aplica el control de datos, consulte la [Información general sobre el control de datos](/help/data-governance/home.md).

## Errores y solución de problemas {#errors-and-troubleshooting}

Consulte la [[!DNL Mailchimp] página de errores](https://mailchimp.com/developer/marketing/docs/errors/) para obtener una lista completa del estado y los códigos de error con explicaciones.

## Recursos adicionales {#additional-resources}

A continuación encontrará información útil adicional de la documentación de [!DNL Mailchimp]:
* [Introducción a [!DNL Mailchimp]](https://mailchimp.com/help/getting-started-with-mailchimp/)
* [Introducción a Audiences](https://mailchimp.com/help/getting-started-audience/)
* [Crear una audiencia](https://mailchimp.com/help/create-audience/)
* [Introducción a las etiquetas](https://mailchimp.com/help/getting-started-tags/)
* [API de marketing](https://mailchimp.com/developer/marketing/api/)
