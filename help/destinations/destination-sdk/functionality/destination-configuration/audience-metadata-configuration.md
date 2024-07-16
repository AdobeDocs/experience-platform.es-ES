---
description: Aprenda a configurar los metadatos de audiencia para los destinos creados con Destination SDK.
title: Configuración de metadatos de audiencia
exl-id: ae71df4f-b753-4084-835f-03559b4986cb
source-git-commit: 20cb2dbfbfc8e73c765073818c8e7e561d4e6629
workflow-type: tm+mt
source-wordcount: '405'
ht-degree: 3%

---

# Configuración de metadatos de audiencia

Al exportar datos de Experience Platform a su destino, es posible que necesite metadatos de audiencia específicos, como nombres de audiencias o ID de audiencia, para compartirlos entre Experience Platform y su destino.

Destination SDK ofrece herramientas que puede utilizar para crear, actualizar o eliminar audiencias en la plataforma de destino mediante programación.

Para saber dónde encaja este componente en una integración creada con Destination SDK, consulte el diagrama en la documentación de [opciones de configuración](../configuration-options.md) o consulte la guía sobre cómo [usar Destination SDK para configurar un  de flujo continuo](../../guides/configure-destination-instructions.md#create-destination-configuration).

Puede configurar la plantilla de metadatos de audiencia mediante el extremo `/authoring/audience-templates`. Después de crear la configuración de metadatos de audiencia, puede usar el extremo `/authoring/destinations` para configurar la sección `audienceMetadataConfig`. Esta sección indica a su destino qué metadatos de audiencia debe asignar a su plantilla de audiencia.

Consulte las siguientes páginas de referencia de la API para ver ejemplos detallados de llamadas de la API donde puede configurar los componentes que se muestran en esta página.

* [Crear una configuración de destino](../../authoring-api/destination-configuration/create-destination-configuration.md)
* [Actualizar una configuración de destino](../../authoring-api/destination-configuration/update-destination-configuration.md)
* [Creación de una plantilla de audiencia](../../metadata-api/create-audience-template.md)
* [Actualización de una plantilla de audiencia](../../metadata-api/update-audience-template.md)

>[!IMPORTANT]
>
>Todos los nombres y valores de parámetro admitidos por el Destination SDK distinguen entre mayúsculas y minúsculas **1}.** Para evitar errores de distinción entre mayúsculas y minúsculas, utilice los nombres y valores de los parámetros exactamente como se muestra en la documentación.

## Tipos de integración admitidos {#supported-integration-types}

Consulte la tabla siguiente para obtener detalles sobre qué tipos de integraciones admiten la funcionalidad descrita en esta página.

| Tipo de integración | Admite funcionalidad |
|---|---|
| Integraciones en tiempo real (streaming) | Sí |
| Integraciones basadas en archivos (por lotes) | Sí |

## Parámetros admitidos {#supported-parameters}

Al crear la configuración de metadatos de audiencia, puede utilizar los parámetros descritos en la tabla siguiente para configurar las opciones de asignación de audiencia.

```json
  "audienceMetadataConfig":{
   "mapExperiencePlatformSegmentName":false,
   "mapExperiencePlatformSegmentId":false,
   "mapUserInput":false,
   "audienceTemplateId":"YOUR_AUDIENCE_TEMPLATE_ID"
}
```

| Parámetro | Tipo | Descripción |
|---------|----------|------|
| `mapExperiencePlatformSegmentName` | Booleano | Indica si el valor de [[!UICONTROL ID de asignación]](../../../ui/activate-segment-streaming-destinations.md#scheduling) en el flujo de trabajo de activación de destino debe ser el nombre de audiencia del Experience Platform. |
| `mapExperiencePlatformSegmentId` | Booleano | Indica si el valor de [[!UICONTROL ID de asignación]](../../../ui/activate-segment-streaming-destinations.md#scheduling) en el flujo de trabajo de activación de destino debe ser el ID de audiencia del Experience Platform. |
| `mapUserInput` | Booleano | Habilita o deshabilita la entrada del usuario para el valor [[!UICONTROL Id. de asignación]](../../../ui/activate-segment-streaming-destinations.md#scheduling) en el flujo de trabajo de activación de destino. Si se establece en `true`, `audienceTemplateId` no puede estar presente. |
| `audienceTemplateId` | Cadena | `instanceId` de [plantilla de metadatos de audiencia](../../metadata-api/create-audience-template.md) utilizada para su destino. |

{style="table-layout:auto"}

## Pasos siguientes {#next-steps}

Después de leer este artículo, debería comprender mejor cómo puede configurar los metadatos de audiencia para su destino.

Para obtener más información acerca de los demás componentes de destino, consulte los siguientes artículos:

* [Configuración de autenticación del cliente](customer-authentication.md)
* [Autorización de OAuth2](oauth2-authorization.md)
* [Campos de datos del cliente](customer-data-fields.md)
* [Atributos de IU](ui-attributes.md)
* [Configuración del esquema](schema-configuration.md)
* [Configuración del área de nombres de identidad](identity-namespace-configuration.md)
* [Configuraciones de asignación compatibles](supported-mapping-configurations.md)
* [Envío de destino](destination-delivery.md)
* [Política de agregación](aggregation-policy.md)
* [Configuración por lotes](batch-configuration.md)
* [Cualificaciones históricas del perfil](historical-profile-qualifications.md)
