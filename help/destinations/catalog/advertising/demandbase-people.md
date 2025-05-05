---
title: Conexión de Demandbase People
description: Utilice este destino para activar sus audiencias y enriquecerlas con datos de terceros de Demandbase, para otros casos de uso descendente en marketing y ventas.
source-git-commit: df2cb1edbf998082fca961e6d9bb567a1ad3b7e6
workflow-type: tm+mt
source-wordcount: '745'
ht-degree: 4%

---


# Conexión de Demandbase People {#demandbase-people}

Active perfiles para sus campañas de Demandbase para la segmentación, personalización y supresión de audiencias.

>[!IMPORTANT]
>
>En los casos de uso B2B en los que necesite [activar audiencias de cuenta](../../ui/activate-account-audiences.md), use el conector de destino [Demandbase](demandbase.md) en su lugar.

## Ejemplo de uso {#use-case}

Los especialistas en marketing pueden utilizar Adobe Real-Time CDP para crear una lista de personas de contactos de origen y activarla en Demandbase para una participación optimizada y orquestada en su plataforma del lado de la demanda (DSP) y otros canales como LinkedIn.

Este enfoque permite a los especialistas en marketing priorizar el gasto en campañas en individuos conocidos procedentes de su propio CRM o sistema de automatización de marketing, lo que garantiza que los esfuerzos de marketing se centren en perspectivas de alto valor.

Una vez activado, Demandbase optimiza la entrega de anuncios y refina las estrategias de segmentación para maximizar la participación, el alcance y las tasas de conversión, lo que a la larga mejora la eficacia de la campaña.

## Identidades admitidas {#supported-identities}

La conexión [!DNL Demandbase People] admite la activación de identidades descritas en la tabla siguiente. Más información sobre [identidades](/help/identity-service/features/namespaces.md).

| Identidad de destino | Descripción | Consideraciones |
|---|---|---|
| email | Direcciones de correo electrónico de texto sin formato | La conexión [!DNL Demandbase People] solo admite direcciones de correo electrónico de texto sin formato. |

{style="table-layout:auto"}

## Audiencias compatibles {#supported-audiences}

Esta sección describe qué tipo de audiencias puede exportar a este destino.

| Origen de audiencia | Admitido | Descripción |
---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Audiencias generadas a través del [servicio de segmentación](../../../segmentation/home.md) de Experience Platform. |
| Cargas personalizadas | X | Las audiencias [importadas](../../../segmentation/ui/overview.md#import-audience) en Experience Platform desde archivos CSV. |

{style="table-layout:auto"}

## Tipo y frecuencia de exportación {#export-type-and-frequency}

Consulte la tabla siguiente para obtener información sobre el tipo y la frecuencia de exportación de destino.

| Elemento | Tipo | Notas |
|--------------|-----------|---------------------------|
| Tipo de exportación | Exportación de audiencia | Va a exportar todos los miembros de una audiencia con los identificadores (nombre, número de teléfono u otros) utilizados en el destino *Demandbase*. |
| Frecuencia | Streaming | Los destinos de streaming son conexiones basadas en API &quot;siempre activadas&quot;. Tan pronto como se actualiza un perfil en Experience Platform basado en la evaluación de audiencias, el conector envía la actualización de forma descendente a la plataforma de destino. Más información sobre [destinos de streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Requisitos previos {#prerequisites}

Para exportar audiencias a Demandbase, necesita lo siguiente:

1. Una cuenta de Demandbase.
2. Un token de API de Demandbase. Puede generar un token de API con el usuario en Demandbase. Para generar un token, vaya a [Mi perfil > Token de API](https://web.demandbase.com/o/ad/at) después de iniciar sesión en su cuenta de Demandbase.

## Conexión al destino {#connect}

>[!IMPORTANT]
> 
>Para conectarse al destino, necesita el **[[!UICONTROL permiso de control de acceso]](/help/access-control/home.md#permissions) de Ver destinos&rbrack;** y **[!UICONTROL Administrar destinos]**&lbrack;para obtener acceso. Lea la [descripción general del control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Para conectarse a este destino, siga los pasos descritos en el [tutorial de configuración de destino](../../ui/connect-destination.md). En el flujo de trabajo de configuración de destino, rellene los campos enumerados en las dos secciones siguientes.

### Autenticarse en el destino {#authenticate}

Para autenticarse en el destino, rellene los campos obligatorios y seleccione **[!UICONTROL Conectar con destino]**.

![Agregar token de portador](../../assets/catalog/advertising/demandbase-people/bearer-token.png)

* **[!UICONTROL Token de portador]**: complete el token de portador para autenticarse en el destino. Vea [requisitos previos](#prerequisites) para obtener información sobre cómo obtener el token.

### Rellenar detalles de destino {#destination-details}

Para configurar los detalles del destino, rellene los campos obligatorios y opcionales a continuación. Un asterisco junto a un campo en la interfaz de usuario indica que el campo es obligatorio.

![Agregar información sobre la conexión de destino](../../assets/catalog/advertising/demandbase-people/name-and-description.png)

* **[!UICONTROL Nombre]**: Un nombre por el cual reconocerá este destino en el futuro.
* **[!UICONTROL Descripción]**: Una descripción que le ayudará a identificar este destino en el futuro.

Ahora está listo para activar sus audiencias en Demandbase People.

## Activar públicos en este destino {#activate}

>[!IMPORTANT]
> 
>* Para activar los datos, necesita los **[!UICONTROL permisos de control de acceso]**, **[!UICONTROL Activar destinos]**, **[!UICONTROL Ver perfiles]** y **[!UICONTROL Ver segmentos]**&#x200B;[para ](/help/access-control/home.md#permissions). Lea la [descripción general del control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.
>* Para exportar *identidades*, necesita el **[[!UICONTROL permiso de control de acceso]](/help/access-control/home.md#permissions) de&rbrack;** Ver gráfico de identidad&lbrack;. <br> ![Seleccione el área de nombres de identidad resaltada en el flujo de trabajo para activar audiencias en los destinos.](/help/destinations/assets/overview/export-identities-to-destination.png "Seleccione el área de nombres de identidad resaltada en el flujo de trabajo para activar audiencias en los destinos."){width="100" zoomable="yes"}

Lea [Activar perfiles y audiencias en destinos de exportación de audiencias de streaming](/help/destinations/ui/activate-segment-streaming-destinations.md) para obtener instrucciones sobre cómo activar audiencias en este destino.

## Notas adicionales y llamadas importantes {#additional-notes}

* **Protecciones de API de Demandbase**: Si ha exportado audiencias a Demandbase y las exportaciones se realizaron correctamente en Experience Platform, pero no todos los datos llegan a Demandbase, es posible que haya encontrado una limitación de API en Demandbase. Póngase en contacto con ellos para obtener una aclaración.
* **Eliminación de lista**: las listas de personas son únicas, por lo que no puede volver a crear una lista nueva con un nombre que ya esté en uso. Cuando elimine personas de una lista, ya no estarán disponibles, pero no se eliminarán.
* **Hora de activación**: la carga de datos en Demandbase está sujeta a un procesamiento nocturno.
* **Nomenclatura de audiencias**: Si una audiencia de cuenta con el mismo nombre se activó anteriormente en Demandbase, no puede volver a activarla a través de un flujo de datos diferente al destino de Demandbase.
