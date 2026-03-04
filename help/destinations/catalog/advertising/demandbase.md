---
title: Conexión de Demandbase
description: Utilice este destino para activar los públicos de cuenta para los casos de uso de Account-Based Marketing (ABM). Anuncie para personas y funciones relevantes en sus cuentas de destino a través de B2B Demand Side Platform (DSP) de DemandBase. Las cuentas de destino también se pueden enriquecer con datos de terceros de Demandbase para otros casos de uso posteriores en marketing y ventas.
last-substantial-update: 2024-09-30T00:00:00Z
exl-id: a84609a2-f1d3-4998-9db4-ad59c0a0b631
source-git-commit: 5a03902df358d804cbafb401ffcef54eab240dfd
workflow-type: tm+mt
source-wordcount: '914'
ht-degree: 15%

---


# Conexión de Demandbase {#demandbase}

>[!AVAILABILITY]
>
>La funcionalidad para activar audiencias de cuenta en el destino de Demandbase está disponible para compañías que compren las ediciones de [empresa a empresa](/help/rtcdp/overview.md#rtcdp-b2b) y [empresa a persona](/help/rtcdp/overview.md#rtcdp-b2p) de Real-Time Customer Data Platform.

Active perfiles para sus campañas de Demandbase para la segmentación, personalización y supresión de audiencias, en función de [audiencias de la cuenta](/help/segmentation/types/account-audiences.md)

## Ejemplo de uso {#use-case}

Utilice este destino para activar los públicos de cuenta para los casos de uso de Account-Based Marketing (ABM). Anuncie para personas y funciones relevantes en sus cuentas de destino a través de B2B Demand Side Platform (DSP) de DemandBase. Las cuentas de destino también se pueden enriquecer con datos de terceros de Demandbase para otros casos de uso posteriores en marketing y ventas.

Por ejemplo, aproveche la tecnología de publicidad de DSP de Demandbase para dirigirse a personas o funciones específicas dentro de cuentas clave para la generación de posibles clientes de la parte superior de funnel, o cree y aumente grupos de compra. Utilice el destino de Demandbase para explorar otros casos de uso y dirigir las cuentas de forma eficaz.

Con esta integración, también puede personalizar la experiencia del sitio web mediante la búsqueda de información de la cuenta en tiempo real para optimizar la participación.

## Audiencias compatibles {#supported-audiences}

Esta sección describe qué tipo de audiencias puede exportar a este destino.

| Origen de audiencia | Admitido | Descripción |
|---------|----------|----------|
| [!DNL Segmentation Service] | Sí | Audiencias generadas a través del [servicio de segmentación](../../../segmentation/home.md) de Experience Platform. |
| Todos los demás orígenes de audiencia | Sí | Esta categoría incluye todos los orígenes de audiencia fuera de las audiencias generadas a través de [!DNL Segmentation Service]. Obtenga información acerca de [varios orígenes de audiencia](/help/segmentation/ui/audience-portal.md#customize). Algunos ejemplos son: <ul><li> audiencias de carga personalizadas [importadas](../../../segmentation/ui/audience-portal.md#import-audience) a Experience Platform desde archivos CSV,</li><li> audiencias de similitud, </li><li> audiencias federadas, </li><li> audiencias generadas en otras aplicaciones de Experience Platform, como Adobe Journey Optimizer, </li><li> y más. </li></ul> |

{style="table-layout:auto"}

Audiencias compatibles por tipo de datos de audiencia:

| Tipo de datos de audiencia | Admitido | Descripción | Casos de uso |
|--------------------|-----------|-------------|-----------|
| [Audiencias de personas](/help/segmentation/types/people-audiences.md) | Sí | Basado en perfiles de clientes, lo que le permite dirigirse a grupos específicos de personas para campañas de marketing. | Compradores frecuentes, abandonadores del carro de compras |
| [Audiencias de la cuenta](/help/segmentation/types/account-audiences.md) | Sí | Segmente a individuos dentro de organizaciones específicas para estrategias de marketing basadas en cuentas. | Marketing B2B |
| [Audiencias potenciales](/help/segmentation/types/prospect-audiences.md) | No | Dirija la actividad a personas que aún no sean clientes, pero que compartan características con la audiencia a la que va dirigida. | Prospección con datos de terceros |
| [Exportaciones de conjuntos de datos](/help/catalog/datasets/overview.md) | No | Recopilaciones de datos estructurados almacenados en el lago de datos de Adobe Experience Platform. | Informes, flujos de trabajo de ciencia de datos |

{style="table-layout:auto"}

## Tipo y frecuencia de exportación {#export-type-and-frequency}

Consulte la tabla siguiente para obtener información sobre el tipo y la frecuencia de exportación de destino.

| Elemento | Tipo | Notas |
|--------------|-----------|---------------------------|
| Tipo de exportación | Exportación de audiencia | Todos los miembros de la audiencia se exportarán con identificadores clave como nombre, número de teléfono y más. |
| Frecuencia | Streaming | Conexiones basadas en API &quot;siempre activas&quot;. Las actualizaciones se envían de forma descendente inmediatamente después de los cambios de perfil. |

{style="table-layout:auto"}

## Requisitos previos {#prerequisites}

Para exportar audiencias de cuenta a Demandbase, necesita lo siguiente:

1. Una cuenta de Demandbase.
2. Un token de API de Demandbase. Puede generar un token de API con el usuario en Demandbase. Para generar un token, vaya a [Mi perfil > Token de API](https://web.demandbase.com/o/ad/at) después de iniciar sesión en su cuenta de Demandbase.

## Conectar con el destino {#connect}

>[!IMPORTANT]
> 
>Para conectarse al destino, necesita el permiso de control de acceso **[!UICONTROL View Destinations]** y **[!UICONTROL Manage Destinations]** [3}. ](/help/access-control/home.md#permissions) Lea la [descripción general del control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Para conectarse a este destino, siga los pasos descritos en el [tutorial de configuración de destino](../../ui/connect-destination.md). En el flujo de trabajo de configuración de destino, rellene los campos enumerados en las dos secciones siguientes.

### Autenticarse en el destino {#authenticate}

Para autenticarse en el destino, rellene los campos obligatorios y seleccione **[!UICONTROL Connect to destination]**.

![Agregar token de portador](/help/destinations/assets/catalog/advertising/demandbase/add-bearer-token.png)

* **[!UICONTROL Bearer token]**: complete el token de portador para autenticarse en el destino. Vea [requisitos previos](#prerequisites) para obtener información sobre cómo obtener el token.

### Rellenar detalles de destino {#destination-details}

Para configurar los detalles del destino, rellene los campos obligatorios y opcionales a continuación. Un asterisco junto a un campo en la interfaz de usuario indica que el campo es obligatorio.

![Agregar información sobre la conexión de destino](/help/destinations/assets/catalog/advertising/demandbase/name-and-description.png)

* **[!UICONTROL Name]**: un nombre con el cual reconocerá este destino en el futuro.
* **[!UICONTROL Description]**: una descripción que le ayudará a identificar este destino en el futuro.
* **[!UICONTROL Entity type]**: seleccione **[!UICONTROL Account]** como tipo de entidad.

Ahora está listo para activar sus audiencias en Demandbase.

## Activar públicos en este destino {#activate}

>[!IMPORTANT]
> 
>* Para activar los datos, necesita los permisos de control de acceso **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** y **[!UICONTROL View Segments]** [5}. ](/help/access-control/home.md#permissions) Lea la [descripción general del control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.
>* Para exportar *identidades*, necesita el **[!UICONTROL View Identity Graph]** [permiso de control de acceso](/help/access-control/home.md#permissions). <br> ![Seleccione el área de nombres de identidad resaltada en el flujo de trabajo para activar audiencias en los destinos.](/help/destinations/assets/overview/export-identities-to-destination.png "Seleccione el área de nombres de identidad resaltada en el flujo de trabajo para activar audiencias en los destinos."){width="100" zoomable="yes"}

Lea [Activar audiencias de cuenta](/help/destinations/ui/activate-account-audiences.md) para obtener instrucciones sobre cómo activar audiencias de cuenta en este destino.

### Asignaciones obligatorias {#mandatory-mappings}

Al activar audiencias en el destino [!DNL Demandbase], debe configurar las siguientes asignaciones de campos obligatorias en el paso de asignación:

| Campo de origen | Campo de destino | Descripción |
|--------------|--------------|-------------|
| `xdm: accountName` | `xdm: accountName` | El nombre de la cuenta |
| `xdm: accountOrganization.domain` | `xdm: accountEmailDomain` | El dominio de correo electrónico de la organización de la cuenta |
| `xdm: accountKey.sourceKey` | `Identity: primaryId` | El identificador principal de la cuenta |

![Asignaciones de Demandbase](/help/destinations/assets/catalog/advertising/demandbase/demandbase-mapping.png)

Estas asignaciones son necesarias para que el destino funcione correctamente y deben configurarse antes de continuar con el flujo de trabajo de activación.

## Notas adicionales y llamadas importantes {#additional-notes}

* **Nomenclatura de audiencias**: Si una audiencia de cuenta con el mismo nombre se activó anteriormente en Demandbase, no puede volver a activarla a través de un flujo de datos diferente al destino de Demandbase.
* **Protecciones de API de Demandbase**: Si ha exportado audiencias a Demandbase y las exportaciones se realizaron correctamente en Experience Platform, pero no todos los datos llegan a Demandbase, es posible que haya encontrado una limitación de API en Demandbase. Póngase en contacto con ellos para obtener una aclaración.
* **Eliminación de lista**: las listas de cuentas son únicas, por lo que no puede volver a crear una lista nueva con un nombre que ya esté en uso. Al eliminar cuentas de una lista, estas ya no estarán disponibles, pero no se eliminarán.
* **Hora de activación**: la carga de datos en Demandbase está sujeta a un procesamiento nocturno.
