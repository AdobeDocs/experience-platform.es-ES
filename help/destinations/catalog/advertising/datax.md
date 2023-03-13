---
title: Conexión de Verizon MediaYahoo DataX
description: DataX es una infraestructura agregada de Verizon Media/Yahoo que aloja varios componentes que permiten a Verizon Media/Yahoo intercambiar datos con sus socios externos de una manera segura, automatizada y escalable.
exl-id: 7d02671d-8650-407d-9c9f-fad7da3156bc
source-git-commit: 0580816c471400ba17eddcb6b1a9dfbf01797938
workflow-type: tm+mt
source-wordcount: '778'
ht-degree: 2%

---

# [!DNL Verizon Media/Yahoo DataX] conexión

## Información general {#overview}

[!DNL DataX] es un agregado [!DNL Verizon Media/Yahoo] infraestructura que aloja varios componentes que habilitan [!DNL Verizon Media/Yahoo] intercambiar datos con sus socios externos de forma segura, automatizada y escalable.

>[!IMPORTANT]
>
>Esta página de documentación la creó [!DNL Verizon Media/Yahoo]de [!DNL DataX] equipo. Para cualquier consulta o solicitud de actualización, póngase en contacto directamente con ellos en [dataops@verizonmedia.com](mailto:dataops@verizonmedia.com)

## Requisitos previos {#prerequisites}

**ID de MDM**

Este es un identificador único en [!DNL Yahoo DataX] y es un campo obligatorio para configurar exportaciones de datos a este destino. Si no conoce este ID, póngase en contacto con su [!DNL Yahoo DataX] administrador de cuentas.

**Metadatos de taxonomía**

El recurso de taxonomía define una extensión sobre la base [!DNL DataX] Estructura de metadatos

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

Más información sobre [Metadatos de taxonomía](https://developer.verizonmedia.com/datax/guide/taxonomy/taxo-metadata/) en el [!DNL DataX] documentación para desarrolladores.

## Límites y protecciones de velocidad {#rate-limits-guardrails}

>[!IMPORTANT]
>
>Al activar más de 100 segmentos en [!DNL Verizon Media/Yahoo DataX], es posible que reciba errores de limitación de velocidad del destino. Al activar segmentos en este destino, intente activar menos de 100 segmentos en un flujo de datos de activación. Si necesita activar más segmentos, cree un nuevo destino en la misma cuenta.

[!DNL DataX] está limitado por las tasas según los límites de cuotas para publicaciones de taxonomía y audiencias descritos en la sección [Documentación de DataX](https://developer.verizonmedia.com/datax/guide/rate-limits/).


| Código de error | Mensaje de error | Descripción |
|---------|----------|---------|
| Demasiadas solicitudes | Límite de velocidad superado por hora **(Límite: 100)** | Número de solicitudes permitidas en una hora por proveedor. |

{style="table-layout:auto"}

## Identidades admitidas {#supported-identities}

[!DNL Verizon Media] admite la activación de identidades descritas en la tabla siguiente. Más información sobre [identidades](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=en#getting-started).

| Identidad de destino | Descripción | Consideraciones |
|---|---|---|
| email_lc_sha256 | Direcciones de correo electrónico con el algoritmo SHA256 | Adobe Experience Platform admite direcciones de correo electrónico con hash SHA256 y de texto sin formato. Si el campo de origen contiene atributos sin hash, marque la **[!UICONTROL Aplicar transformación]** opción, para tener [!DNL Platform] hash automático de los datos en la activación. |
| GAID | ID de publicidad de Google | Seleccione la identidad de destino GAID cuando su identidad de origen sea un área de nombres GAID. |
| IDFA | Apple ID para anunciantes | Seleccione la identidad de destino IDFA cuando la identidad de origen sea un área de nombres IDFA. |

{style="table-layout:auto"}

## Tipo y frecuencia de exportación {#export-type-frequency}

Consulte la tabla siguiente para obtener información sobre el tipo y la frecuencia de exportación de destino.

| Elemento | Tipo | Notas |
---------|----------|---------|
| Tipo de exportación | **[!UICONTROL Exportación de segmentos]** | Está exportando todos los miembros de un segmento (audiencia) con los identificadores (correo electrónico, GAID, IDFA) usados en el destino de Verizon Media. |
| Frecuencia de exportación | **[!UICONTROL Transmisión]** | Los destinos de streaming son conexiones basadas en API &quot;siempre activadas&quot;. Tan pronto como se actualiza un perfil en Experience Platform según la evaluación de segmentos, el conector envía la actualización de forma descendente a la plataforma de destino. Más información sobre [destinos de streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Casos de uso {#use-cases}

[!DNL DataX] Las API están disponibles para los anunciantes que deseen dirigirse a un grupo de audiencia específico con claves de direcciones de correo electrónico en [!DNL Verizon Media] (VMG) puede crear rápidamente un nuevo segmento e insertar el grupo de audiencia deseado mediante la API de VMG en tiempo casi real.

## Conectar con destino {#connect}

>[!IMPORTANT]
> 
>Para conectarse al destino, necesita el **[!UICONTROL Administrar destinos]** [permiso de control de acceso](/help/access-control/home.md#permissions). Lea el [información general de control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

![Tarjeta de destino de Yahoo DataX en la IU de Platform](/help/destinations/assets/catalog/advertising/yahoo-datax/catalog.png)

Para conectarse a este destino, siga los pasos descritos en la sección [tutorial de configuración de destino](../../ui/connect-destination.md).

### Parámetros de conexión {#parameters}

While [configuración](../../ui/connect-destination.md) Para este destino, debe proporcionar la siguiente información:

* **[!UICONTROL Nombre]**: Un nombre con el que reconocerá este destino en el futuro.
* **[!UICONTROL Descripción]**: Una descripción que le ayudará a identificar este destino en el futuro.
* **[!UICONTROL ID de MDM]**: Es un identificador único en [!DNL Yahoo DataX] y es un campo obligatorio para configurar exportaciones de datos a este destino. Si no conoce este ID, póngase en contacto con su [!DNL Yahoo DataX] administrador de cuentas.  Con los ID de MDM, los datos se pueden restringir para su uso únicamente con un determinado conjunto de usuarios exclusivos (como datos de origen de anunciantes).

### Habilitar alertas {#enable-alerts}

Puede activar alertas para recibir notificaciones sobre el estado del flujo de datos a su destino. Seleccione una alerta de la lista a la que suscribirse para recibir notificaciones sobre el estado del flujo de datos. Para obtener más información sobre las alertas, consulte la guía de [suscripción a alertas de destinos mediante la IU](../../ui/alerts.md).

Cuando haya terminado de proporcionar detalles para la conexión de destino, seleccione **[!UICONTROL Siguiente]**.

## Activar segmentos en este destino {#activate}

>[!IMPORTANT]
> 
>Para activar los datos, necesita el **[!UICONTROL Administrar destinos]**, **[!UICONTROL Activar destinos]**, **[!UICONTROL Ver perfiles]**, y **[!UICONTROL Ver segmentos]** [permisos de control de acceso](/help/access-control/home.md#permissions). Lea el [información general de control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Leer [Activación de perfiles y segmentos en un destino](../../ui/activate-segment-streaming-destinations.md) para obtener instrucciones sobre cómo activar segmentos de audiencia en destinos.

## Uso de datos y gobernanza {#data-usage-governance}

Todo [!DNL Adobe Experience Platform] Los destinos de cumplen con las políticas de uso de datos al gestionar los datos. Para obtener información detallada sobre cómo [!DNL Adobe Experience Platform] aplica la gobernanza de datos. Consulte la [Resumen de gobernanza de datos](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html?lang=es).

## Recursos adicionales {#additional-resources}

Para obtener más información, lea la [!DNL Yahoo/Verizon Media] [documentación sobre [!DNL DataX]](https://developer.verizonmedia.com/datax/guide/).
