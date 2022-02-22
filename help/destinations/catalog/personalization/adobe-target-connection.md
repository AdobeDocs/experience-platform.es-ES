---
keywords: personalización de target; destino; destino de experience platform target;destino de adobe target;
title: Conexión Adobe Target
description: Adobe Target es una aplicación que proporciona funciones de personalización y experimentación en tiempo real y con tecnología de IA en todas las interacciones de clientes entrantes entre sitios web, aplicaciones móviles y mucho más.
exl-id: 3e3c405b-8add-4efb-9389-5ad695bc9799
source-git-commit: 61a3a05466eca30ba08fcaf32a3f00e0ca49f325
workflow-type: tm+mt
source-wordcount: '474'
ht-degree: 1%

---

# Conexión Adobe Target {#adobe-target-connection}

## Información general {#overview}

Adobe Target es una aplicación que proporciona funciones de personalización y experimentación en tiempo real y con tecnología de IA en todas las interacciones de clientes entrantes entre sitios web, aplicaciones móviles y mucho más.

Adobe Target es una conexión personalizada en Adobe Experience Platform.

## Requisitos previos {#prerequisites}

Esta integración cuenta con la tecnología [SDK web de Adobe Experience Platform](../../../edge/home.md). Debe utilizar este SDK para utilizar este destino.

## Tipo de exportación {#export-type}

**Solicitud de perfil** : está solicitando todos los segmentos asignados en el destino de Adobe Target para un solo perfil.

## Casos de uso {#use-cases}

**Personalización de un banner de página principal**

Una empresa de ventas y alquiler de casa quiere personalizar su página principal con un banner, según las clasificaciones de segmentos del cliente en Adobe Experience Platform. La empresa puede seleccionar qué audiencias deben obtener una experiencia personalizada y enviarlas a Adobe Target como criterios de objetivo para su oferta de Target.

## Conectarse al destino {#connect}

>[!CONTEXTUALHELP]
>id="platform_destinations_target_datastream"
>title="Acerca de los ID de conjunto de datos"
>abstract="Esta opción determina en qué almacén de datos de recopilación de datos se incluyen los segmentos en la respuesta a la página. El menú desplegable muestra solo los conjuntos de datos que tienen habilitada la configuración de destino. Debe configurar un conjunto de datos para poder configurar el destino."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/datastreams.html?lang=en" text="Aprenda a configurar un conjunto de datos."

>[!IMPORTANT]
>
>Antes de crear una [!DNL Adobe Target] conexión, le recomendamos que lea nuestra guía sobre cómo [configurar destinos de personalización para la personalización de la misma página y de la página siguiente](../../ui/configure-personalization-destinations.md). Esta guía le guía a través de los pasos de configuración necesarios para casos de uso de personalización de la misma página y de la siguiente página, en varios componentes de Experience Platform.

Para conectarse a este destino, siga los pasos descritos en la sección [tutorial de configuración de destino](../../ui/connect-destination.md).

Adobe Experience Platform se conecta automáticamente a la instancia de Adobe Target de su empresa. No se requiere autenticación.

### Parámetros de conexión {#parameters}

While [configuración](../../ui/connect-destination.md) Para este destino, debe proporcionar la siguiente información:

* **Nombre**: Rellene el nombre preferido para este destino.
* **Descripción**: Escriba una descripción para el destino. Por ejemplo, puede mencionar para qué campaña utiliza este destino. Este campo es opcional.
* **ID de almacén de datos**: Esto determina en qué almacén de datos de recopilación de datos se incluyen los segmentos en la respuesta a la página. El menú desplegable muestra solo los conjuntos de datos que tienen habilitada la configuración de destino. Consulte [Configuración de un conjunto de datos](../../../edge/fundamentals/datastreams.md) para obtener más información.

## Activar segmentos en este destino {#activate}

Lectura [Activar perfiles y segmentos en destinos de solicitud de perfil](../../ui/activate-profile-request-destinations.md) para obtener instrucciones sobre la activación de segmentos de audiencia en este destino.

## Datos exportados {#exported-data}

Adobe Target lee datos de perfil de Adobe Experience Platform Edge Network, por lo que no se exportan datos.

## Uso y gobernanza de los datos {#data-usage-governance}

Todo [!DNL Adobe Experience Platform] Los destinos de cumplen las políticas de uso de datos al administrar los datos. Para obtener información detallada sobre cómo [!DNL Adobe Experience Platform] exige la administración de datos, lea la [Información general sobre la administración de datos](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html).
