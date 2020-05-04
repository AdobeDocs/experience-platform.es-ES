---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Guía de solución de problemas del sistema del modelo de datos de experiencia (XDM)
topic: troubleshooting
translation-type: tm+mt
source-git-commit: 14cd3d17c7d9ba602d02925abddec9e0b246a8c8

---


# Guía de solución de problemas del sistema del modelo de datos de experiencia (XDM)

Este documento proporciona respuestas a las preguntas más frecuentes sobre el sistema del modelo de datos de experiencia (XDM), así como una guía de resolución de problemas para errores comunes. Para preguntas y solución de problemas relacionados con otros servicios de Adobe Experience Platform, consulte la guía [de solución de problemas de](../landing/troubleshooting.md)Experience Platform.

**El modelo de datos de experiencia (XDM)** es una especificación de código abierto que define esquemas estandarizados para la administración de la experiencia del cliente. La metodología en la que se basa la plataforma de experiencia, Sistema **** XDM, hace operativos los esquemas del modelo de datos de experiencia para que los utilicen los servicios de plataforma. El Registro **de** Esquema proporciona una interfaz de usuario y una API RESTful para acceder a la biblioteca **de** Esquemas dentro de la plataforma de experiencia. See the [XDM documentation](home.md) for more information.

## Preguntas frecuentes

La siguiente es una lista de respuestas a las preguntas más frecuentes sobre el sistema XDM y el uso de la API del Registro de Esquema.

### ¿Cómo agrego campos a un esquema?

Puede agregar campos a un esquema mediante una mezcla. Cada mezcla es compatible con una o varias clases, lo que permite que la mezcla se utilice en cualquier esquema que implemente una de esas clases compatibles. Aunque Adobe Experience Platform proporciona varias mezclas del sector con sus propios campos predefinidos, puede añadir sus propios campos a un esquema creando nuevas mezclas mediante la API o la interfaz de usuario.

Para obtener más información sobre la creación de nuevas mezclas en la API, consulte [Creación de un documento de mezcla](api/create-mixin.md) en la guía para desarrolladores de la API de registro de Esquema. Si utiliza la interfaz de usuario, consulte el tutorial [Editor de](./tutorials/create-schema-ui.md)Esquema.

### ¿Cuáles son los mejores usos para las mezclas en comparación con los tipos de datos?

[Las mezclas](./schema/composition.md#mixin) son componentes que definen uno o varios campos de un esquema. Las mezclas refuerzan la forma en que sus campos aparecen en la jerarquía del esquema y, por lo tanto, muestran la misma estructura en cada esquema en el que están incluidos. Las mezclas solo son compatibles con clases específicas, identificadas por su `meta:intendedToExtend` atributo.

[Los tipos](./schema/composition.md#data-type) de datos también pueden proporcionar uno o más campos para un esquema. Sin embargo, a diferencia de las mezclas, los tipos de datos no se limitan a una clase determinada. Esto hace que los tipos de datos sean una opción más flexible para describir estructuras de datos comunes que se pueden reutilizar en varios esquemas con clases potencialmente diferentes.

### ¿Cuál es la ID única de un esquema?

Todos los recursos del Registro de Esquemas (esquemas, mezclas, tipos de datos, clases) tienen un URI que actúa como un ID único con fines de referencia y búsqueda. Al ver un esquema en la API, se puede encontrar en el nivel superior `$id` y en los `meta:altId` atributos.

Para obtener más información, consulte la sección de identificación [de](api/getting-started.md#schema-identification) esquemas en la guía para desarrolladores de la API de registro de Esquema.

### ¿Cuándo impide un inicio de esquema romper cambios?

Los cambios de interrupción se pueden realizar en un esquema siempre y cuando nunca se haya utilizado en la creación de un conjunto de datos o se haya habilitado para su uso en el Perfil [del cliente en tiempo](../profile/home.md)real. Una vez que un esquema se ha utilizado en la creación de conjuntos de datos o se ha habilitado para su uso con el Perfil del cliente en tiempo real, el sistema aplica estrictamente las reglas de la evolución del [Esquema](schema/composition.md#evolution) .

### ¿Cuál es el tamaño máximo de un tipo de campo largo?

Un tipo de campo largo es un entero con un tamaño máximo de 53(+1) bits, lo que le proporciona un rango potencial entre -9007199254740992 y 9007199254740992. Esto se debe a una limitación de cómo las implementaciones de JavaScript de JSON representan enteros largos.

Para obtener más información sobre los tipos de campo, consulte la sección [Definición de tipos](api/appendix.md#field-types) de campo XDM en la guía para desarrolladores de API de registro de Esquema.

### ¿Cómo defino las identidades de mi esquema?

En la plataforma de experiencia, las identidades se utilizan para identificar un sujeto (generalmente una persona individual) independientemente de las fuentes de datos que se estén interpretando. Se definen en esquemas marcando los campos clave como &quot;Identidad&quot;. Los campos de identidad más utilizados incluyen dirección de correo electrónico, número de teléfono, ID de [Experience Cloud (ECID)](https://docs.adobe.com/content/help/es-ES/id-service/using/home.html), ID de CRM y otros campos de ID únicos.

Los campos se pueden marcar como identidades mediante la API o la interfaz de usuario.

#### Definición de identidades en la API

En la API, las identidades se establecen creando descriptores de identidad. Los descriptores de identidad indican que una propiedad concreta de un esquema es un identificador único.

Los descriptores de identidad se crean mediante una solicitud POST al extremo /descriptors. Si se realiza correctamente, recibirá un estado HTTP 201 (Creado) y un objeto de respuesta que contiene los detalles del nuevo descriptor.

Para obtener más información sobre la creación de descriptores de identidad en la API, consulte la sección documento sobre [descriptores](api/descriptors.md) en la guía para desarrolladores de Esquema Registry.

#### Definición de identidades en la interfaz de usuario

Con el esquema abierto en el Editor de Esquemas, haga clic en el campo de la sección **Estructura** del editor que desee marcar como identidad. En Propiedades **de campo** en el lado derecho, haga clic en la casilla de verificación **Identidad** .

Para obtener más información sobre la administración de identidades en la interfaz de usuario, consulte la sección sobre la [definición de campos](./tutorials/create-schema-ui.md#identity-field) de identidad en el tutorial Editor de Esquemas.

### ¿Mi esquema necesita una identidad primaria?

Las identidades primarias son opcionales, ya que los esquemas pueden tener 0 o 1 de ellas. Sin embargo, un esquema debe tener una identidad principal para que el esquema se pueda utilizar en el Perfil del cliente en tiempo real. Consulte la sección de [identidad](./tutorials/create-schema-ui.md#identity-field) del tutorial Editor de Esquemas para obtener más información.

### ¿Cómo habilito un esquema para utilizarlo en Perfil de clientes en tiempo real?

Los Esquemas se habilitan para su uso en el Perfil [del cliente en tiempo](../profile/home.md) real mediante la adición de una etiqueta &quot;unión&quot;, ubicada en el `meta:immutableTags` atributo del esquema. La activación de un esquema para su uso con Perfil se puede realizar mediante la API o la interfaz de usuario.

#### Activación de un esquema existente para Perfil mediante la API

Realice una solicitud PATCH para actualizar el esquema y agregar el `meta:immutableTags` atributo como una matriz que contenga el valor &quot;unión&quot;. Si la actualización se realiza correctamente, la respuesta mostrará el esquema actualizado que ahora contiene la etiqueta de unión.

Para obtener más información sobre el uso de la API para habilitar un esquema para su uso en Perfil de clientes en tiempo real, consulte el documento de [uniones](./api/unions.md) de la guía para desarrolladores de Esquema Registry.

#### Activación de un esquema existente para Perfil mediante la interfaz de usuario

En la plataforma de experiencia, haga clic en **Esquemas** en la barra de navegación izquierda y seleccione el nombre del esquema que desea habilitar en la lista de esquemas. A continuación, en el lado derecho del editor, en Propiedades **del** Esquema, haga clic en el **Perfil** para activarlo.


Para obtener más información, consulte la sección sobre el [uso en el Perfil](./tutorials/create-schema-ui.md#profile) del cliente en tiempo real en el tutorial Editor de Esquemas.

### ¿Puedo editar un esquema de unión directamente?

Los esquemas de Unión son de sólo lectura y son generados automáticamente por el sistema. No se pueden editar directamente. Los esquemas de Unión se crean para una clase específica cuando se agrega una etiqueta &quot;unión&quot; al esquema que implementa esa clase.

Para obtener más información sobre uniones en XDM, consulte la sección [uniones](./api/unions.md) en la guía para desarrolladores de la API de registro de Esquema.

### ¿Cómo debo formatear mi archivo de datos para ingerir datos en mi esquema?

La plataforma de experiencia acepta archivos de datos en formato Parquet o JSON. El contenido de estos archivos debe cumplir el esquema al que hace referencia el conjunto de datos. Para obtener más información sobre las prácticas recomendadas para la ingestión de archivos de datos, consulte la descripción general [de la ingestión de](../ingestion/home.md)lotes.

## Errores y solución de problemas

A continuación se muestra una lista de mensajes de error que puede encontrar al trabajar con la API del Registro de Esquema.

### No se encontró el objeto

```json
{
    "type": "/placeholder/type/uri",
    "status": 404,
    "title": "NotFoundError",
    "detail": "Object https://ns.adobe.com/incorrectTenantId/schemas/ee067e31b08514d21e2b82577813409d 
      with version 1 not found"
}
```

Este error se muestra cuando el sistema no pudo encontrar un recurso concreto. Es posible que el recurso se haya eliminado o que la ruta de acceso de la llamada de API no sea válida. Asegúrese de haber introducido una ruta válida para la llamada de API antes de intentarlo de nuevo. Es posible que desee comprobar que ha introducido el ID correcto para el recurso y que la ruta se ha adaptado correctamente al contenedor correspondiente (global o inquilino).

Para obtener más información sobre la construcción de rutas de búsqueda en la API, consulte las secciones de identificación [de](./api/getting-started.md#container) contenedores [y](api/getting-started.md#schema-identification) esquemas en la guía para desarrolladores de Esquema Registry.

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

Este mensaje de error se muestra cuando intenta crear un recurso con un título que ya está utilizando otro recurso. Los títulos deben ser únicos en todos los tipos de recursos. Por ejemplo, si intenta crear una mezcla con un título que ya esté utilizando un esquema, recibirá este error.

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

Este mensaje de error se muestra cuando se intenta crear una nueva mezcla con campos con espacios de nombres incorrectos. Las mezclas definidas por la organización de IMS deben Área de nombres sus campos con un `TENANT_ID` fin de evitar conflictos con otros recursos del sector y del proveedor. Encontrará ejemplos detallados de estructuras de datos adecuadas para las mezclas en el documento sobre la [creación de una sección de mezclas](api/create-mixin.md) en la guía para desarrolladores de la API de registro de Esquema.


### Errores de Perfil del cliente en tiempo real

Los siguientes mensajes de error se asocian con operaciones relacionadas con la activación de esquemas para el Perfil del cliente en tiempo real. Consulte la sección [uniones](./api/unions.md) en la guía para desarrolladores de la API de Registro de Esquema para obtener más información.

#### Para habilitar los conjuntos de datos de perfil, el esquema debe ser válido

```json
{
    "type": "/placeholder/type/uri",
    "status": 400,
    "title": "BadRequestError",
    "detail": "To enable profile datasets the schema should be valid"
}
```

Este mensaje de error se muestra cuando intenta habilitar un conjunto de datos de perfil para un esquema que no se ha habilitado para el Perfil de clientes en tiempo real. Asegúrese de que el esquema contiene una etiqueta de unión antes de habilitar el conjunto de datos.

#### Debe existir un descriptor de identidad de referencia

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

Este mensaje de error se muestra cuando se intenta habilitar un esquema para Perfil y una de sus propiedades contiene un descriptor de relación sin un descriptor de identidad de referencia. Añada un descriptor de identidad de referencia al campo de esquema en cuestión para resolver este error.

#### Las Áreas de nombres del campo descriptor de identidad de referencia y del esquema de destino deben coincidir con

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

Para habilitar esquemas que contengan descriptores de relación para su uso en Perfil, la Área de nombres del campo de origen y la Área de nombres principal del campo de destinatario deben ser las mismas. Este mensaje de error se muestra al intentar habilitar un esquema que contiene una Área de nombres no coincidente para su descriptor de identidad de referencia. Asegúrese de que el `xdm:namespace` valor del campo de identidad del esquema de destino coincide con el de la `xdm:identityNamespace` propiedad en el descriptor de identidad de referencia del campo de origen para resolver este problema.

Para obtener una lista de los códigos de Área de nombres de identidad admitidos, consulte la sección sobre Áreas de nombres [](../identity-service/namespaces.md) estándar en la descripción general de la Área de nombres de identidad.

### Aceptar errores de encabezado

La mayoría de las solicitudes GET de la API del Registro de Esquema requieren un encabezado Accept para que el sistema pueda determinar cómo dar formato a la respuesta. A continuación se muestra una lista de errores comunes asociados con el encabezado Accept. Para obtener listas de encabezados Accept compatibles para diferentes solicitudes de API, consulte sus secciones correspondientes en la guía para desarrolladores de [Esquema Registry](api/getting-started.md).

#### Se requiere el parámetro Accept header

```json
{
    "type": "/placeholder/type/uri",
    "status": 406,
    "title": "NotAcceptableError",
    "detail": "Accept header parameter is required"
}
```

Este mensaje de error se muestra cuando falta un encabezado Accept en una solicitud de API. Asegúrese de incluir un encabezado Accept antes de volver a intentarlo.

#### Se proporcionó un medio de aceptación desconocido

```json
{
    "type": "/placeholder/type/uri",
    "status": 406,
    "title": "NotAcceptableError",
    "detail": "Unknown Accept media supplied: xed+json"
}
```

Este mensaje de error se muestra cuando un encabezado Accept no es válido. Asegúrese de haber introducido correctamente un encabezado Accept que sea compatible con la solicitud de API que intenta realizar antes de intentarlo de nuevo.

#### Formato de aceptación desconocido disponible

```json
{
    "type": "/placeholder/type/uri",
    "status": 406,
    "title": "NotAcceptableError",
    "detail": "Unknown Accept format available "
}
```

Este mensaje de error se muestra cuando el encabezado Accept se ha proporcionado incorrectamente al buscar un descriptor. Antes de volver a intentarlo, asegúrese de haber introducido correctamente uno de los encabezados [admitidos Accept para los descriptores](./api/descriptors.md) .

#### La versión debe proporcionarse en el encabezado Accept

```json
{
    "type": "/placeholder/type/uri",
    "status": 400,
    "title": "BadRequestError",
    "detail": "version must be supplied in the accept header. Example: 
      application/vnd.adobe.xed-full-notext+json; version=1"
}
```

Este mensaje de error se muestra cuando no se ha incluido un número de versión en el encabezado Accept. Determinados elementos como esquemas requieren que se especifique una versión al buscar instancias individuales. Un encabezado Accept que contenga un número de versión tendrá un aspecto similar al siguiente:

```plaintext
application/vnd.adobe.xed+json; version=1
```

Para obtener una lista de los encabezados Accept admitidos, consulte la sección [Accept header](api/getting-started.md#accept) en la guía para desarrolladores de Esquema Registry.

#### La versión no debe proporcionarse en el encabezado Accept

```json
{
    "type": "/placeholder/type/uri",
    "status": 400,
    "title": "BadRequestError",
    "detail": "version must not be supplied in the accept header. Example: 
      application/vnd.adobe.xed-full+json"
}
```

Si intenta incluir una versión en el encabezado Accept al enumerar los recursos (GET), recibirá este error. Las versiones solo son necesarias cuando se intenta realizar una solicitud de búsqueda en un único recurso. Elimine la versión del encabezado Accept para resolver el error.