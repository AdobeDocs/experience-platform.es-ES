---
title: Página Detalles de Destinos
seo-title: Página Detalles de Destinos
description: 'La página de detalles de un destino individual proporciona información general sobre los detalles del destino, como el nombre del destino, el ID, los segmentos asignados al destino y los controles para editar la activación y habilitar y deshabilitar el flujo de datos. '
seo-description: 'La página de detalles de un destino individual proporciona información general sobre los detalles del destino, como el nombre del destino, el ID, los segmentos asignados al destino y los controles para editar la activación y habilitar y deshabilitar el flujo de datos. '
translation-type: tm+mt
source-git-commit: b784b67092ea8d30ad00cda9a40779b3890862fd

---


# Página de detalles de destino {#destinations-details-page}

La página de detalles de un destino individual proporciona información general sobre los detalles del destino, como el nombre del destino, el ID, los segmentos asignados al destino y los controles para editar la activación y habilitar y deshabilitar el flujo de datos. Para ver estos detalles, vaya a **Destinos** > **Examinar** y haga clic en el nombre del destino con el que desee trabajar.

Los componentes principales de un destino individual son:

* 1 - Nombre e ID de destino
* 2 - Segmentos activados en destino
* 3 - Información del carril derecho
* 4 - Controles para editar la activación y habilitar/deshabilitar el flujo de datos

![Página de destinos numerada](/help/rtcdp/destinations/assets/destination-page-numbered.png)

Vaya a una página de destino individual para obtener una descripción general de los detalles de destino, como:

## 1. Nombre e ID de destino

Puede ver el nombre de destino en el encabezado de página y el ID de destino en la dirección URL de la página.

## 2. Segmentos activados en destino

Esta sección muestra qué segmentos están asignados actualmente al destino, así como información adicional sobre dichos segmentos. Consulte la tabla siguiente para obtener más información:

| Elemento | Descripción |
---------|----------|
| Nombre del segmento | El nombre del segmento. |
| Descripción del segmento | Descripción del segmento. |
| Fecha inicial | La fecha a partir de la cual se activan estos segmentos en el destino. |
| Fecha final | Fecha en la que estos segmentos dejarán de activarse en el destino. |
| ID de asignación | *No disponible para destinos* de marketing por correo electrónico. Indica el ID por el que se conoce el segmento en la plataforma de destino. |

## 3. Información del carril derecho

El carril correcto incluye información sobre el destino. Consulte la tabla siguiente para obtener más información:

| Elemento | Descripción |
---------|----------|
| Plataforma | Representa la plataforma de destino a la que se envían las audiencias. Consulte [Catálogo](/help/rtcdp/destinations/destinations-catalog.md) de destinos para obtener más información. |
| Descripción | Puede editar la descripción del flujo de destino. |
| Categoría | Indica el tipo de destino. Consulte [Catálogo](/help/rtcdp/destinations/destinations-catalog.md) de destinos para obtener más información. |
| Tipo de conexión | Indica en qué formulario se envían las audiencias al destino. Puede ser **Cookie** o basada en **perfiles**. |
| Frecuencia | Indica la frecuencia con la que se envían las audiencias al destino. Puede ser por **flujo** o **por lotes**. |
| Identidad | Representa el espacio de nombres de identidad aceptado por el destino. Por ejemplo, el campo Identidad puede ser GAID, IDFA o correo electrónico. Para todos los espacios de nombres de identidad aceptados, consulte los espacios de nombres estándar en la descripción general [del espacio de nombres](https://www.adobe.io/apis/experienceplatform/home/profile-identity-segmentation/profile-identity-segmentation-services.html#!api-specification/markdown/narrative/technical_overview/identity_namespace_overview/identity_namespace_overview.md)Identity. |
| Creado por | Indica el usuario que ha creado este flujo de destino. |
| Creación | Indica la fecha y hora UTC en que se creó este flujo de destino. |

## 4. Controles para editar la activación y habilitar/deshabilitar el flujo de datos

El control de activación Editar permite editar los segmentos asignados al destino. Pulse Editar activación para abrir el flujo de trabajo [de activación de](/help/rtcdp/destinations/activate-destinations.md)segmentos.

Utilice el botón **Activar/Desactivar** para iniciar y pausar la exportación de datos a un destino.