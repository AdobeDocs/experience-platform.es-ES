---
title: Conexión de Zendesk
description: El destino de Zendesk le permite exportar los datos de su cuenta y activarlos dentro de Zendesk para sus necesidades comerciales.
source-git-commit: 6a54926e47fb2364475dbf71593de97b642163d5
workflow-type: tm+mt
source-wordcount: '1340'
ht-degree: 1%

---

# [!DNL Zendesk] conexión

[[!DNL Zendesk]](https://www.zendesk.com) es una solución de servicio al cliente y una herramienta de ventas.

Esta [!DNL Adobe Experience Platform] [destino](/help/destinations/home.md) aprovecha el [[!DNL Zendesk] API de contactos](https://developer.zendesk.com/api-reference/sales-crm/resources/contacts/), para crear y actualizar identidades dentro de un segmento como contactos dentro de [!DNL Zendesk].

[!DNL Zendesk] utiliza tokens de portador como mecanismo de autenticación para comunicarse con el [!DNL Zendesk] API de contactos. Instrucciones para autenticarse en su [!DNL Zendesk] más abajo, en la sección [Autenticar en el destino](#authenticate) sección.

## Casos de uso {#use-cases}

Como experto en marketing, puede ofrecer experiencias personalizadas a los usuarios en función de los atributos de sus perfiles de Adobe Experience Platform. Puede generar segmentos a partir de los datos sin conexión y enviarlos a [!DNL Zendesk], para que se muestren en las fuentes de los usuarios en cuanto los segmentos y perfiles se actualicen en Adobe Experience Platform.

## Requisitos previos {#prerequisites}

### Requisitos previos del Experience Platform {#prerequisites-in-experience-platform}

Antes de activar los datos en [!DNL Zendesk] destino, debe tener un [esquema](/help/xdm/schema/composition.md), a [conjunto de datos](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=en), y [segmentos](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=en) creado en [!DNL Experience Platform].

Consulte la documentación del Experience Platform para [Grupo de campos de esquema Detalles de pertenencia a segmento](/help/xdm/field-groups/profile/segmentation.md) si necesita orientación sobre los estados de los segmentos.

### [!DNL Zendesk] requisitos previos {#prerequisites-destination}

Para exportar datos de Platform a su [!DNL Zendesk] cuenta necesita tener un [!DNL Zendesk] cuenta.

#### Reunir [!DNL Zendesk] credenciales {#gather-credentials}

Tenga en cuenta los elementos siguientes antes de autenticarse en el [!DNL Zendesk] destino:

| Credencial | Descripción | Ejemplo |
| --- | --- | --- |
| `Bearer token` | El token de acceso que ha generado en su [!DNL Zendesk] cuenta. <br> Siga la documentación para [generar un [!DNL Zendesk] token de acceso](https://developer.zendesk.com/documentation/sales-crm/first-call/#1-generate-an-access-token) si no tiene uno. | `a0b1c2d3e4...v20w21x22y23z` |

## Mecanismos de protección {#guardrails}

El [Precios y límites de tarifa](https://developer.zendesk.com/api-reference/sales-crm/rate-limits/#pricing) La página detalla [!DNL Zendesk] Límites de API asociados a su cuenta. Debe asegurarse de que los datos y la carga útil se encuentren dentro de estas restricciones.

## Identidades admitidas {#supported-identities}

[!DNL Zendesk] admite la actualización de identidades que se describe en la tabla siguiente. Más información sobre [identidades](/help/identity-service/namespaces.md).

| Identidad de destino | Ejemplo | Descripción | Obligatorio |
|---|---|---|---|
| `email` | `test@test.com` | Dirección de correo electrónico del contacto. | Sí |

## Tipo y frecuencia de exportación {#export-type-frequency}

Consulte la tabla siguiente para obtener información sobre el tipo y la frecuencia de exportación de destino.

| Elemento | Tipo | Notas |
---------|----------|---------|
| Tipo de exportación | **[!UICONTROL Basado en perfiles]** | <ul><li>Está exportando todos los miembros de un segmento, junto con los campos de esquema deseados *(por ejemplo: dirección de correo electrónico, número de teléfono, apellidos)*, según la asignación de campo.</li><li> Cada estado del segmento en [!DNL Zendesk] se actualiza con el estado del segmento correspondiente de Platform, en función de la variable **[!UICONTROL ID de asignación]** valor proporcionado durante la [programación de segmentos](#schedule-segment-export-example) paso.</li></ul> |
| Frecuencia de exportación | **[!UICONTROL Transmisión]** | <ul><li>Los destinos de streaming son conexiones basadas en API &quot;siempre activadas&quot;. Tan pronto como se actualiza un perfil en Experience Platform según la evaluación de segmentos, el conector envía la actualización de forma descendente a la plataforma de destino. Más información sobre [destinos de streaming](/help/destinations/destination-types.md#streaming-destinations).</li></ul> |

{style="table-layout:auto"}

## Conectar con el destino {#connect}

>[!IMPORTANT]
>
>Para conectarse al destino, necesita el **[!UICONTROL Administrar destinos]** [permiso de control de acceso](/help/access-control/home.md#permissions). Lea el [información general de control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Para conectarse a este destino, siga los pasos descritos en la sección [tutorial de configuración de destino](../../ui/connect-destination.md). En el flujo de trabajo de configuración de destino, rellene los campos enumerados en las dos secciones siguientes.

En **[!UICONTROL Destinos]** > **[!UICONTROL Catálogo]** buscar [!DNL Zendesk]. También puede encontrarlo en la sección **[!UICONTROL CRM]** categoría.

### Autenticar en el destino {#authenticate}

Rellene los campos obligatorios siguientes. Consulte la [Reunir [!DNL Zendesk] credenciales](#gather-credentials) para obtener cualquier guía.
* **[!UICONTROL Token de portador]**: El token de acceso que ha generado en su [!DNL Zendesk] cuenta.

Para autenticarse en el destino, seleccione **[!UICONTROL Conectar con destino]**.
![Captura de pantalla de la IU de Platform que muestra cómo autenticarse.](../../assets/catalog/crm/zendesk/authenticate-destination.png)

Si los detalles proporcionados son válidos, la interfaz de usuario muestra un **[!UICONTROL Conectado]** estado con una marca de verificación verde. A continuación, puede continuar con el paso siguiente.

### Rellenar detalles de destino {#destination-details}

Para configurar los detalles del destino, rellene los campos obligatorios y opcionales a continuación. Un asterisco junto a un campo en la interfaz de usuario indica que el campo es obligatorio.
![Captura de pantalla de la IU de Platform que muestra los detalles del destino.](../../assets/catalog/crm/zendesk/destination-details.png)

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

Para enviar correctamente los datos de audiencia de Adobe Experience Platform a [!DNL Zendesk] destino, debe ir a través del paso de asignación de campos. La asignación consiste en crear un vínculo entre los campos de esquema del Modelo de datos de experiencia (XDM) en la cuenta de Platform y sus equivalentes correspondientes desde el destino de destino.

Atributos especificados en la variable **[!UICONTROL Campo de destino]** debe tener exactamente el nombre descrito en la tabla de asignaciones de atributos, ya que estos atributos formarán el cuerpo de la solicitud.

Atributos especificados en la variable **[!UICONTROL Campo de origen]** no siga ninguna de estas restricciones. Puede asignarlo según sus necesidades, pero si el formato de datos no es correcto cuando se inserta en [!DNL Zendesk] se producirá un error.

Para asignar correctamente los campos XDM a [!DNL Zendesk] campos de destino, siga estos pasos:

1. En el **[!UICONTROL Asignación]** paso, seleccione **[!UICONTROL Añadir nueva asignación]**. Verá una nueva fila de asignación en la pantalla.
1. En el **[!UICONTROL Seleccionar campo de origen]** , seleccione la **[!UICONTROL Seleccionar atributos]** y seleccione el atributo XDM o elija el **[!UICONTROL Seleccionar área de nombres de identidad]** y seleccione una identidad.
1. En el **[!UICONTROL Seleccionar campo de destino]** , seleccione la **[!UICONTROL Seleccionar área de nombres de identidad]** y seleccione una identidad o elija **[!UICONTROL Seleccionar atributos personalizados]** y seleccione un atributo según sea necesario.
   * Repita estos pasos para agregar las siguientes asignaciones entre el esquema de perfil XDM y su [!DNL Zendesk] instancia: |Campo de origen|Campo de destino| obligatorio| |—|—|—| |`xdm: person.name.lastName`|`Attribute: last_name` <br>o `Attribute: name`| Sí | |`IdentityMap: Email`|`Identity: email`| Sí |

   * A continuación se muestra un ejemplo con estas asignaciones:
      ![Ejemplo de captura de pantalla de la IU de Platform con asignaciones de atributos.](../../assets/catalog/crm/zendesk/mappings.png)

      >[!IMPORTANT]
      >
      >Ambas asignaciones de campo de destino son obligatorias y necesarias para [!DNL Zendesk] para trabajar.
      >
      >La asignación para *Apellidos* o *Nombre* es necesario; de lo contrario, la variable [!DNL Zendesk] La API no responde con ningún error y se ignora cualquier valor de atributo pasado.

Cuando haya terminado de proporcionar las asignaciones para la conexión de destino, seleccione **[!UICONTROL Siguiente]**.

### Programar exportación de segmentos y ejemplo {#schedule-segment-export-example}

En el [[!UICONTROL Programar exportación de segmentos]](/help/destinations/ui/activate-segment-streaming-destinations.md#scheduling) del flujo de trabajo de activación, debe asignar manualmente los segmentos de Platform al atributo de campo personalizado en [!DNL Zendesk].

Para ello, seleccione cada segmento e introduzca el atributo de campo personalizado correspondiente en [!DNL Zendesk] en el **[!UICONTROL ID de asignación]** field.

A continuación se muestra un ejemplo:
![Captura de pantalla de la IU de Platform que muestra Programar exportación de segmentos.](../../assets/catalog/crm/zendesk/schedule-segment-export.png)

## Validar exportación de datos {#exported-data}

Para comprobar que ha configurado correctamente el destino, siga los pasos a continuación:

1. Seleccionar **[!UICONTROL Destinos]** > **[!UICONTROL Examinar]** y vaya a la lista de destinos.
1. A continuación, seleccione el destino y cambie a **[!UICONTROL Datos de activación]** y, a continuación, seleccione un nombre de segmento.
   ![Captura de pantalla de la IU de Platform que muestra los datos de activación de destinos.](../../assets/catalog/crm/zendesk/destinations-activation-data.png)

1. Monitorice el resumen del segmento y asegúrese de que el recuento de perfiles corresponda al recuento dentro del segmento.
   ![Captura de pantalla de la IU de Platform que muestra el segmento.](../../assets/catalog/crm/zendesk/segment.png)

1. Inicie sesión en [!DNL Zendesk] sitio web y, a continuación, vaya al **[!UICONTROL Contactos]** para comprobar si se han añadido los perfiles del segmento. Esta lista se puede configurar para mostrar columnas para los campos adicionales creados con el segmento **[!UICONTROL ID de asignación]** y estados de segmentos.
   ![Captura de pantalla de la IU de Zendesk que muestra la página Contactos con los campos adicionales creados con el nombre del segmento.](../../assets/catalog/crm/zendesk/contacts.png)

1. También puede explorar en profundidad un individuo **[!UICONTROL Persona]** y marque la **[!UICONTROL Campos adicionales]** sección que muestra el nombre y los estados del segmento.
   ![Captura de pantalla de la interfaz de usuario de Zendesk que muestra la página Persona con la sección de campos adicionales que muestra el nombre del segmento y los estados del segmento.](../../assets/catalog/crm/zendesk/contact.png)

## Uso de datos y gobernanza {#data-usage-governance}

Todo [!DNL Adobe Experience Platform] Los destinos de cumplen con las políticas de uso de datos al gestionar los datos. Para obtener información detallada sobre cómo [!DNL Adobe Experience Platform] aplica la gobernanza de datos. Consulte la [Resumen de gobernanza de datos](/help/data-governance/home.md).

## Recursos adicionales {#additional-resources}

Información útil adicional del [!DNL Zendesk] Esta documentación es:
* [Realización de la primera llamada](https://developer.zendesk.com/documentation/sales-crm/first-call/)
* [Campos personalizados](https://developer.zendesk.com/api-reference/sales-crm/requests/#custom-fields)