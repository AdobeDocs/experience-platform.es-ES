---
title: Manifiesto de extensión
description: Obtenga información sobre cómo configurar un archivo de manifiesto JSON que informe a Adobe Experience Platform sobre cómo utilizar correctamente su extensión.
exl-id: 7cac020b-3cfd-4a0a-a2d1-edee1be125d0
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '2606'
ht-degree: 86%

---

# Manifiesto de extensión

>[!NOTE]
>
>Adobe Experience Platform Launch se ha convertido en un grupo de tecnologías de recopilación de datos en Adobe Experience Platform. Como resultado, se han implementado varios cambios terminológicos en la documentación del producto. Consulte el siguiente [documento](../term-updates.md) para obtener una referencia consolidada de los cambios terminológicos.

En el directorio base de la extensión debe crear un archivo llamado `extension.json`. Contiene detalles esenciales sobre su extensión que permiten a Adobe Experience Platform consumirla correctamente. Algunos de los contenidos se forman siguiendo [npm `package.json`](https://docs.npmjs.com/files/package.json).

Se puede encontrar un ejemplo `extension.json` en el repositorio de extensión [Hello World](https://github.com/adobe/reactor-helloworld-extension/blob/master/extension.json) de GitHub.

Un manifiesto de extensión debe constar de lo siguiente:

| Propiedad | Descripción |
| --- | --- |
| `name` | El nombre de la extensión. Debe ser único para todas las demás extensiones y debe cumplir con [reglas de nomenclatura](#naming-rules). **Las etiquetas lo utilizan como identificador y no debe cambiarse después de publicar la extensión.** |
| `platform` | La plataforma para la extensión. El único valor aceptado en este momento es `web`. |
| `version` | La versión de la extensión. Debe seguir el formato de versión [semver](https://semver.org/). Esto es coherente con [npm version field](https://docs.npmjs.com/files/package.json#version). |
| `displayName` | El nombre legible en lenguaje natural de su extensión. Esto se mostrará a los usuarios de Experience Platform. No es necesario mencionar “etiquetas” ni “extensión”, pues los usuarios ya sabrán que están viendo una extensión de etiqueta. |
| `description` | La descripción de la extensión. Esto se mostrará a los usuarios de Experience Platform. Si la extensión permite a los usuarios implementar el producto en su sitio web, describa lo que hace el producto. No es necesario mencionar “etiquetas” ni “extensión”, pues los usuarios ya sabrán que están viendo una extensión de etiqueta. |
| `iconPath` *(Opcional)* | La ruta relativa al icono que se mostrará para la extensión. No debe comenzar con una barra oblicua. Debe hacer referencia a un archivo SVG con una extensión `.svg`. La SVG debe ser cuadrada y Experience Platform puede escalarla. |
| `author` | El autor es un objeto que debe estructurarse de la siguiente manera: <ul><li>`name`: nombre del autor de la extensión. También puede utilizar el nombre de la compañía aquí.</li><li>`url` *(opcional)*: dirección URL donde puede obtener más información sobre el autor de la extensión.</li><li>`email` *(opcional)*: dirección de correo electrónico del autor de la extensión.</li></ul>Esto es coherente con las reglas de [npm author field](https://docs.npmjs.com/files/package.json#people-fields-author-contributors). |
| `exchangeUrl` *(necesario para extensiones públicas)* | Dirección URL del listado de la extensión en Adobe Exchange. Debe coincidir con el patrón `https://www.adobeexchange.com/experiencecloud.details.######.html`. |
| `viewBasePath` | La ruta relativa al subdirectorio que contiene todas las vistas y los recursos relacionados con la vista (HTML, JavaScript, CSS e imágenes). Experience Platform alojará este directorio en un servidor web y cargará contenido de iframe desde él. Este campo es obligatorio y no debe comenzar con una barra oblicua. Por ejemplo, si todas sus vistas están contenidas en `src/view/`, el valor de `viewBasePath` sería `src/view/`. |
| `hostedLibFiles` *(Opcional)* | Muchos de nuestros usuarios prefieren alojar todos los archivos relacionados con etiquetas en su propio servidor. Esto proporciona a los usuarios un mayor nivel de certeza con respecto a la disponibilidad de archivos en tiempo de ejecución y pueden analizar fácilmente el código para detectar vulnerabilidades de seguridad. Si la parte de biblioteca de la extensión necesita cargar archivos JavaScript en tiempo de ejecución, se recomienda utilizar esta propiedad para la lista de dichos archivos. Los archivos enumerados se alojarán con la biblioteca de tiempo de ejecución de la etiqueta. La extensión puede cargar los archivos mediante una URL recuperada mediante el método [getHostedLibFileUrl](./turbine.md#get-hosted-lib-file).<br><br>Esta opción contiene una matriz con rutas relativas de archivos de biblioteca de terceros que deben alojarse. |
| `main` *(Opcional)* | La ruta relativa de un módulo de biblioteca que debe ejecutarse en tiempo de ejecución.<br><br>Este módulo siempre se incluirá en la biblioteca de tiempo de ejecución y se ejecutará. Debido a que el módulo siempre se incluye en la biblioteca de tiempo de ejecución, recomendamos utilizar únicamente un módulo &quot;principal&quot; cuando sea absolutamente necesario y mantener un código mínimo.<br><br>No se garantiza que este módulo se ejecute primero, ya que otros módulos pueden ejecutarse antes. |
| `configuration` *(Opcional)* | Esto describe la sección [configuración de la extensión](./configuration.md) de la extensión. Es necesario si necesita que los usuarios proporcionen una configuración global para la extensión. Consulte el [apéndice](#config-object) para obtener información sobre cómo se debe estructurar este campo. |
| `events` *(Opcional)* | Una matriz de definiciones de tipo [evento](./web/event-types.md). Consulte la sección del apéndice sobre [definiciones de tipo](#type-definitions) para ver la estructura de cada objeto de la matriz. |
| `conditions` *(Opcional)* | Una matriz de definiciones de tipo [condición](./web/condition-types.md). Consulte la sección del apéndice sobre [definiciones de tipo](#type-definitions) para ver la estructura de cada objeto de la matriz. |
| `actions` *(Opcional)* | Una matriz de definiciones de tipo [acción](./web/action-types.md). Consulte la sección del apéndice sobre [definiciones de tipo](#type-definitions) para ver la estructura de cada objeto de la matriz. |
| `dataElements` *(Opcional)* | Una matriz de definiciones de tipo [elemento de datos](./web/data-element-types.md). Consulte la sección del apéndice sobre [definiciones de tipo](#type-definitions) para ver la estructura de cada objeto de la matriz. |
| `sharedModules` *(Opcional)* | Una matriz de objetos de definición de módulo compartidos. Cada objeto de módulo compartido de la matriz debe estructurarse de la siguiente manera: <ul><li>`name`: nombre del módulo compartido. Tenga en cuenta que este nombre se utilizará al hacer referencia a módulos compartidos de otras extensiones como se describe en [Módulos compartidos](./web/shared.md). Este nombre nunca se muestra en ninguna interfaz de usuario. Debe ser diferente a los nombres de otros módulos compartidos en la extensión y debe cumplir con las [reglas de nomenclatura](#naming-rules). **Las etiquetas lo utilizan como identificador y no debe cambiarse después de publicar la extensión.**</li><li>`libPath`: ruta relativa al módulo compartido. No debe comenzar con una barra oblicua. Debe hacer referencia a un archivo JavaScript con una extensión `.js`.</li></ul> |

## Apéndice

### Reglas de nomenclatura {#naming-rules}

El valor de cualquier `name` campo interno `extension.json` debe cumplir con las siguientes reglas:

* Debe tener un máximo de 214 caracteres
* No debe comenzar con punto o guion bajo.
* No debe contener letras mayúsculas.
* Solo debe contener caracteres seguros para URL.

Satisfacen las reglas de [npm package name](https://docs.npmjs.com/files/package.json#name).

### Propiedades del objeto de configuración {#config-object}

El objeto de configuración debe estructurarse de la siguiente manera:

<table>
  <thead>
    <tr>
      <th>Propiedad</th>
      <th>Descripción</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><code>viewPath</code></td>
      <td>La dirección URL relativa a la vista de configuración de la extensión. Debe ser relativa a <code>viewBasePath</code> y no debe comenzar con una barra oblicua. Debe hacer referencia a un archivo HTML con una extensión <code>.html</code>. Se aceptan los sufijos de cadena de consulta y de identificador de fragmento (hashes).</td>
    </tr>
    <tr>
      <td><code>schema</code></td>
      <td>Un objeto de <a href="https://json-schema.org/">esquema JSON</a> que describe el formato de un objeto válido que se está guardando desde la vista de configuración de la extensión. Dado que usted es el desarrollador de la vista de configuración, es su responsabilidad asegurarse de que cualquier objeto de configuración guardado coincida con este esquema. Este esquema también se utilizará para la validación cuando los usuarios intenten guardar datos mediante los servicios de Experience Platform.<br><br>A continuación, se muestra un objeto de esquema de ejemplo:
<pre class="JSON language-JSON hljs">
{
  "$schema": "http://json-schema.org/draft-04/schema#",
  "type": "object",
  "properties": {
    "delay": {
      "type": "number",
      "minimum": 1
    }
  },
  "required": [
    "delay"
  ],
  "additionalProperties": false
}
</pre>
      Recomendamos utilizar una herramienta como <a href="https://www.jsonschemavalidator.net/">JSON Schema validator</a> para probar manualmente el esquema.</td>
    </tr>
    <tr>
      <td><code>transforms</code> <em>(Opcional)</em></td>
      <td>Una matriz de objetos en la que cada objeto representa una transformación que debe realizarse en cada objeto de configuración correspondiente cuando se emite en la biblioteca de tiempo de ejecución. Consulte la sección <a href="#transforms">transformaciones</a> para obtener más información sobre por qué esto puede ser necesario y cómo se utiliza.</td>
    </tr>
  </tbody>
</table>

### Definiciones de tipo {#type-definitions}

Una definición de tipo es un objeto que se utiliza para describir un evento, una condición, una acción o un tipo de elemento de datos. El objeto consta de lo siguiente:

<table>
  <thead>
    <tr>
      <th>Propiedad</th>
      <th>Descripción</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><code>name</code></td>
      <td>El nombre del tipo. Debe ser un nombre único dentro de la extensión. El nombre debe cumplir con las <a href="#naming-rules">reglas de nomenclatura</a>. <strong>Las etiquetas lo utilizan como identificador y no debe cambiarse después de publicar la extensión.</strong></td>
    </tr>
    <tr>
      <td><code>displayName</code></td>
      <td>El texto que se utilizará para representar el tipo dentro de la interfaz de usuario de recopilación de datos. Debe ser legible en lenguaje natural.</td>
    </tr>
    <tr>
      <td><code>categoryName</code> <em>(Opcional)</em></td>
      <td>Cuando se proporcione, <code>displayName</code> se enumerará en <code>categoryName</code> dentro de la interfaz de usuario. Todos los tipos que tengan el mismo <code>categoryName</code> se enumerarán en la misma categoría. Por ejemplo, si la extensión proporcionaba un tipo de evento <code>keyUp</code> y un tipo de evento <code>keyDown</code> y ambos tenían un <code>categoryName</code> de <code>Keyboard</code>, ambos tipos de evento se enumerarían en la categoría de teclado mientras el usuario seleccionaba entre la lista de tipos de evento disponibles al crear una regla. El valor de <code>categoryName</code> debe ser legible en lenguaje natural.</td>
    </tr>
    <tr>
      <td><code>libPath</code></td>
      <td>La ruta relativa al módulo de biblioteca del tipo. No debe comenzar con una barra oblicua. Debe hacer referencia a un archivo JavaScript con una extensión <code>.js</code>.</td>
    </tr>
    <tr>
      <td><code>viewPath</code> <em>(Opcional)</em></td>
      <td>La dirección URL relativa a la vista del tipo. Debe ser relativa a <code>viewBasePath</code> y no debe comenzar con una barra oblicua. Debe hacer referencia a un archivo HTML con una extensión <code>.html</code>. Se aceptan cadenas de consulta e identificadores de fragmento (hashes). Si el módulo de biblioteca del tipo no utiliza ninguna configuración de usuario, puede excluir esta propiedad y, en su lugar, Experience Platform mostrará un marcador de posición que indique que no es necesaria ninguna configuración.</td>
    </tr>
    <tr>
      <td><code>schema</code></td>
      <td>Un objeto de <a href="https://json-schema.org/">esquema JSON</a> que describe el formato de un objeto de configuración válido que el usuario puede guardar. Por lo general, el usuario configura y guarda la configuración a través de la interfaz de usuario de recopilación de datos. En estos casos, la vista de la extensión puede realizar los pasos necesarios para validar la configuración proporcionada por el usuario. Por otro lado, algunos usuarios eligen utilizar API de etiquetas directamente sin la ayuda de ninguna interfaz de usuario. El propósito de este esquema es permitir que Experience Platform valide correctamente que los objetos de configuración guardados por los usuarios, independientemente de si se utiliza una interfaz de usuario, están en un formato compatible con el módulo de biblioteca que actuará en el objeto de configuración durante la ejecución.<br><br>A continuación, se muestra un objeto de esquema de ejemplo:<br>
<pre class="JSON language-JSON hljs">
{
  "$schema": "http://json-schema.org/draft-04/schema#",
  "type": "object",
  "properties": {
    "delay": {
      "type": "number",
      "minimum": 1
    }
  },
  "required": [
    "delay"
  ],
  "additionalProperties": false
}
</pre>
      Recomendamos utilizar una herramienta como <a href="https://www.jsonschemavalidator.net/">JSON Schema validator</a> para probar manualmente el esquema.</td>
    </tr>
    <tr>
      <td><code>transforms</code> <em>(Opcional)</em></td>
      <td>Una matriz de objetos en la que cada objeto representa una transformación que debe realizarse en cada objeto de configuración correspondiente cuando se emite en la biblioteca de tiempo de ejecución. Consulte la sección sobre <a href="#transforms">transformaciones</a> para obtener más información sobre por qué esto puede ser necesario y cómo se utiliza.</td>
    </tr>
  </tbody>
</table>

### Transforms {#transforms}

En el caso de determinados casos de uso específicos, las extensiones necesitan que Experience Platform transforme los objetos de configuración guardados desde una vista antes de emitirse en la biblioteca de tiempo de ejecución de etiqueta. Puede solicitar que una o más de estas transformaciones se realicen configurando la propiedad `transforms` al definir una definición de tipo dentro de su `extension.json`. La propiedad `transforms` es una matriz de objetos en la que cada objeto representa una transformación que debe tener lugar.

Todas las transformaciones requieren un `type` y una `propertyPath`. `type` debe ser uno de `function`, `remove` y `file`, y describe qué Experience Platform de transformación debe aplicarse al objeto de configuración. La propiedad `propertyPath` es una cadena delimitada por puntos que indica a las etiquetas dónde encontrar la propiedad que debe modificarse en el objeto de configuración. Este es un objeto de configuración de ejemplo y `propertyPath`:

```js
{
  foo: {
    bar: "A string",
    baz: [
      "A",
      "B",
      "C"
    ]
  }
}
```

* Si establece una `propertyPath` de `foo.bar`, transformará el valor `"A string"`.
* Si establece una `propertyPath` de `foo.baz[]`, transformará cada valor en la matriz `baz`.
* Si establece una `propertyPath` de `foo.baz`, transformará la matriz `baz`.

Las rutas de propiedades pueden utilizar cualquier combinación de notación de objetos y matrices para aplicar transformaciones en cualquier nivel del objeto de configuración.

>[!WARNING]
>
>El uso de notación de matriz en atributos `propertyPath` (por ejemplo, `foo.baz[]`) todavía no se admite en la extensión sandbox*tool.

Las secciones siguientes describen las transformaciones disponibles y cómo utilizarlas.

#### Transformación de funciones

La transformación de funciones permite que el código escrito por los usuarios de Experience Platform lo ejecute un módulo de biblioteca dentro de la biblioteca de tiempo de ejecución de etiqueta emitida.

Supongamos que queremos proporcionar un tipo de acción de &quot;secuencia de comandos personalizada&quot;. La vista de acción &quot;script personalizado&quot; puede proporcionar un área de texto en la que el usuario puede introducir código. Supongamos que un usuario ha introducido el siguiente código en el área de texto:

`console.log('Welcome, ' + username +'. This is ZomboCom.');`

Cuando el usuario guarda la regla, el objeto de configuración guardado por la vista puede tener este aspecto:

```javascript
{
  foo: {
    bar: "console.log('Welcome, ' + username +'. This is ZomboCom.');"
  }
}
```

Cuando una regla que utiliza nuestra acción se activa dentro de la biblioteca de tiempo de ejecución de etiqueta, queremos ejecutar el código del usuario y pasarle un nombre de usuario.

En el momento en que el objeto de configuración se guarda desde la vista del tipo de acción, el código del usuario es simplemente una cadena. Esto es positivo porque se puede serializar correctamente desde JSON y hacia JSON; sin embargo, también es malo porque, por lo general, se emitiría en la biblioteca de tiempo de ejecución de etiqueta como cadena, en lugar de como función ejecutable. Aunque podría intentar ejecutar el código en el módulo de biblioteca del tipo de acción mediante [`eval`](https://developer.mozilla.org/es-ES/docs/Web/JavaScript/Reference/Global_Objects/eval) o un [constructor de funciones](https://developer.mozilla.org/es-ES/docs/Web/JavaScript/Referencia/Objetos_globales/Function), se desaconseja porque las [políticas de seguridad de contenido](https://developer.mozilla.org/es-ES/docs/Web/HTTP/CSP) podrían bloquear la ejecución.

Como solución alternativa a esta situación, el uso de la transformación de funciones indica a Experience Platform que ajuste el código del usuario en una función ejecutable cuando se emite en la biblioteca de tiempo de ejecución de etiqueta. Para solucionar el problema del ejemplo, definiríamos la transformación de la definición de tipo en `extension.json` de la siguiente manera:

```json
{
  "transforms": [
    {
      "type": "function",
      "propertyPath": "foo.bar",
      "parameters": ["username"]
    }
  ]
}
```

* `type` define el tipo de transformación que debe aplicarse al objeto de configuración.
* `propertyPath` es una cadena delimitada por puntos que indica a Experience Platform dónde encontrar la propiedad que debe modificarse en el objeto de configuración.
* `parameters` es una matriz de nombres de parámetros que deben incluirse en la firma de la función de ajuste.

Cuando el objeto de configuración se emite en la biblioteca de tiempo de ejecución de etiqueta, se transforma en lo siguiente:

```javascript
{
  foo: {
    bar: function(username) {
      console.log('Welcome, ' + username +'. This is ZomboCom.');
    }
  }
}
```

El módulo de biblioteca puede, así, llamar a la función que contiene el código del usuario y pasar el argumento `username`.

#### Transformación de archivos

La transformación de archivos permite que el código escrito por los usuarios de Experience Platform se emita en un archivo independiente de la biblioteca de tiempo de ejecución de etiquetas. El archivo se alojará junto a la biblioteca de tiempo de ejecución de etiqueta y, a continuación, se podrá cargar según sea necesario en la extensión durante el tiempo de ejecución.

Supongamos que queremos proporcionar un tipo de acción de &quot;secuencia de comandos personalizada&quot;. La vista del tipo de acción puede proporcionar un área de texto donde el usuario puede introducir código. Supongamos que un usuario ha introducido el siguiente código en el área de texto:

`console.log('This is ZomboCom.');`

Cuando el usuario guarda la regla, el objeto de configuración guardado por la vista puede tener este aspecto:

```js
{
  foo: {
    bar: "console.log('This is ZomboCom.');"
  }
}
```

Queremos que el código del usuario se coloque en un archivo independiente en lugar de incluirse en la biblioteca de tiempo de ejecución de etiqueta. Cuando una regla que utiliza nuestra acción se activa en la biblioteca de tiempo de ejecución de etiqueta, nos gustaría cargar el código del usuario añadiendo un elemento de secuencia de comandos al cuerpo del documento. Para solucionar el problema de ejemplo, definiríamos la transformación de la definición de tipo de acción en `extension.json` de la siguiente manera:

```json
{
  "transforms": [
    {
      "type": "file",
      "propertyPath": "foo.bar"
    }
  ]
}
```

* `type` define el tipo de transformación que debe aplicarse al objeto de configuración.
* `propertyPath` es una cadena delimitada por puntos que indica a Experience Platform dónde encontrar la propiedad que debe modificarse en el objeto de configuración.

Cuando el objeto de configuración se emite en la biblioteca de tiempo de ejecución de etiqueta, se transforma en lo siguiente:

```javascript
{
  foo: {
    bar: "//launch.cdn.com/path/abc.js"
  }
}
```

En este caso, el valor de `foo.bar` se ha transformado en una dirección URL. La dirección URL exacta se determinará en el momento de crear la biblioteca. El archivo siempre recibirá una extensión `.js` y se enviará con un tipo MIME orientado a JavaScript. Podemos añadir compatibilidad con otros tipos MIME en el futuro.

#### Eliminación de la transformación

De forma predeterminada, todas las propiedades del objeto de configuración se emiten en la biblioteca de tiempo de ejecución de etiqueta. Si determinadas propiedades solo se utilizan para la vista de extensión, especialmente si contienen información confidencial (por ejemplo, un token secreto), debe utilizar la transformación de eliminación para evitar que la información se emita en la biblioteca de tiempo de ejecución de etiqueta.

Supongamos que queremos proporcionar un nuevo tipo de acción. La vista del tipo de acción puede proporcionar una entrada en la que el usuario puede introducir una clave secreta que permita la conexión a una API específica. Supongamos que un usuario ha introducido el siguiente texto en la entrada:

`ABCDEFG`

Cuando el usuario guarda la regla, el objeto de configuración guardado por la vista puede tener este aspecto:

```js
{
  foo: {
    bar: "ABCDEFG"
  }
}
```

No queremos incluir la propiedad `bar` en la biblioteca de tiempo de ejecución de etiquetas. Para solucionar el problema de ejemplo, definiríamos la transformación de la definición de tipo de acción en `extension.json` de la siguiente manera:

```json
{
  "transforms": [
    {
      "type": "remove",
      "propertyPath": "foo.bar"
    }
  ]
}
```

* `type` define el tipo de transformación que debe aplicarse al objeto de configuración.
* `propertyPath` es una cadena delimitada por puntos que indica a Experience Platform dónde encontrar la propiedad que debe modificarse en el objeto de configuración.

Cuando el objeto de configuración se emite en la biblioteca de tiempo de ejecución de etiqueta, se transforma en lo siguiente:

```js
{
  foo: {
  }
}
```

En este caso, el valor de `foo.bar` se ha eliminado del objeto de configuración.
