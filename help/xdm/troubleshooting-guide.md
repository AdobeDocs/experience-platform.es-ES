---
keywords: Experience Platform;inicio;temas populares;XDM;sistema XDM;perfil individual XDM;ExperienceEvent XDM;Evento de experiencia XDM;experienceEvent;evento de experiencias;evento de experiencias XDM;ExperienceEvent XDM;modelo de datos de experiencia;modelo de datos de experiencia;modelo de datos de experiencia;modelo de datos;esquema;solución de problemas;preguntas frecuentes;faq;esquema de unión;UNION PROFILE;perfil de unión
solution: Experience Platform
title: Guía de solución de problemas del sistema XDM
description: Este documento proporciona respuestas a las preguntas más frecuentes sobre Experience Data Model (XDM) y el sistema XDM en Adobe Experience Platform, así como una guía de solución de problemas para errores comunes.
topic-legacy: troubleshooting
exl-id: a0c7c661-bee8-4f66-ad5c-f669c52c9de3
translation-type: tm+mt
source-git-commit: 3985ba8f46a62e8d9ea8b1f084198b245318a24f
workflow-type: tm+mt
source-wordcount: '1888'
ht-degree: 0%

---

# Guía de solución de problemas del sistema XDM

Este documento proporciona respuestas a las preguntas más frecuentes sobre [!DNL Experience Data Model] (XDM) y el sistema XDM en Adobe Experience Platform, así como una guía de solución de problemas para errores comunes. Para preguntas y solución de problemas relacionados con otros servicios de Platform, consulte la [guía de solución de problemas del Experience Platform](../landing/troubleshooting.md).

**[!DNL Experience Data Model](XDM)** es una especificación de código abierto que define esquemas estandarizados para la administración de experiencias del cliente. La metodología en la que se crea [!DNL Experience Platform], **XDM System**, operacionaliza los [!DNL Experience Data Model] esquemas para su uso por los servicios [!DNL Platform]. El **[!DNL Schema Registry]** proporciona una interfaz de usuario y una API RESTful para acceder al **[!DNL Schema Library]** dentro de [!DNL Experience Platform]. Consulte la [documentación de XDM](home.md) para obtener más información.

## Preguntas frecuentes

A continuación se ofrece una lista de respuestas a las preguntas más frecuentes sobre el sistema XDM y el uso de la API [!DNL Schema Registry].

### ¿Cómo se agregan campos a un esquema?

Puede añadir campos a un esquema utilizando un grupo de campos de esquema. Cada grupo de campos es compatible con una o más clases, lo que permite utilizar el grupo de campos en cualquier esquema que implemente una de esas clases compatibles. Aunque Adobe Experience Platform proporciona varios grupos de campos del sector con sus propios campos predefinidos, puede añadir sus propios campos a un esquema creando nuevos grupos de campos mediante la API o la interfaz de usuario.

Para obtener más información sobre la creación de nuevos grupos de campos en la API [!DNL Schema Registry], consulte la [guía de extremo del grupo de campos](api/field-groups.md#create). Si utiliza la interfaz de usuario de , consulte el tutorial [Editor de esquemas](./tutorials/create-schema-ui.md).

### ¿Cuáles son los mejores usos para los grupos de campos frente a los tipos de datos?

[Los ](./schema/composition.md#field-group) grupos de campos son componentes que definen uno o más campos de un esquema. Los grupos de campos refuerzan la forma en que sus campos aparecen en la jerarquía del esquema y, por lo tanto, muestran la misma estructura en cada esquema en el que están incluidos. Los grupos de campos solo son compatibles con clases específicas, tal como se identifican con su atributo `meta:intendedToExtend`.

[Los ](./schema/composition.md#data-type) tipos de datos también pueden proporcionar uno o más campos para un esquema. Sin embargo, a diferencia de los grupos de campos, los tipos de datos no están restringidos a una clase en particular. Esto hace que los tipos de datos sean una opción más flexible para describir estructuras de datos comunes que se pueden reutilizar en varios esquemas con clases potencialmente diferentes.

### ¿Cuál es el ID exclusivo de un esquema?

Todos los [!DNL Schema Registry] recursos (esquemas, grupos de campos, tipos de datos, clases) tienen un URI que actúa como ID único con fines de referencia y búsqueda. Al ver un esquema en la API, se puede encontrar en los atributos `$id` y `meta:altId` de nivel superior.

Para obtener más información, consulte la sección [resource identification](api/getting-started.md#resource-identification) en la guía para desarrolladores de API [!DNL Schema Registry].

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

Con el esquema abierto en el Editor de esquemas, seleccione el campo en la sección **[!UICONTROL Structure]** del editor que desea marcar como identidad. En **[!UICONTROL Field Properties]** en el lado derecho, seleccione la casilla **[!UICONTROL Identity]** .

Para obtener más información sobre la administración de identidades en la interfaz de usuario, consulte la sección [definición de campos de identidad](./tutorials/create-schema-ui.md#identity-field) en el tutorial Editor de esquemas.

### ¿Mi esquema necesita una identidad principal?

Las identidades principales son opcionales, ya que los esquemas pueden tener 0 o 1 de ellas. Sin embargo, un esquema debe tener una identidad principal para que el esquema esté habilitado para utilizarse en [!DNL Real-time Customer Profile]. Consulte la sección [identity](./tutorials/create-schema-ui.md#identity-field) del tutorial Editor de esquemas para obtener más información.

### ¿Cómo se habilita un esquema para su uso en [!DNL Real-time Customer Profile]?

Los esquemas se habilitan para su uso en [[!DNL Real-time Customer Profile]](../profile/home.md) mediante la adición de una etiqueta &quot;union&quot;, ubicada en el atributo `meta:immutableTags` del esquema. La activación de un esquema para su uso con [!DNL Profile] se puede realizar mediante la API o la interfaz de usuario.

#### Activación de un esquema existente para [!DNL Profile] mediante la API

Realice una solicitud de PATCH para actualizar el esquema y añadir el atributo `meta:immutableTags` como una matriz que contenga el valor &quot;union&quot;. Si la actualización se realiza correctamente, la respuesta mostrará el esquema actualizado que ahora contiene la etiqueta de unión.

Para obtener más información sobre el uso de la API para habilitar un esquema para utilizarlo en [!DNL Real-time Customer Profile], consulte el documento [union](./api/unions.md) de la guía para desarrolladores de [!DNL Schema Registry].

#### Activación de un esquema existente para [!DNL Profile] mediante la interfaz de usuario

En [!DNL Experience Platform], seleccione **[!UICONTROL Schemas]** en el panel de navegación izquierdo y seleccione el nombre del esquema que desea habilitar en la lista de esquemas. A continuación, en el lado derecho del editor, en **[!UICONTROL Schema Properties]**, seleccione **[!UICONTROL Profile]** para activarlo.


Para obtener más información, consulte la sección [use in Real-time Customer Profile](./tutorials/create-schema-ui.md#profile) en el tutorial [!UICONTROL Schema Editor].

### ¿Puedo editar un esquema de unión directamente?

Los esquemas de unión son de solo lectura y el sistema los genera automáticamente. No se pueden editar directamente. Los esquemas de unión se crean para una clase específica cuando se agrega una etiqueta &quot;unión&quot; al esquema que implementa esa clase.

Para obtener más información sobre las uniones en XDM, consulte la sección [union](./api/unions.md) en la guía para desarrolladores de API [!DNL Schema Registry].

### ¿Cómo debo formatear mi archivo de datos para introducir datos en mi esquema?

[!DNL Experience Platform] acepta archivos de datos en formato  [!DNL Parquet] o JSON. El contenido de estos archivos debe cumplir el esquema al que hace referencia el conjunto de datos. Para obtener más información sobre las prácticas recomendadas para la ingesta de archivos de datos, consulte la [información general sobre la ingesta por lotes](../ingestion/home.md).

## Errores y solución de problemas

A continuación se muestra una lista de mensajes de error que puede encontrar al trabajar con la API [!DNL Schema Registry].

### Objeto no encontrado

```json
{
    "type": "/placeholder/type/uri",
    "status": 404,
    "title": "NotFoundError",
    "detail": "Object https://ns.adobe.com/incorrectTenantId/schemas/ee067e31b08514d21e2b82577813409d 
      with version 1 not found"
}
```

Este error se muestra cuando el sistema no pudo encontrar un recurso en particular. Es posible que el recurso se haya eliminado o que la ruta de acceso de la llamada de API no sea válida. Asegúrese de haber introducido una ruta válida para la llamada de API antes de intentarlo de nuevo. Es posible que desee comprobar que ha introducido el ID correcto para el recurso y que la ruta tiene un espacio de nombres adecuado con el contenedor apropiado (global o inquilino).

Para obtener más información sobre la construcción de rutas de búsqueda en la API, consulte las secciones [container](./api/getting-started.md#container) e [resource identification](api/getting-started.md#resource-identification) en la guía para desarrolladores de [!DNL Schema Registry].

### El título debe ser único

```json
{
    "type": "/placeholder/type/uri",
    "status": 400,
    "title": "BadRequestError",
    "detail": "Title must be unique. An object 
      https://ns.adobe.com/{TENANT_ID}/schemas/26f6833e55db1dd8308aa07a64f2042d 
      already exists with the same title."
}
```

Este mensaje de error se muestra cuando intenta crear un recurso con un título que otro recurso ya está utilizando. Los títulos deben ser únicos en todos los tipos de recursos. Por ejemplo, si intenta crear un grupo de campos con un título que ya esté utilizando un esquema, recibirá este error.

### Los campos personalizados deben utilizar un campo de nivel superior

```json
{
    "type": "/placeholder/type/uri",
    "status": 400,
    "title": "BadRequestError",
    "detail": "For custom fields, you must use a top level field named _{TENANT_ID}
       and all the other fields must be defined under it"
}
```

Este mensaje de error se muestra cuando intenta crear un nuevo grupo de campos con campos con espacio de nombres incorrecto. Los grupos de campos definidos por la organización IMS deben establecer el espacio de nombres de sus campos con un `TENANT_ID` para evitar conflictos con otros recursos del sector y del proveedor. Puede encontrar ejemplos detallados de estructuras de datos adecuadas para grupos de campos en la [guía de extremo de grupos de campos](./api/field-groups.md#create).


### [!DNL Real-time Customer Profile] errors

Los siguientes mensajes de error están asociados a operaciones involucradas en la activación de esquemas para [!DNL Real-time Customer Profile]. Consulte la sección [union](./api/unions.md) en la guía para desarrolladores de API [!DNL Schema Registry] para obtener más información.

#### Para habilitar conjuntos de datos de perfil, el esquema debe ser válido

```json
{
    "type": "/placeholder/type/uri",
    "status": 400,
    "title": "BadRequestError",
    "detail": "To enable profile datasets the schema should be valid"
}
```

Este mensaje de error se muestra cuando intenta habilitar un conjunto de datos de perfil para un esquema que no se ha habilitado para [!DNL Real-time Customer Profile]. Asegúrese de que el esquema contiene una etiqueta de unión antes de habilitar el conjunto de datos.

#### Debe haber un descriptor de identidad de referencia

```json
{
    "type": "/placeholder/type/uri",
    "status": 400,
    "title": "BadRequestError",
    "detail": "For a schema to be able to participate in union, if any of its 
      property is associated with a xdm:descriptorOneToOne descriptor, there must 
      be a xdm:descriptorReferenceIdentity descriptor for that property"
}
```

Este mensaje de error se muestra cuando intenta habilitar un esquema para [!DNL Profile] y una de sus propiedades contiene un descriptor de relación sin un descriptor de identidad de referencia. Agregue un descriptor de identidad de referencia al campo de esquema en cuestión para resolver este error.

#### Los espacios de nombres del campo descriptor de identidad de referencia y del esquema de destino deben coincidir

```json
{
    "type": "/placeholder/type/uri",
    "status": 400,
    "title": "BadRequestError",
    "detail": "If both schemas from an already defined xdm:descriptorOneToOne 
      descriptor are promoted to union, and if there is a primary identity on one of 
      the schemas from the xdm:descriptorOneToOne descriptor, the 
      xdm:identityNamespace of the sourceSchema's descriptorReferenceIdentity and the 
      xdm:namespace field of the xdm:descriptorIdentity for the destinationSchema must 
      match"
}
```

Para habilitar esquemas que contengan descriptores de relación para usarlos en [!DNL Profile], el área de nombres del campo de origen y el área de nombres principal del campo de destino deben ser el mismo. Este mensaje de error se muestra cuando intenta habilitar un esquema que contiene un área de nombres no coincidente para su descriptor de identidad de referencia. Asegúrese de que el valor `xdm:namespace` del campo de identidad del esquema de destino coincide con el de la propiedad `xdm:identityNamespace` en el descriptor de identidad de referencia del campo de origen para resolver este problema.

Para obtener una lista de códigos de área de nombres de identidad admitidos, consulte la sección sobre [áreas de nombres estándar](../identity-service/namespaces.md) en la descripción general del área de nombres de identidad.

### Aceptar errores de encabezado

La mayoría de las solicitudes de GET de la API [!DNL Schema Registry] requieren un encabezado Accept para que el sistema determine cómo dar formato a la respuesta. La siguiente es una lista de errores comunes asociados con el encabezado Accept . Para obtener listas de encabezados Accept compatibles para diferentes solicitudes de API, consulte las secciones correspondientes en la [Guía para desarrolladores del Registro de Esquemas](api/getting-started.md).

#### Se requiere el parámetro Accept header

```json
{
    "type": "/placeholder/type/uri",
    "status": 406,
    "title": "NotAcceptableError",
    "detail": "Accept header parameter is required"
}
```

Este mensaje de error se muestra cuando falta un encabezado Accept de una solicitud de API. Asegúrese de incluir un encabezado Accept antes de volver a intentarlo.

#### Se ha proporcionado un soporte de aceptar desconocido

```json
{
    "type": "/placeholder/type/uri",
    "status": 406,
    "title": "NotAcceptableError",
    "detail": "Unknown Accept media supplied: xed+json"
}
```

Este mensaje de error se muestra cuando un encabezado Accept no es válido. Asegúrese de haber introducido correctamente un encabezado Accept compatible con la solicitud de API que intenta realizar antes de volver a intentarlo.

#### Formato aceptar desconocido disponible

```json
{
    "type": "/placeholder/type/uri",
    "status": 406,
    "title": "NotAcceptableError",
    "detail": "Unknown Accept format available "
}
```

Este mensaje de error se muestra cuando el encabezado Accept se ha proporcionado incorrectamente al buscar un descriptor. Asegúrese de haber introducido correctamente uno de los [encabezados de aceptar admitidos para los descriptores](./api/descriptors.md) antes de volver a intentarlo.

#### La versión debe suministrarse en el encabezado Accept

```json
{
    "type": "/placeholder/type/uri",
    "status": 400,
    "title": "BadRequestError",
    "detail": "version must be supplied in the accept header. Example: 
      application/vnd.adobe.xed-full-notext+json; version=1"
}
```

Este mensaje de error se muestra cuando no se ha incluido un número de versión en el encabezado Accept . Algunos elementos, como los esquemas, requieren que se especifique una versión al buscar instancias individuales. Un encabezado Accept que contenga un número de versión tendrá un aspecto similar al siguiente:

```plaintext
application/vnd.adobe.xed+json; version=1
```

Para obtener una lista de los encabezados Accept admitidos, consulte la sección [Accept header](api/getting-started.md#accept) en la guía para desarrolladores de [!DNL Schema Registry].

#### La versión no debe suministrarse en el encabezado Accept

```json
{
    "type": "/placeholder/type/uri",
    "status": 400,
    "title": "BadRequestError",
    "detail": "version must not be supplied in the accept header. Example: 
      application/vnd.adobe.xed-full+json"
}
```

Si intenta incluir una versión en el encabezado Accept al enumerar recursos (GET), recibirá este error. Las versiones solo son necesarias cuando se intenta realizar una solicitud de consulta en un solo recurso. Elimine la versión del encabezado Accept para resolver el error.
