---
solution: Experience Platform
title: Audiencias de personas
description: Aprenda a segmentar usuarios que utilizan audiencias de personas.
source-git-commit: d73f8c47f9eedff05446688f0c798c322e51aa5d
workflow-type: tm+mt
source-wordcount: '524'
ht-degree: 1%

---

# Guía de audiencias de People

En Adobe Experience Platform, las audiencias basadas en personas le permiten dirigirse a grupos específicos de personas para sus campañas de marketing.

Las audiencias de People utilizan datos de perfil del cliente para dirigirse a mercados específicos, lo que permite dirigirse mejor a sectores demográficos específicos hacia los que desea realizar publicidad.

## Terminología {#terminology}

Antes de comenzar con la audiencia de personas, revise las diferencias entre los distintos tipos de audiencia:

- **Audiencias de cuenta**: una audiencia de cuenta es una audiencia que se crea usando los datos de perfil de **account**. Los datos de perfil de cuenta se pueden utilizar para crear audiencias dirigidas a personas dentro de cuentas de flujo descendente. Para obtener más información acerca de las audiencias de la cuenta, lea [descripción general de la audiencia de la cuenta](./account-audiences.md).
- **Audiencias de personas**: una audiencia de personas es una audiencia creada con datos de perfil de **cliente**. Los datos de perfil del cliente se pueden utilizar para crear audiencias dirigidas a la clientela de su empresa.
- **Audiencias clientes potenciales**: una audiencia cliente potencial es una audiencia creada con datos de perfil de **cliente potencial**. Los datos de perfil del cliente potencial se pueden utilizar para crear audiencias de usuarios no autenticados. Para obtener más información sobre las audiencias de clientes potenciales, lea la [descripción general de la audiencia de clientes potenciales](./prospect-audiences.md).

## Acceso {#access}

Para acceder a las audiencias de personas, seleccione **[!UICONTROL Audiencias]** en la sección **[!UICONTROL Clientes]**.

![La ficha Audiencias está resaltada en la sección Clientes.](../images/types/people/select-audiences.png)

Se muestra Audience Portal, con una lista de todas las audiencias de personas de la organización.

![Se muestra el portal de audiencias para audiencias de personas.](../images/types/people/people-audiences.png)

Esta vista muestra información sobre la audiencia, incluido el nombre, el recuento de perfiles, el origen, el estado del ciclo vital, la fecha de creación y la fecha de la última actualización.

También puede utilizar la funcionalidad de búsqueda y filtrado para buscar y ordenar rápidamente audiencias de cuenta específicas. Encontrará más información sobre esta característica en la [descripción general de Audience Portal](../ui/audience-portal.md#manage-audiences).

## Detalles de público {#details}

Para ver detalles sobre una audiencia de personas específica, seleccione una audiencia en Audience Portal.

![Una audiencia especificada está resaltada en el Portal de audiencias.](../images/types/people/select-audience.png)

Se muestra la página de detalles de la audiencia. Se muestra información, incluida la descripción, el origen y el estado del ciclo vital.

![Se muestra la página de detalles de audiencia, con información sobre la audiencia de personas.](../images/types/people/audience-details.png)

Para obtener más información acerca de la página de detalles de audiencia, lea la [sección de detalles de audiencia de la descripción general del portal de audiencia](../ui/audience-portal.md#audience-details).

## Crear público {#create}

Puede crear una audiencia de personas mediante el Compositor de audiencias o el Generador de segmentos. Para empezar a crear una audiencia de personas, seleccione Crear audiencia en Audience Portal.

![El botón Crear audiencia está resaltado.](../images/types/people/select-create-audience.png)

Aparece una ventana emergente que le permite elegir entre componer una audiencia o crear reglas.

![Se muestra una ventana emergente que muestra una opción entre composición, audiencia y reglas de creación.](../images/types/people/create-audience-popover.png)

Para obtener información más detallada sobre la creación de audiencias, lea [Información general del portal de audiencias](../ui/audience-portal.md#create-audience).

## Activar público {#activate}

Después de crear la audiencia de personas, puede activarla en otros servicios descendentes.

Seleccione la audiencia que desee activar, seguida de **[!UICONTROL Activar en destino]**.

![El botón Activar en destino está resaltado en el menú de acciones rápidas.](../images/types/people/activate-to-destination.png)

Aparecerá la página [!UICONTROL Activar destino], con la lista de destinos disponibles según la frecuencia de actualización de la audiencia. Para obtener más información sobre el proceso de activación, lea la [descripción general de la activación](../../destinations/ui/activation-overview.md).

## Pasos siguientes

Después de leer esta guía, sabe cómo crear y administrar las audiencias de sus recursos en Adobe Experience Platform. Para obtener más información sobre los distintos tipos de audiencias, lea la [descripción general de los tipos de audiencias](./overview.md).
