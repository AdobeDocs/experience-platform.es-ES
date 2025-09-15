---
title: Conexión de Verizon MediaYahoo DataX
description: DataX es una infraestructura agregada de Verizon Media/Yahoo que aloja varios componentes que permiten a Verizon Media/Yahoo intercambiar datos con sus socios externos de una manera segura, automatizada y escalable.
exl-id: 7d02671d-8650-407d-9c9f-fad7da3156bc
source-git-commit: 65809628e8535027edb08e54e84b308777036ab2
workflow-type: tm+mt
source-wordcount: '798'
ht-degree: 3%

---

# [!DNL Verizon Media/Yahoo DataX] conexión

## Información general {#overview}

[!DNL DataX] es una infraestructura [!DNL Verizon Media/Yahoo] agregada que aloja varios componentes que permiten a [!DNL Verizon Media/Yahoo] intercambiar datos con sus socios externos de una manera segura, automatizada y escalable.

>[!IMPORTANT]
>
>El equipo [!DNL Verizon Media/Yahoo] de [!DNL DataX] crea y mantiene este conector de destino y esta página de documentación. Para cualquier consulta o solicitud de actualización, comuníquese directamente con ellos en [dataoperations@yahooinc.com](mailto:dataoperations@yahooinc.com)

## Requisitos previos {#prerequisites}

**ID DE MDM**

Este es un identificador único en [!DNL Yahoo DataX] y es un campo obligatorio para configurar exportaciones de datos a este destino. Si no conoce este identificador, comuníquese con el administrador de cuentas de [!DNL Yahoo DataX].

**Metadatos de taxonomía**

El recurso Taxonomy define una extensión sobre la estructura de metadatos Base [!DNL DataX]

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

Obtenga más información acerca de [metadatos de taxonomía](https://developer.verizonmedia.com/datax/guide/taxonomy/taxo-metadata/) en la documentación para desarrolladores de [!DNL DataX].

## Límites y protecciones de velocidad {#rate-limits-guardrails}

>[!IMPORTANT]
>
>Al activar más de 100 audiencias en [!DNL Verizon Media/Yahoo DataX], es posible que reciba errores de limitación de velocidad del destino. Al activar audiencias en este destino, intente activar menos de 100 audiencias en un flujo de datos de activación. Si necesita activar más segmentos, cree un nuevo destino en la misma cuenta.

[!DNL DataX] tiene una tasa limitada según los límites de cuota para las publicaciones de taxonomía y audiencia descritos en la [documentación de DataX](https://developer.verizonmedia.com/datax/guide/rate-limits/).


| Código de error | Mensaje de error | Descripción |
|---------|----------|---------|
| Demasiadas solicitudes | Límite de velocidad excedido por hora **(Límite: 100)** | Número de solicitudes permitidas en una hora por proveedor. |

{style="table-layout:auto"}

## Identidades admitidas {#supported-identities}

[!DNL Verizon Media] admite la activación de las identidades descritas en la tabla siguiente. Más información sobre [identidades](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html#getting-started).

| Identidad de destino | Descripción | Consideraciones |
|---|---|---|
| email_lc_sha256 | Direcciones de correo electrónico con el algoritmo SHA256 | Adobe Experience Platform admite direcciones de correo electrónico con hash SHA256 y de texto sin formato. Si el campo de origen contiene atributos sin hash, marque la opción **[!UICONTROL Aplicar transformación]** para que [!DNL Experience Platform] aplique automáticamente el hash a los datos durante la activación. |
| GAID | GOOGLE ADVERTISING ID | Seleccione la identidad de destino GAID cuando su identidad de origen sea un área de nombres GAID. |
| IDFA | Apple ID para anunciantes | Seleccione la identidad de destino IDFA cuando la identidad de origen sea un área de nombres IDFA. |

{style="table-layout:auto"}

## Tipo y frecuencia de exportación {#export-type-frequency}

Consulte la tabla siguiente para obtener información sobre el tipo y la frecuencia de exportación de destino.

| Elemento | Tipo | Notas |
---------|----------|---------|
| Tipo de exportación | **[!UICONTROL Exportación de audiencia]** | Estás exportando a todos los miembros de una audiencia con los identificadores (correo electrónico, GAID, IDFA) usados en el destino de Verizon Media. |
| Frecuencia de exportación | **[!UICONTROL Transmisión]** | Los destinos de streaming son conexiones basadas en API &quot;siempre activadas&quot;. Tan pronto como se actualiza un perfil en Experience Platform basado en la evaluación de audiencias, el conector envía la actualización de forma descendente a la plataforma de destino. Más información sobre [destinos de streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Casos de uso {#use-cases}

Las API de [!DNL DataX] están disponibles para anunciantes que deseen dirigirse a un grupo de audiencia específico con claves de direcciones de correo electrónico en [!DNL Verizon Media] (VMG) pueden crear rápidamente una nueva audiencia e insertar el grupo de audiencia deseado mediante la API de VMG en tiempo casi real.

## Conectar con destino {#connect}

>[!IMPORTANT]
> 
>Para conectarse al destino, necesita los **[!UICONTROL permisos de control de acceso]** de Ver destinos **[!UICONTROL y]** Administrar destinos[](/help/access-control/home.md#permissions)5}. Lea la [descripción general del control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

![Tarjeta de destino Yahoo DataX en la interfaz de usuario de Experience Platform](/help/destinations/assets/catalog/advertising/yahoo-datax/catalog.png)

Para conectarse a este destino, siga los pasos descritos en el [tutorial de configuración de destino](../../ui/connect-destination.md).

### Parámetros de conexión {#parameters}

Mientras [configura](../../ui/connect-destination.md) este destino, debe proporcionar la siguiente información:

* **[!UICONTROL Nombre]**: Un nombre por el cual reconocerá este destino en el futuro.
* **[!UICONTROL Descripción]**: Una descripción que le ayudará a identificar este destino en el futuro.
* **[!UICONTROL ID de MDM]**: Este es un identificador único en [!DNL Yahoo DataX] y es un campo obligatorio para configurar exportaciones de datos a este destino. Si no conoce este identificador, comuníquese con el administrador de cuentas de [!DNL Yahoo DataX].  Con los ID de MDM, los datos se pueden restringir para su uso únicamente con un determinado conjunto de usuarios exclusivos (como datos de origen de anunciantes).

### Habilitar alertas {#enable-alerts}

Puede activar alertas para recibir notificaciones sobre el estado del flujo de datos a su destino. Seleccione una alerta de la lista a la que suscribirse para recibir notificaciones sobre el estado del flujo de datos. Para obtener más información sobre las alertas, consulte la guía sobre [suscripción a alertas de destinos mediante la interfaz de usuario](../../ui/alerts.md).

Cuando termine de proporcionar detalles para la conexión de destino, seleccione **[!UICONTROL Siguiente]**.

## Activar públicos en este destino {#activate}

>[!IMPORTANT]
> 
>* Para activar los datos, necesita los **[!UICONTROL permisos de control de acceso]**, **[!UICONTROL Activar destinos]**, **[!UICONTROL Ver perfiles]** y **[!UICONTROL Ver segmentos]**[para ](/help/access-control/home.md#permissions). Lea la [descripción general del control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.
>* Para exportar *identidades*, necesita el **[!UICONTROL permiso de control de acceso]** de [Ver gráfico de identidad](/help/access-control/home.md#permissions). <br> ![Seleccione el área de nombres de identidad resaltada en el flujo de trabajo para activar audiencias en los destinos.](/help/destinations/assets/overview/export-identities-to-destination.png "Seleccione el área de nombres de identidad resaltada en el flujo de trabajo para activar audiencias en los destinos."){width="100" zoomable="yes"}

Lea [Activar perfiles y audiencias en un destino](../../ui/activate-segment-streaming-destinations.md) para obtener instrucciones sobre cómo activar audiencias en destinos.

## Uso de datos y gobernanza {#data-usage-governance}

Todos los destinos de [!DNL Adobe Experience Platform] cumplen con las políticas de uso de datos al administrar los datos. Para obtener información detallada sobre cómo [!DNL Adobe Experience Platform] aplica el control de datos, consulte la [Información general sobre el control de datos](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html?lang=es).

## Recursos adicionales {#additional-resources}

Para obtener más información, lea la [!DNL Yahoo/Verizon Media] [documentación sobre [!DNL DataX]](https://developer.verizonmedia.com/datax/guide/).
