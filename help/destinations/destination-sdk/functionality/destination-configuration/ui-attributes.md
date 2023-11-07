---
description: Obtenga información sobre cómo configurar los atributos de la interfaz de usuario, como el vínculo de documentación, la categoría de la tarjeta de destino, el tipo de conexión de destino y la frecuencia, para los destinos creados con Destination SDK.
title: Atributos de IU
exl-id: aed8d868-c516-45da-b224-c7e99e4bfaf1
source-git-commit: 82ba4e62d5bb29ba4fef22c5add864a556e62c12
workflow-type: tm+mt
source-wordcount: '755'
ht-degree: 0%

---

# Atributos de IU

Los atributos de la interfaz de usuario definen los elementos visuales que debe mostrar el Adobe para la tarjeta de destino en la interfaz de usuario de Adobe Experience Platform, como el logotipo de la plataforma de destino, un vínculo a la página de documentación, una descripción del destino y su categoría y tipo.

Para saber dónde encaja este componente en una integración creada con Destination SDK, consulte el diagrama en la [opciones de configuración](../configuration-options.md) o consulte las siguientes páginas de información general sobre la configuración de destino:

* [Usar Destination SDK para configurar un destino de flujo continuo](../../guides/configure-destination-instructions.md#create-destination-configuration)
* [Usar Destination SDK para configurar un destino basado en archivos](../../guides/configure-file-based-destination-instructions.md#create-destination-configuration)

Cuándo [creación de un destino](../../authoring-api/destination-configuration/create-destination-configuration.md) mediante el Destination SDK, la variable `uiAttributes` define las siguientes propiedades visuales de la tarjeta de destino:

* La dirección URL de la página de documentación de destino en la [catálogo de destino](../../../catalog/overview.md).
* Dirección URL donde alojó el icono que se mostrará en la tarjeta del catálogo de destinos.
* La categoría en la que se mostrará el destino en la interfaz de usuario de Platform.
* Frecuencia de exportación de datos para el destino.
* El tipo de conexión de destino, como Amazon S3, Azure Blob, etc.

Puede configurar los atributos de la interfaz de usuario mediante `/authoring/destinations` punto final. Consulte las siguientes páginas de referencia de la API para ver ejemplos detallados de llamadas de la API donde puede configurar los componentes que se muestran en esta página.

* [Crear una configuración de destino](../../authoring-api/destination-configuration/create-destination-configuration.md)
* [Actualizar una configuración de destino](../../authoring-api/destination-configuration/update-destination-configuration.md)

Este artículo describe todos los atributos de interfaz de usuario admitidos que puede utilizar para el destino y muestra lo que los clientes verán en la interfaz de usuario de Experience Platform.

![Captura de pantalla de la interfaz de usuario que muestra los atributos de la interfaz de Experience Platform](../../assets/functionality/destination-configuration/ui-attributes.png)

>[!IMPORTANT]
>
>Todos los nombres y valores de parámetro admitidos por el Destination SDK son **distingue mayúsculas de minúsculas**. Para evitar errores de distinción entre mayúsculas y minúsculas, utilice los nombres y valores de los parámetros exactamente como se muestra en la documentación.

## Tipos de integración admitidos {#supported-integration-types}

Consulte la tabla siguiente para obtener detalles sobre qué tipos de integraciones admiten la funcionalidad descrita en esta página.

| Tipo de integración | Admite funcionalidad |
|---|---|
| Integraciones en tiempo real (streaming) | Sí |
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

`documentationLink` es un parámetro de cadena que hace referencia a la página de documentación de la [Catálogo de destinos](../../../catalog/overview.md) para su destino. Todos los destinos de producción de Adobe Experience Platform deben tener una página de documentación correspondiente. [Obtenga información sobre cómo crear una página de documentación de destino](../../docs-framework/documentation-instructions.md) para su destino. Tenga en cuenta que esto no es necesario para destinos privados o personalizados.

Utilice el siguiente formato: `http://www.adobe.com/go/destinations-YOURDESTINATION-en`, donde `YOURDESTINATION` es el nombre de su destino. Para un destino llamado Moviestar, debe utilizar `http://www.adobe.com/go/destinations-moviestar-en`.

Los usuarios pueden ver y visitar el vínculo de documentación desde la página del catálogo de destinos en la interfaz de usuario. Deben buscar la tarjeta de destino y seleccionar **[!UICONTROL Más acciones]**, y luego **[!UICONTROL Ver documentación]**, como se muestra en la siguiente imagen.

![Imagen de la IU que muestra la ubicación del vínculo de documentación.](../../assets/functionality/destination-configuration/ui-attributes-doc-link.png)

>[!NOTE]
>
>Este vínculo solo funciona después de que el Adobe active el destino y se publique la documentación.

### `category` {#category}

`category` es un parámetro de cadena que hace referencia a la categoría asignada a su destino en Adobe Experience Platform. Para obtener más información, consulte [Categorías de destino](../../../destination-types.md). Utilice uno de los siguientes valores: `adobeSolutions, advertising, analytics, cdp, cloudStorage, crm, customerSuccess, database, dmp, ecommerce, email, emailMarketing, enrichment, livechat, marketingAutomation, mobile, personalization, protocols, social, streaming, subscriptions, surveys, tagManagers, voc, warehouses, payments`.

Los usuarios pueden ver la lista de categorías de destino en la parte izquierda de la pantalla del catálogo de destino, como se muestra en la siguiente imagen.

![Imagen de la interfaz de usuario que muestra la ubicación de la categoría de destino.](../../assets/functionality/destination-configuration/ui-attributes-category.png)

<!-- ### `iconUrl` {#icon-url}

`iconUrl` is a string parameter that refers to the URL where you hosted the icon to be displayed in the destinations catalog card. For private custom integrations, this is not required. For productized configurations, you need to share an icon with the Adobe team when you [submit the destination for review](../../guides/submit-destination.md#logo).

Users can see the icon on your destination card, as shown in the image below.

![UI image showing the icon location.](../../assets/functionality/destination-configuration/ui-attributes-icon.png) -->

### `connectionType` {#connection-type}

`connectionType` es un parámetro de cadena que hace referencia al tipo de conexión, según el destino. Valores compatibles: <ul><li>`Server-to-server`</li><li>`Cloud storage`</li><li>`Azure Blob`</li><li>`Azure Data Lake Storage`</li><li>`S3`</li><li>`SFTP`</li><li>`DLZ`</li></ul>

Los usuarios pueden ver el tipo de conexión de destino en la [Examinar](../../../ui/destinations-workspace.md#browse) de la pestaña destinos de workspace.

![Imagen de la IU que muestra la ubicación del tipo de conexión en la IU.](../../assets/functionality/destination-configuration/ui-attributes-connection.png)

### `frequency` {#frequency}

`frequency` es un parámetro de cadena que hace referencia al tipo de exportación de datos admitido por el destino. Configure como. `Streaming` para integraciones basadas en API, o `Batch` al exportar archivos a sus destinos.

Los usuarios pueden ver el tipo de frecuencia en la **[!UICONTROL Ejecuciones de flujo de datos]** de cada conexión de destino.

![Imagen de la IU que muestra la ubicación del tipo de frecuencia en la IU.](../../assets/functionality/destination-configuration/ui-attributes-frequency.png)

### `isBeta` {#isbeta}

Si el destino que está creando con Destination SDK estará disponible para un número limitado de clientes, es posible que desee marcar la tarjeta de destino del catálogo de destino como beta.

Para ello, puede utilizar el complemento `isBeta: "true"` en la sección Atributos de interfaz de usuario de la configuración de destino para marcar correctamente la tarjeta de destino.

![Imagen de la interfaz de usuario que muestra una tarjeta de destino marcada como beta.](../../assets/functionality/destination-configuration/ui-attributes-isbeta.png)

## Pasos siguientes {#next-steps}

Después de leer este artículo, debería comprender mejor qué atributos de la interfaz de usuario puede configurar para su destino y dónde los verán los usuarios en la interfaz de usuario de Platform.

Para obtener más información acerca de los demás componentes de destino, consulte los siguientes artículos:

* [Autenticación del cliente](customer-authentication.md)
* [Autorización de OAuth2](oauth2-authorization.md)
* [Campos de datos del cliente](customer-data-fields.md)
* [Configuración del esquema](schema-configuration.md)
* [Configuración del área de nombres de identidad](identity-namespace-configuration.md)
* [Envío de destino](destination-delivery.md)
* [Configuración de metadatos de audiencia](audience-metadata-configuration.md)
* [Política de agregación](aggregation-policy.md)
* [Configuración por lotes](batch-configuration.md)
* [Cualificaciones históricas del perfil](historical-profile-qualifications.md)
