---
keywords: Experience Platform;temas populares;XDM;sistema XDM;perfil individual XDM;XDM ExperienceEvent;Evento de experiencia XDM;experienceEvent;evento de experiencia;evento de experiencia;evento de experiencia XDM;evento de experiencia XDM;ExperienceEvent;modelo de datos de experiencia;modelo de datos de experiencia;modelo de datos de experiencia;modelo de datos;esquema;esquema;solución de problemas;FAQ;faq;esquema de unión;UNION PROFILE;perfil de unión;http://ns.adobe.com/aep/errors/XDM-1010-404;http://ns.adobe.com/aep/errors/XDM-1011-404;http://ns.adobe.com/aep/errors/XDM-1012-404;http://ns.adobe.com/aep/errors/XDM-1013-404;http://ns.adobe.com/aep/errors/XDM-1014-404;http://ns.adobe.com/aep/errors/XDM-1015-404;http://ns.adobe.com/aep/errors/XDM-1016-404;http://ns.adobe.com/aep/errors/XDM-1017-404;http://ns.adobe.com/aep/errors/XDM-1521-400;http://ns.adobe.com/aep/errors/XDM-1020-400;http://ns.adobe.com/aep/errors/XDM-1021-400;http://ns.adobe.com/aep/errors/XDM-1022-400;http://ns.adobe.com/aep/errors/XDM-1023-400;http://ns.adobe.com/aep/errors/XDM-1024-400;http://ns.adobe.com/aep/errors/XDM-1006-400;http://ns.adobe.com/aep/errors/XDM-1007-400;http://ns.adobe.com/aep/errors/XDM-1008-400;http://ns.adobe.com/aep/errors/XDM-1009-400;http://ns.adobe.com/aep/errors/XDM-1526-400;http://ns.adobe.com/aep/errors/XDM-1527-400;http://ns.adobe.com/aep/errors/XDM-1528-400;XDM-1010-404;XDM-1011-404;XDM-1012-404;XDM-1013-404;XDM-1014-404;XDM-1015-404;XDM-1016-404;XDM-1017-404;XDM-1521-400;XDM-1020-400;XDM-1021-400;XDM-1022-400;XDM-1023-400;XDM-1024-400;XDM-1006-400;XDM-1007-400;XDM-1008-400;XDM-1009-400;XDM-1413-400;XDM-1526-400;XDM-1527-400;XDM-1528-400;
solution: Experience Platform
title: Guía de resolución de problemas del sistema XDM
description: Encuentre respuestas a las preguntas frecuentes acerca del Modelo de datos de experiencia (XDM), incluidos pasos para resolver errores comunes de API.
exl-id: a0c7c661-bee8-4f66-ad5c-f669c52c9de3
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '2073'
ht-degree: 0%

---

# Guía de solución de problemas del sistema XDM

Este documento proporciona respuestas a las preguntas frecuentes acerca de [!DNL Experience Data Model] (XDM) y el sistema XDM en Adobe Experience Platform, incluida una guía de solución de problemas para errores comunes. Si tiene alguna pregunta o solución de problemas relacionados con otros servicios de Platform, consulte la [guía de solución de problemas del Experience Platform](../landing/troubleshooting.md).

**[!DNL Experience Data Model](XDM)** es una especificación de código abierto que define esquemas estandarizados para la administración de experiencias del cliente. La metodología en la que [!DNL Experience Platform] se ha creado, **Sistema XDM**, pone en funcionamiento [!DNL Experience Data Model] esquemas que debe utilizar [!DNL Platform] servicios. El **[!DNL Schema Registry]** proporciona una interfaz de usuario y una API de RESTful para acceder a **[!DNL Schema Library]** dentro [!DNL Experience Platform]. Consulte la [Documentación de XDM](home.md) para obtener más información.

## Preguntas frecuentes

A continuación se muestra una lista de respuestas a las preguntas más frecuentes sobre el sistema XDM y el uso del [!DNL Schema Registry] API.

### ¿Cómo se agregan campos a un esquema?

Puede agregar campos a un esquema mediante un grupo de campos de esquema. Cada grupo de campos es compatible con una o más clases, lo que permite utilizar el grupo de campos en cualquier esquema que implemente una de esas clases compatibles. Aunque Adobe Experience Platform proporciona varios grupos de campos del sector con sus propios campos predefinidos, puede agregar sus propios campos a un esquema creando grupos de campos personalizados mediante la API o la interfaz de usuario.

Para obtener más información sobre la creación de grupos de campos en [!DNL Schema Registry] API, consulte la [guía de extremo de grupo de campos](api/field-groups.md#create). Si utiliza la interfaz de usuario de, consulte la [Tutorial del Editor de esquemas](./tutorials/create-schema-ui.md).

### ¿Cuáles son los mejores usos de los grupos de campos en comparación con los tipos de datos?

[Grupos de campos](./schema/composition.md#field-group) son componentes que definen uno o varios campos de un esquema. Los grupos de campos aplican la forma en que sus campos aparecen en la jerarquía del esquema y, por lo tanto, muestran la misma estructura en todos los esquemas en los que se incluyen. Los grupos de campos solo son compatibles con clases específicas, identificadas por sus `meta:intendedToExtend` atributo.

[Tipos de datos](./schema/composition.md#data-type) También puede proporcionar uno o más campos para un esquema. Sin embargo, a diferencia de los grupos de campos, los tipos de datos no están restringidos a una clase en particular. Esto hace que los tipos de datos sean una opción más flexible para describir estructuras de datos comunes que se pueden reutilizar en varios esquemas con clases potencialmente diferentes.

### ¿Cuál es el ID único de un esquema?

Todo [!DNL Schema Registry] Los recursos (esquemas, grupos de campos, tipos de datos y clases) tienen un URI que actúa como un ID único a efectos de referencia y búsqueda. Al ver un esquema en la API, se puede encontrar en el nivel superior `$id` y `meta:altId` atributos.

Para obtener más información, consulte la [identificación de recursos](api/getting-started.md#resource-identification) de la sección [!DNL Schema Registry] Guía de API.

### ¿Cuándo comienza un esquema a evitar cambios importantes?

Se pueden realizar cambios importantes en un esquema siempre y cuando no se haya utilizado nunca en la creación de un conjunto de datos o se haya habilitado para su uso en [[!DNL Real-Time Customer Profile]](../profile/home.md). Una vez que se ha utilizado un esquema en la creación del conjunto de datos o se ha habilitado para su uso con [!DNL Real-Time Customer Profile], las reglas de [Evolución del esquema](schema/composition.md#evolution) ser estrictamente aplicados por el sistema.

### ¿Cuál es el tamaño máximo de un tipo de campo largo?

Un tipo de campo largo es un entero con un tamaño máximo de 53 (+1) bits, lo que le da un rango potencial entre -9007199254740992 y 9007199254740992. Esto se debe a una limitación de cómo las implementaciones de JavaScript de JSON representan enteros largos.

Para obtener más información sobre los tipos de campo, consulte el documento sobre [Restricciones de tipo de campo XDM](./schema/field-constraints.md).

### ¿Cómo defino las identidades de mi esquema?

Entrada [!DNL Experience Platform], las identidades se utilizan para identificar a un sujeto (normalmente una persona individual) independientemente de las fuentes de datos que se interpreten. Se definen en esquemas marcando los campos clave como &quot;Identidad&quot;. Los campos más utilizados para la identidad incluyen la dirección de correo electrónico, el número de teléfono, [[!DNL Experience Cloud ID (ECID)]](https://experienceleague.adobe.com/docs/id-service/using/home.html?lang=es), ID de CRM y otros campos de ID único.

Los campos se pueden marcar como identidades mediante la API o la interfaz de usuario.

#### Definición de identidades en la API

En la API, las identidades se establecen creando descriptores de identidad. Los descriptores de identidad indican que una propiedad particular de un esquema es un identificador único.

Los descriptores de identidad se crean mediante una solicitud de POST al extremo /descriptors. Si se ejecuta correctamente, recibirá un estado HTTP 201 (Creado) y un objeto de respuesta que contiene los detalles del nuevo descriptor.

Para obtener más información sobre la creación de descriptores de identidad en la API, consulte el documento sobre [descriptores](api/descriptors.md) de la sección [!DNL Schema Registry] guía para desarrolladores.

#### Definición de identidades en la IU

Con el esquema abierto en el Editor de esquemas, seleccione el campo en la **[!UICONTROL Estructura]** del editor que desea marcar como una identidad. En **[!UICONTROL Propiedades del campo]** en el lado derecho, seleccione la opción **[!UICONTROL Identidad]** casilla de verificación

Para obtener más información sobre la administración de identidades en la interfaz de usuario, consulte la sección sobre [definición de campos de identidad](./tutorials/create-schema-ui.md#identity-field) de la sección Editor de esquemas.

### ¿Mi esquema necesita una identidad principal?

Las identidades principales son opcionales, ya que los esquemas pueden tener cero o uno de ellos. Sin embargo, un esquema debe tener una identidad principal para que se pueda usar en [!DNL Real-Time Customer Profile]. Consulte la [identidad](./tutorials/create-schema-ui.md#identity-field) de la sección Editor de esquemas para obtener más información.

### ¿Cómo habilito un esquema para utilizarlo en? [!DNL Real-Time Customer Profile]?

Los esquemas están habilitados para su uso en [[!DNL Real-Time Customer Profile]](../profile/home.md) mediante la adición de una etiqueta &quot;union&quot; dentro de `meta:immutableTags` del esquema. Activación de un esquema para utilizarlo con [!DNL Profile] se puede realizar mediante la API o la interfaz de usuario de.

#### Habilitar un esquema existente para [!DNL Profile] uso de la API

Realice una solicitud del PATCH para actualizar el esquema y añadir la variable `meta:immutableTags` como una matriz que contiene el valor &quot;union&quot;. Si la actualización se realiza correctamente, la respuesta mostrará el esquema actualizado que ahora contiene la etiqueta de unión.

Para obtener más información sobre el uso de la API para habilitar un esquema para utilizarlo en [!DNL Real-Time Customer Profile], consulte la [uniones](./api/unions.md) documento de la [!DNL Schema Registry] guía para desarrolladores.

#### Habilitar un esquema existente para [!DNL Profile] uso de la IU

Entrada [!DNL Experience Platform], seleccione **[!UICONTROL Esquemas]** en la barra de navegación izquierda, seleccione el nombre del esquema que desea activar en la lista de esquemas. A continuación, en el lado derecho del editor, en **[!UICONTROL Propiedades del esquema]**, seleccione **[!UICONTROL Perfil]** para activarlo.


Para obtener más información, consulte la sección sobre [uso en el perfil del cliente en tiempo real](./tutorials/create-schema-ui.md#profile) en el [!UICONTROL Editor de esquemas] tutorial.

### ¿Puedo editar un esquema de unión directamente?

Los esquemas de unión son de solo lectura y el sistema los genera automáticamente. No se pueden editar directamente. Los esquemas de unión se crean para una clase específica cuando se agrega una etiqueta &quot;union&quot; al esquema que implementa esa clase.

Para obtener más información sobre las uniones en XDM, consulte la [uniones](./api/unions.md) de la sección [!DNL Schema Registry] Guía de API.

### ¿Cómo debo dar formato a mi archivo de datos para introducir datos en el esquema?

[!DNL Experience Platform] acepta archivos de datos en [!DNL Parquet] o formato JSON. El contenido de estos archivos debe ajustarse al esquema al que hace referencia el conjunto de datos. Para obtener más información sobre las prácticas recomendadas para la ingesta de archivos de datos, consulte la [introducción a la ingesta por lotes](../ingestion/home.md).

## Errores y solución de problemas

A continuación se muestra una lista de mensajes de error que pueden aparecer al trabajar con [!DNL Schema Registry] API.

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
>Según el tipo de recurso que se recupere, este error puede utilizar cualquiera de los siguientes elementos `type` URI:
>
>* `http://ns.adobe.com/aep/errors/XDM-1010-404`
>* `http://ns.adobe.com/aep/errors/XDM-1011-404`
>* `http://ns.adobe.com/aep/errors/XDM-1012-404`
>* `http://ns.adobe.com/aep/errors/XDM-1013-404`
>* `http://ns.adobe.com/aep/errors/XDM-1014-404`
>* `http://ns.adobe.com/aep/errors/XDM-1015-404`
>* `http://ns.adobe.com/aep/errors/XDM-1016-404`
>* `http://ns.adobe.com/aep/errors/XDM-1017-404`


Para obtener más información sobre la construcción de rutas de búsqueda en la API, consulte la [contenedor](./api/getting-started.md#container) y [identificación de recursos](api/getting-started.md#resource-identification) secciones de la [!DNL Schema Registry] guía para desarrolladores.

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

### Error de validación de área de nombres

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
>Según la naturaleza específica del error de área de nombres, este error puede utilizar cualquiera de las siguientes opciones `type` URI junto con diferentes detalles del mensaje:
>
>* `http://ns.adobe.com/aep/errors/XDM-1020-400`
>* `http://ns.adobe.com/aep/errors/XDM-1021-400`
>* `http://ns.adobe.com/aep/errors/XDM-1022-400`
>* `http://ns.adobe.com/aep/errors/XDM-1023-400`
>* `http://ns.adobe.com/aep/errors/XDM-1024-400`


Puede encontrar ejemplos detallados de estructuras de datos adecuadas para los recursos XDM en la guía de API de Registro de esquemas:

* [Crear una clase personalizada](./api/classes.md#create)
* [Crear un grupo de campos personalizados](./api/field-groups.md#create)
* [Creación de un tipo de datos personalizado](./api/data-types.md#create)

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

Solicitudes de GET en [!DNL Schema Registry] La API requiere un `Accept` para que el sistema determine cómo dar formato a la respuesta. Este error se produce cuando se requiere un `Accept` falta el encabezado o no es válido.

Según el extremo que utilice, la variable `detailed-message` indica lo que una propiedad `Accept` debe tener el aspecto de para que la respuesta sea correcta. Asegúrese de haber introducido correctamente una `Accept` que es compatible con la solicitud de API que está intentando realizar antes de intentarlo de nuevo.

>[!NOTE]
>
>Según el extremo que se esté utilizando, este error puede utilizar cualquiera de las siguientes opciones `type` URI:
>
>* `http://ns.adobe.com/aep/errors/XDM-1006-400`
>* `http://ns.adobe.com/aep/errors/XDM-1007-400`
>* `http://ns.adobe.com/aep/errors/XDM-1008-400`
>* `http://ns.adobe.com/aep/errors/XDM-1009-400`


Para obtener listas de encabezados Aceptar compatibles para diferentes solicitudes de API, consulte sus secciones correspondientes en la [Guía para desarrolladores de Schema Registry](./api/overview.md).

### [!DNL Real-Time Customer Profile] errores

Los siguientes mensajes de error están asociados con operaciones implicadas en la activación de esquemas para [!DNL Real-Time Customer Profile]. Consulte la [uniones](./api/unions.md) de la sección [!DNL Schema Registry] Guía de API para obtener más información.

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

Para habilitar los esquemas que contienen descriptores de relación para su uso en [!DNL Profile], el área de nombres del campo de origen y el área de nombres principal del campo de referencia deben ser los mismos. Este mensaje de error se muestra cuando intenta habilitar un esquema que contiene un área de nombres no coincidente para su descriptor de identidad de referencia.

Asegúrese de que la variable `xdm:namespace` el valor del campo de identidad del esquema de referencia coincide con el del `xdm:identityNamespace` en el descriptor de identidad de referencia del campo de origen para resolver este problema.

Para obtener una lista de códigos de área de nombres de identidad estándar, consulte la sección sobre [áreas de nombres estándar](../identity-service/namespaces.md) en información general del área de nombres de identidad.

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

Antes de habilitar un esquema para el perfil, primero debe [creación de un descriptor de identidad principal](./api/descriptors.md#create) para el esquema o incluya un campo de mapa de identidad para que actúe en la identidad principal.

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
