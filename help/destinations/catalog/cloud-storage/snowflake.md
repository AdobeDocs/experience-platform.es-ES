---
title: Conexión de Snowflake
description: Exporte datos a su cuenta de Snowflake mediante anuncios privados.
hide: true
hidefromtoc: true
badgeBeta: label="Beta" type="Informative"
exl-id: 4a00e46a-dedb-4dd3-b496-b0f4185ea9b0
source-git-commit: dca3762169d2a469948ee7e877213697f4c444b6
workflow-type: tm+mt
source-wordcount: '1126'
ht-degree: 6%

---

# Conexión de Snowflake {#snowflake-destination}

>[!IMPORTANT]
>
>Este conector de destino está en versión beta y solo está disponible para clientes seleccionados. Para solicitar acceso, póngase en contacto con su representante de Adobe.

## Información general {#overview}

Use el conector de destino de Snowflake para exportar datos a la instancia de Snowflake de Adobe, que Adobe luego compartirá con su instancia a través de [listados privados](https://other-docs.snowflake.com/en/collaboration/collaboration-listings-about).

Lea las siguientes secciones para comprender cómo funciona el destino de Snowflake y cómo se transfieren los datos entre Adobe y Snowflake.

### Funcionamiento del uso compartido de datos Snowflake {#data-sharing}

Este destino usa un recurso compartido de datos de [!DNL Snowflake], lo que significa que no se exportarán ni transferirán físicamente datos a su propia instancia de Snowflake. En su lugar, Adobe le concede acceso de solo lectura a una tabla activa alojada en el entorno de Snowflake de Adobe. Puede consultar esta tabla compartida directamente desde su cuenta de Snowflake, pero no es el propietario de la tabla y no puede modificarla ni conservarla más allá del período de retención especificado. Adobe administra completamente el ciclo de vida y la estructura de la tabla compartida.

La primera vez que comparta datos de la instancia de Snowflake de Adobe con la suya, se le pedirá que acepte el anuncio privado de Adobe.

![Captura de pantalla que muestra la pantalla de aceptación de anuncios privados de Snowflake](../../assets/catalog/cloud-storage/snowflake/snowflake-accept-listing.png)

### Retención de datos y tiempo de vida (TTL) {#ttl}

Todos los datos compartidos a través de esta integración tienen un tiempo de vida (TTL) fijo de siete días. Siete días después de la última exportación, la tabla compartida caduca automáticamente y se vuelve inaccesible, independientemente de si el flujo de datos sigue activo. Si necesita conservar los datos durante más de siete días, debe copiar el contenido en una tabla suya en su propia instancia de Snowflake antes de que caduque el TTL.

### Comportamiento de actualización de audiencia {#audience-update-behavior}

Si la audiencia se evalúa en [modo por lotes](../../../segmentation/methods/batch-segmentation.md), los datos de la tabla compartida se actualizarán cada 24 horas. Esto significa que puede haber un retraso de hasta 24 horas entre los cambios en la pertenencia a la audiencia y cuando esos cambios se reflejan en la tabla compartida.

### Lógica de exportación incremental {#incremental-export}

Cuando un flujo de datos se ejecuta para una audiencia por primera vez, realiza un relleno y comparte todos los perfiles cualificados actualmente. Después de este relleno inicial, solo las actualizaciones incrementales se reflejan en la tabla compartida. Esto significa perfiles que se añaden o eliminan de la audiencia. Este método garantiza actualizaciones eficientes y mantiene la tabla compartida actualizada.

## Requisitos previos {#prerequisites}

Antes de configurar la conexión de Snowflake, asegúrese de cumplir los siguientes requisitos previos:

* Tiene acceso a una cuenta de [!DNL Snowflake].
* Tu cuenta de Snowflake está suscrita a anuncios privados. Usted o alguien de su compañía que tenga privilegios de administrador de cuentas en Snowflake puede configurarlo.

## Audiencias compatibles {#supported-audiences}

Esta sección describe qué tipos de audiencias puede exportar a este destino. Las dos tablas siguientes indican qué audiencias admite este conector, según los _tipos de origen de audiencia_ y _perfil incluidos en la audiencia_:

| Origen de audiencia | Admitido | Descripción |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Audiencias generadas a través del [servicio de segmentación](../../../segmentation/home.md) de Experience Platform. |
| Todos los demás orígenes de audiencia | ✓ | Esta categoría incluye todos los orígenes de audiencia fuera de las audiencias generadas a través de [!DNL Segmentation Service]. Obtenga información acerca de [varios orígenes de audiencia](/help/segmentation/ui/audience-portal.md#customize). Algunos ejemplos son: <ul><li> audiencias de carga personalizadas [importadas](../../../segmentation/ui/audience-portal.md#import-audience) a Experience Platform desde archivos CSV,</li><li> audiencias de similitud, </li><li> audiencias federadas, </li><li> audiencias generadas en otras aplicaciones de Experience Platform, como Adobe Journey Optimizer, </li><li> y más. </li></ul> |

{style="table-layout:auto"}

## Tipo y frecuencia de exportación {#export-type-frequency}

Consulte la tabla siguiente para obtener información sobre el tipo y la frecuencia de exportación de destino.

| Elemento | Tipo | Notas |
---------|----------|---------|
| Tipo de exportación | **[!UICONTROL Exportación de audiencia]** | Está exportando todos los miembros de una audiencia con los identificadores (nombre, número de teléfono u otros) utilizados en el destino [!DNL Snowflake]. |
| Frecuencia de exportación | **[!UICONTROL Transmisión]** | Los destinos de streaming son conexiones basadas en API &quot;siempre activadas&quot;. Tan pronto como se actualiza un perfil en Experience Platform basado en la evaluación de audiencias, el conector envía la actualización de forma descendente a la plataforma de destino. Más información sobre [destinos de streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Conexión al destino {#connect}

>[!IMPORTANT]
> 
>Para conectarse al destino, necesita los **[!UICONTROL permisos de control de acceso]** de Ver destinos **[!UICONTROL y]** Administrar destinos[](/help/access-control/home.md#permissions)5}. Lea la [descripción general del control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Para conectarse a este destino, siga los pasos descritos en el [tutorial de configuración de destino](../../ui/connect-destination.md). En el flujo de trabajo de configuración de destino, rellene los campos enumerados en las dos secciones siguientes.

### Autenticarse en el destino {#authenticate}

Para autenticarse en el destino, seleccione **[!UICONTROL Conectarse al destino]**.

![Captura de pantalla de muestra que muestra cómo autenticarse en el destino](../../assets/catalog/cloud-storage/snowflake/authenticate-destination.png)

### Rellenar detalles de destino {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_snowflake_accountID"
>title="Escriba su ID de cuenta técnica de Snofwflake "
>abstract="Si su cuenta está vinculada a una organización, use este formato: `OrganizationName.AccountName`<br><br> Si su cuenta no está vinculada a una organización, use este formato:`AccountName`"

Para configurar los detalles del destino, rellene los campos obligatorios y opcionales a continuación. Un asterisco junto a un campo en la interfaz de usuario indica que el campo es obligatorio.

![Captura de pantalla de muestra que muestra cómo rellenar los detalles de tu destino](../../assets/catalog/cloud-storage/snowflake/configure-destination-details.png)

* **[!UICONTROL Nombre]**: Un nombre por el cual reconocerá este destino en el futuro.
* **[!UICONTROL Descripción]**: Una descripción que le ayudará a identificar este destino en el futuro.
* **[!UICONTROL ID de cuenta de Snowflake]**: tu ID de cuenta de Snowflake. Utilice el siguiente formato de ID de cuenta en función de si su cuenta está vinculada a una organización:
   * Si su cuenta está vinculada a una organización:`OrganizationName.AccountName`.
   * Si su cuenta no está vinculada a una organización:`AccountName`.
* **[!UICONTROL Reconocimiento de cuenta]**: alterne el reconocimiento de ID de cuenta de Snowflake para confirmar que el ID de cuenta es correcto y que le pertenece.

>[!IMPORTANT]
>
> Los caracteres especiales utilizados en el nombre de destino y en el nombre de la zona protegida de Experience Platform se convierten automáticamente en guiones bajos (`_`) en Snowflake. Para evitar confusiones, no utilice caracteres especiales en el nombre del destino y de la zona protegida.

### Habilitar alertas {#enable-alerts}

Puede activar alertas para recibir notificaciones sobre el estado del flujo de datos a su destino. Seleccione una alerta de la lista a la que suscribirse para recibir notificaciones sobre el estado del flujo de datos. Para obtener más información sobre las alertas, lea la guía sobre [suscripción a alertas de destinos mediante la interfaz de usuario](../../ui/alerts.md).

Cuando termine de proporcionar detalles para la conexión de destino, seleccione **[!UICONTROL Siguiente]**.

## Activar públicos en este destino {#activate}

>[!IMPORTANT]
> 
>* Para activar los datos, necesita los **[!UICONTROL permisos de control de acceso]**, **[!UICONTROL Activar destinos]**, **[!UICONTROL Ver perfiles]** y **[!UICONTROL Ver segmentos]**[para ](/help/access-control/home.md#permissions). Lea la [descripción general del control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.
>* Para exportar *identidades*, necesita el **[!UICONTROL permiso de control de acceso]** de [Ver gráfico de identidad](/help/access-control/home.md#permissions). <br> ![Seleccione el área de nombres de identidad resaltada en el flujo de trabajo para activar audiencias en los destinos.](/help/destinations/assets/overview/export-identities-to-destination.png "Seleccione el área de nombres de identidad resaltada en el flujo de trabajo para activar audiencias en los destinos."){width="100" zoomable="yes"}

Lea [Activar perfiles y audiencias en destinos de exportación de audiencias de streaming](/help/destinations/ui/activate-segment-streaming-destinations.md) para obtener instrucciones sobre cómo activar audiencias en este destino.

### Asignar atributos {#map}

El destino de Snowflake admite la asignación de atributos de perfil a atributos personalizados.

![Imagen de la interfaz de usuario de Experience Platform que muestra la pantalla de asignación del destino de Snowflake.](../../assets/catalog/cloud-storage/snowflake/mapping.png)

Los atributos de destino se crean automáticamente en Snowflake utilizando el nombre de atributo proporcionado en el campo **[!UICONTROL Nombre de atributo]**.

## Datos exportados / Validar exportación de datos {#exported-data}

Compruebe su cuenta de Snowflake para comprobar que los datos se exportaron correctamente.

## Uso de datos y gobernanza {#data-usage-governance}

Todos los destinos de [!DNL Adobe Experience Platform] cumplen con las políticas de uso de datos al administrar los datos. Para obtener información detallada sobre cómo [!DNL Adobe Experience Platform] aplica el control de datos, lea la [Información general sobre el control de datos](/help/data-governance/home.md).
