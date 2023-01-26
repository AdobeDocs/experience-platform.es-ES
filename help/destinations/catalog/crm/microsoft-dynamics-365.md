---
keywords: crm;CRM;destinos crm;Microsoft Dynamics 365;destino crm de Microsoft Dynamics 365
title: Conexión de Microsoft Dynamics 365
description: El destino de Microsoft Dynamics 365 le permite exportar los datos de su cuenta y activarlos en Microsoft Dynamics 365 según sus necesidades comerciales.
last-substantial-update: 2022-11-08T00:00:00Z
exl-id: 49bb5c95-f4b7-42e1-9aae-45143bbb1d73
source-git-commit: 83778bc5d643f69e0393c0a7767fef8a4e8f66e9
workflow-type: tm+mt
source-wordcount: '1790'
ht-degree: 1%

---

# [!DNL Microsoft Dynamics 365] connection

## Información general {#overview}

[[!DNL Microsoft Dynamics 365]](https://dynamics.microsoft.com/en-us/) es una plataforma de aplicaciones empresariales basada en la nube que combina Enterprise Resource Planning (ERP) y Customer Relationship Management (CRM) junto con aplicaciones de productividad y herramientas de IA, para ofrecer operaciones integrales más fluidas y controladas, un mejor potencial de crecimiento y menores costos.

Esta [!DNL Adobe Experience Platform] [destino](/help/destinations/home.md) aprovecha el [[!DNL Contact Entity Reference API]](https://docs.microsoft.com/en-us/dynamics365/customerengagement/on-premises/developer/entities/contact?view=op-9-1), que le permite actualizar las identidades de un segmento en [!DNL Dynamics 365].

[!DNL Dynamics 365] utiliza OAuth 2 con la concesión de autorización como mecanismo de autenticación para comunicarse con el [!DNL Contact Entity Reference API]. Instrucciones para autenticarse en su [!DNL Dynamics 365] más abajo, en la [Autenticar en destino](#authenticate) para obtener más información.

## Casos de uso {#use-cases}

Como especialista en marketing, puede ofrecer experiencias personalizadas a los usuarios en función de los atributos de sus perfiles de Adobe Experience Platform. Puede generar segmentos a partir de los datos sin conexión y enviarlos a [!DNL Dynamics 365], para que se muestren en las fuentes de los usuarios en cuanto los segmentos y perfiles se actualicen en Adobe Experience Platform.

## Requisitos previos {#prerequisites}

### Requisitos previos del Experience Platform {#prerequisites-in-experience-platform}

Antes de activar los datos en la variable [!DNL Dynamics 365] destino, debe tener un [esquema](/help/xdm/schema/composition.md), [conjunto de datos](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=en)y [segmentos](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=en) creado en [!DNL Experience Platform].

Consulte la documentación del Adobe para [Grupo de campos de esquema Detalles de pertenencia a segmentos](/help/xdm/field-groups/profile/segmentation.md) si necesita instrucciones sobre los estados de los segmentos.

### [!DNL Microsoft Dynamics 365] requisitos previos {#prerequisites-destination}

Tenga en cuenta los siguientes requisitos previos en [!DNL Dynamics 365], para exportar datos de Platform a su [!DNL Dynamics 365] cuenta:

#### Debe tener un [!DNL Microsoft Dynamics 365] account {#prerequisites-account}

Vaya a la [!DNL Dynamics 365] [prueba](https://dynamics.microsoft.com/en-us/dynamics-365-free-trial/) para registrar y crear una cuenta, si todavía no la tiene.

#### Crear campo dentro de [!DNL Dynamics 365] {#prerequisites-custom-field}

Cree el campo personalizado de tipo `Simple` con tipo de datos de campo como `Single Line of Text` qué Experience Platform utilizará para actualizar el estado del segmento en [!DNL Dynamics 365].
Consulte la [!DNL Dynamics 365] documentación para [crear un campo (atributo)](https://docs.microsoft.com/en-us/dynamics365/customerengagement/on-premises/customize/create-edit-fields?view=op-9-1) si necesita más instrucciones.

Un ejemplo de configuración dentro de [!DNL Dynamics 365] se muestra a continuación:
![Captura de pantalla de la interfaz de usuario de Dynamics 365 que muestra los campos personalizados.](../../assets/catalog/crm/microsoft-dynamics-365/dynamics-365-fields.png)

#### Registrar un usuario de aplicación y aplicación en Azure Active Directory {#prerequisites-app-user}

Para habilitar [!DNL Dynamics 365] para acceder a los recursos, deberá iniciar sesión con su [!DNL Azure Account] a [[!DNL Azure Active Directory]](https://docs.microsoft.com/en-us/azure/active-directory/develop/howto-create-service-principal-portal#register-an-application-with-azure-ad-and-create-a-service-principal) y cree lo siguiente:
* Un [!DNL Azure Active Directory] aplicación
* Un servicio principal
* Un secreto de aplicación

También deberá [crear un usuario de aplicación](https://docs.microsoft.com/en-us/power-platform/admin/manage-application-users#create-an-application-user) en [!DNL Azure Active Directory] y asociarlo a la aplicación recién creada.

#### Recopilar [!DNL Dynamics 365] credenciales {#gather-credentials}

Tenga en cuenta los elementos siguientes antes de autenticarse en la variable [!DNL Dynamics 365] Destino de CRM:

| Credencial | Descripción | Ejemplo |
| --- | --- | --- |
| `Client ID` | La variable [!DNL Dynamics 365] ID de cliente para su [!DNL Azure Active Directory] aplicación. Consulte la [[!DNL Dynamics 365] documentación](https://docs.microsoft.com/en-us/azure/active-directory/develop/howto-create-service-principal-portal#get-tenant-and-app-id-values-for-signing-in) para obtener más información. | `ababbaba-abab-baba-acac-acacacacacac` |
| `Client Secret` | La variable [!DNL Dynamics 365] Secreto del cliente para su [!DNL Azure Active Directory] aplicación. Utilizaría la opción #2 dentro del [[!DNL Dynamics 365] documentación](https://docs.microsoft.com/en-us/azure/active-directory/develop/howto-create-service-principal-portal#authentication-two-options). | `abcde~abcdefghijklmnopqrstuvwxyz12345678` para obtener más información. |
| `Tenant ID` | La variable [!DNL Dynamics 365] ID del inquilino para su [!DNL Azure Active Directory] aplicación. Consulte la [[!DNL Dynamics 365] documentación](https://docs.microsoft.com/en-us/azure/active-directory/develop/howto-create-service-principal-portal#get-tenant-and-app-id-values-for-signing-in) para obtener más información. | `1234567-aaaa-12ab-ba21-1234567890` |
| `Environment URL` | Consulte la [[!DNL Dynamics 365] documentación](https://docs.microsoft.com/en-us/dynamics365/customerengagement/on-premises/developer/org-service/discover-url-organization-organization-service?view=op-9-1) para obtener más información. | Si su [!DNL Dynamics 365] es como se muestra a continuación, necesita el valor resaltado.<br> *`org57771b33`.crm.dynamics.com* |

## Límites de protección  {#guardrails}

La variable [Limitaciones de solicitudes y asignaciones](https://docs.microsoft.com/en-us/power-platform/admin/api-request-limits-allocations) detalles de la página [!DNL Dynamics 365] Límites de API asociados con su [!DNL Dynamics 365] licencia. Debe asegurarse de que los datos y la carga útil se encuentran dentro de estas restricciones.

## Identidades compatibles {#supported-identities}

[!DNL Dynamics 365] admite la actualización de identidades descritas en la siguiente tabla. Más información sobre [identidades](/help/identity-service/namespaces.md).

| Identidad de Target | Ejemplo | Descripción | Consideraciones |
|---|---|---|---|
| `contactId` | 7eb682f1-ca75-e511-80d4-00155d2a68d1 | Identificador único de un contacto. | **Obligatorio**. Consulte la [[!DNL Dynamics 365] documentación](https://docs.microsoft.com/en-us/dynamics365/customerengagement/on-premises/developer/entities/contact?view=op-9-1) para obtener más información. |

## Tipo de exportación y frecuencia {#export-type-frequency}

Consulte la tabla siguiente para obtener información sobre el tipo y la frecuencia de exportación de destino.

| Elemento | Tipo | Notas |
---------|----------|---------|
| Tipo de exportación | **[!UICONTROL Basado en perfiles]** | <ul><li>Está exportando todos los miembros de un segmento, junto con los campos de esquema deseados *(por ejemplo: dirección de correo electrónico, número de teléfono, apellidos)*, según la asignación de campos.</li><li> Cada estado de segmento en [!DNL Dynamics 365] se actualiza con el estado del segmento correspondiente de Platform, en función de la variable **[!UICONTROL ID de asignación]** valor proporcionado durante el [programación de segmentos](#schedule-segment-export-example) paso a paso.</li></ul> |
| Frecuencia de exportación | **[!UICONTROL Transmisión]** | <ul><li>Los destinos de flujo continuo son conexiones basadas en API &quot;siempre activadas&quot;. Tan pronto como un perfil se actualiza en el Experience Platform en función de la evaluación de segmentos, el conector envía la actualización descendente a la plataforma de destino. Más información sobre [destinos de flujo continuo](/help/destinations/destination-types.md#streaming-destinations).</li></ul> |

{style=&quot;table-layout:auto&quot;}

## Conectarse al destino {#connect}

>[!IMPORTANT]
>
>Para conectarse al destino, necesita la variable **[!UICONTROL Administrar destinos]** [permiso de control de acceso](/help/access-control/home.md#permissions). Lea el [información general sobre el control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Para conectarse a este destino, siga los pasos descritos en la sección [tutorial de configuración de destino](../../ui/connect-destination.md). En el flujo de trabajo de configuración de destino, rellene los campos que aparecen en las dos secciones siguientes.

Within **[!UICONTROL Destinos]** > **[!UICONTROL Catálogo]** buscar [!DNL Dynamics 365]. También puede localizarlo en la sección **[!UICONTROL CRM]** categoría.

### Autenticar en destino {#authenticate}

Para autenticarse en el destino, seleccione **[!UICONTROL Conectarse al destino]**.
![Captura de pantalla de la interfaz de usuario de Platform que muestra cómo autenticarse.](../../assets/catalog/crm/microsoft-dynamics-365/authenticate-destination.png)

Complete los campos obligatorios a continuación. Consulte la [Recopilar credenciales de Dynamics 365](#gather-credentials) para obtener más información.
* **[!UICONTROL ID de cliente]**: La variable [!DNL Dynamics 365] ID de cliente para su [!DNL Azure Active Directory] aplicación.
* **[!UICONTROL ID del inquilino]**: La variable [!DNL Dynamics 365] ID del inquilino para su [!DNL Azure Active Directory] aplicación.
* **[!UICONTROL Secreto del cliente]**: La variable [!DNL Dynamics 365] Secreto del cliente para su [!DNL Azure Active Directory] aplicación.
* **[!UICONTROL URL del entorno]**: Su [!DNL Dynamics 365] URL de entorno.

Si los detalles proporcionados son válidos, la interfaz de usuario muestra un **[!UICONTROL Conectado]** con una marca de verificación verde. A continuación, puede continuar con el paso siguiente.

### Rellenar detalles de destino {#destination-details}

Para configurar los detalles del destino, rellene los campos opcionales y requeridos a continuación. Un asterisco junto a un campo en la interfaz de usuario indica que el campo es obligatorio.
![Captura de pantalla de la interfaz de usuario de Platform que muestra los detalles del destino.](../../assets/catalog/crm/microsoft-dynamics-365/destination-details.png)

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

Para enviar correctamente los datos de audiencia de Adobe Experience Platform a [!DNL Dynamics 365] destino, debe pasar por el paso de asignación de campos. La asignación consiste en la creación de un vínculo entre los campos de esquema del Modelo de datos de experiencia (XDM) en la cuenta de Platform y sus equivalentes correspondientes desde el destino de destino. Para asignar correctamente los campos XDM a la variable [!DNL Dynamics 365] campos de destino, siga estos pasos:

1. En el **[!UICONTROL Asignación]** paso, seleccione **[!UICONTROL Añadir nueva asignación]**. Verá una nueva fila de asignación en la pantalla.
   ![Ejemplo de captura de pantalla de la interfaz de usuario de Platform para Añadir nueva asignación.](../../assets/catalog/crm/microsoft-dynamics-365/add-new-mapping.png)

1. En el **[!UICONTROL Seleccionar campo de origen]** , seleccione **[!UICONTROL Seleccionar área de nombres de identidad]** categoría y seleccione `contactId`.
   ![Ejemplo de captura de pantalla de la interfaz de usuario de Platform para la asignación de origen.](../../assets/catalog/crm/microsoft-dynamics-365/source-mapping.png)

1. En el **[!UICONTROL Seleccionar campo de destino]** , seleccione el tipo de campo de destino al que desea asignar el campo de origen.
   * **[!UICONTROL Seleccionar área de nombres de identidad]**: seleccione esta opción para asignar el campo de origen a un área de nombres de identidad de la lista.
      ![Captura de pantalla de la interfaz de usuario de Platform que muestra la asignación de Target para contactId.](../../assets/catalog/crm/microsoft-dynamics-365/target-mapping-contactid.png)

   * Añada la siguiente asignación entre el esquema de perfil XDM y el [!DNL Dynamics 365] instancia: |Esquema de perfil XDM|[!DNL Dynamics 365] Instancia| Obligatoria| |—|—|—| |`contactId`|`contactId`| Sí |

   * **[!UICONTROL Seleccionar atributos personalizados]**: seleccione esta opción para asignar el campo de origen a un atributo personalizado que defina en la variable **[!UICONTROL Nombre del atributo]** campo . Consulte [[!DNL Dynamics 365] documentación](https://docs.microsoft.com/en-us/dynamics365/customerengagement/on-premises/developer/entities/contact?view=op-9-1#entity-properties) para obtener una lista completa de los atributos admitidos.
      ![Captura de pantalla de la interfaz de usuario de Platform que muestra la asignación de Target para LastName.](../../assets/catalog/crm/microsoft-dynamics-365/target-mapping-lastname.png)

      >[!IMPORTANT]
      >
      >Si tiene un campo de origen de fecha o marca de tiempo asignado a una [!DNL Dynamics 365] [fecha o marca de hora](https://docs.microsoft.com/en-us/power-apps/developer/data-platform/webapi/reference/timestampdatemapping?view=dataverse-latest) campo de destino, asegúrese de que el valor asignado no esté vacío. Si el valor pasado está vacío, aparecerá un *`Bad request reported while pushing events to the destination. Please contact the administrator and try again.`* y los datos no se actualizarán. Esto es un [!DNL Dynamics 365] limitación.

   * Por ejemplo, según los valores que desee actualizar, agregue la siguiente asignación entre el esquema de perfil XDM y el [!DNL Dynamics 365] instancia: |Esquema de perfil XDM|[!DNL Dynamics 365] Instancia| |—|—| |`person.name.firstName`|`FirstName`| |`person.name.lastName`|`LastName`| |`personalEmail.address`|`Email`|

   * A continuación se muestra un ejemplo con estas asignaciones:
      ![Captura de pantalla de la interfaz de usuario de Platform que muestra asignaciones de Target.](../../assets/catalog/crm/microsoft-dynamics-365/mappings.png)

### Programar exportación de segmentos y ejemplo {#schedule-segment-export-example}

En el [[!UICONTROL Programar exportación de segmentos]](/help/destinations/ui/activate-segment-streaming-destinations.md#scheduling) paso del flujo de trabajo de activación, debe asignar manualmente los segmentos de Platform al atributo de campo personalizado en [!DNL Dynamics 365].

Para ello, seleccione cada segmento e introduzca el atributo de campo personalizado correspondiente en [!DNL Dynamics 365] en el **[!UICONTROL ID de asignación]** campo .

>[!IMPORTANT]
>
>El valor utilizado para la variable **[!UICONTROL ID de asignación]** debe coincidir exactamente con el nombre del atributo de campo personalizado creado en [!DNL Dynamics 365]. Consulte [[!DNL Dynamics 365] documentación](https://docs.microsoft.com/en-us/dynamics365/customerengagement/on-premises/customize/create-edit-fields?view=op-9-1) si necesita instrucciones para encontrar los atributos de campo personalizados.

A continuación se muestra un ejemplo:
![Captura de pantalla de la interfaz de usuario de Platform que muestra Programar exportación de segmentos.](../../assets/catalog/crm/microsoft-dynamics-365/schedule-segment-export.png)

## Validación de la exportación de datos {#exported-data}

Para validar que ha configurado correctamente el destino, siga los pasos a continuación:

1. Select **[!UICONTROL Destinos]** > **[!UICONTROL Examinar]** para navegar a la lista de destinos.
   ![Captura de pantalla de la interfaz de usuario de Platform que muestra los destinos de exploración.](../../assets/catalog/crm/microsoft-dynamics-365/browse-destinations.png)

1. Seleccione el destino y valide que el estado es **[!UICONTROL enabled]**.
   ![Captura de pantalla de la interfaz de usuario de Platform que muestra la ejecución del flujo de datos de Destinations.](../../assets/catalog/crm/microsoft-dynamics-365/destination-dataflow-run.png)

1. Cambie a la **[!DNL Activation data]** y, a continuación, seleccione un nombre de segmento.
   ![Captura de pantalla de la interfaz de usuario de Platform que muestra los datos de activación de destinos.](../../assets/catalog/crm/microsoft-dynamics-365/destinations-activation-data.png)

1. Monitorice el resumen del segmento y asegúrese de que el recuento de perfiles corresponde al recuento creado dentro del segmento.
   ![Captura de pantalla de la interfaz de usuario de Platform que muestra el segmento.](../../assets/catalog/crm/microsoft-dynamics-365/segment.png)

1. Inicie sesión en la [!DNL Dynamics 365] sitio web y, a continuación, vaya a la [!DNL Customers] > [!DNL Contacts] y compruebe si se han añadido los perfiles del segmento. Puede ver cada estado de segmento en [!DNL Dynamics 365] se actualizó con el estado del segmento correspondiente de Platform, en función de la variable **[!UICONTROL ID de asignación]** valor proporcionado durante el [programación de segmentos](#schedule-segment-export-example) paso a paso.
   ![Captura de pantalla de la interfaz de usuario de Dynamics 365 que muestra la página Contactos con estados de segmento actualizados.](../../assets/catalog/crm/microsoft-dynamics-365/contacts.png)

## Uso y gobernanza de los datos {#data-usage-governance}

Todo [!DNL Adobe Experience Platform] Los destinos de cumplen las políticas de uso de datos al administrar los datos. Para obtener información detallada sobre cómo [!DNL Adobe Experience Platform] exige el control de datos; consulte [Información general sobre la administración de datos](/help/data-governance/home.md).

## Errores y solución de problemas {#errors-and-troubleshooting}

### Se han encontrado errores desconocidos al insertar eventos en el destino {#unknown-errors}

Al comprobar la ejecución de un flujo de datos, si obtiene el siguiente mensaje de error: `Bad request reported while pushing events to the destination. Please contact the administrator and try again.`

![Captura de pantalla de la interfaz de usuario de Platform que muestra un error de solicitud incorrecto.](../../assets/catalog/crm/microsoft-dynamics-365/error.png)

Para solucionar este error, compruebe que la variable **[!UICONTROL ID de asignación]** ha proporcionado [!DNL Dynamics 365] para su segmento de Platform es válido y existe dentro de [!DNL Dynamics 365].

## Recursos adicionales {#additional-resources}

Información útil adicional de [[!DNL Dynamics 365] documentación](https://docs.microsoft.com/en-us/dynamics365/) a continuación:
* [IOrOrganizationService.Update(Entity) (método)](https://docs.microsoft.com/en-us/dotnet/api/microsoft.xrm.sdk.iorganizationservice.update?view=dataverse-sdk-latest)
* [Actualizar y eliminar filas de tabla mediante la API web](https://docs.microsoft.com/en-us/power-apps/developer/data-platform/webapi/update-delete-entities-using-web-api#basic-update)
