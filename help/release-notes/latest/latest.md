---
title: Notas de la versión de Adobe Experience Platform
description: Notas de la versión de julio de 2023 de Adobe Experience Platform.
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: 4064c4a7f855fa065c711df5d02d6b7982cc7627
workflow-type: tm+mt
source-wordcount: '659'
ht-degree: 33%

---

# Notas de la versión de Adobe Experience Platform

**Fecha de la versión: 26 de julio de 2023**

Actualizaciones de las funciones existentes en Adobe Experience Platform:

- [Recopilación de datos](#data-collection)
- [Preparación de los datos](#data-prep)
- [Servicio de segmentación](#segmentation)
- [Fuentes](#sources)

## Recopilación de datos {#data-collection}

Adobe Experience Platform proporciona un conjunto de tecnologías que le permiten recopilar datos de experiencia del cliente del lado del cliente y enviarlos a la red perimetral de Adobe Experience Platform, donde se pueden enriquecer, transformar y distribuir a destinos de Adobe o que no sean de Adobe.

**Funciones nuevas o actualizadas**

| Tipo | Función | Descripción |
| --- | --- | --- |
| Reenvío de eventos y etiquetas | Registros de auditoría de recopilación de datos | Ahora puede ver cuándo se realizó una acción y quién realizó esta acción en Etiquetas y Reenvío de eventos. Esto facilita la resolución de problemas del producto, el control adecuado y las actividades de auditoría interna. Estos datos de auditoría se muestran mediante menús deslizantes en contexto que también incluyen acciones rápidas y actualizaciones de estado de los recursos. Estos datos son visibles en la IU de Etiquetas y Reenvío de eventos en las pantallas siguientes:<br><ul><li>[Información general de propiedad](../../tags/ui/event-forwarding/overview.md#properties)</li><li>[Reglas](../../tags/ui/event-forwarding/overview.md#rules)</li><li>[Elementos de datos](../../tags/ui/event-forwarding/overview.md#data-elements)</li><li>[Extensiones](../../tags/ui/event-forwarding/overview.md#extensions)</li><li>[Revisión de biblioteca](https://experienceleague.adobe.com/docs/platform-learn/data-collection/tags/build-and-publish-a-library.html)</li><li>[Última compilación y publicación de la biblioteca](https://experienceleague.adobe.com/docs/platform-learn/data-collection/tags/build-and-publish-a-library.html)</li></ul> |
| Corrientes de datos | [Búsqueda geográfica](../../datastreams/configure.md#advanced-options) | Ahora puede configurar la geolocalización y la búsqueda de red de flujos de datos para incluir información como: <ul><li>País</li><li>Código postal</li><li>Estado/Provincia</li><li>DMA</li><li>Ciudad</li><li>Latitud </li><li>Longitud</li><li>Portadora</li><li>Domain</li><li>ISP</li></ul> Usted es responsable de garantizar que ha obtenido todos los permisos, consentimientos, autorizaciones y autorizaciones necesarios según las leyes y regulaciones aplicables para recopilar, procesar y transmitir datos personales, incluida información precisa sobre geolocalización. <br> La selección de la ofuscación de la dirección IP no afecta al nivel de información de geolocalización que se derivará de la dirección IP y se enviará a las soluciones de Adobe configuradas. Las búsquedas de geolocalización deben limitarse o deshabilitarse por separado. <br> Consulte la [documentación de flujos de datos](../../datastreams/configure.md#advanced-options) para obtener más información. |

{style="table-layout:auto"}

Para obtener más información sobre la recopilación de datos, lea la [información general sobre colecciones de datos](../../tags/home.md).

## Preparación de los datos {#data-prep}

La preparación de datos permite a los ingenieros de datos asignar, transformar y validar datos desde y hacia el modelo de datos de experiencia (XDM).

**Funciones nuevas o actualizadas**

| Función | Descripción |
| --- | --- |
| Nuevas funciones de asignación | Ahora puede utilizar las siguientes funciones al asignar objetos en la preparación de datos: <ul><li>`map_get_values`</li><li>`map_has_keys`</li><li>`add_to_map`</li></ul> Para obtener más información sobre estas funciones, lea la [Guía de funciones de preparación de datos](../../data-prep/functions.md#hierarchies---objects). |

{style="table-layout:auto"}

Para obtener más información sobre la preparación de datos, lea [Información general sobre preparación de datos](../../data-prep/home.md).

## Servicio de segmentación {#segmentation}

[!DNL Segmentation Service] le permite segmentar datos almacenados en [!DNL Experience Platform] que se relaciona con personas (como clientes, clientes potenciales, usuarios u organizaciones) en audiencias. Puede crear audiencias a través de definiciones de segmentos u otras fuentes a partir de sus [!DNL Real-Time Customer Profile] datos. Estas audiencias se configuran de forma centralizada y se mantienen en [!DNL Platform]y son fácilmente accesibles desde cualquier solución de Adobe.

**Funciones nuevas o actualizadas**

| Función | Descripción |
| ------- | ----------- |
| Audiencia  Portal | Audience Portal ofrece una nueva experiencia de navegación para acceder, crear y administrar audiencias en Adobe Experience Platform. En Audience Portal, puede ver audiencias generadas por Platform y audiencias generadas externamente; mejorar la eficacia del trabajo mediante el filtrado, las carpetas y las etiquetas; crear audiencias generadas por Platform; e importar audiencias generadas externamente a través de archivos CSV. Para obtener más información sobre Audience Portal, lea la [Guía de IU del servicio de segmentación](../../segmentation/ui/overview.md). |
| Composición de audiencia | Composición de audiencia proporciona un espacio de trabajo fácil de usar para crear y editar audiencias, mediante bloques que se utilizan para representar diferentes acciones. Para obtener más información sobre la composición de audiencias, lea la [Guía de IU de composición de audiencia](../../segmentation/ui/audience-composition.md). |

Para obtener más información sobre [!DNL Segmentation Service], lea la [Resumen de segmentación](../../segmentation/home.md).

## Fuentes {#sources}

Experience Platform proporciona una API RESTful y una IU interactiva que le permite configurar conexiones de origen para varios proveedores de datos con facilidad. Estas conexiones de origen le permiten autenticarse y conectarse a sistemas de almacenamiento externos y servicios CRM, establecer tiempos para ejecuciones de ingesta y administrar el rendimiento de ingesta de datos.

**Funciones nuevas o actualizadas**

| Función | Descripción |
| --- | --- |
| [!BADGE Beta]{type=Informative}[!DNL SAP Commerce] | Ahora puede utilizar la variable [[!DNL SAP Commerce] origen](../../sources/connectors/ecommerce/sap-commerce.md) para obtener datos de facturación de suscripción de su [!DNL SAP Commerce] cuenta para el Experience Platform. |
| Compatibilidad con [!DNL Phoenix] | Ahora puede utilizar la variable [[!DNL Phoenix] origen](../../sources/connectors/databases/phoenix.md) para obtener datos de su [!DNL Phoenix] base de datos a Experience Platform. |
| Actualizaciones de autenticación a [!DNL Salesforce] y [!DNL Salesforce Service Cloud] | Ahora puede especificar la versión de API de su [[!DNL Salesforce]](../../sources/connectors/crm/salesforce.md) y [[!DNL Salesforce Service Cloud]](../../sources/connectors/customer-success/salesforce-service-cloud.md) origen al autenticar una cuenta nueva con la interfaz de usuario de Experience Platform o la [!DNL Flow Service] API. |

{style="table-layout:auto"}

Para obtener más información sobre las fuentes, lea la [información general de orígenes](../../sources/home.md).
