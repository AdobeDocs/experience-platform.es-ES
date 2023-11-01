---
description: Adobe Experience Platform Destination SDK es un conjunto de API de configuración que le permiten configurar patrones de integración de destino para que Experience Platform envíe datos de audiencia y perfil a su punto final o ubicación de almacenamiento, en función de los datos y los formatos de autenticación de su elección. Las configuraciones se almacenan en el Experience Platform y se pueden recuperar mediante API para actualizaciones adicionales.
title: Adobe Experience Platform Destination SDK
exl-id: 7aca9f40-98c8-47c2-ba88-4308fc2b1798
source-git-commit: e300e57df998836a8c388511b446e90499185705
workflow-type: tm+mt
source-wordcount: '848'
ht-degree: 4%

---

# Adobe Experience Platform Destination SDK

Adobe Experience Platform Destination SDK es un conjunto de API de configuración que le permiten configurar patrones de integración de destino para que Experience Platform envíe datos de audiencia y perfil a su punto final o ubicación de almacenamiento, en función de los datos y los formatos de autenticación de su elección. Las configuraciones se almacenan en el Experience Platform y se pueden recuperar mediante API para actualizaciones adicionales.

En la documentación del Destination SDK se proporcionan instrucciones para utilizar el Adobe Experience Platform Destination SDK con el fin de configurar, probar y publicar una integración de destino producida con Adobe Experience Platform, y para que su destino forme parte del creciente catálogo de destinos. Con Destination SDK, también puede crear su propio destino privado personalizado para exportar datos adaptados a sus necesidades.

![Captura de pantalla de la IU de Experience Platform que muestra el catálogo de destinos](assets/destinations-catalog-overview.png)

## Integraciones personalizadas y producidas {#productized-custom-integrations}

>[!IMPORTANT]
>
> Esta funcionalidad para crear destinos personalizados privados solo está disponible para [Adobe Real-time Customer Data Platform Ultimate](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform.html?lang=es) clientes.

Como socio Destination SDK, puede beneficiarse de añadir su destino de productos a [catálogo del Experience Platform](../catalog/overview.md):

1. Estandarice las configuraciones de integración entre clientes con parámetros preconfigurados y simplifique la experiencia de configuración para los clientes.
2. Introduzca una tarjeta de destino con marca en el catálogo de destinos de Experience Platform para facilitar la configuración y la concienciación del cliente.
3. Incluirse como una integración de destino de producción con Adobe Experience Platform y Adobe Real-time Customer Data Platform.

Como cliente Experience Platform, también puede crear su propio destino personalizado privado, que mejor se adapte a sus necesidades de activación.

![Diagrama de información general que muestra cómo los desarrolladores de destinos interactúan con Destination SDK y cómo los clientes de Real-Time CDP se benefician de los destinos productivos y privados.](assets/destination-sdk-visual.png)

## Tipos de integración admitidos {#supported-integration-types}

### Integraciones en tiempo real (streaming) {#real-time-integrations}

A través de Destination SDK, Adobe Experience Platform admite integraciones en tiempo real (también denominadas &quot;streaming&quot;) con destinos que tienen un extremo de API de REST. La integración en tiempo real con Experience Platform admite funciones como:

* Transformación y agregación de mensajes
* Relleno de perfil
* Integración de metadatos configurable para inicializar la configuración de audiencia y la transferencia de datos
* Autenticación configurable
* Un conjunto de API de prueba y validación para probar e iterar las configuraciones de destino

### Integraciones basadas en archivos {#file-based-integrations}

Mediante Destination SDK, también puede configurar integraciones para exportar archivos periódicamente a la ubicación de almacenamiento que elija. La integración basada en archivos con Experience Platform admite funciones como:

* Exportación de archivos en varios formatos compatibles (CSV, Parquet, JSON)
* Opciones de formato de archivo configurables, que permiten estructurar el formato de los archivos exportados para satisfacer los requisitos de flujo descendente.

Obtenga información sobre los requisitos técnicos en el lado de los destinos en la [requisitos previos de integración](integration-prerequisites.md) y lea todas las configuraciones compatibles en la [opciones de configuración](functionality/configuration-options.md) artículo

## Obtener acceso al Destination SDK {#get-access}

El acceso de Destination SDK varía en función de su estado como socio o Experience Platform, cliente de Real-Time CDP. Consulte la tabla siguiente para obtener más información.

| Tipo de socio o cliente | Cómo acceder al Destination SDK |
---------|----------|
| Proveedor de software independiente (ISV) | Únase a [Programa de socios de tecnología de Adobe](https://partners.adobe.com/technologyprogram/experiencecloud.html) y solicite disponer de una zona protegida de Experience Platform para acceder al Destination SDK. |
| Integrador de sistemas (SI) | Debe tener nivel Gold o Platinum en el [Programa de socios de soluciones de Adobe](https://solutionpartners.adobe.com/home.html), y obtendrá una zona protegida de Experience Platform aprovisionada y acceso a Destination SDK. |
| Cliente Experience Platform en [Paquete de Real-Time CDP Ultimate](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform.html?lang=es) | De forma predeterminada, se obtiene acceso a los entornos limitados y a Destination SDK de Experience Platform, lo que le permite crear destinos privados para su organización. |

{style="table-layout:auto"}

## Proceso de alto nivel {#process}

El proceso para configurar el destino en Experience Platform se describe a continuación:

1. Si es ISV o SI, consulte la [obtención de acceso](#get-access) información en la sección anterior. [Paquete de Real-Time CDP Ultimate](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform.html?lang=es) Los clientes de pueden omitir este paso.
2. [Solicitud para aprovisionar una zona protegida de Experience Platform](https://adobeexchangeec.zendesk.com/hc/en-us/articles/360037457812-Adobe-Experience-Platform-Sandbox-Accounts-Access-Adding-Users-and-Support) y habilite el permiso de creación de destino.
3. Cree su integración. Siga las instrucciones de la documentación del producto para configurarlo [destinos de streaming](guides/configure-destination-instructions.md) o [destinos basados en archivos](guides/configure-file-based-destination-instructions.md).
4. Pruebe la integración. Siga las instrucciones de la documentación del producto para realizar la prueba [destinos de streaming](testing-api/streaming-destinations/streaming-destination-testing-overview.md) o [destinos basados en archivos](testing-api/batch-destinations/file-based-destination-testing-overview.md).
5. Si es ISV o SI está creando un [integración de productos](./overview.md#productized-custom-integrations), [envíe su integración](guides/submit-destination.md) para que el Adobe lo revise (el tiempo de respuesta estándar es de cinco días hábiles).
6. Si es un ISV o SI que crea una integración de productos, utilice el [proceso de documentación de autoservicio](docs-framework/documentation-instructions.md) para crear una página de documentación del producto en Experience League para su destino.
7. Para integraciones de productos, una vez aprobadas por el Adobe, la integración se mostrará en la [catálogo del Experience Platform](../catalog/overview.md).
8. Si desea actualizar la integración, siga el mismo proceso.

## Referencia {#reference}

El Adobe recomienda leer y comprender la siguiente documentación de Experience Platform:

* [Información general sobre destinos Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/destinations/home.html?lang=es)
* [Base de composición de esquema XDM](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/composition.html?lang=es)
* [Información general de área de nombres de identidad](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=es)
