---
keywords: crm;CRM;destinos de crm;Extensión;Destino de extensiones crm
title: Conexión de extensión
description: El destino de Extensión le permite exportar los datos de su cuenta y activarlos dentro de Extensión para sus necesidades comerciales.
source-git-commit: 27da0f8d7896fd32e8a1b828630db7e5e08185c2
workflow-type: tm+mt
source-wordcount: '1714'
ht-degree: 1%

---


# [!DNL Outreach] connection

## Información general {#overview}

[[!DNL Outreach]](https://www.outreach.io/) es una plataforma de ejecución de ventas con la mayor cantidad de datos de interacción entre compradores y vendedores entre B2B en el mundo y con importantes inversiones en tecnologías de IA propietarias para traducir los datos de ventas a inteligencia. [!DNL Outreach] ayuda a las organizaciones a automatizar la participación de ventas y a utilizar la inteligencia de ingresos para mejorar su eficiencia, previsibilidad y crecimiento.

Esta [!DNL Adobe Experience Platform] [destino](/help/destinations/home.md) aprovecha el [API de recursos de actualización de extensión](https://api.outreach.io/api/v2/docs#update-an-existing-resource), que le permite actualizar las identidades de un segmento correspondiente a los posibles clientes en [!DNL Outreach].

[!DNL Outreach] utiliza OAuth 2 con la concesión de autorización como mecanismo de autenticación para comunicarse con el [!DNL Outreach] [!DNL Update Resource API]. Instrucciones para autenticarse en su [!DNL Outreach] más abajo, dentro de [Autenticar en destino](#authenticate) para obtener más información.

## Casos de uso {#use-cases}

Como especialista en marketing, puede ofrecer experiencias personalizadas a sus posibles clientes en función de los atributos de sus perfiles de Adobe Experience Platform. Puede generar segmentos a partir de los datos sin conexión y enviarlos a [!DNL Outreach], para que se muestren en las fuentes de los posibles clientes en cuanto los segmentos y perfiles se actualicen en Adobe Experience Platform.

## Requisitos previos {#prerequisites}

### Requisitos previos del Experience Platform {#prerequisites-in-experience-platform}

Antes de activar los datos en la variable [!DNL Outreach] destino, debe tener un [esquema](/help/xdm/schema/composition.md), [conjunto de datos](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=en)y [segmentos](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=en) creado en [!DNL Experience Platform].

Consulte la documentación del Adobe para [Grupo de campos de esquema Detalles de pertenencia a segmentos](/help/xdm/field-groups/profile/segmentation.md) si necesita instrucciones sobre los estados de los segmentos.

### Requisitos previos de extensión {#prerequisites-destination}

Tenga en cuenta los siguientes requisitos previos en [!DNL Outreach], para exportar datos de Platform a su [!DNL Outreach] cuenta:

#### Necesita tener una cuenta de Extensión {#prerequisites-account}

Vaya a la [!DNL Outreach] [iniciar sesión](https://accounts.outreach.io/users/sign_in) para registrar y crear una cuenta, si todavía no la tiene. Consulte también la [!DNL Outreach] support [página](https://support.outreach.io/hc/en-us/articles/207238607-Claim-Your-Outreach-Account) para obtener más información.

Tenga en cuenta los elementos siguientes antes de autenticarse en la variable [!DNL Outreach] Destino de CRM:

| Credencial | Descripción |
|---|---|
| Correo electrónico | Su [!DNL Outreach] correo electrónico de la cuenta |
| Contraseña | Su [!DNL Outreach] contraseña de la cuenta |

#### Configuración de etiquetas de campo personalizadas {#prerequisites-custom-fields}

[!DNL Outreach] admite campos personalizados para [perspectivas](https://support.outreach.io/hc/en-us/articles/360001557554-Outreach-Prospect-Profile-Overview). Consulte [Adición de un campo personalizado en Extensión](https://support.outreach.io/hc/en-us/articles/219124908-How-To-Add-a-Custom-Field-in-Outreach) para obtener más información. Para facilitar la identificación, se recomienda actualizar manualmente las etiquetas a sus nombres de segmento correspondientes en lugar de mantener los valores predeterminados. Por ejemplo, como se muestra a continuación:

[!DNL Outreach] página de configuración para los posibles clientes que muestren campos personalizados.
![Captura de pantalla de la interfaz de usuario de extensión que muestra los campos personalizados en la página de configuración.](../../assets/catalog/crm/outreach/outreach-custom-fields.png)

[!DNL Outreach] página de configuración para posibles clientes que muestre campos personalizados con *fácil de usar* etiquetas que coinciden con los nombres de segmentos. Puede ver el estado del segmento en la página de posibles clientes con estas etiquetas.
![Captura de pantalla de la interfaz de usuario de extensión que muestra campos personalizados con etiquetas asociadas en la página de configuración.](../../assets/catalog/crm/outreach/outreach-custom-field-labels.png)

>[!NOTE]
>
> Los nombres de las etiquetas solo facilitan la identificación. No se utilizan al actualizar los prospectos.

## Límites de protección 

La variable [!DNL Outreach] La API tiene un límite de velocidad de 10 000 solicitudes por hora por usuario. Si alcanza este límite, recibirá un `429` con el siguiente mensaje: `You have exceeded your permitted rate limit of 10,000; please try again at 2017-01-01T00:00:00.`.

Si ha recibido este mensaje, debe actualizar la programación de exportación de segmentos para ajustarse al umbral de tasa.

Consulte la [[!DNL Outreach] documentación](https://api.outreach.io/api/v2/docs#rate-limiting) para obtener más información.

## Identidades compatibles {#supported-identities}

[!DNL Outreach] admite la actualización de identidades descritas en la siguiente tabla. Más información sobre [identidades](/help/identity-service/namespaces.md).

| Identidad objetivo | Descripción | Consideraciones |
|---|---|---|
| `OutreachId` | <ul><li>[!DNL Outreach] identificador. Se trata de un valor numérico correspondiente al perfil del cliente potencial.</li><li>El ID debe coincidir con el ID dentro de la variable [!DNL Outreach] URL del posible cliente que se está actualizando.</li><li>Consulte la [[!DNL Outreach] documentación](https://api.outreach.io/api/v2/docs#update-an-existing-resource) para obtener más información.</li></ul> | Obligatorio |

## Tipo de exportación y frecuencia {#export-type-frequency}

Consulte la tabla siguiente para obtener información sobre el tipo y la frecuencia de exportación de destino.

| Elemento | Tipo | Notas |
---------|----------|---------|
| Tipo de exportación | **[!UICONTROL Basado en perfiles]** | <ul><li> Está exportando todos los miembros de un segmento, junto con los campos de esquema deseados *(por ejemplo: dirección de correo electrónico, número de teléfono, apellidos)*, según la asignación de campos.</li><li> Cada estado de segmento en [!DNL Outreach] se actualiza con el estado del segmento correspondiente de Platform, en función de la variable [!UICONTROL ID de asignación] valor proporcionado durante el [programación de segmentos](#schedule-segment-export-example) paso a paso.</li></ul> |
| Frecuencia de exportación | **[!UICONTROL Transmisión]** | <ul><li> Los destinos de flujo continuo son conexiones basadas en API &quot;siempre activadas&quot;. Tan pronto como un perfil se actualiza en el Experience Platform en función de la evaluación de segmentos, el conector envía la actualización descendente a la plataforma de destino. Más información sobre [destinos de flujo continuo](/help/destinations/destination-types.md#streaming-destinations).</li></ul> |

{style=&quot;table-layout:auto&quot;}

## Conectarse al destino {#connect}

>[!IMPORTANT]
> 
> Para conectarse al destino, necesita la variable **[!UICONTROL Administrar destinos]** [permiso de control de acceso](/help/access-control/home.md#permissions). Lea el [información general sobre el control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Para conectarse a este destino, siga los pasos descritos en la sección [tutorial de configuración de destino](../../ui/connect-destination.md). En el flujo de trabajo de configuración de destino, rellene los campos que aparecen en las dos secciones siguientes.

Within **[!UICONTROL Destinos]** > **[!UICONTROL Catálogo]** buscar [!DNL Outreach]. También puede localizarlo en la categoría CRM .

### Autenticar en destino {#authenticate}

Para autenticarse en el destino, seleccione **[!UICONTROL Conectarse al destino]**.

![Captura de pantalla de la interfaz de usuario de Platform que muestra cómo autenticarse en el Extensión.](../../assets/catalog/crm/outreach/authenticate-destination.png)

Se le mostrará la variable [!DNL Outreach] página de inicio de sesión. Proporcione su correo electrónico.

![Captura de pantalla de la interfaz de usuario de extensión que muestra el campo para introducir el correo electrónico para autenticarse en el área de divulgación.](../../assets/catalog/crm/outreach/authenticate-destination-login-email.png)

A continuación, proporcione su contraseña.

![Captura de pantalla de la interfaz de usuario de extensión que muestra el campo para introducir el paso de contraseña para autenticarse en el área de divulgación.](../../assets/catalog/crm/outreach/authenticate-destination-login-password.png)

* **[!UICONTROL Nombre de usuario]**: Su [!DNL Outreach] correo electrónico de la cuenta.
* **[!UICONTROL Contraseña]**: Su [!DNL Outreach] contraseña de la cuenta.

Si los detalles proporcionados son válidos, la interfaz de usuario muestra un **Conectado** con una marca de verificación verde. A continuación, puede continuar con el paso siguiente.

### Rellenar detalles de destino {#destination-details}

Para configurar los detalles del destino, rellene los campos opcionales y requeridos a continuación. Un asterisco junto a un campo en la interfaz de usuario indica que el campo es obligatorio.
![Captura de pantalla de la interfaz de usuario de Platform que muestra cómo rellenar los detalles para el destino de Extensión.](../../assets/catalog/crm/outreach/destination-details.png)

* **[!UICONTROL Nombre]**: Un nombre por el cual reconocerá este destino en el futuro.
* **[!UICONTROL Descripción]**: Descripción que le ayudará a identificar este destino en el futuro.

### Habilitar alertas {#enable-alerts}

Puede activar las alertas para recibir notificaciones sobre el estado del flujo de datos a su destino. Seleccione una alerta de la lista para suscribirse y recibir notificaciones sobre el estado de su flujo de datos. Para obtener más información sobre las alertas, consulte la guía de [suscripción a alertas de destinos mediante la interfaz de usuario](../../ui/alerts.md).

Cuando haya terminado de proporcionar detalles para la conexión de destino, seleccione **[!UICONTROL Siguiente]**.

## Activar segmentos en este destino {#activate}

>[!IMPORTANT]
> 
> Para activar los datos, necesita la variable **[!UICONTROL Administrar destinos]**, **[!UICONTROL Activar destinos]**, **[!UICONTROL Ver perfiles]** y **[!UICONTROL Ver segmentos]** [permisos de control de acceso](/help/access-control/home.md#permissions). Lea el [información general sobre el control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Lectura [Activar perfiles y segmentos en destinos de exportación de segmentos de flujo continuo](../../ui/activate-segment-streaming-destinations.md) para obtener instrucciones sobre la activación de segmentos de audiencia en este destino.

### Consideraciones de asignación y ejemplo {#mapping-considerations-example}

Para enviar correctamente los datos de audiencia de Adobe Experience Platform a [!DNL Outreach] destino, debe pasar por el paso de asignación de campos. La asignación consiste en la creación de un vínculo entre los campos de esquema del Modelo de datos de experiencia (XDM) en la cuenta de Platform y sus equivalentes correspondientes desde el destino de destino. Para asignar correctamente los campos XDM a la variable [!DNL Outreach] campos de destino, siga estos pasos:

1. En el [!UICONTROL Asignación] paso, haga clic en **[!UICONTROL Añadir nueva asignación]**. Verá una nueva fila de asignación en la pantalla.
   ![Captura de pantalla de la interfaz de usuario de Platform que muestra cómo agregar una nueva asignación](../../assets/catalog/crm/outreach/add-new-mapping.png)

1. En el [!UICONTROL Seleccionar campo de origen] , seleccione **[!UICONTROL Seleccionar área de nombres de identidad]** y añada las asignaciones deseadas.
   ![Captura de pantalla de la interfaz de usuario de Platform que muestra la asignación de fuentes](../../assets/catalog/crm/outreach/source-mapping.png)

1. En el [!UICONTROL Seleccionar campo de destino] , seleccione el tipo de campo de destino al que desea asignar el campo de origen.
   * **[!UICONTROL Seleccionar área de nombres de identidad]**: seleccione esta opción para asignar el campo de origen a un área de nombres de identidad de la lista.
      ![Captura de pantalla de la interfaz de usuario de la plataforma que muestra la asignación de Target mediante Id de Extensión.](../../assets/catalog/crm/outreach/target-mapping.png)

   * Añada la siguiente asignación entre el esquema de perfil XDM y el [!DNL Outreach] instancia: |Esquema de perfil XDM|[!DNL Outreach] Instancia| Obligatoria| |—|—|—| |`Oid`|`OutreachId`| Sí |

   * **[!UICONTROL Seleccionar atributos personalizados]**: seleccione esta opción para asignar el campo de origen a un atributo personalizado que defina en la variable [!UICONTROL Nombre del atributo] campo . Consulte [[!DNL Outreach] documentación del cliente potencial](https://api.outreach.io/api/v2/docs#prospect) para obtener una lista completa de los atributos admitidos.
      ![Captura de pantalla de la interfaz de usuario de Platform que muestra la asignación de Target con LastName.](../../assets/catalog/crm/outreach/target-mapping-lastname.png)

   * Por ejemplo, según los valores que desee actualizar, agregue la siguiente asignación entre el esquema de perfil XDM y el [!DNL Outreach] instancia: |Esquema de perfil XDM|[!DNL Outreach] Instancia| |—|—| |`person.name.firstName`|`firstName`| |`person.name.lastName`|`lastName`|

   * A continuación se muestra un ejemplo con estas asignaciones:
      ![Captura de pantalla de la interfaz de usuario de Platform que muestra asignaciones de Target.](../../assets/catalog/crm/outreach/mappings.png)

### Programar exportación de segmentos y ejemplo {#schedule-segment-export-example}

* Al realizar el [Programar exportación de segmentos](../../ui/activate-segment-streaming-destinations.md) paso debe asignar manualmente los segmentos de Platform al atributo de campo personalizado en [!DNL Outreach].

* Para ello, seleccione cada segmento e introduzca el valor numérico correspondiente que corresponda a la variable *Campo personalizado `N` Etiqueta* campo de [!DNL Outreach] en el **[!UICONTROL ID de asignación]** campo .

   >[!IMPORTANT]
   >
   > * El valor numérico *(`N`)* se usa dentro de la variable [!UICONTROL ID de asignación] debe coincidir con la clave de atributo personalizada con el valor numérico dentro de [!DNL Outreach]. Ejemplo: *Campo personalizado `N` Etiqueta*.
   > * Solo es necesario especificar el valor numérico, no toda la etiqueta de campo personalizada.
   > * [!DNL Outreach] admite un máximo de 150 campos de etiqueta personalizados.
   > * Consulte [[!DNL Outreach] documentación del cliente potencial](https://api.outreach.io/api/v2/docs#prospect) para obtener más información.


   * Por ejemplo:

      | [!DNL Outreach] Campo | ID de asignación de plataforma |
      |---|---|
      | Campo personalizado `4` Etiqueta | `4` |

      ![Captura de pantalla de la interfaz de usuario de Platform que muestra un ejemplo de Id de asignación durante la exportación del segmento de programación.](../../assets/catalog/crm/outreach/schedule-segment-export.png)

## Validación de la exportación de datos {#exported-data}

Para validar que ha configurado correctamente el destino, siga los pasos a continuación:

1. Select **[!UICONTROL Destinos]** > **[!UICONTROL Examinar]** para navegar a la lista de destinos.
   ![Captura de pantalla de la interfaz de usuario de Platform que muestra los destinos de exploración.](../../assets/catalog/crm/outreach/browse-destinations.png)

1. Seleccione el destino y valide que el estado es **[!UICONTROL enabled]**.
   ![Captura de pantalla de la interfaz de usuario de Platform que muestra la ejecución del flujo de datos de Destinations para el destino seleccionado.](../../assets/catalog/crm/outreach/destination-dataflow-run.png)

1. Cambie a la **[!DNL Activation data]** y, a continuación, seleccione un nombre de segmento.
   ![Captura de pantalla de la interfaz de usuario de Platform que muestra los datos de activación de destinos .](../../assets/catalog/crm/outreach/destinations-activation-data.png)

1. Monitorice el resumen del segmento y asegúrese de que el recuento de perfiles corresponde al recuento creado dentro del segmento.
   ![Captura de pantalla de la interfaz de usuario de Platform que muestra el resumen del segmento.](../../assets/catalog/crm/outreach/segment.png)

1. Inicie sesión en la [!DNL Outreach] sitio web y, a continuación, vaya a la [!DNL Apps] > [!DNL Contacts] y compruebe si se han añadido los perfiles del segmento. Puede ver cada estado de segmento en [!DNL Outreach] se actualizó con el estado del segmento correspondiente de Platform, en función de la variable [!UICONTROL ID de asignación] valor proporcionado durante el [programación de segmentos](#schedule-segment-export-example) paso a paso.

![Captura de pantalla de la interfaz de usuario de extensión que muestra la página de perspectivas de extensión con los estados de segmento actualizados.](../../assets/catalog/crm/outreach/outreach-prospect.png)

## Uso y gobernanza de los datos {#data-usage-governance}

Todo [!DNL Adobe Experience Platform] Los destinos de cumplen las políticas de uso de datos al administrar los datos. Para obtener información detallada sobre cómo [!DNL Adobe Experience Platform] exige el control de datos; consulte [Información general sobre la administración de datos](/help/data-governance/home.md).

## Errores y solución de problemas {#errors-and-troubleshooting}

Al comprobar la ejecución de un flujo de datos, es posible que vea el siguiente mensaje de error: `Bad request reported while pushing events to the destination. Please contact the administrator and try again.`

![Captura de pantalla de la interfaz de usuario de Platform que muestra el error de solicitud incorrecta.](../../assets/catalog/crm/outreach/error.png)

Para solucionar este error, compruebe que la variable [!UICONTROL ID de asignación] ha proporcionado Platform para su [!DNL Outreach] el segmento es válido y existe en [!DNL Outreach].

## Recursos adicionales {#additional-resources}

La variable [[!DNL Outreach] documentación](https://api.outreach.io/api/v2/docs/) tiene detalles sobre [Respuestas de error](https://api.outreach.io/api/v2/docs#error-responses) que puede utilizar para depurar cualquier problema.
