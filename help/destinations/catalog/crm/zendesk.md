---
title: Conexión de Zendesk
description: El destino de Zendesk le permite exportar los datos de su cuenta y activarlos dentro de Zendesk para sus necesidades comerciales.
last-substantial-update: 2023-03-14T00:00:00Z
exl-id: e7fcbbf4-5d6c-4abb-96cb-ea5b67a88711
source-git-commit: 5aefa362d7a7d93c12f9997d56311127e548497e
workflow-type: tm+mt
source-wordcount: '1469'
ht-degree: 3%

---

# [!DNL Zendesk] conexión

[[!DNL Zendesk]](https://www.zendesk.com) es una solución de servicio al cliente y una herramienta de ventas.

Este [!DNL Adobe Experience Platform] [destino](/help/destinations/home.md) aprovecha la API [[!DNL Zendesk] Contactos](https://developer.zendesk.com/api-reference/sales-crm/resources/contacts/) para **crear y actualizar identidades** dentro de una audiencia como contactos dentro de [!DNL Zendesk].

[!DNL Zendesk] usa tokens de portador como mecanismo de autenticación para comunicarse con la API de contactos de [!DNL Zendesk]. Las instrucciones para autenticarse en su instancia de [!DNL Zendesk] se encuentran más abajo, en la sección [Autenticar en destino](#authenticate).

## Casos de uso {#use-cases}

El departamento de servicio al cliente de una plataforma B2C multicanal quiere garantizar una experiencia personalizada sin problemas para sus clientes. El departamento puede crear audiencias a partir de sus propios datos sin conexión para crear nuevos perfiles de usuario o actualizar la información de perfil existente de diferentes interacciones (por ejemplo, compras, devoluciones, etc.) y enviar estas audiencias desde Adobe Experience Platform a [!DNL Zendesk]. Tener la información actualizada en [!DNL Zendesk] garantiza que el agente de servicio al cliente tenga disponible de inmediato la información reciente del cliente, lo que permite respuestas y resolución más rápidas.

## Requisitos previos {#prerequisites}

### Requisitos previos del Experience Platform {#prerequisites-in-experience-platform}

Antes de activar datos en el destino [!DNL Zendesk], debe tener un [esquema](/help/xdm/schema/composition.md), un [conjunto de datos](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html) y [segmentos](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html) creados en [!DNL Experience Platform].

Consulte la documentación del Experience Platform para el [grupo de campos de esquema Detalles de pertenencia a audiencias](/help/xdm/field-groups/profile/segmentation.md) si necesita instrucciones sobre los estados de audiencia.

### [!DNL Zendesk] requisitos previos {#prerequisites-destination}

Para exportar datos de Platform a su cuenta de [!DNL Zendesk], necesita tener una cuenta de [!DNL Zendesk].

#### Recopilar [!DNL Zendesk] credenciales {#gather-credentials}

Observe los elementos siguientes antes de autenticarse en el destino [!DNL Zendesk]:

| Credencial | Descripción | Ejemplo |
| --- | --- | --- |
| `Bearer token` | El token de acceso que generó en su cuenta de [!DNL Zendesk]. <br> Siga la documentación para [generar un [!DNL Zendesk] token de acceso](https://developer.zendesk.com/documentation/sales-crm/first-call/#1-generate-an-access-token) si no dispone de uno. | `a0b1c2d3e4...v20w21x22y23z` |

## Mecanismos de protección {#guardrails}

La página [Precios y límites de tarifas](https://developer.zendesk.com/api-reference/sales-crm/rate-limits/#pricing) detalla los límites de API [!DNL Zendesk] asociados con su cuenta. Debe asegurarse de que los datos y la carga útil se encuentren dentro de estas restricciones.

## Identidades admitidas {#supported-identities}

[!DNL Zendesk] admite la actualización de las identidades descritas en la tabla siguiente. Más información sobre [identidades](/help/identity-service/features/namespaces.md).

| Identidad de destino | Ejemplo | Descripción | Obligatorio |
|---|---|---|---|
| `email` | `test@test.com` | Dirección de correo electrónico del contacto. | Sí |

## Tipo y frecuencia de exportación {#export-type-frequency}

Consulte la tabla siguiente para obtener información sobre el tipo y la frecuencia de exportación de destino.

| Elemento | Tipo | Notas |
---------|----------|---------|
| Tipo de exportación | **[!UICONTROL Basado en perfil]** | <ul><li>Va a exportar todos los miembros de un segmento, junto con los campos de esquema deseados *(por ejemplo: dirección de correo electrónico, número de teléfono, apellidos)*, según la asignación de campos.</li><li> Cada estado de segmento de [!DNL Zendesk] se actualiza con el estado de audiencia correspondiente de Platform, según el valor de **[!UICONTROL ID de asignación]** proporcionado durante el paso [programación de audiencia](#schedule-segment-export-example).</li></ul> |
| Frecuencia de exportación | **[!UICONTROL Transmisión]** | <ul><li>Los destinos de streaming son conexiones basadas en API &quot;siempre activadas&quot;. Tan pronto como se actualiza un perfil en Experience Platform según la evaluación de audiencias, el conector envía la actualización de forma descendente a la plataforma de destino. Más información sobre [destinos de streaming](/help/destinations/destination-types.md#streaming-destinations).</li></ul> |

{style="table-layout:auto"}

## Conexión al destino {#connect}

>[!IMPORTANT]
>
>Para conectarse al destino, necesita los **[!UICONTROL permisos de control de acceso](/help/access-control/home.md#permissions) de Ver destinos]** y **[!UICONTROL Administrar destinos]**[5}. Lea la [descripción general del control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Para conectarse a este destino, siga los pasos descritos en el [tutorial de configuración de destino](../../ui/connect-destination.md). En el flujo de trabajo de configuración de destino, rellene los campos enumerados en las dos secciones siguientes.

En **[!UICONTROL destinos]** > **[!UICONTROL catálogo]**, busque [!DNL Zendesk]. También puede ubicarlo en la categoría **[!UICONTROL CRM]**.

### Autenticarse en el destino {#authenticate}

Rellene los campos obligatorios siguientes. Consulte la sección [Recopilar [!DNL Zendesk] credenciales](#gather-credentials) para obtener instrucciones.
* **[!UICONTROL Token de portador]**: El token de acceso que generó en su cuenta de [!DNL Zendesk].

Para autenticarse en el destino, seleccione **[!UICONTROL Conectarse al destino]**.
![Captura de pantalla de IU de Platform que muestra cómo autenticarse.](../../assets/catalog/crm/zendesk/authenticate-destination.png)

Si los detalles proporcionados son válidos, la interfaz de usuario mostrará el estado **[!UICONTROL Conectado]** con una marca de verificación verde. A continuación, puede continuar con el paso siguiente.

### Rellenar detalles de destino {#destination-details}

Para configurar los detalles del destino, rellene los campos obligatorios y opcionales a continuación. Un asterisco junto a un campo en la interfaz de usuario indica que el campo es obligatorio.
![Captura de pantalla de IU de Platform que muestra los detalles del destino.](../../assets/catalog/crm/zendesk/destination-details.png)

* **[!UICONTROL Nombre]**: Un nombre por el cual reconocerá este destino en el futuro.
* **[!UICONTROL Descripción]**: Una descripción que le ayudará a identificar este destino en el futuro.

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

Para enviar correctamente los datos de audiencia de Adobe Experience Platform al destino [!DNL Zendesk], debe pasar por el paso de asignación de campos. La asignación consiste en crear un vínculo entre los campos de esquema del Modelo de datos de experiencia (XDM) en la cuenta de Platform y sus equivalentes correspondientes desde el destino de destino.

Los atributos especificados en el **[!UICONTROL campo de destino]** deben tener exactamente el nombre descrito en la tabla de asignaciones de atributos, ya que estos atributos formarán el cuerpo de la solicitud.

Los atributos especificados en el **[!UICONTROL campo Source]** no siguen ninguna restricción de este tipo. Puede asignarlo según sus necesidades. Sin embargo, si el formato de datos no es correcto cuando se inserta en [!DNL Zendesk], se producirá un error.

Para asignar correctamente los campos XDM a los campos de destino [!DNL Zendesk], siga estos pasos:

1. En el paso **[!UICONTROL Asignación]**, seleccione **[!UICONTROL Agregar nueva asignación]**. Verá una nueva fila de asignación en la pantalla.
1. En la ventana **[!UICONTROL Seleccionar campo de origen]**, elija la categoría **[!UICONTROL Seleccionar atributos]** y seleccione el atributo XDM o elija **[!UICONTROL Seleccionar área de nombres de identidad]** y seleccione una identidad.
1. En la ventana **[!UICONTROL Seleccionar campo de destino]**, elija la categoría **[!UICONTROL Seleccionar área de nombres de identidad]** y seleccione una identidad de destino, o bien elija la categoría **[!UICONTROL Seleccionar atributos]** y seleccione uno de los atributos de esquema admitidos.

   * Repita estos pasos para agregar las siguientes asignaciones obligatorias, también puede agregar cualquier otro atributo que desee actualizar entre el esquema de perfil XDM y la instancia [!DNL Zendesk]:

     | Campo de origen | Campo de destino | Obligatorio |
     |---|---|---|
     | `xdm: person.name.lastName` | `xdm: last_name` | Sí |
     | `IdentityMap: Email` | `Identity: email` | Sí |
     | `xdm: person.name.firstName` | `xdm: first_name` | |

   * A continuación se muestra un ejemplo con estas asignaciones:
     ![Ejemplo de captura de pantalla de IU de plataforma con asignaciones de atributos.](../../assets/catalog/crm/zendesk/mappings.png)

>[!IMPORTANT]
>
>Las asignaciones de destino `Attribute: last_name` y `Identity: email` son obligatorias para este destino. Si faltan estas asignaciones, se omitirán las demás asignaciones y no se enviarán a [!DNL Zendesk].

Cuando termine de proporcionar las asignaciones para la conexión de destino, seleccione **[!UICONTROL Siguiente]**.

### Programar exportación de audiencias y ejemplo {#schedule-segment-export-example}

En el paso [[!UICONTROL Programar exportación de audiencias]](/help/destinations/ui/activate-segment-streaming-destinations.md#scheduling) del flujo de trabajo de activación, debe asignar manualmente las audiencias de Platform al atributo de campo personalizado en [!DNL Zendesk].

Para ello, seleccione cada segmento e introduzca el atributo de campo personalizado correspondiente de [!DNL Zendesk] en el campo **[!UICONTROL ID de asignación]**.

A continuación se muestra un ejemplo:
![Ejemplo de captura de pantalla de la IU de Platform que muestra Programar exportación de audiencias.](../../assets/catalog/crm/zendesk/schedule-segment-export.png)

## Validar exportación de datos {#exported-data}

Para comprobar que ha configurado correctamente el destino, siga los pasos a continuación:

1. Seleccione **[!UICONTROL Destinos]** > **[!UICONTROL Examinar]** y vaya a la lista de destinos.
1. A continuación, seleccione el destino y cambie a la ficha **[!UICONTROL Datos de activación]** y, a continuación, seleccione un nombre de audiencia.
   ![Ejemplo de captura de pantalla de IU de Platform que muestra datos de activación de destinos.](../../assets/catalog/crm/zendesk/destinations-activation-data.png)

1. Monitorice el resumen de audiencia y asegúrese de que el recuento de perfiles corresponde al recuento dentro del segmento.
   ![Ejemplo de captura de pantalla de IU de Platform que muestra el segmento.](../../assets/catalog/crm/zendesk/segment.png)

1. Inicie sesión en el sitio web de [!DNL Zendesk] y luego vaya a la página de **[!UICONTROL Contactos]** para comprobar si se han agregado los perfiles de la audiencia. Esta lista se puede configurar para mostrar columnas para los campos adicionales creados con la audiencia**[!UICONTROL ID de asignación]** y los estados de audiencia.
   ![Captura de pantalla de la interfaz de usuario de Zendesk que muestra la página Contactos con los campos adicionales creados con el nombre de audiencia.](../../assets/catalog/crm/zendesk/contacts.png)

1. También puede explorar en profundidad una página individual de **[!UICONTROL Persona]** y comprobar la sección de **[!UICONTROL Campos adicionales]** que muestra el nombre de la audiencia y los estados de la audiencia.
   ![Captura de pantalla de la interfaz de usuario de Zendesk que muestra la página Persona con la sección de campos adicionales que muestra el nombre y los estados de audiencia.](../../assets/catalog/crm/zendesk/contact.png)

## Uso de datos y gobernanza {#data-usage-governance}

Todos los destinos de [!DNL Adobe Experience Platform] cumplen con las políticas de uso de datos al administrar los datos. Para obtener información detallada sobre cómo [!DNL Adobe Experience Platform] aplica el control de datos, consulte la [Información general sobre el control de datos](/help/data-governance/home.md).

## Recursos adicionales {#additional-resources}

A continuación encontrará información útil adicional de la documentación de [!DNL Zendesk]:
* [Realizando tu primera llamada](https://developer.zendesk.com/documentation/sales-crm/first-call/)
* [Campos personalizados](https://developer.zendesk.com/api-reference/sales-crm/requests/#custom-fields)

### Changelog

Esta sección recoge la funcionalidad y las actualizaciones significativas de la documentación realizadas en este conector de destino.

+++ Ver registro de cambios

| Mes de lanzamiento | Tipo de actualización | Descripción |
|---|---|---|
| Abril de 2023 | Actualización de documentación | <ul><li>Hemos actualizado la sección [casos de uso](#use-cases) con un ejemplo más claro de cuándo se beneficiarían los clientes de utilizar este destino.</li> <li>Actualizamos la sección [mapping](#mapping-considerations-example) para reflejar las asignaciones requeridas correctas. Las asignaciones de destino `Attribute: last_name` y `Identity: email` son obligatorias para este destino. Si faltan estas asignaciones, se omitirán las demás asignaciones y no se enviarán a [!DNL Zendesk].</li> <li>Hemos actualizado la sección [asignación](#mapping-considerations-example) con ejemplos claros de asignaciones obligatorias y opcionales.</li></ul> |
| Marzo de 2023 | Versión inicial | Versión de destino inicial y publicación de documentación. |

{style="table-layout:auto"}

+++
