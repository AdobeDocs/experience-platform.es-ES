---
description: Obtenga información sobre cómo configurar las identidades de destino admitidas para los destinos creados con Destination SDK.
title: Configuración del área de nombres de identidad
exl-id: 30c0939f-b968-43db-b09b-ce5b34349c6e
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '925'
ht-degree: 3%

---

# Configuración del área de nombres de identidad

Experience Platform utiliza áreas de nombres de identidad para describir el tipo de identidades específicas. Por ejemplo, un área de nombres de identidad denominada `Email` identifica un valor como `name@email.com` como dirección de correo electrónico.

Según el tipo de destino que cree (de flujo continuo o basado en archivos), tenga en cuenta los siguientes requisitos del área de nombres de identidad:

* Al crear destinos en tiempo real (streaming) a través de Destination SDK, además de [configurar un esquema de socio](schema-configuration.md) al que los usuarios pueden asignar atributos e identidades de perfil, también debe definir *al menos una* área de nombres de identidad que sea compatible con su plataforma de destino. Por ejemplo, si su plataforma de destino acepta correos electrónicos con hash y [!DNL IDFA], debe definir estas dos identidades como [descritas más adelante en este documento](#supported-parameters).

  >[!IMPORTANT]
  >
  >Al activar audiencias en destinos de flujo continuo, los usuarios también deben asignar _al menos una identidad de destino_, además de los atributos de perfil de destino. De lo contrario, las audiencias no se activarán en la plataforma de destino.

* Al crear destinos basados en archivos mediante Destination SDK, la configuración de las áreas de nombres de identidad es _opcional_.

Para obtener más información sobre áreas de nombres de identidad en Experience Platform, consulte la [documentación de áreas de nombres de identidad](../../../../identity-service/features/namespaces.md).

Al configurar áreas de nombres de identidad para su destino, puede ajustar la asignación de identidad de destino admitida por su destino, como:

* Permite a los usuarios asignar atributos XDM a áreas de nombres de identidad.
* Permite a los usuarios asignar [áreas de nombres de identidad estándar](../../../../identity-service/features/namespaces.md#standard) a sus propias áreas de nombres de identidad.
* Permite que los usuarios asignen [áreas de nombres de identidad personalizadas](../../../../identity-service/features/namespaces.md#manage-namespaces) a sus propias áreas de nombres de identidad.

Para saber dónde encaja este componente en una integración creada con Destination SDK, consulte el diagrama en la documentación de [opciones de configuración](../configuration-options.md) o vea la guía sobre cómo [usar Destination SDK para configurar un destino basado en archivos](../../guides/configure-file-based-destination-instructions.md#create-server-file-configuration).

Puede configurar las áreas de nombres de identidad admitidas a través del extremo `/authoring/destinations`. Consulte las siguientes páginas de referencia de la API para ver ejemplos detallados de llamadas de la API donde puede configurar los componentes que se muestran en esta página.

* [Crear una configuración de destino](../../authoring-api/destination-configuration/create-destination-configuration.md)
* [Actualizar una configuración de destino](../../authoring-api/destination-configuration/update-destination-configuration.md)

Este artículo describe todas las opciones de configuración de áreas de nombres de identidad admitidas que puede utilizar para su destino y muestra lo que los clientes verán en la interfaz de usuario de Experience Platform.

>[!IMPORTANT]
>
>Todos los nombres y valores de parámetro admitidos por Destination SDK distinguen entre mayúsculas y minúsculas **1}.** Para evitar errores de distinción entre mayúsculas y minúsculas, utilice los nombres y valores de los parámetros exactamente como se muestra en la documentación.

## Tipos de integración admitidos {#supported-integration-types}

Consulte la tabla siguiente para obtener detalles sobre qué tipos de integraciones admiten la funcionalidad descrita en esta página.

| Tipo de integración | Admite funcionalidad |
|---|---|
| Integraciones en tiempo real (streaming) | Sí (obligatorio) |
| Integraciones basadas en archivos (por lotes) | Sí (opcional) |

## Parámetros admitidos {#supported-parameters}

Al definir las identidades de destino que admite su destino, puede utilizar los parámetros descritos en la tabla siguiente para configurar su comportamiento.

| Parámetro | Tipo | Obligatorio/Opcional | Descripción |
|---------|----------|---|------|
| `acceptsAttributes` | Booleano | Opcional | Indica si los clientes pueden asignar atributos de perfil estándar a la identidad que está configurando. |
| `acceptsCustomNamespaces` | Booleano | Opcional | Indica si los clientes pueden asignar áreas de nombres de identidad personalizadas al área de nombres de identidad que está configurando. |
| `acceptedGlobalNamespaces` | - | Opcional | Indica qué [áreas de nombres de identidad estándar](../../../../identity-service/features/namespaces.md#standard) (por ejemplo, [!UICONTROL IDFA]) los clientes pueden asignar a la identidad que está configurando. |
| `transformation` | Cadena | Opcional | Muestra la casilla de verificación [[!UICONTROL Aplicar transformación]](../../../ui/activate-segment-streaming-destinations.md#apply-transformation) en la interfaz de usuario de Experience Platform cuando el campo de origen es un atributo XDM o un área de nombres de identidad personalizada. Utilice esta opción para dar a los usuarios la capacidad de hash los atributos de origen en la exportación. Para habilitar esta opción, establezca el valor en `sha256(lower($))`. |
| `requiredTransformation` | Cadena | Opcional | Cuando los clientes seleccionan este área de nombres de identidad de origen, la casilla de verificación [[!UICONTROL Aplicar transformación]](../../../ui/activate-segment-streaming-destinations.md#apply-transformation) se aplica automáticamente a la asignación y los clientes no pueden deshabilitarla. Para habilitar esta opción, establezca el valor en `sha256(lower($))`. |

{style="table-layout:auto"}


```json
"identityNamespaces":{
      "external_id":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true,
         "acceptedGlobalNamespaces":{
            "Email":{
            }
         }
      },
      "another_id":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true
      }
   }
```

Debe indicar qué identidades de [!DNL Experience Platform] pueden exportar los clientes a su destino. Algunos ejemplos son [!DNL Experience Cloud ID], correo electrónico con hash, ID de dispositivo ([!DNL IDFA], [!DNL GAID]). Estos valores son [!DNL Experience Platform] áreas de nombres de identidad que los clientes pueden asignar a áreas de nombres de identidad desde su destino.

Las áreas de nombres de identidad no requieren una correspondencia de 1 a 1 entre [!DNL Experience Platform] y su destino.
Por ejemplo, los clientes podrían asignar un área de nombres [!DNL Experience Platform] [!DNL IDFA] a un área de nombres [!DNL IDFA] desde su destino, o pueden asignar el mismo área de nombres [!DNL Experience Platform] [!DNL IDFA] a un área de nombres [!DNL Customer ID] en su destino.

Obtenga más información sobre identidades en la [descripción general del área de nombres de identidad](../../../../identity-service/features/namespaces.md).

## Consideraciones de asignación

Si los clientes seleccionan un área de nombres de identidad de origen y no seleccionan una asignación de destino, Experience Platform rellena automáticamente la asignación de destino con un atributo con el mismo nombre.

## Configuración del hashing de campos de origen opcional

Los clientes de Experience Platform pueden elegir ingerir datos en Experience Platform en formato hash o en texto sin formato. Si la plataforma de destino acepta datos con hash y sin hash, puede dar a los clientes la opción de elegir si Experience Platform debe tener hash en los valores de los campos de origen cuando se exporten al destino.

La configuración siguiente habilita la opción [Aplicar transformación](../../../ui/activate-segment-streaming-destinations.md#apply-transformation) opcional en la interfaz de usuario de Experience Platform, en el paso Asignación.

```json {line-numbers="true" highlight="5"}
"identityNamespaces":{
      "Customer_contact":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true,
         "transformation": "sha256(lower($))",
         "acceptedGlobalNamespaces":{
            "Email":{
            },
            "Phone":{
            }
         }
      }
   }
```

Marque esta opción cuando utilice campos de origen sin hash, para que Adobe Experience Platform aplique un algoritmo hash en ellos automáticamente en la activación.

Cuando asigne atributos de origen sin hash a atributos de destino que el destino espera que tengan hash (por ejemplo: `email_lc_sha256` o `phone_sha256`), marque la opción **Aplicar transformación** para que Adobe Experience Platform aplique automáticamente hash a los atributos de origen al activarlos.

## Configuración del hashing obligatorio de campos de origen

Si el destino solo acepta datos con hash, puede configurar los atributos exportados para que Experience Platform los aplique automáticamente. La configuración siguiente comprueba automáticamente la opción **Aplicar transformación** cuando se asignan las identidades `Email` y `Phone`.

```json {line-numbers="true" highlight="8,11"}
"identityNamespaces":{
      "Customer_contact":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true,
         "transformation": "sha256(lower($))",
         "acceptedGlobalNamespaces":{
            "Email":{
               "requiredTransformation": "sha256(lower($))"
            },
            "Phone":{
               "requiredTransformation": "sha256(lower($))"
            }
         }
      }
   }
```

## Pasos siguientes {#next-steps}

Después de leer este artículo, debería comprender mejor cómo configurar las áreas de nombres de identidad para los destinos creados con Destination SDK.

Para obtener más información acerca de los demás componentes de destino, consulte los siguientes artículos:

* [Autenticación del cliente](customer-authentication.md)
* [Autorización de OAuth2](oauth2-authorization.md)
* [Campos de datos del cliente](customer-data-fields.md)
* [Atributos de IU](ui-attributes.md)
* [Configuración del esquema](schema-configuration.md)
* [Configuración del área de nombres de identidad](identity-namespace-configuration.md)
* [Configuraciones de asignación compatibles](supported-mapping-configurations.md)
* [Envío de destino](destination-delivery.md)
* [Configuración de metadatos de audiencia](audience-metadata-configuration.md)
* [Política de agregación](aggregation-policy.md)
* [Configuración por lotes](batch-configuration.md)
* [Cualificaciones históricas del perfil](historical-profile-qualifications.md)
