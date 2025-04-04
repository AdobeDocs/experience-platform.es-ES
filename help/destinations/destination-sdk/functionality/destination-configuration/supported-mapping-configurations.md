---
description: Obtenga información sobre cómo configurar el destino para las configuraciones de asignación de atributos e identidad admitidas.
title: Configuraciones de asignación compatibles
exl-id: a477a3f2-a229-4b22-8588-ee58bd5436c6
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '670'
ht-degree: 3%

---

# Configuraciones de asignación compatibles

Los destinos creados con Destination SDK admiten configuraciones específicas de área de nombres de identidad y asignación de atributos, en función del tipo de destino.

Este artículo describe todas las configuraciones de asignación admitidas que puede utilizar al configurar el destino.

>[!WARNING]
>
>Destination SDK no admite ninguna configuración de asignación que no se describa en este artículo.

Al crear el destino, configure el esquema y las áreas de nombres de identidad según una de las configuraciones de asignación descritas en esta página.

>[!IMPORTANT]
>
>Todos los nombres y valores de parámetro admitidos por Destination SDK distinguen entre mayúsculas y minúsculas **1}.** Para evitar errores de distinción entre mayúsculas y minúsculas, utilice los nombres y valores de los parámetros exactamente como se muestra en la documentación.

## Asignaciones compatibles con destinos de flujo continuo {#streaming-mappings}

Los destinos en tiempo real (streaming) creados con Destination SDK admiten las configuraciones de asignación que se describen en la tabla siguiente.

| Campo de origen | Campo de destino |
| --- | --- |
| Atributo XDM | Atributo personalizado |
| Área de nombres de identidad | Área de nombres de identidad |

El ejemplo de configuración siguiente permite a los clientes utilizar ambas asignaciones en la tabla anterior.

```json
"schemaConfig":{
   "profileRequired":true,
   "segmentRequired":true,
   "identityRequired":true
},
"identityNamespaces":{
   "Customer_contact":{
      "acceptsAttributes":false,
      "acceptsCustomNamespaces":true,
      "acceptedGlobalNamespaces":{
         "Email":{
            
         },
         "Phone":{
            
         }
      }
   }
},
```

### Asignar atributos XDM a atributos personalizados {#streaming-xdm-to-custom}

Los usuarios pueden asignar atributos de su perfil XDM de origen a atributos personalizados del lado del destino.

Los usuarios deben introducir manualmente el nombre del atributo personalizado de destino al seleccionar la asignación del campo de destino.

![Captura de pantalla de la IU de Experience Platform que muestra la selección personalizada de atributos.](../../assets/functionality/destination-configuration/mapping-streaming-select-custom-attribute.png)

La experiencia de IU resultante se muestra en la siguiente imagen.

![Captura de pantalla de la IU de Experience Platform que muestra la asignación de atributos XDM a atributos personalizados para destinos de streaming.](../../assets/functionality/destination-configuration/mapping-streaming-xdm-custom.png)

### Asignar áreas de nombres de identidad a áreas de nombres de identidad de socio {#streaming-identity-to-identity}

Los usuarios pueden asignar áreas de nombres de identidad personalizadas o globales desde Experience Platform a las áreas de nombres de identidad que haya definido.

La experiencia de IU resultante se muestra en la siguiente imagen.

![Captura de pantalla de la interfaz de usuario de Experience Platform que muestra la asignación de identidad a destinos de streaming.](../../assets/functionality/destination-configuration/mapping-streaming-identity-identity.png)

## Asignaciones compatibles con destinos basados en archivos {#batch-mappings}

Los destinos basados en archivos creados con Destination SDK admiten las configuraciones de asignación que se describen en la tabla siguiente. Consulte las secciones siguientes para ver ejemplos de asignación detallados.

| Campo de origen | Campo de destino |
| --- | --- |
| Atributo XDM | Atributo / Atributo personalizado |
| Área de nombres de identidad | Atributo / Atributo personalizado |
| Área de nombres de identidad | Área de nombres de identidad |

El ejemplo de configuración siguiente permite a los clientes utilizar todas las asignaciones de la tabla anterior.

```json
"schemaConfig":{
   "profileRequired":true,
   "segmentRequired":true,
   "identityRequired":true
},
"identityNamespaces":{
   "Customer_contact":{
      "acceptsAttributes":false,
      "acceptsCustomNamespaces":true,
      "acceptedGlobalNamespaces":{
         "Email":{
         },
         "Phone":{
         }
      }
   }
},
```

### Asignar atributos XDM a atributos personalizados {#batch-xdm-to-custom}

Los usuarios pueden asignar atributos de su perfil XDM de origen a atributos personalizados del lado del destino.

Para los destinos basados en archivos, el campo de destino se rellena automáticamente con un atributo predeterminado del mismo nombre que el campo de origen.

La experiencia de IU resultante se muestra en la siguiente imagen.

![Captura de pantalla de la interfaz de usuario de Experience Platform que muestra la asignación XDM a atributos personalizados para destinos basados en archivos.](../../assets/functionality/destination-configuration/mapping-batch-xdm-custom.png)

Los usuarios pueden dejar el nombre predeterminado en su lugar o introducir un nombre de atributo personalizado en la pantalla de selección del campo de destino.

![Captura de pantalla de la interfaz de usuario de Experience Platform que muestra la selección personalizada de atributos de destino para destinos basados en archivos.](../../assets/functionality/destination-configuration/mapping-batch-custom-attribute.png)

### Asignar áreas de nombres de identidad a atributos personalizados {#batch-identity-to-custom}

Los usuarios pueden asignar áreas de nombres de identidad personalizadas o globales desde Experience Platform a atributos personalizados del lado del destino.

Al seleccionar un área de nombres de identidad como campo de origen, el campo de destino se rellena automáticamente con un área de nombres de identidad equivalente. Para reemplazar el campo de destino con un atributo personalizado, los usuarios deben introducir un nombre de atributo personalizado en la pantalla de selección de campo de destino.

![Captura de pantalla de la interfaz de usuario de Experience Platform que muestra la selección personalizada de atributos de destino para destinos basados en archivos.](../../assets/functionality/destination-configuration/mapping-batch-custom-attribute.png)

La experiencia de IU resultante se muestra en la siguiente imagen.

![Captura de pantalla de la interfaz de usuario de Experience Platform que muestra la asignación de identidades a atributos personalizados para destinos basados en archivos.](../../assets/functionality/destination-configuration/mapping-batch-identity-custom.png)

### Asignar áreas de nombres de identidad a áreas de nombres de identidad de socio {#batch-identity-to-identity}

Los usuarios pueden asignar áreas de nombres de identidad personalizadas o globales desde Experience Platform a áreas de nombres de identidad equivalentes.

Al seleccionar un área de nombres de identidad como campo de origen, el campo de destino se rellena automáticamente con un área de nombres de identidad equivalente.

La experiencia de IU resultante se muestra en la siguiente imagen.

![Captura de pantalla de la interfaz de usuario de Experience Platform que muestra la asignación de identidad a destinos basados en archivos.](../../assets/functionality/destination-configuration/mapping-batch-identity-identity.png)


## Pasos siguientes {#next-steps}

Después de leer este artículo, debería comprender mejor qué asignaciones son compatibles con los destinos creados con Destination SDK.

Para obtener más información acerca de los demás componentes de destino, consulte los siguientes artículos:

* [Autenticación del cliente](customer-authentication.md)
* [Autorización de OAuth2](oauth2-authorization.md)
* [Campos de datos del cliente](customer-data-fields.md)
* [Atributos de IU](ui-attributes.md)
* [Configuración del esquema](schema-configuration.md)
* [Configuración del área de nombres de identidad](identity-namespace-configuration.md)
* [Envío de destino](destination-delivery.md)
* [Configuración de metadatos de audiencia](audience-metadata-configuration.md)
* [Política de agregación](aggregation-policy.md)
* [Configuración por lotes](batch-configuration.md)
* [Cualificaciones históricas del perfil](historical-profile-qualifications.md)
