---
title: Conexión de audiencias ABM de Bombora
description: Active perfiles para sus campañas Bombora para la segmentación, personalización y supresión de audiencias, en función de las audiencias de la cuenta.
exl-id: a2f8e399-e192-4104-876a-fe60f8403143
source-git-commit: 049112b29b593daa69a11302e828dc968d7abae3
workflow-type: tm+mt
source-wordcount: '1170'
ht-degree: 3%

---

# Conexión de audiencias ABM de Bombora {#bombora}

>[!AVAILABILITY]
>
>La funcionalidad para activar audiencias de cuenta en el destino de audiencias ABM de Bombora está disponible para compañías que compren las ediciones de Real-Time Customer Data Platform [De empresa a empresa](/help/rtcdp/overview.md#rtcdp-b2b) y [De empresa a persona](/help/rtcdp/overview.md#rtcdp-b2p).

Active perfiles para sus campañas Bombora para la segmentación, personalización y supresión de audiencias, según [audiencias de la cuenta](/help/segmentation/types/account-audiences.md).

## Casos de uso {#use-case}

Para ayudarle a comprender mejor cómo y cuándo debe utilizar el destino Bombora, aquí tiene algunos casos de uso que los clientes de Adobe Experience Platform pueden solucionar mediante este destino.

### Integración de DSP {#dsp-integration}

Como experto en marketing B2B, puede crear una lista de cuentas en Real-Time CDP que identifique las empresas que muestran una alta intención con sus productos y, a continuación, utilizar este destino para activar esta lista en Bombora.

A través de la integración de Bombora con DSPs puede ejecutar campañas de publicidad dirigidas usando datos de Bombora. Esto garantiza que el gasto en publicidad se centre en las empresas que tienen más probabilidades de realizar una conversión.

### Account-Based Marketing {#abm}

Como experto en marketing B2B, puede crear una lista de cuentas basada en las señales de marketing y CRM. Luego, puede usar este destino para activar esta lista en Bombora, donde los controles con conocimiento de ABM le ayudan a dirigir a los tomadores de decisiones en estas compañías.

### Activación de marketing multicanal basada en cuentas {#multi-channel-abm}

Como experto en marketing B2B, puede crear una lista de cuentas en Real-Time CDP que identifique compañías con alta intención. A continuación, puede utilizar este destino para activar la lista en Bombora y ejecutar campañas dirigidas en varios canales.

En medios sociales de pago, podría publicar anuncios personalizados para profesionales de cuentas de Target en plataformas como [!DNL LinkedIn] y [!DNL Facebook]. Con las plataformas de publicidad nativas, puede asegurarse de que el contenido llegue a los responsables de la toma de decisiones relevantes.

También puede ampliar las campañas a TV avanzada y enviar anuncios a cuentas clave.

Este enfoque multicanal garantiza una mensajería coherente entre plataformas, maximizando las tasas de participación y conversión.

## Audiencias compatibles {#supported-audiences}

En esta sección se describe qué tipo de audiencias puede exportar a este destino.

| Origen de audiencia | Admitido | Descripción |
|---------|----------|----------|
| [!DNL Segmentation Service] | Sí | Audiencias generadas a través del Experience Platform [Segmentation Service](../../../segmentation/home.md). |
| Todos los demás orígenes de audiencia | Sí | Esta categoría incluye todos los orígenes de audiencia fuera de las audiencias generadas mediante [!DNL Segmentation Service]. Obtenga más información sobre los [distintos orígenes de audiencia](/help/segmentation/ui/audience-portal.md#customize). Algunos ejemplos incluyen: <ul><li> audiencias de carga personalizadas [importadas](../../../segmentation/ui/audience-portal.md#import-audience) en Experience Platform desde archivos CSV,</li><li> audiencias parecidas, </li><li> audiencias federadas, </li><li> audiencias generadas en otras aplicaciones de Experience Platform, como Adobe Journey Optimizer, </li><li> y más. </li></ul> |

{style="table-layout:auto"}

Audiencias compatibles por tipo de datos de audiencia:

| Tipo de datos de audiencia | Admitido | Descripción | Casos de uso |
|--------------------|-----------|-------------|-----------|
| [Audiencias de personas](/help/segmentation/types/people-audiences.md) | Sí | Basado en perfiles de clientes, lo que le permite dirigirse a grupos específicos de personas para campañas de marketing. | Compradores frecuentes, abandonadores del carro de compras |
| [Audiencias de la cuenta](/help/segmentation/types/account-audiences.md) | No | Segmente a individuos dentro de organizaciones específicas para estrategias de marketing basadas en cuentas. | Marketing B2B |
| [Audiencias potenciales](/help/segmentation/types/prospect-audiences.md) | No | Dirígete a personas que aún no son clientes, pero que comparten características con tu público objetivo. | Prospección con datos de terceros |
| [Exportaciones de conjuntos de datos](/help/catalog/datasets/overview.md) | No | Recopilación de datos estructurados almacenados en Adobe Experience Platform Data Lake. | Informes, flujos de trabajo de ciencia de datos |

{style="table-layout:auto"}


## Identidades admitidas {#supported-identities}

Bombora requiere la asignación de la identidad de destino descrita en la siguiente tabla. Más información sobre [identidades](/help/identity-service/features/namespaces.md).

| Identidad de destino | Descripción |
|---|---|
| `primaryId` | Bombora requiere el mapeo de esta identidad objetivo para que la integración funcione correctamente. Puede asignar cualquier campo de origen a esta identidad. Esta asignación es obligatoria, pero no exporta datos a Bombora. |

{style="table-layout:auto"}

## Tipo y frecuencia de exportación {#export-type-and-frequency}

Consulte la tabla siguiente para obtener información sobre el tipo y la frecuencia de exportación de destino.

| Elemento | Tipo | Notas |
|---------|----------|---------|
| Tipo de exportación | **[!UICONTROL Audience export]** | Está exportando todos los miembros de una audiencia con los identificadores (nombre, número de teléfono u otros) utilizados en el destino [!DNL Bombora]. |
| Frecuencia de exportación | **[!UICONTROL Streaming]** | Los destinos de streaming son conexiones basadas en API &quot;siempre activadas&quot;. Tan pronto como se actualiza un perfil en Experience Platform basado en la evaluación de audiencias, el conector envía la actualización de forma descendente a la plataforma de destino. Más información sobre [destinos de streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Requisitos previos {#prerequisites}

Para exportar audiencias de cuenta a Bombora, necesita la siguiente información.

1. Una cuenta de Bombora. Si no tiene una, puede solicitar una cuenta Bombora usando el [formulario de solicitud de activación de audiencia de Bombora](https://customers.bombora.com/artcdp/audience-activation-request).
2. Una Bombora **[!UICONTROL client ID]** y **[!UICONTROL client secret]**.
3. Los datos enviados a Bombora deben ser de conjuntos de datos que tengan **Perfil habilitado**, de manera que el conjunto de datos se incluya en el perfil. Asegúrese de que los conjuntos de datos estén [habilitados para el perfil](/help/catalog/datasets/enable-for-profile.md) antes de activar audiencias en este destino.

## Conectar con el destino {#connect}

>[!IMPORTANT]
> 
>Para conectarse al destino, necesita el permiso de control de acceso **[!UICONTROL View Destinations]** y **[!UICONTROL Manage Destinations]** [3}. ](/help/access-control/home.md#permissions) Lea la [descripción general del control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Para conectarse a este destino, siga los pasos descritos en el [tutorial de configuración de destino](../../ui/connect-destination.md). En el flujo de trabajo de configuración de destino, rellene los campos enumerados en las dos secciones siguientes.

### Autenticarse en el destino {#authenticate}

Para autenticarse en el destino, rellene los campos obligatorios y seleccione **[!UICONTROL Connect to destination]**.

![Agregar token de portador](../../assets/catalog/advertising/bombora/add-bearer-token.png)

* **[!UICONTROL Client ID]**: Escriba su Id. de cliente [!DNL Bombora].
* **[!UICONTROL Client secret]**: Escriba el secreto de cliente [!DNL Bombora].

### Rellenar detalles de destino {#destination-details}

Para configurar los detalles del destino, rellene los campos obligatorios y opcionales que aparecen a continuación. Un asterisco junto a un campo de la interfaz de usuario indica que el campo es obligatorio.

![Agregar información sobre la conexión de destino](../..//assets/catalog/advertising/bombora/name-and-description.png)

* **[!UICONTROL Name]**: nombre por el que reconocerá este destino en el futuro.
* **[!UICONTROL Description]**: descripción que le ayudará a identificar este destino en el futuro.

Ahora está listo para activar sus audiencias en Bombora.

## Activar públicos en este destino {#activate}

>[!IMPORTANT]
> 
>* Para activar los datos, necesita los permisos de control de acceso **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** y **[!UICONTROL View Segments]** [5}. ](/help/access-control/home.md#permissions) Lea la [descripción general del control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.
>* Para exportar *identidades*, necesita el **[!UICONTROL View Identity Graph]** [permiso de control de acceso](/help/access-control/home.md#permissions). <br> ![Selecciona el espacio de nombres de identidad resaltado en el flujo de trabajo para activar las audiencias en los destinos.](/help/destinations/assets/overview/export-identities-to-destination.png "Seleccione el espacio de nombres de identidad resaltado en el flujo de trabajo para activar las audiencias en los destinos."){width="100" zoomable="yes"}

Lee [Activar audiencias de cuentas](/help/destinations/ui/activate-account-audiences.md) para obtener instrucciones sobre cómo activar audiencias de cuentas en este destino.

### Asignación obligatoria {#mapping}

El destino de Bombora requiere que configure las siguientes asignaciones para que la activación de los datos se realice correctamente.

| Campo de origen | Campo de destino | Descripción |
|---------|----------|---------|
| Cualquier valor | `Identity: primaryId` | Este mapeo es obligatorio para que el Experience Platform establezca una conexión con Bombora. Este valor no se exporta a Bombora, pero es necesario para la configuración de destino. Puede seleccionar cualquier atributo para el campo de origen. |
| `xdm: accountOrganization.domain` | `xdm: companyWebsiteDomain` | Bombora utiliza direcciones de dominios o sitios web para crear una lista de cuentas. |

![Agregar asignaciones obligatorias](../..//assets/catalog/advertising/bombora/mappings.png)

## Comportamiento de sincronización de audiencia {#sync-behavior}

Después de la activación inicial de la audiencia, las actualizaciones posteriores de la audiencia en Experience Platform se sincronizan gradualmente con Bombora. Se aplican los siguientes comportamientos:

* **Cuenta agregada a la audiencia**: Cuando se agrega una cuenta a la audiencia en Experience Platform, se agrega automáticamente a la audiencia correspondiente en Bombora.
* **Cuenta eliminada o ya no califica**: Cuando una cuenta ya no califica para la audiencia o es eliminada de la audiencia en Experience Platform, es eliminada de la audiencia correspondiente en Bombora.
* **Eliminación de cuenta o perfil**: Cuando se elimina una cuenta o perfil del Experience Platform y esa cuenta ya no cumple los requisitos para ser considerada como audiencia, se elimina de la audiencia correspondiente en Bombora.

### Comportamiento de eliminación y desconexión de audiencia {#deletion-disconnect}

Si elimina una audiencia en Experience Platform o elimina una audiencia de un flujo de datos de activación de Bombora, se elimina la audiencia de su cuenta de Bombora.

## Notas adicionales y rótulos importantes {#additional-notes}

Si una audiencia de cuenta con el mismo nombre fue activada anteriormente en Bombora, recibirá un error si intenta activarla nuevamente a través de un flujo de datos diferente al destino de Bombora.
