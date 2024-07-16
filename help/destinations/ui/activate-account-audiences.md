---
title: Activar audiencias de cuenta en destinos
type: Tutorial
description: Obtenga información sobre cómo activar audiencias de cuenta en destinos
badgeB2B: label="Edición B2B" type="Informative" url=" https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html?lang=en#rtcdp-editions newtab=true"
badgeB2P: label="Edición B2P" type="Positive" url=" https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html?lang=en#rtcdp-editions newtab=true"
exl-id: ad69d0a8-bf5b-42ac-97a3-401eadda62cd
source-git-commit: dff460f0b0d365d3d643744544642d9f9488e18a
workflow-type: tm+mt
source-wordcount: '834'
ht-degree: 0%

---

# Activar audiencias de cuenta

>[!AVAILABILITY]
>
>La funcionalidad para activar audiencias de cuenta en destinos está disponible para compañías que compren las ediciones de Real-time Customer Data Platform [De empresa a empresa](/help/rtcdp/overview.md#rtcdp-b2b) y [De empresa a persona](/help/rtcdp/overview.md#rtcdp-b2p).

En este artículo se explica el flujo de trabajo necesario para exportar [audiencias de cuenta](/help/segmentation/ui/account-audiences.md) de Adobe Experience Platform a su destino preferido.

## Destinos admitidos {#supported-destinations}

Vaya a **[!UICONTROL Conexiones]** > **[!UICONTROL Destinos]** y seleccione la ficha **[!UICONTROL Catálogo]**. Use el filtro **[!UICONTROL Tipos de datos]** y seleccione **[!UICONTROL Cuentas]** para ver los destinos que admiten la activación de audiencias de cuenta. Actualmente, la exportación de audiencias de cuenta solo está disponible para determinados destinos de almacenamiento en la nube ([Amazon S3](/help/destinations/catalog/cloud-storage/amazon-s3.md), [ADLS Gen 2](/help/destinations/catalog/cloud-storage/adls-gen2.md), [Azure Blob Storage](/help/destinations/catalog/cloud-storage/azure-blob.md), [Data Landing Zone](/help/destinations/catalog/cloud-storage/data-landing-zone.md) y [SFTP](/help/destinations/catalog/cloud-storage/sftp.md)) y el destino de [(Empresas) audiencias coincidentes de LinkedIn](/help/destinations/catalog/social/linkedin.md).

![Destinos que admiten audiencias de cuenta.](/help/destinations/assets/ui/activate-account-audiences/data-types-filter.png)

## Vídeo introductorio

Vea el siguiente vídeo para obtener información general sobre la creación y activación de audiencias de cuenta y los casos de uso admitidos al activar audiencias de cuenta.

>[!VIDEO](https://video.tv.adobe.com/v/338252/?learn=on)

## Requisitos previos {#prerequisites}

* Primero debe ingerir [perfiles de cuenta](/help/rtcdp/accounts/account-profile-overview.md) y crear [audiencias de cuenta](/help/segmentation/ui/account-audiences.md) para poder activarlos en destinos de flujo descendente.
* Para activar audiencias de cuenta en destinos, debe haberse conectado correctamente a un destino. Si aún no lo ha hecho, vaya al [catálogo de destinos](../catalog/overview.md), examine los destinos admitidos y configure el destino que desee utilizar. Lea el tutorial de la interfaz de usuario sobre [conexión a destinos](./connect-destination.md) para obtener más información.

### Permisos necesarios {#permissions}

Para activar audiencias de cuenta, necesitas los **[!UICONTROL permisos de control de acceso](/help/access-control/home.md#permissions) de Ver destinos]** y **[!UICONTROL Activar destinos]**[5}. Lea la [descripción general del control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Para asegurarse de que tiene los permisos necesarios para activar audiencias de cuenta, examine el catálogo de destinos. Si un destino tiene un control **[!UICONTROL Activate]**, usted cuenta con los permisos apropiados.

## Seleccione su destino {#select-destination}

Siga las instrucciones para seleccionar un destino al que exportar los conjuntos de datos:

1. Vaya a **[!UICONTROL Conexiones > Destinos]** y seleccione la pestaña **[!UICONTROL Catálogo]**.

   ![Pestaña Catálogo de destino con control de catálogo resaltado.](/help/destinations/assets/ui/export-datasets/catalog-tab.png)

1. Seleccione **[!UICONTROL Activar]** en la tarjeta correspondiente al destino al que desea exportar los conjuntos de datos.

>[!TIP]
>
>Los destinos que pueden exportar audiencias de cuenta se indican con un icono en la esquina superior derecha de la tarjeta, similar al destino resaltado más abajo, o puede usar el filtro de tipo de datos para mostrar solo los destinos que pueden exportar audiencias de cuenta, como [se muestra más arriba en la página](#supported-destinations).

![Página de destino de Amazon S3 que puede exportar audiencias de perfil resaltadas.](/help/destinations/assets/ui/activate-account-audiences/amazon-s3-icon-activate-account-audiences.png)

1. Seleccione **[!UICONTROL Cuentas de tipo de datos]**, seguidas de la conexión de destino a la que desea exportar conjuntos de datos y, a continuación, seleccione **[!UICONTROL Siguiente]**.

>[!TIP]
> 
>Si desea configurar un nuevo destino para activar las audiencias de la cuenta, seleccione **[!UICONTROL Configurar nuevo destino]** para almacenar en déclencheur el flujo de trabajo [Conectarse al destino](/help/destinations/ui/connect-destination.md) y [seleccionar cuentas como tipo de datos](/help/destinations/ui/connect-destination.md#segment-activation-or-dataset-exports).

![Flujo de trabajo de activación de destino con control de cuentas resaltado.](/help/destinations/assets/ui/activate-account-audiences/activate-account-audiences-highlighted.png)

1. Continúe con la siguiente sección para [seleccionar las audiencias de su cuenta](#select-profile-audiences) para la exportación.

## Seleccione las audiencias de la cuenta {#select-account-audiences}

Utilice las casillas de verificación de la izquierda de los nombres de audiencias de la cuenta para seleccionar las audiencias que desea exportar al destino y, a continuación, seleccione **[!UICONTROL Siguiente]**. Tenga en cuenta que solo se muestran *audiencias de cuenta* en esta vista, y no se muestran otros tipos de audiencia.

![Flujo de trabajo de exportación del conjunto de datos que muestra el paso Seleccionar audiencias, donde puede seleccionar qué audiencias de cuenta desea exportar.](/help/destinations/assets/ui/activate-account-audiences/select-account-audiences.png)

## Programación y pasos siguientes

Para el resto del flujo de trabajo de activación para exportar audiencias de cuenta, lea el tutorial sobre la activación de datos en destinos basados en archivos. Continúe desde el paso [programar exportación de audiencia](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling). Si está activando audiencias de cuenta en el destino **[!UICONTROL (Compañías) Audiencias coincidentes de LinkedIn]**, lea el tutorial sobre la activación de destinos de flujo continuo. Continúe desde el [paso de asignación](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping).

>[!NOTE]
>
>Tenga en cuenta que en el paso de programación al exportar audiencias de cuenta a destinos de almacenamiento en la nube, el flujo de trabajo para activar audiencias de cuenta solo le permite exportar [archivos completos](/help/destinations/ui/activate-batch-profile-destinations.md#export-full-files) y [archivos incrementales](/help/destinations/ui/activate-batch-profile-destinations.md#export-incremental-files) _en una programación diaria_. No se admiten exportaciones por hora. Tenga en cuenta también que **[!UICONTROL Después de la evaluación de audiencia]** es el único tipo de evaluación admitido.

## Llamadas importantes y limitaciones conocidas {#important-callouts-known-limitations}

Tenga en cuenta las siguientes llamadas importantes y limitaciones conocidas para la versión de disponibilidad general de la funcionalidad para activar audiencias de cuenta.

### Pares de asignación requeridos en el paso de asignación al activar audiencias de cuenta en el destino **[!UICONTROL (Compañías) Audiencias coincidentes de LinkedIn]** {#required-mappings}

Al activar audiencias de cuenta en el destino **[!UICONTROL (Compañías) Audiencias coincidentes de LinkedIn]**, tenga en cuenta que los dos pares de asignación siguientes son obligatorios para exportar datos correctamente:

![Campos obligatorios de asignación de LinkedIn.](/help/destinations/assets/ui/activate-account-audiences/linkedin-mapping-required-fields.png)

| Campo de origen | Campo de destino |
|---------|----------|
| `accountName` | `companyName` |
| `accountKey.sourceKey` | `primaryId` (seleccione este campo en la vista **[!UICONTROL Seleccionar área de nombres de identidad]** al seleccionar el **[!UICONTROL Campo de destino]**). <br> ![Seleccione el área de nombres de identidad resaltada en el flujo de trabajo para activar las audiencias de cuenta en los destinos.](/help/destinations/assets/ui/activate-account-audiences/identity-namespace-highlighted.png "Seleccione el área de nombres de identidad resaltada en el flujo de trabajo para activar las audiencias de cuenta en los destinos."){width="100" zoomable="yes"} |

### Aplicación de gobernanza de datos {#data-governance-enforcement}

El consentimiento se aplica en el nivel de persona o perfil para *clientes y clientes potenciales*. Por lo tanto, [la evaluación de la directiva de consentimiento](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation) no se admite actualmente al activar audiencias de cuenta en destinos. En el paso de revisión del flujo de trabajo de activación, puede ver un control atenuado para **[!UICONTROL Ver directivas de consentimiento aplicables]**.

![Revise el paso del flujo de trabajo para activar audiencias de cuenta con el control de aplicación de consentimiento atenuado.](/help/destinations/assets/ui/activate-account-audiences/consent-checks-greyed-out.png)

Se admiten otros mecanismos de control de datos en Real-Time CDP, como [comprobaciones de directivas de uso de datos](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation) y [control de acceso basado en atributos](/help/destinations/home.md#attribute-based-access).
