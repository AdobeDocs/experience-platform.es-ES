---
title: Adform
description: Adform es un proveedor líder de soluciones programáticas de compra y venta de medios. Al conectar Adform a Adobe Experience Platform, puede activar las audiencias de origen mediante Adform en función del Experience Cloud ID (ECID).
last-substantial-update: 2025-10-22T00:00:00Z
source-git-commit: f7fd7a83f6d047877697b72e78ac0d4b08c0ff00
workflow-type: tm+mt
source-wordcount: '972'
ht-degree: 3%

---


# Adform connection {#adform}

## Información general {#overview}

Adform es un proveedor líder de soluciones programáticas de compra y venta de medios. Al conectar Adform a Adobe Experience Platform, puede activar las audiencias de origen a través de Adform en función del Experience Cloud ID (ECID).

>[!IMPORTANT]
>
>El conector de destino y la página de documentación los crea y mantiene el equipo de Adobe Forms. Para cualquier consulta o solicitud de actualización, comuníquese directamente con ellos al `support@adform.com`.

## Casos de uso {#use-cases}

Para ayudarle a comprender mejor cómo y cuándo debe utilizar el destino de Adobe, aquí hay ejemplos de casos de uso que los clientes de Adobe Experience Platform pueden solucionar mediante este destino.

### Activación de audiencia de Adobe Real-Time CDP {#use-case-1}

Utilice este destino para enviar audiencias de Adobe Real-Time CDP a Adobe para su activación en función del Experience Cloud ID (ECID) y del ID de Fusion de Adobe. ID Fusion de Adobe es el servicio de resolución de ID de Adobe que le permite activar audiencias de origen basadas en el Experience Cloud ID (ECID).

Un caso común es el redireccionamiento de los visitantes del sitio web a su sitio web o aplicación en función del Experience Cloud ID (ECID). Todo lo que debe hacer es enviar el Experience Cloud ID (ECID) a Adobe a través de las extensiones de [flujo de eventos](https://exchange.adobe.com/apps/ec/600102/adform-s2s-site-tracking) o [del lado del cliente](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/catalog/analytics/adform) de Adobe disponibles. Después, puede compartir audiencias con Adobe Forms a través del destino de Adobe para la activación, únicamente en función del Experience Cloud ID (ECID).

## Requisitos previos {#prerequisites}

* Debe ser cliente de Adform existente para utilizar este destino.
* Debe tener sus credenciales de conexión de datos de Adform Audience Base.
   * Si no tiene credenciales de conexión de datos de Adform Audience Base, póngase en contacto con su representante de Adform.
* Para realizar la sincronización correctamente, necesita tener una conexión de [Flujo de eventos](https://exchange.adobe.com/apps/ec/600102/adform-s2s-site-tracking) o [del lado del cliente](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/catalog/analytics/adform) desde sus entidades al Seguimiento de sitios de Adobe.
   * Si no tiene una conexión de flujo de eventos o del lado del cliente desde sus entidades a Seguimiento de sitios de Adobe, póngase en contacto con su representante de Adform.
   * Adform proporciona extensiones Adobe Experience Cloud para [flujo de eventos](https://exchange.adobe.com/apps/ec/600102/adform-s2s-site-tracking) y [del lado del cliente](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/catalog/analytics/adform).


## Identidades admitidas {#supported-identities}

Adform admite la activación de las identidades descritas en la siguiente tabla. Más información sobre [identidades](/help/identity-service/features/namespaces.md).

| Identidad de destino | Descripción | Consideraciones |
|---|---|---|
| ECID | Experience Cloud ID | Un área de nombres que representa ECID. Este área de nombres también se puede mencionar mediante los siguientes alias: &quot;Adobe Marketing Cloud ID&quot;, &quot;Adobe Experience Cloud ID&quot;, &quot;Adobe Experience Platform ID&quot;. Consulte el siguiente documento sobre [ECID](/help/identity-service/features/ecid.md) para obtener más información. |

{style="table-layout:auto"}

## Audiencias compatibles {#supported-audiences}

Esta sección describe qué tipo de audiencias puede exportar a este destino.

| Origen de audiencia | Admitido | Descripción |
---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Audiencias generadas a través del [servicio de segmentación](../../../segmentation/home.md) de Experience Platform. |
| Cargas personalizadas | ✓ | Las audiencias [importadas](../../../segmentation/ui/overview.md#import-audience) en Experience Platform desde archivos CSV. |

{style="table-layout:auto"}

## Tipo y frecuencia de exportación {#export-type-frequency}

Consulte la tabla siguiente para obtener información sobre el tipo y la frecuencia de exportación de destino.

| Elemento | Tipo | Notas |
---------|----------|---------|
| Tipo de exportación | **[!UICONTROL Segment export]** | Va a exportar todos los miembros de un segmento (audiencia) con los identificadores (nombre, número de teléfono u otros) utilizados en el destino *YourDestination*. |
| Frecuencia de exportación | **[!UICONTROL Batch]** | Los destinos por lotes exportan archivos a plataformas descendentes en incrementos de tres, seis, ocho, doce o veinticuatro horas. Obtenga más información sobre [destinos basados en archivos por lotes](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## Conectar con el destino {#connect}

>[!IMPORTANT]
> 
>Para conectarse al destino, necesita el permiso de control de acceso **[!UICONTROL View Destinations]** y **[!UICONTROL Manage Destinations]** [3}. ](/help/access-control/home.md#permissions) Lea la [descripción general del control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Para conectarse a este destino, siga los pasos descritos en el [tutorial de configuración de destino](../../ui/connect-destination.md). En el flujo de trabajo de configuración de destino, rellene los campos enumerados en las dos secciones siguientes.

### Autenticarse en el destino {#authenticate}

Para autenticarse en el destino, rellene los campos obligatorios y seleccione **[!UICONTROL Connect to destination]**.

![Autenticar con el destino](../../assets/catalog/advertising/adform/authenticate-destination.png)

* **[!UICONTROL Account name]**: escriba un nombre de cuenta mediante el cual pueda identificar esta conexión de destino en el futuro.
* **[!UICONTROL S3 Access Key ID]**: complete la clave de acceso S3 proporcionada por Adform.
* **[!UICONTROL S3 Secret Access Key]**: complete la clave de acceso secreto S3 proporcionada por Adform.

### Rellenar detalles de destino {#destination-details}

Para configurar los detalles del destino, rellene los campos obligatorios y opcionales a continuación. Un asterisco junto a un campo en la interfaz de usuario indica que el campo es obligatorio.

![Rellene los detalles de destino](../../assets/catalog/advertising/adform/configure-destination-details.png)

* **[!UICONTROL Name]**: un nombre con el cual reconocerá este destino en el futuro.
* **[!UICONTROL Description]**: una descripción que le ayudará a identificar este destino en el futuro.
* **[!UICONTROL Provider Name]**: el nombre de su cuenta de Adform proporcionado por Adform.

### Habilitar alertas {#enable-alerts}

Puede activar alertas para recibir notificaciones sobre el estado del flujo de datos a su destino. Seleccione una alerta de la lista a la que suscribirse para recibir notificaciones sobre el estado del flujo de datos. Para obtener más información sobre las alertas, consulte la guía sobre [suscripción a alertas de destinos mediante la interfaz de usuario](../../ui/alerts.md).

Cuando termine de proporcionar detalles para la conexión de destino, seleccione **[!UICONTROL Next]**.

## Activar públicos en este destino {#activate}

>[!IMPORTANT]
> 
>* Para activar los datos, necesita los permisos de control de acceso **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** y **[!UICONTROL View Segments]** [5}. ](/help/access-control/home.md#permissions) Lea la [descripción general del control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.
>* Para exportar *identidades*, necesita el **[!UICONTROL View Identity Graph]** [permiso de control de acceso](/help/access-control/home.md#permissions). <br> ![Seleccione el área de nombres de identidad resaltada en el flujo de trabajo para activar audiencias en los destinos.](/help/destinations/assets/overview/export-identities-to-destination.png "Seleccione el área de nombres de identidad resaltada en el flujo de trabajo para activar audiencias en los destinos."){width="100" zoomable="yes"}

Lea [Activar datos de audiencia en destinos de exportación de perfiles por lotes](/help/destinations/ui/activate-batch-profile-destinations.md) para obtener instrucciones sobre cómo activar segmentos de audiencia en este destino.

### Asignar atributos e identidades {#map}

* **ECID** (Experience Cloud ID)

Durante el paso de asignación, utilice solamente la asignación de identidad de destino [!DNL ECID]. No incluya ningún otro campo de identidad, ya que esto impedirá que la activación se complete correctamente.

## Datos exportados / Validar exportación de datos {#exported-data}

El conector de destino solo exporta la identidad de ECID al destino. No se exporta ninguna otra identidad. Para comprobar si la exportación de datos se ha realizado correctamente, inicie sesión en su cuenta de Adform Audience Base y compruebe si las audiencias están disponibles.

## Uso de datos y gobernanza {#data-usage-governance}

Todos los destinos de [!DNL Adobe Experience Platform] cumplen con las políticas de uso de datos al administrar los datos. Para obtener información detallada sobre cómo [!DNL Adobe Experience Platform] aplica el control de datos, lea la [Información general sobre el control de datos](/help/data-governance/home.md).

## Recursos adicionales {#additional-resources}

Para obtener información adicional acerca de Adform Audience Base, consulte la [Documentación de Adform Audience Base](https://www.adformhelp.com/hc/en-us/categories/9738365991697-Data-Management-Platform).