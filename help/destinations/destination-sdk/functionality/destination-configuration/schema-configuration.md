---
description: Obtenga información sobre cómo configurar el esquema de socio para destinos creados con Destination SDK.
title: Configuración del esquema de socio
exl-id: 0548e486-206b-45c5-8d18-0d6427c177c5
source-git-commit: 30a237c7acf814722d384792366f95289dc3f34a
workflow-type: tm+mt
source-wordcount: '1896'
ht-degree: 3%

---

# Configuración del esquema de socio

Experience Platform utiliza esquemas para describir la estructura de los datos de una manera uniforme y reutilizable. Cuando se incorporan datos en Experience Platform, se estructuran según un esquema XDM. Para obtener más información sobre el modelo de composición de esquema, incluidos los principios de diseño y las prácticas recomendadas, vea los [conceptos básicos de la composición de esquema](../../../../xdm/schema/composition.md).

Al crear un destino con Destination SDK, puede definir su propio esquema de socio para que lo utilice su plataforma de destino. Esto permite a los usuarios asignar atributos de perfil de Experience Platform a campos específicos que reconoce la plataforma de destino, todo ello dentro de la interfaz de usuario de Experience Platform.

Al configurar el esquema de socio para el destino, puede ajustar la asignación de campos admitida por la plataforma de destino, como:

* Permitir que los usuarios asignen un atributo XDM `phoneNumber` a un atributo `phone` compatible con la plataforma de destino.
* Cree esquemas de socios dinámicos a los que Experience Platform pueda llamar dinámicamente para recuperar una lista de todos los atributos admitidos dentro del destino.
* Defina las asignaciones de campos obligatorias que requiere la plataforma de destino.

Para saber dónde encaja este componente en una integración creada con Destination SDK, consulte el diagrama en la documentación de [opciones de configuración](../configuration-options.md) o vea la guía sobre cómo [usar Destination SDK para configurar un destino basado en archivos](../../guides/configure-file-based-destination-instructions.md#create-server-file-configuration).

Puede configurar las opciones del esquema a través del extremo `/authoring/destinations`. Consulte las siguientes páginas de referencia de la API para ver ejemplos detallados de llamadas de la API donde puede configurar los componentes que se muestran en esta página.

* [Crear una configuración de destino](../../authoring-api/destination-configuration/create-destination-configuration.md)
* [Actualizar una configuración de destino](../../authoring-api/destination-configuration/update-destination-configuration.md)

Este artículo describe todas las opciones de configuración de esquema admitidas que puede utilizar para su destino y muestra lo que los clientes verán en la interfaz de usuario de Experience Platform.

>[!IMPORTANT]
>
>Todos los nombres y valores de parámetro admitidos por Destination SDK distinguen entre mayúsculas y minúsculas **1}.** Para evitar errores de distinción entre mayúsculas y minúsculas, utilice los nombres y valores de los parámetros exactamente como se muestra en la documentación.

## Tipos de integración admitidos {#supported-integration-types}

Consulte la tabla siguiente para obtener detalles sobre qué tipos de integraciones admiten la funcionalidad descrita en esta página.

| Tipo de integración | Admite funcionalidad |
|---|---|
| Integraciones en tiempo real (streaming) | Sí |
| Integraciones basadas en archivos (por lotes) | Sí |

## Configuración de esquema admitida {#supported-schema-types}

Destination SDK admite varias configuraciones de esquema:

* Los esquemas estáticos se definen mediante la matriz `profileFields` en la sección `schemaConfig`. En un esquema estático, define todos los atributos de destino que deben mostrarse en la interfaz de usuario de Experience Platform en la matriz `profileFields`. Si necesita actualizar su esquema, debe [actualizar la configuración de destino](../../authoring-api/destination-configuration/update-destination-configuration.md).
* Los esquemas dinámicos utilizan un tipo de servidor de destino adicional, denominado [servidor de esquema dinámico](../../authoring-api/destination-server/create-destination-server.md#dynamic-schema-servers), para recuperar dinámicamente los atributos de destino admitidos y generar esquemas basados en su propia API. Los esquemas dinámicos no utilizan la matriz `profileFields`. Si necesita actualizar su esquema, no es necesario [actualizar la configuración de destino](../../authoring-api/destination-configuration/update-destination-configuration.md). En su lugar, el servidor de esquema dinámico recupera el esquema actualizado de la API.
* En la configuración del esquema, tiene la opción de añadir las asignaciones necesarias (o predefinidas). Son asignaciones que los usuarios pueden ver en la interfaz de usuario de Experience Platform, pero no pueden modificarlas al configurar una conexión con el destino. Por ejemplo, puede hacer que el campo de dirección de correo electrónico se envíe siempre al destino.

La sección `schemaConfig` utiliza varios parámetros de configuración, según el tipo de esquema que necesite, como se muestra en las secciones siguientes.

## Creación de un esquema estático {#attributes-schema}

Para crear un esquema estático con atributos de perfil, defina los atributos de destino en la matriz `profileFields` como se muestra a continuación.

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
| `profileFields` | Matriz | Opcional | Define la matriz de atributos de destinatario aceptados por la plataforma de destino a los que los clientes pueden asignar sus atributos de perfil. Al utilizar una matriz `profileFields`, puede omitir completamente el parámetro `useCustomerSchemaForAttributeMapping`. |
| `useCustomerSchemaForAttributeMapping` | Booleano | Opcional | Habilita o deshabilita la asignación de atributos del esquema cliente a los atributos definidos en la matriz `profileFields`. <ul><li>Si se establece en `true`, los usuarios solo verán la columna de origen en el campo de asignación. `profileFields` no son aplicables en este caso.</li><li>Si se establece en `false`, los usuarios pueden asignar atributos de origen de su esquema a los atributos definidos en la matriz `profileFields`.</li></ul> El valor predeterminado es `false`. |
| `profileRequired` | Booleano | Opcional | Use `true` si los usuarios deben poder asignar atributos de perfil de Experience Platform a atributos personalizados en la plataforma de destino. |
| `segmentRequired` | Booleano | Requerido | Destination SDK requiere este parámetro y siempre se debe establecer en `true`. |
| `identityRequired` | Booleano | Requerido | Se establece en `true` si los usuarios deben poder asignar [tipos de identidad](identity-namespace-configuration.md) de Experience Platform a los atributos definidos en la matriz `profileFields` |
| `segmentNamespaceAllowList` | Matriz | Opcional | Permite a los usuarios asignar únicamente audiencias de las áreas de nombres de audiencia definidas en la matriz al destino. <br><br> En la mayoría de los casos no se recomienda el uso de este parámetro. En su lugar, use `"segmentNamespaceDenyList":[]` para permitir que se exporten todos los tipos de audiencias a su destino. <br><br> Si faltan `segmentNamespaceAllowList` y `segmentNamespaceDenyList` en la configuración, los usuarios solo podrán exportar audiencias que se originen del [servicio de segmentación](../../../../segmentation/home.md). <br><br>`segmentNamespaceAllowList` y `segmentNamespaceDenyList` se excluyen mutuamente. |
| `segmentNamespaceDenyList` | Matriz | Opcional | Restringe a los usuarios de la asignación de audiencias desde las áreas de nombres de audiencia definidas en la matriz al destino. <br><br>Adobe recomienda permitir la exportación de todas las audiencias, independientemente del origen, estableciendo `"segmentNamespaceDenyList":[]`. <br><br>Si faltan `segmentNamespaceAllowed` y `segmentNamespaceDenyList` en la configuración, los usuarios solo podrán exportar audiencias que se originen del [servicio de segmentación](../../../../segmentation/home.md). <br><br>`segmentNamespaceAllowList` y `segmentNamespaceDenyList` se excluyen mutuamente. |

{style="table-layout:auto"}

La experiencia de IU resultante se muestra en las imágenes siguientes.

Cuando los usuarios seleccionan la asignación de destino, pueden ver los campos definidos en la matriz `profileFields`.

![Imagen de interfaz de usuario que muestra la pantalla de atributos de destino.](../../assets/functionality/destination-configuration/select-attributes.png)

Después de seleccionar los atributos, pueden verlos en la columna del campo de destinatario.

![Imagen de interfaz de usuario que muestra un esquema de destino estático con atributos](../../assets/functionality/destination-configuration/static-schema-attributes.png)

## Creación de un esquema dinámico {#dynamic-schema-configuration}

Destination SDK admite la creación de esquemas de socios dinámicos. A diferencia de un esquema estático, un esquema dinámico no utiliza una matriz `profileFields`. En su lugar, los esquemas dinámicos utilizan un servidor de esquema dinámico que se conecta a su propia API desde donde recupera la configuración de esquema.

>[!IMPORTANT]
>
>Antes de crear un esquema dinámico, debe [crear un servidor de esquema dinámico](../../authoring-api/destination-server/create-destination-server.md#dynamic-schema-servers).

En una configuración de esquema dinámico, la matriz `profileFields` se reemplaza por la sección `dynamicSchemaConfig`, como se muestra a continuación.

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
| `dynamicEnum.authenticationRule` | Cadena | Requerido | Indica cómo se conectan los clientes de [!DNL Experience Platform] a su destino. Los valores aceptados son `CUSTOMER_AUTHENTICATION`, `PLATFORM_AUTHENTICATION`, `NONE`. <br> <ul><li>Use `CUSTOMER_AUTHENTICATION` si los clientes de Experience Platform inician sesión en el sistema mediante cualquiera de los métodos de autenticación descritos [aquí](customer-authentication.md). </li><li> Use `PLATFORM_AUTHENTICATION` si existe un sistema de autenticación global entre Adobe y su destino y el cliente [!DNL Experience Platform] no necesita proporcionar credenciales de autenticación para conectarse a su destino. En este caso, debe [crear un objeto de credenciales](../../credentials-api/create-credential-configuration.md) mediante la API de credenciales. </li><li>Use `NONE` si no se requiere autenticación para enviar datos a la plataforma de destino. </li></ul> |
| `dynamicEnum.destinationServerId` | Cadena | Requerido | El `instanceId` de su servidor de esquema dinámico. Este servidor de destino incluye el extremo de API al que Experience Platform llamará para recuperar el esquema dinámico. |
| `dynamicEnum.value` | Cadena | Requerido | El nombre del esquema dinámico, tal como se define en la configuración del servidor de esquema dinámico. |
| `dynamicEnum.responseFormat` | Cadena | Requerido | Siempre se establece en `SCHEMA` al definir un esquema dinámico. |
| `profileRequired` | Booleano | Opcional | Use `true` si los usuarios deben poder asignar atributos de perfil de Experience Platform a atributos personalizados en la plataforma de destino. |
| `segmentRequired` | Booleano | Requerido | Destination SDK requiere este parámetro y siempre se debe establecer en `true`. |
| `identityRequired` | Booleano | Requerido | Se establece en `true` si los usuarios deben poder asignar [tipos de identidad](identity-namespace-configuration.md) de Experience Platform a los atributos definidos en la matriz `profileFields` |

{style="table-layout:auto"}

## Asignaciones requeridas {#required-mappings}

En la configuración del esquema, además del esquema estático o dinámico, tiene la opción de añadir las asignaciones necesarias (o predefinidas). Son asignaciones que los usuarios pueden ver en la interfaz de usuario de Experience Platform, pero no pueden modificarlas al configurar una conexión con el destino.

Por ejemplo, puede hacer que el campo de dirección de correo electrónico se envíe siempre al destino.

>[!NOTE]
>
>Actualmente se admiten las siguientes combinaciones de asignaciones requeridas:
>* Puede configurar un campo de origen y un campo de destino obligatorios. En este caso, los usuarios no pueden editar ni seleccionar ninguno de los dos campos y solo pueden ver la selección.
>* Solo puede configurar un campo de destino requerido. En este caso, los usuarios podrán seleccionar un campo de origen para asignarlo al destino.
>
> Actualmente solo se admite la configuración de un campo de origen obligatorio *no*.

Vea a continuación dos ejemplos de una configuración de esquema con asignaciones requeridas y cómo se ven en el paso de asignación de [activar datos en el flujo de trabajo de destinos por lotes](../../../ui/activate-batch-profile-destinations.md).


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
| `requiredMappingsOnly` | Booleano | Opcional | Cuando se establece en true , los usuarios no pueden asignar otros atributos e identidades en el flujo de activación, aparte de las asignaciones necesarias que defina en la matriz `requiredMappings`. |
| `requiredMappings.sourceType` | Cadena | Requerido | Indica el tipo del campo `source`. Valores compatibles: <ul><li>`text/x.schema-path`: utilice este valor cuando el campo `source` sea un atributo de perfil de un esquema XDM.</li><li>`text/x.aep-xl`: utilice este valor cuando su campo `source` esté definido por una expresión regular. Ejemplo: `iif(segmentMembership.ups.aep_seg_id.status==\"exited\", \"1\", \"0\")`</li><li>`text/plain`: utilice este valor cuando el campo `source` esté definido por una plantilla de macro. Actualmente, la única plantilla de macro admitida es `metadata.segment.alias`.</li></ul> |
| `requiredMappings.source` | Cadena | Requerido | Indica el valor del campo de origen. Tipos de valores admitidos: <ul><li>Atributos de perfil XDM. Ejemplo: `personalEmail.address`. Si el atributo de origen es un atributo de perfil XDM, establezca el parámetro `sourceType` en `text/x.schema-path`.</li><li>Expresiones regulares. Ejemplo: `iif(segmentMembership.ups.aep_seg_id.status==\"exited\", \"1\", \"0\")`. Si el atributo de origen es una expresión regular, establezca el parámetro `sourceType` en `text/x.aep-xl`.</li><li>Plantillas de macros. Ejemplo:`metadata.segment.alias`. Si el atributo de origen es una plantilla de macro, establezca el parámetro `sourceType` en `text/plain`. Actualmente, la única plantilla de macro admitida es `metadata.segment.alias`.</li></ul> |
| `requiredMappings.destination` | Cadena | Requerido | Indica el valor del campo de destino. Cuando los campos de origen y de destino se especifican como asignaciones requeridas, los usuarios no pueden seleccionar ni editar ninguno de los dos campos y solo pueden ver la selección. |

{style="table-layout:auto"}

Como resultado, las secciones **[!UICONTROL Campo de Source]** y **[!UICONTROL Campo de destino]** de la interfaz de usuario de Experience Platform aparecen atenuadas.

![Imagen de las asignaciones requeridas en el flujo de activación de la interfaz de usuario.](../../assets/functionality/destination-configuration/required-mappings-2.png)

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
| `requiredMappingsOnly` | Booleano | Opcional | Cuando se establece en true , los usuarios no pueden asignar otros atributos e identidades en el flujo de activación, aparte de las asignaciones necesarias que defina en la matriz `requiredMappings`. |
| `requiredMappings.destination` | Cadena | Requerido | Indica el valor del campo de destino. Cuando solo se especifica el campo de destino, los usuarios pueden seleccionar un campo de origen para asignarlo al destino. |
| `mandatoryRequired` | Booleano | Opcional | Indica si la asignación debe marcarse como [atributo obligatorio](../../../ui/activate-batch-profile-destinations.md#mandatory-attributes). |
| `primaryKeyRequired` | Booleano | Opcional | Indica si la asignación debe marcarse como [clave de anulación de duplicación](../../../ui/activate-batch-profile-destinations.md#deduplication-keys). |

{style="table-layout:auto"}

Como resultado, la sección **[!UICONTROL Campo de destino]** de la interfaz de usuario de Experience Platform aparece atenuada, mientras que la sección **[!UICONTROL Campo de Source]** está activa y los usuarios pueden interactuar con ella. Las opciones **[!UICONTROL Clave obligatoria]** y **[!UICONTROL Clave de anulación de duplicación]** están activas y los usuarios no pueden cambiarlas.

![Imagen de las asignaciones requeridas en el flujo de activación de la interfaz de usuario.](../../assets/functionality/destination-configuration/required-mappings-1.png)

>[!ENDTABS]

## Configuración de la compatibilidad con audiencias externas {#external-audiences}

Para configurar el destino de modo que admita la activación de [audiencias generadas externamente](../../../../segmentation/ui/audience-portal.md#import-audience), incluya el fragmento de código siguiente en la sección `schemaConfig`.

```json
"schemaConfig": {
  "segmentNamespaceDenyList": [],
  ...
}
```

Consulte las descripciones de las propiedades en la [tabla](#attributes-schema) más arriba en esta página para obtener más información acerca de la funcionalidad `segmentNamespaceDenyList`.

## Pasos siguientes {#next-steps}

Después de leer este artículo, debería comprender mejor qué tipos de esquema admite Destination SDK y cómo puede configurarlo.

Para obtener más información acerca de los demás componentes de destino, consulte los siguientes artículos:

* [Autenticación del cliente](customer-authentication.md)
* [Autorización de OAuth2](oauth2-authorization.md)
* [Atributos de IU](ui-attributes.md)
* [Campos de datos del cliente](customer-data-fields.md)
* [Configuración del área de nombres de identidad](identity-namespace-configuration.md)
* [Configuraciones de asignación compatibles](supported-mapping-configurations.md)
* [Envío de destino](destination-delivery.md)
* [Configuración de metadatos de audiencia](audience-metadata-configuration.md)
* [Política de agregación](aggregation-policy.md)
* [Configuración por lotes](batch-configuration.md)
* [Cualificaciones históricas del perfil](historical-profile-qualifications.md)
