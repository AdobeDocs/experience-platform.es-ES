---
title: PubMatic Connect
description: PubMatic maximiza el valor del cliente al ofrecer la cadena de suministro de marketing digital programática del futuro. PubMatic Connect combina la tecnología de la plataforma y el servicio dedicado para mejorar la forma en que se empaquetan y se realizan las transacciones de inventario y datos.
last-substantial-update: 2023-12-14T00:00:00Z
source-git-commit: c3ef732ee82f6c0d56e89e421da0efc4fbea2c17
workflow-type: tm+mt
source-wordcount: '923'
ht-degree: 3%

---


# Destino de PubMatic Connect {#pubmatic-connect}

## Información general {#overview}

Uso [!DNL PubMatic Connect] para maximizar el valor del cliente al ofrecer la cadena de suministro programática de marketing digital del futuro. [!DNL PubMatic Connect] combina la tecnología de la plataforma y el servicio dedicado para mejorar la forma en que se empaquetan y realizan las transacciones de inventario y datos.

Utilice este destino para enviar datos de audiencia a [!DNL PubMatic Connect] plataforma.

>[!IMPORTANT]
>
>El conector de destino y la página de documentación los crea y mantiene el [!DNL PubMatic] equipo. Para cualquier consulta o solicitud de actualización, póngase en contacto directamente con ellos en `support@pubmatic.com`.

## Casos de uso {#use-cases}

Para ayudarle a comprender mejor cómo y cuándo debe utilizar el [!DNL PubMatic Connect] Destino, este es un ejemplo de caso de uso que los clientes de Adobe Experience Platform pueden solucionar mediante este destino.

### Segmentación de usuarios en plataformas móviles, web y CTV {#targeting}

Los editores o proveedores de datos desean enviar audiencias de Adobe Experience Platform a [!DNL PubMatic Connect] para dirigirse a usuarios en plataformas móviles, web y CTV, utilizando una amplia gama de identificadores.

## Requisitos previos {#prerequisites}

Hable con su [!DNL PubMatic] Administrador de cuentas para asegurarse de que su cuenta de está configurada correctamente y admite la incorporación de segmentos de audiencia. También se asegurarán de que tenga todos los detalles relevantes para utilizar este destino y para proporcionarle asistencia durante la configuración.

## Identidades admitidas {#supported-identities}

[!DNL PubMatic Connect] admite la activación de identidades descritas en la tabla siguiente. Más información sobre [identidades](/help/identity-service/namespaces.md).

| Identidad de destino | Descripción | Consideraciones |
| --------------- | ------ | --- |
| GAID | ID de publicidad de Google | Seleccione la identidad de destino GAID cuando su identidad de origen sea un área de nombres GAID. |
| IDFA | Apple ID para anunciantes | Seleccione la identidad de destino IDFA cuando la identidad de origen sea un área de nombres IDFA. |
| extern_id | ID de usuario personalizados | Seleccione esta identidad de destino cuando la identidad de origen sea un área de nombres personalizada. |

{style="table-layout:auto"}

## Audiencias compatibles {#supported-audiences}

Esta sección describe qué tipo de audiencias puede exportar a este destino.

| Origen de audiencia | Admitido | Descripción |
| --- | --------- | ------ |
| [!DNL Segmentation Service] | ✓ | Audiencias generadas mediante el Experience Platform [Servicio de segmentación](../../../segmentation/home.md). |
| Cargas personalizadas | ✓ | Audiencias [importado](../../../segmentation/ui/overview.md#import-audience) en el Experience Platform desde archivos CSV. |

{style="table-layout:auto"}

## Tipo y frecuencia de exportación {#export-type-frequency}

Consulte la tabla siguiente para obtener información sobre el tipo y la frecuencia de exportación de destino.

| Elemento | Tipo | Notas |
| --- | --- | --- |
| Tipo de exportación | **[!UICONTROL Exportación de segmentos]** | Va a exportar todos los miembros de un segmento (audiencia) con los identificadores (nombre, número de teléfono u otros) utilizados en el destino de PubMatic Connect. |
| Frecuencia de exportación | **[!UICONTROL Transmisión]** | Los destinos de streaming son conexiones basadas en API &quot;siempre activadas&quot;. Cuando se actualiza un perfil en Experience Platform en función de la evaluación de segmentos, el conector envía la actualización de forma descendente a la plataforma de destino. Más información sobre [destinos de streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Conexión al destino {#connect}

>[!IMPORTANT]
>
> Para conectarse al destino, necesita el **[!UICONTROL Administrar destinos]** [permiso de control de acceso](/help/access-control/home.md#permissions). Lea el [información general de control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Para conectarse a este destino, siga los pasos descritos en la sección [tutorial de configuración de destino](../../ui/connect-destination.md). En el flujo de trabajo de configuración de destino, rellene los campos enumerados en las dos secciones siguientes.

### Autenticarse en el destino {#authenticate}

Para autenticarse en el destino, rellene los campos obligatorios y seleccione **[!UICONTROL Conectar con destino]**.

![Cómo autenticarse](../../assets/catalog/advertising/pubmatic/authenticate-destination.png)

- **[!UICONTROL Token de portador]**: complete el token de portador para autenticarse en el destino.

### Rellenar detalles de destino {#destination-details}

Para configurar los detalles del destino, rellene los campos obligatorios y opcionales a continuación. Un asterisco junto a un campo en la interfaz de usuario indica que el campo es obligatorio.

![Detalles del destino](../../assets/catalog/advertising/pubmatic/destination-details.png)

- **[!UICONTROL Nombre]**: Un nombre con el que reconocerá este destino en el futuro.
- **[!UICONTROL Descripción]**: Una descripción que le ayudará a identificar este destino en el futuro.
- **[!UICONTROL ID del socio de datos]**: el ID del socio de datos configurado en su [!DNL PubMatic] cuenta para esta integración.
- **[!UICONTROL Código de país predeterminado]**: El código de país predeterminado que debe aplicarse a todas las identidades si no se proporciona ninguna en el perfil.
- **[!UICONTROL ID de cuenta]**: su [!DNL PubMatic Connect] ID de cuenta.
- **[!UICONTROL Tipo de cuenta]**: el tipo de cuenta de su [!DNL PubMatic] cuenta de platform. Hable con su [!DNL PubMatic] Administrador de cuentas si tiene alguna pregunta sobre la que elegir. Las opciones disponibles son:
   - [!UICONTROL EDITOR]
   - [!UICONTROL DEMAND_PARTNER]
   - [!UICONTROL COMPRADOR]

### Habilitar alertas {#enable-alerts}

Puede activar alertas para recibir notificaciones sobre el estado del flujo de datos a su destino. Seleccione una alerta de la lista a la que suscribirse para recibir notificaciones sobre el estado del flujo de datos. Para obtener más información sobre las alertas, consulte la guía de [suscripción a alertas de destinos mediante la IU](../../ui/alerts.md).

Cuando haya terminado de proporcionar detalles para la conexión de destino, seleccione **[!UICONTROL Siguiente]**.

## Activar segmentos en este destino {#activate}

>[!IMPORTANT]
>
> - Para activar los datos, necesita el **[!UICONTROL Ver destinos]**, **[!UICONTROL Activar destinos]**, **[!UICONTROL Ver perfiles]**, y **[!UICONTROL Ver segmentos]** [permisos de control de acceso](/help/access-control/home.md#permissions). Lea el [información general de control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.
>
> - Para exportar _identidades_, necesita el **[!UICONTROL Ver gráfico de identidad]** [permiso de control de acceso](/help/access-control/home.md#permissions). <br> ![Seleccione el área de nombres de identidad resaltada en el flujo de trabajo para activar audiencias en los destinos.](../../assets/overview/export-identities-to-destination.png "Seleccione el área de nombres de identidad resaltada en el flujo de trabajo para activar audiencias en los destinos."){width="100" zoomable="yes"}

Leer [Activación de perfiles y segmentos en destinos de exportación de segmentos de flujo continuo](/help/destinations/ui/activate-segment-streaming-destinations.md) para obtener instrucciones sobre cómo activar segmentos de audiencia en este destino.

### Asignar atributos e identidades {#map}

Selección de campos de origen:

- Seleccione un identificador (normalmente áreas de nombres como IDFA o un área de nombres de ID personalizada).

Selección de campos de destino:

- Hable con su [!DNL PubMatic] Administrador de cuentas para obtener la información sobre el tipo de UID que será correcto durante este paso.
- Seleccione el [!DNL PubMatic UID] escriba un número que coincida con el identificador seleccionado en el primer paso.

![Asignar atributos e identidades](../..//assets/catalog/advertising/pubmatic/export-identities-to-destination.png)

## Datos exportados / Validar exportación de datos {#exported-data}

El [!DNL PubMatic] La interfaz de usuario le permite comprobar si los datos se han insertado correctamente y si los segmentos están disponibles. Puede tardar hasta 24 horas en insertarse los datos para [!DNL PubMatic] IU que se va a actualizar.

## Uso de datos y gobernanza {#data-usage-governance}

Todo [!DNL Adobe Experience Platform] Los destinos de cumplen con las políticas de uso de datos al gestionar los datos. Para obtener información detallada sobre cómo [!DNL Adobe Experience Platform] aplica la gobernanza de datos, lea la [Resumen de gobernanza de datos](/help/data-governance/home.md).
