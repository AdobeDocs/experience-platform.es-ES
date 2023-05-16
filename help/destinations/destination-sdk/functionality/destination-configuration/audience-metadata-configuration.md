---
description: Obtenga información sobre cómo configurar la configuración de metadatos de audiencia para destinos creados con Destination SDK.
title: Configuración de metadatos de audiencia
source-git-commit: 118ff85a9fceb8ee81dbafe2c381d365b813da29
workflow-type: tm+mt
source-wordcount: '406'
ht-degree: 2%

---


# Configuración de metadatos de audiencia

Al exportar datos de un Experience Platform a un destino, es posible que necesite metadatos de audiencia específicos, como nombres de segmento o ID de segmento, para compartirlos entre el Experience Platform y el destino.

Destination SDK ofrece herramientas que puede utilizar para crear, actualizar o eliminar audiencias mediante programación en la plataforma de destino.

Para comprender dónde encaja este componente en una integración creada con el Destination SDK, consulte el diagrama en la [opciones de configuración](../configuration-options.md) o consulte la guía sobre cómo [usar Destination SDK para configurar un destino de flujo continuo](../../guides/configure-destination-instructions.md#create-destination-configuration).

Puede configurar la plantilla de metadatos de audiencia mediante la variable `/authoring/audience-templates` punto final. Después de crear la configuración de metadatos de audiencia, puede usar la variable `/authoring/destinations` para configurar el `audienceMetadataConfig` para obtener más información. Esta sección indica a su destino qué metadatos de segmento debe asignar a su plantilla de audiencia.

Consulte las siguientes páginas de referencia de API para ver ejemplos detallados de llamadas de API donde puede configurar los componentes que se muestran en esta página.

* [Crear una configuración de destino](../../authoring-api/destination-configuration/create-destination-configuration.md)
* [Actualizar una configuración de destino](../../authoring-api/destination-configuration/update-destination-configuration.md)
* [Creación de una plantilla de audiencia](../../metadata-api/create-audience-template.md)
* [Actualizar una plantilla de audiencia](../../metadata-api/update-audience-template.md)

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

Al crear la configuración de metadatos de audiencia, puede utilizar los parámetros descritos en la tabla siguiente para configurar los ajustes de asignación de segmentos.

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
| `mapExperiencePlatformSegmentName` | Booleano | Indica si la variable [[!UICONTROL ID de asignación]](../../../ui/activate-segment-streaming-destinations.md#scheduling) en el flujo de trabajo de activación de destino debe ser el nombre del segmento del Experience Platform. |
| `mapExperiencePlatformSegmentId` | Booleano | Indica si la variable [[!UICONTROL ID de asignación]](../../../ui/activate-segment-streaming-destinations.md#scheduling) en el flujo de trabajo de activación de destino debe ser el ID de segmento del Experience Platform. |
| `mapUserInput` | Booleano | Activa o desactiva la entrada de usuario para la variable [[!UICONTROL ID de asignación]](../../../ui/activate-segment-streaming-destinations.md#scheduling) en el flujo de trabajo de activación de destino. Si está configurado como `true`, `audienceTemplateId` no puede estar presente. |
| `audienceTemplateId` | Booleano | La variable `instanceId` del [plantilla de metadatos de audiencia](../../metadata-api/create-audience-template.md) para su destino. |

{style="table-layout:auto"}

## Pasos siguientes {#next-steps}

Después de leer este artículo, debe comprender mejor cómo puede configurar los metadatos de audiencia para el destino.

Para obtener más información sobre los otros componentes de destino, consulte los siguientes artículos:

* [Configuración de autenticación de cliente](customer-authentication.md)
* [Autenticación OAuth2](oauth2-authentication.md)
* [Campos de datos del cliente](customer-data-fields.md)
* [Atributos de interfaz de usuario](ui-attributes.md)
* [Configuración del esquema](schema-configuration.md)
* [Configuración del área de nombres de identidad](identity-namespace-configuration.md)
* [Configuraciones de asignación admitidas](supported-mapping-configurations.md)
* [Entrega de destino](destination-delivery.md)
* [Política de agregación](aggregation-policy.md)
* [Configuración por lotes](batch-configuration.md)
* [Calificaciones históricas de perfil](historical-profile-qualifications.md)