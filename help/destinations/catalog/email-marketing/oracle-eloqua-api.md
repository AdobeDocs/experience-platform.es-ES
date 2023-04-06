---
title: Conexión (API) Eloqua de Oracle
description: El destino Eloqua de Oracle (API) le permite exportar los datos de su cuenta y activarlos en Oracle Eloqua para sus necesidades comerciales.
last-substantial-update: 2023-03-14T00:00:00Z
source-git-commit: e8aa09545c95595e98b4730188bd8a528ca299a9
workflow-type: tm+mt
source-wordcount: '1642'
ht-degree: 0%

---


# [!DNL (API) Oracle Eloqua] connection

[[!DNL Oracle Eloqua]](https://www.oracle.com/cx/marketing/automation/) permite a los especialistas en marketing planificar y ejecutar campañas al mismo tiempo que ofrecen una experiencia de cliente personalizada para sus clientes potenciales. Gracias a la administración integrada de posibles clientes y a la sencilla creación de campañas, ayuda a los especialistas en marketing a atraer a la audiencia adecuada en el momento adecuado en el recorrido de su comprador y escala elegantemente para llegar a las audiencias en todos los canales, incluidos el correo electrónico, la búsqueda en pantalla, el vídeo y el móvil. Los equipos de ventas pueden cerrar más ofertas a una velocidad más rápida, lo que aumenta el ROI de marketing a través de la perspectiva en tiempo real.

Esta [!DNL Adobe Experience Platform] [destino](/help/destinations/home.md) aprovecha el [Actualizar un contacto](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/op-api-rest-1.0-data-contact-id-put.html) operación desde el [!DNL Oracle Eloqua] API de REST, que le permite **actualizar identidades** dentro de un segmento [!DNL Oracle Eloqua].

[!DNL Oracle Eloqua] uses [Autenticación básica](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/Authentication_Basic.html) para comunicarse con el [!DNL Oracle Eloqua] API de REST. Instrucciones para autenticarse en su [!DNL Oracle Eloqua] más abajo, en la [Autenticar en destino](#authenticate) para obtener más información.

## Casos de uso {#use-cases}

El departamento de marketing de una plataforma en línea quiere transmitir una campaña de marketing basada en correo electrónico a una audiencia seleccionada de posibles clientes. El equipo de marketing de la plataforma puede actualizar la información de posibles clientes existente a través de Adobe Experience Platform, crear segmentos a partir de sus propios datos sin conexión y enviar estos segmentos a [!DNL Oracle Eloqua], que se puede utilizar para enviar el correo electrónico de la campaña de marketing.

## Requisitos previos {#prerequisites}

### Requisitos previos del Experience Platform {#prerequisites-in-experience-platform}

Antes de activar los datos en la variable [!DNL Oracle Eloqua] destino, debe tener un [esquema](/help/xdm/schema/composition.md), [conjunto de datos](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=en)y [segmentos](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=en) creado en [!DNL Experience Platform].

Consulte la documentación del Experience Platform para [Grupo de campos de esquema Detalles de pertenencia a segmentos](/help/xdm/field-groups/profile/segmentation.md) si necesita instrucciones sobre los estados de los segmentos.

### [!DNL Oracle Eloqua] requisitos previos {#prerequisites-destination}

Para exportar datos de Platform a su [!DNL Oracle Eloqua] cuenta que necesita tener una [!DNL Oracle Eloqua] cuenta.

#### Recopilar [!DNL Oracle Eloqua] credenciales {#gather-credentials}

Tenga en cuenta los elementos siguientes antes de autenticarse en la variable [!DNL Oracle Eloqua] destino:

| Credencial | Descripción |
| --- | --- |
| `Username` | El nombre de usuario de su [!DNL Oracle Eloqua] cuenta. |
| `Password` | La contraseña de su [!DNL Oracle Eloqua] cuenta. |

## Mecanismos de protección {#guardrails}

>[!NOTE]
>
>* [!DNL Oracle Eloqua] los campos de contacto personalizados se crean automáticamente con los nombres de los segmentos seleccionados durante el **[!UICONTROL Seleccionar segmentos]** paso a paso.


* [!DNL Oracle Eloqua] tiene un límite máximo de 250 campos de contacto personalizados.
* Antes de exportar nuevos segmentos, asegúrese de que el número de segmentos de Platform y el número de segmentos existentes dentro de [!DNL Oracle Eloqua] no superen este límite.
* Si se supera este límite, se producirá un error en el Experience Platform. Esto se debe a que la variable [!DNL Oracle Eloqua] La API no valida la solicitud y responde con - *400: Error de validación* - mensaje de error que describe el problema.
* Si ha alcanzado el límite especificado anteriormente, debe eliminar las asignaciones existentes de su destino y los campos de contacto personalizados correspondientes de su [!DNL Oracle Eloqua] para poder exportar más segmentos.

* Consulte la [[!DNL Oracle Eloqua] Creación de campos de contacto](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-user/Help/ContactFields/Tasks/CreatingContactFields.htm) para obtener más información sobre los límites adicionales.

## Identidades compatibles {#supported-identities}

[!DNL Oracle Eloqua] admite la actualización de identidades descritas en la siguiente tabla. Más información sobre [identidades](/help/identity-service/namespaces.md).

| Identidad de Target | Descripción | Obligatorio |
|---|---|---|
| `EloquaId` | Identificador único del contacto. | Sí |

## Tipo de exportación y frecuencia {#export-type-frequency}

Consulte la tabla siguiente para obtener información sobre el tipo y la frecuencia de exportación de destino.

| Elemento | Tipo | Notas |
---------|----------|---------|
| Tipo de exportación | **[!UICONTROL Basado en perfiles]** | <ul><li>Está exportando todos los miembros de un segmento, junto con los campos de esquema deseados *(por ejemplo: dirección de correo electrónico, número de teléfono, apellidos)*, según la asignación de campos.</li><li> Para cada segmento seleccionado en Platform, el [!DNL Oracle Eloqua] el estado del segmento se actualiza con su estado del segmento desde Platform.</li></ul> |
| Frecuencia de exportación | **[!UICONTROL Transmisión]** | <ul><li>Los destinos de flujo continuo son conexiones basadas en API &quot;siempre activadas&quot;. Tan pronto como un perfil se actualiza en el Experience Platform en función de la evaluación de segmentos, el conector envía la actualización descendente a la plataforma de destino. Más información sobre [destinos de flujo continuo](/help/destinations/destination-types.md#streaming-destinations).</li></ul> |

{style="table-layout:auto"}

## Conectarse al destino {#connect}

>[!IMPORTANT]
>
>Para conectarse al destino, necesita la variable **[!UICONTROL Administrar destinos]** [permiso de control de acceso](/help/access-control/home.md#permissions). Lea el [información general sobre el control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Para conectarse a este destino, siga los pasos descritos en la sección [tutorial de configuración de destino](../../ui/connect-destination.md). En el flujo de trabajo de configuración de destino, rellene los campos que aparecen en las dos secciones siguientes.

Within **[!UICONTROL Destinos]** > **[!UICONTROL Catálogo]** buscar [!DNL (API) Oracle Eloqua]. También puede localizarlo en la sección **[!UICONTROL Marketing por correo electrónico]** categoría.

### Autenticar en destino {#authenticate}

Complete los campos obligatorios a continuación. Consulte la [Recopilar [!DNL Oracle Eloqua] credenciales](#gather-credentials) para obtener más información.
* **[!UICONTROL Contraseña]**: La contraseña de su [!DNL Oracle Eloqua] cuenta.
* **[!UICONTROL Nombre de usuario]**: El nombre de usuario de su [!DNL Oracle Eloqua] cuenta.

Para autenticarse en el destino, seleccione **[!UICONTROL Conectarse al destino]**.
![Captura de pantalla de la interfaz de usuario de Platform que muestra cómo autenticarse.](../../assets/catalog/email-marketing/oracle-eloqua-api/authenticate-destination.png)

Si los detalles proporcionados son válidos, la interfaz de usuario muestra un **[!UICONTROL Conectado]** con una marca de verificación verde. A continuación, puede continuar con el paso siguiente.

### Rellenar detalles de destino {#destination-details}

Para configurar los detalles del destino, rellene los campos opcionales y requeridos a continuación. Un asterisco junto a un campo en la interfaz de usuario indica que el campo es obligatorio.
![Captura de pantalla de la interfaz de usuario de Platform que muestra los detalles del destino.](../../assets/catalog/email-marketing/oracle-eloqua-api/destination-details.png)

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

Para enviar correctamente los datos de audiencia de Adobe Experience Platform a [!DNL Oracle Eloqua] destino, debe pasar por el paso de asignación de campos. La asignación consiste en la creación de un vínculo entre los campos de esquema del Modelo de datos de experiencia (XDM) en la cuenta de Platform y sus equivalentes correspondientes desde el destino de destino.

Para asignar los campos XDM a la variable [!DNL Oracle Eloqua] campos de destino, siga estos pasos:

1. En el **[!UICONTROL Asignación]** paso, seleccione **[!UICONTROL Añadir nueva asignación]**. Verá una nueva fila de asignación en la pantalla.
1. En el **[!UICONTROL Seleccionar campo de origen]** , seleccione **[!UICONTROL Seleccionar atributos]** y seleccione el atributo XDM o elija el **[!UICONTROL Seleccionar área de nombres de identidad]** y seleccione una identidad.
1. En el **[!UICONTROL Seleccionar campo de destino]** ventana, elija **[!UICONTROL Seleccionar área de nombres de identidad]** y seleccione una identidad o elija **[!UICONTROL Seleccionar atributos personalizados]** y escriba el nombre de atributo deseado en la **[!UICONTROL Nombre del atributo]** campo . El nombre de atributo que proporcione debe coincidir con un atributo de contacto existente en [!DNL Oracle Eloqua]. Consulte [[!DNL create a contact]](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/op-api-rest-1.0-data-contact-post.html) para los nombres de atributos exactos que puede usar en [!DNL Oracle Eloqua].
   * Repita estos pasos para agregar las asignaciones de atributos necesarias y deseadas entre el esquema de perfil XDM y [!DNL Oracle Eloqua]: | Campo de origen | Campo Target | Obligatorio | |—|—|—| |`IdentityMap: Eid`|`Identity: EloquaId`| Sí | |`xdm: personalEmail.address`|`Attribute: emailAddress`| Sí | |`xdm: personName.firstName`|`Attribute: firstName`| | |`xdm: personName.lastName`|`Attribute: lastName`| | |`xdm: workAddress.street1`|`Attribute: address1`| | |`xdm: workAddress.street2`|`Attribute: address2`| | |`xdm: workAddress.street3`|`Attribute: address3`| | |`xdm: workAddress.postalCode`|`Attribute: postalCode`| | |`xdm: workAddress.country`|`Attribute: country`| | |`xdm: workAddress.city`|`Attribute: city`| |

   * A continuación se muestra un ejemplo con las asignaciones anteriores:
      ![Ejemplo de captura de pantalla de la interfaz de usuario de Platform con asignaciones de atributos.](../../assets/catalog/email-marketing/oracle-eloqua-api/mappings.png)

>[!IMPORTANT]
>
>* Los atributos especificados en la variable **[!UICONTROL Campo de destino]** debe tener el mismo nombre que el especificado en la variable [[!DNL Create a contact]](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/op-api-rest-1.0-data-contact-post.html) ya que estos atributos formarán el cuerpo de la solicitud.
>* Los atributos especificados en la variable **[!UICONTROL Campo de origen]** no seguir ninguna restricción de este tipo. Puede asignarlo en función de sus necesidades, pero si el formato de los datos no es correcto al insertarlo en [!DNL Oracle Eloqua] resultará en un error. Por ejemplo, puede asignar la variable **[!UICONTROL Campo de origen]** área de nombres de identidad `contact key`, `ABC ID` etc. a **[!UICONTROL Campo de destino]** : `EloquaId` después de asegurarse de que los valores de ID coinciden con el formato aceptado por [!DNL Oracle Eloqua].
>* La variable `EloquaID` la asignación es obligatoria para actualizar los atributos correspondientes a la identidad.
>* La variable `emailAddress` se requiere la asignación. Sin ella, la API genera un error como se muestra a continuación:
>
>```json
>{
>     "type":"ObjectValidationError",
>     "container":{
>           "type":"ObjectKey",
>           "objectType":"Contact"
>     },
>     "property":"emailAddress",
>     "requirement":{
>           "type":"EmailAddressRequirement"
>     },
>     "value":"<null>"
>}
>```

Cuando haya terminado de proporcionar las asignaciones para la conexión de destino, seleccione **[!UICONTROL Siguiente]**.

>[!NOTE]
>
>El destino agrega automáticamente un identificador único a los nombres de segmento seleccionados en cada ejecución al enviar la información del campo de contacto a [!DNL Oracle Eloqua]. Esto garantiza que los nombres de los campos de contacto correspondientes a sus nombres de segmento no se superpongan. Consulte la [Validación de la exportación de datos](#exported-data) captura de pantalla ejemplo de [!DNL Oracle Eloqua] Página Detalles de contacto con el campo de contacto personalizado creado con los nombres de segmento.

## Validación de la exportación de datos {#exported-data}

Para validar que ha configurado correctamente el destino, siga los pasos a continuación:

1. Select **[!UICONTROL Destinos]** > **[!UICONTROL Examinar]** y vaya a la lista de destinos.
1. A continuación, seleccione el destino y cambie a la **[!UICONTROL Datos de activación]** y, a continuación, seleccione un nombre de segmento.
   ![Captura de pantalla de la interfaz de usuario de Platform que muestra los datos de activación de destinos.](../../assets/catalog/email-marketing/oracle-eloqua-api/destinations-activation-data.png)

1. Monitorice el resumen del segmento y asegúrese de que el recuento de perfiles corresponde al recuento dentro del segmento.
   ![Captura de pantalla de la interfaz de usuario de Platform que muestra el segmento.](../../assets/catalog/email-marketing/oracle-eloqua-api/segment.png)

1. Inicie sesión en la [!DNL Oracle Eloqua] sitio web y, a continuación, vaya a la **[!UICONTROL Información general de contactos]** para comprobar si se han añadido los perfiles del segmento. Para ver el estado del segmento, explore en profundidad una **[!UICONTROL Detalles de contacto]** y compruebe si se ha creado el campo de contacto con el nombre del segmento seleccionado como prefijo.

![Captura de pantalla de la interfaz de usuario de Eloqua de oracle que muestra la página Detalles de contacto con el campo de contacto personalizado creado con el nombre del segmento.](../../assets/catalog/email-marketing/oracle-eloqua-api/contact.png)

## Uso y gobernanza de los datos {#data-usage-governance}

Todo [!DNL Adobe Experience Platform] Los destinos de cumplen las políticas de uso de datos al administrar los datos. Para obtener información detallada sobre cómo [!DNL Adobe Experience Platform] exige el control de datos; consulte [Información general sobre la administración de datos](/help/data-governance/home.md).

## Errores y solución de problemas {#errors-and-troubleshooting}

Al crear el destino, puede recibir uno de los siguientes mensajes de error: `400: There was a validation error` o `400 BAD_REQUEST`. Esto sucede cuando se supera el límite de 250 campos de contacto personalizados, tal como se describe en la sección [guardrails](#guardrails) para obtener más información. Para solucionar este error, asegúrese de que no está superando el límite del campo de contacto personalizado en [!DNL Oracle Eloqua].
![Captura de pantalla de la interfaz de usuario de Platform que muestra el error.](../../assets/catalog/email-marketing/oracle-eloqua-api/error.png)

Consulte la [[!DNL Oracle Eloqua] Códigos de estado HTTP](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/APIRequests_HTTPStatusCodes.html) y [[!DNL Oracle Eloqua] Errores de validación](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/APIRequests_HTTPValidationErrors.html) para obtener una lista completa de estados y códigos de error con explicaciones.

## Recursos adicionales {#additional-resources}

Para obtener más información, consulte la [!DNL Oracle Eloqua] documentación:

* [Automatización de mercadotecnia Eloqua de oracle](https://docs.oracle.com/en/cloud/saas/marketing/eloqua.html)
* [API de REST para el servicio de Marketing Cloud de Oracle Eloqua](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/rest-endpoints.html)