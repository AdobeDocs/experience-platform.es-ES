---
description: Obtenga información sobre cómo configurar el esquema de socio para destinos creados con Destination SDK.
title: Configuración del esquema de socio
source-git-commit: b66a50e40aaac8df312a2c9a977fb8d4f1fb0c80
workflow-type: tm+mt
source-wordcount: '1897'
ht-degree: 4%

---


# Configuración del esquema de socio

Experience Platform utiliza esquemas para describir la estructura de los datos de una manera uniforme y reutilizable. Cuando se incorporan datos en Platform, se estructuran según un esquema XDM. Para obtener más información sobre el modelo de composición de esquemas, incluidos los principios de diseño y las prácticas recomendadas, consulte la [conceptos básicos de composición de esquemas](../../../../xdm/schema/composition.md).

Al crear un destino con Destination SDK, puede definir su propio esquema de socio para que lo utilice su plataforma de destino. Esto permite a los usuarios asignar atributos de perfil de Platform a campos específicos que la plataforma de destino reconoce, todo ello dentro de la interfaz de usuario de Platform.

Al configurar el esquema de socio para el destino, puede ajustar la asignación de campos admitida por la plataforma de destino, como:

* Permitir que los usuarios asignen un `phoneNumber` Atributo XDM a `phone` atributo admitido por la plataforma de destino.
* Cree esquemas de socios dinámicos a los que el Experience Platform pueda llamar dinámicamente para recuperar una lista de todos los atributos admitidos dentro del destino.
* Defina las asignaciones de campos obligatorias que requiere la plataforma de destino.

Para saber dónde encaja este componente en una integración creada con Destination SDK, consulte el diagrama en la [opciones de configuración](../configuration-options.md) o consulte la guía sobre cómo [usar Destination SDK para configurar un destino basado en archivos](../../guides/configure-file-based-destination-instructions.md#create-server-file-configuration).

Puede configurar los ajustes del esquema mediante la variable `/authoring/destinations` punto final. Consulte las siguientes páginas de referencia de la API para ver ejemplos detallados de llamadas de la API donde puede configurar los componentes que se muestran en esta página.

* [Crear una configuración de destino](../../authoring-api/destination-configuration/create-destination-configuration.md)
* [Actualizar una configuración de destino](../../authoring-api/destination-configuration/update-destination-configuration.md)

Este artículo describe todas las opciones de configuración de esquema admitidas que puede utilizar para su destino y muestra lo que los clientes verán en la interfaz de usuario de Platform.

>[!IMPORTANT]
>
>Todos los nombres y valores de parámetro admitidos por el Destination SDK son **distingue mayúsculas de minúsculas**. Para evitar errores de distinción entre mayúsculas y minúsculas, utilice los nombres y valores de los parámetros exactamente como se muestra en la documentación.

## Tipos de integración admitidos {#supported-integration-types}

Consulte la tabla siguiente para obtener detalles sobre qué tipos de integraciones admiten la funcionalidad descrita en esta página.

| Tipo de integración | Admite funcionalidad |
|---|---|
| Integraciones en tiempo real (streaming) | Sí |
| Integraciones basadas en archivos (por lotes) | Sí |

## Configuración de esquema admitida {#supported-schema-types}

El Destination SDK admite varias configuraciones de esquema:

* Los esquemas estáticos se definen mediante la variable `profileFields` matriz en la `schemaConfig` sección. En un esquema estático, se definen todos los atributos de destino que deben mostrarse en la interfaz de usuario del Experience Platform en la `profileFields` matriz. Si necesita actualizar el esquema, debe [actualizar la configuración de destino](../../authoring-api/destination-configuration/update-destination-configuration.md).
* Los esquemas dinámicos utilizan un tipo de servidor de destino adicional, denominado [servidor de esquema dinámico](../../authoring-api/destination-server/create-destination-server.md#dynamic-schema-servers), para recuperar dinámicamente los atributos de destino admitidos y generar esquemas basados en su propia API. Los esquemas dinámicos no utilizan `profileFields` matriz. Si necesita actualizar el esquema, no es necesario [actualizar la configuración de destino](../../authoring-api/destination-configuration/update-destination-configuration.md). En su lugar, el servidor de esquema dinámico recupera el esquema actualizado de la API.
* En la configuración del esquema, tiene la opción de añadir las asignaciones necesarias (o predefinidas). Son asignaciones que los usuarios pueden ver en la interfaz de usuario de Platform, pero no pueden modificarlas al configurar una conexión con el destino. Por ejemplo, puede hacer que el campo de dirección de correo electrónico se envíe siempre al destino.

El `schemaConfig` utiliza varios parámetros de configuración, según el tipo de esquema que necesite, como se muestra en las secciones siguientes.

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
      "identityRequired":true,
      "segmentNamespaceAllowList": ["someNamespace"],
      "segmentNamespaceDenyList": ["someOtherNamespace"]

}
```

| Parámetro | Tipo | Obligatorio/Opcional | Descripción |
|---------|----------|------|---|
| `profileFields` | Matriz | Opcional | Define la matriz de atributos de destinatario aceptados por la plataforma de destino a los que los clientes pueden asignar sus atributos de perfil. Cuando se utiliza un `profileFields` matriz, puede omitir la variable `useCustomerSchemaForAttributeMapping` parámetro por completo. |
| `useCustomerSchemaForAttributeMapping` | Booleano | Opcional | Activa o desactiva la asignación de atributos del esquema del cliente a los atributos definidos en la variable `profileFields` matriz. <ul><li>Si se establece en `true`Sin embargo, los usuarios solo ven la columna de origen en el campo de asignación. `profileFields` no son aplicables en este caso.</li><li>Si se establece en `false`, los usuarios pueden asignar atributos de origen de su esquema a los atributos definidos en la variable `profileFields` matriz.</li></ul> El valor predeterminado es `false`. |
| `profileRequired` | Booleano | Opcional | Uso `true` si los usuarios deben poder asignar atributos de perfil de Experience Platform a atributos personalizados en la plataforma de destino. |
| `segmentRequired` | Booleano | Requerido | Este parámetro es obligatorio para el Destination SDK y siempre debe configurarse como `true`. |
| `identityRequired` | Booleano | Requerido | Configure como. `true` si los usuarios deben poder asignar [tipos de identidad](identity-namespace-configuration.md) del Experience Platform a los atributos definidos en el `profileFields` matriz . |
| `segmentNamespaceAllowList` | Matriz | Opcional | Define áreas de nombres de audiencia específicas desde las que los usuarios pueden asignar audiencias al destino. Utilice este parámetro para restringir el acceso de los usuarios de Platform a la exportación de audiencias únicamente desde las áreas de nombres de audiencia definidas en la matriz. Este parámetro no se puede usar junto con `segmentNamespaceDenyList`.<br> <br> Ejemplo: `"segmentNamespaceAllowList": ["AudienceManager"]` permitirá a los usuarios asignar solamente audiencias de `AudienceManager` a este destino. <br> <br> Para permitir que los usuarios exporten cualquier audiencia a su destino, puede ignorar este parámetro. <br> <br> Si ambos `segmentNamespaceAllowList` y `segmentNamespaceDenyList` no aparecen en la configuración, los usuarios solo podrán exportar audiencias procedentes de [Servicio de segmentación](../../../../segmentation/home.md). |
| `segmentNamespaceDenyList` | Matriz | Opcional | Restringe a los usuarios de la asignación de audiencias al destino, desde los espacios de nombres de audiencia definidos en la matriz. No se puede usar junto con `segmentNamespaceAllowed`. <br> <br> Ejemplo: `"segmentNamespaceDenyList": ["AudienceManager"]` bloqueará a los usuarios la asignación de audiencias del `AudienceManager` a este destino. <br> <br> Para permitir que los usuarios exporten cualquier audiencia a su destino, puede ignorar este parámetro. <br> <br> Si ambos `segmentNamespaceAllowed` y `segmentNamespaceDenyList` no aparecen en la configuración, los usuarios solo podrán exportar audiencias procedentes de [Servicio de segmentación](../../../../segmentation/home.md). <br> <br> Para permitir la exportación de todas las audiencias, independientemente del origen, establezca `"segmentNamespaceDenyList":[]`. |

{style="table-layout:auto"}

La experiencia de IU resultante se muestra en las imágenes siguientes.

Cuando los usuarios seleccionan la asignación de destino, pueden ver los campos definidos en la variable `profileFields` matriz.

![Imagen de la interfaz de usuario que muestra la pantalla de atributos de destinatario.](../../assets/functionality/destination-configuration/select-attributes.png)

Después de seleccionar los atributos, pueden verlos en la columna del campo de destinatario.

![Imagen de la interfaz de usuario que muestra un esquema de destinatario estático con atributos](../../assets/functionality/destination-configuration/static-schema-attributes.png)

## Creación de un esquema dinámico {#dynamic-schema-configuration}

Destination SDK permite crear esquemas de socios dinámicos. A diferencia de un esquema estático, un esquema dinámico no utiliza un `profileFields` matriz. En su lugar, los esquemas dinámicos utilizan un servidor de esquema dinámico que se conecta a su propia API desde donde recupera la configuración de esquema.

>[!IMPORTANT]
>
>Antes de crear un esquema dinámico, debe [creación de un servidor de esquema dinámico](../../authoring-api/destination-server/create-destination-server.md#dynamic-schema-servers).

En una configuración de esquema dinámico, la variable `profileFields` La matriz se reemplaza por `dynamicSchemaConfig` , como se muestra a continuación.

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
| `dynamicEnum.authenticationRule` | Cadena | Requerido | Indica cómo [!DNL Platform] los clientes se conectan a su destino. Los valores aceptados son `CUSTOMER_AUTHENTICATION`, `PLATFORM_AUTHENTICATION`, `NONE`. <br> <ul><li>Uso `CUSTOMER_AUTHENTICATION` si los clientes de Platform inician sesión en el sistema mediante cualquiera de los métodos de autenticación descritos [aquí](customer-authentication.md). </li><li> Uso `PLATFORM_AUTHENTICATION` si existe un sistema de autenticación global entre el Adobe y el destino y el [!DNL Platform] el cliente no necesita proporcionar credenciales de autenticación para conectarse a su destino. En este caso, debe [crear un objeto de credenciales](../../credentials-api/create-credential-configuration.md) mediante la API de credenciales. </li><li>Uso `NONE` si no se requiere autenticación para enviar datos a la plataforma de destino. </li></ul> |
| `dynamicEnum.destinationServerId` | Cadena | Requerido | El `instanceId` del servidor de esquema dinámico. Este servidor de destino incluye el extremo de API al que el Experience Platform llamará para recuperar el esquema dinámico. |
| `dynamicEnum.value` | Cadena | Requerido | El nombre del esquema dinámico, tal como se define en la configuración del servidor de esquema dinámico. |
| `dynamicEnum.responseFormat` | Cadena | Requerido | Siempre establecido en `SCHEMA` al definir un esquema dinámico. |
| `profileRequired` | Booleano | Opcional | Uso `true` si los usuarios deben poder asignar atributos de perfil de Experience Platform a atributos personalizados en la plataforma de destino. |
| `segmentRequired` | Booleano | Requerido | Este parámetro es obligatorio para el Destination SDK y siempre debe configurarse como `true`. |
| `identityRequired` | Booleano | Requerido | Configure como. `true` si los usuarios deben poder asignar [tipos de identidad](identity-namespace-configuration.md) del Experience Platform a los atributos definidos en el `profileFields` matriz . |

{style="table-layout:auto"}

## Asignaciones requeridas {#required-mappings}

En la configuración del esquema, además del esquema estático o dinámico, tiene la opción de añadir las asignaciones necesarias (o predefinidas). Son asignaciones que los usuarios pueden ver en la interfaz de usuario de Platform, pero no pueden modificarlas al configurar una conexión con el destino.

Por ejemplo, puede hacer que el campo de dirección de correo electrónico se envíe siempre al destino.

>[!NOTE]
>
>Actualmente se admiten las siguientes combinaciones de asignaciones requeridas:
>* Puede configurar un campo de origen y un campo de destino obligatorios. En este caso, los usuarios no pueden editar ni seleccionar ninguno de los dos campos y solo pueden ver la selección.
>* Solo puede configurar un campo de destino requerido. En este caso, los usuarios podrán seleccionar un campo de origen para asignarlo al destino.
>
> Actualmente solo se puede configurar un campo de origen obligatorio *no* compatible.

Vea a continuación dos ejemplos de una configuración de esquema con asignaciones requeridas y cómo se ven en el paso de asignación de la variable [flujo de trabajo activar datos en destinos por lotes](../../../ui/activate-batch-profile-destinations.md).


>[!BEGINTABS]

>[!TAB Asignaciones de origen y destino requeridas]

El ejemplo siguiente muestra las asignaciones de origen y destino requeridas. Cuando los campos de origen y de destino se especifican como asignaciones requeridas, los usuarios no pueden seleccionar ni editar ninguno de los dos campos y solo pueden ver la selección predefinida.

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
| `requiredMappingsOnly` | Booleano | Opcional | Cuando se establece en true , los usuarios no pueden asignar otros atributos e identidades en el flujo de activación, aparte de las asignaciones requeridas que defina en la variable `requiredMappings` matriz. |
| `requiredMappings.sourceType` | Cadena | Requerido | Indica el tipo de `source` field. Valores compatibles: <ul><li>`text/x.schema-path`: utilice este valor cuando el `source` Este campo es un atributo de perfil de un esquema XDM.</li><li>`text/x.aep-xl`: Utilice este valor cuando `source` El campo se define mediante una expresión regular. Ejemplo: `iif(segmentMembership.ups.aep_seg_id.status==\"exited\", \"1\", \"0\")`</li><li>`text/plain`: Utilice este valor cuando `source` El campo se define mediante una plantilla de macro. Actualmente, la única plantilla de macro admitida es `metadata.segment.alias`.</li></ul> |
| `requiredMappings.source` | Cadena | Requerido | Indica el valor del campo de origen. Tipos de valores admitidos: <ul><li>Atributos de perfil XDM. Ejemplo: `personalEmail.address`. Cuando el atributo de origen sea un atributo de perfil XDM, defina la variable `sourceType` parámetro a `text/x.schema-path`.</li><li>Expresiones regulares. Ejemplo: `iif(segmentMembership.ups.aep_seg_id.status==\"exited\", \"1\", \"0\")`. Cuando el atributo de origen sea una expresión regular, establezca el `sourceType` parámetro a `text/x.aep-xl`.</li><li>Plantillas de macros. Ejemplo:`metadata.segment.alias`. Si el atributo de origen es una plantilla de macro, establezca la variable `sourceType` parámetro a `text/plain`. Actualmente, la única plantilla de macro admitida es `metadata.segment.alias`.</li></ul> |
| `requiredMappings.destination` | Cadena | Requerido | Indica el valor del campo de destino. Cuando los campos de origen y de destino se especifican como asignaciones requeridas, los usuarios no pueden seleccionar ni editar ninguno de los dos campos y solo pueden ver la selección. |

{style="table-layout:auto"}

Como resultado, tanto la variable **[!UICONTROL Campo de origen]** y **[!UICONTROL Campo de destino]** Las secciones de la IU de Platform aparecen atenuadas.

![Imagen de las asignaciones requeridas en el flujo de activación de la IU.](../../assets/functionality/destination-configuration/required-mappings-2.png)

>[!TAB Asignación de destino requerida]

El ejemplo siguiente muestra una asignación de destino requerida. Si solo se especifica el campo de destino como obligatorio, los usuarios pueden seleccionar qué campo de origen se asignará a él.

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
| `requiredMappingsOnly` | Booleano | Opcional | Cuando se establece en true , los usuarios no pueden asignar otros atributos e identidades en el flujo de activación, aparte de las asignaciones requeridas que defina en la variable `requiredMappings` matriz. |
| `requiredMappings.destination` | Cadena | Requerido | Indica el valor del campo de destino. Cuando solo se especifica el campo de destino, los usuarios pueden seleccionar un campo de origen para asignarlo al destino. |
| `mandatoryRequired` | Booleano | Opcional | Indica si la asignación debe marcarse como [atributo obligatorio](../../../ui/activate-batch-profile-destinations.md#mandatory-attributes). |
| `primaryKeyRequired` | Booleano | Opcional | Indica si la asignación debe marcarse como [clave de deduplicación](../../../ui/activate-batch-profile-destinations.md#deduplication-keys). |

{style="table-layout:auto"}

Como resultado, la variable **[!UICONTROL Campo de destino]** de la IU de Platform aparece atenuada, mientras que la sección **[!UICONTROL Campo de origen]** La sección está activa y los usuarios pueden interactuar con ella. El **[!UICONTROL Clave obligatoria]** y **[!UICONTROL Clave de deduplicación]** Las opciones de están activas y los usuarios no pueden cambiarlas.

![Imagen de las asignaciones requeridas en el flujo de activación de la IU.](../../assets/functionality/destination-configuration/required-mappings-1.png)

>[!ENDTABS]

## Pasos siguientes {#next-steps}

Después de leer este artículo, debería comprender mejor qué tipos de esquema admite Destination SDK y cómo puede configurar el esquema.

Para obtener más información acerca de los demás componentes de destino, consulte los siguientes artículos:

* [Autenticación del cliente](customer-authentication.md)
* [Autenticación OAuth2](oauth2-authentication.md)
* [Atributos de IU](ui-attributes.md)
* [Campos de datos del cliente](customer-data-fields.md)
* [Configuración del área de nombres de identidad](identity-namespace-configuration.md)
* [Configuraciones de asignación compatibles](supported-mapping-configurations.md)
* [Envío de destino](destination-delivery.md)
* [Configuración de metadatos de audiencia](audience-metadata-configuration.md)
* [Política de agregación](aggregation-policy.md)
* [Configuración por lotes](batch-configuration.md)
* [Cualificaciones históricas del perfil](historical-profile-qualifications.md)