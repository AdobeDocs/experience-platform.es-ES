---
title: (API) Conexión de Oracle Eloqua
description: El Oracle (API) Eloqua permite exportar los datos de la cuenta y activarlos dentro de Oracle Eloqua para satisfacer sus necesidades comerciales.
last-substantial-update: 2023-03-14T00:00:00Z
exl-id: 97ff41a2-2edd-4608-9557-6b28e74c4480
source-git-commit: cf7ad18fa3d8f074371a0f03e09e218d37be5e01
workflow-type: tm+mt
source-wordcount: '2033'
ht-degree: 1%

---


# [!DNL (API) Oracle Eloqua] conexión

[[!DNL Oracle Eloqua]](https://www.oracle.com/cx/marketing/automation/) permite a los especialistas en marketing planificar y ejecutar campañas al tiempo que ofrecen una experiencia del cliente personalizada para sus posibles clientes. Con una administración de posibles clientes integrada y una creación de campañas sencilla, ayuda a los especialistas en marketing a atraer a la audiencia adecuada en el momento adecuado en el recorrido del comprador y se escala de forma elegante para llegar a audiencias de varios canales, incluidos correo electrónico, búsqueda en pantalla, vídeo y móvil. Los equipos de ventas pueden cerrar más acuerdos a una velocidad más rápida, lo que aumenta el retorno de la inversión de marketing a través de una perspectiva en tiempo real.

Esta [!DNL Adobe Experience Platform] [destino](/help/destinations/home.md) aprovecha el [Actualizar un contacto](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/op-api-rest-1.0-data-contact-id-put.html) operación desde el [!DNL Oracle Eloqua] API de REST, que le permite **actualizar identidades** dentro de una audiencia en [!DNL Oracle Eloqua].

[!DNL Oracle Eloqua] utiliza [Autenticación básica](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/Authentication_Basic.html) para comunicarse con el [!DNL Oracle Eloqua] API DE REST. Instrucciones para autenticarse en su [!DNL Oracle Eloqua] más abajo, en la sección [Autenticar en el destino](#authenticate) sección.

## Casos de uso {#use-cases}

El departamento de marketing de una plataforma en línea desea difundir una campaña de marketing basada en correo electrónico a una audiencia seleccionada de posibles clientes. El equipo de marketing de la plataforma puede actualizar la información de posibles clientes existente a través de Adobe Experience Platform, crear audiencias a partir de sus propios datos sin conexión y enviar estas audiencias a [!DNL Oracle Eloqua], que se puede utilizar para enviar el correo electrónico de la campaña de marketing.

## Requisitos previos {#prerequisites}

### Requisitos previos del Experience Platform {#prerequisites-in-experience-platform}

Antes de activar los datos en [!DNL Oracle Eloqua] destino, debe tener un [esquema](/help/xdm/schema/composition.md), a [conjunto de datos](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html), y [segmentos](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html) creado en [!DNL Experience Platform].

Consulte la documentación del Experience Platform para [Grupo de campos de esquema Detalles de pertenencia a audiencia](/help/xdm/field-groups/profile/segmentation.md) si necesita orientación sobre los estados de audiencia.

### [!DNL Oracle Eloqua] requisitos previos {#prerequisites-destination}

Para exportar datos de Platform a su [!DNL Oracle Eloqua] cuenta necesita tener un [!DNL Oracle Eloqua] cuenta.

Además, necesita, como mínimo, el *&quot;Usuarios avanzados: permisos de marketing&quot;* para su [!DNL Oracle Eloqua] ejemplo. Consulte la *&quot;Grupos de seguridad&quot;* en la sección [Acceso seguro del usuario](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-user/Help/SecurityOverview/SecuredUserAccess.htm) página para obtener instrucciones. El destino requiere el acceso para programar [determinar la dirección URL base](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/DeterminingBaseURL.html) al invocar el [!DNL Oracle Eloqua] API.

#### Reunir [!DNL Oracle Eloqua] credenciales {#gather-credentials}

Tenga en cuenta los elementos siguientes antes de autenticarse en el [!DNL Oracle Eloqua] destino:

| Credencial | Descripción |
| --- | --- |
| `Company Name` | El nombre de la empresa asociada con su [!DNL Oracle Eloqua] cuenta. <br>Más adelante utilizará la variable `Company Name` y [!DNL Oracle Eloqua] `Username` como una cadena concatenada que se utilizará como **[!UICONTROL Nombre de usuario]** cuando [autenticación en el destino](#authenticate). |
| `Username` | El nombre de usuario de su [!DNL Oracle Eloqua] cuenta. |
| `Password` | La contraseña de su [!DNL Oracle Eloqua] cuenta. |
| `Pod` | [!DNL Oracle Eloqua] admite varios centros de datos, cada uno con un nombre de dominio único. [!DNL Oracle Eloqua] se refiere a estos como &quot;pods&quot;, actualmente hay siete en total: p01, p02, p03, p04, p06, p07 y p08. Para obtener en qué POD se encuentra, inicie sesión en [!DNL Oracle Eloqua] y anote la URL en el navegador después de haber iniciado sesión correctamente. Por ejemplo, si la dirección URL del explorador es `secure.p01.eloqua.com` su `pod` es `p01`. Consulte la [determinación del POD](https://community.oracle.com/topliners/discussion/4470225/determining-your-pod-number-for-oracle-eloqua) página para obtener más información. |

Consulte la [Iniciando sesión en [!DNL Oracle Eloqua]](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-user/Help/Administration/Tasks/SigningInToEloqua.htm#Signing) para obtener orientación.

## Mecanismos de protección {#guardrails}

>[!NOTE]
>
>* [!DNL Oracle Eloqua] los campos de contacto personalizados se crean automáticamente con los nombres de las audiencias seleccionadas durante la **[!UICONTROL Seleccionar segmentos]** paso.

* [!DNL Oracle Eloqua] tiene un límite máximo de 250 campos de contacto personalizados.
* Antes de exportar nuevas audiencias, asegúrese de que el número de audiencias de Platform y el número de audiencias existentes dentro de [!DNL Oracle Eloqua] no supere este límite.
* Si se supera este límite, se producirá un error en el Experience Platform. Esto se debe a que [!DNL Oracle Eloqua] La API no puede validar la solicitud y responde con un - *400: Error de validación* - mensaje de error que describe el problema.
* Si ha alcanzado el límite especificado anteriormente, debe eliminar las asignaciones existentes de su destino y eliminar los campos de contacto personalizados correspondientes en su [!DNL Oracle Eloqua] cuenta antes de poder exportar más segmentos.

* Consulte la [[!DNL Oracle Eloqua] Creación de campos de contacto](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-user/Help/ContactFields/Tasks/CreatingContactFields.htm) para obtener información sobre los límites adicionales.

## Identidades admitidas {#supported-identities}

[!DNL Oracle Eloqua] admite la actualización de identidades que se describe en la tabla siguiente. Más información sobre [identidades](/help/identity-service/features/namespaces.md).

| Identidad de destino | Descripción | Obligatorio |
|---|---|---|
| `EloquaId` | Identificador único del contacto. | Sí |

## Tipo y frecuencia de exportación {#export-type-frequency}

Consulte la tabla siguiente para obtener información sobre el tipo y la frecuencia de exportación de destino.

| Elemento | Tipo | Notas |
---------|----------|---------|
| Tipo de exportación | **[!UICONTROL Basado en perfiles]** | <ul><li>Está exportando todos los miembros de un segmento, junto con los campos de esquema deseados *(por ejemplo: dirección de correo electrónico, número de teléfono, apellidos)*, según la asignación de campo.</li><li> Para cada audiencia seleccionada en Platform, la correspondiente [!DNL Oracle Eloqua] El estado del segmento se actualiza con su estado de audiencia de Platform.</li></ul> |
| Frecuencia de exportación | **[!UICONTROL Transmisión]** | <ul><li>Los destinos de streaming son conexiones basadas en API &quot;siempre activadas&quot;. Tan pronto como se actualiza un perfil en Experience Platform según la evaluación de audiencias, el conector envía la actualización de forma descendente a la plataforma de destino. Más información sobre [destinos de streaming](/help/destinations/destination-types.md#streaming-destinations).</li></ul> |

{style="table-layout:auto"}

## Conectar con el destino {#connect}

>[!IMPORTANT]
>
>Para conectarse al destino, necesita el **[!UICONTROL Ver destinos]** y **[!UICONTROL Administrar destinos]** [permisos de control de acceso](/help/access-control/home.md#permissions). Lea el [información general de control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Para conectarse a este destino, siga los pasos descritos en la sección [tutorial de configuración de destino](../../ui/connect-destination.md). En el flujo de trabajo de configuración de destino, rellene los campos enumerados en las dos secciones siguientes.

En **[!UICONTROL Destinos]** > **[!UICONTROL Catálogo]** buscar [!DNL (API) Oracle Eloqua]. También puede encontrarlo en la sección **[!UICONTROL Marketing por correo electrónico]** categoría.

### Autenticar en el destino {#authenticate}

>[!CONTEXTUALHELP]
>id="platform_destinations_apioracleeloqua_companyname_username"
>title="Nombre de empresa\Nombre de usuario"
>abstract="Rellene este campo con su nombre de empresa y nombre de usuario del Oracle Eloqua en el formulario `{COMPANY_NAME}\{USERNAME}`"

Rellene los campos obligatorios siguientes. Consulte la [Reunir [!DNL Oracle Eloqua] credenciales](#gather-credentials) para obtener cualquier guía.
* **[!UICONTROL Contraseña]**: La contraseña de su [!DNL Oracle Eloqua] cuenta.
* **[!UICONTROL Nombre de usuario]**: una cadena concatenada compuesta por su [!DNL Oracle Eloqua] Nombre de la empresa y [!DNL Oracle Eloqua] Nombre de usuario.<br>El valor concatenado adopta la forma de `{COMPANY_NAME}\{USERNAME}`.<br> Tenga en cuenta que no utilice llaves ni espacios y conserve `\`. <br>Por ejemplo, si su [!DNL Oracle Eloqua] El nombre de empresa es `MyCompany` y [!DNL Oracle Eloqua] Nombre de usuario: `Username`, el valor concatenado que utilizará en el **[!UICONTROL Nombre de usuario]** el campo es `MyCompany\Username`.

Para autenticarse en el destino, seleccione **[!UICONTROL Conectar con destino]**.
![Captura de pantalla de la IU de Platform que muestra cómo autenticarse.](../../assets/catalog/email-marketing/oracle-eloqua-api/authenticate-destination.png)

Si los detalles proporcionados son válidos, la interfaz de usuario muestra un **[!UICONTROL Conectado]** estado con una marca de verificación verde. A continuación, puede continuar con el paso siguiente.

### Rellenar detalles de destino {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_apioracleeloqua_pod"
>title="Pod"
>abstract="Para encontrar su número de pod, inicie sesión en el Oracle Eloqua. Anote la dirección URL en el explorador después de haber iniciado sesión correctamente. "

<!-- >additional-url="https://support.oracle.com/knowledge/Oracle%20Cloud/2307176_1.html" text="Oracle Knowledge base - find out your Pod number" -->

Para configurar los detalles del destino, rellene los campos obligatorios y opcionales a continuación. Un asterisco junto a un campo en la interfaz de usuario indica que el campo es obligatorio.
![Captura de pantalla de la IU de Platform que muestra los detalles del destino.](../../assets/catalog/email-marketing/oracle-eloqua-api/destination-details.png)

* **[!UICONTROL Nombre]**: Un nombre con el que reconocerá este destino en el futuro.
* **[!UICONTROL Descripción]**: Una descripción que le ayudará a identificar este destino en el futuro.
* **[!UICONTROL Pod]**: para obtener qué `pod` está en, inicie sesión en [!DNL Oracle Eloqua] y anote la URL en el navegador después de haber iniciado sesión correctamente. Por ejemplo, si la dirección URL del explorador es `secure.p01.eloqua.com` el `pod` el valor que debe seleccionar es `p01`. Consulte la [Reunir [!DNL Oracle Eloqua] credenciales](#gather-credentials) para obtener más información.

### Habilitar alertas {#enable-alerts}

Puede activar alertas para recibir notificaciones sobre el estado del flujo de datos a su destino. Seleccione una alerta de la lista a la que suscribirse para recibir notificaciones sobre el estado del flujo de datos. Para obtener más información sobre las alertas, consulte la guía de [suscripción a alertas de destinos mediante la IU](../../ui/alerts.md).

Cuando haya terminado de proporcionar detalles para la conexión de destino, seleccione **[!UICONTROL Siguiente]**.

## Activar audiencias en este destino {#activate}

>[!IMPORTANT]
> 
>* Para activar los datos, necesita el **[!UICONTROL Ver destinos]**, **[!UICONTROL Activar destinos]**, **[!UICONTROL Ver perfiles]**, y **[!UICONTROL Ver segmentos]** [permisos de control de acceso](/help/access-control/home.md#permissions). Lea el [información general de control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.
>* Para exportar *identidades*, necesita el **[!UICONTROL Ver gráfico de identidad]** [permiso de control de acceso](/help/access-control/home.md#permissions). <br> ![Seleccione el área de nombres de identidad resaltada en el flujo de trabajo para activar audiencias en los destinos.](/help/destinations/assets/overview/export-identities-to-destination.png "Seleccione el área de nombres de identidad resaltada en el flujo de trabajo para activar audiencias en los destinos."){width="100" zoomable="yes"}

Leer [Activación de perfiles y audiencias en destinos de exportación de audiencia de streaming](/help/destinations/ui/activate-segment-streaming-destinations.md) para obtener instrucciones sobre cómo activar audiencias en este destino.

### Consideraciones sobre asignación y ejemplo {#mapping-considerations-example}

Para enviar correctamente los datos de audiencia de Adobe Experience Platform a [!DNL Oracle Eloqua] destino, debe ir a través del paso de asignación de campos. La asignación consiste en crear un vínculo entre los campos de esquema del Modelo de datos de experiencia (XDM) en la cuenta de Platform y sus equivalentes correspondientes desde el destino de destino.

Para asignar los campos XDM a [!DNL Oracle Eloqua] campos de destino, siga estos pasos:

1. En el **[!UICONTROL Asignación]** paso, seleccione **[!UICONTROL Añadir nueva asignación]**. Verá una nueva fila de asignación en la pantalla.
1. En el **[!UICONTROL Seleccionar campo de origen]** , seleccione la **[!UICONTROL Seleccionar atributos]** y seleccione el atributo XDM o elija el **[!UICONTROL Seleccionar área de nombres de identidad]** y seleccione una identidad.
1. En el **[!UICONTROL Seleccionar campo de destino]** ventana, elija **[!UICONTROL Seleccionar área de nombres de identidad]** y seleccione una identidad o elija **[!UICONTROL Seleccionar atributos personalizados]** y escriba el nombre de atributo deseado en la **[!UICONTROL Nombre de atributo]** field. El nombre de atributo que proporcione debe coincidir con un atributo de contacto existente en [!DNL Oracle Eloqua]. Consulte [[!DNL create a contact]](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/op-api-rest-1.0-data-contact-post.html) para los nombres de atributo exactos que puede utilizar en [!DNL Oracle Eloqua].
   * Repita estos pasos para agregar las asignaciones de atributos necesarias y deseadas entre el esquema de perfil XDM y [!DNL Oracle Eloqua]: | Campo de origen | Campo de destino | Obligatorio | |—|—|—| |`IdentityMap: Eid`|`Identity: EloquaId`| Sí | |`xdm: personalEmail.address`|`Attribute: emailAddress`| Sí | |`xdm: personName.firstName`|`Attribute: firstName`| | |`xdm: personName.lastName`|`Attribute: lastName`| | |`xdm: workAddress.street1`|`Attribute: address1`| | |`xdm: workAddress.street2`|`Attribute: address2`| | |`xdm: workAddress.street3`|`Attribute: address3`| | |`xdm: workAddress.postalCode`|`Attribute: postalCode`| | |`xdm: workAddress.country`|`Attribute: country`| | |`xdm: workAddress.city`|`Attribute: city`| |

   * A continuación, se muestra un ejemplo con las asignaciones anteriores:
     ![Ejemplo de captura de pantalla de la IU de Platform con asignaciones de atributos.](../../assets/catalog/email-marketing/oracle-eloqua-api/mappings.png)

>[!IMPORTANT]
>
>* Atributos especificados en la variable **[!UICONTROL Campo de destino]** debe tener exactamente el nombre especificado en la variable [[!DNL Create a contact]](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/op-api-rest-1.0-data-contact-post.html) ya que estos atributos forman el cuerpo de la solicitud.
>* Atributos especificados en la variable **[!UICONTROL Campo de origen]** no siga ninguna de estas restricciones. Puede asignarlo según sus necesidades, pero si el formato de datos no es correcto cuando se inserta en [!DNL Oracle Eloqua] se producirá un error. Por ejemplo, puede asignar el **[!UICONTROL Campo de origen]** área de nombres de identidad `contact key`, `ABC ID` etc. hasta **[!UICONTROL Campo de destino]** : `EloquaId` después de asegurarse de que los valores de ID coinciden con el formato aceptado por [!DNL Oracle Eloqua].
>* El `EloquaID` la asignación es obligatoria para actualizar los atributos correspondientes a la identidad.
>* El `emailAddress` se requiere la asignación. Sin ella, la API genera un error como se muestra a continuación:
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
>El destino sufijo automáticamente un identificador único a los nombres de audiencia seleccionados en cada ejecución al enviar la información del campo de contacto a [!DNL Oracle Eloqua]. Esto garantiza que los nombres de los campos de contacto correspondientes a sus nombres de audiencia no se superpongan. Consulte la [Validar exportación de datos](#exported-data) captura de pantalla de sección ejemplo de un [!DNL Oracle Eloqua] Página de detalles del contacto con campo de contacto personalizado creado con los nombres de las audiencias.

## Validar exportación de datos {#exported-data}

Para comprobar que ha configurado correctamente el destino, siga los pasos a continuación:

1. Seleccionar **[!UICONTROL Destinos]** > **[!UICONTROL Examinar]** y vaya a la lista de destinos.
1. A continuación, seleccione el destino y cambie a **[!UICONTROL Datos de activación]** y, a continuación, seleccione un nombre de audiencia.
   ![Captura de pantalla de la IU de Platform que muestra los datos de activación de destinos.](../../assets/catalog/email-marketing/oracle-eloqua-api/destinations-activation-data.png)

1. Monitorice el resumen de audiencia y asegúrese de que el recuento de perfiles corresponde al recuento dentro del segmento.
   ![Captura de pantalla de la IU de Platform que muestra el segmento.](../../assets/catalog/email-marketing/oracle-eloqua-api/segment.png)

1. Inicie sesión en [!DNL Oracle Eloqua] sitio web y, a continuación, vaya al **[!UICONTROL Información general de contactos]** para comprobar si se han añadido los perfiles de la audiencia. Para ver el estado de la audiencia, explore en profundidad un **[!UICONTROL Detalles de contacto]** y compruebe si se ha creado el campo de contacto con el nombre de audiencia seleccionado como prefijo.

![Captura de pantalla de la IU de Eloqua de oracle que muestra la página Detalles de contacto con el campo de contacto personalizado creado con el nombre de la audiencia.](../../assets/catalog/email-marketing/oracle-eloqua-api/contact.png)

## Uso de datos y gobernanza {#data-usage-governance}

Todo [!DNL Adobe Experience Platform] Los destinos de cumplen con las políticas de uso de datos al gestionar los datos. Para obtener información detallada sobre cómo [!DNL Adobe Experience Platform] aplica la gobernanza de datos. Consulte la [Resumen de gobernanza de datos](/help/data-governance/home.md).

## Errores y solución de problemas {#errors-and-troubleshooting}

Al crear el destino, puede recibir uno de los siguientes mensajes de error: `400: There was a validation error` o `400 BAD_REQUEST`. Esto sucede cuando se supera el límite de 250 campos de contacto personalizados, tal como se describe en la sección [barandas](#guardrails) sección. Para corregir este error, asegúrese de que no supera el límite del campo de contacto personalizado en [!DNL Oracle Eloqua].
![Captura de pantalla de la IU de Platform que muestra un error.](../../assets/catalog/email-marketing/oracle-eloqua-api/error.png)

Consulte la [[!DNL Oracle Eloqua] Códigos de estado HTTP](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/APIRequests_HTTPStatusCodes.html) y [[!DNL Oracle Eloqua] Errores de validación](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/APIRequests_HTTPValidationErrors.html) páginas para obtener una lista completa de estados y códigos de error con explicaciones.

## Recursos adicionales {#additional-resources}

Para obtener más información, consulte la [!DNL Oracle Eloqua] documentación:

* [Oracle Eloqua Marketing Automation](https://docs.oracle.com/en/cloud/saas/marketing/eloqua.html)
* [API de REST para el servicio de Marketing Cloud de Oracle Eloqua](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/rest-endpoints.html)

### Changelog

Esta sección recoge la funcionalidad y las actualizaciones significativas de la documentación realizadas en este conector de destino.

+++ Ver registro de cambios

| Mes de lanzamiento | Tipo de actualización | Descripción |
|---|---|---|
| Abril de 2023 | Actualización de documentación | <ul><li>Hemos actualizado la [casos de uso](#use-cases) con un ejemplo más claro de cuándo se beneficiarían los clientes de utilizar este destino.</li> <li>Hemos actualizado la [asignación](#mapping-considerations-example) con ejemplos claros de asignaciones obligatorias y opcionales.</li> <li>Hemos actualizado la [Conectar con el destino](#connect) con un ejemplo sobre cómo construir el valor concatenado para la variable **[!UICONTROL Nombre de usuario]** mediante el campo [!DNL Oracle Eloqua] Nombre de la empresa y [!DNL Oracle Eloqua] Nombre de usuario. (PLATIR-28343)</li><li>Hemos actualizado la [Reunir [!DNL Oracle Eloqua] credenciales](#gather-credentials) y el [Rellenar detalles de destino](#destination-details) secciones con directrices sobre [!DNL Oracle Eloqua] **[!UICONTROL Pod]** selección. El *&quot;Pod&quot;* El valor lo utiliza el destino para construir la dirección URL base para las llamadas de API. El [[!DNL Oracle Eloqua] requisitos previos](#prerequisites-destination) También se ha actualizado esta sección con directrices sobre la asignación de *&quot;Usuarios avanzados: permisos de marketing&quot;* como obligatorio *&quot;Grupos de seguridad&quot;* para su [!DNL Oracle Eloqua] ejemplo.</li></ul> |
| Marzo de 2023 | Versión inicial | Versión de destino inicial y publicación de documentación. |

{style="table-layout:auto"}

+++