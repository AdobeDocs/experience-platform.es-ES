---
keywords: Experience Platform;temas populares;XDM;sistema XDM;perfil individual XDM;XDM ExperienceEvent;Evento de experiencia XDM;experienceEvent;evento de experiencia;evento de experiencia;evento de experiencia XDM;evento de experiencia XDM;ExperienceEvent;modelo de datos de experiencia;modelo de datos de experiencia;modelo de datos de experiencia;modelo de datos;esquema;esquema;solución de problemas;FAQ;faq;esquema de unión;UNION PROFILE;perfil de unión;http://ns.adobe.com/aep/errors/XDM-1010-404;http://ns.adobe.com/aep/errors/XDM-1011-404;http://ns.adobe.com/aep/errors/XDM-1012-404;http://ns.adobe.com/aep/errors/XDM-1013-404;http://ns.adobe.com/aep/errors/XDM-1014-404;http://ns.adobe.com/aep/errors/XDM-1015-404;http://ns.adobe.com/aep/errors/XDM-1016-404;http://ns.adobe.com/aep/errors/XDM-1017-404;http://ns.adobe.com/aep/errors/XDM-1521-400;http://ns.adobe.com/aep/errors/XDM-1020-400;http://ns.adobe.com/aep/errors/XDM-1021-400;http://ns.adobe.com/aep/errors/XDM-1022-400;http://ns.adobe.com/aep/errors/XDM-1023-400;http://ns.adobe.com/aep/errors/XDM-1024-400;http://ns.adobe.com/aep/errors/XDM-1006-400;http://ns.adobe.com/aep/errors/XDM-1007-400;http://ns.adobe.com/aep/errors/XDM-1008-400;http://ns.adobe.com/aep/errors/XDM-1009-400;http://ns.adobe.com/aep/errors/XDM-1526-400;http://ns.adobe.com/aep/errors/XDM-1527-400;http://ns.adobe.com/aep/errors/XDM-1528-400;XDM-1010-404;XDM-1011-404;XDM-1012-404;XDM-1013-404;XDM-1014-404;XDM-1015-404;XDM-1016-404;XDM-1017-404;XDM-1521-400;XDM-1020-400;XDM-1021-400;XDM-1022-400;XDM-1023-400;XDM-1024-400;XDM-1006-400;XDM-1007-400;XDM-1008-400;XDM-1009-400;XDM-1413-400;XDM-1526-400;XDM-1527-400;XDM-1528-400;
solution: Experience Platform
title: Guía de resolución de problemas del sistema XDM
description: Encuentre respuestas a las preguntas frecuentes acerca del Modelo de datos de experiencia (XDM), incluidos pasos para resolver errores comunes de API.
exl-id: a0c7c661-bee8-4f66-ad5c-f669c52c9de3
source-git-commit: b345330595aadcfe2380dd1795802470b249cb4a
workflow-type: tm+mt
source-wordcount: '2347'
ht-degree: 0%

---

# Guía de solución de problemas del sistema XDM

Este documento proporciona respuestas a las preguntas más frecuentes sobre [!DNL Experience Data Model] (XDM) y el sistema XDM en Adobe Experience Platform, incluida una guía de solución de problemas para errores comunes. Si tiene preguntas o necesita solución de problemas en relación con otros servicios de Platform, consulte la [guía de solución de problemas para Experience Platform](../landing/troubleshooting.md).

**[!DNL Experience Data Model](XDM)** es una especificación de código abierto que define esquemas estandarizados para la administración de experiencias del cliente. La metodología en la que se ha creado [!DNL Experience Platform], **Sistema XDM**, pone en funcionamiento [!DNL Experience Data Model] esquemas para que los usen los servicios de [!DNL Platform]. **[!DNL Schema Registry]** proporciona una interfaz de usuario y una API RESTful para acceder a **[!DNL Schema Library]** en [!DNL Experience Platform]. Consulte la [documentación de XDM](home.md) para obtener más información.

## Preguntas frecuentes

A continuación se muestra una lista de respuestas a las preguntas más frecuentes sobre el sistema XDM y el uso de la API [!DNL Schema Registry].

## Conceptos básicos del esquema

En esta sección, puede encontrar respuestas a preguntas fundamentales sobre la estructura de esquema, el uso de campos y la identificación en el sistema XDM.

### ¿Cómo se agregan campos a un esquema?

Puede agregar campos a un esquema mediante un grupo de campos de esquema. Cada grupo de campos es compatible con una o más clases, lo que permite utilizar el grupo de campos en cualquier esquema que implemente una de esas clases compatibles. Aunque Adobe Experience Platform proporciona varios grupos de campos del sector con sus propios campos predefinidos, puede agregar sus propios campos a un esquema creando grupos de campos personalizados mediante la API o la interfaz de usuario.

Para obtener más información sobre la creación de grupos de campos en la API [!DNL Schema Registry], consulte la [guía de extremo de grupo de campos](api/field-groups.md#create). Si está usando la interfaz de usuario, vea el [tutorial del Editor de esquemas](./tutorials/create-schema-ui.md).

### ¿Cuáles son los mejores usos de los grupos de campos en comparación con los tipos de datos?

[Los grupos de campos](./schema/composition.md#field-group) son componentes que definen uno o más campos de un esquema. Los grupos de campos aplican la forma en que sus campos aparecen en la jerarquía del esquema y, por lo tanto, muestran la misma estructura en todos los esquemas en los que se incluyen. Los grupos de campos solo son compatibles con clases específicas, identificadas por su atributo `meta:intendedToExtend`.

[Los tipos de datos](./schema/composition.md#data-type) también pueden proporcionar uno o más campos para un esquema. Sin embargo, a diferencia de los grupos de campos, los tipos de datos no están restringidos a una clase en particular. Esto hace que los tipos de datos sean una opción más flexible para describir estructuras de datos comunes que se pueden reutilizar en varios esquemas con clases potencialmente diferentes.

### ¿Cuál es el ID único de un esquema?

Todos los recursos de [!DNL Schema Registry] (esquemas, grupos de campos, tipos de datos y clases) tienen un URI que actúa como un ID único a efectos de referencia y búsqueda. Al ver un esquema en la API, se puede encontrar en los atributos de nivel superior `$id` y `meta:altId`.

Para obtener más información, consulte la sección [identificación de recursos](api/getting-started.md#resource-identification) en la guía de API [!DNL Schema Registry].

### ¿Cuál es el tamaño máximo de un tipo de campo largo?

Un tipo de campo largo es un entero con un tamaño máximo de 53 (+1) bits, lo que le da un rango potencial entre -9007199254740992 y 9007199254740992. Esto se debe a una limitación de cómo las implementaciones de JavaScript de JSON representan enteros largos.

Para obtener más información sobre los tipos de campo, consulte el documento sobre [restricciones de tipo de campo XDM](./schema/field-constraints.md).

### ¿Qué es meta:AltId?

`meta:altId` es un identificador único para un esquema. `meta:altId` proporciona un identificador fácil de hacer referencia para utilizarlo en llamadas API. Este ID evita la necesidad de codificarlo/descodificarlo cada vez que se utiliza con el formato URI JSON.
<!-- (Needs clarification - How do I retrieve it INCOMPLETE) ... -->

<!-- ### How can I generate a sample payload for a schema? -->

<!-- No Answer available.  -->
<!-- INCOMPLETE ... -->

### ¿Cuáles son las restricciones de uso de un tipo de datos de mapa?

XDM impone las siguientes restricciones al uso de este tipo de datos:

- Los tipos de mapa DEBEN ser de tipo objeto.
- Los tipos de mapa NO DEBEN tener propiedades definidas (es decir, definen objetos &quot;vacíos&quot;).
- Los tipos de mapa DEBEN incluir un campo additionalProperties.type que describa los valores que se pueden colocar dentro del mapa, ya sea cadena o entero.
- La segmentación de varias entidades solo se puede definir en función de las claves de asignación y no de los valores.
- Las audiencias de la cuenta no admiten mapas.

Vea las [restricciones de uso para objetos de mapa](./ui/fields/map.md#restrictions) para obtener más detalles.

>[!NOTE]
>
>No se admiten mapas multinivel ni mapas de mapas.

<!-- You cannot create a complex map object. However, you can define map fields in the Schema Editor. See the guide on [defining map fields in the UI](./ui/fields/map.md) for more information. -->

<!-- ### How do I create a complex map object using APIs? -->

<!-- You cannot create a complex map object. -->

<!-- ### How can I manage schema inheritance in Adobe Experience Platform? -->

<!-- No Answer available.  -->
<!-- INCOMPLETE ... -->

## Esquema Identity Management

Esta sección contiene respuestas a preguntas comunes sobre la definición y administración de identidades dentro de los esquemas.

### ¿Cómo defino las identidades de mi esquema?

En [!DNL Experience Platform], las identidades se utilizan para identificar a un sujeto (normalmente, una persona individual) independientemente de las fuentes de datos que se interpreten. Se definen en esquemas marcando los campos clave como &quot;Identidad&quot;. Los campos más utilizados para la identidad incluyen la dirección de correo electrónico, el número de teléfono, [[!DNL Experience Cloud ID (ECID)]](https://experienceleague.adobe.com/docs/id-service/using/home.html?lang=es), el ID de CRM y otros campos de ID únicos.

Los campos se pueden marcar como identidades mediante la API o la interfaz de usuario.

### Definición de identidades en la API

En la API, las identidades se establecen creando descriptores de identidad. Los descriptores de identidad indican que una propiedad particular de un esquema es un identificador único.

Los descriptores de identidad se crean mediante una solicitud de POST al extremo /descriptors. Si se ejecuta correctamente, recibirá un estado HTTP 201 (Creado) y un objeto de respuesta que contiene los detalles del nuevo descriptor.

Para obtener más información sobre la creación de descriptores de identidad en la API, consulte el documento en la sección [descriptores](api/descriptors.md) en la guía para desarrolladores de [!DNL Schema Registry].

### Definición de identidades en la IU

Con el esquema abierto en el Editor de esquemas, seleccione el campo de la sección **[!UICONTROL Estructura]** del editor que desee marcar como identidad. En **[!UICONTROL Propiedades del campo]**, en el lado derecho, seleccione la casilla de verificación **[!UICONTROL Identidad]**.

Para obtener más información sobre la administración de identidades en la interfaz de usuario, consulte la sección sobre [definición de campos de identidad](./tutorials/create-schema-ui.md#identity-field) en el tutorial del Editor de esquemas.

### ¿Mi esquema necesita una identidad principal?

Las identidades principales son opcionales, ya que los esquemas pueden tener cero o uno de ellos. Sin embargo, un esquema debe tener una identidad principal para que se pueda usar en [!DNL Real-Time Customer Profile]. Consulte la sección [identity](./tutorials/create-schema-ui.md#identity-field) del tutorial del editor de esquemas para obtener más información.

## Habilitación del perfil de esquema

En esta sección se proporciona orientación sobre la activación de esquemas para utilizarlos con el Perfil del cliente en tiempo real.

### ¿Cómo habilito un esquema para utilizarlo en [!DNL Real-Time Customer Profile]?

Los esquemas están habilitados para su uso en [[!DNL Real-Time Customer Profile]](../profile/home.md) mediante la adición de una etiqueta &quot;union&quot; dentro del atributo `meta:immutableTags` del esquema. Se puede habilitar un esquema para usarlo con [!DNL Profile] mediante la API o la interfaz de usuario.

### Habilitando un esquema existente para [!DNL Profile] mediante la API

Realice una solicitud del PATCH para actualizar el esquema y agregar el atributo `meta:immutableTags` como una matriz que contenga el valor &quot;union&quot;. Si la actualización se realiza correctamente, la respuesta mostrará el esquema actualizado que ahora contiene la etiqueta de unión.

Para obtener más información sobre cómo usar la API para habilitar un esquema para utilizarlo en [!DNL Real-Time Customer Profile], consulte el documento [union](./api/unions.md) de la guía para desarrolladores de [!DNL Schema Registry].

### Habilitando un esquema existente para [!DNL Profile] mediante la interfaz de usuario

En [!DNL Experience Platform], seleccione **[!UICONTROL Esquemas]** en el panel de navegación izquierdo y seleccione el nombre del esquema que desea habilitar de la lista de esquemas. A continuación, en el lado derecho del editor en **[!UICONTROL Propiedades del esquema]**, seleccione **[!UICONTROL Perfil]** para activarlo.

Para obtener más información, consulte la sección sobre [usar en Real-Time Customer Profile](./tutorials/create-schema-ui.md#profile) en el tutorial de [!UICONTROL Editor de esquemas].

### Cuando los datos de Adobe Analytics se importan como origen, ¿está habilitado el esquema creado automáticamente para el perfil?

El esquema no se activa automáticamente para el perfil del cliente en tiempo real. Debe habilitar explícitamente el conjunto de datos para el perfil en función del esquema que esté habilitado para el perfil. Consulte la documentación para conocer los [pasos y requisitos necesarios para habilitar un conjunto de datos para utilizarlo en el perfil del cliente en tiempo real](../catalog/datasets/user-guide.md#enable-profile).

### ¿Puedo eliminar esquemas con perfil habilitado?

No puede eliminar un esquema una vez habilitado para el Perfil del cliente en tiempo real. Una vez que un esquema está habilitado para el perfil, no se puede deshabilitar ni eliminar, y los campos no se pueden eliminar del esquema. Por lo tanto, es crucial planificar y verificar cuidadosamente la configuración del esquema antes de habilitarla para el perfil. Sin embargo, puede eliminar un conjunto de datos con perfil habilitado. Encontrará información aquí: <https://experienceleague.adobe.com/en/docs/experience-platform/catalog/datasets/user-guide#delete-a-profile-enabled-dataset>

Si ya no desea que se use un esquema con perfil habilitado, se recomienda cambiar el nombre del esquema para incluir **No usar** o **Inactivo**.

## Modificación y restricciones del esquema

En esta sección se proporcionan aclaraciones sobre las reglas de modificación de esquemas y la prevención de cambios importantes.

### ¿Cuándo comienza un esquema a evitar cambios importantes?

Se pueden realizar cambios importantes en un esquema siempre y cuando no se haya utilizado nunca en la creación de un conjunto de datos o se haya habilitado para su uso en [[!DNL Real-Time Customer Profile]](../profile/home.md). Una vez que se ha utilizado un esquema en la creación del conjunto de datos o se ha habilitado para su uso con [!DNL Real-Time Customer Profile], el sistema aplica estrictamente las reglas de [Evolución del esquema](schema/composition.md#evolution).

### ¿Puedo editar un esquema de unión directamente?

Los esquemas de unión son de solo lectura y el sistema los genera automáticamente. No se pueden editar directamente. Los esquemas de unión se crean para una clase específica cuando se agrega una etiqueta &quot;union&quot; al esquema que implementa esa clase.

Para obtener más información sobre las uniones en XDM, consulte la sección [union](./api/unions.md) en la guía de API [!DNL Schema Registry].

### ¿Cómo debo dar formato a mi archivo de datos para introducir datos en el esquema?

[!DNL Experience Platform] acepta archivos de datos en formato [!DNL Parquet] o JSON. El contenido de estos archivos debe ajustarse al esquema al que hace referencia el conjunto de datos. Para obtener más información sobre las prácticas recomendadas para la ingesta de archivos de datos, consulte la [descripción general de la ingesta por lotes](../ingestion/home.md).

### ¿Cómo puedo convertir un esquema en un esquema de solo lectura?

Actualmente, un esquema no se puede convertir en solo lectura.

## Errores y solución de problemas

A continuación se muestra una lista de mensajes de error que pueden aparecer al trabajar con la API [!DNL Schema Registry].

### Recurso no encontrado

```json
{
    "type": "http://ns.adobe.com/aep/errors/XDM-1010-404",
    "title": "Resource not found",
    "status": 404,
    "report": {
        "registryRequestId": "a15996b5-5133-4cec-9bf7-7d1207904ae3",
        "timestamp": "06-01-2021 04:11:06",
        "detailed-message": "The requested class resource https://ns.adobe.com/{TENANT_ID}/classes/11447bb484d4599d2cd9b0aseefff78b463cbbde1527f498 with version 1 is not found.",
        "sub-errors": []
    },
    "detail": "The requested class resource https://ns.adobe.com/{TENANT_ID}/classes/11447bb484d4599d2cd9b0aseefff78b463cbbde1527f498 with version 1 is not found."
}
```

Este error se muestra cuando el sistema no ha podido encontrar un recurso en particular. Es posible que el recurso se haya eliminado o que la ruta de la llamada de API no sea válida. Asegúrese de haber introducido una ruta válida para la llamada de API antes de intentarlo de nuevo. Es posible que desee comprobar que ha introducido el ID correcto para el recurso y que la ruta tiene el espacio de nombres correcto con el contenedor adecuado (global o inquilino).

>[!NOTE]
>
>Según el tipo de recurso que se recupere, este error puede utilizar cualquiera de los siguientes URI `type`:
>
>- `http://ns.adobe.com/aep/errors/XDM-1010-404`
>- `http://ns.adobe.com/aep/errors/XDM-1011-404`
>- `http://ns.adobe.com/aep/errors/XDM-1012-404`
>- `http://ns.adobe.com/aep/errors/XDM-1013-404`
>- `http://ns.adobe.com/aep/errors/XDM-1014-404`
>- `http://ns.adobe.com/aep/errors/XDM-1015-404`
>- `http://ns.adobe.com/aep/errors/XDM-1016-404`
>- `http://ns.adobe.com/aep/errors/XDM-1017-404`

Para obtener más información sobre la construcción de rutas de búsqueda en la API, consulte las secciones [contenedor](./api/getting-started.md#container) e [identificación de recursos](api/getting-started.md#resource-identification) en la guía para desarrolladores de [!DNL Schema Registry].

### El título no es único

```json
{
    "type": "http://ns.adobe.com/aep/errors/XDM-1521-400",
    "title": "Title not unique",
    "status": 400,
    "report": {
        "registryRequestId": "a15996b5-5133-4cec-9bf7-7d1207904ae3",
        "timestamp": "06-01-2021 04:11:06",
        "detailed-message": "Object titles must be unique. An object https://ns.adobe.com/{TENANT_ID}/classes/11447bb484d4599d2cd9b0aseefff78b463cbbde1527f498 already exists with the same title",
        "sub-errors": []
    },
    "detail": "Object titles must be unique. An object https://ns.adobe.com/{TENANT_ID}/classes/11447bb484d4599d2cd9b0aseefff78b463cbbde1527f498 already exists with the same title"
}
```

Este mensaje de error se muestra cuando intenta crear un recurso con un título que ya está siendo utilizado por otro recurso. Los títulos deben ser únicos en todos los tipos de recursos. Por ejemplo, si intenta crear un grupo de campos con un título que ya está siendo utilizado por un esquema, recibirá este error.

### Error de validación de espacio de nombres

```json
{
    "type": "http://ns.adobe.com/aep/errors/XDM-1021-400",
    "title": "Namespace validation error",
    "status": 400,
    "report": {
        "registryRequestId": "a15996b5-5133-4cec-9bf7-7d1207904ae3",
        "timestamp": "06-01-2021 04:11:06",
        "detailed-message": "A custom field is defined under an invalid namespace. All custom fields must be defined under a top-level field named {TENANT_ID}.",
        "sub-errors": []
    },
    "detail": "A custom field is defined under an invalid namespace. All custom fields must be defined under a top-level field named {TENANT_ID}."
}
```

Este mensaje de error se muestra cuando intenta crear un recurso con campos con un espacio de nombres incorrecto o cuando agrega campos con un espacio de nombres incorrecto a un recurso existente.

Los recursos definidos por su organización deben asignar un área de nombres a sus campos en el ID de inquilino para evitar conflictos con otros recursos del sector y del proveedor. Al crear un esquema con grupos de campos estándar, los campos personalizados que agregue dentro de la estructura de esos grupos de campos también deben tener un espacio de nombres en el ID de inquilino.

>[!NOTE]
>
>Según la naturaleza específica del error de área de nombres, este error puede utilizar cualquiera de los siguientes URI `type` junto con diferentes detalles del mensaje:
>
>- `http://ns.adobe.com/aep/errors/XDM-1020-400`
>- `http://ns.adobe.com/aep/errors/XDM-1021-400`
>- `http://ns.adobe.com/aep/errors/XDM-1022-400`
>- `http://ns.adobe.com/aep/errors/XDM-1023-400`
>- `http://ns.adobe.com/aep/errors/XDM-1024-400`

Puede encontrar ejemplos detallados de estructuras de datos adecuadas para los recursos XDM en la guía de API de Registro de esquemas:

- [Crear una clase personalizada](./api/classes.md#create)
- [Crear un grupo de campos personalizados](./api/field-groups.md#create)
- [Creación de un tipo de datos personalizado](./api/data-types.md#create)

### Encabezado Aceptar no válido

```json
{
    "type": "http://ns.adobe.com/aep/errors/XDM-1006-400",
    "title": "Accept header invalid",
    "status": 400,
    "report": {
        "registryRequestId": "a15996b5-5133-4cec-9bf7-7d1207904ae3",
        "timestamp": "06-01-2021 04:11:06",
        "detailed-message": "The supplied Accept header is not valid: application/vnd.adobe.xed+json;version=1 - A valid Accept value should look like application/vnd.adobe.{xed|xdm}+json",
        "sub-errors": []
    },
    "detail": "The supplied Accept header is not valid: application/vnd.adobe.xed+json;version=1 - A valid Accept value should look like application/vnd.adobe.{xed|xdm}+json"
}
```

Las solicitudes de GET en la API [!DNL Schema Registry] requieren un encabezado `Accept` para que el sistema determine cómo dar formato a la respuesta. Este error se produce cuando falta o no es válido un encabezado `Accept` necesario.

Según el extremo que esté utilizando, la propiedad `detailed-message` indica el aspecto que debería tener un encabezado `Accept` válido para obtener una respuesta correcta. Asegúrese de haber escrito correctamente un encabezado `Accept` compatible con la solicitud de API que está intentando realizar antes de intentarlo de nuevo.

>[!NOTE]
>
>Según el extremo que se esté usando, este error puede usar cualquiera de los siguientes URI `type`:
>
>- `http://ns.adobe.com/aep/errors/XDM-1006-400`
>- `http://ns.adobe.com/aep/errors/XDM-1007-400`
>- `http://ns.adobe.com/aep/errors/XDM-1008-400`
>- `http://ns.adobe.com/aep/errors/XDM-1009-400`

Para obtener listas de encabezados Aceptar compatibles para diferentes solicitudes de API, consulte sus secciones correspondientes en la [Guía para desarrolladores de Schema Registry](./api/overview.md).

### [!DNL Real-Time Customer Profile] errores

Los siguientes mensajes de error están asociados con operaciones involucradas en la habilitación de esquemas para [!DNL Real-Time Customer Profile]. Consulte la sección [union](./api/unions.md) en la guía de la API [!DNL Schema Registry] para obtener más información.

#### Debe haber un descriptor de identidad de referencia

```json
{
    "type": "http://ns.adobe.com/aep/errors/XDM-1526-400",
    "title": "Union descriptor validation error",
    "status": 400,
    "report": {
        "registryRequestId": "a15996b5-5133-4cec-9bf7-7d1207904ae3",
        "timestamp": "06-01-2021 04:11:06",
        "detailed-message": "If a schema contains properties that are associated with an xdm:descriptorOneToOne descriptor, those properties must also have a xdm:descriptorReferenceIdentity descriptor for that schema to participate in a union.",
        "sub-errors": []
    },
    "detail": "If a schema contains properties that are associated with an xdm:descriptorOneToOne descriptor, those properties must also have a xdm:descriptorReferenceIdentity descriptor for that schema to participate in a union."
}
```

Este mensaje de error se muestra cuando intenta habilitar un esquema para [!DNL Profile] y una de sus propiedades contiene un descriptor de relación sin un descriptor de identidad de referencia. Añada un descriptor de identidad de referencia al campo de esquema en cuestión para resolver este error.

#### Las áreas de nombres del campo descriptor de identidad de referencia y el esquema de destino deben coincidir

```json
{
    "type": "http://ns.adobe.com/aep/errors/XDM-1527-400",
    "title": "Union descriptor validation error",
    "status": 400,
    "report": {
        "registryRequestId": "a15996b5-5133-4cec-9bf7-7d1207904ae3",
        "timestamp": "06-01-2021 04:11:06",
        "detailed-message": "If both schemas from an existing xdm:descriptorOneToOne descriptor are promoted to union, and one of those schemas contains a primary identity, the xdm:identityNamespace of the source schema's descriptorReferenceIdentity field must match the xdm:namespace field of destination schema's xdm:descriptorIdentity field.",
        "sub-errors": []
    },
    "detail": "If both schemas from an existing xdm:descriptorOneToOne descriptor are promoted to union, and one of those schemas contains a primary identity, the xdm:identityNamespace of the source schema's descriptorReferenceIdentity field must match the xdm:namespace field of destination schema's xdm:descriptorIdentity field."
}
```

>[!NOTE]
>
>Para este error, el &quot;esquema de destino&quot; hace referencia al esquema de referencia en la relación.

Para habilitar los esquemas que contienen descriptores de relación para su uso en [!DNL Profile], el espacio de nombres del campo de origen y el espacio de nombres principal del campo de referencia deben ser iguales. Este mensaje de error se muestra cuando intenta habilitar un esquema que contiene un área de nombres no coincidente para su descriptor de identidad de referencia.

Asegúrese de que el valor `xdm:namespace` del campo de identidad del esquema de referencia coincida con el de la propiedad `xdm:identityNamespace` en el descriptor de identidad de referencia del campo de origen para resolver este problema.

Para obtener una lista de códigos de área de nombres de identidad estándar, consulte la sección sobre [áreas de nombres estándar](../identity-service/features/namespaces.md) en la descripción general del área de nombres de identidad.

#### El esquema debe incluir un identityMap o una identidad principal

```json
{
    "type": "http://ns.adobe.com/aep/errors/XDM-1528-400",
    "title": "Union descriptor validation error",
    "status": 400,
    "report": {
        "registryRequestId": "a15996b5-5133-4cec-9bf7-7d1207904ae3",
        "timestamp": "06-01-2021 04:11:06",
        "detailed-message": "To participate in a union, a schema must include an identityMap fieldgroup or a primary identity descriptor.",
        "sub-errors": []
    },
    "detail": "To participate in a union, a schema must include an identityMap fieldgroup or a primary identity descriptor."
}
```

Antes de habilitar un esquema para el perfil, primero debe [crear un descriptor de identidad principal](./api/descriptors.md#create) para el esquema o incluir un campo de mapa de identidad para que actúe en la identidad principal.

#### No se pueden combinar tipos de datos incompatibles

```json
{
    "type": "http://ns.adobe.com/aep/errors/XDM-1413-400",
    "title": "Merge Schema Error",
    "status": 400,
    "report": {
        "registryRequestId": "a15996b5-5133-4cec-9bf7-7d1207904ae3",
        "timestamp": "06-01-2021 04:11:06",
        "detailed-message": "Cannot merge incompatible data types. The path /person/name has already been defined in schema (id=0238be93d3e7a06aec5e0655955901ec) using a different data type. Types: string, object",
        "sub-errors": []
    },
    "detail": "Cannot merge incompatible data types. The path /person/name has already been defined in schema (id=0238be93d3e7a06aec5e0655955901ec) using a different data type. Types: string, object"
}
```

Todos los esquemas habilitados para perfiles que pertenecen a la misma clase deben poder combinarse para construir el esquema de unión para esa clase. Este error aparece cuando intenta agregar un campo a un esquema cuya ruta está compartida por otro esquema con perfil habilitado y el tipo de datos es diferente del original. Dado que los esquemas están habilitados para perfiles y contienen la misma ruta de campo, Profile intentaría combinar estos dos campos en uno al construir el esquema de unión. Dado que no se pueden combinar distintos tipos de datos, esto se consideraría un conflicto de combinación y no está permitido.

Para resolver el problema, elija un nombre diferente para el campo o anídelo en un objeto con espacio de nombres único para evitar conflictos de combinación con otros esquemas habilitados para perfiles de la misma clase con campos similares.
