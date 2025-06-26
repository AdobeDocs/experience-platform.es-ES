---
keywords: mobile; braze; mensajería;
title: Conexión de Braze
description: Braze es una plataforma completa de participación del cliente que potencia experiencias relevantes y memorables entre los clientes y las marcas que aman.
last-substantial-update: 2024-08-20T00:00:00Z
exl-id: 508e79ee-7364-4553-b153-c2c00cc85a73
source-git-commit: 2440a4d4ec5d572d1d44228fe99914a01e19d60d
workflow-type: tm+mt
source-wordcount: '1123'
ht-degree: 3%

---

# [!DNL Braze] conexión

## Información general {#overview}

El destino [!DNL Braze] le ayuda a enviar datos de perfil a [!DNL Braze].

[!DNL Braze] es una plataforma integral de participación del cliente que proporciona experiencias relevantes y memorables entre los clientes y las marcas que aman.

Para enviar datos de perfil a [!DNL Braze], primero debe conectarse al destino.

## Detalles del destino {#specifics}

Tenga en cuenta los siguientes detalles específicos del destino [!DNL Braze]:

* Las audiencias de [!DNL Adobe Experience Platform] se han exportado a [!DNL Braze] con el atributo `AdobeExperiencePlatformSegments`.

>[!NOTE]
>
>Tenga en cuenta que enviar atributos personalizados adicionales a [!DNL Braze] puede causar aumentos en el consumo de puntos de datos [!DNL Braze]. Consulte con su administrador de cuentas de [!DNL Braze] antes de enviar atributos personalizados adicionales.

## Casos de uso {#use-cases}

Como especialista en marketing, quiero segmentar usuarios en un destino de participación móvil, con audiencias creadas en [!DNL Adobe Experience Platform]. Además, deseo ofrecerles experiencias personalizadas basadas en los atributos de sus perfiles [!DNL Adobe Experience Platform] en cuanto las audiencias y los perfiles se actualicen en [!DNL Adobe Experience Platform].

## Identidades admitidas {#supported-identities}

[!DNL Braze] admite la activación de las identidades descritas en la tabla siguiente.

| Identidad de destino | Descripción | Consideraciones |
|---|---|---|
| external_id | Identificador [!DNL Braze] personalizado que admite la asignación de cualquier identidad. | Puede enviar cualquier [identidad](../../../identity-service/features/namespaces.md) al destino [!DNL Braze], siempre y cuando la asigne a [!DNL Braze] [`external_id`](https://www.braze.com/docs/api/basics/#external-user-id-explanation). |

{style="table-layout:auto"}

## Audiencias compatibles {#supported-audiences}

Esta sección describe qué tipos de audiencias puede exportar a este destino.

| Origen de audiencia | Admitido | Descripción |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Audiencias generadas a través del [servicio de segmentación](../../../segmentation/home.md) de Experience Platform. |
| Cargas personalizadas | ✓ | Las audiencias [importadas](../../../segmentation/ui/audience-portal.md#import-audience) en Experience Platform desde archivos CSV. |

{style="table-layout:auto"}

## Tipo y frecuencia de exportación {#export-type-frequency}

Consulte la tabla siguiente para obtener información sobre el tipo y la frecuencia de exportación de destino.

| Elemento | Tipo | Notas |
---------|----------|---------|
| Tipo de exportación | **[!UICONTROL Basado en perfil]** | Va a exportar todos los miembros de un segmento, junto con los campos de esquema deseados (por ejemplo: dirección de correo electrónico, número de teléfono, apellidos) o identidades, según la asignación de campos.Las audiencias de [!DNL Adobe Experience Platform] se han exportado a [!DNL Braze] con el atributo `AdobeExperiencePlatformSegments`. |
| Frecuencia de exportación | **[!UICONTROL Transmisión]** | Los destinos de streaming son conexiones basadas en API &quot;siempre activadas&quot;. Tan pronto como se actualiza un perfil en Experience Platform basado en la evaluación de audiencias, el conector envía la actualización de forma descendente a la plataforma de destino. Más información sobre [destinos de streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Conexión al destino {#connect}

>[!IMPORTANT]
> 
>Para conectarse al destino, necesita los **[!UICONTROL permisos de control de acceso](/help/access-control/home.md#permissions) de Ver destinos]** y **[!UICONTROL Administrar destinos]**[5}. Lea la [descripción general del control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Para conectarse a este destino, siga los pasos descritos en el [tutorial de configuración de destino](../../ui/connect-destination.md). En el flujo de trabajo de configuración de destino, rellene los campos enumerados en las dos secciones siguientes.

### Autenticarse en el destino {#authenticate}

Para autenticarse en el destino, rellene los campos obligatorios y seleccione **[!UICONTROL Conectar con destino]**.

* **[!UICONTROL Token de cuenta de Braze]**: Esta es su clave de [!DNL Braze] [!DNL API]. Puede encontrar instrucciones detalladas sobre cómo obtener su clave [!DNL API] aquí: [Información general sobre la clave API REST](https://www.braze.com/docs/api/api_key/).

### Rellenar detalles de destino {#destination-details}

Para configurar los detalles del destino, rellene los campos obligatorios y opcionales a continuación. Un asterisco junto a un campo en la interfaz de usuario indica que el campo es obligatorio.

* **[!UICONTROL Nombre]**: escriba un nombre para reconocer este destino en el futuro.
* **[!UICONTROL Descripción]**: escribe una descripción que te ayudará a identificar este destino en el futuro.
* **[!UICONTROL Instancia de extremo]**: pregunte a su representante de [!DNL Braze] qué instancia de extremo debe usar.

### Habilitar alertas {#enable-alerts}

Puede activar alertas para recibir notificaciones sobre el estado del flujo de datos a su destino. Seleccione una alerta de la lista a la que suscribirse para recibir notificaciones sobre el estado del flujo de datos. Para obtener más información sobre las alertas, consulte la guía sobre [suscripción a alertas de destinos mediante la interfaz de usuario](../../ui/alerts.md).

Cuando termine de proporcionar detalles para la conexión de destino, seleccione **[!UICONTROL Siguiente]**.

## Activar públicos en este destino {#activate}

>[!IMPORTANT]
> 
>* Para activar los datos, necesita los **[!UICONTROL permisos de control de acceso]**, **[!UICONTROL Activar destinos]**, **[!UICONTROL Ver perfiles]** y **[!UICONTROL Ver segmentos]**[para ](/help/access-control/home.md#permissions). Lea la [descripción general del control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.
>* Para exportar *identidades*, necesita el **[!UICONTROL permiso de control de acceso](/help/access-control/home.md#permissions) de]** Ver gráfico de identidad[. <br> ![Seleccione el área de nombres de identidad resaltada en el flujo de trabajo para activar audiencias en los destinos.](/help/destinations/assets/overview/export-identities-to-destination.png "Seleccione el área de nombres de identidad resaltada en el flujo de trabajo para activar audiencias en los destinos."){width="100" zoomable="yes"}

Consulte [Activar datos de audiencia en destinos de exportación de audiencia de streaming](../../ui/activate-segment-streaming-destinations.md) para obtener instrucciones sobre cómo activar audiencias en este destino.

## Consideraciones de asignación {#mapping-considerations}

Para enviar correctamente los datos de audiencia de [!DNL Adobe Experience Platform] al destino [!DNL Braze], debe pasar por el paso de asignación de campos.

La asignación consiste en crear un vínculo entre los campos de esquema [!DNL Experience Data Model] (XDM) de la cuenta [!DNL Experience Platform] y sus equivalentes correspondientes del destino.

Para asignar correctamente los campos XDM a los campos de destino [!DNL Braze], siga estos pasos:

En el paso [!UICONTROL Asignación], haga clic en **[!UICONTROL Agregar nueva asignación]**.

![Asignación de adición de destino de Braze](../../assets/catalog/mobile-engagement/braze/mapping.png)

En la sección [!UICONTROL Campo de Source], haga clic en el botón de flecha situado junto al campo vacío.

![Asignación de destino de Source de Braze](../../assets/catalog/mobile-engagement/braze/mapping-source.png)

En la ventana [!UICONTROL Seleccionar campo de origen], puede elegir entre dos categorías de campos XDM:
* [!UICONTROL Seleccionar atributos]: utilice esta opción para asignar un campo específico del esquema XDM a un atributo [!DNL Braze].

![Atributo Source de asignación de destino de Braze](../../assets/catalog/mobile-engagement/braze/mapping-attributes.png)

* [!UICONTROL Seleccionar área de nombres de identidad]: utilice esta opción para asignar un área de nombres de identidad [!DNL Experience Platform] a un área de nombres [!DNL Braze].

![Espacio de nombres de Source de asignación de destino de Braze](../../assets/catalog/mobile-engagement/braze/mapping-namespaces.png)

Elija su campo de origen y luego haga clic en **[!UICONTROL Seleccionar]**.

En la sección [!UICONTROL Campo de destino], haga clic en el icono de asignación a la derecha del campo.

![Asignar Destino De Destino De Braze](../../assets/catalog/mobile-engagement/braze/mapping-target.png)

En la ventana [!UICONTROL Seleccionar campo de destino], puede elegir entre dos categorías de campos de destino:
* [!UICONTROL Seleccionar área de nombres de identidad]: utilice esta opción para asignar [!DNL Experience Platform] áreas de nombres de identidad a [!DNL Braze] áreas de nombres de identidad.
* [!UICONTROL Seleccionar atributos personalizados]: utilice esta opción para asignar atributos XDM a atributos personalizados [!DNL Braze] que haya definido en su cuenta de [!DNL Braze]. <br> También puede utilizar esta opción para cambiar el nombre de los atributos XDM existentes a [!DNL Braze]. Por ejemplo, si se asigna un atributo XDM `lastName` a un atributo `Last_Name` personalizado en [!DNL Braze], se creará el atributo `Last_Name` en [!DNL Braze], si aún no existe, y se le asignará el atributo XDM `lastName`.

![Campos de asignación de destino de destino de Braze](../../assets/catalog/mobile-engagement/braze/mapping-target-fields.png)

Elija su campo de destino y luego haga clic en **[!UICONTROL Seleccionar]**.

Ahora debería ver la asignación de campos en la lista.

![Asignación de destino de Bear completada](../../assets/catalog/mobile-engagement/braze/mapping-complete.png)

Para agregar más asignaciones, repita los pasos anteriores.

## Ejemplo de asignación {#mapping-example}

Supongamos que su esquema de perfil XDM y su instancia [!DNL Braze] contienen los atributos e identidades siguientes:

|  | Esquema de perfil XDM | Instancia de [!DNL Braze] |
|---|---|---|
| Atributos | <ul><li><code>person.name.firstName</code></li><li><code>person.name.lastName</code></li><li><code>mobilePhone.number</code></li></ul> | <ul><li><code>Nombre</code></li><li><code>Apellidos</code></li><li><code>NúmeroTeléfono</code></li></ul> |
| Identidades | <ul><li><code>Correo electrónico</code></li><li><code>ID de Google Ad (GAID)</code></li><li><code>Apple ID para anunciantes (IDFA)</code></li></ul> | <ul><li><code>external_id</code></li></ul> |

La asignación correcta tendría este aspecto:

![Ejemplo de asignación de destino de Braze](../../assets/catalog/mobile-engagement/braze/mapping-example.png)

## Datos exportados {#exported-data}

Para comprobar si los datos se han exportado correctamente al destino [!DNL Braze], compruebe su cuenta de [!DNL Braze]. Las audiencias de [!DNL Adobe Experience Platform] se han exportado a [!DNL Braze] con el atributo `AdobeExperiencePlatformSegments`.

## Resolución de problemas {#troubleshooting}

**He recibido un error de tiempo de espera al activar mis audiencias en este destino. ¿Qué debo hacer?**

En ocasiones, la activación de audiencias en este destino puede provocar un error de tiempo de espera. Este error no siempre indica un problema de activación.

Si se produce un error de tiempo de espera, compruebe el tamaño de la audiencia en la plataforma de destino. Si el tamaño de la audiencia es correcto, la integración funciona según lo esperado.

## Uso de datos y gobernanza {#data-usage-governance}

Todos los destinos de [!DNL Adobe Experience Platform] cumplen con las políticas de uso de datos al administrar los datos. Para obtener información detallada sobre cómo [!DNL Adobe Experience Platform] aplica el control de datos, consulte [Resumen de control de datos](../../../data-governance/home.md).
