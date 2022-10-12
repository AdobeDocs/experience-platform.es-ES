---
description: Adobe Experience Platform Destination SDK es un conjunto de API de configuración que le permiten configurar patrones de integración de destino para que el Experience Platform entregue datos de audiencia y perfil a su punto final o ubicación de almacenamiento, en función de los formatos de autenticación y datos que elija. Las configuraciones se almacenan en Experience Platform y se pueden recuperar mediante API para obtener actualizaciones adicionales.
title: Adobe Experience Platform Destination SDK
exl-id: 7aca9f40-98c8-47c2-ba88-4308fc2b1798
source-git-commit: 94d46ceeef6eef507115c60aaa6820d4560e4d44
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Adobe Experience Platform Destination SDK

## Información general {#destinations-sdk}

Adobe Experience Platform Destination SDK es un conjunto de API de configuración que le permiten configurar patrones de integración de destino para que el Experience Platform entregue datos de audiencia y perfil a su punto final o ubicación de almacenamiento, en función de los formatos de autenticación y datos que elija. Las configuraciones se almacenan en Experience Platform y se pueden recuperar mediante API para obtener actualizaciones adicionales.

La documentación del Destination SDK le indica que debe utilizar el Adobe Experience Platform Destination SDK para configurar, probar y publicar una integración de destino de productos con Adobe Experience Platform, y que su destino forme parte del catálogo de destinos en constante crecimiento. Con Destination SDK, también puede crear su propio destino privado personalizado para exportar datos adaptados a sus necesidades.

![Captura de pantalla de la interfaz de usuario del Experience Platform que muestra el catálogo de destinos](./assets/destinations-catalog-overview.png)

## Integraciones personalizadas y producidas {#productized-custom-integrations}

>[!IMPORTANT]
>
> Esta funcionalidad para crear destinos personalizados privados solo está disponible para [Real-time Customer Data Platform Ultimate](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform.html) clientes.

Como socio Destination SDK, puede beneficiarse de añadir su destino de producto al [catálogo de Experience Platform](/help/destinations/catalog/overview.md):
1. Estandarizar las configuraciones de integración entre clientes con parámetros preconfigurados y simplificar la experiencia de configuración para los clientes.
2. Introduzca una tarjeta de destino con marca en el catálogo de destinos de Experience Platform para simplificar la configuración y el conocimiento del cliente.
3. Se presenta como una integración de destino productizada con Adobe Experience Platform &amp; Real-time Customer Data Platform.

Como cliente Experience Platform, también puede crear un destino personalizado privado propio, que se adapte mejor a sus necesidades de activación.

![Diagrama de información general que muestra cómo los desarrolladores de destino interactúan con el Destination SDK y cómo los clientes de CDP en tiempo real se benefician de los destinos productivos y privados.](./assets/destination-sdk-visual.png)

## Tipos de integraciones compatibles {#supported-integration-types}

A través de Destination SDK, Adobe Experience Platform admite integraciones en tiempo real con destinos que tienen un extremo de API de REST. La integración en tiempo real con Experience Platform admite funciones como:
* Transformación y agregación de mensajes
* Relleno de perfiles
* Integración de metadatos configurables para inicializar la configuración de audiencias y la transferencia de datos
* Autenticación configurable
* Un conjunto de API de prueba y validación para que pueda probar e iterar las configuraciones de destino

A través de Destination SDK, también puede configurar integraciones para exportar periódicamente archivos a la ubicación de almacenamiento que elija. La integración en tiempo real con Experience Platform admite funciones como:
* Exportación de archivos en varios formatos compatibles (CSV, Parquet, JSON)
* Opciones de formato de archivo configurables, que le permiten estructurar el formato de los archivos exportados para que cumpla los requisitos del flujo descendente.

Obtenga información sobre los requisitos técnicos del lado de los destinos en la [requisitos previos de integración](./integration-prerequisites.md) artículo.

## Obtener acceso al Destination SDK {#get-access}

El acceso de los Destination SDK varía en función de su estado como socio o Experience Platform, cliente de Real-Time CDP. Para obtener más información, consulte la siguiente tabla.


| Tipo de socio o cliente | Cómo acceder al Destination SDK |
---------|----------|
| Proveedor de software independiente (ISV) | Únase a [Programa de intercambio de Adobes](https://partners.adobe.com/exchangeprogram/experiencecloud.html) y solicitar obtener un simulador para pruebas de Experience Platform aprovisionado para acceder al Destination SDK. |
| Integrador de sistemas (SI) | Debe encontrarse en el nivel oro o platino en la variable [Programa para Socios de Soluciones de Adobe](https://solutionpartners.adobe.com/home.html), y obtendrá un simulador para pruebas de Experience Platform aprovisionado y acceso al Destination SDK. |
| cliente Experience Platform en la variable [Paquete Real-Time CDP Ultimate](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform.html) | De forma predeterminada, puede acceder a los entornos limitados y al Destination SDK de Experience Platform, lo que le permite crear destinos privados para su organización. |

{style=&quot;table-layout:auto&quot;}

## Proceso de alto nivel {#process}

A continuación se describe el proceso para configurar el destino en Experience Platform:

1. Si es un ISV o SI, consulte la información de acceso de la sección anterior. [Activación de Adobe Experience Platform](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-platform0.html) los clientes de pueden omitir este paso.
2. [Solicitud de aprovisionamiento de un simulador para pruebas de Experience Platform](https://adobeexchangeec.zendesk.com/hc/en-us/articles/360037457812-Adobe-Experience-Platform-Sandbox-Accounts-Access-Adding-Users-and-Support) y habilite el permiso de creación de destino.
3. Cree su integración. Siga las instrucciones de la documentación del producto para configurar [destinos de flujo continuo](./configure-destination-instructions.md) o [destinos basados en archivos](./configure-file-based-destination-instructions.md).
4. Pruebe la integración. Siga las instrucciones de la documentación del producto para probar [destinos de flujo continuo](./test-destination.md) o [destinos basados en archivos](./file-based-destination-testing-overview.md).
5. Si es un ISV o SI crea un [integración de productos](./overview.md#productized-custom-integrations), [enviar su integración](./submit-destination.md) para la revisión del Adobe (el tiempo de respuesta estándar es de cinco días hábiles).
6. Si es un ISV o SI que crea una integración de productos, utilice la variable [proceso de documentación de autoservicio](./docs-framework/documentation-instructions.md) para crear una página de documentación del producto en el Experience League de destino.
7. Para las integraciones de productos, una vez aprobadas por Adobe, la integración se mostrará en la variable [catálogo de Experience Platform](/help/destinations/catalog/overview.md).
8. Si desea actualizar la integración, siga el mismo proceso.

## Referencia {#reference}

Adobe recomienda leer y comprender la siguiente documentación del Experience Platform:

* [Información general sobre los destinos de Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/destinations/home.html?lang=en)
* [Base de la composición del esquema XDM](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/composition.html?lang=es)
* [Información general del área de nombres de identidad](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=es)
