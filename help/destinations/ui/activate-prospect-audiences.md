---
title: Activar audiencias de clientes potenciales en destinos
type: Tutorial
description: Obtenga información sobre cómo activar audiencias de clientes potenciales en destinos
exl-id: 3e034a14-09d0-4b08-b171-5afb62ae4b62
source-git-commit: fdb9d7b168d6323fddaab1ac7abc44d3a390afea
workflow-type: tm+mt
source-wordcount: '620'
ht-degree: 12%

---

# Activar audiencias de clientes potenciales

>[!AVAILABILITY]
>
>Esta funcionalidad está disponible para los clientes que han adquirido el paquete Real-Time CDP Prime y Ultimate. Póngase en contacto con el representante del Adobe para obtener más información.

Este artículo explica el flujo de trabajo necesario para exportar [audiencias de clientes potenciales](/help/segmentation/ui/prospect-audience.md) de Adobe Experience Platform a su destino preferido.

## Destinos admitidos {#supported-destinations}

Ir a **[!UICONTROL Conexiones]** > **[!UICONTROL Destinos]** y seleccione la opción **[!UICONTROL Catálogo]** pestaña. Utilice el **[!UICONTROL Tipos de datos]** filtrar y seleccionar **[!UICONTROL Posibles clientes]** para ver los destinos que admiten la activación de audiencias de clientes potenciales. Actualmente, la exportación de audiencias potenciales solo está disponible para destinos de almacenamiento en la nube.

![Destinos que admiten audiencias de clientes potenciales.](/help/destinations/assets/ui/activate-prospect-audiences/data-types-filter.png)

## Requisitos previos {#prerequisites}

* Primero debe ingerir [perfiles de clientes potenciales](/help/profile/ui/prospect-profile.md) y crear [audiencias de clientes potenciales](/help/segmentation/ui/prospect-audience.md) antes de poder activarlos en destinos de flujo descendente.
* Para activar audiencias de clientes potenciales en destinos, debe haberse conectado correctamente a un destino. Si aún no lo ha hecho, vaya al [catálogo de destinos](../catalog/overview.md), examine los destinos admitidos y configure el destino que desee utilizar. Lea el tutorial de la interfaz de usuario sobre [conexión a destinos](./connect-destination.md) para obtener más información.

### Permisos necesarios {#permissions}

Para activar audiencias de clientes potenciales, necesita el **[!UICONTROL Administrar destinos]**, **[!UICONTROL Ver destinos]**, **[!UICONTROL Activar destinos]** [permisos de control de acceso](/help/access-control/home.md#permissions). Lea el [información general de control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Para asegurarse de que dispone de los permisos necesarios para activar las audiencias de clientes potenciales, consulte el catálogo de destinos. Si un destino tiene un **[!UICONTROL Activar]** control y, a continuación, dispone de los permisos adecuados.

## Seleccione su destino {#select-destination}

Siga las instrucciones para seleccionar un destino al que exportar los conjuntos de datos:

1. Ir a **[!UICONTROL Conexiones > Destinos]** y seleccione la opción **[!UICONTROL Catálogo]** pestaña.

   ![Pestaña Catálogo de destino con control de catálogo resaltado.](/help/destinations/assets/ui/export-datasets/catalog-tab.png)

2. Seleccionar **[!UICONTROL Activar]** en la tarjeta correspondiente al destino al que desee exportar los conjuntos de datos.

>[!TIP]
>
>Los destinos que pueden exportar audiencias de perfil se indican con un icono en la esquina superior derecha de la tarjeta, similar al destino resaltado a continuación, o puede utilizar el filtro de tipo de datos para mostrar solo los destinos que pueden exportar audiencias de cliente potencial, como [se muestra más arriba en la página](#supported-destinations).

![Página de destino de Amazon S3 que puede exportar audiencias de perfil resaltadas.](/help/destinations/assets/ui/activate-prospect-audiences/amazon-s3-icon-activate-prospect-audiences.png)

1. Seleccionar **[!UICONTROL Tipo de datos: clientes potenciales]**, seguido de la conexión de destino a la que desea exportar los conjuntos de datos y, a continuación, seleccione **[!UICONTROL Siguiente]**.

>[!TIP]
> 
>Si desea configurar un nuevo destino para activar audiencias de clientes potenciales, seleccione **[!UICONTROL Configurar nuevo destino]** para almacenar en déclencheur el [Conectar con destino](/help/destinations/ui/connect-destination.md) flujo de trabajo.

![Flujo de trabajo de activación de destino con control de clientes potenciales resaltado.](/help/destinations/assets/ui/activate-prospect-audiences/activate-prospects-highlighted.png)

1. Continúe con la siguiente sección para [seleccionar las audiencias de perfil](#select-profile-audiences) para la exportación.

## Seleccionar las audiencias de clientes potenciales {#select-prospect-audiences}

Utilice las casillas de verificación de la izquierda de los nombres de las audiencias de clientes potenciales para seleccionar las audiencias que desea exportar al destino y, a continuación, seleccione **[!UICONTROL Siguiente]**. Tenga en cuenta que solo se muestran las audiencias de clientes potenciales en esta vista y no se muestran otras audiencias.

![Flujo de trabajo de exportación de conjuntos de datos que muestra el paso Seleccionar audiencias, donde puede seleccionar qué audiencias de cliente potencial exportar.](/help/destinations/assets/ui/activate-prospect-audiences/select-prospect-audiences.png)

## Programación y pasos siguientes

Para el resto del flujo de trabajo de activación para exportar audiencias potenciales, lea el tutorial sobre la activación de datos en destinos basados en archivos. Continúe desde el [paso programar exportación de audiencia](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling).

>[!NOTE]
>
>Tenga en cuenta que en el paso de programación, el flujo de trabajo para activar audiencias de clientes potenciales solo le permite [exportar archivos completos](/help/destinations/ui/activate-batch-profile-destinations.md#export-full-files). No se admiten exportaciones de archivos incrementales.

<!--

Note that we will need to add links to other destination types here as more destinations become supported 

-->

## Otros casos de uso obtenidos mediante la compatibilidad con datos de socios {#other-use-cases}

Explore más casos de uso habilitados a través de la compatibilidad con datos de socios en Real-Time CDP:

* [Complemente perfiles de origen con atributos de socios de datos de confianza para mejorar la base de datos, obtener nueva información sobre la base de clientes y optimizar mejor los públicos.](/help/rtcdp/partner-data/supplement-first-party-profiles.md)
* Utilice la compatibilidad con datos de terceros en Real-Time CDP para [ampliar su base de perfiles con perfiles potenciales de socios de datos y participe con ellos para adquirir o llegar a nuevos clientes](/help/rtcdp/partner-data/prospecting.md).
* [Aproveche el reconocimiento asistido por socios para personalizar las experiencias en el sitio](/help/rtcdp/partner-data/onsite-personalization.md) durante la visita sin que el usuario se autentique ni tenga historial previo con su marca.
