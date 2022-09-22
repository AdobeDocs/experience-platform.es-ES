---
title: Elementos de datos
description: Los Data Elements son los componentes básicos del diccionario de datos (o mapa de datos). Utilice Data Elements para recopilar, organizar y entregar datos a través de la tecnología de marketing y publicidad.
exl-id: 1e7b03cc-5a54-403d-bf8d-dbc206cfeb2d
source-git-commit: 0c2ee3bbb4d85bd755b4847a509fc7bd50ba67bc
workflow-type: tm+mt
source-wordcount: '1631'
ht-degree: 98%

---

# Elementos de datos

>[!NOTE]
>
>Adobe Experience Platform Launch se ha convertido en un conjunto de tecnologías de recopilación de datos en Adobe Experience Platform. Como resultado, se han implementado varios cambios terminológicos en la documentación del producto. Consulte el siguiente [documento](../../term-updates.md) para obtener una referencia consolidada de los cambios terminológicos.

Los Data Elements son los componentes básicos del diccionario de datos (o mapa de datos). Utilice Data Elements para recopilar, organizar y entregar datos a través de la tecnología de marketing y publicidad.

Un solo elemento de datos es una variable cuyo valor puede asignarse a cadenas de consulta, URL, valores de cookies, variables JavaScript, etc. Puede hacer referencia a este valor por su nombre de variable en Adobe Experience Platform. Esta colección de Data Elements se convierte en el diccionario de los datos definidos que puede utilizar para crear reglas (eventos, condiciones y acciones). Este diccionario de datos se comparte entre etiquetas para utilizarlo con cualquier extensión agregada a su propiedad.

>[!IMPORTANT]
>
>Los cambios no surtirán efecto hasta [que se publiquen](../publishing/overview.md).

Utilice los Data Elements tan ampliamente como pueda mediante la creación de reglas para consolidar la definición de los elementos dinámicos y mejorar la eficacia del proceso de etiquetado. Solo es necesario definir las reglas de datos una vez y, a continuación, podrá utilizarlas en muchas ubicaciones.

El concepto de Data Elements reutilizables es muy eficiente y debe usarse como práctica recomendada.

Por ejemplo, si tiene alguna forma particular de referirse a nombres de páginas o ID de productos o de obtener información de parámetros de cadenas de consulta de un vínculo de marketing de afiliados o de [!DNL AdWords], entre otras cosas, puede crear un diccionario de datos (elementos de datos) recopilando información de su fuente y utilizando estos datos en diversas reglas de etiquetado.

Si utilizamos los nombres de páginas como ejemplo, supongamos que utiliza un esquema de nombre de página específico haciendo referencia a una capa de datos, al elemento `document.title` o a una etiqueta de título del sitio web. Las etiquetas de Adobe Experience Platform permiten crear un elemento de datos como único punto de referencia para ese punto de datos en particular. A continuación, puede utilizar este elemento de datos en cualquier regla que deba hacer referencia al nombre de página. Si, por algún motivo, en el futuro decide cambiar la forma de hacer referencia a ese nombre de página (por ejemplo, hasta ahora ha hecho referencia a `document.title`, pero ahora quiere hacer referencia a una capa de datos específica), no es necesario que edite las distintas reglas para cambiar la referencia. Simplemente debe cambiar la referencia una vez en el elemento de datos y todas las reglas que hagan referencia a ese elemento de datos se actualizarán automáticamente.

>[!NOTE]
>
>Si no se hace referencia a un elemento de datos en una regla, este no estará cargado en ninguna página a menos que se llame específicamente en un script personalizado.

Los Data Elements se rellenan con datos cuando se utilizan en reglas o cuando se llaman manualmente en scripts. En un nivel superior puede:

1. [Crear un elemento de datos](#create-a-data-element), si aún no lo ha hecho.
1. Utilizar el elemento de datos de una [regla](./rules.md) o un script personalizado.

## Uso de los Data Elements

### En las reglas

Puede utilizar Data Elements en la interfaz de edición de reglas utilizando el cuadro de búsqueda para encontrar el nombre del elemento de datos.

### En el script personalizado

Es posible utilizar los Data Elements en las secuencias de datos personalizadas mediante la sintaxis del objeto `_satellite`:

`_satellite.getVar('data element name');`

## Crear un elemento de datos {#create-a-data-element}

Los Data Elements constituyen los bloques generadores de las reglas. Los Data Elements le permiten crear un diccionario de datos (o mapa de datos) de elementos que se utilizan normalmente en una página, independientemente de su origen (cadenas de consultas, URL o valores de cookies), para cualquier objeto incluido en su sitio.

1. En una página Propiedad, abra la pestaña [!UICONTROL Elementos de datos] y seleccione **[!UICONTROL Crear nuevo elemento de datos]**.
1. Asigne un nombre al elemento de datos.
1. Seleccione una extensión y un tipo.

   Los tipos de Data Elements disponibles están determinados por la extensión. Para obtener información sobre los tipos disponibles con la extensión principal de etiqueta, consulte [Tipos de elementos de datos](data-elements.md#types-of-data-elements).

1. Proporcione toda la información solicitada sobre el tipo elegido en los campos proporcionados.
1. (Opcional) Introduzca un valor predeterminado.

   Si no selecciona esta opción, no hay ningún valor predeterminado. La mayoría de los usuarios deja esto en estado predeterminado. Los distintos sistemas tratan las variables vacías de forma diferente. Algunas personas eligen introducir algo como &quot;ninguno&quot; o &quot;n/a&quot; para poder crear coherencia en el sistema de informes cuando el elemento de datos no arroja un valor.

1. Seleccione si desea forzar un valor en minúsculas y si desea eliminar los saltos y espacios de línea.
1. Seleccione una duración.

   Las opciones disponibles son:

   * Ninguna
      * The value is not stored.
   * Page view
      * El valor se mantiene en una variable JavaScript hasta que se actualiza la página o se carga una nueva.
      * Puede crearse y configurarse en scripts mediante la sintaxis de objeto `_satellite`.

         `_satellite.setVar('data_element_name')`
   * Session
      * Los valores persisten en el almacenamiento de sesiones del explorador hasta que se cierra la pestaña.
      * Disponible durante toda la visita al sitio.
   * Visitor
      * El valor se guarda de forma indefinida en el almacenamiento local del explorador.

1. Seleccione **[!UICONTROL Guardar]**.

Al crear o editar elementos, puede guardar y desarrollar en su [biblioteca activa](../publishing/libraries.md#active-library). Esto guarda inmediatamente el cambio en la biblioteca y ejecuta una compilación. Se muestra el estado de la compilación. También puede crear una nueva biblioteca desde la lista desplegable [!UICONTROL Biblioteca activa].

## Tipos de Data Elements {#types-of-data-elements}

Los tipos de Data Elements están determinados por la extensión. No hay límite para los tipos que se pueden crear.

Las secciones siguientes describen los tipos de Data Elements disponibles en la Extensión principal. Otras extensiones utilizan tipos de Data Elements diferentes.

### Cookie

Es posible hacer referencia a cualquier cookie de dominio disponible en el campo de nombre de cookie.

#### Ejemplo:

`cookieName`

### Código personalizado

Puede introducir código JavaScript personalizado en la IU si selecciona la opción [!UICONTROL Abrir editor] e inserta código en la ventana del editor.

Se debe incluir una sentencia de retorno en la ventana del editor para indicar qué valor debe establecerse como valor del elemento de datos. Si no se incluye una declaración de retorno, el elemento de datos se resuelve en `undefined`. Esto activa una alternativa para buscar un valor almacenado y, luego, un valor predeterminado si no hay ningún valor almacenado.

**Ejemplo:**

```text
var pageType = $('div.page-wrapper').attr('class').split('')[1];
if (window.location.pathname == '/') {
  return 'homepage';
} else {
  return pageType;
}
```

El código personalizado puede aceptar el objeto `event` de la regla de llamada como argumento. Permite que el código lea el valor allí.

**Ejemplo:**

```text
// `event` is the default object provided by the rule
var eventType = event.$type;
return eventType; // if this data element is called from a "DOM Ready" event, then `core.dom-ready` is returned
```

Puede utilizar esto en los scripts personalizados con la sintaxis del objeto `_satellite`:

```javascript
// event refers to the calling rule's event
var rule = _satellite.getVar('return event rule', event);
```

Cuando se usa un porcentaje (`%`), solo es necesario especificar el nombre del elemento de datos. No necesita especificar `event`.

```text
%data element name%
```

### Atributo DOM

Es posible recuperar cualquier elemento, como una etiqueta H1 o div.

#### Ejemplo:

Cadena de selector de CSS:

`id#dc logo img`

Obtener el valor de:

`src`

### Variable de JavaScript

Es posible hacer referencia a cualquier objeto JavaScript o variable mediante el campo de ruta.

Si desea recopilar variables de JavaScript o propiedades de objeto en el marcado y utilizarlas con cualquiera de las extensiones o reglas, se pueden utilizar elementos de datos para capturar estos valores. De esta forma, puede hacer referencia al elemento de datos mediante las reglas y, en caso de que la fuente de datos cambie en algún momento, solo deberá cambiar la referencia a la fuente (el elemento de datos) en un lugar de la recopilación de datos de la IU.

Por ejemplo, supongamos que el marcado contiene una variable de JavaScript llamada “`Page_Name`” similar a la que se muestra a continuación:

```markup
<script>
  //data layer
  var Page_Name = "Homepage"
</script>
```

Debe proporcionar la ruta a esa variable cuando cree el elemento de datos.

Si utiliza un objeto de recopilación de datos como parte de la capa de datos, solo tiene que utilizar la notación de puntos en la ruta para hacer referencia al objeto y la propiedad que desea capturar en el elemento de datos como, por ejemplo, `_myData.pageName` o `digitalData.pageName`, etc.

#### Ejemplo:

`window.document.title`

### Almacenamiento local

Proporcione el nombre del elemento de almacenamiento local en el campo [!UICONTROL Nombre del elemento de almacenamiento local].

El almacenamiento local proporciona a los exploradores una forma de almacenar información de página a página ([https://www.w3schools.com/html/html5_webstorage.asp](https://www.w3schools.com/html/html5_webstorage.asp)). El almacenamiento local funciona de forma muy similar a las cookies, pero es mucho más amplio y flexible.

Utilice el campo proporcionado para especificar el valor que ha creado para un elemento de almacenamiento local, como `lastProductViewed.`

### Información de página

Utilice estos puntos de datos para capturar información de página para usarla en la lógica de regla o para enviar información a [!DNL Analytics] o a sistemas de seguimiento externos.

Puede seleccionar uno de los siguientes atributos de página para usarlos en el elemento de datos:

* URL
* Hostname
* Pathname
* Protocol
* Referrer
* Title

### Query string Parameter

Especifique un único parámetro de URL en el campo [!UICONTROL Parámetro de URL].

Solo es necesaria la sección de nombres y cualquier indicador especial como “?” o &quot;=&quot; debe omitirse.

#### Ejemplo:

`contentType`

### Número aleatorio

Utilice este elemento de datos para generar un número aleatorio. A menudo se utiliza para datos de muestra o para crear ID, como un ID de visita individual. El número aleatorio puede utilizarse para proteger o desproteger datos confidenciales. Algunos ejemplos pueden incluir:

* Generar un ID de visita individual (Hit ID)
* Concatenar el número a un token de usuario o una marca de tiempo para garantizar su exclusividad
* Realizar un hash unidireccional en los datos PII
* Decidir al azar cuándo se muestra una solicitud de encuesta en el sitio

Especifique los valores mínimos y máximos del número aleatorio.

**Valores predeterminados:**

Mínimo: 0

Máximo: 1000000000

### Almacenamiento de sesión

Proporcione el nombre del elemento de almacenamiento de la sesión en el campo [!UICONTROL Nombre del elemento de almacenamiento de sesión].

El almacenamiento de sesión es similar al almacenamiento local, excepto que los datos se descartan después de que finalice la sesión, mientras que el almacenamiento local o una cookie pueden retener los datos.

### Comportamiento de los visitantes

De manera similar a Información de página, este elemento de datos utiliza tipos de comportamiento comunes para enriquecer la lógica dentro de las reglas u otras soluciones de la plataforma.

Seleccione uno de los siguientes atributos de comportamiento del visitante:

* Landing page
* Traffic source
* Minutes on site
* Session count
* Session page view count
* Lifetime page view count
* Is new visitor

Algunos casos de uso común son:

* Mostrar una encuesta después de que un visitante haya estado en el sitio durante cinco minutos
* Si ésta es la página de aterrizaje de la visita, rellene una métrica de [!DNL Analytics]
* Mostrar una oferta nueva al visitante después de un determinado número de sesiones
* Mostrar una sugerencia de suscripción a la newsletter a los nuevos visitantes

## Elementos de datos integrados

Debe crear un elemento de datos personalizado en la interfaz de usuario de recopilación de datos si anteriormente ha utilizado cualquiera de los siguientes elementos de datos:

* URI
* Protocolo
* Nombre del host
