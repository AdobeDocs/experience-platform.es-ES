---
description: Obtenga información sobre cómo configurar el esquema de socio para los destinos creados con Destination SDK.
title: Configuración de esquema de socio
source-git-commit: acb7075f49b4194c31371d2de63709eea7821329
workflow-type: tm+mt
source-wordcount: '1715'
ht-degree: 5%

---


# Configuración de esquema de socio

Experience Platform utiliza esquemas para describir la estructura de los datos de una manera uniforme y reutilizable. Cuando los datos se incorporan en Platform, se estructuran según un esquema XDM. Para obtener más información sobre el modelo de composición del esquema, incluidos los principios de diseño y las prácticas recomendadas, consulte la [conceptos básicos de la composición del esquema](../../../../xdm/schema/composition.md).

Al crear un destino con Destination SDK, puede definir su propio esquema de socio para utilizarlo en la plataforma de destino. Esto permite a los usuarios asignar atributos de perfil de Platform a campos específicos que reconoce su plataforma de destino, todos dentro de la interfaz de usuario de Platform.

Al configurar el esquema del socio para el destino, puede ajustar la asignación de campos admitida por la plataforma de destino, como:

* Permitir que los usuarios asignen un `phoneNumber` Atributo XDM a un `phone` admitido por la plataforma de destino.
* Cree esquemas de socios dinámicos a los que el Experience Platform pueda llamar dinámicamente para recuperar una lista de todos los atributos admitidos dentro del destino.
* Defina asignaciones de campo obligatorias que requiera la plataforma de destino.

Para comprender dónde encaja este componente en una integración creada con el Destination SDK, consulte el diagrama en la [opciones de configuración](../configuration-options.md) o consulte la guía sobre cómo [usar Destination SDK para configurar un destino basado en archivos](../../guides/configure-file-based-destination-instructions.md#create-server-file-configuration).

Puede configurar la configuración del esquema mediante la variable `/authoring/destinations` punto final. Consulte las siguientes páginas de referencia de API para ver ejemplos detallados de llamadas de API donde puede configurar los componentes que se muestran en esta página.

* [Crear una configuración de destino](../../authoring-api/destination-configuration/create-destination-configuration.md)
* [Actualizar una configuración de destino](../../authoring-api/destination-configuration/update-destination-configuration.md)

Este artículo describe todas las opciones de configuración de esquema compatibles que puede utilizar para el destino y muestra lo que verán los clientes en la interfaz de usuario de Platform.

>[!IMPORTANT]
>
>Todos los nombres y valores de parámetro admitidos por el Destination SDK son **con distinción de mayúsculas y minúsculas**. Para evitar errores de distinción entre mayúsculas y minúsculas, utilice los parámetros nombres y valores exactamente como se muestra en la documentación.

## Tipos de integración compatibles {#supported-integration-types}

Consulte la siguiente tabla para obtener más información sobre los tipos de integraciones que admiten la funcionalidad descrita en esta página.

| Tipo de integración | Admite funcionalidad |
|---|---|
| Integraciones en tiempo real (flujo continuo) | Sí |
| Integraciones basadas en archivos (por lotes) | Sí |

## Configuración de esquema admitida {#supported-schema-types}

Destination SDK admite varias configuraciones de esquema:

* Los esquemas estáticos se definen mediante la variable `profileFields` en el `schemaConfig` para obtener más información. En un esquema estático, se definen todos los atributos de destino que deben mostrarse en la interfaz de usuario del Experience Platform en la variable `profileFields` matriz. Si necesita actualizar el esquema, debe [actualizar la configuración de destino](../../authoring-api/destination-configuration/update-destination-configuration.md).
* Los esquemas dinámicos utilizan un tipo de servidor de destino adicional, denominado [servidor de esquema dinámico](../../authoring-api/destination-server/create-destination-server.md), para generar esquemas basados en su propia API de forma dinámica. Los esquemas dinámicos no utilizan la variable `profileFields` matriz. Si necesita actualizar el esquema, no es necesario [actualizar la configuración de destino](../../authoring-api/destination-configuration/update-destination-configuration.md). En su lugar, el servidor de esquema dinámico recupera el esquema actualizado desde la API de .
* Dentro de la configuración de esquema, tiene la opción de añadir asignaciones necesarias (o predefinidas). Son asignaciones que los usuarios pueden ver en la interfaz de usuario de Platform, pero no pueden modificarlas al configurar una conexión con el destino. Por ejemplo, puede aplicar el campo de dirección de correo electrónico para que siempre se envíe al destino.

La variable `schemaConfig` utiliza varios parámetros de configuración, según el tipo de esquema que necesite, como se muestra en las secciones siguientes.

## Creación de un esquema estático {#attributes-schema}

Para crear un esquema estático con atributos de perfil, defina los atributos de destino en la variable `profileFields` como se muestra a continuación.

```json
"schemaConfig":{
      "profileFields":[
           {
              "name":"phoneNo",
              "title":"phoneNo",
              "description":"This is a fixed attribute on your destination side that customers can map profile attributes to. For example, the mobilePhone.number value in Experience Platform could be phoneNo on your side.",
              "type":"string",
              "isRequired":false,
              "readOnly":false,
              "hidden":false
           },
                      {
              "name":"firstName",
              "title":"firstName",
              "description":"This is a fixed attribute on your destination side that customers can map profile attributes to. For example, the person.name.firstName value in Experience Platform could be firstName on your side.",
              "type":"string",
              "isRequired":false,
              "readOnly":false,
              "hidden":false
           },
                      {
              "name":"lastName",
              "title":"lastName",
              "description":"This is a fixed attribute on your destination side that customers can map profile attributes to. For example, the person.name.lastName value in Experience Platform could be phoneNo on your side.",
              "type":"string",
              "isRequired":false,
              "readOnly":false,
              "hidden":false
           }
        ],
      "useCustomerSchemaForAttributeMapping":false,
      "profileRequired":true,
      "segmentRequired":true,
      "identityRequired":true
}
```

| Parámetro | Tipo | Obligatorio/Opcional | Descripción |
|---------|----------|------|---|
| `profileFields` | Matriz | Opcional | Define la matriz de atributos de destino aceptados por la plataforma de destino a la que los clientes pueden asignar sus atributos de perfil. Al usar un `profileFields` matriz, puede omitir el `useCustomerSchemaForAttributeMapping` completamente. |
| `useCustomerSchemaForAttributeMapping` | Booleano | Opcional | Activa o desactiva la asignación de atributos del esquema del cliente a los atributos definidos en la variable `profileFields` matriz. <ul><li>Si está configurado como `true`, los usuarios solo ven la columna de origen en el campo de asignación. `profileFields` no son aplicables en este caso.</li><li>Si está configurado como `false`, los usuarios pueden asignar atributos de origen desde su esquema a los atributos definidos en el `profileFields` matriz.</li></ul> El valor predeterminado es `false`. |
| `profileRequired` | Booleano | Opcional | Uso `true` si los usuarios deben poder asignar atributos de perfil de Experience Platform a atributos personalizados en la plataforma de destino. |
| `segmentRequired` | Booleano | Requerido | Este parámetro lo requiere el Destination SDK y siempre debe configurarse como `true`. |
| `identityRequired` | Booleano | Requerido | Establecer como `true` si los usuarios deben poder asignar [tipos de identidad](identity-namespace-configuration.md) del Experience Platform a los atributos definidos en la variable `profileFields` matriz . |

{style="table-layout:auto"}

La experiencia de IU resultante se muestra en las imágenes siguientes.

Cuando los usuarios seleccionan la asignación de destino, pueden ver los campos definidos en la variable `profileFields` matriz.

![La imagen de la interfaz de usuario muestra la pantalla de atributos de destino.](../../assets/functionality/destination-configuration/select-attributes.png)

Después de seleccionar los atributos, pueden verlos en la columna de campo de destino.

![Imagen de interfaz de usuario que muestra un esquema de destino estático con atributos](../../assets/functionality/destination-configuration/static-schema-attributes.png)

## Crear un esquema dinámico {#dynamic-schema-configuration}

Destination SDK admite la creación de esquemas de socios dinámicos. A diferencia de los esquemas estáticos, los esquemas dinámicos no utilizan `profileFields` matriz. En su lugar, los esquemas dinámicos utilizan un servidor de esquema dinámico que se conecta a su propia API desde donde recupera la configuración del esquema.

>[!IMPORTANT]
>
>Antes de crear un esquema dinámico, debe [crear un servidor de esquema dinámico](../../authoring-api/destination-server/create-destination-server.md).

En una configuración de esquema dinámico, la variable `profileFields` la matriz se reemplaza por la `dynamicSchemaConfig` como se muestra a continuación.

```json
"schemaConfig":{
   "dynamicSchemaConfig":{
      "dynamicEnum": {
         "authenticationRule":"CUSTOMER_AUTHENTICATION",
         "destinationServerId":"DYNAMIC_SCHEMA_SERVER_ID",
         "value": "Schema Name",
         "responseFormat": "SCHEMA"
      }
   },
   "profileRequired":true,
   "segmentRequired":true,
   "identityRequired":true
}
```

| Parámetro | Tipo | Obligatorio/Opcional | Descripción |
|---------|----------|------|---|
| `dynamicEnum.authenticationRule` | Cadena | Requerido | Indica cómo [!DNL Platform] los clientes se conectan a su destino. Los valores aceptados son `CUSTOMER_AUTHENTICATION`, `PLATFORM_AUTHENTICATION`, `NONE`. <br> <ul><li>Uso `CUSTOMER_AUTHENTICATION` si los clientes de Platform inician sesión en el sistema mediante cualquiera de los métodos de autenticación descritos [here](customer-authentication.md). </li><li> Uso `PLATFORM_AUTHENTICATION` si hay un sistema de autenticación global entre el Adobe y el destino y la variable [!DNL Platform] El cliente no necesita proporcionar credenciales de autenticación para conectarse al destino. En este caso, debe [crear un objeto credentials](../../credentials-api/create-credential-configuration.md) mediante la API de credenciales. </li><li>Uso `NONE` si no se requiere autenticación para enviar datos a la plataforma de destino. </li></ul> |
| `dynamicEnum.destinationServerId` | Cadena | Requerido | La variable `instanceId` del servidor de esquema dinámico. Este servidor de destino incluye el extremo de API que llamará el Experience Platform para recuperar el esquema dinámico. |
| `dynamicEnum.value` | Cadena | Requerido | Nombre del esquema dinámico, tal como se define en la configuración del servidor de esquema dinámico. |
| `dynamicEnum.responseFormat` | Cadena | Requerido | Siempre se configura como `SCHEMA` al definir un esquema dinámico. |
| `profileRequired` | Booleano | Opcional | Uso `true` si los usuarios deben poder asignar atributos de perfil de Experience Platform a atributos personalizados en la plataforma de destino. |
| `segmentRequired` | Booleano | Requerido | Este parámetro lo requiere el Destination SDK y siempre debe configurarse como `true`. |
| `identityRequired` | Booleano | Requerido | Establecer como `true` si los usuarios deben poder asignar [tipos de identidad](identity-namespace-configuration.md) del Experience Platform a los atributos definidos en la variable `profileFields` matriz . |

{style="table-layout:auto"}

## Asignaciones necesarias {#required-mappings}

Dentro de la configuración de esquema, además del esquema estático o dinámico, tiene la opción de añadir asignaciones necesarias (o predefinidas). Son asignaciones que los usuarios pueden ver en la interfaz de usuario de Platform, pero no pueden modificarlas al configurar una conexión con el destino.

Por ejemplo, puede aplicar el campo de dirección de correo electrónico para que siempre se envíe al destino.

>[!NOTE]
>
>Actualmente se admiten las siguientes combinaciones de asignaciones requeridas:
>* Puede configurar un campo de origen requerido y un campo de destino requerido. En este caso, los usuarios no pueden editar ni seleccionar ninguno de los dos campos y solo pueden ver la selección.
>* Solo puede configurar un campo de destino requerido. En este caso, los usuarios podrán seleccionar un campo de origen para asignarlo al destino.
>
> Actualmente, la configuración de un campo de origen requerido solo está *not* compatible.

Consulte a continuación dos ejemplos de una configuración de esquema con asignaciones necesarias y su aspecto en el paso de asignación de la variable [flujo de trabajo de activación de datos en destinos por lotes](../../../ui/activate-batch-profile-destinations.md).


>[!BEGINTABS]

>[!TAB Asignaciones de origen y destino requeridas]

El ejemplo siguiente muestra las asignaciones de origen y destino necesarias. Cuando se especifican los campos de origen y de destino como asignaciones requeridas, los usuarios no pueden seleccionar ni editar ninguno de los dos campos y solo pueden ver la selección predefinida.

```json
"schemaConfig": {
    "requiredMappingsOnly": true,
    "requiredMappings": [
      {
        "sourceType": "text/x.schema-path",
        "source": "personalEmail.address",
        "destination": "personalEmail.address"
      }
    ] 
}
```

| Parámetro | Tipo | Obligatorio/Opcional | Descripción |
|---|---|---|---|
| `requiredMappingsOnly` | Booleano | Opcional | Cuando se establece en true , los usuarios no pueden asignar otros atributos e identidades en el flujo de activación, aparte de las asignaciones necesarias que defina en la variable `requiredMappings` matriz. |
| `requiredMappings.sourceType` | Cadena | Requerido | Indica el tipo de `source` campo . Valores compatibles: <ul><li>`text/x.schema-path`: Utilice este valor cuando la variable `source` field es un atributo de perfil de un esquema XDM.</li><li>`text/x.aep-xl`: Utilice este valor cuando `source` se define mediante una expresión regular. Ejemplo: `iif(segmentMembership.ups.aep_seg_id.status==\"exited\", \"1\", \"0\")`</li><li>`text/plain`: Utilice este valor cuando `source` se define mediante una plantilla de macro. Actualmente, la única plantilla de macro admitida es `metadata.segment.alias`.</li></ul> |
| `requiredMappings.source` | Cadena | Requerido | Indica el valor del campo de origen. Tipos de valores compatibles: <ul><li>Atributos de perfil XDM. Ejemplo: `personalEmail.address`. Cuando el atributo de origen es un atributo de perfil XDM, establezca la variable `sourceType` parámetro a `text/x.schema-path`.</li><li>Expresiones regulares. Ejemplo: `iif(segmentMembership.ups.aep_seg_id.status==\"exited\", \"1\", \"0\")`. Cuando el atributo de origen es una expresión regular, establezca la variable `sourceType` parámetro a `text/x.aep-xl`.</li><li>Plantillas de macro. Ejemplo:`metadata.segment.alias`. Cuando el atributo de origen es una plantilla de macro, establezca la variable `sourceType` parámetro a `text/plain`. Actualmente, la única plantilla de macro admitida es `metadata.segment.alias`.</li></ul> |
| `requiredMappings.destination` | Cadena | Requerido | Indica el valor del campo de destino. Cuando se especifican los campos de origen y de destino como asignaciones requeridas, los usuarios no pueden seleccionar ni editar ninguno de los dos campos y solo pueden ver la selección. |

{style="table-layout:auto"}

Como resultado, ambas variables **[!UICONTROL Campo de origen]** y **[!UICONTROL Campo de destino]** las secciones de la interfaz de usuario de Platform aparecen atenuadas.

![Imagen de las asignaciones necesarias en el flujo de activación de la interfaz de usuario.](../../assets/functionality/destination-configuration/required-mappings-2.png)

>[!TAB Asignación de destino necesaria]

El ejemplo siguiente muestra una asignación de destino necesaria. Si solo se especifica el campo de destino según sea necesario, los usuarios pueden seleccionar qué campo de origen asignarle.

```json
"schemaConfig": {
    "requiredMappingsOnly": true,
    "requiredMappings": [
      {
        "destination": "identityMap.ExamplePartner_ID",
        "mandatoryRequired": true,
        "primaryKeyRequired": true
      }
    ] 
}
```

| Parámetro | Tipo | Obligatorio/Opcional | Descripción |
|---|---|---|---|
| `requiredMappingsOnly` | Booleano | Opcional | Cuando se establece en true , los usuarios no pueden asignar otros atributos e identidades en el flujo de activación, aparte de las asignaciones necesarias que defina en la variable `requiredMappings` matriz. |
| `requiredMappings.destination` | Cadena | Requerido | Indica el valor del campo de destino. Cuando solo se especifica el campo de destino, los usuarios pueden seleccionar un campo de origen para asignarlo al destino. |
| `mandatoryRequired` | Booleano | Opcional | Indica si la asignación debe marcarse como un [atributo obligatorio](../../../ui/activate-batch-profile-destinations.md#mandatory-attributes). |
| `primaryKeyRequired` | Booleano | Opcional | Indica si la asignación debe marcarse como un [clave de deduplicación](../../../ui/activate-batch-profile-destinations.md#deduplication-keys). |

{style="table-layout:auto"}

Como resultado, la variable **[!UICONTROL Campo de destino]** en la interfaz de usuario de Platform aparece atenuada, mientras que la variable **[!UICONTROL Campo de origen]** está activa y los usuarios pueden interactuar con ella. La variable **[!UICONTROL Clave obligatoria]** y **[!UICONTROL Clave de deduplicación]** están activas y los usuarios no pueden cambiarlas.

![Imagen de las asignaciones necesarias en el flujo de activación de la interfaz de usuario.](../../assets/functionality/destination-configuration/required-mappings-1.png)

>[!ENDTABS]

## Pasos siguientes {#next-steps}

Después de leer este artículo, debe comprender mejor qué tipos de esquema admite el Destination SDK y cómo puede configurar el esquema.

Para obtener más información sobre los otros componentes de destino, consulte los siguientes artículos:

* [Autenticación del cliente](customer-authentication.md)
* [Autenticación OAuth2](oauth2-authentication.md)
* [Atributos de interfaz de usuario](ui-attributes.md)
* [Campos de datos del cliente](customer-data-fields.md)
* [Configuración del área de nombres de identidad](identity-namespace-configuration.md)
* [Configuraciones de asignación admitidas](supported-mapping-configurations.md)
* [Entrega de destino](destination-delivery.md)
* [Configuración de metadatos de audiencia](audience-metadata-configuration.md)
* [Política de agregación](aggregation-policy.md)
* [Configuración por lotes](batch-configuration.md)
* [Calificaciones históricas de perfil](historical-profile-qualifications.md)