---
keywords: crm;CRM;destinos de crm;salesforce crm;destino de crm de salesforce
title: Conexión de Salesforce CRM
description: El destino de CRM de Salesforce le permite exportar los datos de su cuenta y activarlos dentro de CRM de Salesforce para sus necesidades comerciales.
exl-id: bd9cb656-d742-4a18-97a2-546d4056d093
source-git-commit: ba39f62cd77acedb7bfc0081dbb5f59906c9b287
workflow-type: tm+mt
source-wordcount: '2821'
ht-degree: 1%

---

# [!DNL Salesforce CRM] conexión

## Información general {#overview}

[[!DNL Salesforce CRM]](https://www.salesforce.com/crm/) es una popular plataforma de administración de la relación con los clientes (CRM) y admite los tipos de perfiles que se describen a continuación:

* [Posibles clientes](https://developer.salesforce.com/docs/atlas.en-us.object_reference.meta/object_reference/sforce_api_objects_lead.htm) - Un posible cliente es el nombre de una persona o compañía que puede (o no) estar interesada en los productos o servicios que vende.
* [Contactos](https://developer.salesforce.com/docs/atlas.en-us.object_reference.meta/object_reference/sforce_api_objects_contact.htm): un contacto es una persona con la que uno de sus representantes ha establecido una relación y ha sido calificado como cliente potencial.

Este [!DNL Adobe Experience Platform] [destino](/help/destinations/home.md) aprovecha [[!DNL Salesforce composite API]](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/resources_composite_sobjects_collections_update.htm), que admite ambos tipos de perfiles descritos anteriormente.

Al [activar segmentos](#activate), puede seleccionar entre posibles clientes o contactos y actualizar atributos y datos de audiencia en [!DNL Salesforce CRM].

[!DNL Salesforce CRM] utiliza OAuth 2 con concesión de contraseña como mecanismo de autenticación para comunicarse con la API de REST de Salesforce. Las instrucciones para autenticarse en su instancia de [!DNL Salesforce CRM] se encuentran más abajo, en la sección [Autenticar en destino](#authenticate).

## Casos de uso {#use-cases}

Como experto en marketing, puede ofrecer experiencias personalizadas a los usuarios en función de los atributos de sus perfiles de Adobe Experience Platform. Puede crear audiencias a partir de los datos sin conexión y enviarlas a Salesforce CRM para actualizar la pertenencia a CRM en cuanto se actualicen las audiencias y los perfiles en Adobe Experience Platform.

## Requisitos previos {#prerequisites}

### Requisitos previos en Experience Platform {#prerequisites-in-experience-platform}

Antes de activar datos en el destino de Salesforce CRM, debe tener [schema](/help/xdm/schema/composition.md), [dataset](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html) y [segments](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html) creados en [!DNL Experience Platform].

### Requisitos previos en [!DNL Salesforce CRM] {#prerequisites-destination}

Tenga en cuenta los siguientes requisitos previos de [!DNL Salesforce CRM] para exportar datos de Platform a su cuenta de Salesforce:

#### Necesita tener una cuenta de [!DNL Salesforce] {#prerequisites-account}

Vaya a la página [!DNL Salesforce] [prueba](https://www.salesforce.com/in/form/signup/freetrial-sales/) para registrarse y crear una cuenta de [!DNL Salesforce], si todavía no la tiene.

#### Configurar una aplicación conectada en [!DNL Salesforce] {#prerequisites-connected-app}

Primero, debe configurar una [[!DNL Salesforce] aplicación conectada](https://help.salesforce.com/s/articleView?id=sf.connected_app_create.htm&amp;language=en_US&amp;r=https%3A%2F%2Fhelp.salesforce.com%2F&amp;type=5) dentro de su cuenta de [!DNL Salesforce], si todavía no la tiene. [!DNL Salesforce CRM] aprovechará la aplicación conectada para conectarse a [!DNL Salesforce].

A continuación, habilite [!DNL OAuth Settings for API Integration] para [!DNL Salesforce connected app]. Consulte la documentación de [[!DNL Salesforce]](https://help.salesforce.com/s/articleView?id=connected_app_create_api_integration.htm&amp;type=5&amp;language=en_US) para obtener instrucciones.

Además, asegúrese de que los [ámbitos](https://help.salesforce.com/s/articleView?id=connected_app_create_api_integration.htm&amp;type=5&amp;language=en_US) mencionados a continuación estén seleccionados para [!DNL Salesforce connected app].

* ``chatter_api``
* ``lightning``
* ``visualforce``
* ``content``
* ``openid``
* ``full``
* ``api``
* ``web``
* ``refresh_token``
* ``offline_access``

Por último, asegúrese de que la concesión `password` esté habilitada en su cuenta de [!DNL Salesforce]. Consulte la documentación de [!DNL Salesforce] [Flujo de nombre de usuario y contraseña de OAuth 2.0 para escenarios especiales](https://help.salesforce.com/s/articleView?id=sf.remoteaccess_oauth_username_password_flow.htm&amp;type=5) si necesita ayuda.

>[!IMPORTANT]
>
>Si el administrador de su cuenta de [!DNL Salesforce] ha restringido el acceso a rangos de IP de confianza, deberá ponerse en contacto con ellos para obtener [IP del Experience Platform](/help/destinations/catalog/streaming/ip-address-allow-list.md) incluidas en la lista de permitidos. Consulte la documentación de [!DNL Salesforce] [Restringir el acceso a rangos de IP fiables para una aplicación conectada](https://help.salesforce.com/s/articleView?id=sf.connected_app_edit_ip_ranges.htm&amp;type=5) si necesita instrucciones adicionales.

#### Crear campos personalizados en [!DNL Salesforce] {#prerequisites-custom-field}

Al activar audiencias en el destino [!DNL Salesforce CRM], debe introducir un valor en el campo **[!UICONTROL ID de asignación]** para cada audiencia activada, en el paso **[Programación de audiencias](#schedule-segment-export-example)**.

[!DNL Salesforce CRM] requiere este valor para leer e interpretar correctamente las audiencias que llegan del Experience Platform y actualizar su estado de audiencia en [!DNL Salesforce]. Consulte la documentación del Experience Platform para el [grupo de campos de esquema Detalles de pertenencia a audiencias](/help/xdm/field-groups/profile/segmentation.md) si necesita instrucciones sobre los estados de audiencia.

Para cada audiencia que active desde Platform a [!DNL Salesforce CRM], debe crear un campo personalizado del tipo `Text Area (Long)` en [!DNL Salesforce]. Puede definir la longitud de caracteres de campo de cualquier tamaño entre 256 y 131 072 caracteres según sus necesidades comerciales. Consulte la página de documentación de [!DNL Salesforce] [Tipos de campos personalizados](https://help.salesforce.com/s/articleView?id=sf.custom_field_types.htm&amp;type=5) para obtener información adicional sobre los tipos de campos personalizados. Consulte también la documentación de [!DNL Salesforce] para [crear campos personalizados](https://help.salesforce.com/s/articleView?id=mc_cab_create_an_attribute.htm&amp;type=5&amp;language=en_US) si necesita ayuda para crear campos.

>[!IMPORTANT]
>
>No incluya espacios en blanco en el nombre del campo. En su lugar, utilice el carácter de subrayado `(_)` como separador.
>En [!DNL Salesforce] debe crear campos personalizados con un **[!UICONTROL Nombre de campo]** que coincida exactamente con el valor especificado en **[!UICONTROL Id. de asignación]** para cada segmento de Platform activado. Por ejemplo, la captura de pantalla siguiente muestra un campo personalizado denominado `crm_2_seg`. Al activar una audiencia en este destino, agregue `crm_2_seg` como **[!UICONTROL ID de asignación]** para rellenar audiencias de Experience Platform en este campo personalizado.

A continuación se muestra un ejemplo de creación de campo personalizado en [!DNL Salesforce], *Paso 1 - Seleccionar el tipo de datos*:
![Captura de pantalla de la interfaz de usuario de Salesforce que muestra la creación de campos personalizados, paso 1: seleccione el tipo de datos.](../../assets/catalog/crm/salesforce/create-salesforce-custom-field-step-1.png)

A continuación se muestra un ejemplo de creación de campo personalizado en [!DNL Salesforce], *Paso 2 - Escriba los detalles del campo personalizado*:
![Captura de pantalla de la interfaz de usuario de Salesforce que muestra la creación de campos personalizados, paso 2: escriba los detalles del campo personalizado.](../../assets/catalog/crm/salesforce/create-salesforce-custom-field-step-2.png)

>[!TIP]
>
>* Para distinguir entre los campos personalizados utilizados para audiencias de Platform y otros campos personalizados dentro de [!DNL Salesforce], puede incluir un prefijo o sufijo reconocible al crear el campo personalizado. Por ejemplo, en lugar de `test_segment`, use `Adobe_test_segment` o `test_segment_Adobe`
>* Si ya tiene otros campos personalizados creados en [!DNL Salesforce], puede usar el mismo nombre que el segmento de Platform para identificar fácilmente la audiencia en [!DNL Salesforce].

>[!NOTE]
>
>* Los objetos de Salesforce están restringidos a 25 campos externos; consulte [Atributos de campo personalizados](https://help.salesforce.com/s/articleView?id=sf.custom_field_attributes.htm&amp;type=5).
>* Esta restricción implica que solo puede tener un máximo de 25 suscripciones a la audiencia de Experience Platform activas en cualquier momento.
>* Si ha alcanzado este límite en Salesforce, debe eliminar los atributos personalizados de Salesforce que se usaron para almacenar el estado de audiencia con audiencias antiguas en Experience Platform antes de poder usar un nuevo **[!UICONTROL ID de asignación]**.

#### Recopilar [!DNL Salesforce CRM] credenciales {#gather-credentials}

Observe los elementos siguientes antes de autenticarse en el destino [!DNL Salesforce CRM]:

| Credencial | Descripción | Ejemplo |
| --- | --- | --- |
| `Username` | Su nombre de usuario de la cuenta [!DNL Salesforce]. | |
| `Password` | Contraseña de su cuenta de [!DNL Salesforce]. | |
| `Security Token` | El token de seguridad [!DNL Salesforce] que adjuntará más adelante al final de su contraseña de [!DNL Salesforce] para crear una cadena concatenada que se utilizará como la **[!UICONTROL contraseña]** al [autenticarse en el destino](#authenticate).<br> Consulte la documentación de [!DNL Salesforce] para [restablecer el token de seguridad](https://help.salesforce.com/s/articleView?id=sf.user_security_token.htm&amp;type=5) para obtener información sobre cómo regenerarlo desde la interfaz de [!DNL Salesforce] si no dispone del token de seguridad. |  |
| `Custom Domain` | Prefijo de dominio [!DNL Salesforce]. <br> Consulte la [[!DNL Salesforce] documentación](https://help.salesforce.com/s/articleView?id=sf.domain_name_setting_login_policy.htm&amp;type=5) para obtener información sobre cómo obtener este valor de la interfaz [!DNL Salesforce]. | Si el dominio [!DNL Salesforce] es <br> *`d5i000000isb4eak-dev-ed`.my.salesforce.com*,<br> necesitará `d5i000000isb4eak-dev-ed` como valor. |
| `Client ID` | Su Salesforce `Consumer Key`. <br> Consulte la [[!DNL Salesforce] documentación](https://help.salesforce.com/s/articleView?id=sf.connected_app_rotate_consumer_details.htm&amp;type=5) para obtener información sobre cómo obtener este valor de la interfaz [!DNL Salesforce]. | |
| `Client Secret` | Su Salesforce `Consumer Secret`. <br> Consulte la [[!DNL Salesforce] documentación](https://help.salesforce.com/s/articleView?id=sf.connected_app_rotate_consumer_details.htm&amp;type=5) para obtener información sobre cómo obtener este valor de la interfaz [!DNL Salesforce]. | |

### Mecanismos de protección {#guardrails}

[!DNL Salesforce] equilibra las cargas de transacción mediante la imposición de límites de solicitud, tasa y tiempo de espera. Consulte [Límites y asignaciones de solicitudes de API](https://developer.salesforce.com/docs/atlas.en-us.salesforce_app_limits_cheatsheet.meta/salesforce_app_limits_cheatsheet/salesforce_app_limits_platform_api.htm) para obtener detalles.

Si el administrador de cuentas de [!DNL Salesforce] ha impuesto restricciones de IP, tendrá que agregar [direcciones IP de Experience Platform](/help/destinations/catalog/streaming/ip-address-allow-list.md) a los intervalos de IP de confianza de sus cuentas de [!DNL Salesforce]. Consulte la documentación de [!DNL Salesforce] [Restringir el acceso a rangos de IP fiables para una aplicación conectada](https://help.salesforce.com/s/articleView?id=sf.connected_app_edit_ip_ranges.htm&amp;type=5) si necesita instrucciones adicionales.

>[!IMPORTANT]
>
>Al [activar segmentos](#activate), debe seleccionar entre los tipos *Contacto* o *Posible cliente*. Debe asegurarse de que las audiencias tengan la asignación de datos adecuada según el tipo seleccionado.

## Identidades admitidas {#supported-identities}

[!DNL Salesforce CRM] admite la actualización de las identidades descritas en la tabla siguiente. Más información sobre [identidades](/help/identity-service/features/namespaces.md).

| Identidad de destino | Descripción | Consideraciones |
|---|---|---|
| `SalesforceId` | El identificador [!DNL Salesforce CRM] de las identidades de contacto o posible cliente que exporta o actualiza a través del segmento. | Obligatorio |

## Tipo y frecuencia de exportación {#export-type-frequency}

Consulte la tabla siguiente para obtener información sobre el tipo y la frecuencia de exportación de destino.

| Elemento | Tipo | Notas |
---------|----------|---------|
| Tipo de exportación | **[!UICONTROL Basado en perfil]** | <ul><li>Va a exportar todos los miembros de un segmento, junto con los campos de esquema deseados *(por ejemplo: dirección de correo electrónico, número de teléfono, apellidos)*, según la asignación de campos.</li><li> Cada estado de audiencia de [!DNL Salesforce CRM] se actualiza con el estado de audiencia correspondiente de Platform, según el valor de **[!UICONTROL ID de asignación]** proporcionado durante el paso [programación de audiencia](#schedule-segment-export-example).</li></ul> |
| Frecuencia de exportación | **[!UICONTROL Transmisión]** | <ul><li>Los destinos de streaming son conexiones basadas en API &quot;siempre activadas&quot;. Tan pronto como se actualiza un perfil en Experience Platform según la evaluación de audiencias, el conector envía la actualización de forma descendente a la plataforma de destino. Más información sobre [destinos de streaming](/help/destinations/destination-types.md#streaming-destinations).</li></ul> |

{style="table-layout:auto"}

## Conexión al destino {#connect}

>[!IMPORTANT]
>
>Para conectarse al destino, necesita los **[!UICONTROL permisos de control de acceso](/help/access-control/home.md#permissions) de Ver destinos]** y **[!UICONTROL Administrar destinos]**[5}. Lea la [descripción general del control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Para conectarse a este destino, siga los pasos descritos en el [tutorial de configuración de destino](../../ui/connect-destination.md). En el flujo de trabajo de configuración de destino, rellene los campos enumerados en las dos secciones siguientes.

En **[!UICONTROL destinos]** > **[!UICONTROL catálogo]**, busque [!DNL Salesforce CRM]. También puede ubicarlo en la categoría **[!UICONTROL CRM]**.

### Autenticarse en el destino {#authenticate}

Para autenticarte en el destino, rellena los campos obligatorios a continuación y selecciona **[!UICONTROL Conectarse al destino]**. Consulte la sección [Recopilar [!DNL Salesforce CRM] credenciales](#gather-credentials) para obtener instrucciones.
| Credencial | Descripción |
| — | — |
| **[!UICONTROL Nombre de usuario]** | Su nombre de usuario de cuenta [!DNL Salesforce]. |
| **[!UICONTROL Contraseña]** | Una cadena concatenada compuesta por la contraseña de su cuenta [!DNL Salesforce] anexada con el token de seguridad [!DNL Salesforce].<br>El valor concatenado adopta la forma de `{PASSWORD}{TOKEN}`.<br> Tenga en cuenta que no utilice llaves ni espacios.<br>Por ejemplo, si la contraseña de [!DNL Salesforce] es `MyPa$$w0rd123` y el token de seguridad de [!DNL Salesforce] es `TOKEN12345....0000`, el valor concatenado que usará en el campo **[!UICONTROL Contraseña]** es `MyPa$$w0rd123TOKEN12345....0000`. |
| **[!UICONTROL Dominio personalizado]** | Prefijo de dominio [!DNL Salesforce]. <br>Por ejemplo, si su dominio es *`d5i000000isb4eak-dev-ed`.my.salesforce.com*, debe proporcionar `d5i000000isb4eak-dev-ed` como valor. |
| **[!UICONTROL ID de cliente]** | Su [!DNL Salesforce] conectó la aplicación `Consumer Key`. |
| **[!UICONTROL Secreto de cliente]** | Su [!DNL Salesforce] conectó la aplicación `Consumer Secret`. |

![Captura de pantalla de IU de Platform que muestra cómo autenticarse.](../../assets/catalog/crm/salesforce/authenticate-destination.png)

Si los detalles proporcionados son válidos, la interfaz de usuario muestra el estado **[!UICONTROL Conectado]** con una marca de verificación verde y, a continuación, puede continuar con el siguiente paso.

### Rellenar detalles de destino {#destination-details}

Para configurar los detalles del destino, rellene los campos obligatorios y opcionales a continuación. Un asterisco junto a un campo en la interfaz de usuario indica que el campo es obligatorio.
* **[!UICONTROL Nombre]**: Un nombre por el cual reconocerá este destino en el futuro.
* **[!UICONTROL Descripción]**: Una descripción que le ayudará a identificar este destino en el futuro.
* **[!UICONTROL Tipo de ID de Salesforce]**:
   * Seleccione **[!UICONTROL Contacto]** si las identidades que desea exportar o actualizar son del tipo *Contacto*.
   * Seleccione **[!UICONTROL posible cliente]** si las identidades que desea exportar o actualizar son del tipo *posible cliente*.

![Captura de pantalla de IU de Platform que muestra los detalles del destino.](../../assets/catalog/crm/salesforce/destination-details.png)

### Habilitar alertas {#enable-alerts}

Puede activar alertas para recibir notificaciones sobre el estado del flujo de datos a su destino. Seleccione una alerta de la lista a la que suscribirse para recibir notificaciones sobre el estado del flujo de datos. Para obtener más información sobre las alertas, consulte la guía sobre [suscripción a alertas de destinos mediante la interfaz de usuario](../../ui/alerts.md).

Cuando termine de proporcionar detalles para la conexión de destino, seleccione **[!UICONTROL Siguiente]**.

## Activar públicos en este destino {#activate}

>[!IMPORTANT]
> 
>* Para activar los datos, necesita los **[!UICONTROL permisos de control de acceso]**, **[!UICONTROL Activar destinos]**, **[!UICONTROL Ver perfiles]** y **[!UICONTROL Ver segmentos]**[para ](/help/access-control/home.md#permissions). Lea la [descripción general del control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.
>* Para exportar *identidades*, necesita el **[!UICONTROL permiso de control de acceso](/help/access-control/home.md#permissions) de]** Ver gráfico de identidad[. <br> ![Seleccione el área de nombres de identidad resaltada en el flujo de trabajo para activar audiencias en los destinos.](/help/destinations/assets/overview/export-identities-to-destination.png "Seleccione el área de nombres de identidad resaltada en el flujo de trabajo para activar audiencias en los destinos."){width="100" zoomable="yes"}

Lea [Activar perfiles y audiencias en destinos de exportación de audiencias de streaming](/help/destinations/ui/activate-segment-streaming-destinations.md) para obtener instrucciones sobre cómo activar audiencias en este destino.

### Consideraciones sobre asignación y ejemplo {#mapping-considerations-example}

Para enviar correctamente los datos de audiencia de Adobe Experience Platform al destino [!DNL Salesforce CRM], debe pasar por el paso de asignación de campos. La asignación consiste en crear un vínculo entre los campos de esquema del Modelo de datos de experiencia (XDM) en la cuenta de Platform y sus equivalentes correspondientes desde el destino de destino.

Los atributos especificados en el **[!UICONTROL campo de destino]** deben tener exactamente el nombre descrito en la tabla de asignaciones de atributos, ya que estos atributos formarán el cuerpo de la solicitud.

Los atributos especificados en el **[!UICONTROL campo Source]** no siguen ninguna restricción de este tipo. Puede asignarlo según sus necesidades; sin embargo, asegúrese de que el formato de los datos de entrada sea válido según la [[!DNL Salesforce] documentación](https://help.salesforce.com/s/articleView?id=sf.custom_field_attributes.htm&amp;type=5). Si los datos de entrada no son válidos, se producirá un error en la llamada de actualización a [!DNL Salesforce] y no se actualizarán los contactos ni los posibles clientes.

Para asignar correctamente los campos XDM a los campos de destino [!DNL (API) Salesforce CRM], siga estos pasos:

1. En el paso **[!UICONTROL Asignación]**, seleccione **[!UICONTROL Agregar nueva asignación]**, verá una nueva fila de asignación en la pantalla.
   ![Ejemplo de captura de pantalla de IU de Platform para agregar nueva asignación.](../../assets/catalog/crm/salesforce/add-new-mapping.png)
1. En la ventana **[!UICONTROL Seleccionar campo de origen]**, elija la categoría **[!UICONTROL Seleccionar atributos]** y seleccione el atributo XDM o elija **[!UICONTROL Seleccionar área de nombres de identidad]** y seleccione una identidad.
1. En la ventana **[!UICONTROL Seleccionar campo de destino]**, elija **[!UICONTROL Seleccionar área de nombres de identidad]** y seleccione una identidad o elija **[!UICONTROL Seleccionar atributos personalizados]** categoría y seleccione un atributo o defina uno con el campo **[!UICONTROL Nombre de atributo]** según sea necesario. Consulte la [[!DNL Salesforce CRM] documentación](https://help.salesforce.com/s/articleView?id=sf.custom_field_attributes.htm&amp;type=5) para obtener instrucciones sobre los atributos admitidos.
   * Repita estos pasos para agregar las siguientes asignaciones entre su esquema de perfil XDM y [!DNL (API) Salesforce CRM]:

   **Trabajando con contactos**

   * Si está trabajando con *Contactos* dentro de su segmento, consulte la Referencia de objeto en Salesforce para [Contacto](https://developer.salesforce.com/docs/atlas.en-us.object_reference.meta/object_reference/sforce_api_objects_contact.htm) para definir asignaciones para los campos que se van a actualizar.
   * Puede identificar los campos obligatorios si busca la palabra *Requerido*, que se menciona en las descripciones de los campos del vínculo anterior.
   * Según los campos que desee exportar o actualizar, agregue asignaciones entre el esquema de perfil XDM y [!DNL (API) Salesforce CRM]:
|Campo de Source|Campo de destino| Notas |
| — | — | — |
|`IdentityMap: crmID`|`Identity: SalesforceId`|`Mandatory`|
|`xdm: person.name.lastName`|`Attribute: LastName`| `Mandatory`. Apellidos del contacto de hasta 80 caracteres. |\
     |`xdm: person.name.firstName`|`Attribute: FirstName`| Nombre del contacto de hasta 40 caracteres. |
|`xdm: personalEmail.address`|`Attribute: Email`| La dirección de correo electrónico del contacto. |

   * A continuación se muestra un ejemplo con estas asignaciones:
     ![Ejemplo de captura de pantalla de IU de Platform que muestra asignaciones de Target.](../../assets/catalog/crm/salesforce/mappings-contacts.png)

   **Trabajando con posibles clientes**

   * Si está trabajando con *posibles clientes* dentro del segmento, consulte la Referencia de objeto en Salesforce para [Posible cliente](https://developer.salesforce.com/docs/atlas.en-us.object_reference.meta/object_reference/sforce_api_objects_lead.htm) para definir asignaciones para los campos que se van a actualizar.
   * Puede identificar los campos obligatorios si busca la palabra *Requerido*, que se menciona en las descripciones de los campos del vínculo anterior.
   * Según los campos que desee exportar o actualizar, agregue asignaciones entre el esquema de perfil XDM y [!DNL (API) Salesforce CRM]:
|Campo de Source|Campo de destino| Notas |
| — | — | — |
|`IdentityMap: crmID`|`Identity: SalesforceId`|`Mandatory`|
|`xdm: person.name.lastName`|`Attribute: LastName`| `Mandatory`. Apellidos del posible cliente de hasta 80 caracteres. |\
     |`xdm: b2b.companyName`|`Attribute: Company`| `Mandatory`. La compañía del líder. |
|`xdm: personalEmail.address`|`Attribute: Email`| La dirección de correo electrónico del posible cliente. |

   * A continuación se muestra un ejemplo con estas asignaciones:
     ![Ejemplo de captura de pantalla de IU de Platform que muestra asignaciones de Target.](../../assets/catalog/crm/salesforce/mappings-leads.png)

Cuando haya terminado de proporcionar las asignaciones para la conexión de destino, seleccione **[!UICONTROL Siguiente]**.

### Programar exportación de audiencias y ejemplo {#schedule-segment-export-example}

Al realizar el paso [Programar exportación de audiencias](/help/destinations/ui/activate-segment-streaming-destinations.md#scheduling), debe asignar manualmente las audiencias activadas desde Platform a su campo personalizado correspondiente en [!DNL Salesforce].

Para ello, seleccione cada segmento y luego introduzca el nombre de campo personalizado de [!DNL Salesforce] en el campo [!DNL Salesforce CRM] **[!UICONTROL ID de asignación]**. Consulte la sección [Crear campos personalizados en [!DNL Salesforce]](#prerequisites-custom-field) para obtener instrucciones y prácticas recomendadas sobre la creación de campos personalizados en [!DNL Salesforce].

Por ejemplo, si el campo personalizado [!DNL Salesforce] es `crm_2_seg`, especifique este valor en [!DNL Salesforce CRM] **[!UICONTROL Id. de asignación]** para rellenar audiencias de Experience Platform en este campo personalizado.

A continuación se muestra un ejemplo de campo personalizado de [!DNL Salesforce]:
![[!DNL Salesforce] captura de pantalla de la interfaz de usuario que muestra el campo personalizado.](../../assets/catalog/crm/salesforce/salesforce-custom-field.png)

A continuación se muestra un ejemplo que indica la ubicación de [!DNL Salesforce CRM] **[!UICONTROL ID de asignación]**:
![Ejemplo de captura de pantalla de la IU de Platform que muestra Programar exportación de audiencias.](../../assets/catalog/crm/salesforce/schedule-segment-export.png)

Como se muestra arriba del [!DNL Salesforce] **[!UICONTROL Nombre de campo]** coincide exactamente con el valor especificado en [!DNL Salesforce CRM] **[!UICONTROL Id. de asignación]**.

Según el caso de uso, todas las audiencias activadas se pueden asignar al mismo campo personalizado de [!DNL Salesforce] o a diferentes **[!UICONTROL nombres de campo]** en [!DNL Salesforce CRM]. Un ejemplo típico basado en la imagen mostrada arriba podría ser.
| [!DNL Salesforce CRM] nombre de segmento | [!DNL Salesforce] **[!UICONTROL Nombre de campo]** | [!DNL Salesforce CRM] **[!UICONTROL ID de asignación]** |
| — | — | — |
| crm_1_seg | `crm_1_seg` | `crm_1_seg` |
| crm_2_seg | `crm_2_seg` | `crm_2_seg` |

Repita esta sección para cada segmento de Platform activado.

## Validar exportación de datos {#exported-data}

Para comprobar que ha configurado correctamente el destino, siga los pasos a continuación:

1. Seleccione **[!UICONTROL Destinos]** > **[!UICONTROL Examinar]** para navegar a la lista de destinos.
   ![Captura de pantalla de IU que muestra destinos de exploración.](../../assets/catalog/crm/salesforce/browse-destinations.png)

1. Seleccione el destino y valide que el estado es **[!UICONTROL enabled]**.
   ![Captura de pantalla de IU de Platform que muestra la ejecución del flujo de datos de destinos.](../../assets/catalog/crm/salesforce/destination-dataflow-run.png)

1. Cambie a la ficha **[!UICONTROL Datos de activación]** y, a continuación, seleccione un nombre de audiencia.
   ![Ejemplo de captura de pantalla de IU de Platform que muestra datos de activación de destinos.](../../assets/catalog/crm/salesforce/destinations-activation-data.png)

1. Monitorice el resumen de audiencia y asegúrese de que el recuento de perfiles corresponde al recuento creado dentro del segmento.
   ![Ejemplo de captura de pantalla de IU de Platform que muestra el segmento.](../../assets/catalog/crm/salesforce/segment.png)

1. Finalmente, inicie sesión en el sitio web de Salesforce y valide si los perfiles de la audiencia se han agregado o actualizado.

   **Trabajando con contactos**

   * Si ha seleccionado *Contactos* dentro del segmento de Platform, vaya a la página **[!DNL Apps]** > **[!DNL Contacts]**.
     ![Captura de pantalla de Salesforce CRM que muestra la página Contactos con los perfiles del segmento.](../../assets/catalog/crm/salesforce/contacts.png)

   * Seleccione un *contacto* y compruebe si los campos están actualizados. Puede ver que cada estado de audiencia en [!DNL Salesforce CRM] se actualizó con el estado de audiencia correspondiente de Platform, según el valor de **[!UICONTROL ID de asignación]** proporcionado durante la [programación de audiencias](#schedule-segment-export-example).
     ![Captura de pantalla de Salesforce CRM que muestra la página Detalles de contacto con estados de audiencia actualizados.](../../assets/catalog/crm/salesforce/contact-info.png)

   **Trabajando con posibles clientes**

   * Si ha seleccionado *posibles clientes* dentro del segmento de Platform, vaya a la página **[!DNL Apps]** > **[!DNL Leads]**.
     ![Captura de pantalla de Salesforce CRM que muestra la página de posibles clientes con los perfiles del segmento.](../../assets/catalog/crm/salesforce/leads.png)

   * Seleccione un *posible cliente* y compruebe si los campos están actualizados. Puede ver que cada estado de audiencia en [!DNL Salesforce CRM] se actualizó con el estado de audiencia correspondiente de Platform, según el valor de **[!UICONTROL ID de asignación]** proporcionado durante la [programación de audiencias](#schedule-segment-export-example).
     ![Captura de pantalla de Salesforce CRM que muestra la página Detalles del posible cliente con estados de audiencia actualizados.](../../assets/catalog/crm/salesforce/lead-info.png)

## Uso de datos y gobernanza {#data-usage-governance}

Todos los destinos de [!DNL Adobe Experience Platform] cumplen con las políticas de uso de datos al administrar los datos. Para obtener información detallada sobre cómo [!DNL Adobe Experience Platform] aplica el control de datos, consulte la [Información general sobre el control de datos](/help/data-governance/home.md).

## Errores y solución de problemas {#errors-and-troubleshooting}

### Se detectaron errores desconocidos al insertar eventos en el destino {#unknown-errors}

* Al comprobar la ejecución de un flujo de datos, puede que aparezca el siguiente mensaje de error: `Unknown errors encountered while pushing events to the destination. Please contact the administrator and try again.`
  ![Captura de pantalla de IU de Platform que muestra error.](../../assets/catalog/crm/salesforce/error.png)

   * Para corregir este error, compruebe que la **[!UICONTROL ID. de asignación]** proporcionada en el flujo de trabajo de activación para el destino [!DNL Salesforce CRM] coincide exactamente con el valor del tipo de campo personalizado que creó en [!DNL Salesforce]. Consulte la sección [Crear campos personalizados dentro de [!DNL Salesforce]](#prerequisites-custom-field) para obtener instrucciones.

* Al activar un segmento, podría obtener un mensaje de error: `The client's IP address is unauthorized for this account. Allowlist the client's IP address...`
   * Para corregir este error, póngase en contacto con el administrador de su cuenta de [!DNL Salesforce] para agregar [direcciones IP de Experience Platform](/help/destinations/catalog/streaming/ip-address-allow-list.md) a los intervalos de IP de confianza de sus cuentas de [!DNL Salesforce]. Consulte la documentación de [!DNL Salesforce] [Restringir el acceso a rangos de IP fiables para una aplicación conectada](https://help.salesforce.com/s/articleView?id=sf.connected_app_edit_ip_ranges.htm&amp;type=5) si necesita instrucciones adicionales.

## Recursos adicionales {#additional-resources}

A continuación encontrará información útil adicional del [Portal para desarrolladores de Salesforce](https://developer.salesforce.com/):
* [Introducción](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/quickstart.htm)
* [Crear un registro](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/dome_sobject_create.htm)
* [Audiencias de recomendaciones personalizadas](https://developer.salesforce.com/docs/atlas.en-us.236.0.chatterapi.meta/chatterapi/connect_resources_recommendation_audiences_list.htm)
* [Uso de recursos compuestos](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/using_composite_resources.htm?q=composite)
* Este destino aprovecha la API [Upsert Multiple Records](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/resources_composite_sobjects_collections_update.htm) en lugar de la llamada a la API [Upsert Single Record](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/dome_composite_upsert_example.htm?q=contacts).