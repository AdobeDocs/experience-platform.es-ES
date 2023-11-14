---
title: Conector de origen de Adobe Commerce
description: Aprenda a utilizar la fuente de Adobe Commerce para llevar los datos de comercio a Experience Platform.
last-substantial-update: 2023-06-21T00:00:00Z
exl-id: 8313e3d5-5c3d-448c-883c-b9386dbbb2f5
source-git-commit: 5eaa5e518de72b452d43a9abca3082efe9e4cb32
workflow-type: tm+mt
source-wordcount: '535'
ht-degree: 1%

---

# Adobe Commerce

Adobe Commerce es una plataforma de comercio ágil B2B y B2C que permite a los comerciantes y marcas acelerar los ingresos mediante experiencias de comercio digital centradas en el cliente en espacios en línea y físicos.

Fuentes de Adobe Experience Platform admite la integración de Adobe Commerce para permitir que los comerciantes envíen datos de tienda y back office a la red perimetral de Experience Platform, de modo que otros productos de Adobe Experience Cloud como Adobe Analytics y Adobe Target puedan utilizar [!DNL Commerce] datos.

* **Eventos de tienda**: Capturar interacciones del comprador como `View Page`, `View Product`, y `Add to Cart`. Para los comerciantes B2B, los eventos de tienda también capturan [listas de solicitudes](<https://experienceleague.adobe.com/docs/commerce-admin/b2b/requisition-lists/requisition-lists.html>).
* **Eventos de back office**: captura información sobre el estado de un pedido, como si se ha realizado, cancelado, reembolsado, enviado o completado.

>[!NOTE]
>
>Los datos capturados en Adobe Commerce no incluyen información de identificación personal (PII). Todos los identificadores de usuario, como los ID de cookie y las direcciones IP, se anonimizan estrictamente.

## Requisitos previos

Para conectar Adobe Commerce a Experience Platform, debe tener lo siguiente:

* Adobe Commerce 2.4.3 o posterior.
* Un Adobe ID y un ID de organización válidos.
* Acceso a la [Extensión de capa de datos del cliente de Adobe](../../../tags/extensions/client/client-data-layer/overview.md). Esta extensión es necesaria para recopilar datos de evento de tienda.
* Derechos a otros productos DX de Adobe.

## Pasos de incorporación

Para incorporar completamente su cuenta de origen de Adobe Commerce, siga los pasos descritos a continuación junto con la documentación correspondiente.

* [Instale el [!DNL Data Connection] extensión](https://experienceleague.adobe.com/docs/commerce-merchant-services/data-connection/fundamentals/install.html) para Adobe Commerce. Puede descargar la extensión del conector desde [Adobe Marketplace](https://commercemarketplace.adobe.com/magento-experience-platform-connector.html).
* Una vez que haya instalado correctamente la extensión del conector, inicie sesión en su cuenta de Adobe en Experience Cloud y [confirmación de su ID de organización](https://experienceleague.adobe.com/docs/core-services/interface/administration/organizations.html#concept_EA8AEE5B02CF46ACBDAD6A8508646255). Este ID está asociado con la empresa de Experience Cloud aprovisionada. Tiene el formato de una cadena alfanumérica de 24 caracteres e incluye un `@AdobeOrg`.
* A continuación, cree o actualice el esquema del Modelo de datos de experiencia (XDM) con los grupos de campos específicos de Commerce. Para ver los pasos detallados sobre cómo agregar grupos de campos específicos de Commerce al esquema XDM, lea la guía sobre [adición de grupos de campos a un esquema XDM](https://experienceleague.adobe.com/docs/commerce-merchant-services/data-connection/fundamentals/update-xdm.html).
* Una vez configurado el esquema, debe crear un conjunto de datos basado en el nuevo esquema. Este conjunto de datos contendrá el [!DNL Commerce] datos que envía. Para ver los pasos detallados sobre cómo crear un conjunto de datos para [!DNL Commerce] datos, lea la guía sobre [envío de datos al Experience Platform](https://experienceleague.adobe.com/docs/platform-learn/implement-mobile-sdk/experience-cloud/platform.html#create-a-dataset).
* A continuación, cree una secuencia de datos y seleccione el esquema XDM que contiene los grupos de campos específicos de Commerce. Para obtener más información sobre las secuencias de datos, lea la [información general sobre flujos de datos](https://experienceleague.adobe.com/docs/experience-platform/datastreams/overview.html?lang=es).
* A continuación, debe conectar la instancia de Adobe Commerce a [Conector de Commerce Services](https://experienceleague.adobe.com/docs/commerce-merchant-services/user-guides/integration-services/saas.html). Esto permite implementar la instancia de Commerce como SaaS (software como servicio).
* Una vez completadas todas las configuraciones mencionadas, ahora puede conectarse a Experience Platform configurando tanto el conector de Commerce Services como el [!DNL Data Connection] Extensión de mediante [!DNL Commerce Admin]. Para obtener más información sobre este paso final, lea la guía de [conexión de datos de Commerce a Experience Platform](https://experienceleague.adobe.com/docs/commerce-merchant-services/data-connection/fundamentals/connect-data.html).
