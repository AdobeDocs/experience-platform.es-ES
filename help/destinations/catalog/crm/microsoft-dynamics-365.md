---
keywords: crm;CRM;destinos de crm;Microsoft Dynamics 365;destino de crm de Microsoft Dynamics 365
title: Conexión de Microsoft Dynamics 365
description: El destino de Microsoft Dynamics 365 le permite exportar los datos de su cuenta y activarlos en Microsoft Dynamics 365 para sus necesidades comerciales.
last-substantial-update: 2022-11-08T00:00:00Z
exl-id: 49bb5c95-f4b7-42e1-9aae-45143bbb1d73
source-git-commit: ba39f62cd77acedb7bfc0081dbb5f59906c9b287
workflow-type: tm+mt
source-wordcount: '2019'
ht-degree: 1%

---

# [!DNL Microsoft Dynamics 365] conexión

## Información general {#overview}

[[!DNL Microsoft Dynamics 365]](https://dynamics.microsoft.com/en-us/) es una plataforma de aplicaciones empresariales basada en la nube que combina Planificación de recursos empresariales (ERP) y Administración de relaciones con el cliente (CRM) junto con aplicaciones de productividad y herramientas de IA, para ofrecer operaciones de extremo a extremo más suaves y controladas, un mejor potencial de crecimiento y costes reducidos.

Este [!DNL Adobe Experience Platform] [destino](/help/destinations/home.md) aprovecha [[!DNL Contact Entity Reference API]](https://docs.microsoft.com/en-us/dynamics365/customerengagement/on-premises/developer/entities/contact?view=op-9-1), lo que le permite actualizar identidades dentro de una audiencia en [!DNL Dynamics 365].

[!DNL Dynamics 365] utiliza OAuth 2 con concesión de autorización como mecanismo de autenticación para comunicarse con [!DNL Contact Entity Reference API]. Las instrucciones para autenticarse en su instancia de [!DNL Dynamics 365] se encuentran más abajo, en la sección [Autenticar en destino](#authenticate).

## Casos de uso {#use-cases}

Como experto en marketing, puede ofrecer experiencias personalizadas a los usuarios en función de los atributos de sus perfiles de Adobe Experience Platform. Puede generar audiencias a partir de los datos sin conexión y enviarlas a [!DNL Dynamics 365] para que se muestren en las fuentes de los usuarios en cuanto las audiencias y los perfiles se actualicen en Adobe Experience Platform.

## Requisitos previos {#prerequisites}

### Requisitos previos del Experience Platform {#prerequisites-in-experience-platform}

Antes de activar datos en el destino [!DNL Dynamics 365], debe tener un [esquema](/help/xdm/schema/composition.md), un [conjunto de datos](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html) y [audiencias](https://experienceleague.adobe.com/docs/platform-learn/tutorials/audiences/create-audiences.html) creados en [!DNL Experience Platform].

Consulte la documentación de Adobe para el [grupo de campos de esquema Detalles de pertenencia a audiencias](/help/xdm/field-groups/profile/segmentation.md) si necesita instrucciones sobre los estados de audiencia.

### [!DNL Microsoft Dynamics 365] requisitos previos {#prerequisites-destination}

Tenga en cuenta los siguientes requisitos previos de [!DNL Dynamics 365] para exportar datos de Platform a su cuenta de [!DNL Dynamics 365]:

#### Necesita tener una cuenta de [!DNL Microsoft Dynamics 365] {#prerequisites-account}

Vaya a la página [!DNL Dynamics 365] [prueba](https://dynamics.microsoft.com/en-us/dynamics-365-free-trial/) para registrarse y crear una cuenta, si todavía no la tiene.

#### Crear campo dentro de [!DNL Dynamics 365] {#prerequisites-custom-field}

Cree el campo personalizado de tipo `Simple` con el tipo de datos de campo `Single Line of Text` que el Experience Platform utilizará para actualizar el estado de la audiencia en [!DNL Dynamics 365].

Consulte la documentación de [!DNL Dynamics 365] [Crear o editar un campo (atributo)](https://docs.microsoft.com/en-us/dynamics365/customerengagement/on-premises/customize/create-edit-fields?view=op-9-1) si necesita instrucciones adicionales.

Anote el **[!UICONTROL prefijo de personalización]** del campo personalizado que crea en [!DNL Dynamics 365]. Necesitará este prefijo durante el paso [Rellenar detalles de destino](#destination-details). Consulte la sección [Crear y editar campos](https://learn.microsoft.com/en-us/dynamics365/customerengagement/on-premises/customize/create-edit-fields?view=op-9-1#create-and-edit-fields) de la documentación de [!DNL Dynamics 365] para obtener más información.
![Captura de pantalla de la interfaz de usuario de Dynamics 365 que muestra el prefijo de personalización.](../../assets/catalog/crm/microsoft-dynamics-365/dynamics-365-customization-prefix.png)

A continuación se muestra un ejemplo de configuración en [!DNL Dynamics 365]:
![Captura de pantalla de la interfaz de usuario de Dynamics 365 que muestra los campos personalizados.](../../assets/catalog/crm/microsoft-dynamics-365/dynamics-365-fields.png)

#### Registrar una aplicación y un usuario de aplicación en Azure Active Directory {#prerequisites-app-user}

Para permitir que [!DNL Dynamics 365] acceda a los recursos, deberá iniciar sesión con su [!DNL Azure Account] en [[!DNL Azure Active Directory]](https://docs.microsoft.com/en-us/azure/active-directory/develop/howto-create-service-principal-portal#register-an-application-with-azure-ad-and-create-a-service-principal) y crear lo siguiente:
* Una aplicación [!DNL Azure Active Directory]
* Una entidad de servicio
* Un secreto de aplicación

También necesitará [crear un usuario de aplicación](https://docs.microsoft.com/en-us/power-platform/admin/manage-application-users#create-an-application-user) en [!DNL Azure Active Directory] y asociarlo con la aplicación recién creada.

#### Recopilar [!DNL Dynamics 365] credenciales {#gather-credentials}

Tenga en cuenta los elementos siguientes antes de autenticarse en el destino de CRM [!DNL Dynamics 365]:

| Credencial | Descripción | Ejemplo |
| --- | --- | --- |
| `Client ID` | Identificador de cliente [!DNL Dynamics 365] para su aplicación [!DNL Azure Active Directory]. Consulte la [[!DNL Dynamics 365] documentación](https://docs.microsoft.com/en-us/azure/active-directory/develop/howto-create-service-principal-portal#get-tenant-and-app-id-values-for-signing-in) para obtener instrucciones. | `ababbaba-abab-baba-acac-acacacacacac` |
| `Client Secret` | Secreto de cliente [!DNL Dynamics 365] para su aplicación [!DNL Azure Active Directory]. Utilizaría la opción #2 en la [[!DNL Dynamics 365] documentación](https://docs.microsoft.com/en-us/azure/active-directory/develop/howto-create-service-principal-portal#authentication-two-options). | `abcde~abcdefghijklmnopqrstuvwxyz12345678` como guía. |
| `Tenant ID` | Identificador de inquilino [!DNL Dynamics 365] para su aplicación [!DNL Azure Active Directory]. Consulte la [[!DNL Dynamics 365] documentación](https://docs.microsoft.com/en-us/azure/active-directory/develop/howto-create-service-principal-portal#get-tenant-and-app-id-values-for-signing-in) para obtener instrucciones. | `1234567-aaaa-12ab-ba21-1234567890` |
| `Region` | La región de Microsoft asociada a la URL del entorno.<br> Consulte la [[!DNL Dynamics 365] documentación](https://learn.microsoft.com/en-us/power-platform/admin/new-datacenter-regions) para obtener instrucciones. | Si su dominio es como se muestra a continuación, debe proporcionar el valor resaltado para el campo CRM en el selector desplegable al autenticarse en [destino](#authenticate).<br> *org57771b33.`crm`.dynamics.com*<br> Por ejemplo: Si su compañía está aprovisionada en la región de Norteamérica (NAM), su dirección URL sería `crm.dynamics.com` y debe seleccionar `crm`. Si su empresa está aprovisionada en la región de Canadá (CAN), su dirección URL sería `crm3.dynamics.com` y necesita seleccionar `crm3`. |
| `Environment URL` | Consulte la [[!DNL Dynamics 365] documentación](https://docs.microsoft.com/en-us/dynamics365/customerengagement/on-premises/developer/org-service/discover-url-organization-organization-service?view=op-9-1) para obtener instrucciones. | Si el dominio [!DNL Dynamics 365] es como se muestra a continuación, necesita el valor resaltado.<br> *`org57771b33`.crm.dynamics.com* |

{style="table-layout:auto"}

## Mecanismos de protección {#guardrails}

La página [Límites de solicitudes y asignaciones](https://docs.microsoft.com/en-us/power-platform/admin/api-request-limits-allocations) detalla los límites de API [!DNL Dynamics 365] asociados con su licencia de [!DNL Dynamics 365]. Debe asegurarse de que los datos y la carga útil se encuentren dentro de estas restricciones.

## Identidades admitidas {#supported-identities}

[!DNL Dynamics 365] admite la actualización de las identidades descritas en la tabla siguiente. Más información sobre [identidades](/help/identity-service/features/namespaces.md).

| Identidad de destino | Ejemplo | Descripción | Consideraciones |
|---|---|---|---|
| `contactid` | 7eb682f1-ca75-e511-80d4-00155d2a68d1 | Identificador único de un contacto. | **Obligatorio**. Consulte la [[!DNL Dynamics 365] documentación](https://docs.microsoft.com/en-us/dynamics365/customerengagement/on-premises/developer/entities/contact?view=op-9-1) para obtener más información. |

{style="table-layout:auto"}

## Audiencias compatibles {#supported-audiences}

Esta sección describe todas las audiencias que puede exportar a este destino.

Este destino admite la activación de todas las audiencias generadas a través del Experience Platform [Servicio de segmentación](../../../segmentation/home.md).

## Tipo y frecuencia de exportación {#export-type-frequency}

Consulte la tabla siguiente para obtener información sobre el tipo y la frecuencia de exportación de destino.

| Elemento | Tipo | Notas |
---------|----------|---------|
| Tipo de exportación | **[!UICONTROL Basado en perfil]** | <ul><li>Va a exportar todos los miembros de una audiencia, junto con los campos de esquema deseados *(por ejemplo: dirección de correo electrónico, número de teléfono, apellidos)*, según la asignación de campos.</li><li> Cada estado de audiencia de [!DNL Dynamics 365] se actualiza con el estado de audiencia correspondiente de Platform, según el valor de **[!UICONTROL ID de asignación]** proporcionado durante el paso [programación de audiencia](#schedule-audience-export-example).</li></ul> |
| Frecuencia de exportación | **[!UICONTROL Transmisión]** | <ul><li>Los destinos de streaming son conexiones basadas en API &quot;siempre activadas&quot;. Tan pronto como se actualiza un perfil en Experience Platform según la evaluación de audiencias, el conector envía la actualización de forma descendente a la plataforma de destino. Más información sobre [destinos de streaming](/help/destinations/destination-types.md#streaming-destinations).</li></ul> |

{style="table-layout:auto"}

## Conexión al destino {#connect}

>[!IMPORTANT]
>
>Para conectarse al destino, necesita los **[!UICONTROL permisos de control de acceso](/help/access-control/home.md#permissions) de Ver destinos]** y **[!UICONTROL Administrar destinos]**[5}. Lea la [descripción general del control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Para conectarse a este destino, siga los pasos descritos en el [tutorial de configuración de destino](../../ui/connect-destination.md). En el flujo de trabajo de configuración de destino, rellene los campos enumerados en las dos secciones siguientes.

En **[!UICONTROL destinos]** > **[!UICONTROL catálogo]**, busque [!DNL Dynamics 365]. También puede ubicarlo en la categoría **[!UICONTROL CRM]**.

### Autenticarse en el destino {#authenticate}

Para autenticarse en el destino, seleccione **[!UICONTROL Conectarse al destino]**.
![Captura de pantalla de IU de Platform que muestra cómo autenticarse.](../../assets/catalog/crm/microsoft-dynamics-365/authenticate-destination.png)

Rellene los campos obligatorios siguientes. Consulte la sección [Recopilar credenciales de Dynamics 365](#gather-credentials) para obtener instrucciones.
* **[!UICONTROL ID de cliente]**: El ID de cliente [!DNL Dynamics 365] para su aplicación [!DNL Azure Active Directory].
* **[!UICONTROL ID de inquilino]**: El ID de inquilino de [!DNL Dynamics 365] para su aplicación de [!DNL Azure Active Directory].
* **[!UICONTROL Secreto de cliente]**: El secreto de cliente [!DNL Dynamics 365] para su aplicación [!DNL Azure Active Directory].
* **[!UICONTROL Región]**: Tu Región [[!DNL Dynamics 365]](https://learn.microsoft.com/en-us/power-platform/admin/new-datacenter-regions). Por ejemplo: si su empresa está aprovisionada en la región de América del Norte (NAM), su dirección URL sería `crm.dynamics.com` y debe seleccionar `crm`. Si su empresa está aprovisionada en la región de Canadá (CAN), su dirección URL sería `crm3.dynamics.com` y necesita seleccionar `crm3`.
* **[!UICONTROL URL de entorno]**: La URL de entorno [!DNL Dynamics 365].

Si los detalles proporcionados son válidos, la interfaz de usuario mostrará el estado **[!UICONTROL Conectado]** con una marca de verificación verde. A continuación, puede continuar con el paso siguiente.

### Rellenar detalles de destino {#destination-details}

Para configurar los detalles del destino, rellene los campos obligatorios y opcionales a continuación. Un asterisco junto a un campo en la interfaz de usuario indica que el campo es obligatorio.
![Captura de pantalla de IU de Platform que muestra los detalles del destino.](../../assets/catalog/crm/microsoft-dynamics-365/destination-details.png)

* **[!UICONTROL Nombre]**: Un nombre por el cual reconocerá este destino en el futuro.
* **[!UICONTROL Descripción]**: Una descripción que le ayudará a identificar este destino en el futuro.
* **[!UICONTROL Prefijo de personalización]**: El `Customization prefix` del campo personalizado que creó en [!DNL Dynamics 365]. Consulte la sección [Crear y editar campos](https://learn.microsoft.com/en-us/dynamics365/customerengagement/on-premises/customize/create-edit-fields?view=op-9-1#create-and-edit-fields) de la documentación de [!DNL Dynamics 365] para obtener más información.

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

Para enviar correctamente los datos de audiencia de Adobe Experience Platform al destino [!DNL Dynamics 365], debe pasar por el paso de asignación de campos. La asignación consiste en crear un vínculo entre los campos de esquema del Modelo de datos de experiencia (XDM) en la cuenta de Platform y sus equivalentes correspondientes desde el destino de destino. Para asignar correctamente los campos XDM a los campos de destino [!DNL Dynamics 365], siga estos pasos:

1. En el paso **[!UICONTROL Asignación]**, seleccione **[!UICONTROL Agregar nueva asignación]**. Verá una nueva fila de asignación en la pantalla.
   ![Ejemplo de captura de pantalla de IU de Platform para agregar nueva asignación.](../../assets/catalog/crm/microsoft-dynamics-365/add-new-mapping.png)

1. En la ventana **[!UICONTROL Seleccionar campo de origen]**, elija la categoría **[!UICONTROL Seleccionar área de nombres de identidad]** y seleccione `contactid`.
   ![Ejemplo de captura de pantalla de IU de Platform para asignación de Source.](../../assets/catalog/crm/microsoft-dynamics-365/source-mapping.png)

1. En la ventana **[!UICONTROL Seleccionar campo de destino]**, seleccione el tipo de campo de destino al que desea asignar el campo de origen.
   * **[!UICONTROL Seleccionar área de nombres de identidad]**: seleccione esta opción para asignar el campo de origen a un área de nombres de identidad de la lista.
     ![Captura de pantalla de IU de Platform que muestra la asignación de Target para contactid.](../../assets/catalog/crm/microsoft-dynamics-365/target-mapping-contactid.png)

   * Agregue la siguiente asignación entre su esquema de perfil XDM y su instancia [!DNL Dynamics 365]:
|Esquema de perfil XDM|[!DNL Dynamics 365] instancia| Obligatorio|
|—|—|—|
|`contactid`|`contactid`| Sí |

   * **[!UICONTROL Seleccionar atributos personalizados]**: seleccione esta opción para asignar el campo de origen a un atributo personalizado que defina en el campo **[!UICONTROL Nombre de atributo]**. Consulte [[!DNL Dynamics 365] documentación](https://docs.microsoft.com/en-us/dynamics365/customerengagement/on-premises/developer/entities/contact?view=op-9-1#entity-properties) para obtener una lista completa de los atributos admitidos.
     ![Captura de pantalla de IU de Platform que muestra la asignación de destino para correo electrónico.](../../assets/catalog/crm/microsoft-dynamics-365/target-mapping-email.png)

     >[!IMPORTANT]
     >
     > * Los nombres de los campos de destino deben estar en `lowercase`.
     > * Además, si tiene un campo de origen de fecha u hora asignado a un campo de destino [!DNL Dynamics 365] [fecha o marca de hora](https://docs.microsoft.com/en-us/power-apps/developer/data-platform/webapi/reference/timestampdatemapping?view=dataverse-latest), asegúrese de que el valor asignado no esté vacío. Si el valor del campo exportado está vacío, aparecerá un mensaje de error *`Bad request reported while pushing events to the destination. Please contact the administrator and try again.`* y los datos no se actualizarán. Esta es una limitación de [!DNL Dynamics 365].

   * Por ejemplo, según los valores que desee actualizar, agregue la siguiente asignación entre el esquema de perfil XDM y la instancia [!DNL Dynamics 365]:
|Esquema de perfil XDM|[!DNL Dynamics 365] instancia|
|—|—|
|`person.name.firstName`|`firstname`|
|`person.name.lastName`|`lastname`|
|`personalEmail.address`|`emailaddress1`|

   * A continuación se muestra un ejemplo con estas asignaciones:
     ![Ejemplo de captura de pantalla de IU de Platform que muestra asignaciones de Target.](../../assets/catalog/crm/microsoft-dynamics-365/mappings.png)

### Programar exportación de audiencias y ejemplo {#schedule-audience-export-example}

En el paso [[!UICONTROL Programar exportación de audiencias]](/help/destinations/ui/activate-segment-streaming-destinations.md#scheduling) del flujo de trabajo de activación, debe asignar manualmente las audiencias de Platform al atributo de campo personalizado en [!DNL Dynamics 365].

Para ello, seleccione cada audiencia e introduzca el atributo de campo personalizado correspondiente de [!DNL Dynamics 365] en el campo **[!UICONTROL ID de asignación]**.

>[!IMPORTANT]
>
>El valor usado para **[!UICONTROL ID de asignación]** debe coincidir exactamente con el nombre del atributo de campo personalizado creado en [!DNL Dynamics 365]. Consulte [[!DNL Dynamics 365] documentación](https://docs.microsoft.com/en-us/dynamics365/customerengagement/on-premises/customize/create-edit-fields?view=op-9-1) si necesita ayuda para encontrar los atributos de sus campos personalizados.

A continuación se muestra un ejemplo:
![Ejemplo de captura de pantalla de la IU de Platform que muestra Programar exportación de audiencias.](../../assets/catalog/crm/microsoft-dynamics-365/schedule-segment-export.png)

## Validar exportación de datos {#exported-data}

Para comprobar que ha configurado correctamente el destino, siga los pasos a continuación:

1. Seleccione **[!UICONTROL Destinos]** > **[!UICONTROL Examinar]** para navegar a la lista de destinos.
   ![Captura de pantalla de IU que muestra destinos de exploración.](../../assets/catalog/crm/microsoft-dynamics-365/browse-destinations.png)

1. Seleccione el destino y valide que el estado es **[!UICONTROL enabled]**.
   ![Captura de pantalla de IU de Platform que muestra la ejecución del flujo de datos de destinos.](../../assets/catalog/crm/microsoft-dynamics-365/destination-dataflow-run.png)

1. Cambie a la ficha **[!DNL Activation data]** y, a continuación, seleccione un nombre de audiencia.
   ![Ejemplo de captura de pantalla de IU de Platform que muestra datos de activación de destinos.](../../assets/catalog/crm/microsoft-dynamics-365/destinations-activation-data.png)

1. Monitorice el resumen de audiencia y asegúrese de que el recuento de perfiles corresponde al recuento creado dentro de la audiencia.
   ![Ejemplo de captura de pantalla de IU de Platform que muestra la audiencia.](../../assets/catalog/crm/microsoft-dynamics-365/segment.png)

1. Inicie sesión en el sitio web de [!DNL Dynamics 365], luego vaya a la página [!DNL Customers] > [!DNL Contacts] y compruebe si se han agregado los perfiles de la audiencia. Puede ver que cada estado de audiencia en [!DNL Dynamics 365] se actualizó con el estado de audiencia correspondiente de Platform, según el valor de **[!UICONTROL ID de asignación]** proporcionado durante el paso [programación de audiencia](#schedule-audience-export-example).
   ![Captura de pantalla de la interfaz de usuario de Dynamics 365 que muestra la página Contactos con estados de audiencia actualizados.](../../assets/catalog/crm/microsoft-dynamics-365/contacts.png)

## Uso de datos y gobernanza {#data-usage-governance}

Todos los destinos de [!DNL Adobe Experience Platform] cumplen con las políticas de uso de datos al administrar los datos. Para obtener información detallada sobre cómo [!DNL Adobe Experience Platform] aplica el control de datos, consulte la [Información general sobre el control de datos](/help/data-governance/home.md).

## Errores y solución de problemas {#errors-and-troubleshooting}

### Se detectaron errores desconocidos al insertar eventos en el destino {#unknown-errors}

Al comprobar la ejecución de un flujo de datos, si obtiene el siguiente mensaje de error: `Bad request reported while pushing events to the destination. Please contact the administrator and try again.`

![Captura de pantalla de IU de plataforma que muestra error de solicitud incorrecto.](../../assets/catalog/crm/microsoft-dynamics-365/error.png)

Para corregir este error, compruebe que la **[!UICONTROL ID de asignación]** que ha proporcionado en [!DNL Dynamics 365] para la audiencia de Platform sea válida y exista en [!DNL Dynamics 365].

## Recursos adicionales {#additional-resources}

A continuación encontrará información útil adicional de la [[!DNL Dynamics 365] documentación](https://docs.microsoft.com/en-us/dynamics365/):
* [Método IOrganizationService.Update(Entity)](https://docs.microsoft.com/en-us/dotnet/api/microsoft.xrm.sdk.iorganizationservice.update?view=dataverse-sdk-latest)
* [Actualizar y eliminar filas de tabla mediante la API web](https://docs.microsoft.com/en-us/power-apps/developer/data-platform/webapi/update-delete-entities-using-web-api#basic-update)

### Changelog

Esta sección recoge la funcionalidad y las actualizaciones significativas de la documentación realizadas en este conector de destino.

+++ Ver registro de cambios

| Mes de lanzamiento | Tipo de actualización | Descripción |
|---|---|---|
| Octubre de 2023 | Actualización de documentación | Se ha actualizado la guía para indicar que todos los nombres de atributos de destino deben estar en minúsculas, en el paso [Consideraciones de asignación y ejemplo](#mapping-considerations-example). |
| Agosto de 2023 | Actualización de funcionalidad y documentación | Se agregó compatibilidad con [!DNL Dynamics 365] prefijos de campo personalizados para campos personalizados que no se crearon dentro de la solución predeterminada en [!DNL Dynamics 365]. Se ha agregado un nuevo campo de entrada **[!UICONTROL Prefijo de personalización]** en el paso [Rellenar detalles de destino](#destination-details). (PLATIR-31602). |
| Noviembre de 2022 | Versión inicial | Versión de destino inicial y publicación de documentación. |

{style="table-layout:auto"}

+++