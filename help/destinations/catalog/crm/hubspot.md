---
title: Conexión HubSpot
description: El destino de HubSpot le permite administrar los registros de contacto en su cuenta de HubSpot.
last-substantial-update: 2023-09-28T00:00:00Z
exl-id: e2114bde-b7c3-43da-9f3a-919322000ef4
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '1604'
ht-degree: 1%

---

# [!DNL HubSpot] conexión

[[!DNL HubSpot]](https://www.hubspot.com) es una plataforma CRM con todo el software, las integraciones y los recursos que necesita para conectar marketing, ventas, gestión de contenido y servicio al cliente. Permite conectar los datos, los equipos y los clientes en una plataforma CRM.

Esta [!DNL Adobe Experience Platform] [destino](/help/destinations/home.md) aprovecha el [[!DNL HubSpot] API de contactos](https://developers.hubspot.com/docs/api/crm/contacts), para actualizar contactos en [!DNL HubSpot] desde una audiencia de Experience Platform existente después de la activación.

Instrucciones para autenticarse en su [!DNL HubSpot] más abajo, en la sección [Autenticar en el destino](#authenticate) sección.

## Casos de uso {#use-cases}

Para ayudarle a comprender mejor cómo y cuándo debe utilizar el [!DNL HubSpot] Destino, este es un ejemplo de caso de uso que los clientes de Adobe Experience Platform pueden solucionar mediante este destino.

[!DNL HubSpot] los contactos almacenan información sobre las personas que interactúan con su negocio. Su equipo utiliza los contactos que existen en [!DNL HubSpot] para crear audiencias de Experience Platform. Después de enviar estas audiencias a [!DNL HubSpot]Sin embargo, su información se actualiza y a cada contacto se le asigna una propiedad con su valor como nombre de audiencia que indica a qué audiencia pertenece el contacto.

## Requisitos previos {#prerequisites}

Consulte las secciones siguientes para conocer todos los requisitos previos que debe configurar en Experience Platform y [!DNL HubSpot] y para la información que debe recopilar antes de trabajar con [!DNL HubSpot] destino.

### Requisitos previos del Experience Platform {#prerequisites-in-experience-platform}

Antes de activar los datos en [!DNL HubSpot] destino, debe tener un [esquema](/help/xdm/schema/composition.md), a [conjunto de datos](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=en), y [audiencias](https://experienceleague.adobe.com/docs/platform-learn/tutorials/audiences/create-audiences.html?lang=en) creado en [!DNL Experience Platform].

Consulte la documentación del Experience Platform para [Grupo de campos de esquema Detalles de pertenencia a audiencia](/help/xdm/field-groups/profile/segmentation.md) si necesita orientación sobre los estados de audiencia.

### Requisitos previos para la [!DNL HubSpot] destino {#prerequisites-destination}

Tenga en cuenta los siguientes requisitos previos para exportar datos de Platform a su [!DNL HubSpot] cuenta:

#### Debe tener un [!DNL HubSpot] account {#prerequisites-account}

Para exportar datos de Platform a su [!DNL Hubspot] cuenta necesita tener un [!DNL HubSpot] cuenta. Si todavía no tiene uno, visite la [Configurar tu cuenta de HubSpot](https://knowledge.hubspot.com/get-started/set-up-your-account) y siga las instrucciones para registrarse y crear su cuenta.

#### Reúna los [!DNL HubSpot] token de acceso de aplicación privada {#gather-credentials}

Necesita su [!DNL HubSpot] `Access token` para permitir el [!DNL HubSpot] destino para hacer llamadas de API a través de su [!DNL HubSpot] aplicación privada dentro de su [!DNL HubSpot] cuenta. El `Access token` sirve como `Bearer token` cuando usted [autenticar el destino](#authenticate).

Si no tiene una aplicación privada, siga la documentación para [Creación de una aplicación privada en [!DNL HubSpot]](https://developers.hubspot.com/docs/api/private-apps).

>[!IMPORTANT]
>
> A la aplicación privada se le deben asignar los ámbitos siguientes:
> `crm.objects.contacts.write`, `crm.objects.contacts.read`
> `crm.schemas.contacts.write`, `crm.schemas.contacts.read`

| Credencial | Descripción | Ejemplo |
| --- | --- | --- |
| `Bearer token` | El `Access token` de su [!DNL HubSpot] aplicación privada. <br>Para obtener su [!DNL HubSpot] `Access token` siga las [!DNL HubSpot] documentación para [realice llamadas API con el token de acceso de su aplicación](https://developers.hubspot.com/docs/api/private-apps#make-api-calls-with-your-app-s-access-token). | `pat-na1-11223344-abcde-12345-9876-1234a1b23456` |

## Mecanismos de protección {#guardrails}

[!DNL HubSpot] las aplicaciones privadas están sujetas a [Límites de velocidad](https://developers.hubspot.com/docs/api/usage-details). El número de llamadas que puede realizar su aplicación privada se basa en su [!DNL HubSpot] la suscripción de la cuenta y si ha adquirido el complemento API. Además, consulte la [Otros límites](https://developers.hubspot.com/docs/api/usage-details#other-limits).

## Identidades admitidas {#supported-identities}

[!DNL HubSpot] admite la actualización de identidades que se describe en la tabla siguiente. Más información sobre [identidades](/help/identity-service/namespaces.md).

| Identidad de destino | Ejemplo | Descripción | Consideraciones |
|---|---|---|---|
| `email` | `test@test.com` | Dirección de correo electrónico del contacto. | Obligatorio |

## Audiencias compatibles {#supported-audiences}

Esta sección describe todas las audiencias que puede exportar a este destino.

Este destino admite la activación de todas las audiencias generadas a través del Experience Platform [Servicio de segmentación](../../../segmentation/home.md).

Este destino también admite la activación de las audiencias que se describen en la tabla siguiente.

| Tipo de audiencia | Descripción |
---------|----------|
| Cargas personalizadas | Audiencias [importado](../../../segmentation/ui/overview.md#import-audience) en el Experience Platform desde archivos CSV. |

{style="table-layout:auto"}

## Tipo y frecuencia de exportación {#export-type-frequency}

Consulte la tabla siguiente para obtener información sobre el tipo y la frecuencia de exportación de destino.

| Elemento | Tipo | Notas |
---------|----------|---------|
| Tipo de exportación | **[!UICONTROL Basado en perfiles]** | <ul><li>Está exportando todos los miembros de una audiencia, junto con los campos de esquema deseados *(por ejemplo: dirección de correo electrónico, número de teléfono, apellidos)*, según la asignación de campo.</li><li> Además, se crea una nueva propiedad en [!DNL HubSpot] usando el nombre de audiencia y su valor se asocia con el estado de audiencia correspondiente de Platform, para cada una de las audiencias seleccionadas.</li></ul> |
| Frecuencia de exportación | **[!UICONTROL Transmisión]** | <ul><li>Los destinos de streaming son conexiones basadas en API &quot;siempre activadas&quot;. Tan pronto como se actualiza un perfil en Experience Platform según la evaluación de audiencias, el conector envía la actualización de forma descendente a la plataforma de destino. Más información sobre [destinos de streaming](/help/destinations/destination-types.md#streaming-destinations).</li></ul> |

{style="table-layout:auto"}

## Conectar con el destino {#connect}

>[!IMPORTANT]
>
>Para conectarse al destino, necesita el **[!UICONTROL Administrar destinos]** [permiso de control de acceso](/help/access-control/home.md#permissions). Lea el [información general de control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Para conectarse a este destino, siga los pasos descritos en la sección [tutorial de configuración de destino](../../ui/connect-destination.md). En el flujo de trabajo de configuración de destino, rellene los campos enumerados en las dos secciones siguientes.

En **[!UICONTROL Destinos]** > **[!UICONTROL Catálogo]** buscar [!DNL HubSpot]. También puede encontrarlo en la sección **[!UICONTROL CRM]** categoría.

### Autenticar en el destino {#authenticate}

Rellene los campos obligatorios siguientes. Consulte la [Reúna los [!DNL HubSpot] token de acceso de aplicación privada](#gather-credentials) para obtener cualquier guía.
* **[!UICONTROL Token de portador]**: El token de acceso para su [!DNL HubSpot] aplicación privada.

Para autenticarse en el destino, seleccione **[!UICONTROL Conectar con destino]**.
![Captura de pantalla de la IU de Platform que muestra cómo autenticarse.](../../assets/catalog/crm/hubspot/authenticate-destination.png)

Si los detalles proporcionados son válidos, la interfaz de usuario muestra un **[!UICONTROL Conectado]** estado con una marca de verificación verde. A continuación, puede continuar con el paso siguiente.

### Rellenar detalles de destino {#destination-details}

Para configurar los detalles del destino, rellene los campos obligatorios y opcionales a continuación. Un asterisco junto a un campo en la interfaz de usuario indica que el campo es obligatorio.
![Captura de pantalla de la IU de Platform que muestra los detalles del destino.](../../assets/catalog/crm/hubspot/destination-details.png)

* **[!UICONTROL Nombre]**: Un nombre con el que reconocerá este destino en el futuro.
* **[!UICONTROL Descripción]**: Una descripción que le ayudará a identificar este destino en el futuro.

### Habilitar alertas {#enable-alerts}

Puede activar alertas para recibir notificaciones sobre el estado del flujo de datos a su destino. Seleccione una alerta de la lista a la que suscribirse para recibir notificaciones sobre el estado del flujo de datos. Para obtener más información sobre las alertas, consulte la guía de [suscripción a alertas de destinos mediante la IU](../../ui/alerts.md).

Cuando haya terminado de proporcionar detalles para la conexión de destino, seleccione **[!UICONTROL Siguiente]**.

## Activar audiencias en este destino {#activate}

>[!IMPORTANT]
>
>Para activar los datos, necesita el **[!UICONTROL Administrar destinos]**, **[!UICONTROL Activar destinos]**, **[!UICONTROL Ver perfiles]**, y **[!UICONTROL Ver segmentos]** [permisos de control de acceso](/help/access-control/home.md#permissions). Lea el [información general de control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Leer [Activación de perfiles y audiencias en destinos de exportación de audiencia de streaming](/help/destinations/ui/activate-segment-streaming-destinations.md) para obtener instrucciones sobre cómo activar audiencias en este destino.

### Asignar atributos e identidades {#map}

Para enviar correctamente los datos de audiencia de Adobe Experience Platform a [!DNL HubSpot] destino, debe pasar por el paso de asignación de campos. La asignación consiste en crear un vínculo entre los campos de esquema del Modelo de datos de experiencia (XDM) en la cuenta de Platform y sus equivalentes correspondientes desde el destino de destino.

Para asignar correctamente los campos XDM a [!DNL HubSpot] campos de destino, siga los pasos a continuación:

#### Asignación de la variable `Email` identidad

El `Email` La identidad es una asignación obligatoria para este destino. Siga los pasos a continuación para asignarlo:
1. En el **[!UICONTROL Asignación]** paso, seleccione **[!UICONTROL Añadir nueva asignación]**. Ahora puede ver una nueva fila de asignación en la pantalla.
   ![Captura de pantalla de la IU de Platform con el botón Añadir nueva asignación resaltado.](../../assets/catalog/crm/hubspot/mapping-add-new-mapping.png)
1. En el **[!UICONTROL Seleccionar campo de origen]** , seleccione la **[!UICONTROL Seleccionar área de nombres de identidad]** y seleccione una identidad.
   ![Captura de pantalla de la IU de Platform seleccionando el correo electrónico como atributo de origen para asignarlo como identidad.](../../assets/catalog/crm/hubspot/mapping-select-source-identity.png)
1. En el **[!UICONTROL Seleccionar campo de destino]** , seleccione la **[!UICONTROL Seleccionar atributos]** y seleccione `email`.
   ![Captura de pantalla de la IU de Platform seleccionando el correo electrónico como atributo de destino para asignarlo como identidad.](../../assets/catalog/crm/hubspot/mapping-select-target-identity.png)

| Campo de origen | Campo de destino | Obligatorio |
| --- | --- | --- |
| `IdentityMap: Email` | `Identity: email` | Sí |

A continuación, se muestra un ejemplo con la asignación de identidad:
![Captura de pantalla de la IU de Platform con asignación de identidad de correo electrónico.](../../assets/catalog/crm/hubspot/mapping-identities.png)

#### Asignación **opcional** atributos

Para agregar cualquier otro atributo que desee actualizar entre el esquema de perfil XDM y la variable [!DNL HubSpot] cuenta repita los pasos a continuación:
1. En el **[!UICONTROL Asignación]** paso, seleccione **[!UICONTROL Añadir nueva asignación]**. Ahora puede ver una nueva fila de asignación en la pantalla.
   ![Captura de pantalla de la IU de Platform con el botón Añadir nueva asignación resaltado.](../../assets/catalog/crm/hubspot/mapping-add-new-mapping.png)
1. En el **[!UICONTROL Seleccionar campo de origen]** , seleccione la **[!UICONTROL Seleccionar atributos]** y seleccione el atributo XDM.
   ![Captura de pantalla de la IU de Platform seleccionando Nombre como atributo de origen.](../../assets/catalog/crm/hubspot/mapping-select-source-attribute.png)
1. En el **[!UICONTROL Seleccionar campo de destino]** ventana, elija **[!UICONTROL Seleccionar atributos]** y seleccione de la lista de atributos que se rellenan automáticamente desde su [!DNL HubSpot] cuenta. El destino utiliza el [[!DNL HubSpot] Propiedades](https://developers.hubspot.com/docs/api/crm/properties) API para recuperar esta información. Ambos [!DNL HubSpot] [propiedades predeterminadas](https://knowledge.hubspot.com/contacts/hubspots-default-contact-properties) y cualquier propiedad personalizada se recupera para su selección como campos de destino.
   ![Captura de pantalla de la IU de Platform seleccionando Nombre como atributo de destino.](../../assets/catalog/crm/hubspot/mapping-select-target-attribute.png)

Algunas asignaciones disponibles entre el esquema de perfil XDM y [!DNL Hubspot] se muestran a continuación:

| Campo de origen | Campo de destino |
| --- | --- |
| `xdm: person.name.firstName` | `Attribute: firstname` |
| `xdm: person.name.lastName` | `Attribute: lastname` |
| `xdm: workAddress.street1` | `Attribute: address` |
| `xdm: workAddress.city` | `Attribute: city` |
| `xdm: workAddress.country` | `Attribute: country` |

A continuación, se muestra un ejemplo con estas asignaciones de atributos:
![Ejemplo de captura de pantalla de la IU de Platform con asignaciones de atributos.](../../assets/catalog/crm/hubspot/mapping-attributes.png)

Cuando haya terminado de proporcionar las asignaciones para la conexión de destino, seleccione **[!UICONTROL Siguiente]**.

## Validar exportación de datos {#exported-data}

Para comprobar que ha configurado correctamente el destino, siga los pasos a continuación:

1. Inicie sesión en [!DNL HubSpot] sitio web y, a continuación, vaya al **[!UICONTROL Contactos]** para comprobar los estados de audiencia. Esta lista se puede configurar para que muestre columnas para las propiedades personalizadas creadas con el nombre de la audiencia cuyo valor sean los estados de audiencia.
   ![Captura de pantalla de la IU de HubSpot que muestra la página Contactos con encabezados de columna que muestran el nombre de la audiencia y las celdas y los estados de audiencia](../../assets/catalog/crm/hubspot/contacts.png)

1. También puede explorar en profundidad un individuo **[!UICONTROL Persona]** y vaya a las propiedades que muestran el nombre y los estados de audiencia.
   ![Captura de pantalla de la interfaz de usuario de HubSpot que muestra la página de contacto con propiedades personalizadas que muestran el nombre y los estados de audiencia.](../../assets/catalog/crm/hubspot/contact.png)

## Uso de datos y gobernanza {#data-usage-governance}

Todo [!DNL Adobe Experience Platform] Los destinos de cumplen con las políticas de uso de datos al gestionar los datos. Para obtener información detallada sobre cómo [!DNL Adobe Experience Platform] aplica la gobernanza de datos. Consulte la [Resumen de gobernanza de datos](/help/data-governance/home.md).

## Recursos adicionales {#additional-resources}

Información útil adicional del [!DNL HubSpot] Esta documentación es:
* [Métodos de autenticación en HubSpot](https://developers.hubspot.com/docs/api/intro-to-auth)
* [!DNL HubSpot] Referencias de API para [Contactos](https://developers.hubspot.com/docs/api/crm/contacts) y [Propiedades](https://developers.hubspot.com/docs/api/crm/properties) API.

### Changelog

Esta sección recoge la funcionalidad y las actualizaciones significativas de la documentación realizadas en este conector de destino.

+++ Ver registro de cambios

| Mes de lanzamiento | Tipo de actualización | Descripción |
|---|---|---|
| Septiembre de 2023 | Versión inicial | Versión de destino inicial y publicación de documentación. |

{style="table-layout:auto"}

+++
