---
description: Obtenga información sobre cómo configurar los atributos de la interfaz de usuario, como el vínculo de documentación, la categoría de tarjeta de destino y el tipo y la frecuencia de conexión de destino, para los destinos creados con el Destination SDK.
title: Atributos de interfaz de usuario
source-git-commit: 118ff85a9fceb8ee81dbafe2c381d365b813da29
workflow-type: tm+mt
source-wordcount: '755'
ht-degree: 0%

---


# Atributos de interfaz de usuario

Los atributos de interfaz de usuario definen los elementos visuales que el Adobe debe mostrar para la tarjeta de destino en la interfaz de usuario de Adobe Experience Platform, como el logotipo de la plataforma de destino, un vínculo a la página de documentación, una descripción de destino y su categoría y tipo.

Para comprender dónde encaja este componente en una integración creada con el Destination SDK, consulte el diagrama en la [opciones de configuración](../configuration-options.md) para ver las siguientes páginas de información general sobre la configuración de destino:

* [Usar Destination SDK para configurar un destino de flujo continuo](../../guides/configure-destination-instructions.md#create-destination-configuration)
* [Usar Destination SDK para configurar un destino basado en archivos](../../guides/configure-file-based-destination-instructions.md#create-destination-configuration)

When [creación de un destino](../../authoring-api/destination-configuration/create-destination-configuration.md) mediante el Destination SDK, la variable `uiAttributes` define las siguientes propiedades visuales de la tarjeta de destino:

* La dirección URL de la página de documentación de destino en la variable [catálogo de destino](../../../catalog/overview.md).
* Dirección URL donde alojó el icono para que se muestre en la tarjeta de catálogo de destinos.
* La categoría en la que el destino será visible en la interfaz de usuario de Platform.
* Frecuencia de exportación de datos para el destino.
* El tipo de conexión de destino, como Amazon S3, Azure Blob, etc.

Puede configurar los atributos de la interfaz de usuario a través del `/authoring/destinations` punto final. Consulte las siguientes páginas de referencia de API para ver ejemplos detallados de llamadas de API donde puede configurar los componentes que se muestran en esta página.

* [Crear una configuración de destino](../../authoring-api/destination-configuration/create-destination-configuration.md)
* [Actualizar una configuración de destino](../../authoring-api/destination-configuration/update-destination-configuration.md)

En este artículo se describen todos los atributos de interfaz de usuario admitidos que puede utilizar para el destino y se muestra lo que verán los clientes en la interfaz de usuario del Experience Platform.

![Captura de pantalla de la interfaz de usuario que muestra los atributos de la interfaz de usuario en la interfaz de Experience Platform](../../assets/functionality/destination-configuration/ui-attributes.png)

>[!IMPORTANT]
>
>Todos los nombres y valores de parámetro admitidos por el Destination SDK son **con distinción de mayúsculas y minúsculas**. Para evitar errores de distinción entre mayúsculas y minúsculas, utilice los parámetros nombres y valores exactamente como se muestra en la documentación.

## Tipos de integración compatibles {#supported-integration-types}

Consulte la siguiente tabla para obtener más información sobre los tipos de integraciones que admiten la funcionalidad descrita en esta página.

| Tipo de integración | Admite funcionalidad |
|---|---|
| Integraciones en tiempo real (flujo continuo) | Sí |
| Integraciones basadas en archivos (por lotes) | Sí |

## Parámetros admitidos {#supported-parameters}

```json
"uiAttributes":{
      "documentationLink":"http://www.adobe.com/go/YOURDESTINATION-en",
      "category":"cloudStorage",
      "connectionType":"S3",
      "frequency":"batch",
      "isBeta":"true"
   }
```

### `documentationLink` {#documentation-link}

`documentationLink` es un parámetro de cadena que hace referencia a la página de documentación en la variable [Catálogo de destinos](../../../catalog/overview.md) para su destino. Todos los destinos de productos en Adobe Experience Platform deben tener una página de documentación correspondiente. [Obtenga información sobre cómo crear una página de documentación de destino](../../docs-framework/documentation-instructions.md) para su destino. Tenga en cuenta que esto no es necesario para destinos privados/personalizados.

Utilice el siguiente formato: `http://www.adobe.com/go/destinations-YOURDESTINATION-en`, donde `YOURDESTINATION` es el nombre de su destino. Para un destino llamado Moviestar, debe usar `http://www.adobe.com/go/destinations-moviestar-en`.

Los usuarios pueden ver y visitar el vínculo de documentación desde la página del catálogo de destinos en la interfaz de usuario. Deben buscar la tarjeta de destino y seleccionar **[!UICONTROL Más acciones]** y luego **[!UICONTROL Ver documentación]**, como se muestra en la imagen siguiente.

![La imagen de la interfaz de usuario muestra la ubicación del vínculo de documentación.](../../assets/functionality/destination-configuration/ui-attributes-doc-link.png)

>[!NOTE]
>
>Este vínculo solo funciona después de que el Adobe establezca el destino en vivo y la documentación se publique.

### `category` {#category}

`category` es un parámetro de cadena que hace referencia a la categoría asignada al destino en Adobe Experience Platform. Para obtener más información, lea [Categorías de destino](../../../destination-types.md). Utilice uno de los siguientes valores: `adobeSolutions, advertising, analytics, cdp, cloudStorage, crm, customerSuccess, database, dmp, ecommerce, email, emailMarketing, enrichment, livechat, marketingAutomation, mobile, personalization, protocols, social, streaming, subscriptions, surveys, tagManagers, voc, warehouses, payments`.

Los usuarios pueden ver la lista de categorías de destino en la parte izquierda de la pantalla en el catálogo de destino, como se muestra en la imagen siguiente.

![La imagen de la interfaz de usuario muestra la ubicación de la categoría de destino.](../../assets/functionality/destination-configuration/ui-attributes-category.png)

<!-- ### `iconUrl` {#icon-url}

`iconUrl` is a string parameter that refers to the URL where you hosted the icon to be displayed in the destinations catalog card. For private custom integrations, this is not required. For productized configurations, you need to share an icon with the Adobe team when you [submit the destination for review](../../guides/submit-destination.md#logo).

Users can see the icon on your destination card, as shown in the image below.

![UI image showing the icon location.](../../assets/functionality/destination-configuration/ui-attributes-icon.png) -->

### `connectionType` {#connection-type}

`connectionType` es un parámetro de cadena que hace referencia al tipo de conexión, según el destino. Valores compatibles: <ul><li>`Server-to-server`</li><li>`Cloud storage`</li><li>`Azure Blob`</li><li>`Azure Data Lake Storage`</li><li>`S3`</li><li>`SFTP`</li><li>`DLZ`</li></ul>

Los usuarios pueden ver el tipo de conexión de destino en el [Examinar](../../../ui/destinations-workspace.md#browse) del espacio de trabajo de destinos.

![La imagen de la interfaz de usuario muestra la ubicación del tipo de conexión en la interfaz de usuario.](../../assets/functionality/destination-configuration/ui-attributes-connection.png)

### `frequency` {#frequency}

`frequency` es un parámetro de cadena que hace referencia al tipo de exportación de datos admitido por el destino. Establecer como `Streaming` para integraciones basadas en API, o `Batch` al exportar archivos a sus destinos.

Los usuarios pueden ver el tipo de frecuencia en la **[!UICONTROL Ejecuciones de flujo de datos]** de cada conexión de destino.

![La imagen de la interfaz de usuario muestra la ubicación del tipo de frecuencia en la interfaz de usuario.](../../assets/functionality/destination-configuration/ui-attributes-frequency.png)

### `isBeta` {#isbeta}

Si el destino que está creando con Destination SDK estará disponible para un número limitado de clientes, es posible que desee marcar la tarjeta de destino del catálogo de destino como beta.

Para ello, puede usar la variable `isBeta: "true"` en la sección de atributos de la interfaz de usuario de la configuración de destino para marcar la tarjeta de destino correctamente.

![La imagen de la interfaz de usuario muestra una tarjeta de destino marcada como beta.](../../assets/functionality/destination-configuration/ui-attributes-isbeta.png)

## Pasos siguientes {#next-steps}

Después de leer este artículo, debe comprender mejor qué atributos de interfaz de usuario puede configurar para su destino y dónde los verán los usuarios en la interfaz de usuario de Platform.

Para obtener más información sobre los otros componentes de destino, consulte los siguientes artículos:

* [Autenticación del cliente](customer-authentication.md)
* [Autenticación OAuth2](oauth2-authentication.md)
* [Campos de datos del cliente](customer-data-fields.md)
* [Configuración del esquema](schema-configuration.md)
* [Configuración del área de nombres de identidad](identity-namespace-configuration.md)
* [Entrega de destino](destination-delivery.md)
* [Configuración de metadatos de audiencia](audience-metadata-configuration.md)
* [Política de agregación](aggregation-policy.md)
* [Configuración por lotes](batch-configuration.md)
* [Calificaciones históricas de perfil](historical-profile-qualifications.md)