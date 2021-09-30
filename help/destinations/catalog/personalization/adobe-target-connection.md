---
keywords: personalización de target; destino; destino de experience platform target;destino de adobe target;
title: Conexión de Adobe Target (Beta)
description: Adobe Target es una aplicación que proporciona personalización y experimentación en tiempo real, 1:1 y con tecnología de IA en todas las interacciones de clientes entrantes entre sitios web, aplicaciones móviles y mucho más.
source-git-commit: 0635828cf3f637e67d2cabda860ca452e61892d4
workflow-type: tm+mt
source-wordcount: '392'
ht-degree: 2%

---


# Conexión de Adobe Target (Beta) {#adobe-target-connection}

## Información general {#overview}

>[!IMPORTANT]
>
>La conexión de Adobe Target en Adobe Experience Platform está actualmente en fase beta. La documentación y la funcionalidad están sujetas a cambios.

Adobe Target es una aplicación que proporciona personalización y experimentación en tiempo real, 1:1 , con tecnología de IA en todas las interacciones de clientes entrantes entre sitios web, aplicaciones móviles y mucho más.

Adobe Target es una conexión personalizada en Adobe Experience Platform.

## Requisitos previos {#prerequisites}

Esta integración es ofrecida por el [Adobe Experience Platform Web SDK](../../../edge/home.md). Debe utilizar este SDK para utilizar este destino.

## Tipo de exportación {#export-type}

**Solicitud de perfil** : está solicitando todos los segmentos asignados en el destino de Adobe Target para un solo perfil.

## Casos de uso {#use-cases}

**Personalización de un banner de página principal**

Una empresa de ventas y alquiler de casa quiere personalizar su página principal con un banner, según las clasificaciones de segmentos del cliente en Adobe Experience Platform. La empresa puede seleccionar qué audiencias deben obtener una experiencia personalizada y enviarlas a Adobe Target como criterios de objetivo para su oferta de Target.

## Conectarse al destino {#connect}

Para conectarse a este destino, siga los pasos descritos en el [tutorial de configuración de destino](../../ui/connect-destination.md).

Adobe Experience Platform se conecta automáticamente a la instancia de Adobe Target de su empresa. No se requiere autenticación.

### Parámetros de conexión {#parameters}

Mientras [configura](../../ui/connect-destination.md) este destino, debe proporcionar la siguiente información:

* **Nombre**: Rellene el nombre preferido para este destino.
* **Descripción**: Escriba una descripción para el destino. Por ejemplo, puede mencionar para qué campaña utiliza este destino. Este campo es opcional.
* **ID de almacén de datos**: Esto determina en qué almacén de datos de recopilación de datos se incluyen los segmentos en la respuesta a la página. El menú desplegable muestra solo los conjuntos de datos que tienen habilitada la configuración de destino. Consulte [Configuración de un conjunto de datos](../../../edge/fundamentals/datastreams.md) para obtener más información.

## Activar segmentos en este destino {#activate}

Lea [Activar perfiles y segmentos en destinos de solicitud de perfil](../../ui/activate-profile-request-destinations.md) para obtener instrucciones sobre cómo activar segmentos de audiencia en este destino.

## Datos exportados {#exported-data}

Adobe Target lee datos de perfil de Adobe Experience Platform Edge Network, por lo que no se exportan datos.

## Uso y gobernanza de los datos {#data-usage-governance}

Todos los destinos [!DNL Adobe Experience Platform] cumplen las políticas de uso de datos al administrar los datos. Para obtener información detallada sobre cómo [!DNL Adobe Experience Platform] aplica el control de datos, lea la [Información general sobre el control de datos](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html).
