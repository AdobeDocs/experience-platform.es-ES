---
keywords: Experience Platform;inicio;temas populares;XDM;sistema XDM;perfil individual XDM;ExperienceEvent XDM;Evento de experiencia XDM;experienceEvent;evento de experiencias;evento de experiencias XDM;ExperienceEvent XDM;modelo de datos de experiencia;modelo de datos de experiencia;modelo de datos de experiencia;modelo de datos;esquema;solución de problemas;preguntas frecuentes;faq;esquema de unión;UNION PROFILE;perfil de unión;http://ns.adobe.com/aep/errors/XDM-1010-404;http://ns.adobe.com/aep/errors/XDM-1011-404;http://ns.adobe.com/aep/errors/XDM-1012-404;http://ns.adobe.com/aep/errors/XDM-1013-404;http://ns.adobe.com/aep/errors/XDM-1014-404;http://ns.adobe.com/aep/errors/XDM-1015-404;http://ns.adobe.com/aep/errors/XDM-1016-404;http://ns.adobe.com/aep/errors/XDM-1017-404;http://ns.adobe.com/aep/errors/XDM-1521-400;http://ns.adobe.com/aep/errors/XDM-1020-400;http://ns.adobe.com/aep/errors/XDM-1021-400;http://ns.adobe.com/aep/errors/XDM-1022-400;http://ns.adobe.com/aep/errors/XDM-1023-400;http://ns.adobe.com/aep/errors/XDM-1024-400;http://ns.adobe.com/aep/errors/XDM-1006-400;http://ns.adobe.com/aep/errors/XDM-1007-400;http://ns.adobe.com/aep/errors/XDM-1008-400;http://ns.adobe.com/aep/errors/XDM-1009-400;http://ns.adobe.com/aep/errors/XDM-1526-400;http://ns.adobe.com/aep/errors/XDM-1527-400;http://ns.adobe.com/aep/errors/XDM-1528-400;
solution: Experience Platform
title: Guía de solución de problemas del sistema XDM
description: Encuentre respuestas a las preguntas más frecuentes sobre Experience Data Model (XDM), incluidos pasos para resolver errores comunes de API.
topic-legacy: troubleshooting
exl-id: a0c7c661-bee8-4f66-ad5c-f669c52c9de3
source-git-commit: 415938f6f3aeec342774b73d1ae5f2dc0e27349c
workflow-type: tm+mt
source-wordcount: '1898'
ht-degree: 0%

---

# Guía de solución de problemas del sistema XDM

Este documento proporciona respuestas a las preguntas más frecuentes sobre [!DNL Experience Data Model] (XDM) y el sistema XDM en Adobe Experience Platform, incluida una guía de solución de problemas para errores comunes. Para preguntas y solución de problemas relacionados con otros servicios de Platform, consulte la [guía de solución de problemas del Experience Platform](../landing/troubleshooting.md).

**[!DNL Experience Data Model](XDM)** es una especificación de código abierto que define esquemas estandarizados para la administración de experiencias del cliente. La metodología en la que se crea [!DNL Experience Platform], **XDM System**, operacionaliza los [!DNL Experience Data Model] esquemas para su uso por los servicios [!DNL Platform]. El **[!DNL Schema Registry]** proporciona una interfaz de usuario y una API RESTful para acceder al **[!DNL Schema Library]** dentro de [!DNL Experience Platform]. Consulte la [documentación de XDM](home.md) para obtener más información.

## Preguntas frecuentes

A continuación se ofrece una lista de respuestas a las preguntas más frecuentes sobre el sistema XDM y el uso de la API [!DNL Schema Registry].

### ¿Cómo se agregan campos a un esquema?

Puede añadir campos a un esquema utilizando un grupo de campos de esquema. Cada grupo de campos es compatible con una o más clases, lo que permite utilizar el grupo de campos en cualquier esquema que implemente una de esas clases compatibles. Aunque Adobe Experience Platform proporciona varios grupos de campos del sector con sus propios campos predefinidos, puede añadir sus propios campos a un esquema creando grupos de campos personalizados mediante la API o la interfaz de usuario.

Para obtener más información sobre la creación de grupos de campos en la API [!DNL Schema Registry], consulte la [guía de extremo de grupo de campos](api/field-groups.md#create). Si utiliza la interfaz de usuario de , consulte el tutorial [Editor de esquemas](./tutorials/create-schema-ui.md).

### ¿Cuáles son los mejores usos para los grupos de campos frente a los tipos de datos?

[Los ](./schema/composition.md#field-group) grupos de campos son componentes que definen uno o más campos de un esquema. Los grupos de campos refuerzan la forma en que sus campos aparecen en la jerarquía del esquema y, por lo tanto, muestran la misma estructura en cada esquema en el que están incluidos. Los grupos de campos solo son compatibles con clases específicas, tal como se identifican con su atributo `meta:intendedToExtend`.

[Los ](./schema/composition.md#data-type) tipos de datos también pueden proporcionar uno o más campos para un esquema. Sin embargo, a diferencia de los grupos de campos, los tipos de datos no están restringidos a una clase en particular. Esto hace que los tipos de datos sean una opción más flexible para describir estructuras de datos comunes que se pueden reutilizar en varios esquemas con clases potencialmente diferentes.

### ¿Cuál es el ID exclusivo de un esquema?

Todos los [!DNL Schema Registry] recursos (esquemas, grupos de campos, tipos de datos, clases) tienen un URI que actúa como ID único con fines de referencia y búsqueda. Al ver un esquema en la API, se puede encontrar en los atributos `$id` y `meta:altId` de nivel superior.

Para obtener más información, consulte la sección [identificación de recursos](api/getting-started.md#resource-identification) en la guía de API [!DNL Schema Registry].

### ¿Cuándo comienza un esquema a impedir que se rompan los cambios?

Los cambios que rompen se pueden realizar en un esquema siempre y cuando nunca se haya utilizado en la creación de un conjunto de datos o se haya habilitado para su uso en [[!DNL Real-time Customer Profile]](../profile/home.md). Una vez que se ha utilizado un esquema en la creación del conjunto de datos o se ha habilitado para utilizarlo con [!DNL Real-time Customer Profile], el sistema aplica estrictamente las reglas de [Evolución del esquema](schema/composition.md#evolution).

### ¿Cuál es el tamaño máximo de un tipo de campo largo?

Un tipo de campo largo es un número entero con un tamaño máximo de 53(+1) bits, lo que le proporciona un rango potencial entre -9007199254740992 y 9007199254740992. Esto se debe a una limitación de cómo las implementaciones de JavaScript de JSON representan enteros largos.

Para obtener más información sobre los tipos de campo, consulte el documento sobre [restricciones de tipo de campo XDM](./schema/field-constraints.md).

### ¿Cómo puedo definir identidades para mi esquema?

En [!DNL Experience Platform], las identidades se utilizan para identificar un sujeto (normalmente una persona individual) independientemente de las fuentes de datos que se interpreten. Se definen en esquemas marcando los campos clave como &quot;Identidad&quot;. Los campos de identidad que se utilizan con más frecuencia incluyen dirección de correo electrónico, número de teléfono, [[!DNL Experience Cloud ID (ECID)]](https://experienceleague.adobe.com/docs/id-service/using/home.html), ID de CRM y otros campos de ID únicos.

Los campos se pueden marcar como identidades mediante la API o la interfaz de usuario.

#### Definición de identidades en la API

En la API, las identidades se establecen creando descriptores de identidad. Los descriptores de identidad indican que una propiedad concreta de un esquema es un identificador único.

Los descriptores de identidad se crean mediante una solicitud de POST al extremo /descriptors . Si se realiza correctamente, recibirá un Estado HTTP 201 (Creado) y un objeto Response que contiene los detalles del nuevo descriptor.

Para obtener más información sobre la creación de descriptores de identidad en la API, consulte el documento sobre la sección [descriptores](api/descriptors.md) en la guía para desarrolladores de [!DNL Schema Registry].

#### Definición de identidades en la interfaz de usuario

Con el esquema abierto en el Editor de esquemas, seleccione el campo en la sección **[!UICONTROL Structure]** del editor que desea marcar como identidad. En **[!UICONTROL Propiedades del campo]** en el lado derecho, seleccione la casilla **[!UICONTROL Identidad]**.

Para obtener más información sobre la administración de identidades en la interfaz de usuario, consulte la sección [definición de campos de identidad](./tutorials/create-schema-ui.md#identity-field) en el tutorial Editor de esquemas.

### ¿Mi esquema necesita una identidad principal?

Las identidades principales son opcionales, ya que los esquemas pueden tener cero o uno de ellos. Sin embargo, un esquema debe tener una identidad principal para que el esquema esté habilitado para utilizarse en [!DNL Real-time Customer Profile]. Consulte la sección [identity](./tutorials/create-schema-ui.md#identity-field) del tutorial Editor de esquemas para obtener más información.

### ¿Cómo se habilita un esquema para su uso en [!DNL Real-time Customer Profile]?

Los esquemas se habilitan para su uso en [[!DNL Real-time Customer Profile]](../profile/home.md) mediante la adición de una etiqueta &quot;union&quot; dentro del atributo `meta:immutableTags` del esquema. La activación de un esquema para su uso con [!DNL Profile] se puede realizar mediante la API o la interfaz de usuario.

#### Activación de un esquema existente para [!DNL Profile] mediante la API

Realice una solicitud de PATCH para actualizar el esquema y añadir el atributo `meta:immutableTags` como una matriz que contenga el valor &quot;union&quot;. Si la actualización se realiza correctamente, la respuesta mostrará el esquema actualizado que ahora contiene la etiqueta de unión.

Para obtener más información sobre el uso de la API para habilitar un esquema para utilizarlo en [!DNL Real-time Customer Profile], consulte el documento [union](./api/unions.md) de la guía para desarrolladores de [!DNL Schema Registry].

#### Activación de un esquema existente para [!DNL Profile] mediante la interfaz de usuario

En [!DNL Experience Platform], seleccione **[!UICONTROL Esquemas]** en el panel de navegación izquierdo y seleccione el nombre del esquema que desea habilitar en la lista de esquemas. A continuación, en el lado derecho del editor, en **[!UICONTROL Propiedades del esquema]**, seleccione **[!UICONTROL Perfil]** para activarlo.


Para obtener más información, consulte la sección [use in Real-time Customer Profile](./tutorials/create-schema-ui.md#profile) en el tutorial [!UICONTROL Editor de esquemas].

### ¿Puedo editar un esquema de unión directamente?

Los esquemas de unión son de solo lectura y el sistema los genera automáticamente. No se pueden editar directamente. Los esquemas de unión se crean para una clase específica cuando se agrega una etiqueta &quot;unión&quot; al esquema que implementa esa clase.

Para obtener más información sobre las uniones en XDM, consulte la sección [union](./api/unions.md) en la guía de API [!DNL Schema Registry].

### ¿Cómo debo formatear mi archivo de datos para introducir datos en mi esquema?

[!DNL Experience Platform] acepta archivos de datos en formato  [!DNL Parquet] o JSON. El contenido de estos archivos debe cumplir el esquema al que hace referencia el conjunto de datos. Para obtener más información sobre las prácticas recomendadas para la ingesta de archivos de datos, consulte la [información general sobre la ingesta por lotes](../ingestion/home.md).

## Errores y solución de problemas

A continuación se muestra una lista de mensajes de error que puede encontrar al trabajar con la API [!DNL Schema Registry].

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

Este error se muestra cuando el sistema no pudo encontrar un recurso en particular. Es posible que el recurso se haya eliminado o que la ruta de acceso de la llamada de API no sea válida. Asegúrese de haber introducido una ruta válida para la llamada de API antes de intentarlo de nuevo. Es posible que desee comprobar que ha introducido el ID correcto para el recurso y que la ruta tiene un espacio de nombres adecuado con el contenedor apropiado (global o inquilino).

>[!NOTE]
>
>Según el tipo de recurso que se recupere, este error puede utilizar cualquiera de los siguientes URI `type`:
>
>* `http://ns.adobe.com/aep/errors/XDM-1010-404`
>* `http://ns.adobe.com/aep/errors/XDM-1011-404`
>* `http://ns.adobe.com/aep/errors/XDM-1012-404`
>* `http://ns.adobe.com/aep/errors/XDM-1013-404`
>* `http://ns.adobe.com/aep/errors/XDM-1014-404`
>* `http://ns.adobe.com/aep/errors/XDM-1015-404`
>* `http://ns.adobe.com/aep/errors/XDM-1016-404`
>* `http://ns.adobe.com/aep/errors/XDM-1017-404`


Para obtener más información sobre la construcción de rutas de búsqueda en la API, consulte las secciones [container](./api/getting-started.md#container) e [resource identification](api/getting-started.md#resource-identification) en la guía para desarrolladores de [!DNL Schema Registry].

### Título no único

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

Este mensaje de error se muestra cuando intenta crear un recurso con un título que otro recurso ya está utilizando. Los títulos deben ser únicos en todos los tipos de recursos. Por ejemplo, si intenta crear un grupo de campos con un título que ya esté utilizando un esquema, recibirá este error.

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

Este mensaje de error se muestra cuando intenta crear un recurso con campos con espacio de nombres incorrecto o agregar campos con espacio de nombres incorrecto a un recurso existente.

Los recursos definidos por su organización de IMS deben establecer el espacio de nombres de sus campos en el ID de inquilino para evitar conflictos con otros recursos del sector y del proveedor. Al crear un esquema utilizando grupos de campos estándar, los campos personalizados que agregue dentro de la estructura de esos grupos de campos también deben tener espacio de nombres en el ID de inquilino.

>[!NOTE]
>
>Según la naturaleza específica del error de área de nombres, este error puede utilizar cualquiera de los siguientes URI `type` junto con diferentes detalles del mensaje:
>
>* `http://ns.adobe.com/aep/errors/XDM-1020-400`
>* `http://ns.adobe.com/aep/errors/XDM-1021-400`
>* `http://ns.adobe.com/aep/errors/XDM-1022-400`
>* `http://ns.adobe.com/aep/errors/XDM-1023-400`
>* `http://ns.adobe.com/aep/errors/XDM-1024-400`


Puede encontrar ejemplos detallados de estructuras de datos adecuadas para los recursos XDM en la guía de API del Registro de esquemas:

* [Crear una clase personalizada](./api/classes.md#create)
* [Crear un grupo de campos personalizado](./api/field-groups.md#create)
* [Crear un tipo de datos personalizado](./api/data-types.md#create)

### Aceptar encabezado no válido

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

Las solicitudes de GET de la API [!DNL Schema Registry] requieren un encabezado `Accept` para que el sistema determine cómo dar formato a la respuesta. Este error se produce cuando falta un encabezado `Accept` requerido o no es válido.

Dependiendo del punto final que utilice, la propiedad `detailed-message` indica el aspecto que debe tener un encabezado `Accept` válido para obtener una respuesta correcta. Asegúrese de haber introducido correctamente un encabezado `Accept` compatible con la solicitud de API que intenta realizar antes de intentarlo de nuevo.

>[!NOTE]
>
>En función del punto final que se utilice, este error puede utilizar cualquiera de los siguientes URI `type`:
>
>* `http://ns.adobe.com/aep/errors/XDM-1006-400`
>* `http://ns.adobe.com/aep/errors/XDM-1007-400`
>* `http://ns.adobe.com/aep/errors/XDM-1008-400`
>* `http://ns.adobe.com/aep/errors/XDM-1009-400`


Para obtener listas de encabezados Accept compatibles para diferentes solicitudes de API, consulte las secciones correspondientes en la [Guía para desarrolladores del Registro de Esquemas](./api/overview.md).

### [!DNL Real-time Customer Profile] errors

Los siguientes mensajes de error están asociados a operaciones involucradas en la activación de esquemas para [!DNL Real-time Customer Profile]. Consulte la sección [union](./api/unions.md) en la guía de API [!DNL Schema Registry] para obtener más información.

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

Este mensaje de error se muestra cuando intenta habilitar un esquema para [!DNL Profile] y una de sus propiedades contiene un descriptor de relación sin un descriptor de identidad de referencia. Agregue un descriptor de identidad de referencia al campo de esquema en cuestión para resolver este error.

#### Los espacios de nombres del campo descriptor de identidad de referencia y del esquema de destino deben coincidir

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

Para habilitar esquemas que contengan descriptores de relación para usarlos en [!DNL Profile], el área de nombres del campo de origen y el área de nombres principal del campo de destino deben ser el mismo. Este mensaje de error se muestra cuando intenta habilitar un esquema que contiene un área de nombres no coincidente para su descriptor de identidad de referencia. Asegúrese de que el valor `xdm:namespace` del campo de identidad del esquema de destino coincide con el de la propiedad `xdm:identityNamespace` en el descriptor de identidad de referencia del campo de origen para resolver este problema.

Para obtener una lista de códigos de área de nombres de identidad estándar, consulte la sección sobre [áreas de nombres estándar](../identity-service/namespaces.md) en la descripción general del área de nombres de identidad.

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

Antes de habilitar un esquema para Perfil, primero debe [crear un descriptor de identidad principal](./api/descriptors.md#create) para el esquema o incluir un campo de mapa de identidad para actuar en la identidad principal.