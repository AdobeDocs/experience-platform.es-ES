---
description: Adobe Experience Platform Destination SDK es un conjunto de API de configuración que le permiten configurar patrones de integración de destino para que el Experience Platform entregue datos de audiencia y perfil a su punto final o ubicación de almacenamiento, en función de los formatos de autenticación y datos que elija. Las configuraciones se almacenan en Experience Platform y se pueden recuperar mediante API para obtener actualizaciones adicionales.
title: Adobe Experience Platform Destination SDK
exl-id: 7aca9f40-98c8-47c2-ba88-4308fc2b1798
source-git-commit: 118ff85a9fceb8ee81dbafe2c381d365b813da29
workflow-type: tm+mt
source-wordcount: '854'
ht-degree: 2%

---

# Adobe Experience Platform Destination SDK

Adobe Experience Platform Destination SDK es un conjunto de API de configuración que le permiten configurar patrones de integración de destino para que el Experience Platform entregue datos de audiencia y perfil a su punto final o ubicación de almacenamiento, en función de los formatos de autenticación y datos que elija. Las configuraciones se almacenan en Experience Platform y se pueden recuperar mediante API para obtener actualizaciones adicionales.

La documentación del Destination SDK le indica que debe utilizar el Adobe Experience Platform Destination SDK para configurar, probar y publicar una integración de destino de productos con Adobe Experience Platform, y que su destino forme parte del catálogo de destinos en constante crecimiento. Con Destination SDK, también puede crear su propio destino privado personalizado para exportar datos adaptados a sus necesidades.

![Captura de pantalla de la interfaz de usuario del Experience Platform que muestra el catálogo de destinos](assets/destinations-catalog-overview.png)

## Integraciones personalizadas y producidas {#productized-custom-integrations}

>[!IMPORTANT]
>
> Esta funcionalidad para crear destinos personalizados privados solo está disponible para [Adobe Real-time Customer Data Platform Ultimate](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform.html) clientes.

Como socio Destination SDK, puede beneficiarse de añadir su destino de producto al [catálogo de Experience Platform](../catalog/overview.md):

1. Estandarizar las configuraciones de integración entre clientes con parámetros preconfigurados y simplificar la experiencia de configuración para los clientes.
2. Introduzca una tarjeta de destino con marca en el catálogo de destinos de Experience Platform para simplificar la configuración y el conocimiento del cliente.
3. Se presenta como una integración de destino productizada con Adobe Experience Platform &amp; Adobe Real-time Customer Data Platform.

Como cliente Experience Platform, también puede crear su propio destino personalizado privado, que se adapte mejor a sus necesidades de activación.

![Diagrama de información general que muestra cómo interactúan los desarrolladores de destino con Destination SDK y cómo se benefician los clientes de Real-Time CDP de los destinos productivos y privados.](assets/destination-sdk-visual.png)

## Tipos de integración compatibles {#supported-integration-types}

### Integraciones en tiempo real (flujo continuo) {#real-time-integrations}

A través de Destination SDK, Adobe Experience Platform admite integraciones en tiempo real (también denominadas flujo continuo) con destinos que tienen un extremo de API de REST. La integración en tiempo real con Experience Platform admite funciones como:

* Transformación y agregación de mensajes
* Relleno de perfiles
* Integración de metadatos configurables para inicializar la configuración de audiencias y la transferencia de datos
* Autenticación configurable
* Un conjunto de API de prueba y validación para que pueda probar e iterar las configuraciones de destino

### Integraciones basadas en archivos {#file-based-integrations}

A través de Destination SDK, también puede configurar integraciones para exportar periódicamente archivos a la ubicación de almacenamiento que elija. La integración basada en archivos con Experience Platform admite funciones como:

* Exportación de archivos en varios formatos compatibles (CSV, Parquet, JSON)
* Opciones de formato de archivo configurables, que le permiten estructurar el formato de los archivos exportados para que cumpla los requisitos del flujo descendente.

Obtenga información sobre los requisitos técnicos del lado de los destinos en la [requisitos previos de integración](integration-prerequisites.md) y lea sobre todas las configuraciones admitidas en el [opciones de configuración](functionality/configuration-options.md) article

## Obtener acceso al Destination SDK {#get-access}

El acceso de los Destination SDK varía en función de su estado como socio o Experience Platform, cliente de Real-Time CDP. Consulte la siguiente tabla para obtener más información.

| Tipo de socio o cliente | Cómo acceder al Destination SDK |
---------|----------|
| Proveedor de software independiente (ISV) | Únase a [Programa de Socios de Tecnología de Adobe](https://partners.adobe.com/technologyprogram/experiencecloud.html) y solicitar obtener un simulador para pruebas de Experience Platform aprovisionado para acceder al Destination SDK. |
| Integrador de sistemas (SI) | Debe encontrarse en el nivel oro o platino en la variable [Programa para Socios de Soluciones de Adobe](https://solutionpartners.adobe.com/home.html), y obtendrá un simulador para pruebas de Experience Platform aprovisionado y acceso al Destination SDK. |
| cliente Experience Platform en la variable [Paquete Real-Time CDP Ultimate](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform.html) | De forma predeterminada, puede acceder a los entornos limitados y al Destination SDK de Experience Platform, lo que le permite crear destinos privados para su organización. |

{style="table-layout:auto"}

## Proceso de alto nivel {#process}

A continuación se describe el proceso para configurar el destino en Experience Platform:

1. Si es un ISV o SI, consulte la [obtener acceso](#get-access) en la sección anterior. [Paquete Real-Time CDP Ultimate](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform.html) los clientes de pueden omitir este paso.
2. [Solicitud de aprovisionamiento de un simulador para pruebas de Experience Platform](https://adobeexchangeec.zendesk.com/hc/en-us/articles/360037457812-Adobe-Experience-Platform-Sandbox-Accounts-Access-Adding-Users-and-Support) y habilite el permiso de creación de destino.
3. Cree su integración. Siga las instrucciones de la documentación del producto para configurar [destinos de flujo continuo](guides/configure-destination-instructions.md) o [destinos basados en archivos](guides/configure-file-based-destination-instructions.md).
4. Pruebe la integración. Siga las instrucciones de la documentación del producto para probar [destinos de flujo continuo](testing-api/streaming-destinations/streaming-destination-testing-overview.md) o [destinos basados en archivos](testing-api/batch-destinations/file-based-destination-testing-overview.md).
5. Si es un ISV o SI crea un [integración de productos](./overview.md#productized-custom-integrations), [enviar su integración](guides/submit-destination.md) para la revisión del Adobe (el tiempo de respuesta estándar es de cinco días hábiles).
6. Si es un ISV o SI que crea una integración de productos, utilice la variable [proceso de documentación de autoservicio](docs-framework/documentation-instructions.md) para crear una página de documentación del producto en el Experience League de destino.
7. Para las integraciones de productos, una vez aprobadas por Adobe, la integración se mostrará en la variable [catálogo de Experience Platform](../catalog/overview.md).
8. Si desea actualizar la integración, siga el mismo proceso.

## Referencia {#reference}

Adobe recomienda leer y comprender la siguiente documentación del Experience Platform:

* [Información general sobre los destinos de Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/destinations/home.html?lang=en)
* [Base de la composición del esquema XDM](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/composition.html?lang=es)
* [Información general del área de nombres de identidad](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=es)
