---
title: Conexión FreeWheel
description: Aprenda a activar audiencias de Adobe Experience Platform a FreeWheel para publicidad programática en todo el inventario de TV, pantalla y vídeo conectado.
hide: true
hidefromtoc: true
badge: label="Beta" type="Informative"
exl-id: 1f1d3e57-a8ef-4971-b3d1-43521bd158bb
source-git-commit: d946d3dbb09c1fe0163fba3a892b4c0f1b331f87
workflow-type: tm+mt
source-wordcount: '1525'
ht-degree: 8%

---

# [!DNL FreeWheel] conexión {#freewheel}

>[!AVAILABILITY]
>
>El destino [!DNL FreeWheel] se encuentra actualmente en Beta y solo está disponible para clientes seleccionados. Para solicitar acceso, póngase en contacto con su representante de Adobe.

## Información general {#overview}

[!DNL FreeWheel] es una plataforma de tecnología de publicidad global que potencia la compra y venta mediante programación en el inventario de pantallas, vídeo y televisión conectada (CTV). [!DNL FreeWheel] proporciona un mercado basado en datos que conecta a los anunciantes con propietarios de medios de primera categoría en todo el mundo.

Use este destino para enviar audiencias de [!DNL Adobe Experience Platform] a [!DNL FreeWheel]. Las audiencias se entregan como archivos por lotes diarios y están disponibles para la segmentación en [!DNL FreeWheel] ofertas y campañas.

## Requisitos previos {#prerequisites}

Antes de activar audiencias en [!DNL FreeWheel], revise los siguientes requisitos:

* **Id. de red FreeWheel**: debe tener un Id. de red [!DNL FreeWheel] válido. Esto lo proporciona [!DNL FreeWheel] cuando se configura su cuenta.

## Identidades admitidas {#supported-identities}

[!DNL FreeWheel] admite la activación de las identidades descritas en la tabla siguiente. Además de estas identidades, puede usar cualquier identidad disponible en su cuenta de [!DNL FreeWheel]. Consulte [Asignar atributos e identidades](#map) para obtener instrucciones sobre cómo asignar una identidad que no se encuentra en la tabla siguiente. Más información sobre [identidades](/help/identity-service/features/namespaces.md).

| Identidad de destino | Descripción | Consideraciones |
|---|---|---|
| `idfa` | Apple ID para anunciantes | Seleccione esta identidad de destino cuando la identidad de origen sea un área de nombres IDFA. |
| `aaid` | ANDROID ADVERTISING ID | Seleccione esta identidad de destino cuando su identidad de origen sea un área de nombres GAID. |
| `ctv` | ID del dispositivo de TV conectado | Seleccione esta identidad de destino al segmentar dispositivos CTV. |
| `ip` | Dirección IPv4 | Seleccione esta identidad de destino para dirigirse a los usuarios en función de su dirección IP. Asigne un atributo de perfil que contenga una dirección IPv4 válida o utilice un campo calculado para derivar el valor. |
| `ipv6` | Dirección IPv6 | Seleccione esta identidad de destino para dirigirse a los usuarios en función de su dirección IPv6. Asigne un atributo de perfil que contenga una dirección IPv6 válida o utilice un campo calculado para derivar el valor. |

{style="table-layout:auto"}

## Audiencias compatibles {#supported-audiences}

Esta sección describe qué tipos de audiencias puede exportar a este destino.

| Origen de audiencia | Admitido | Descripción |
|---------|----------|----------|
| [!DNL Segmentation Service] | Sí | Audiencias generadas a través del [servicio de segmentación](../../../segmentation/home.md) de Experience Platform. |
| Todos los demás orígenes de audiencia | Sí | Esta categoría incluye todos los orígenes de audiencia fuera de las audiencias generadas a través de [!DNL Segmentation Service]. Obtenga información acerca de [varios orígenes de audiencia](/help/segmentation/ui/audience-portal.md#customize). Algunos ejemplos son: <ul><li>audiencias de carga personalizadas [importadas](../../../segmentation/ui/audience-portal.md#import-audience) a Experience Platform desde archivos CSV,</li><li>audiencias de similitud,</li><li>audiencias federadas,</li><li>audiencias generadas en otras aplicaciones de Experience Platform, como [!DNL Adobe Journey Optimizer],</li><li>y más.</li></ul> |

{style="table-layout:auto"}

Audiencias compatibles por tipo de datos de audiencia:

| Tipo de datos de audiencia | Admitido | Descripción | Casos de uso |
|--------------------|-----------|-------------|-----------|
| [Audiencias de personas](/help/segmentation/types/people-audiences.md) | Sí | Basado en perfiles de clientes, lo que le permite dirigirse a grupos específicos de personas para campañas de marketing. | Retargeting de CTV, supresión de alcance |
| [Audiencias de la cuenta](/help/segmentation/types/account-audiences.md) | No | Segmente a individuos dentro de organizaciones específicas para estrategias de marketing basadas en cuentas. | Marketing B2B |
| [Audiencias potenciales](/help/segmentation/types/prospect-audiences.md) | No | Dirija la actividad a personas que aún no sean clientes, pero que compartan características con la audiencia a la que va dirigida. | Prospección con datos de terceros |
| [Exportaciones de conjuntos de datos](/help/catalog/datasets/overview.md) | No | Colecciones de datos estructurados almacenados en el lago de datos [!DNL Adobe Experience Platform]. | Informes, flujos de trabajo de ciencia de datos |

{style="table-layout:auto"}

## Tipo y frecuencia de exportación {#export-type-frequency}

Consulte la tabla siguiente para obtener información sobre el tipo y la frecuencia de exportación de destino.

| Elemento | Tipo | Notas |
|---------|----------|---------|
| Tipo de exportación | **[!UICONTROL Profile-based]** | Está exportando todos los miembros de una audiencia, junto con los campos de identidad deseados tal como se eligió en el paso de asignación de [flujo de trabajo de activación de destino](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes). |
| Frecuencia de exportación | **[!UICONTROL Batch]** | La primera exportación es una instantánea completa de todos los perfiles cualificados para las audiencias activadas. Las exportaciones posteriores son actualizaciones incrementales diarias que incluyen nuevas cualificaciones de audiencia (adiciones) y salidas de audiencia (eliminaciones). También está disponible un intervalo completo de actualización de audiencia configurable (4, 8 o 12 semanas) que activa exportaciones completas periódicas además de los incrementos diarios. Las exportaciones completas solo contienen perfiles cualificados actualmente. Las salidas de audiencia no se incluyen y se entregan exclusivamente a través de las actualizaciones incrementales diarias. Obtenga más información sobre [destinos basados en archivos por lotes](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## Conectar con el destino {#connect}

>[!IMPORTANT]
>
>Para conectarse al destino, necesita los **[!UICONTROL View Destinations]** y **[!UICONTROL Manage Destinations]** [permisos de control de acceso](/help/access-control/home.md#permissions). Lea la [descripción general del control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Para conectarse a este destino, siga los pasos descritos en el [tutorial de configuración de destino](../../ui/connect-destination.md). En el flujo de trabajo de configuración de destino, rellene los campos enumerados en las dos secciones siguientes.

### Autenticarse en el destino {#authenticate}

Adobe administra automáticamente la autenticación en el destino [!DNL FreeWheel]. No se le necesitan credenciales ni claves API durante la autenticación. Adobe administra la conexión segura con [!DNL FreeWheel] en su nombre.

![Captura de pantalla del paso de autenticación para el destino FreeWheel.](../../assets/catalog/advertising/freewheel/connect-destination.png)

Seleccione **[!UICONTROL Connect to destination]** para continuar con el paso de detalles de destino.

### Rellenar detalles de destino {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_freewheel_backfill"
>title="Intervalo completo de actualización de audiencia"
>abstract="Seleccione el intervalo con el cual se enviará una exportación de audiencia completa a [!DNL FreeWheel], además de las actualizaciones incrementales diarias. Una exportación de audiencia completa evita que los miembros de la audiencia caduquen en [!DNL FreeWheel], de modo que no experimente caídas en los miembros de destino mientras se ejecutan las campañas. Las opciones disponibles son 4 semanas, 8 semanas y 12 semanas."

Para configurar los detalles del destino, rellene los campos obligatorios y opcionales a continuación. Un asterisco junto a un campo en la interfaz de usuario indica que el campo es obligatorio.

![Captura de pantalla de muestra que muestra cómo rellenar detalles para el destino FreeWheel.](../../assets/catalog/advertising/freewheel/destination-details.png)

* **[!UICONTROL Name]**: un nombre con el cual reconocerá este destino en el futuro.
* **[!UICONTROL Description]**: una descripción que le ayudará a identificar este destino en el futuro.
* **[!UICONTROL Region]**: la región [!DNL FreeWheel] en la que está alojada su cuenta. Seleccione una de las siguientes opciones:
   * **[!UICONTROL US East]**
   * **[!UICONTROL Europe]**
   * **[!UICONTROL Asia Pacific]**
* **[!UICONTROL FreeWheel network ID]**: su ID de red [!DNL FreeWheel]. Este valor lo proporciona [!DNL FreeWheel] e identifica de forma exclusiva a su organización en la plataforma [!DNL FreeWheel].
* **[!UICONTROL Full audience refresh interval]**: la frecuencia con la que se envía una exportación de audiencia completa a [!DNL FreeWheel], además de las actualizaciones incrementales diarias. Una exportación de audiencia completa evita que los miembros de la audiencia caduquen en [!DNL FreeWheel], de modo que no experimente caídas en los miembros de destino mientras se ejecutan las campañas. Seleccione un intervalo en la lista desplegable.

### Habilitar alertas {#enable-alerts}

Puede activar alertas para recibir notificaciones sobre el estado del flujo de datos a su destino. Seleccione una alerta de la lista a la que suscribirse para recibir notificaciones sobre el estado del flujo de datos. Para obtener más información sobre las alertas, consulte la guía sobre [suscripción a alertas de destinos mediante la interfaz de usuario](../../ui/alerts.md).

Cuando termine de proporcionar detalles para la conexión de destino, seleccione **[!UICONTROL Next]**.

## Activar públicos en este destino {#activate}

>[!IMPORTANT]
>
>* Para activar los datos, necesita los permisos de control de acceso **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** y **[!UICONTROL View Segments]** [5}. ](/help/access-control/home.md#permissions) Lea la [descripción general del control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.
>* Para exportar *identidades*, necesita el **[!UICONTROL View Identity Graph]** [permiso de control de acceso](/help/access-control/home.md#permissions). <br> ![Seleccione el área de nombres de identidad resaltada en el flujo de trabajo para activar audiencias en los destinos.](/help/destinations/assets/overview/export-identities-to-destination.png "Seleccione el área de nombres de identidad resaltada en el flujo de trabajo para activar audiencias en los destinos."){width="100" zoomable="yes"}

Lea [Activar datos de audiencia en destinos de exportación de perfiles por lotes](/help/destinations/ui/activate-batch-profile-destinations.md) para obtener instrucciones sobre cómo activar audiencias en este destino.

### Programar exportaciones de audiencia {#schedule}

![Captura de pantalla del paso Programación en el flujo de trabajo de activación de FreeWheel.](../../assets/catalog/advertising/freewheel/scheduling.png)

En el paso **[!UICONTROL Scheduling]**, configure la programación de exportación para cada audiencia. [!DNL FreeWheel] utiliza un modelo de exportación híbrido: la primera exportación para cada audiencia activada es una instantánea completa, seguida de actualizaciones incrementales diarias.

Configure los campos siguientes:

* **[!UICONTROL File export options]**: **[!UICONTROL Export incremental files]** está preseleccionado y es la única opción admitida. La primera exportación incluye automáticamente una instantánea completa de todos los perfiles cualificados. Las exportaciones posteriores solo proporcionan nuevas cualificaciones de audiencia y salidas desde la última exportación.
* **[!UICONTROL Frequency]**: seleccione **[!UICONTROL Daily]**. [!DNL FreeWheel] espera un envío diario de archivos incrementales.
* **[!UICONTROL Scheduled start time]**: escriba la hora en UTC a la que se debe ejecutar la exportación diaria.
* **[!UICONTROL Date]**: establezca la fecha de inicio y finalización de la activación. La fecha de inicio determina cuándo se envía la primera exportación de instantánea completa.

>[!NOTE]
>
>Las exportaciones completas (tanto la instantánea inicial como las actualizaciones completas periódicas) solo contienen perfiles cualificados actualmente. Las salidas de audiencia no se incluyen en las exportaciones completas y se entregan exclusivamente a través de las actualizaciones incrementales diarias.

### Asignar atributos e identidades {#map}

En el paso de asignación, seleccione los campos de origen de los perfiles de Experience Platform y asígnelos a los tipos de identidad admitidos por [!DNL FreeWheel]. Se requiere al menos una asignación.

>[!IMPORTANT]
>
>Los tipos de identidad compatibles con [!DNL FreeWheel] se presentan como **atributos de destino** en la interfaz de usuario de asignación, no como áreas de nombres de identidad.

Si su cuenta de [!DNL FreeWheel] admite tipos de identidad que no están enumerados en la tabla [identidades admitidas](#supported-identities), puede asignarlos introduciendo manualmente el nombre de identidad en el campo de destino en lugar de seleccionarlos de la lista predefinida.

![Captura de pantalla que muestra un nombre de identidad personalizado escrito directamente en el campo de destino en el paso de asignación.](../../assets/catalog/advertising/freewheel/custom-identity.png)

A continuación se muestran ejemplos de asignaciones. Las asignaciones reales dependerán del esquema de perfil y de los tipos de identidad que admita su cuenta de [!DNL FreeWheel].

| Campo de origen | Campo de destino |
| --- | --- |
| `identityMap.IDFA` | `idfa` |
| `identityMap.GAID` | `aaid` |
| `homeAddress.ipAddress` | `ip` |

{style="table-layout:auto"}

>[!NOTE]
>
>No se aplican asignaciones obligatorias. Sin embargo, los perfiles sin al menos una asignación de identidad válida no se incluirán en los archivos exportados.

## Datos exportados / Validar exportación de datos {#exported-data}

[!DNL FreeWheel] recibe dos tipos de archivos por exportación. Ambos tipos de archivo se generan y entregan automáticamente. No se requiere ninguna acción por su parte.

**Los archivos de identidad (datos)** contienen los datos de pertenencia a audiencias. Cada fila asigna un identificador de usuario a uno o varios ID de audiencia. Los archivos se entregan a [!DNL FreeWheel] en formato CSV sin encabezados de columna. Se generan archivos independientes para cada tipo de identidad presente en la exportación (por ejemplo, un archivo para `aaid` y un archivo independiente para `idfa`).

Ejemplo de formato de archivo de datos:

```csv
aebc1234-56f7-89ab-cdef-0123456789ab,segment_1,segment_2
f7c9a8b0-4d33-11ec-81d3-0242ac130003,segment_1,segment_3
123e4567-e89b-12d3-a456-426614174000,segment_2
```

**Archivos de taxonomía** describen las audiencias incluidas en la exportación. Estos archivos se entregan junto con los archivos de datos e incluyen el ID de audiencia, el nombre y el TTL (tiempo de vida) en días. El TTL máximo admitido por [!DNL FreeWheel] es de 90 días. Los valores del ejemplo siguiente son ilustrativos.

Ejemplo de formato de archivo de taxonomía:

```csv
Segment ID,Segment Name,TTL
segment_1,my_first_segment,30
segment_2,my_second_segment,30
segment_3,my_third_segment,30
```

## Uso de datos y gobernanza {#data-usage-governance}

Todos los destinos de [!DNL Adobe Experience Platform] cumplen con las políticas de uso de datos al administrar los datos. Para obtener información detallada sobre cómo [!DNL Adobe Experience Platform] aplica el control de datos, consulte la [Información general sobre el control de datos](/help/data-governance/home.md).

## Recursos adicionales {#additional-resources}

Para obtener información adicional acerca de [!DNL FreeWheel] y su plataforma de tecnología de publicidad, visite el [sitio web de FreeWheel](https://www.freewheel.com){target="_blank"}.
