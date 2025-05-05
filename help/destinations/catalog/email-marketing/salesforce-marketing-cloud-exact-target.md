---
title: (API) Conexión de Salesforce Marketing Cloud
description: El destino de Salesforce Marketing Cloud (anteriormente conocido como ExactTarget) le permite exportar los datos de su cuenta y activarlos dentro de Salesforce Marketing Cloud para sus necesidades comerciales.
exl-id: 0cf068e6-8a0a-4292-a7ec-c40508846e27
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '2916'
ht-degree: 2%

---

# [!DNL (API) Salesforce Marketing Cloud] conexión

## Información general {#overview}

[[!DNL (API) Salesforce Marketing Cloud]](https://www.salesforce.com/products/marketing-cloud/engagement/) (anteriormente conocido como [!DNL ExactTarget]) es un grupo de marketing digital que le permite crear y personalizar recorridos para que los visitantes y clientes personalicen su experiencia.

>[!IMPORTANT]
>
> Observe la diferencia entre esta conexión y la otra [[!DNL Salesforce Marketing Cloud] conexión](/help/destinations/catalog/email-marketing/salesforce-marketing-cloud.md) que existe dentro de la sección Catálogo de marketing de correo electrónico. La otra conexión de Salesforce Marketing Cloud le permite exportar archivos a una ubicación de almacenamiento especificada, mientras que esta es una conexión de flujo continuo basada en API.

En comparación con [!DNL Salesforce Marketing Cloud Account Engagement], que está más orientado al marketing **B2B**, el destino [!DNL (API) Salesforce Marketing Cloud] es ideal para los casos de uso **B2C** con ciclos de toma de decisiones transaccionales más cortos. Puede consolidar conjuntos de datos más grandes que representen el comportamiento de su audiencia objetivo para ajustar y mejorar las campañas de marketing priorizando y segmentando contactos, especialmente de conjuntos de datos fuera de [!DNL Salesforce]. *Tenga en cuenta que Experience Platform también tiene una conexión para [[!DNL Salesforce Marketing Cloud Account Engagement]](/help/destinations/catalog/email-marketing/salesforce-marketing-cloud-account-engagement.md).*

Este [!DNL Adobe Experience Platform] [destino](/help/destinations/home.md) usa la API [!DNL Salesforce Marketing Cloud] [actualizar contactos](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/updateContacts.html), que te permite **agregar contactos y actualizar datos de contacto** para tus necesidades comerciales después de activarlos en un nuevo segmento [!DNL Salesforce Marketing Cloud].

[!DNL Salesforce Marketing Cloud] utiliza OAuth 2 con credenciales de cliente como mecanismo de autenticación para comunicarse con la API [!DNL Salesforce Marketing Cloud]. Las instrucciones para autenticarse en su instancia de [!DNL Salesforce Marketing Cloud] se encuentran más abajo, en la sección [Autenticar en destino](#authenticate).

## Casos de uso {#use-cases}

Para ayudarle a comprender mejor cómo y cuándo debe utilizar el destino [!DNL (API) Salesforce Marketing Cloud], aquí tiene un ejemplo de uso que los clientes de Adobe Experience Platform pueden solucionar mediante este destino.

### Envío de correos electrónicos a contactos para campañas de marketing {#use-case-send-emails}

El departamento de ventas de una plataforma de alquiler de viviendas desea difundir un correo electrónico de marketing a una audiencia de cliente objetivo. El equipo de marketing de la plataforma puede agregar nuevos contactos o actualizar los contactos existentes *(y sus direcciones de correo electrónico)* a través de Adobe Experience Platform, crear audiencias a partir de sus propios datos sin conexión y enviar estas audiencias a [!DNL Salesforce Marketing Cloud], que luego se pueden usar para enviar el correo electrónico de la campaña de marketing.

## Requisitos previos {#prerequisites}

### Requisitos previos en Experience Platform {#prerequisites-in-experience-platform}

Antes de activar datos en el destino [!DNL (API) Salesforce Marketing Cloud], debe tener un [esquema](/help/xdm/schema/composition.md), un [conjunto de datos](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html) y [segmentos](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html) creados en [!DNL Experience Platform].

### Requisitos previos en [!DNL (API) Salesforce Marketing Cloud] {#prerequisites-destination}

Tenga en cuenta los siguientes requisitos previos para exportar datos de Experience Platform a su cuenta de [!DNL Salesforce Marketing Cloud]:

#### Necesita tener una cuenta de [!DNL Salesforce Marketing Cloud] {#prerequisites-account}

Es obligatorio abrir una cuenta de [!DNL Salesforce Marketing Cloud] con una suscripción al producto [[!DNL Marketing Cloud Engagement]](https://www.salesforce.com/products/marketing-cloud/engagement/) para continuar.

Póngase en contacto con [[!DNL Salesforce] Soporte técnico](https://www.salesforce.com/company/contact-us/?d=cta-glob-footer-10) si no tiene una cuenta de [!DNL Salesforce Marketing Cloud] o si a su cuenta le falta la suscripción de producto de [!DNL Marketing Cloud Engagement].

#### Crear atributos dentro de [!DNL Salesforce Marketing Cloud] {#prerequisites-attribute}

Al activar audiencias en el destino [!DNL (API) Salesforce Marketing Cloud], debe introducir un valor en el campo **[!UICONTROL ID de asignación]** para cada audiencia activada, en el paso **[Programación de audiencias](#schedule-segment-export-example)**.

[!DNL Salesforce] requiere este valor para leer e interpretar correctamente las audiencias que llegan desde Experience Platform y para actualizar su estado de audiencia en [!DNL Salesforce Marketing Cloud]. Consulte la documentación de Experience Platform para el [grupo de campos de esquema Detalles de pertenencia a audiencias](/help/xdm/field-groups/profile/segmentation.md) si necesita instrucciones sobre los estados de audiencia.

Para cada audiencia que active de Experience Platform a [!DNL Salesforce], debe tener un atributo de tipo `Text` vinculado a la extensión de datos [!DNL Email Demographics] en [!DNL Salesforce Marketing Cloud]. Use [!DNL Salesforce Marketing Cloud] [!DNL Contact Builder] para crear atributos. Consulte la documentación de [!DNL Salesforce Marketing Cloud] para [crear atributos](https://help.salesforce.com/s/articleView?id=mc_cab_create_an_attribute.htm&amp;type=5&amp;language=en_US) si necesita ayuda para crear atributos.

Los nombres de los campos de atributo se utilizan para el campo de destino [!DNL (API) Salesforce Marketing Cloud] durante el paso **[!UICONTROL Mapping]**. Puede definir el carácter de campo con un máximo de 4000 caracteres, según sus necesidades comerciales. Consulte la página de documentación [!DNL Salesforce Marketing Cloud] [Tipos de datos de extensiones de datos](https://help.salesforce.com/s/articleView?id=sf.mc_es_data_extension_data_types.htm&amp;type=5) para obtener información adicional sobre los tipos de atributos.

A continuación se muestra un ejemplo de la pantalla del diseñador de datos en [!DNL Salesforce Marketing Cloud], en la que agregará el atributo:
![Diseñador de datos de IU de Salesforce Marketing Cloud.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/salesforce-data-designer.png)

A continuación se muestra una vista de un grupo de atributos [!DNL Salesforce Marketing Cloud] [!DNL Email Data] con atributos correspondientes al estado de audiencia dentro de la extensión de datos [!DNL Email Demographics]:
![Grupo de atributos de datos de correo electrónico de la IU de Salesforce Marketing Cloud.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/salesforce-email-demographics-fields.png)

El destino [!DNL (API) Salesforce Marketing Cloud] usa la [!DNL Salesforce Marketing Cloud] [!DNL Search Attribute-Set Definitions REST] [API](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/retrieveAttributeSetDefinitions.html) para recuperar dinámicamente las extensiones de datos y sus atributos vinculados&#39; definidos dentro de [!DNL Salesforce Marketing Cloud].

Se muestran en la ventana de selección de **[!UICONTROL Campo de destino]** al configurar la [asignación](#mapping-considerations-example) en el flujo de trabajo para [activar audiencias en el destino](#activate).

>[!IMPORTANT]
>
> En [!DNL Salesforce Marketing Cloud], debe crear atributos con un **[!UICONTROL NOMBRE DE CAMPO]** que coincida exactamente con el valor especificado en **[!UICONTROL ID de asignación]** para cada segmento de Experience Platform activado. Por ejemplo, la captura de pantalla siguiente muestra un atributo denominado `salesforce_mc_segment_1`. Al activar una audiencia en este destino, agregue `salesforce_mc_segment_1` como **[!UICONTROL ID de asignación]** para rellenar audiencias de Experience Platform en este atributo.

A continuación se muestra un ejemplo de creación de atributos en [!DNL Salesforce Marketing Cloud]:
![Captura de pantalla de la interfaz de usuario de Salesforce Marketing Cloud que muestra un atributo.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/salesforce-custom-field.png)

>[!TIP]
>
> * Al crear el atributo, no incluya espacios en blanco en el nombre del campo. En su lugar, utilice el carácter de subrayado `(_)` como separador.
> * Para distinguir entre atributos utilizados para audiencias de Experience Platform y otros atributos dentro de [!DNL Salesforce Marketing Cloud], puede incluir un prefijo o sufijo reconocible para los atributos utilizados para segmentos de Adobe. Por ejemplo, en lugar de `test_segment`, use `Adobe_test_segment` o `test_segment_Adobe`.
> * Si ya ha creado otros atributos en [!DNL Salesforce Marketing Cloud], puede usar el mismo nombre que el segmento de Experience Platform para identificar fácilmente la audiencia en [!DNL Salesforce Marketing Cloud].

#### Asignar roles y permisos de usuario dentro de [!DNL Salesforce Marketing Cloud] {#prerequisites-roles-permissions}

Como [!DNL Salesforce Marketing Cloud] admite funciones personalizadas según el caso de uso, se debe asignar al usuario las funciones relevantes para actualizar los atributos en [!DNL Salesforce Marketing Cloud]. A continuación, se muestra un ejemplo de las funciones asignadas a un usuario:
![Interfaz de usuario de Salesforce Marketing Cloud para un usuario seleccionado que muestra sus roles asignados.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/salesforce-edit-roles.png)

Según las funciones que se hayan asignado al usuario [!DNL Salesforce Marketing Cloud], también deberá asignar permisos a la extensión de datos [!DNL Salesforce Marketing Cloud] que esté vinculada a los campos que desea actualizar.

Dado que este destino requiere acceso a `[!DNL data extension]`, debe permitirlo. Por ejemplo, para `Email` [!DNL data extension], debe permitirlo como se muestra a continuación:

![IU de Salesforce Marketing Cloud que muestra la extensión de datos de correo electrónico con los permisos permitidos.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/salesforce-permisions-list.png)

Para restringir el nivel de acceso, también puede anular el acceso individual mediante privilegios granulares.
![IU de Salesforce Marketing Cloud que muestra la extensión de datos de correo electrónico con permisos granulares.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/sales-email-attribute-set-permission.png)

Consulte las páginas [[!DNL Marketing Cloud Roles]](https://help.salesforce.com/s/articleView?language=en_US&amp;id=sf.mc_overview_marketing_cloud_roles.htm&amp;type=5) y [[!DNL Marketing Cloud Roles and Permissions]](https://help.salesforce.com/s/articleView?language=en_US&amp;id=sf.mc_overview_roles.htm&amp;type=5) para obtener instrucciones detalladas.

#### Recopilar [!DNL Salesforce Marketing Cloud] credenciales {#gather-credentials}

Observe los elementos siguientes antes de autenticarse en el destino [!DNL (API) Salesforce Marketing Cloud].

| Credencial | Descripción | Ejemplo |
| --- | --- | --- |
| Subdominio | Consulte [[!DNL Salesforce Marketing Cloud domain prefix]](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/your-subdomain-tenant-specific-endpoints.html) para obtener información sobre cómo obtener este valor de la interfaz [!DNL Salesforce Marketing Cloud]. | Si el dominio [!DNL Salesforce Marketing Cloud] es <br> *`mcq4jrssqdlyc4lph19nnqgzzs84`.login.exacttarget.com*, <br>debe proporcionar `mcq4jrssqdlyc4lph19nnqgzzs84` como valor. |
| ID de cliente | Consulte la [!DNL Salesforce Marketing Cloud] [documentación](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/access-token-s2s.html) para obtener información sobre cómo obtener este valor de la interfaz [!DNL Salesforce Marketing Cloud]. | r23kxxxxxxx0z05xxxxxx |
| Secreto del cliente | Consulte la [!DNL Salesforce Marketing Cloud] [documentación](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/access-token-s2s.html) para obtener información sobre cómo obtener este valor de la interfaz [!DNL Salesforce Marketing Cloud]. | ipxxxxxxxxxxT4xxxxxxxxxxx |

{style="table-layout:auto"}

### Mecanismos de protección {#guardrails}

* Salesforce impone ciertos [límites de tarifa](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/rate-limiting.html).
   * Consulte la [!DNL Salesforce Marketing Cloud] [documentación](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/rate-limiting-errors.html) para resolver cualquier límite probable que pueda encontrar y reducir los errores durante la ejecución.
   * Consulte la página [[!DNL Salesforce Marketing Cloud] Precios de participación](https://www.salesforce.com/editions-pricing/marketing-cloud/email/) para *descargar el gráfico comparativo de edición completa* como PDF que detalla los límites impuestos por su plan.
   * La página [Información general de API](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/apis-overview.html) detalla límites adicionales.
   * Consulta [aquí](https://salesforce.stackexchange.com/questions/205898/marketing-cloud-api-limits) para ver una página que recopila estos detalles.
* El recuento de *campos personalizados permitidos por objeto* varía según la edición de Salesforce.
   * Consulte la [!DNL Salesforce] [documentación](https://help.salesforce.com/s/articleView?id=sf.custom_field_allocations.htm&amp;type=5) para obtener instrucciones adicionales.
   * Si ha alcanzado el límite definido de *campos personalizados permitidos por objeto* en [!DNL Salesforce Marketing Cloud], deberá
      * Quite los atributos antiguos antes de agregar nuevos atributos en [!DNL Salesforce Marketing Cloud].
      * Actualice o elimine cualquier audiencia activada en destinos de Experience Platform que use estos nombres de atributo antiguos como el valor proporcionado para **[!UICONTROL ID de asignación]** durante el paso [programación de audiencias](#schedule-segment-export-example).

## Identidades admitidas {#supported-identities}

[!DNL (API) Salesforce Marketing Cloud] admite la activación de las identidades descritas en la tabla siguiente. Más información sobre [identidades](/help/identity-service/features/namespaces.md).

| Identidad de destino | Descripción | Consideraciones |
|---|---|---|
| contactKey | Clave de contacto [!DNL Salesforce Marketing Cloud]. Consulte la [!DNL Salesforce Marketing Cloud] [documentación](https://help.salesforce.com/s/articleView?id=sf.mc_cab_contact_builder_best_practices.htm&amp;type=5) si necesita más instrucciones. | Obligatorio |

## Audiencias compatibles {#supported-audiences}

Esta sección describe qué tipos de audiencias puede exportar a este destino.

| Origen de audiencia | Admitido | Descripción |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Audiencias generadas a través del [servicio de segmentación](../../../segmentation/home.md) de Experience Platform. |
| Cargas personalizadas | X | Las audiencias [importadas](../../../segmentation/ui/audience-portal.md#import-audience) en Experience Platform desde archivos CSV. |

{style="table-layout:auto"}

## Tipo y frecuencia de exportación {#export-type-frequency}

Consulte la tabla siguiente para obtener información sobre el tipo y la frecuencia de exportación de destino.

| Elemento | Tipo | Notas |
---------|----------|---------|
| Tipo de exportación | **[!UICONTROL Basado en perfil]** | <ul><li>Va a exportar todos los miembros de un segmento, junto con los campos de esquema deseados *(por ejemplo: dirección de correo electrónico, número de teléfono, apellidos)*, según la asignación de campos.</li><li> Cada estado de segmento de [!DNL Salesforce Marketing Cloud] se actualiza con el estado de audiencia correspondiente de Experience Platform, según el valor de **[!UICONTROL ID de asignación]** proporcionado durante el paso [programación de audiencias](#schedule-segment-export-example).</li></ul> |
| Frecuencia de exportación | **[!UICONTROL Transmisión]** | Los destinos de streaming son conexiones basadas en API &quot;siempre activadas&quot;. Tan pronto como se actualiza un perfil en Experience Platform basado en la evaluación de audiencias, el conector envía la actualización de forma descendente a la plataforma de destino. Más información sobre [destinos de streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Conexión al destino {#connect}

>[!IMPORTANT]
>
> Para conectarse al destino, necesita el **[!UICONTROL permiso Administrar destinos]** [control de acceso](/help/access-control/home.md#permissions). Lea la [descripción general del control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Para conectarse a este destino, siga los pasos descritos en el [tutorial de configuración de destino](../../ui/connect-destination.md). En el flujo de trabajo de configuración de destino, rellene los campos enumerados en las dos secciones siguientes.

En **[!UICONTROL destinos]** > **[!UICONTROL catálogo]**, busque [!DNL (API) Salesforce Marketing Cloud]. También puede ubicarlo en la categoría **[!UICONTROL Marketing por correo electrónico]**.

### Autenticarse en el destino {#authenticate}

Para autenticarte en el destino, rellena los campos obligatorios a continuación y selecciona **[!UICONTROL Conectarse al destino]**. Consulte la sección [Recopilar [!DNL Salesforce Marketing Cloud] credenciales](#gather-credentials) para obtener instrucciones.

| [!DNL (API) Salesforce Marketing Cloud] destino | [!DNL Salesforce Marketing Cloud] |
| --- | --- |
| **[!UICONTROL Subdominio]** | Prefijo de dominio [!DNL Salesforce Marketing Cloud]. <br>Por ejemplo, si su dominio es <br> *`mcq4jrssqdlyc4lph19nnqgzzs84`.login.exacttarget.com*, <br> debe proporcionar `mcq4jrssqdlyc4lph19nnqgzzs84` como valor. |
| **[!UICONTROL ID de cliente]** | Su [!DNL Salesforce Marketing Cloud] `Client ID`. |
| **[!UICONTROL Secreto de cliente]** | Su [!DNL Salesforce Marketing Cloud] `Client Secret`. |

![Captura de pantalla de la interfaz de usuario de Experience Platform que muestra cómo autenticarse en Salesforce Marketing Cloud.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/authenticate-destination.png)

Si los detalles proporcionados son válidos, la interfaz de usuario muestra el estado **[!UICONTROL Conectado]** con una marca de verificación verde y, a continuación, puede continuar con el siguiente paso.

### Rellenar detalles de destino {#destination-details}

Para configurar los detalles del destino, rellene los campos obligatorios y opcionales a continuación. Un asterisco junto a un campo en la interfaz de usuario indica que el campo es obligatorio.
![Captura de pantalla de la interfaz de usuario de Experience Platform que muestra los detalles del destino.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/destination-details.png)

* **[!UICONTROL Nombre]**: Un nombre por el cual reconocerá este destino en el futuro.
* **[!UICONTROL Descripción]**: Una descripción que le ayudará a identificar este destino en el futuro.

### Habilitar alertas {#enable-alerts}

Puede activar alertas para recibir notificaciones sobre el estado del flujo de datos a su destino. Seleccione una alerta de la lista a la que suscribirse para recibir notificaciones sobre el estado del flujo de datos. Para obtener más información sobre las alertas, consulte la guía sobre [suscripción a alertas de destinos mediante la interfaz de usuario](../../ui/alerts.md).

Cuando termine de proporcionar detalles para la conexión de destino, seleccione **[!UICONTROL Siguiente]**.

## Activar públicos en este destino {#activate}

>[!IMPORTANT]
> 
> * Para activar los datos, necesita los **[!UICONTROL permisos de control de acceso]**, **[!UICONTROL Activar destinos]**, **[!UICONTROL Ver perfiles]** y **[!UICONTROL Ver segmentos]**&#x200B;[para ](/help/access-control/home.md#permissions). Lea la [descripción general del control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.
> * Para exportar *identidades*, necesita el **[[!UICONTROL permiso de control de acceso]](/help/access-control/home.md#permissions) de&rbrack;** Ver gráfico de identidad&lbrack;. <br> ![Seleccione el área de nombres de identidad resaltada en el flujo de trabajo para activar audiencias en los destinos.](/help/destinations/assets/overview/export-identities-to-destination.png "Seleccione el área de nombres de identidad resaltada en el flujo de trabajo para activar audiencias en los destinos."){width="100" zoomable="yes"}

Lea [Activar perfiles y audiencias en destinos de exportación de audiencias de streaming](/help/destinations/ui/activate-segment-streaming-destinations.md) para obtener instrucciones sobre cómo activar audiencias en este destino.

### Consideraciones sobre asignación y ejemplo {#mapping-considerations-example}

Para enviar correctamente los datos de audiencia de Adobe Experience Platform al destino [!DNL (API) Salesforce Marketing Cloud], debe pasar por el paso de asignación de campos. La asignación consiste en crear un vínculo entre los campos de esquema del Modelo de datos de experiencia (XDM) en la cuenta de Experience Platform y sus equivalentes correspondientes desde el destino de destino.

Para asignar correctamente los campos XDM a los campos de destino [!DNL (API) Salesforce Marketing Cloud], siga los pasos a continuación.

>[!IMPORTANT]
>
> * Aunque los nombres de atributo estarían de acuerdo con su cuenta de [!DNL Salesforce Marketing Cloud], las asignaciones para `contactKey` y `personalEmail.address` son obligatorias.
>
> * La integración con la API [!DNL Salesforce Marketing Cloud] está sujeta a un límite de paginación en cuanto a la cantidad de atributos que Experience Platform puede recuperar de Salesforce. Esto significa que durante el paso de **[!UICONTROL Asignación]**, el esquema del campo de destino puede mostrar un máximo de 2000 atributos de su cuenta de Salesforce.

1. En el paso **[!UICONTROL Asignación]**, seleccione **[!UICONTROL Agregar nueva asignación]**. Verá una nueva fila de asignación en la pantalla.
   ![Ejemplo de captura de pantalla de la interfaz de usuario de Experience Platform para Agregar nueva asignación.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/add-new-mapping.png)
1. En la ventana **[!UICONTROL Seleccionar campo de origen]**, elija la categoría **[!UICONTROL Seleccionar atributos]** y seleccione el atributo XDM o elija **[!UICONTROL Seleccionar área de nombres de identidad]** y seleccione una identidad.
1. En la ventana **[!UICONTROL Seleccionar campo de destino]**, elija **[!UICONTROL Seleccionar área de nombres de identidad]** y seleccione una identidad o elija **[!UICONTROL Seleccionar atributos]** categoría y seleccione un atributo de las extensiones de datos que se muestran según sea necesario. El destino [!DNL (API) Salesforce Marketing Cloud] usa la [!DNL Salesforce Marketing Cloud] [!DNL Search Attribute-Set Definitions REST] [API](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/retrieveAttributeSetDefinitions.html) para recuperar dinámicamente las extensiones de datos y sus atributos vinculados&#39; definidos dentro de [!DNL Salesforce Marketing Cloud]. Se muestran en la ventana emergente **[!UICONTROL Campo de destino]** al configurar la [asignación](#mapping-considerations-example) en el [flujo de trabajo de activación de audiencias](#activate).

   * Repita estos pasos para agregar las siguientes asignaciones entre su esquema de perfil XDM y [!DNL (API) Salesforce Marketing Cloud]:

     | Campo de origen | Campo de destino | Obligatorio |
     |---|---|---|
     | `IdentityMap: contactKey` | `Identity: salesforceContactKey` | `Mandatory` |
     | `xdm: personalEmail.address` | `Attribute: Email Address` de la extensión de datos [!DNL Salesforce Marketing Cloud] [!DNL Email Addresses]. | `Mandatory`, al agregar nuevos contactos. |
     | `xdm: person.name.firstName` | `Attribute: First Name` de la extensión de datos [!DNL Salesforce Marketing Cloud] deseada. | - |

   * A continuación se muestra un ejemplo con estas asignaciones:

     ![Ejemplo de captura de pantalla de IU de Experience Platform que muestra asignaciones de destino.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/mappings.png)

Cuando haya terminado de proporcionar las asignaciones para la conexión de destino, seleccione **[!UICONTROL Siguiente]**.

### Programar exportación de audiencias y ejemplo {#schedule-segment-export-example}

Al realizar el paso [Programar exportación de audiencias](/help/destinations/ui/activate-segment-streaming-destinations.md#scheduling), debe asignar manualmente las audiencias de Experience Platform a los [atributos](#prerequisites-attribute) en [!DNL Salesforce Marketing Cloud].

Para ello, seleccione cada segmento y, a continuación, introduzca el nombre del atributo de [!DNL Salesforce Marketing Cloud] en el campo [!DNL (API) Salesforce Marketing Cloud] **[!UICONTROL ID de asignación]**. Consulte la sección [Crear atributo en [!DNL Salesforce Marketing Cloud]](#prerequisites-custom-field) para obtener instrucciones y prácticas recomendadas sobre la creación de atributos en [!DNL Salesforce Marketing Cloud].

Por ejemplo, si el atributo [!DNL Salesforce Marketing Cloud] es `salesforce_mc_segment_1`, especifique este valor en [!DNL (API) Salesforce Marketing Cloud] **[!UICONTROL Id. de asignación]** para rellenar audiencias de Experience Platform en este atributo.

A continuación se muestra un atributo de ejemplo de [!DNL Salesforce Marketing Cloud]:
![Captura de pantalla de la interfaz de usuario de Salesforce Marketing Cloud que muestra un atributo.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/salesforce-custom-field.png)

A continuación se muestra un ejemplo que indica la ubicación de [!DNL (API) Salesforce Marketing Cloud] **[!UICONTROL ID de asignación]**:

![Ejemplo de captura de pantalla de la IU de Experience Platform que muestra Programar exportación de audiencias.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/schedule-segment-export.png)

Como se muestra, el [!DNL (API) Salesforce Marketing Cloud] **[!UICONTROL ID. de asignación]** debe coincidir exactamente con el valor especificado en [!DNL Salesforce Marketing Cloud] **[!UICONTROL NOMBRE DE CAMPO]**.

Repita esta sección para cada segmento de Experience Platform activado.

Un ejemplo típico basado en la imagen mostrada arriba podría ser.

| [!DNL (API) Salesforce Marketing Cloud] nombre de segmento | [!DNL Salesforce Marketing Cloud] **[!UICONTROL NOMBRE DE CAMPO]** | [!DNL (API) Salesforce Marketing Cloud] **[!UICONTROL ID de asignación]** |
| --- | --- | --- |
| salesforce mc audience 1 | `salesforce_mc_segment_1` | `salesforce_mc_segment_1` |
| salesforce mc audience 2 | `salesforce_mc_segment_2` | `salesforce_mc_segment_2` |

## Validar exportación de datos {#exported-data}

Para comprobar que ha configurado correctamente el destino, siga los pasos a continuación:

1. Seleccione **[!UICONTROL Destinos]** > **[!UICONTROL Examinar]** para navegar a la lista de destinos.
   ![Captura de pantalla de la IU de Experience Platform que muestra destinos de exploración.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/browse-destinations.png)

1. Seleccione el destino y valide que el estado es **[!UICONTROL enabled]**.
   ![Captura de pantalla de la IU de Experience Platform que muestra la ejecución del flujo de datos de destinos.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/destination-dataflow-run.png)

1. Cambie a la ficha **[!DNL Activation data]** y, a continuación, seleccione un nombre de audiencia.
   ![Ejemplo de captura de pantalla de la IU de Experience Platform que muestra datos de activación de destinos.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/destinations-activation-data.png)

1. Monitorice el resumen de audiencia y asegúrese de que el recuento de perfiles corresponde al recuento creado dentro del segmento.
   ![Ejemplo de captura de pantalla de la IU de Experience Platform que muestra el segmento.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/segment.png)

1. Inicie sesión en el sitio web [[!DNL Salesforce Marketing Cloud]](https://mc.exacttarget.com/). A continuación, vaya a la página **[!DNL Audience Builder]** > **[!DNL Contact Builder]** > **[!DNL All contacts]** > **[!DNL Email]** y compruebe si se han agregado los perfiles de la audiencia.
   ![Captura de pantalla de la interfaz de usuario de Salesforce Marketing Cloud que muestra la página Contactos con los perfiles utilizados en el segmento.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/contacts.png)

1. Para comprobar si se han actualizado los perfiles, vaya a la página **[!UICONTROL Correo electrónico]** y compruebe si se han actualizado los valores de atributo del perfil de la audiencia. Si lo consigue, verá que cada estado de audiencia de [!DNL Salesforce Marketing Cloud] se actualizó con el estado de audiencia correspondiente de Experience Platform, según el valor de **[!UICONTROL ID. de asignación]** proporcionado en el paso [programación de audiencia](#schedule-segment-export-example).
   ![Captura de pantalla de la interfaz de usuario de Salesforce Marketing Cloud que muestra la página de correo electrónico Contactos seleccionada con estados de audiencia actualizados.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/contact-detail.png)

## Uso de datos y gobernanza {#data-usage-governance}

Todos los destinos de [!DNL Adobe Experience Platform] cumplen con las políticas de uso de datos al administrar los datos. Para obtener información detallada sobre cómo [!DNL Adobe Experience Platform] aplica el control de datos, consulte la [Información general sobre el control de datos](/help/data-governance/home.md).

## Errores y solución de problemas {#errors-and-troubleshooting}

### Se detectaron errores desconocidos al insertar eventos en Salesforce Marketing Cloud {#unknown-errors}

* Al comprobar la ejecución de un flujo de datos, puede que aparezca el siguiente mensaje de error: `Unknown errors encountered while pushing events to the destination. Please contact the administrator and try again.`
  ![Captura de pantalla de la IU de Experience Platform que muestra error.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/error.png)

   * Para corregir este error, compruebe que la **[!UICONTROL ID. de asignación]** proporcionada en el flujo de trabajo de activación para el destino [!DNL (API) Salesforce Marketing Cloud] coincide exactamente con el nombre del atributo que creó en [!DNL Salesforce Marketing Cloud]. Consulte la sección [Crear atributo en [!DNL Salesforce Marketing Cloud]](#prerequisites-custom-field) para obtener instrucciones.

* Al activar un segmento, podría obtener un mensaje de error: `The client's IP address is unauthorized for this account. Allowlist the client's IP address...`
   * Para corregir este error, póngase en contacto con el administrador de su cuenta de [!DNL Salesforce Marketing Cloud] para agregar [direcciones IP de Experience Platform](/help/destinations/catalog/streaming/ip-address-allow-list.md) a los intervalos de IP de confianza de sus cuentas de [!DNL Salesforce Marketing Cloud]. Consulte la documentación de [!DNL Salesforce Marketing Cloud] [Direcciones IP para su inclusión en Listas de permitidos en Marketing Cloud](https://help.salesforce.com/s/articleView?id=sf.mc_es_ip_addresses_for_inclusion.htm&amp;type=5) si necesita más instrucciones.

## Recursos adicionales {#additional-resources}

* [!DNL Salesforce Marketing Cloud] [API](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/apis-overview.html)
* [!DNL Salesforce Marketing Cloud] [documentación](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/updateContacts.html) que explica cómo se actualizan los contactos con la información especificada.

### Changelog {#changelog}

Esta sección recoge la funcionalidad y las actualizaciones significativas de la documentación realizadas en este conector de destino.

+++ Ver registro de cambios

| Mes de lanzamiento | Tipo de actualización | Descripción |
|---|---|---|
| Octubre de 2023 | Actualización de documentación  | <ul><li>Actualizamos la sección [Requisitos previos en (API) Salesforce Marketing Cloud](#prerequisites-destination) y, en general, eliminamos las referencias innecesarias a los grupos de atributos en todo el documento.</li> <li>Se ha actualizado la documentación para indicar que los atributos de los estados de audiencias deben crearse en [!DNL Salesforce Marketing Cloud] dentro de la extensión de datos [!DNL Email Demographics] solamente.</li> <li>Actualizamos la tabla de asignación en la sección [Consideraciones sobre la asignación y ejemplo](#mapping-considerations-example); la asignación del atributo `Email Address` dentro de la extensión de datos `Email Addresses` está marcada como obligatoria; este requisito se mencionó en la llamada marcada como IMPORTANTE pero se omitió de la tabla.</li></ul> |
| Abril de 2023 | Actualización de documentación  | <ul><li>Hemos corregido un enunciado y un vínculo de referencia en la sección [Requisitos previos de (API) Salesforce Marketing Cloud](#prerequisites-destination) para indicar que [!DNL Salesforce Marketing Cloud Engagement] es una suscripción obligatoria para usar este destino. Anteriormente, la sección indicaba erróneamente que los usuarios necesitaban una suscripción al acuerdo de **Account** de Marketing Cloud para continuar.</li> <li>Hemos agregado una sección en [requisitos previos](#prerequisites) para que [roles y permisos](#prerequisites-roles-permissions) se asignen al usuario [!DNL Salesforce] para que este destino funcione. (PLATIR-26299)</li></ul> |
| Febrero de 2023 | Actualización de documentación  | Actualizamos la sección [Requisitos previos en (API) Salesforce Marketing Cloud](#prerequisites-destination) para incluir un vínculo de referencia que indique que [!DNL Salesforce Marketing Cloud Engagement] es una suscripción obligatoria para usar este destino. |
| Febrero de 2023 | Actualización de funcionalidad | Se ha corregido un problema por el cual una configuración incorrecta en el destino provocaba que se enviara un JSON con formato incorrecto a Salesforce. Esto provocaba que algunos usuarios vieran un alto número de identidades con errores en la activación. (PLATIR-26299) |
| Enero de 2023 | Actualización de documentación  | <ul><li>Hemos actualizado la sección [Requisitos previos en [!DNL Salesforce]](#prerequisites-destination) para indicar que se deben crear atributos en el lado [!DNL Salesforce]. Esta sección ahora incluye instrucciones detalladas sobre cómo hacerlo y prácticas recomendadas para nombrar los atributos en [!DNL Salesforce]. (PLATIR-25602)</li><li>Hemos agregado instrucciones claras sobre cómo usar el ID de asignación para cada audiencia activada en el paso [programación de audiencias](#schedule-segment-export-example). (PLATIR-25602)</li></ul> |
| Octubre de 2022 | Versión inicial | Versión de destino inicial y publicación de documentación. |

{style="table-layout:auto"}

+++
