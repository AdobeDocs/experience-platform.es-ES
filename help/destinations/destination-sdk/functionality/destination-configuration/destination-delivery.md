---
description: Obtenga información sobre cómo configurar los ajustes de entrega de destino para destinos creados con Destination SDK, para indicar a dónde se dirigen los datos exportados y qué regla de autenticación se utiliza en la ubicación a la que llegan los datos.
title: Entrega de destino
source-git-commit: 118ff85a9fceb8ee81dbafe2c381d365b813da29
workflow-type: tm+mt
source-wordcount: '563'
ht-degree: 1%

---


# Entrega de destino

Para ofrecer más control sobre dónde se exportan los datos a las tierras de destino, el Destination SDK permite especificar la configuración de envío de destino.

La sección de entrega de destino indica adónde se dirigen los datos exportados y qué regla de autenticación se utiliza en la ubicación a la que llegan los datos.

<!-- When configuring a destination, you must specify an authentication rule and one or more `destinationServerId` parameters, corresponding to the destination servers that define where the data will be delivered to. In most cases, the authentication rule that you should use is `CUSTOMER_AUTHENTICATION`.  -->

Para comprender dónde encaja este componente en una integración creada con el Destination SDK, consulte el diagrama en la [opciones de configuración](../configuration-options.md) para ver las siguientes páginas de información general sobre la configuración de destino:

* [Usar Destination SDK para configurar un destino de flujo continuo](../../guides/configure-destination-instructions.md#create-destination-configuration)
* [Usar Destination SDK para configurar un destino basado en archivos](../../guides/configure-file-based-destination-instructions.md#create-destination-configuration)

Puede configurar las opciones de envío de destino mediante la variable `/authoring/destinations` punto final. Consulte las siguientes páginas de referencia de API para ver ejemplos detallados de llamadas de API donde puede configurar los componentes que se muestran en esta página.

* [Crear una configuración de destino](../../authoring-api/destination-configuration/create-destination-configuration.md)
* [Actualizar una configuración de destino](../../authoring-api/destination-configuration/update-destination-configuration.md)

Este artículo describe todas las opciones de envío de destino compatibles que puede utilizar para el destino.

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

Al configurar la entrega de destino, puede utilizar los parámetros descritos en la tabla siguiente para definir a dónde se deben enviar los datos exportados.

| Parámetro | Tipo | Descripción |
|---------|----------|------|
| `authenticationRule` | Cadena | Indica cómo [!DNL Platform] debe conectarse a su destino. Valores compatibles:<ul><li>`CUSTOMER_AUTHENTICATION`: Utilice esta opción si los clientes de Platform inician sesión en su sistema mediante cualquiera de los métodos de autenticación descritos [here](customer-authentication.md).</li><li>`PLATFORM_AUTHENTICATION`: Utilice esta opción si hay un sistema de autenticación global entre el Adobe y el destino y el [!DNL Platform] El cliente no necesita proporcionar credenciales de autenticación para conectarse al destino. En este caso, debe crear un objeto credentials utilizando la variable [API de credenciales](../../credentials-api/create-credential-configuration.md) configuración. </li><li>`NONE`: Utilice esta opción si no se requiere autenticación para enviar datos a la plataforma de destino. </li></ul> |
| `destinationServerId` | Cadena | La variable `instanceId` del [servidor de destino](../../authoring-api/destination-server/create-destination-server.md) a la que desea exportar los datos. |
| `deliveryMatchers.type` | Cadena | <ul><li>Al configurar la entrega de destino para destinos basados en archivos, establezca siempre esto como `SOURCE`.</li><li>Al configurar la entrega de destino para un destino de flujo continuo, la variable `deliveryMatchers` no es obligatorio.</li></ul> |
| `deliveryMatchers.value` | Cadena | <ul><li>Al configurar la entrega de destino para destinos basados en archivos, establezca siempre esto como `batch`.</li><li>Al configurar la entrega de destino para un destino de flujo continuo, la variable `deliveryMatchers` no es obligatorio.</li></ul> |

{style="table-layout:auto"}

## Configuración de entrega de destino para destinos de flujo continuo {#destination-delivery-streaming}

El ejemplo siguiente muestra cómo se deben configurar los ajustes de envío de destino para un destino de flujo continuo. Tenga en cuenta que `deliveryMatchers` no es necesaria para los destinos de flujo continuo.

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

## Configuración de entrega de destino para destinos basados en archivos {#destination-delivery-file-based}

El ejemplo siguiente muestra cómo se debe configurar la configuración de envío de destino para un destino basado en archivos. Tenga en cuenta que `deliveryMatchers` para destinos basados en archivos.

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

Después de leer este artículo, debe comprender mejor cómo puede configurar las ubicaciones en las que el destino debe exportar datos, tanto para el flujo continuo como para los destinos basados en archivos.

Para obtener más información sobre los otros componentes de destino, consulte los siguientes artículos:

* [Autenticación del cliente](customer-authentication.md)
* [Autenticación OAuth2](oauth2-authentication.md)
* [Atributos de interfaz de usuario](ui-attributes.md)
* [Campos de datos del cliente](customer-data-fields.md)
* [Configuración del esquema](schema-configuration.md)
* [Configuración del área de nombres de identidad](identity-namespace-configuration.md)
* [Configuraciones de asignación admitidas](supported-mapping-configurations.md)
* [Configuración de metadatos de audiencia](audience-metadata-configuration.md)
* [Política de agregación](aggregation-policy.md)
* [Configuración por lotes](batch-configuration.md)
* [Calificaciones históricas de perfil](historical-profile-qualifications.md)