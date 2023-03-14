---
title: (API) Conexión de Oracle Eloqua
description: El Oracle (API) Eloqua permite exportar los datos de la cuenta y activarlos dentro de Oracle Eloqua para satisfacer sus necesidades comerciales.
last-substantial-update: 2023-03-14T00:00:00Z
source-git-commit: 3197eddcf9fef2870589fdf9f09276a333f30cd1
workflow-type: tm+mt
source-wordcount: '1494'
ht-degree: 0%

---

# [!DNL (API) Oracle Eloqua] conexión

[[!DNL Oracle Eloqua]](https://www.oracle.com/cx/marketing/automation/) permite a los especialistas en marketing planificar y ejecutar campañas al tiempo que ofrecen una experiencia del cliente personalizada para sus posibles clientes. Con una administración de posibles clientes integrada y una creación de campañas sencilla, ayuda a los especialistas en marketing a atraer a la audiencia adecuada en el momento adecuado en el recorrido del comprador y se escala de forma elegante para llegar a audiencias de varios canales, incluidos correo electrónico, búsqueda en pantalla, vídeo y móvil. Los equipos de ventas pueden cerrar más acuerdos a una velocidad más rápida, lo que aumenta el retorno de la inversión de marketing a través de una perspectiva en tiempo real.

Esta [!DNL Adobe Experience Platform] [destino](/help/destinations/home.md) aprovecha el [Actualizar un contacto](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/op-api-rest-1.0-data-contact-id-put.html) operación desde el [!DNL Oracle Eloqua] API de REST, que le permite actualizar identidades dentro de un segmento en [!DNL Oracle Eloqua].

[!DNL Oracle Eloqua] utiliza [Autenticación básica](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/Authentication_Basic.html) para comunicarse con el [!DNL Oracle Eloqua] API DE REST. Instrucciones para autenticarse en su [!DNL Oracle Eloqua] más abajo, en la sección [Autenticar en el destino](#authenticate) sección.

## Casos de uso {#use-cases}

Como experto en marketing, puede ofrecer experiencias personalizadas a los usuarios en función de los atributos de sus perfiles de Adobe Experience Platform. Puede generar segmentos a partir de los datos sin conexión y enviarlos a [!DNL Oracle Eloqua], para que se muestren en las fuentes de los usuarios en cuanto los segmentos y perfiles se actualicen en Adobe Experience Platform.

## Requisitos previos {#prerequisites}

### Requisitos previos del Experience Platform {#prerequisites-in-experience-platform}

Antes de activar los datos en [!DNL Oracle Eloqua] destino, debe tener un [esquema](/help/xdm/schema/composition.md), a [conjunto de datos](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=en), y [segmentos](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=en) creado en [!DNL Experience Platform].

Consulte la documentación del Experience Platform para [Grupo de campos de esquema Detalles de pertenencia a segmento](/help/xdm/field-groups/profile/segmentation.md) si necesita orientación sobre los estados de los segmentos.

### [!DNL Oracle Eloqua] requisitos previos {#prerequisites-destination}

Para exportar datos de Platform a su [!DNL Oracle Eloqua] cuenta necesita tener un [!DNL Oracle Eloqua] cuenta.

#### Reunir [!DNL Oracle Eloqua] credenciales {#gather-credentials}

Tenga en cuenta los elementos siguientes antes de autenticarse en el [!DNL Oracle Eloqua] destino:

| Credencial | Descripción |
| --- | --- |
| `Username` | El nombre de usuario de su [!DNL Oracle Eloqua] cuenta. |
| `Password` | La contraseña de su [!DNL Oracle Eloqua] cuenta. |

## Mecanismos de protección {#guardrails}

>[!NOTE]
>
>* [!DNL Oracle Eloqua] los campos de contacto personalizados se crean automáticamente con los nombres de los segmentos seleccionados durante la **[!UICONTROL Seleccionar segmentos]** paso.


* [!DNL Oracle Eloqua] tiene un límite máximo de 250 campos de contacto personalizados.
* Antes de exportar nuevos segmentos, asegúrese de que el número de segmentos de Platform y el número de segmentos existentes dentro de [!DNL Oracle Eloqua] no supere este límite.
* Si se supera este límite, se producirá un error en el Experience Platform. Esto se debe a que [!DNL Oracle Eloqua] La API no puede validar la solicitud y responde con un - *400: Error de validación* - mensaje de error que describe el problema.
* Si ha alcanzado el límite especificado anteriormente, debe eliminar las asignaciones existentes de su destino y eliminar los campos de contacto personalizados correspondientes en su [!DNL Oracle Eloqua] cuenta antes de poder exportar más segmentos.

* Consulte la [Oracle Eloqua Creación de campos de contacto](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-user/Help/ContactFields/Tasks/CreatingContactFields.htm) para obtener información sobre los límites adicionales.

## Identidades admitidas {#supported-identities}

[!DNL Oracle Eloqua] admite la actualización de identidades que se describe en la tabla siguiente. Más información sobre [identidades](/help/identity-service/namespaces.md).

| Identidad de destino | Ejemplo | Descripción | Obligatorio |
|---|---|---|---|
| `EloquaId` | `111111` | Identificador único del contacto. | Sí |

## Conectar con el destino {#connect}

>[!IMPORTANT]
>
>Para conectarse al destino, necesita el **[!UICONTROL Administrar destinos]** [permiso de control de acceso](/help/access-control/home.md#permissions). Lea el [información general de control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Para conectarse a este destino, siga los pasos descritos en la sección [tutorial de configuración de destino](../../ui/connect-destination.md). En el flujo de trabajo de configuración de destino, rellene los campos enumerados en las dos secciones siguientes.

En **[!UICONTROL Destinos]** > **[!UICONTROL Catálogo]** buscar [!DNL (API) Oracle Eloqua]. También puede encontrarlo en la sección **[!UICONTROL Marketing por correo electrónico]** categoría.

### Autenticar en el destino {#authenticate}

Rellene los campos obligatorios siguientes. Consulte la [Reunir [!DNL Oracle Eloqua] credenciales](#gather-credentials) para obtener cualquier guía.
* **[!UICONTROL Contraseña]**: La contraseña de su [!DNL Oracle Eloqua] cuenta.
* **[!UICONTROL Nombre de usuario]**: El nombre de usuario de su [!DNL Oracle Eloqua] cuenta.

Para autenticarse en el destino, seleccione **[!UICONTROL Conectar con destino]**.
![Captura de pantalla de la IU de Platform que muestra cómo autenticarse.](../../assets/catalog/email-marketing/oracle-eloqua-api/authenticate-destination.png)

Si los detalles proporcionados son válidos, la interfaz de usuario muestra un **[!UICONTROL Conectado]** estado con una marca de verificación verde. A continuación, puede continuar con el paso siguiente.

### Rellenar detalles de destino {#destination-details}

Para configurar los detalles del destino, rellene los campos obligatorios y opcionales a continuación. Un asterisco junto a un campo en la interfaz de usuario indica que el campo es obligatorio.
![Captura de pantalla de la IU de Platform que muestra los detalles del destino.](../../assets/catalog/email-marketing/oracle-eloqua-api/destination-details.png)

* **[!UICONTROL Nombre]**: Un nombre con el que reconocerá este destino en el futuro.
* **[!UICONTROL Descripción]**: Una descripción que le ayudará a identificar este destino en el futuro.

### Habilitar alertas {#enable-alerts}

Puede activar alertas para recibir notificaciones sobre el estado del flujo de datos a su destino. Seleccione una alerta de la lista a la que suscribirse para recibir notificaciones sobre el estado del flujo de datos. Para obtener más información sobre las alertas, consulte la guía de [suscripción a alertas de destinos mediante la IU](../../ui/alerts.md).

Cuando haya terminado de proporcionar detalles para la conexión de destino, seleccione **[!UICONTROL Siguiente]**.

## Activar segmentos en este destino {#activate}

>[!IMPORTANT]
>
>Para activar los datos, necesita el **[!UICONTROL Administrar destinos]**, **[!UICONTROL Activar destinos]**, **[!UICONTROL Ver perfiles]**, y **[!UICONTROL Ver segmentos]** [permisos de control de acceso](/help/access-control/home.md#permissions). Lea el [información general de control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Leer [Activación de perfiles y segmentos en destinos de exportación de segmentos de flujo continuo](/help/destinations/ui/activate-segment-streaming-destinations.md) para obtener instrucciones sobre cómo activar segmentos de audiencia en este destino.

### Consideraciones sobre asignación y ejemplo {#mapping-considerations-example}

Para enviar correctamente los datos de audiencia de Adobe Experience Platform a [!DNL Oracle Eloqua] destino, debe ir a través del paso de asignación de campos. La asignación consiste en crear un vínculo entre los campos de esquema del Modelo de datos de experiencia (XDM) en la cuenta de Platform y sus equivalentes correspondientes desde el destino de destino.

`EloquaID` es necesario para actualizar los atributos correspondientes a Identity. El `emailAddress` también es necesario, ya que sin ella la API genera un error como se indica a continuación:

```json
{
   "type":"ObjectValidationError",
   "container":{
      "type":"ObjectKey",
      "objectType":"Contact"
   },
   "property":"emailAddress",
   "requirement":{
      "type":"EmailAddressRequirement"
   },
   "value":"<null>"
}
```

Atributos especificados en la variable **[!UICONTROL Campo de destino]** debe tener exactamente el nombre descrito en la tabla de asignaciones de atributos, ya que estos atributos formarán el cuerpo de la solicitud.

Atributos especificados en la variable **[!UICONTROL Campo de origen]** no siga ninguna de estas restricciones. Puede asignarlo según sus necesidades, pero si el formato de datos no es correcto cuando se inserta en [!DNL Oracle Eloqua] se producirá un error.

Por ejemplo, puede asignar **[!UICONTROL Campo de origen]** área de nombres de identidad `contact key`, `ABC ID` etc. hasta **[!UICONTROL Campo de destino]** : `EloquaID` después de asegurarse de que los valores de ID se ajustan al formato aceptado por [!DNL Oracle Eloqua].

Para asignar correctamente los campos XDM a [!DNL Oracle Eloqua] campos de destino, siga estos pasos:

1. En el **[!UICONTROL Asignación]** paso, seleccione **[!UICONTROL Añadir nueva asignación]**. Verá una nueva fila de asignación en la pantalla.
1. En el **[!UICONTROL Seleccionar campo de origen]** , seleccione la **[!UICONTROL Seleccionar atributos]** y seleccione el atributo XDM o elija el **[!UICONTROL Seleccionar área de nombres de identidad]** y seleccione una identidad.
1. En el **[!UICONTROL Seleccionar campo de destino]** , seleccione la **[!UICONTROL Seleccionar área de nombres de identidad]** y seleccione una identidad o elija **[!UICONTROL Seleccionar atributos personalizados]** y seleccione un atributo según sea necesario.
   * Repita estos pasos para agregar las siguientes asignaciones entre el esquema de perfil XDM y su [!DNL Oracle Eloqua] instancia: |Campo de origen|Campo de destino| obligatorio| |—|—|—| |`xdm: personalEmail.address`|`Attribute: emailAddress`| Sí | |`IdentityMap: Eid`|`Identity: EloquaId`| Sí |

   * A continuación se muestra un ejemplo con estas asignaciones:
      ![Ejemplo de captura de pantalla de la IU de Platform con asignaciones de atributos.](../../assets/catalog/email-marketing/oracle-eloqua-api/mappings.png)

      >[!IMPORTANT]
      >
      >Tanto la `emailAddress` y `EloquaId` las asignaciones de atributos de destino son obligatorias.

Cuando haya terminado de proporcionar las asignaciones para la conexión de destino, seleccione **[!UICONTROL Siguiente]**.

>[!NOTE]
>
>El destino sufijo automáticamente un identificador único a los nombres de segmento seleccionados en cada ejecución al enviar la información del campo de contacto a [!DNL Oracle Eloqua]. Esto garantiza que los nombres de los campos de contacto correspondientes a sus nombres de segmento no se superpongan. Consulte la [Validar exportación de datos](#exported-data) captura de pantalla de sección ejemplo de un [!DNL Oracle Eloqua] Página de detalles del contacto con el campo de contacto personalizado creado con los nombres de los segmentos.

## Validar exportación de datos {#exported-data}

Para comprobar que ha configurado correctamente el destino, siga los pasos a continuación:

1. Seleccionar **[!UICONTROL Destinos]** > **[!UICONTROL Examinar]** y vaya a la lista de destinos.
1. A continuación, seleccione el destino y cambie a **[!UICONTROL Datos de activación]** y, a continuación, seleccione un nombre de segmento.
   ![Captura de pantalla de la IU de Platform que muestra los datos de activación de destinos.](../../assets/catalog/email-marketing/oracle-eloqua-api/destinations-activation-data.png)

1. Monitorice el resumen del segmento y asegúrese de que el recuento de perfiles corresponda al recuento dentro del segmento.
   ![Captura de pantalla de la IU de Platform que muestra el segmento.](../../assets/catalog/email-marketing/oracle-eloqua-api/segment.png)

1. Inicie sesión en [!DNL Oracle Eloqua] sitio web y, a continuación, vaya al **[!UICONTROL Información general de contactos]** para comprobar si se han añadido los perfiles del segmento. Para ver el estado del segmento, explore en profundidad un **[!UICONTROL Detalles de contacto]** y compruebe si se ha creado el campo de contacto con el nombre del segmento seleccionado como prefijo.

![Captura de pantalla de la IU de Eloqua de oracle que muestra la página Detalles de contacto con el campo de contacto personalizado creado con el nombre del segmento.](../../assets/catalog/email-marketing/oracle-eloqua-api/contact.png)

## Uso de datos y gobernanza {#data-usage-governance}

Todo [!DNL Adobe Experience Platform] Los destinos de cumplen con las políticas de uso de datos al gestionar los datos. Para obtener información detallada sobre cómo [!DNL Adobe Experience Platform] aplica la gobernanza de datos. Consulte la [Resumen de gobernanza de datos](/help/data-governance/home.md).

## Errores y solución de problemas {#errors-and-troubleshooting}

Al crear el destino, puede recibir uno de los siguientes mensajes de error: `400: There was a validation error` o `400 BAD_REQUEST`. Esto sucede cuando se supera el límite de 250 campos de contacto personalizados, tal como se describe en la sección [barandas](#guardrails) sección. Para corregir este error, asegúrese de que no supera el límite del campo de contacto personalizado en [!DNL Oracle Eloqua].
![Captura de pantalla de la IU de Platform que muestra un error.](../../assets/catalog/email-marketing/oracle-eloqua-api/error.png)

Consulte la [[!DNL Oracle Eloqua] Códigos de estado HTTP](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/APIRequests_HTTPStatusCodes.html) y [[!DNL Oracle Eloqua] Errores de validación](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/APIRequests_HTTPValidationErrors.html) páginas para obtener una lista completa de estados y códigos de error con explicaciones.

## Recursos adicionales {#additional-resources}

Información útil adicional del [!DNL Oracle ELoqua] Esta documentación es:
* [Oracle Eloqua Marketing Automation](https://docs.oracle.com/en/cloud/saas/marketing/eloqua.html)
* [API de REST para el servicio de Marketing Cloud de Oracle Eloqua](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/rest-endpoints.html)