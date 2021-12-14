---
title: Conexión de datos de Verizon MediaYahoo
description: DataX es una infraestructura agregada de Verizon Media/Yahoo que aloja varios componentes que permiten a Verizon Media/Yahoo intercambiar datos con sus socios externos de forma segura, automatizada y escalable.
exl-id: 7d02671d-8650-407d-9c9f-fad7da3156bc
source-git-commit: 27e5c64f31b9a68252d262b531660811a0576177
workflow-type: tm+mt
source-wordcount: '586'
ht-degree: 2%

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

## Tipo de exportación {#export-type}

**Exportación de segmentos** : exporta todos los miembros de un segmento (audiencia) con los identificadores (correo electrónico) utilizados en el destino de Verizon Media.

## Casos de uso {#use-cases}

Las API de DataX están disponibles para los anunciantes que deseen dirigirse a un grupo de audiencia específico con direcciones de correo electrónico marcadas por Verizon Media (VMG) pueden crear rápidamente un nuevo segmento y insertar el grupo de audiencia deseado con la API casi en tiempo real de VMG.

## Conectarse al destino {#connect}

![Tarjeta de destino de Yahoo DataX en la interfaz de usuario de Platform](/help/destinations/assets/catalog/advertising/yahoo-datax/catalog.png)

Para conectarse a este destino, siga los pasos descritos en la sección [tutorial de configuración de destino](../../ui/connect-destination.md).

### Parámetros de conexión {#parameters}

While [configuración](../../ui/connect-destination.md) Para este destino, debe proporcionar la siguiente información:

* **[!UICONTROL Nombre]**: Un nombre por el cual reconocerá este destino en el futuro.
* **[!UICONTROL Descripción]**: Descripción que le ayudará a identificar este destino en el futuro.
* **[!UICONTROL ID de MDM]**: Se trata de un identificador único en Yahoo DataX y es un campo obligatorio para configurar exportaciones de datos a este destino. Si no conoce este ID, póngase en contacto con su administrador de cuentas de Yahoo Data X.  Con los ID de MDM, los datos pueden restringirse para su uso únicamente con un determinado conjunto de usuarios exclusivos (como los datos de origen de los anunciantes).

## Activar segmentos en este destino {#activate}

Lectura [Activar perfiles y segmentos en un destino](../../ui/activate-segment-streaming-destinations.md) para obtener instrucciones sobre la activación de segmentos de audiencia en destinos.

## Uso y gobernanza de los datos {#data-usage-governance}

Todo [!DNL Adobe Experience Platform] Los destinos de cumplen las políticas de uso de datos al administrar los datos. Para obtener información detallada sobre cómo [!DNL Adobe Experience Platform] exige el control de datos; consulte [Información general sobre la administración de datos](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html).

## Recursos adicionales {#additional-resources}

Para obtener más información, consulte Yahoo/Verizon Media [documentación sobre DataX](https://developer.verizonmedia.com/datax/guide/).
