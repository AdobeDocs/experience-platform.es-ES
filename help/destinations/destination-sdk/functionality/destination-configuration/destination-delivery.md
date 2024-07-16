---
description: Obtenga información sobre cómo ajustar la configuración de entrega de destino para los destinos creados con Destination SDK, para indicar a dónde van los datos exportados y qué regla de autenticación se utiliza en la ubicación a la que aterrizarán los datos.
title: Envío de destino
exl-id: ade77b6b-4b62-4b17-a155-ef90a723a4ad
source-git-commit: 82ba4e62d5bb29ba4fef22c5add864a556e62c12
workflow-type: tm+mt
source-wordcount: '563'
ht-degree: 2%

---

# Envío de destino

Para ofrecer más control sobre dónde llegan los datos exportados a su destino, Destination SDK le permite especificar la configuración de envío de destino.

La sección de entrega de destino indica a dónde van los datos exportados y qué regla de autenticación se utiliza en la ubicación donde aterrizarán los datos.

<!-- When configuring a destination, you must specify an authentication rule and one or more `destinationServerId` parameters, corresponding to the destination servers that define where the data will be delivered to. In most cases, the authentication rule that you should use is `CUSTOMER_AUTHENTICATION`.  -->

Para saber dónde encaja este componente en una integración creada con Destination SDK, consulte el diagrama en la documentación de [opciones de configuración](../configuration-options.md) o consulte las siguientes páginas de información general sobre la configuración de destino:

* [Usar Destination SDK para configurar un destino de flujo continuo](../../guides/configure-destination-instructions.md#create-destination-configuration)
* [Usar Destination SDK para configurar un destino basado en archivos](../../guides/configure-file-based-destination-instructions.md#create-destination-configuration)

Puede configurar las opciones de entrega de destino a través del extremo `/authoring/destinations`. Consulte las siguientes páginas de referencia de la API para ver ejemplos detallados de llamadas de la API donde puede configurar los componentes que se muestran en esta página.

* [Crear una configuración de destino](../../authoring-api/destination-configuration/create-destination-configuration.md)
* [Actualizar una configuración de destino](../../authoring-api/destination-configuration/update-destination-configuration.md)

Este artículo describe todas las opciones de envío de destino admitidas que puede utilizar para su destino.

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

Al configurar la entrega de destino, puede utilizar los parámetros descritos en la tabla siguiente para definir dónde se deben enviar los datos exportados.

| Parámetro | Tipo | Descripción |
|---------|----------|------|
| `authenticationRule` | Cadena | Indica cómo debe conectarse [!DNL Platform] a su destino. Valores compatibles:<ul><li>`CUSTOMER_AUTHENTICATION`: utilice esta opción si los clientes de Platform inician sesión en el sistema mediante cualquiera de los métodos de autenticación descritos [aquí](customer-authentication.md).</li><li>`PLATFORM_AUTHENTICATION`: utilice esta opción si existe un sistema de autenticación global entre el Adobe y el destino y el cliente [!DNL Platform] no necesita proporcionar credenciales de autenticación para conectarse al destino. En este caso, debe crear un objeto de credenciales con la configuración de la API [credentials](../../credentials-api/create-credential-configuration.md). </li><li>`NONE`: utilice esta opción si no se requiere autenticación para enviar datos a la plataforma de destino. </li></ul> |
| `destinationServerId` | Cadena | `instanceId` del [servidor de destino](../../authoring-api/destination-server/create-destination-server.md) al que desea exportar los datos. |
| `deliveryMatchers.type` | Cadena | <ul><li>Al configurar la entrega de destino para destinos basados en archivos, establezca siempre `SOURCE`.</li><li>Al configurar la entrega de destino para un destino de flujo continuo, no es necesaria la sección `deliveryMatchers`.</li></ul> |
| `deliveryMatchers.value` | Cadena | <ul><li>Al configurar la entrega de destino para destinos basados en archivos, establezca siempre `batch`.</li><li>Al configurar la entrega de destino para un destino de flujo continuo, no es necesaria la sección `deliveryMatchers`.</li></ul> |

{style="table-layout:auto"}

## Configuración de envío de destino para destinos de flujo continuo {#destination-delivery-streaming}

El ejemplo siguiente muestra cómo se debe configurar la configuración de entrega de destino para un destino de flujo continuo. Tenga en cuenta que la sección `deliveryMatchers` no es necesaria para los destinos de flujo continuo.

>[!BEGINSHADEBOX]

```json
{
   "destinationDelivery":[
      {
         "authenticationRule":"CUSTOMER_AUTHENTICATION",
         "destinationServerId":"{{destinationServerId}}"
      }
   ]
}
```

>[!ENDSHADEBOX]

## Configuración de envío de destino para destinos basados en archivos {#destination-delivery-file-based}

El ejemplo siguiente muestra cómo se debe configurar la entrega de destino para un destino basado en archivos. Tenga en cuenta que la sección `deliveryMatchers` es necesaria para los destinos basados en archivos.

>[!BEGINSHADEBOX]

```json
{
   "destinationDelivery":[
      {
         "deliveryMatchers":[
            {
               "type":"SOURCE",
               "value":[
                  "batch"
               ]
            }
         ],
         "authenticationRule":"CUSTOMER_AUTHENTICATION",
         "destinationServerId":"{{destinationServerId}}"
      }
   ]
}
```

>[!ENDSHADEBOX]

## Pasos siguientes {#next-steps}

Después de leer este artículo, debería comprender mejor cómo puede configurar las ubicaciones en las que el destino debe exportar los datos, tanto para los destinos de flujo continuo como basados en archivos.

Para obtener más información acerca de los demás componentes de destino, consulte los siguientes artículos:

* [Autenticación del cliente](customer-authentication.md)
* [Autorización de OAuth2](oauth2-authorization.md)
* [Atributos de IU](ui-attributes.md)
* [Campos de datos del cliente](customer-data-fields.md)
* [Configuración del esquema](schema-configuration.md)
* [Configuración del área de nombres de identidad](identity-namespace-configuration.md)
* [Configuraciones de asignación compatibles](supported-mapping-configurations.md)
* [Configuración de metadatos de audiencia](audience-metadata-configuration.md)
* [Política de agregación](aggregation-policy.md)
* [Configuración por lotes](batch-configuration.md)
* [Cualificaciones históricas del perfil](historical-profile-qualifications.md)
