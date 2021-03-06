---
title: Conexión de datos de Verizon MediaYahoo
description: DataX es una infraestructura agregada de Verizon Media/Yahoo que aloja varios componentes que permiten a Verizon Media/Yahoo intercambiar datos con sus socios externos de forma segura, automatizada y escalable.
exl-id: 7d02671d-8650-407d-9c9f-fad7da3156bc
source-git-commit: dd18350387aa6bdeb61612f0ccf9d8d2223a8a5d
workflow-type: tm+mt
source-wordcount: '775'
ht-degree: 4%

---

# Conexión de datos de Verizon Media/Yahoo DataX

## Información general {#overview}

DataX es una infraestructura agregada de Verizon Media/Yahoo que aloja varios componentes que permiten a Verizon Media/Yahoo intercambiar datos con sus socios externos de forma segura, automatizada y escalable.

>[!IMPORTANT]
>
>Esta página de documentación la creó el equipo DataX de Verizon Media/Yahoo. Para cualquier consulta o solicitud de actualización, póngase en contacto con ellos directamente en [dataops@verizonmedia.com](mailto:dataops@verizonmedia.com)

## Requisitos previos {#prerequisites}

**ID de MDM**

Se trata de un identificador único en Yahoo DataX y es un campo obligatorio para configurar exportaciones de datos a este destino. Si no conoce este ID, póngase en contacto con su administrador de cuentas de Yahoo Data X.

**Límite de tasa**

DataX tiene una tasa limitada según los límites de cuota para las publicaciones de taxonomía y audiencia que se describen en la [Documentación de DataX](https://developer.verizonmedia.com/datax/guide/rate-limits/).


| Código de error | Mensaje de error | Descripción |
|---------|----------|---------|
| 429 Demasiadas solicitudes | Límite de tasa excedido por hora **(Límite: 100)** | Número de solicitudes permitidas en una hora por proveedor. |

{style=&quot;table-layout:auto&quot;}

**Metadatos de taxonomía**

El recurso taxonomía define una extensión sobre la estructura de metadatos DataX base

```
{

  >>(Base DataX Metadata)<<

        "extensions": { "action":
        {string}, "incrementalData":
        {
                "taxonomyId": {string}
                },
                "links": [{
                "rel": "https://datax.yahooapis.com/rels/fullTaxonomy", "title": "Full
                Taxonomy post processing",
                "href": {string}
                ]
        }
}
```

Más información sobre [Metadatos de taxonomía](https://developer.verizonmedia.com/datax/guide/taxonomy/taxo-metadata/) en la documentación para desarrolladores de DataX.

## Identidades compatibles {#supported-identities}

Verizon Media admite la activación de identidades descritas en la tabla siguiente. Más información sobre [identidades](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=en#getting-started).

| Identidad de Target | Descripción | Consideraciones |
|---|---|---|
| email_lc_sha256 | Direcciones de correo electrónico con hash con el algoritmo SHA256 | Adobe Experience Platform admite las direcciones de correo electrónico con texto sin formato y con hash SHA 256. Si el campo de origen contiene atributos sin hash, marque la casilla de verificación **[!UICONTROL Aplicar transformación]** para [!DNL Platform] hash automático de los datos al activarlos. |
| GAID | Google Advertising ID | Seleccione la identidad objetivo GAID cuando su identidad de origen sea un área de nombres GAID. |
| IDFA | Apple ID para anunciantes | Seleccione la identidad de destino IDFA cuando la identidad de origen sea un área de nombres IDFA. |

{style=&quot;table-layout:auto&quot;}

## Tipo de exportación y frecuencia {#export-type-frequency}

Consulte la tabla siguiente para obtener información sobre el tipo y la frecuencia de exportación de destino.

| Elemento | Tipo | Notas |
---------|----------|---------|
| Tipo de exportación | **[!UICONTROL Exportación de segmentos]** | Está exportando todos los miembros de un segmento (audiencia) con los identificadores (correo electrónico, GAID, IDFA) utilizados en el destino de Verizon Media. |
| Frecuencia de exportación | **[!UICONTROL Transmisión]** | Los destinos de flujo continuo son conexiones basadas en API &quot;siempre activadas&quot;. Tan pronto como un perfil se actualiza en el Experience Platform en función de la evaluación de segmentos, el conector envía la actualización descendente a la plataforma de destino. Más información sobre [destinos de flujo continuo](/help/destinations/destination-types.md#streaming-destinations). |

{style=&quot;table-layout:auto&quot;}

## Casos de uso {#use-cases}

Las API de DataX están disponibles para los anunciantes que deseen dirigirse a un grupo de audiencia específico con direcciones de correo electrónico marcadas por Verizon Media (VMG) pueden crear rápidamente un nuevo segmento y insertar el grupo de audiencia deseado con la API casi en tiempo real de VMG.

## Conectarse al destino {#connect}

>[!IMPORTANT]
> 
>Para conectarse al destino, necesita la variable **[!UICONTROL Administrar destinos]** [permiso de control de acceso](/help/access-control/home.md#permissions). Lea el [información general sobre el control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

![Tarjeta de destino de Yahoo DataX en la interfaz de usuario de Platform](/help/destinations/assets/catalog/advertising/yahoo-datax/catalog.png)

Para conectarse a este destino, siga los pasos descritos en la sección [tutorial de configuración de destino](../../ui/connect-destination.md).

### Parámetros de conexión {#parameters}

While [configuración](../../ui/connect-destination.md) Para este destino, debe proporcionar la siguiente información:

* **[!UICONTROL Nombre]**: Un nombre por el cual reconocerá este destino en el futuro.
* **[!UICONTROL Descripción]**: Descripción que le ayudará a identificar este destino en el futuro.
* **[!UICONTROL ID de MDM]**: Se trata de un identificador único en Yahoo DataX y es un campo obligatorio para configurar exportaciones de datos a este destino. Si no conoce este ID, póngase en contacto con su administrador de cuentas de Yahoo Data X.  Con los ID de MDM, los datos pueden restringirse para su uso únicamente con un determinado conjunto de usuarios exclusivos (como los datos de origen de los anunciantes).

### Habilitar alertas {#enable-alerts}

Puede activar las alertas para recibir notificaciones sobre el estado del flujo de datos a su destino. Seleccione una alerta de la lista para suscribirse y recibir notificaciones sobre el estado de su flujo de datos. Para obtener más información sobre las alertas, consulte la guía de [suscripción a alertas de destinos mediante la interfaz de usuario](../../ui/alerts.md).

Cuando haya terminado de proporcionar detalles para la conexión de destino, seleccione **[!UICONTROL Siguiente]**.

## Activar segmentos en este destino {#activate}

>[!IMPORTANT]
> 
>Para activar los datos, necesita la variable **[!UICONTROL Administrar destinos]**, **[!UICONTROL Activar destinos]**, **[!UICONTROL Ver perfiles]** y **[!UICONTROL Ver segmentos]** [permisos de control de acceso](/help/access-control/home.md#permissions). Lea el [información general sobre el control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Lectura [Activar perfiles y segmentos en un destino](../../ui/activate-segment-streaming-destinations.md) para obtener instrucciones sobre la activación de segmentos de audiencia en destinos.

## Uso y gobernanza de los datos {#data-usage-governance}

Todo [!DNL Adobe Experience Platform] Los destinos de cumplen las políticas de uso de datos al administrar los datos. Para obtener información detallada sobre cómo [!DNL Adobe Experience Platform] exige el control de datos; consulte [Información general sobre la administración de datos](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html?lang=es).

## Recursos adicionales {#additional-resources}

Para obtener más información, consulte Yahoo/Verizon Media [documentación sobre DataX](https://developer.verizonmedia.com/datax/guide/).
