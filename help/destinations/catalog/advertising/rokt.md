---
title: Rokt
description: Aprenda a conectar las audiencias de Adobe Experience Platform a Rokt para mejorar el rendimiento de la campaña mediante una segmentación, supresión y personalización más inteligentes.
source-git-commit: a281a7c961b8576105913feb7a7f8258c975e875
workflow-type: tm+mt
source-wordcount: '1235'
ht-degree: 4%

---


# [!DNL Rokt] conexión {#rokt-destination}

## Información general {#overview}

[[!DNL Rokt]](https://www.rokt.com) desbloquea el valor en el comercio electrónico mediante la toma de decisiones en tiempo real impulsada por IA para que cada Momento de transacción™ sea más relevante. Ofrece experiencias personalizadas y conecta a los anunciantes con clientes de alta intención. Conecte las audiencias de [!DNL Adobe Experience Platform] a [!DNL Rokt] para mejorar el rendimiento de la campaña mediante una segmentación, supresión y personalización más inteligentes. Llegue a los clientes adecuados en el momento adecuado y reduzca el gasto desperdiciado.

>[!IMPORTANT]
>
>El conector de destino y la página de documentación los crea y mantiene el equipo [!DNL Rokt]. Para cualquier consulta o solicitud de actualización, comuníquese con el administrador de cuentas de [!DNL Rokt] o comuníquese con `support@rokt.com`.

## Casos de uso {#use-cases}

Los siguientes casos de uso muestran cómo los clientes de [!DNL Experience Platform] pueden usar el destino [!DNL Rokt].

### Caso de uso #1: Redireccionamiento {#use-case-1}

Vuelva a atraer a los clientes con altas intenciones que visitaron su sitio o aplicación, pero que no se convirtieron. Cree una audiencia en [!DNL Experience Platform] que incluya a los usuarios que exploraron categorías de productos específicas o que abandonaron un flujo de cierre de compra. Luego, inserte esa audiencia en [!DNL Rokt] para ofrecer ofertas personalizadas en el punto de compra en sitios de socios. [!DNL Rokt] opera en el momento de la transacción, inmediatamente después de que un cliente complete una compra en otro lugar. Las audiencias redirigidas se alcanzan cuando la intención de compra está en su punto máximo, lo que provoca tasas de conversión más altas que el retargeting de visualización tradicional.

### Caso de uso #2: Listas de supresión {#use-case-2}

Evite el gasto desperdiciado y las experiencias irrelevantes suprimiendo las audiencias que no deben recibir determinadas ofertas de [!DNL Rokt]. Los casos de uso de supresión comunes incluyen la exclusión de convertidores recientes, miembros socio en una promoción activa o usuarios que se excluyeron del marketing. Por ejemplo, excluya a los clientes que hayan realizado compras en los últimos 30 días. Sincronizar estas audiencias de supresión de [!DNL Experience Platform] a [!DNL Rokt] en tiempo real. Esto mantiene las campañas centradas en usuarios nuevos o que se pueden volver a atraer. Esto mejora el retorno de la inversión y protege la experiencia del cliente.

## Requisitos previos {#prerequisites}

Antes de configurar el destino [!DNL Rokt] en [!DNL Adobe Experience Platform], debe obtener las siguientes credenciales de su **[!DNL Rokt]Administrador de cuentas**:

* **Clave de API**: use esto como **[!UICONTROL Username]** al [autenticar la conexión de destino](#authenticate).
* **Secreto de API**: úselo como **[!UICONTROL Password]** al [autenticar la conexión de destino](#authenticate).

El administrador de cuentas de [!DNL Rokt] aprovisionará estas credenciales en la plataforma de [!DNL Rokt] antes de la configuración. Póngase en contacto con el Administrador de cuentas si aún no lo ha recibido.

## Identidades admitidas {#supported-identities}

[!DNL Rokt] admite la activación de las identidades descritas en la tabla siguiente. Más información sobre [identidades](/help/identity-service/features/namespaces.md).

| Identidad de destino | Descripción | Consideraciones |
|---|---|---|
| correo electrónico | Dirección de correo electrónico de texto sin formato | Recomendado. Se usa para la coincidencia de perfiles en [!DNL Rokt]. |
| email_lc_sha256 | Direcciones de correo electrónico con el algoritmo SHA256 | Se admiten direcciones de correo electrónico con hash SHA256 y de texto sin formato. Si el campo de origen contiene atributos sin hash, seleccione la opción **[!UICONTROL Apply transformation]** para que [!DNL Experience Platform] agregue automáticamente los datos al realizar la activación. |
| phone | Número de teléfono de texto normal | Se usa para la coincidencia de perfiles en [!DNL Rokt]. |
| phone_sha256 | Números de teléfono con hash con el algoritmo SHA256 | Se admiten números de teléfono con hash SHA256 y texto sin formato. Si el campo de origen contiene atributos sin hash, seleccione la opción **[!UICONTROL Apply transformation]** para que [!DNL Experience Platform] agregue automáticamente los datos al realizar la activación. |
| GAID | [!DNL Google] ID de Advertising | Seleccione la identidad de destino GAID cuando su identidad de origen sea un área de nombres GAID. |
| IDFA | ID de [!DNL Apple] para anunciantes | Seleccione la identidad de destino IDFA cuando la identidad de origen sea un área de nombres IDFA. |
| aepProfileId | [!DNL Adobe Experience Platform] ID de perfil | Asigna el identificador de perfil (`xdm:_id`) como identificador de reserva. |

{style="table-layout:auto"}

## Audiencias compatibles {#supported-audiences}

Esta sección describe qué tipos de audiencias puede exportar a este destino.

| Origen de audiencia | Admitido | Descripción |
|---------|----------|----------|
| [!DNL Segmentation Service] | Sí | Audiencias generadas mediante [!DNL Experience Platform] [[!DNL Segmentation Service]](/help/segmentation/home.md). |
| Todos los demás orígenes de audiencia | Sí | Esta categoría incluye todos los orígenes de audiencia fuera de las audiencias generadas a través de [!DNL Segmentation Service]. Obtenga información acerca de [varios orígenes de audiencia](/help/segmentation/ui/audience-portal.md#customize). Algunos ejemplos son: <ul><li> audiencias de carga personalizadas [importadas](/help/segmentation/ui/audience-portal.md#import-audience) en [!DNL Experience Platform] desde archivos CSV,</li><li> audiencias de similitud, </li><li> audiencias federadas, </li><li> audiencias generadas en otras [!DNL Experience Platform] aplicaciones como [!DNL Adobe Journey Optimizer], </li><li> y más. </li></ul> |

{style="table-layout:auto"}

Audiencias compatibles por tipo de datos de audiencia:

| Tipo de datos de audiencia | Admitido | Descripción | Casos de uso |
|--------------------|-----------|-------------|-----------|
| [Audiencias de personas](/help/segmentation/types/people-audiences.md) | Sí | Basado en perfiles de clientes. Utilícelos para dirigirse a grupos específicos de personas para campañas de marketing. | Compradores frecuentes, abandonadores del carro de compras |
| [Audiencias de la cuenta](/help/segmentation/types/account-audiences.md) | No | Segmente a individuos dentro de organizaciones específicas para estrategias de marketing basadas en cuentas. | Marketing B2B |
| [Audiencias potenciales](/help/segmentation/types/prospect-audiences.md) | No | Dirija la actividad a personas que aún no sean clientes, pero que compartan características con la audiencia a la que va dirigida. | Prospección con datos de terceros |
| [Exportaciones de conjuntos de datos](/help/catalog/datasets/overview.md) | No | Colecciones de datos estructurados almacenados en el lago de datos [!DNL Adobe Experience Platform]. | Informes, flujos de trabajo de ciencia de datos |

{style="table-layout:auto"}

## Tipo y frecuencia de exportación {#export-type-frequency}

Consulte la tabla siguiente para obtener información sobre el tipo y la frecuencia de exportación de destino.

| Elemento | Tipo | Notas |
|---------|----------|---------|
| Tipo de exportación | **[!UICONTROL Audience export]** | Va a exportar todos los miembros de una audiencia con los identificadores (correo electrónico, teléfono, ID de publicidad móvil u otros) utilizados en el destino [!DNL Rokt]. |
| Frecuencia de exportación | **[!UICONTROL Streaming]** | Los destinos de streaming son conexiones basadas en API &quot;siempre activadas&quot;. Tan pronto como se actualiza un perfil en [!DNL Experience Platform] según la evaluación de audiencia, el conector envía la actualización descendente a [!DNL Rokt]. Más información sobre [destinos de streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Conectar con el destino {#connect}

>[!IMPORTANT]
>
>Para conectarse al destino, necesita los **[!UICONTROL View Destinations]** y **[!UICONTROL Manage Destinations]** [permisos de control de acceso](/help/access-control/home.md#permissions). Lea la [descripción general del control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Para conectarse a este destino, siga los pasos descritos en el [tutorial de configuración de destino](/help/destinations/ui/connect-destination.md). En el flujo de trabajo de configuración de destino, rellene los campos enumerados en las dos secciones siguientes.

### Autenticarse en el destino {#authenticate}

Para autenticarse en el destino, rellene los campos obligatorios y seleccione **[!UICONTROL Connect to destination]**.

* **[!UICONTROL Username]**: su clave API proporcionada por el administrador de cuentas de [!DNL Rokt].
* **[!UICONTROL Password]**: Secreto de API proporcionado por el administrador de cuentas de [!DNL Rokt].

  ![Pantalla de configuración de destino [!DNL Rokt] en [!DNL Experience Platform], con detalles de cuenta, campos de autenticación y detalles de destino rellenados.](/help/destinations/assets/catalog/advertising/rokt/aep-configure-destination.png)

### Rellenar detalles de destino {#destination-details}

Para configurar los detalles del destino, rellene los campos obligatorios y opcionales a continuación. Un asterisco junto a un campo en la interfaz de usuario indica que el campo es obligatorio.

* **[!UICONTROL Name]**: un nombre con el cual reconocerá este destino en el futuro (por ejemplo, &quot;[!DNL Rokt] - Audiencias de redireccionamiento&quot;).
* **[!UICONTROL Description]**: una descripción que le ayudará a identificar este destino en el futuro.

### Habilitar alertas {#enable-alerts}

Puede activar alertas para recibir notificaciones sobre el estado del flujo de datos a su destino. Seleccione una alerta de la lista a la que suscribirse para recibir notificaciones sobre el estado del flujo de datos. Para obtener más información sobre las alertas, consulte la guía sobre [suscripción a alertas de destinos mediante la interfaz de usuario](/help/destinations/ui/alerts.md).

Cuando termine de proporcionar detalles para la conexión de destino, seleccione **[!UICONTROL Next]**.

## Activar públicos en este destino {#activate}

>[!IMPORTANT]
>
>* Para activar los datos, necesita los permisos de control de acceso **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** y **[!UICONTROL View Segments]** [5}. ](/help/access-control/home.md#permissions)Lea la [descripción general del control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.
>* Para exportar *identidades*, necesita el **[!UICONTROL View Identity Graph]** [permiso de control de acceso](/help/access-control/home.md#permissions). <br> ![Seleccione el área de nombres de identidad resaltada en el flujo de trabajo para activar audiencias en los destinos.](/help/destinations/assets/overview/export-identities-to-destination.png "Seleccione el área de nombres de identidad resaltada en el flujo de trabajo para activar audiencias en los destinos."){width="100" zoomable="yes"}

Lea [Activar perfiles y audiencias en destinos de exportación de audiencias de streaming](/help/destinations/ui/activate-segment-streaming-destinations.md) para obtener instrucciones sobre cómo activar audiencias en este destino.

### Asignar atributos e identidades {#map}

El destino [!DNL Rokt] admite la asignación de áreas de nombres de identidad de [!DNL Experience Platform] a [!DNL Rokt] campos de identidad. Debe asignar al menos una identidad para activar correctamente una audiencia. Las asignaciones recomendadas se muestran en la siguiente tabla.

| Campo de origen | Campo de destino | Consideraciones |
|---|---|---|
| `IdentityMap: Email` | `Identity: email` | Recomendado |
| `IdentityMap: Email_LC_SHA256` | `Identity: emailSha256` | Recomendado |
| `IdentityMap: Phone` | `Identity: phone` | Opcional |
| `IdentityMap: Phone_SHA256` | `Identity: phoneSha256` | Opcional |
| `IdentityMap: GAID` | `Identity: gaid` | Opcional |
| `IdentityMap: IDFA` | `Identity: idfa` | Opcional |
| `xdm: _id` | `Identity: aepProfileId` | Opcional |

{style="table-layout:auto"}

Este es un ejemplo de asignación completa:

![Paso de asignación del flujo de trabajo de activación de destino [!DNL Rokt] en [!DNL Experience Platform], con campos de identidad de origen y destino configurados.](/help/destinations/assets/catalog/advertising/rokt/aep-identity-mapping.png)

>[!NOTE]
>
>Se recomienda usar al menos una asignación de identidad basada en correo electrónico (`email` o `emailSha256`) para maximizar las tasas de coincidencia en [!DNL Rokt].

### Configurar programación de audiencia {#audience-schedule}

Después de completar el paso de asignación, configure una programación de audiencia para cada audiencia seleccionada. Proporcione un **[!UICONTROL Start date]** para saber cuándo debe comenzar la sincronización de la audiencia, y un **[!UICONTROL Mapping ID]** (etiqueta utilizada para identificar esta audiencia en [!DNL Rokt]). Puede usar el nombre de audiencia [!DNL Experience Platform] o cualquier cadena descriptiva que le ayude a usted y a su administrador de cuentas [!DNL Rokt] a identificar la audiencia.

## Uso de datos y gobernanza {#data-usage-governance}

Todos los destinos de [!DNL Experience Platform] cumplen con las políticas de uso de datos al administrar los datos. Para obtener información detallada sobre cómo [!DNL Experience Platform] aplica el control de datos, lea la [Información general sobre el control de datos](/help/data-governance/home.md).

## Recursos adicionales {#additional-resources}

* [Documentación para desarrolladores de [!DNL Rokt]](https://docs.rokt.com)
* [Información general sobre destinos Adobe Experience Platform](/help/destinations/home.md)
