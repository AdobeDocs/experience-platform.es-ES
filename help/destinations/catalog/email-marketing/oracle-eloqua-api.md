---
title: (API) Conexión de Oracle Eloqua
description: El destino Oracle Eloqua (API) le permite exportar los datos de su cuenta y activarlos dentro de Oracle Eloqua para sus necesidades comerciales.
last-substantial-update: 2023-03-14T00:00:00Z
exl-id: 97ff41a2-2edd-4608-9557-6b28e74c4480
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '1967'
ht-degree: 4%

---


# [!DNL (API) Oracle Eloqua] conexión

[[!DNL Oracle Eloqua]](https://www.oracle.com/cx/marketing/automation/) permite a los especialistas en marketing planificar y ejecutar campañas a la vez que ofrecen una experiencia de cliente personalizada para sus posibles clientes. Con una administración de posibles clientes integrada y una creación de campañas sencilla, ayuda a los especialistas en marketing a atraer a la audiencia adecuada en el momento adecuado en el recorrido del comprador y se escala de forma elegante para llegar a audiencias de varios canales, incluidos correo electrónico, búsqueda en pantalla, vídeo y móvil. Los equipos de ventas pueden cerrar más acuerdos a una velocidad más rápida, lo que aumenta el retorno de la inversión de marketing a través de insight en tiempo real.

Este [!DNL Adobe Experience Platform] [destino](/help/destinations/home.md) aprovecha la operación [Actualizar un contacto](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/op-api-rest-1.0-data-contact-id-put.html) de la API de REST [!DNL Oracle Eloqua], que le permite **actualizar identidades** dentro de una audiencia en [!DNL Oracle Eloqua].

[!DNL Oracle Eloqua] utiliza [Authentication](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/Authentication_Basic.html) básicos para comunicarse con la API de [!DNL Oracle Eloqua] REST. Las instrucciones para autenticarse en su instancia de [!DNL Oracle Eloqua] se encuentran más abajo, en la sección [Autenticar en destino](#authenticate).

## Casos de uso {#use-cases}

El departamento de marketing de una plataforma de en línea quiere transmitir un campaña de marketing basado en correo electrónico a un audiencia curado de clientes potenciales. Los equipo marketing de la plataforma pueden actualizar la información de posible cliente existente a través de Adobe Experience Platform, versión audiencias a partir de sus propios datos sin conexión y enviar estas audiencias a [!DNL Oracle Eloqua], que luego se pueden usar para enviar el correo electrónico campaña de marketing.

## Requisitos previos {#prerequisites}

### Requisitos previos de Experience Platform {#prerequisites-in-experience-platform}

Antes de activar datos en el destino [!DNL Oracle Eloqua], debe tener un [esquema](/help/xdm/schema/composition.md), un [conjunto de datos](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html) y [segmentos](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html) creados en [!DNL Experience Platform].

Consulte la documentación de Experience Platform para el [grupo de campos de esquema Detalles de pertenencia a audiencias](/help/xdm/field-groups/profile/segmentation.md) si necesita instrucciones sobre los estados de audiencia.

### [!DNL Oracle Eloqua] requisitos previos {#prerequisites-destination}

Para exportar datos de Experience Platform a su cuenta de [!DNL Oracle Eloqua], necesita tener una cuenta de [!DNL Oracle Eloqua].

Además, necesita, como mínimo, los *&quot;Usuarios Avanzadas - Permisos de marketing&quot;* de su [!DNL Oracle Eloqua] instancia. Consulte la *sección &quot;Grupos de seguridad&quot;* en el [Página de acceso al usuario](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-user/Help/SecurityOverview/SecuredUserAccess.htm) seguro para obtener orientación. El destino requiere el acceso para determinar mediante [programación su URL](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/DeterminingBaseURL.html) base al invocar la [!DNL Oracle Eloqua] API.

#### Recopilar [!DNL Oracle Eloqua] credenciales {#gather-credentials}

Observe los elementos siguientes antes de autenticarse en el destino [!DNL Oracle Eloqua]:

| Credencial | Descripción |
| --- | --- |
| `Company Name` | Nombre compañía asociado a su [!DNL Oracle Eloqua] cuenta. <br>Más adelante utilizará el `Company Name` y [!DNL Oracle Eloqua] `Username` como una cadena concatenada que se utilizará como **[!UICONTROL Username]** al [ autenticarse en el destino](#authenticate). |
| `Username` | Nombre de usuario de su [!DNL Oracle Eloqua] cuenta. |
| `Password` | El contraseña de su [!DNL Oracle Eloqua] cuenta. |
| `Pod` | [!DNL Oracle Eloqua] Admite varios centros de datos, cada uno con un nombre de dominio único. [!DNL Oracle Eloqua] Se refiere a estos como &quot;pods&quot;, actualmente hay siete en total: P01, P02, P03, P04, P06, P07 y P08. Para obtener en qué POD se encuentra, inicio de sesión y [!DNL Oracle Eloqua] anote el URL en su explorador después de haber iniciado sesión correctamente. Por ejemplo, si la dirección URL de su explorador es `secure.p01.eloqua.com`, su `pod` es `p01`. Consulte la página [determinar su POD](https://community.oracle.com/topliners/discussion/4470225/determining-your-pod-number-for-oracle-eloqua) para obtener más información. |

Consulte [Iniciar sesión en [!DNL Oracle Eloqua]](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-user/Help/Administration/Tasks/SigningInToEloqua.htm#Signing) para obtener instrucciones.

## Mecanismos de protección {#guardrails}

>[!NOTE]
>
>* [!DNL Oracle Eloqua] campos de contacto personalizados se crean automáticamente con los nombres de las audiencias seleccionadas durante el paso **[!UICONTROL Select segments]**.

* [!DNL Oracle Eloqua] tiene un límite máximo de 250 campos de contacto personalizados.
* Antes de exportar nuevas audiencias, asegúrese de que el número de audiencias de Experience Platform y el número de audiencias existentes dentro de [!DNL Oracle Eloqua] no superen este límite.
* Si se supera este límite, se producirá un error al Experience Platform. Esto se debe a que la [!DNL Oracle Eloqua] API no valida el solicitud y responde con un - *400: Hubo un error* de validación - mensaje de error que describe el problema.
* Si ha alcanzado el límite especificado anteriormente, debe eliminar las asignaciones existentes de su destino y eliminar los campos de contacto personalizados correspondientes en su [!DNL Oracle Eloqua] cuenta antes de poder exportar más segmentos.

* Consulte la página [[!DNL Oracle Eloqua] Creando campos de contacto](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-user/Help/ContactFields/Tasks/CreatingContactFields.htm) para obtener información sobre los límites adicionales.

## Identidades admitidas {#supported-identities}

[!DNL Oracle Eloqua] Admite la actualización de identidades descrita en la tabla siguiente. Obtenga más información sobre [las identidades](/help/identity-service/features/namespaces.md).

| Target Identidad | Descripción | Obligatorio |
|---|---|---|
| `EloquaId` | Identificador único del contacto. | Sí |

## Tipo y frecuencia de exportación {#export-type-frequency}

Consulte la tabla siguiente para obtener información sobre el tipo y la frecuencia de exportación de destino.

| Elemento | Tipo | Notas |
|---------|----------|---------|
| Tipo de exportación | **[!UICONTROL Profile-based]** | <ul><li>Va a exportar todos los miembros de un segmento, junto con los campos de esquema deseados *(por ejemplo: dirección de correo electrónico, número de teléfono, apellidos)*, según la asignación de campos.</li><li> Para cada audiencia seleccionada en Experience Platform, el estado del segmento [!DNL Oracle Eloqua] correspondiente se actualiza con su estado de audiencia de Experience Platform.</li></ul> |
| Frecuencia de exportación | **[!UICONTROL Streaming]** | <ul><li>Los destinos de streaming son conexiones basadas en API &quot;siempre activadas&quot;. Tan pronto como se actualiza un perfil en Experience Platform basado en la evaluación de audiencias, el conector envía la actualización de forma descendente a la plataforma de destino. Más información sobre [destinos de streaming](/help/destinations/destination-types.md#streaming-destinations).</li></ul> |

{style="table-layout:auto"}

## Conectar con el destino {#connect}

>[!IMPORTANT]
>
>Para conectarse al destino, necesita los **[!UICONTROL View Destinations]** y **[!UICONTROL Manage Destinations]** [permisos de control de acceso](/help/access-control/home.md#permissions). Lea la [descripción general del control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Para conectarse a este destino, siga los pasos descritos en el [tutorial de configuración de destino](../../ui/connect-destination.md). En el flujo de trabajo de configuración de destino, rellene los campos enumerados en las dos secciones siguientes.

En **[!UICONTROL Destinations]** > **[!UICONTROL Catalog]** buscar [!DNL (API) Oracle Eloqua]. También puede ubicarlo en la categoría **[!UICONTROL Email Marketing]**.

### Autenticarse en el destino {#authenticate}

>[!CONTEXTUALHELP]
>id="platform_destinations_apioracleeloqua_companyname_username"
>title="Nombre de la compañía\Nombre de usuario"
>abstract="Rellene este campo con el nombre de la compañía y el nombre de usuario de Oracle Eloqua en el formulario `{COMPANY_NAME}\{USERNAME}`"

Rellene los campos obligatorios siguientes. Consulte la sección [Recopilar [!DNL Oracle Eloqua] credenciales](#gather-credentials) para obtener instrucciones.

* **[!UICONTROL Password]**: la contraseña de su cuenta de [!DNL Oracle Eloqua].
* **[!UICONTROL Username]**: una cadena concatenada compuesta por el nombre de la [!DNL Oracle Eloqua] empresa y el nombre de usuario [!DNL Oracle Eloqua] .<br>El valor concatenado adopta la forma de `{COMPANY_NAME}\{USERNAME}`.<br> Tenga en cuenta que no utilice aparatos ortopédicos ni espacios, y conserve el `\`archivo . <br>Por ejemplo, si el [!DNL Oracle Eloqua] nombre de la empresa es `MyCompany` y [!DNL Oracle Eloqua] el nombre de usuario es `Username`, el valor concatenado que utilizará en el **[!UICONTROL Username]** campo es `MyCompany\Username`.

Para autenticarse en el destino, seleccione **[!UICONTROL Connect to destination]**.
![Experience Platform IU captura de pantalla muestra cómo autenticarse.](../../assets/catalog/email-marketing/oracle-eloqua-api/authenticate-destination.png)

Si los detalles proporcionados son válidos, el IU muestra un **[!UICONTROL Connected]** estado con una marca de verificación verde. A continuación, puede continuar con el paso siguiente.

### Rellenar detalles de destino {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_apioracleeloqua_pod"
>title="Pod"
>abstract="Para encontrar su número de pod, inicie sesión en Oracle Eloqua. Tenga en cuenta la dirección URL en el explorador después de iniciar sesión correctamente. "

<!-- >additional-url="https://support.oracle.com/knowledge/Oracle%20Cloud/2307176_1.html" text="Oracle Knowledge base - find out your Pod number" -->

Para configurar los detalles del destino, rellene los campos obligatorios y opcionales a continuación. Un asterisco junto a un campo en la interfaz de usuario indica que el campo es obligatorio.
![Experience Platform IU captura de pantalla mostrar los detalles del destino.](../../assets/catalog/email-marketing/oracle-eloqua-api/destination-details.png)

* **[!UICONTROL Name]**: nombre con el que reconocerá este destino en el futuro.
* **[!UICONTROL Description]**: una descripción que le ayudará a identificar este destino en el futuro.
* **[!UICONTROL Pod]**: para obtener en qué `pod` se encuentra, inicie sesión en [!DNL Oracle Eloqua] y anote la dirección URL en su explorador después de haber iniciado sesión correctamente. Por ejemplo, si la dirección URL del explorador es `secure.p01.eloqua.com`, el valor `pod` que debe seleccionar es `p01`. Consulte la sección [Recopilar [!DNL Oracle Eloqua] credenciales](#gather-credentials) para obtener instrucciones adicionales.

### Habilitar alertas {#enable-alerts}

Puede activar alertas para recibir notificaciones sobre el estado del flujo de datos hacia su destino. Seleccione una alerta de la lista a suscribirse para recibir notificaciones sobre el estado del flujo de datos. Para obtener más información sobre las alertas, consulte la guía sobre [suscripción a alertas de destinos mediante la interfaz de usuario](../../ui/alerts.md).

Cuando haya terminado de proporcionar detalles para la conexión de destino, seleccione **[!UICONTROL Next]**.

## Activar públicos en este destino {#activate}

>[!IMPORTANT]
> 
>* Para activar los datos, necesita los **[!UICONTROL View Destinations]** permisos **[!UICONTROL Activate Destinations]** , **[!UICONTROL View Profiles]**, **[!UICONTROL View Segments]**, y [ ](/help/access-control/home.md#permissions)control de acceso. Lea la control de acceso descripción general[ o póngase en contacto con el ](/help/access-control/ui/overview.md)administrador del producto para obtener los permisos necesarios.
>* Para exportar *identidades*, necesita el **[!UICONTROL View Identity Graph]** [permiso de control de acceso](/help/access-control/home.md#permissions). <br> ![Seleccione el área de nombres de identidad resaltada en el flujo de trabajo para activar audiencias en los destinos.](/help/destinations/assets/overview/export-identities-to-destination.png "Seleccione el área de nombres de identidad resaltada en el flujo de trabajo para activar audiencias en los destinos."){width="100" zoomable="yes"}

Lea [Activar perfiles y audiencias en destinos de exportación de audiencias de streaming](/help/destinations/ui/activate-segment-streaming-destinations.md) para obtener instrucciones sobre cómo activar audiencias en este destino.

### Consideraciones sobre asignación y ejemplo {#mapping-considerations-example}

Para enviar correctamente los datos de audiencia de Adobe Experience Platform al destino [!DNL Oracle Eloqua], debe pasar por el paso de asignación de campos. La asignación consiste en crear un vincular entre el Modelo de datos de experiencia (XDM) esquema los campos del cuenta de Experience Platform y sus equivalentes correspondientes del destino destino.

Para asignar los campos XDM a los campos de [!DNL Oracle Eloqua] destino, seguir estos pasos:

1. En el paso **[!UICONTROL Mapping]**, seleccione **[!UICONTROL Add new mapping]**. Verá una nueva fila de asignación en la pantalla.
1. En la ventana **[!UICONTROL Select source field]**, elija la categoría **[!UICONTROL Select attributes]** y seleccione el atributo XDM o elija **[!UICONTROL Select identity namespace]** y seleccione una identidad.
1. En la ventana **[!UICONTROL Select target field]**, elija **[!UICONTROL Select identity namespace]** y seleccione una identidad, o bien elija **[!UICONTROL Select custom attributes]** y escriba el nombre de atributo deseado en el campo **[!UICONTROL Attribute name]**. El nombre de atributo que proporcione debe coincidir con un atributo de contacto existente en [!DNL Oracle Eloqua]. Consulte [[!DNL create a contact]](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/op-api-rest-1.0-data-contact-post.html) los nombres de atributo exactos que puede utilizar en [!DNL Oracle Eloqua].

   * Repita estos pasos para agregar las asignaciones de atributos necesarias y las deseadas entre su esquema de perfil XDM y :[!DNL Oracle Eloqua]

     | Campo de origen | Campo de destino | Obligatorio |
     |---|---|---|
     | `IdentityMap: Eid` | `Identity: EloquaId` | Sí |
     | `xdm: personalEmail.address` | `Attribute: emailAddress` | Sí |
     | `xdm: personName.firstName` | `Attribute: firstName` | |
     | `xdm: personName.lastName` | `Attribute: lastName` | |
     | `xdm: workAddress.street1` | `Attribute: address1` | |
     | `xdm: workAddress.street2` | `Attribute: address2` | |
     | `xdm: workAddress.street3` | `Attribute: address3` | |
     | `xdm: workAddress.postalCode` | `Attribute: postalCode` | |
     | `xdm: workAddress.country` | `Attribute: country` | |
     | `xdm: workAddress.city` | `Attribute: city` | |

   * A continuación, se muestra un ejemplo con las asignaciones anteriores:
     ![Ejemplo de captura de pantalla de IU de Experience Platform con asignaciones de atributos.](../../assets/catalog/email-marketing/oracle-eloqua-api/mappings.png)

>[!IMPORTANT]
>
>* Los atributos especificados en **[!UICONTROL Target field]** deben tener exactamente el nombre especificado en [[!DNL Create a contact]](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/op-api-rest-1.0-data-contact-post.html), ya que formarán el cuerpo de la solicitud.
>* Los atributos especificados en **[!UICONTROL Source field]** no siguen ninguna restricción de este tipo. Puede asignarlo según sus necesidades. Sin embargo, si el formato de datos no es correcto cuando se inserta en [!DNL Oracle Eloqua], se producirá un error. Por ejemplo, puede asignar el área de nombres de identidad **[!UICONTROL Source field]** `contact key`, `ABC ID`, etc. a **[!UICONTROL Target field]** : `EloquaId` después de asegurarse de que los valores de ID coinciden con el formato aceptado por [!DNL Oracle Eloqua].
>* La asignación `EloquaID` es obligatoria para actualizar los atributos correspondientes a la identidad.
>* Se requiere la asignación `emailAddress`. Sin ella, la API genera un error como se muestra a continuación:
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

Cuando termine de proporcionar las asignaciones para la conexión de destino, seleccione **[!UICONTROL Next]**.

>[!NOTE]
>
>El destino sufijo automáticamente un identificador único a los nombres de audiencia seleccionados en cada ejecución al enviar la información del campo de contacto a [!DNL Oracle Eloqua]. Esto garantiza que los nombres de los campos de contacto correspondientes a sus nombres de audiencia no se superpongan. Consulte el ejemplo de captura de pantalla de la sección [Validar exportación de datos](#exported-data) de una página de detalles de contacto de [!DNL Oracle Eloqua] con un campo de contacto personalizado creado con los nombres de audiencia.

## Validar exportación de datos {#exported-data}

Para comprobar que ha configurado correctamente el destino, siga los pasos a continuación:

1. Seleccione **[!UICONTROL Destinations]** > **[!UICONTROL Browse]** y vaya a la lista de destinos.
1. A continuación, seleccione el destino y cambie a la pestaña **[!UICONTROL Activation data]**; luego, seleccione un nombre de audiencia.
   ![Ejemplo de captura de pantalla de la IU de Experience Platform que muestra datos de activación de destinos.](../../assets/catalog/email-marketing/oracle-eloqua-api/destinations-activation-data.png)

1. Monitorice el resumen de audiencia y asegúrese de que el recuento de perfiles corresponde al recuento dentro del segmento.
   ![Ejemplo de captura de pantalla de la IU de Experience Platform que muestra el segmento.](../../assets/catalog/email-marketing/oracle-eloqua-api/segment.png)

1. Inicie sesión en el sitio web de [!DNL Oracle Eloqua] y luego vaya a la página de **[!UICONTROL Contacts Overview]** para comprobar si se han agregado los perfiles de la audiencia. Para ver el estado de la audiencia, explore en profundidad una página de **[!UICONTROL Contact Detail]** y compruebe si se ha creado el campo de contacto con el nombre de audiencia seleccionado como prefijo.

![Captura de pantalla de la interfaz de usuario de Oracle Eloqua que muestra la página Detalles de contacto con el campo de contacto personalizado creado con el nombre de la audiencia.](../../assets/catalog/email-marketing/oracle-eloqua-api/contact.png)

## Uso de datos y gobernanza {#data-usage-governance}

Todos los [!DNL Adobe Experience Platform] destinos cumplen con las políticas de uso de datos al manejar sus datos. Para obtener información detallada sobre cómo [!DNL Adobe Experience Platform] se aplica el gobierno de datos, consulte Información general[ sobre el ](/help/data-governance/home.md)gobierno de datos.

## Errores y solución de problemas {#errors-and-troubleshooting}

Al crear el destino, es posible que reciba uno de los siguientes mensajes de error: `400: There was a validation error` o `400 BAD_REQUEST`. Esto sucede cuando excede el límite de 250 campos de contacto personalizados, como se describe en la [sección de](#guardrails) barandillas. Para solucionar este error, asegúrese de que no está superando el límite del campo de contacto personalizado en [!DNL Oracle Eloqua].
![Experience Platform IU captura de pantalla mostrando un error.](../../assets/catalog/email-marketing/oracle-eloqua-api/error.png)

Consulte las páginas [[!DNL Oracle Eloqua] Códigos de estado HTTP](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/APIRequests_HTTPStatusCodes.html) y [[!DNL Oracle Eloqua] Errores de validación](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/APIRequests_HTTPValidationErrors.html) para obtener una lista completa del estado y los códigos de error con explicaciones.

## Recursos adicionales {#additional-resources}

Para obtener más información, consulte la documentación de [!DNL Oracle Eloqua]:

* [Automatización de marketing Oracle Eloqua](https://docs.oracle.com/en/cloud/saas/marketing/eloqua.html)
* [API de REST para el servicio Oracle Eloqua Marketing Cloud](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/rest-endpoints.html)

### Changelog

Esta sección recoge la funcionalidad y las actualizaciones significativas de la documentación realizadas en este conector de destino.

+++ Ver registro de cambios

| Mes de lanzamiento | Tipo de actualización | Descripción |
|---|---|---|
| Abril de 2023 | Actualización de documentación  | <ul><li>Actualizamos la [sección de casos](#use-cases) de uso con un ejemplo más claro de cuándo los clientes se beneficiarían del uso de este destino.</li> <li>Actualizamos la [sección de mapeo](#mapping-considerations-example) con ejemplos claros de mapeos obligatorios y opcionales.</li> <li>Hemos actualizado la [sección Conectar al destino](#connect) con un ejemplo sobre cómo construir el valor concatenado para el **[!UICONTROL Username]** campo mediante el nombre de empresa [!DNL Oracle Eloqua] y el nombre de [!DNL Oracle Eloqua] usuario. (PLATIR-28343)</li><li>Actualizamos las secciones [Recopilar [!DNL Oracle Eloqua] credenciales](#gather-credentials) y [Rellenar detalles de destino](#destination-details) con instrucciones sobre la selección de [!DNL Oracle Eloqua] **[!UICONTROL Pod]**. El valor *&quot;Pod&quot;* lo usa el destino para construir la dirección URL base para las llamadas a la API. La sección [[!DNL Oracle Eloqua] requisitos previos](#prerequisites-destination) también se actualizó con instrucciones para asignar *&quot;Usuarios avanzados - Permisos de marketing&quot;* como *&quot;Grupos de seguridad&quot;* necesarios para su instancia de [!DNL Oracle Eloqua].</li></ul> |
| Marzo de 2023 | Versión inicial | Versión de destino inicial y publicación de documentación. |

{style="table-layout:auto"}

+++
