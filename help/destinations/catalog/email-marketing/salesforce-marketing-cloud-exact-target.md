---
keywords: correo electrónico;correo electrónico;destinos de correo electrónico;salesforce;api salesforce marketing cloud destination
title: (API) Conexión de Marketing Cloud de Salesforce
description: El destino de Marketing Cloud de Salesforce (anteriormente conocido como ExactTarget) le permite exportar los datos de su cuenta y activarlos dentro de Salesforce Marketing Cloud para sus necesidades comerciales.
exl-id: 0cf068e6-8a0a-4292-a7ec-c40508846e27
source-git-commit: 5a9b7af3b009f8529f2e473b17f77c54de35003e
workflow-type: tm+mt
source-wordcount: '2464'
ht-degree: 1%

---

# [!DNL (API) Salesforce Marketing Cloud] connection

## Información general {#overview}

[[!DNL (API) Salesforce Marketing Cloud]](https://www.salesforce.com/products/marketing-cloud/overview/) (anteriormente conocido como [!DNL ExactTarget]) es un grupo de marketing digital que le permite crear y personalizar recorridos para que los visitantes y clientes personalicen su experiencia.

>[!IMPORTANT]
>
>Tenga en cuenta la diferencia entre esta conexión y la otra [[!DNL Salesforce Marketing Cloud] connection](/help/destinations/catalog/email-marketing/salesforce-marketing-cloud.md) que existe en la sección catálogo de marketing por correo electrónico . La otra conexión de Marketing Cloud de Salesforce le permite exportar archivos a una ubicación de almacenamiento especificada, mientras que se trata de una conexión de flujo basada en API.

Esta [!DNL Adobe Experience Platform] [destino](/help/destinations/home.md) aprovecha el [!DNL Salesforce Marketing Cloud] [actualizar contactos](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/updateContacts.html) API, que le permite añadir contactos o actualizar los datos de contacto para sus necesidades comerciales después de activarlos en un nuevo [!DNL Salesforce Marketing Cloud] segmento.

[!DNL Salesforce Marketing Cloud] utiliza OAuth 2 con Credenciales de cliente como mecanismo de autenticación para comunicarse con el [!DNL Salesforce Marketing Cloud] API. Instrucciones para autenticarse en su [!DNL Salesforce Marketing Cloud] más abajo, en la [Autenticar en destino](#authenticate) para obtener más información.

## Casos de uso {#use-cases}

Para ayudarle a comprender mejor cómo y cuándo debe usar la variable [!DNL (API) Salesforce Marketing Cloud] destino, aquí hay un ejemplo de caso de uso que los clientes de Adobe Experience Platform pueden resolver utilizando este destino.

### Enviar correos electrónicos a contactos para campañas de marketing {#use-case-send-emails}

El departamento de ventas de una plataforma de alquiler de viviendas quiere transmitir un correo electrónico de marketing a una audiencia de cliente objetivo. El equipo de marketing de la plataforma puede agregar nuevos contactos o actualizar contactos existentes *(y sus direcciones de correo electrónico)* a través de Adobe Experience Platform, cree segmentos a partir de sus propios datos sin conexión y envíelos a [!DNL Salesforce Marketing Cloud], que se puede utilizar para enviar el correo electrónico de la campaña de marketing.

## Requisitos previos {#prerequisites}

### Requisitos previos en el Experience Platform {#prerequisites-in-experience-platform}

Antes de activar los datos en la variable [!DNL (API) Salesforce Marketing Cloud] destino, debe tener un [esquema](/help/xdm/schema/composition.md), [conjunto de datos](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=en)y [segmentos](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=en) creado en [!DNL Experience Platform].

### Requisitos previos en [!DNL (API) Salesforce Marketing Cloud] {#prerequisites-destination}

Tenga en cuenta los siguientes requisitos previos para exportar datos de Platform a su [!DNL Salesforce Marketing Cloud] cuenta:

#### Debe tener un [!DNL Salesforce Marketing Cloud] account {#prerequisites-account}

A [!DNL Salesforce Marketing Cloud] cuenta con una suscripción a [Participación en la cuenta de Marketing Cloud](https://www.salesforce.com/products/marketing-cloud/marketing-automation/) es obligatorio para continuar.

Póngase en contacto con [[!DNL Salesforce] Asistencia](https://www.salesforce.com/company/contact-us/?d=cta-glob-footer-10) si no tiene un [!DNL Salesforce Marketing Cloud] falta la cuenta o la cuenta [!DNL Marketing Cloud Account Engagement] suscripción al producto.

#### Crear atributos dentro de [!DNL Salesforce Marketing Cloud] {#prerequisites-attribute}

Al activar segmentos en la variable [!DNL (API) Salesforce Marketing Cloud] destino, debe introducir un valor en la variable **[!UICONTROL ID de asignación]** para cada segmento activado, en la variable **[Programación de segmentos](#schedule-segment-export-example)** paso a paso.

[!DNL Salesforce] requiere que este valor lea e interprete correctamente los segmentos que llegan del Experience Platform y que actualice su estado de segmento en [!DNL Salesforce Marketing Cloud]. Consulte la documentación del Experience Platform para [Grupo de campos de esquema Detalles de pertenencia a segmentos](/help/xdm/field-groups/profile/segmentation.md) si necesita instrucciones sobre los estados de los segmentos.

Para cada segmento que active de Platform a [!DNL Salesforce Marketing Cloud], debe crear un atributo del tipo `Text` en [!DNL Salesforce]. Utilice la variable [!DNL Salesforce Marketing Cloud] [!DNL Contact Builder] para crear atributos. Los nombres de campo de atributo se utilizan para la variable [!DNL (API) Salesforce Marketing Cloud] campo de destino y debe crearse en el `[!DNL Email Demographics system attribute-set]`. Puede definir el carácter de campo con un máximo de 4000 caracteres, según sus necesidades comerciales. Consulte la [!DNL Salesforce Marketing Cloud] [Tipos de datos de Extensiones de datos](https://help.salesforce.com/s/articleView?id=sf.mc_es_data_extension_data_types.htm&amp;type=5) página de documentación para obtener información adicional sobre los tipos de atributos.

Consulte la [!DNL Salesforce Marketing Cloud] documentación para [crear atributos](https://help.salesforce.com/s/articleView?id=mc_cab_create_an_attribute.htm&amp;type=5&amp;language=en_US) si necesita instrucciones para crear atributos.

Ejemplo de la pantalla del diseñador de datos en [!DNL Salesforce Marketing Cloud], al que agregará el atributo se muestra a continuación:
![Diseñador de datos de la interfaz de usuario del Marketing Cloud de Salesforce.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/salesforce-data-designer.png)

Las vistas al [!DNL Salesforce Marketing Cloud] [!DNL Email Demographics] a continuación se muestra el conjunto de atributos:
![Conjunto de atributos demográficos de la interfaz de usuario de Marketing Cloud de Salesforce.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/salesforce-email-demograhics-fields.png)

La variable [!DNL (API) Salesforce Marketing Cloud] el destino utiliza la variable [!DNL Salesforce Marketing Cloud] [!DNL Search Attribute-Set Definitions REST] [API](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/retrieveAttributeSetDefinitions.html) para recuperar dinámicamente los atributos y sus conjuntos de atributos definidos en [!DNL Salesforce Marketing Cloud].

Se muestran en la sección **[!UICONTROL Campo de destino]** ventana de selección al configurar la variable [asignación](#mapping-considerations-example) en el flujo de trabajo para [activar segmentos en el destino](#activate). Tenga en cuenta que solo las asignaciones para los atributos definidos dentro de la variable [!DNL Salesforce Marketing Cloud] `[!DNL Email Demographics]` se admiten conjuntos de atributos.

>[!IMPORTANT]
>
>Within [!DNL Salesforce Marketing Cloud], debe crear atributos con un **[!UICONTROL NOMBRE DEL CAMPO]** que coincida exactamente con el valor especificado en **[!UICONTROL ID de asignación]** para cada segmento de Platform activado. Por ejemplo, la captura de pantalla siguiente muestra un atributo denominado `salesforce_mc_segment_1`. Al activar un segmento en este destino, agregue `salesforce_mc_segment_1` como **[!UICONTROL ID de asignación]** para rellenar las audiencias de segmento de Experience Platform en este atributo.

Un ejemplo de creación de atributos en [!DNL Salesforce Marketing Cloud], se muestra a continuación:
![Captura de pantalla de la interfaz de usuario del Marketing Cloud de Salesforce que muestra un atributo.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/salesforce-custom-field.png)

>[!TIP]
>
>* Al crear el atributo, no incluya caracteres de espacio en blanco en el nombre del campo. En su lugar, utilice el guión bajo `(_)` como separador.
>* Para distinguir entre atributos utilizados para segmentos de Platform y otros atributos dentro de [!DNL Salesforce Marketing Cloud], puede incluir un prefijo o sufijo reconocible para los atributos utilizados para los segmentos de Adobe. Por ejemplo, en lugar de `test_segment`, use `Adobe_test_segment` o `test_segment_Adobe`.
>* Si ya tiene otros atributos creados en [!DNL Salesforce Marketing Cloud], puede utilizar el mismo nombre que el segmento de Platform para identificar fácilmente el segmento en [!DNL Salesforce Marketing Cloud].


#### Recopilar [!DNL Salesforce Marketing Cloud] credenciales {#gather-credentials}

Tenga en cuenta los elementos siguientes antes de autenticarse en la variable [!DNL (API) Salesforce Marketing Cloud] destino.

| Credencial | Descripción | Ejemplo |
| --- | --- | --- |
| Subdomain | Consulte [[!DNL Salesforce Marketing Cloud domain prefix]](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/your-subdomain-tenant-specific-endpoints.html) para obtener este valor de la variable [!DNL Salesforce Marketing Cloud] interfaz. | Si su [!DNL Salesforce Marketing Cloud] el dominio es<br> *`mcq4jrssqdlyc4lph19nnqgzzs84`.login.exacttarget.com*, <br>debe proporcionar `mcq4jrssqdlyc4lph19nnqgzzs84` como valor. |
| ID del cliente | Consulte la [!DNL Salesforce Marketing Cloud] [documentación](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/access-token-s2s.html) para obtener este valor de la variable [!DNL Salesforce Marketing Cloud] interfaz. | r23kxxxxxxxx0z05xxxxxx |
| Secreto de cliente | Consulte la [!DNL Salesforce Marketing Cloud] [documentación](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/access-token-s2s.html) para obtener este valor de la variable [!DNL Salesforce Marketing Cloud] interfaz. | ipxxxxxxxxxxT4xxxxxxxxxx |

{style=&quot;table-layout:auto&quot;}

### Mecanismos de protección {#guardrails}

* Salesforce impone ciertos [límites de tasa](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/rate-limiting.html).
   * Consulte la [!DNL Salesforce Marketing Cloud] [documentación](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/rate-limiting-errors.html) para abordar los límites probables con los que podría encontrar y reducir los errores durante la ejecución.
   * Consulte la [[!DNL Salesforce Marketing Cloud] Precio de participación](https://www.salesforce.com/editions-pricing/marketing-cloud/email/) a *Descargar el gráfico comparativo de la edición completa* como pdf que detalla los límites impuestos por su plan.
   * La variable [Información general de API](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/apis-overview.html) detalles de la página límites adicionales.
   * Consulte [here](https://salesforce.stackexchange.com/questions/205898/marketing-cloud-api-limits) para una página que recopila estos detalles.
* El recuento de *campos personalizados permitidos por objeto* varía según su edición de Salesforce.
   * Consulte la [!DNL Salesforce] [documentación](https://help.salesforce.com/s/articleView?id=sf.custom_field_allocations.htm&amp;type=5) para obtener más información.
   * Si ha alcanzado el límite definido para *campos personalizados permitidos por objeto* en [!DNL Salesforce Marketing Cloud] necesitará
      * Elimine los atributos antiguos antes de agregar nuevos atributos en [!DNL Salesforce Marketing Cloud].
      * Actualice o elimine cualquier segmento activado en destinos de Platform que utilice estos nombres de atributo antiguos como valor proporcionado para **[!UICONTROL ID de asignación]** durante el [programación de segmentos](#schedule-segment-export-example) paso a paso.

## Identidades compatibles {#supported-identities}

[!DNL (API) Salesforce Marketing Cloud] admite la activación de identidades descritas en la tabla siguiente. Más información sobre [identidades](/help/identity-service/namespaces.md).

| Identidad de Target | Descripción | Consideraciones |
|---|---|---|
| contactKey | [!DNL Salesforce Marketing Cloud] Clave de contacto. Consulte la [!DNL Salesforce Marketing Cloud] [documentación](https://help.salesforce.com/s/articleView?id=sf.mc_cab_contact_builder_best_practices.htm&amp;type=5) si necesita más instrucciones. | Obligatorio |

## Tipo de exportación y frecuencia {#export-type-frequency}

Consulte la tabla siguiente para obtener información sobre el tipo y la frecuencia de exportación de destino.

| Elemento | Tipo | Notas |
---------|----------|---------|
| Tipo de exportación | **[!UICONTROL Basado en perfiles]** | <ul><li>Está exportando todos los miembros de un segmento, junto con los campos de esquema deseados *(por ejemplo: dirección de correo electrónico, número de teléfono, apellidos)*, según la asignación de campos.</li><li> Cada estado de segmento en [!DNL Salesforce Marketing Cloud] se actualiza con el estado del segmento correspondiente de Platform, en función de la variable **[!UICONTROL ID de asignación]** valor proporcionado durante el [programación de segmentos](#schedule-segment-export-example) paso a paso.</li></ul> |
| Frecuencia de exportación | **[!UICONTROL Transmisión]** | Los destinos de flujo continuo son conexiones basadas en API &quot;siempre activadas&quot;. Tan pronto como un perfil se actualiza en el Experience Platform en función de la evaluación de segmentos, el conector envía la actualización descendente a la plataforma de destino. Más información sobre [destinos de flujo continuo](/help/destinations/destination-types.md#streaming-destinations). |

{style=&quot;table-layout:auto&quot;}

## Conectarse al destino {#connect}

>[!IMPORTANT]
>
>Para conectarse al destino, necesita la variable **[!UICONTROL Administrar destinos]** [permiso de control de acceso](/help/access-control/home.md#permissions). Lea el [información general sobre el control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Para conectarse a este destino, siga los pasos descritos en la sección [tutorial de configuración de destino](../../ui/connect-destination.md). En el flujo de trabajo de configuración de destino, rellene los campos que aparecen en las dos secciones siguientes.

Within **[!UICONTROL Destinos]** > **[!UICONTROL Catálogo]**, busque [!DNL (API) Salesforce Marketing Cloud]. También puede localizarlo en la sección **[!UICONTROL Marketing por correo electrónico]** categoría.

### Autenticar en destino {#authenticate}

Para autenticarse en el destino, rellene los campos obligatorios a continuación y seleccione **[!UICONTROL Conectarse al destino]**. Consulte la [Recopilar [!DNL Salesforce Marketing Cloud] credenciales](#gather-credentials) para obtener más información.

| [!DNL (API) Salesforce Marketing Cloud] destino | [!DNL Salesforce Marketing Cloud] |
| --- | --- |
| **[!UICONTROL Subdomain]** | Su [!DNL Salesforce Marketing Cloud] prefijo de dominio. <br>Por ejemplo, si su dominio es <br> *`mcq4jrssqdlyc4lph19nnqgzzs84`.login.exacttarget.com*, <br> debe proporcionar `mcq4jrssqdlyc4lph19nnqgzzs84` como valor. |
| **[!UICONTROL ID del cliente]** | Su [!DNL Salesforce Marketing Cloud] `Client ID`. |
| **[!UICONTROL Secreto de cliente]** | Su [!DNL Salesforce Marketing Cloud] `Client Secret`. |

![Captura de pantalla de la interfaz de usuario de Platform que muestra cómo autenticarse en el Marketing Cloud de Salesforce.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/authenticate-destination.png)

Si los detalles proporcionados son válidos, la interfaz de usuario muestra un **[!UICONTROL Conectado]** con una marca de verificación verde, puede continuar con el siguiente paso.

### Rellenar detalles de destino {#destination-details}

Para configurar los detalles del destino, rellene los campos opcionales y requeridos a continuación. Un asterisco junto a un campo en la interfaz de usuario indica que el campo es obligatorio.
![Captura de pantalla de la interfaz de usuario de Platform que muestra los detalles del destino.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/destination-details.png)

* **[!UICONTROL Nombre]**: Un nombre por el cual reconocerá este destino en el futuro.
* **[!UICONTROL Descripción]**: Descripción que le ayudará a identificar este destino en el futuro.

### Habilitar alertas {#enable-alerts}

Puede activar las alertas para recibir notificaciones sobre el estado del flujo de datos a su destino. Seleccione una alerta de la lista para suscribirse y recibir notificaciones sobre el estado de su flujo de datos. Para obtener más información sobre las alertas, consulte la guía de [suscripción a alertas de destinos mediante la interfaz de usuario](../../ui/alerts.md).

Cuando haya terminado de proporcionar detalles para la conexión de destino, seleccione **[!UICONTROL Siguiente]**.

## Activar segmentos en este destino {#activate}

>[!IMPORTANT]
>
>Para activar los datos, necesita la variable **[!UICONTROL Administrar destinos]**, **[!UICONTROL Activar destinos]**, **[!UICONTROL Ver perfiles]** y **[!UICONTROL Ver segmentos]** [permisos de control de acceso](/help/access-control/home.md#permissions). Lea el [información general sobre el control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Lectura [Activar perfiles y segmentos en destinos de exportación de segmentos de flujo continuo](/help/destinations/ui/activate-segment-streaming-destinations.md) para obtener instrucciones sobre la activación de segmentos de audiencia en este destino.

### Consideraciones de asignación y ejemplo {#mapping-considerations-example}

Para enviar correctamente los datos de audiencia de Adobe Experience Platform a [!DNL (API) Salesforce Marketing Cloud] destino, debe pasar por el paso de asignación de campos. La asignación consiste en la creación de un vínculo entre los campos de esquema del Modelo de datos de experiencia (XDM) en la cuenta de Platform y sus equivalentes correspondientes desde el destino de destino.

Para asignar correctamente los campos XDM a la variable [!DNL (API) Salesforce Marketing Cloud] campos de destino, siga los pasos a continuación.

>[!IMPORTANT]
>
>Aunque los nombres de atributos serían según su [!DNL Salesforce Marketing Cloud] cuenta, las asignaciones para ambas `contactKey` y `personalEmail.address` son obligatorios. Al asignar atributos, solo los atributos del Experience Platform `Email Demographics` el conjunto de atributos debe utilizarse dentro de los campos de destino.

1. En el **[!UICONTROL Asignación]** paso, seleccione **[!UICONTROL Añadir nueva asignación]**. Verá una nueva fila de asignación en la pantalla.
   ![Ejemplo de captura de pantalla de la interfaz de usuario de Platform para Añadir nueva asignación.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/add-new-mapping.png)
1. En el **[!UICONTROL Seleccionar campo de origen]** , seleccione **[!UICONTROL Seleccionar atributos]** y seleccione el atributo XDM o elija el **[!UICONTROL Seleccionar área de nombres de identidad]** y seleccione una identidad.
1. En el **[!UICONTROL Seleccionar campo de destino]** , seleccione **[!UICONTROL Seleccionar área de nombres de identidad]** y seleccione una identidad o elija **[!UICONTROL Seleccionar atributos personalizados]** y seleccione un atributo de la categoría `Email Demographics` atributos mostrados según sea necesario. La variable [!DNL (API) Salesforce Marketing Cloud] el destino utiliza la variable [!DNL Salesforce Marketing Cloud] [!DNL Search Attribute-Set Definitions REST] [API](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/retrieveAttributeSetDefinitions.html) para recuperar dinámicamente los atributos y sus conjuntos de atributos definidos en [!DNL Salesforce Marketing Cloud]. Se muestran en la sección **[!UICONTROL Campo de destino]** ventana emergente al configurar el [asignación](#mapping-considerations-example) en el [activar segmentos en el flujo de trabajo](#activate). Tenga en cuenta que solo las asignaciones para los atributos definidos dentro de la variable [!DNL Salesforce Marketing Cloud] `[!DNL Email Demographics]` se admiten conjuntos de atributos.

   * Repita estos pasos para añadir las siguientes asignaciones entre el esquema de perfil XDM y [!DNL (API) Salesforce Marketing Cloud]: |Campo de origen|Campo de destino| Obligatorio| |—|—|—| |`IdentityMap: contactKey`|`Identity: salesforceContactKey`| `Mandatory` |\
      |`xdm: person.name.firstName`|`Attribute: Email Demographics.First Name`| - | |`xdm: personalEmail.address`|`Attribute: Email Addresses.Email Address`| - |

   * A continuación se muestra un ejemplo con estas asignaciones:
      ![Captura de pantalla de la interfaz de usuario de Platform que muestra asignaciones de Target.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/mappings.png)

Cuando haya terminado de proporcionar las asignaciones para la conexión de destino, seleccione **[!UICONTROL Siguiente]**.

### Programar exportación de segmentos y ejemplo {#schedule-segment-export-example}

Al realizar el [Programar exportación de segmentos](/help/destinations/ui/activate-segment-streaming-destinations.md#scheduling) paso, debe asignar manualmente los segmentos de Platform al [attributes](#prerequisites-attribute) en [!DNL Salesforce Marketing Cloud].

Para ello, seleccione cada segmento e introduzca el nombre del atributo en [!DNL Salesforce Marketing Cloud] en el [!DNL (API) Salesforce Marketing Cloud] **[!UICONTROL ID de asignación]** campo . Consulte la [Crear atributo dentro de [!DNL Salesforce Marketing Cloud]](#prerequisites-custom-field) para obtener instrucciones y prácticas recomendadas sobre la creación de atributos en [!DNL Salesforce Marketing Cloud].

Por ejemplo, si su [!DNL Salesforce Marketing Cloud] el atributo es `salesforce_mc_segment_1`, especifique este valor en la variable [!DNL (API) Salesforce Marketing Cloud] **[!UICONTROL ID de asignación]** para rellenar las audiencias de segmento de Experience Platform en este atributo.

Un atributo de ejemplo de [!DNL Salesforce Marketing Cloud] se muestra a continuación:
![Captura de pantalla de la interfaz de usuario del Marketing Cloud de Salesforce que muestra un atributo.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/salesforce-custom-field.png)

Ejemplo que indica la ubicación de la variable [!DNL (API) Salesforce Marketing Cloud] **[!UICONTROL ID de asignación]** se muestra a continuación:
![Captura de pantalla de la interfaz de usuario de Platform que muestra Programar exportación de segmentos.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/schedule-segment-export.png)

Como se muestra, la variable [!DNL (API) Salesforce Marketing Cloud] **[!UICONTROL ID de asignación]** debe coincidir exactamente con el valor especificado en [!DNL Salesforce Marketing Cloud] **[!UICONTROL NOMBRE DEL CAMPO]**.

Repita esta sección para cada segmento de Platform activado.

Según el caso de uso, todos los segmentos activados se pueden asignar al mismo [!DNL Salesforce Marketing Cloud] **[!UICONTROL NOMBRE DEL CAMPO]** o a diferentes **[!UICONTROL NOMBRE DEL CAMPO]** en [!DNL (API) Salesforce Marketing Cloud]. Podría ser un ejemplo típico basado en la imagen mostrada arriba.
| [!DNL (API) Salesforce Marketing Cloud] nombre del segmento | [!DNL Salesforce Marketing Cloud] **[!UICONTROL NOMBRE DEL CAMPO]** | [!DNL (API) Salesforce Marketing Cloud] **[!UICONTROL ID de asignación]** | | — | — | — | | segmento 1 de mc de salesforce | `salesforce_mc_segment_1` | `salesforce_mc_segment_1` | | segmento 2 de salesforce mc | `salesforce_mc_segment_2` | `salesforce_mc_segment_2` |

## Validación de la exportación de datos {#exported-data}

Para validar que ha configurado correctamente el destino, siga los pasos a continuación:

1. Select **[!UICONTROL Destinos]** > **[!UICONTROL Examinar]** para navegar a la lista de destinos.
   ![Captura de pantalla de la interfaz de usuario de Platform que muestra los destinos de exploración.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/browse-destinations.png)

1. Seleccione el destino y valide que el estado es **[!UICONTROL enabled]**.
   ![Captura de pantalla de la interfaz de usuario de Platform que muestra la ejecución del flujo de datos de Destinations.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/destination-dataflow-run.png)

1. Cambie a la **[!DNL Activation data]** y, a continuación, seleccione un nombre de segmento.
   ![Captura de pantalla de la interfaz de usuario de Platform que muestra los datos de activación de destinos.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/destinations-activation-data.png)

1. Monitorice el resumen del segmento y asegúrese de que el recuento de perfiles corresponde al recuento creado dentro del segmento.
   ![Captura de pantalla de la interfaz de usuario de Platform que muestra el segmento.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/segment.png)

1. Inicie sesión en la [[!DNL Salesforce Marketing Cloud]](https://mc.exacttarget.com/) sitio web. A continuación, vaya a la **[!DNL Audience Builder]** > **[!DNL Contact Builder]** > **[!DNL All contacts]** > **[!DNL Email]** y compruebe si se han añadido los perfiles del segmento.
   ![Captura de pantalla de la interfaz de usuario del Marketing Cloud de Salesforce que muestra la página Contactos con perfiles utilizados en el segmento.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/contacts.png)

1. Para comprobar si se ha actualizado algún perfil, vaya a la **[!UICONTROL Correo electrónico]** y compruebe si se han actualizado los valores de atributo del perfil del segmento. Si se realiza correctamente, puede ver que cada estado de segmento en [!DNL Salesforce Marketing Cloud] se actualizó con el estado del segmento correspondiente de Platform, en función de la variable **[!UICONTROL ID de asignación]** valor proporcionado en la variable [programación de segmentos](#schedule-segment-export-example) paso a paso.
   ![Captura de pantalla de la interfaz de usuario del Marketing Cloud de Salesforce que muestra la página de correo electrónico de contactos seleccionada con los estados de segmento actualizados.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/contact-detail.png)

## Uso y gobernanza de los datos {#data-usage-governance}

Todo [!DNL Adobe Experience Platform] Los destinos de cumplen las políticas de uso de datos al administrar los datos. Para obtener información detallada sobre cómo [!DNL Adobe Experience Platform] exige el control de datos; consulte [Información general sobre la administración de datos](/help/data-governance/home.md).

## Errores y solución de problemas {#errors-and-troubleshooting}

### Se han encontrado errores desconocidos al insertar eventos en el Marketing Cloud de Salesforce {#unknown-errors}

* Al comprobar la ejecución de un flujo de datos, podría encontrar el siguiente mensaje de error: `Unknown errors encountered while pushing events to the destination. Please contact the administrator and try again.`

   ![Captura de pantalla de la interfaz de usuario de Platform que muestra el error.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/error.png)

   * Para solucionar este error, compruebe que la variable **[!UICONTROL ID de asignación]** que proporcionó en el flujo de trabajo de activación para la variable [!DNL (API) Salesforce Marketing Cloud] el destino coincide exactamente con el nombre del atributo creado en [!DNL Salesforce Marketing Cloud]. Consulte la [Crear atributo dentro de [!DNL Salesforce Marketing Cloud]](#prerequisites-custom-field) para obtener más información.

* Al activar un segmento, puede obtener un mensaje de error: `The client's IP address is unauthorized for this account. Allowlist the client's IP address...`
   * Para solucionar este error, póngase en contacto con su [!DNL Salesforce Marketing Cloud] administrador de cuentas para agregar [Direcciones IP del Experience Platform](/help/destinations/catalog/streaming/ip-address-allow-list.md) a su [!DNL Salesforce Marketing Cloud] rangos de IP de confianza de las cuentas. Consulte la [!DNL Salesforce Marketing Cloud] [Direcciones IP para la inclusión en Listas de permitidos de Marketing Cloud](https://help.salesforce.com/s/articleView?id=sf.mc_es_ip_addresses_for_inclusion.htm&amp;type=5) documentación si necesita orientación adicional.

## Recursos adicionales {#additional-resources}

* [!DNL Salesforce Marketing Cloud] [API](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/apis-overview.html)
* [!DNL Salesforce Marketing Cloud] [documentación](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/updateContacts.html) explicación de cómo se actualizan los contactos con la información especificada en los grupos de atributos especificados.