---
title: Activar audiencias de clientes potenciales en destinos
type: Tutorial
description: Obtenga información sobre cómo activar audiencias de clientes potenciales en destinos
exl-id: 3e034a14-09d0-4b08-b171-5afb62ae4b62
source-git-commit: e7c0551276d31d6809ace096c00e0dc2665090e6
workflow-type: tm+mt
source-wordcount: '619'
ht-degree: 13%

---

# Activar públicos de clientes potenciales

>[!AVAILABILITY]
>
>Esta funcionalidad está disponible para los clientes que han adquirido el paquete Real-Time CDP Prime y Ultimate. Póngase en contacto con su representante de Adobe para obtener más información.

En este artículo se explica el flujo de trabajo necesario para exportar [audiencias de clientes potenciales](/help/segmentation/types/prospect-audiences.md) de Adobe Experience Platform a su destino preferido.

## Destinos admitidos {#supported-destinations}

Vaya a **[!UICONTROL Conexiones]** > **[!UICONTROL Destinos]** y seleccione la ficha **[!UICONTROL Catálogo]**. Use el filtro **[!UICONTROL Tipos de datos]** y seleccione **[!UICONTROL Clientes potenciales]** para ver los destinos que admiten la activación de audiencias de clientes potenciales. Actualmente, la exportación de audiencias potenciales solo está disponible para destinos de almacenamiento en la nube.

![Destinos que admiten audiencias de clientes potenciales.](/help/destinations/assets/ui/activate-prospect-audiences/data-types-filter.png)

## Requisitos previos {#prerequisites}

* Primero debe ingerir [perfiles de clientes potenciales](/help/profile/ui/prospect-profile.md) y crear [audiencias de clientes potenciales](/help/segmentation/types/prospect-audiences.md) para poder activarlos en destinos descendentes.
* Para activar audiencias de clientes potenciales en destinos, debe haberse conectado correctamente a un destino. Si aún no lo ha hecho, vaya al [catálogo de destinos](../catalog/overview.md), examine los destinos admitidos y configure el destino que desee utilizar. Lea el tutorial de la interfaz de usuario sobre [conexión a destinos](./connect-destination.md) para obtener más información.

### Permisos necesarios {#permissions}

Para activar las audiencias de clientes potenciales, necesitas los **[[!UICONTROL permisos de control de acceso]](/help/access-control/home.md#permissions) de Ver destinos&rbrack;** y **[!UICONTROL Activar destinos]**&lbrack;5&rbrace;. Lea la [descripción general del control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Para asegurarse de que dispone de los permisos necesarios para activar las audiencias de clientes potenciales, consulte el catálogo de destinos. Si un destino tiene un control **[!UICONTROL Activate]**, usted cuenta con los permisos apropiados.

## Seleccione su destino {#select-destination}

Siga las instrucciones para seleccionar un destino al que exportar los conjuntos de datos:

1. Vaya a **[!UICONTROL Conexiones > Destinos]** y seleccione la pestaña **[!UICONTROL Catálogo]**.

   ![Pestaña Catálogo de destino con control de catálogo resaltado.](/help/destinations/assets/ui/export-datasets/catalog-tab.png)

2. Seleccione **[!UICONTROL Activar]** en la tarjeta correspondiente al destino al que desea exportar los conjuntos de datos.

>[!TIP]
>
>Los destinos que pueden exportar audiencias de perfil se indican con un icono en la esquina superior derecha de la tarjeta, similar al destino resaltado más abajo, o puede usar el filtro de tipo de datos para mostrar solo los destinos que pueden exportar audiencias de clientes potenciales, como [se muestra más arriba en la página](#supported-destinations).

![Página de destino de Amazon S3 que puede exportar audiencias de perfil resaltadas.](/help/destinations/assets/ui/activate-prospect-audiences/amazon-s3-icon-activate-prospect-audiences.png)

1. Seleccione **[!UICONTROL Perspectivas de tipo de datos]**, seguido de la conexión de destino a la que desea exportar conjuntos de datos y, a continuación, seleccione **[!UICONTROL Siguiente]**.

>[!TIP]
> 
>Si desea configurar un nuevo destino para activar las audiencias de clientes potenciales, seleccione **[!UICONTROL Configurar nuevo destino]** para almacenar en déclencheur el flujo de trabajo [Conectarse al destino](/help/destinations/ui/connect-destination.md).

![Flujo de trabajo de activación de destino con control de clientes potenciales resaltado.](/help/destinations/assets/ui/activate-prospect-audiences/activate-prospects-highlighted.png)

1. Continúe con la siguiente sección para [seleccionar las audiencias de perfil](#select-profile-audiences) para la exportación.

## Seleccionar las audiencias de clientes potenciales {#select-prospect-audiences}

Utilice las casillas de verificación de la izquierda de los nombres de audiencias de clientes potenciales para seleccionar las audiencias que desea exportar al destino y, a continuación, seleccione **[!UICONTROL Siguiente]**. Tenga en cuenta que solo se muestran las audiencias de clientes potenciales en esta vista y no se muestran otras audiencias.

![Flujo de trabajo de exportación del conjunto de datos que muestra el paso Seleccionar audiencias, donde puede seleccionar qué audiencias de cliente potencial exportar.](/help/destinations/assets/ui/activate-prospect-audiences/select-prospect-audiences.png)

## Programación y pasos siguientes

Para el resto del flujo de trabajo de activación para exportar audiencias potenciales, lea el tutorial sobre la activación de datos en destinos basados en archivos. Continúe desde el paso [programar exportación de audiencia](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling).

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
* [Aproveche el reconocimiento ayudado por los socios para personalizar las experiencias en el sitio](/help/rtcdp/partner-data/onsite-personalization.md) durante la visita sin que el usuario se autentique ni tenga un historial previo con su marca.
