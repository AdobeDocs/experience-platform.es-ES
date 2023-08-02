---
keywords: mobile; braze; mensajería;
title: Conexión de Braze
description: Braze es una plataforma completa de participación del cliente que potencia experiencias relevantes y memorables entre los clientes y las marcas que aman.
exl-id: 508e79ee-7364-4553-b153-c2c00cc85a73
source-git-commit: 16365865e349f8805b8346ec98cdab89cd027363
workflow-type: tm+mt
source-wordcount: '1040'
ht-degree: 1%

---

# [!DNL Braze] conexión

## Información general {#overview}

El [!DNL Braze] El destino le ayuda a enviar datos de perfil a [!DNL Braze].

[!DNL Braze] es una plataforma completa de participación del cliente que potencia experiencias relevantes y memorables entre los clientes y las marcas que aman.

Para enviar datos de perfil a [!DNL Braze], primero debe conectarse al destino.

## Detalles del destino {#specifics}

Tenga en cuenta los siguientes detalles específicos de [!DNL Braze] destino:

* [!DNL Adobe Experience Platform] Las audiencias de se exportan a [!DNL Braze] en el `AdobeExperiencePlatformSegments` atributo.

>[!NOTE]
>
>Tenga en cuenta que enviar atributos personalizados adicionales a [!DNL Braze] puede causar aumentos en su [!DNL Braze] consumo de puntos de datos. Consulte a su [!DNL Braze] administrador de cuentas antes de enviar atributos personalizados adicionales.

## Casos de uso {#use-cases}

Como especialista en marketing, quiero segmentar usuarios en un destino de participación móvil, con audiencias integradas [!DNL Adobe Experience Platform]. Además, quiero ofrecerles experiencias personalizadas, en función de los atributos de sus [!DNL Adobe Experience Platform] perfiles, en cuanto las audiencias y los perfiles se actualicen en [!DNL Adobe Experience Platform].

## Identidades admitidas {#supported-identities}

[!DNL Braze] admite la activación de identidades descritas en la tabla siguiente.

| Identidad de destino | Descripción | Consideraciones |
|---|---|---|
| external_id | Personalizado [!DNL Braze] identificador que admite la asignación de cualquier identidad. | Puede enviar cualquier [identidad](../../../identity-service/namespaces.md) a la [!DNL Braze] destino, siempre y cuando lo asigne a la variable [!DNL Braze] [`external_id`](https://www.braze.com/docs/api/basics/#external-user-id-explanation). |

{style="table-layout:auto"}

## Audiencias compatibles {#supported-audiences}

Este destino admite la activación de todas las audiencias generadas a través del Experience Platform [Servicio de segmentación](../../../segmentation/home.md).

*Adicionalmente* Sin embargo, este destino también admite la activación de las audiencias que se describen en la tabla siguiente.

| Tipo de audiencia externa | Descripción |
---------|----------|
| Cargas personalizadas | Audiencias [importado](../../../segmentation/ui/overview.md#import-audience) en el Experience Platform desde archivos CSV. |

{style="table-layout:auto"}

## Tipo y frecuencia de exportación {#export-type-frequency}

Consulte la tabla siguiente para obtener información sobre el tipo y la frecuencia de exportación de destino.

| Elemento | Tipo | Notas |
---------|----------|---------|
| Tipo de exportación | **[!UICONTROL Basado en perfiles]** | Va a exportar todos los miembros de un segmento, junto con los campos de esquema deseados (por ejemplo: dirección de correo electrónico, número de teléfono, apellidos) o identidades, según la asignación de campos.[!DNL Adobe Experience Platform] Las audiencias de se exportan a [!DNL Braze] en el `AdobeExperiencePlatformSegments` atributo. |
| Frecuencia de exportación | **[!UICONTROL Transmisión]** | Los destinos de streaming son conexiones basadas en API &quot;siempre activadas&quot;. Tan pronto como se actualiza un perfil en Experience Platform según la evaluación de audiencias, el conector envía la actualización de forma descendente a la plataforma de destino. Más información sobre [destinos de streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Conectar con el destino {#connect}

>[!IMPORTANT]
> 
>Para conectarse al destino, necesita el **[!UICONTROL Administrar destinos]** [permiso de control de acceso](/help/access-control/home.md#permissions). Lea el [información general de control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Para conectarse a este destino, siga los pasos descritos en la sección [tutorial de configuración de destino](../../ui/connect-destination.md). En el flujo de trabajo de configuración de destino, rellene los campos enumerados en las dos secciones siguientes.

### Autenticar en el destino {#authenticate}

Para autenticarse en el destino, rellene los campos obligatorios y seleccione **[!UICONTROL Conectar con destino]**.

* **[!UICONTROL Token de cuenta de Braze]**: Este es su [!DNL Braze] [!DNL API] clave. Puede encontrar instrucciones detalladas sobre cómo obtener su [!DNL API] clave aquí: [Información general sobre la clave API REST](https://www.braze.com/docs/api/api_key/).

### Rellenar detalles de destino {#destination-details}

Para configurar los detalles del destino, rellene los campos obligatorios y opcionales a continuación. Un asterisco junto a un campo en la interfaz de usuario indica que el campo es obligatorio.

* **[!UICONTROL Nombre]**: introduzca un nombre por el cual reconocerá este destino en el futuro.
* **[!UICONTROL Descripción]**: introduzca una descripción que le ayude a identificar este destino en el futuro.
* **[!UICONTROL Instancia de extremo]**: pregunte a su [!DNL Braze] representante de qué instancia de extremo debe utilizar.

### Habilitar alertas {#enable-alerts}

Puede activar alertas para recibir notificaciones sobre el estado del flujo de datos a su destino. Seleccione una alerta de la lista a la que suscribirse para recibir notificaciones sobre el estado del flujo de datos. Para obtener más información sobre las alertas, consulte la guía de [suscripción a alertas de destinos mediante la IU](../../ui/alerts.md).

Cuando haya terminado de proporcionar detalles para la conexión de destino, seleccione **[!UICONTROL Siguiente]**.

## Activar audiencias en este destino {#activate}

>[!IMPORTANT]
> 
>Para activar los datos, necesita el **[!UICONTROL Administrar destinos]**, **[!UICONTROL Activar destinos]**, **[!UICONTROL Ver perfiles]**, y **[!UICONTROL Ver segmentos]** [permisos de control de acceso](/help/access-control/home.md#permissions). Lea el [información general de control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Consulte [Activar datos de audiencia en destinos de exportación de audiencia de flujo continuo](../../ui/activate-segment-streaming-destinations.md) para obtener instrucciones sobre cómo activar audiencias en este destino.

## Consideraciones de asignación {#mapping-considerations}

Para enviar correctamente los datos de audiencia desde [!DNL Adobe Experience Platform] a la [!DNL Braze] destino, debe ir a través del paso de asignación de campos.

La asignación consiste en crear un vínculo entre las [!DNL Experience Data Model] Campos de esquema (XDM) en su [!DNL Platform] y sus equivalentes correspondientes desde el destino de destino.

Para asignar correctamente los campos XDM a [!DNL Braze] campos de destino, siga estos pasos:

En el [!UICONTROL Asignación] , haga clic en **[!UICONTROL Añadir nueva asignación]**.

![Asignación de adición de destino de Bear](../../assets/catalog/mobile-engagement/braze/mapping.png)

En el [!UICONTROL Campo de origen] , haga clic en el botón de flecha situado junto al campo vacío.

![Asignación de origen de destino de Bear](../../assets/catalog/mobile-engagement/braze/mapping-source.png)

En el [!UICONTROL Seleccionar campo de origen] , puede elegir entre dos categorías de campos XDM:
* [!UICONTROL Seleccionar atributos]: utilice esta opción para asignar un campo específico del esquema XDM a una [!DNL Braze] atributo.

![Atributo de origen de asignación de destino de Bear](../../assets/catalog/mobile-engagement/braze/mapping-attributes.png)

* [!UICONTROL Seleccionar área de nombres de identidad]: utilice esta opción para asignar un [!DNL Platform] área de nombres de identidad a [!DNL Braze] namespace.

![Espacio De Nombres De Origen De Asignación De Destino De Braze](../../assets/catalog/mobile-engagement/braze/mapping-namespaces.png)

Elija el campo de origen y haga clic en **[!UICONTROL Seleccionar]**.

En el [!UICONTROL Campo de destino] , haga clic en el icono de asignación a la derecha del campo.

![Asignación de destino de destino de Bear](../../assets/catalog/mobile-engagement/braze/mapping-target.png)

En el [!UICONTROL Seleccionar campo de destino] , puede elegir entre dos categorías de campos de destino:
* [!UICONTROL Seleccionar área de nombres de identidad]: utilice esta opción para asignar [!DNL Platform] identifique áreas de nombres en [!DNL Braze] áreas de nombres de identidad.
* [!UICONTROL Seleccionar atributos personalizados]: utilice esta opción para asignar atributos XDM a personalizados [!DNL Braze] atributos que definió en su [!DNL Braze] cuenta. <br> También puede utilizar esta opción para cambiar el nombre de los atributos XDM existentes a [!DNL Braze]. Por ejemplo, la asignación de un `lastName` Atributo XDM a un personalizado `Last_Name` atributo en [!DNL Braze], creará el `Last_Name` atributo en [!DNL Braze], si aún no existe, y asigne el `lastName` Atributo XDM correspondiente.

![Campos de asignación de destino de destino de Bear](../../assets/catalog/mobile-engagement/braze/mapping-target-fields.png)

Elija el campo de destino y haga clic en **[!UICONTROL Seleccionar]**.

Ahora debería ver la asignación de campos en la lista.

![Asignación de destino de Bear finalizada](../../assets/catalog/mobile-engagement/braze/mapping-complete.png)

Para agregar más asignaciones, repita los pasos anteriores.

## Ejemplo de asignación {#mapping-example}

Digamos que su esquema de perfil XDM y su [!DNL Braze] La instancia de contiene los siguientes atributos e identidades:

|  | Esquema de perfil XDM | [!DNL Braze] Instancia |
|---|---|---|
| Atributos | <ul><li><code>person.name.firstName</code></li><li><code>person.name.lastName</code></li><li><code>mobilePhone.number</code></li></ul> | <ul><li><code>FirstName</code></li><li><code>LastName</code></li><li><code>PhoneNumber</code></li></ul> |
| Identidades | <ul><li><code>Correo electrónico</code></li><li><code>ID de anuncio de Google (GAID)</code></li><li><code>Apple ID para anunciantes (IDFA)</code></li></ul> | <ul><li><code>external_id</code></li></ul> |

La asignación correcta tendría este aspecto:

![Ejemplo de asignación de destino de Bear](../../assets/catalog/mobile-engagement/braze/mapping-example.png)

## Datos exportados {#exported-data}

Para comprobar si los datos se han exportado correctamente a [!DNL Braze] destino, compruebe su [!DNL Braze] cuenta. [!DNL Adobe Experience Platform] Las audiencias de se exportan a [!DNL Braze] en el `AdobeExperiencePlatformSegments` atributo.

## Uso de datos y gobernanza {#data-usage-governance}

Todo [!DNL Adobe Experience Platform] Los destinos de cumplen con las políticas de uso de datos al gestionar los datos. Para obtener información detallada sobre cómo [!DNL Adobe Experience Platform] aplica la gobernanza de datos, consulte [Resumen de gobernanza de datos](../../../data-governance/home.md).
