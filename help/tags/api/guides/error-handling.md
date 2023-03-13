---
title: Control de errores
description: Descubra cómo se gestionan los errores en la API de Reactor.
exl-id: 336c0ced-1067-4519-94e1-85aea700fce6
source-git-commit: f3c23665229a83d6c63c7d6026ebf463069d8ad9
workflow-type: tm+mt
source-wordcount: '1062'
ht-degree: 99%

---

# Control de errores

Cuando se produce un problema al realizar una llamada a la API de Reactor, puede dar error de una de las siguientes maneras:

* **Errores inmediatos**: Al realizar una solicitud que resulta en un error inmediato, la API devuelve una respuesta de error, con el estado HTTP reflejando el tipo general de error que se produjo.
* **Errores retrasados**: Al realizar una solicitud de API que resulta en un error retrasado (como una actividad asincrónica), la API puede devolver un error en el caso `meta.status_details` de un recurso relacionado.

## Formato de error

Las respuestas de error pretenden ajustarse a la [especificación de errores JSON:API](http://jsonapi.org/format/#errors) y, en general, adherirse a la siguiente estructura:

```json
{
  "errors": [
    {
      "id": "8a5526da-ab12-4be9-b084-2efe537f388c",
      "status": "404",
      "code": "not-found",
      "title": "Record Not Found",
      "meta": {
        "request_id": "jfb0dQ2e0XVTkQ6AOfEJFfTDjguw9x3d"
      },
      "source": {
        "pointer": "/data"
      }
    }
  ]
}
```

| Propiedad | Descripción |
| --- | --- |
| `id` | Un identificador único para esta incidencia particular del problema. |
| `status` | El código de estado HTTP aplicable a este problema, expresado como un valor de cadena. |
| `code` | Un código de error específico de la aplicación, expresado como valor de cadena. |
| `title` | Un breve resumen legible en lenguaje natural del problema que **no debería cambiar** de ocurrencia a ocurrencia, excepto para fines de localización. |
| `detail` | Una explicación legible en lenguaje natural específica de esta ocurrencia del problema. Al igual que `title`, el valor de este campo se puede localizar. |
| `source` | Un objeto que contiene referencias al origen del error, incluyendo opcionalmente cualquiera de los siguientes miembros:<ul><li>`pointer`: una cadena de puntero [JSON (RFC6901)](https://datatracker.ietf.org/doc/html/rfc6901) que hace referencia a la entidad asociada en el documento de solicitud (por ejemplo, `/data` para un objeto de datos principal o `/data/attributes/title` para un atributo específico).</li></ul> |
| `meta` | Un objeto que contiene metadatos no estándar sobre el error. |

{style="table-layout:auto"}

## Referencia de error

En la tabla siguiente se enumeran los diferentes errores que puede devolver la API.

| Título de error | Descripción |
| --- | --- |
| `authentication-failure` | El token de acceso de IMS no es válido. Para obtener un nuevo token de acceso, vuelva a iniciar sesión. O, en el caso de cuentas técnicas, generando un nuevo JWT e intercambiando por un token de acceso IMS. |
| `connection-refused` | No se ha podido establecer una conexión con el servidor. |
| `decrypt-bad-passphrase` | No se han podido descifrar los datos con la frase de contraseña proporcionada. |
| `decrypt-failed` | No se han podido descifrar los datos con la clave privada proporcionada. Asegúrese de que la clave funciona localmente y que se han eliminado los espacios en blanco. |
| `decrypt-no-data` | Los datos no se pueden descifrar sin una clave privada. Proporcione una clave privada cifrada. |
| `delegate-descriptor-unresolved` | La extensión no ha proporcionado la definición esperada de este descriptor delegado. Puede que sea necesario actualizar la extensión. |
| `deleted-resources` | Se han eliminado los recursos que usted está intentando agregar a la biblioteca. |
| `environment-in-use` | A cada entorno solo se le puede asignar una compilación de biblioteca de forma simultánea. La opción 1 es elegir un entorno diferente. La opción 2 es liberar este entorno moviendo la biblioteca a otro o eliminando la biblioteca. |
| `environment-required` | La biblioteca debe tener un entorno asignado para poder crear una compilación. |
| `extension-not-found` | La extensión que define un elemento de datos o un componente de regla no se incluye en la biblioteca. Asegúrese de que todas las extensiones requeridas se hayan añadido a la biblioteca. |
| `extension-package-path-error` | Una ruta definida en extension.json no se ha construido correctamente. |
| `extension-package-transform-definition-error` | Ha definido una transformación no válida para una propiedad de objeto. Cada propiedad de objeto puede tener una transformación definida y debe ser una transformación de archivo o una transformación de función. |
| `extension-package-zip-error` | Error al descomprimir ExtensionPackage o comprimir los archivos para su distribución. |
| `host-in-use` | Un host no se puede eliminar si lo utilizan uno o más entornos. |
| `host-required` | El entorno asignado a esta biblioteca no tiene un host válido. Compruebe qué entorno está asignado a la biblioteca. A continuación, asigne un host válido a ese entorno. |
| `host-type-error` | Solo es necesario comprobar las credenciales de los hosts SFTP para poder utilizarlos, por lo que la prueba previa solo está disponible para ese tipo de host. |
| `illegal-custom-code-transform` | No se le permite utilizar la transformación customCode. Especifique una función o transformación de archivo. |
| `ims-not-authorized` | Error desconocido al autorizar su cuenta. Inténtelo de nuevo más tarde. |
| `ims-session-error` | Hay un problema con la sesión iniciada. Cierre la sesión y vuelva a iniciarla. |
| `internal-error` | Error interno. Espere unos minutos e inténtelo de nuevo. Si el problema persiste, póngase en contacto con el servicio de atención al cliente. |
| `invalid-data_element` | No se puede añadir un elemento de datos no válido a una biblioteca. |
| `invalid-embed_code` | No se trata de un código incrustado válido o está intentando vincularlo a un entorno de ensayo o desarrollo. Los códigos incrustados de administración dinámica de etiquetas (Dynamic Tag Management, DTM) solo se pueden vincular a entornos de producción. |
| `invalid-extension` | No se puede añadir una extensión no válida a una biblioteca. |
| `invalid-extension_package_id` | Solo puede modificar algunas de las propiedades de objeto de un paquete de extensión. Intentó modificar una de las que no están permitidas. |
| `invalid-new-owner-org-id` | El identificador de organización que intentó asignar no es un identificador de organización válido. |
| `invalid-org` | Su organización activa no tiene acceso a la API. Compruebe que está utilizando la organización correcta. |
| `invalid-rule` | No se puede añadir una regla no válida a una biblioteca. |
| `invalid-settings-syntax` | Se encontró un error de sintaxis al analizar la configuración JSON. |
| `library-file-not-found` | No se encontró un archivo requerido definido en extension.json dentro del paquete zip. |
| `minification-error` | No se pudo compilar el código porque no es válido. |
| `multiple-revisions` | En una biblioteca solo se puede incluir una revisión de cada recurso. |
| `no-available-orgs` | Esta cuenta de usuario no pertenece a ningún perfil de producto que tenga acceso a etiquetas. Utilice Admin Console para añadir a este usuario a un perfil de producto con derechos de etiquetas. |
| `not-authorized` | Esta cuenta de usuario no tiene los permisos necesarios para realizar esta acción. |
| `not-found` | No se pudo encontrar el registro. Compruebe el identificador del objeto que está intentando recuperar. |
| `not-unique` | El nombre que intenta usar ya está en uso. Para este recurso, la propiedad “name” debe ser única. |
| `public-release-not-authorized` | El lanzamiento público de extensiones está coordinado por `launch-ext-dev@adobe.com`. Para obtener más información, consulte el documento sobre [lanzamiento de extensiones](../../extension-dev/submit/release.md). |
| `read-only` | Este recurso es de solo lectura y no se puede modificar. |
| `session-timeout` | La sesión del usuario ha caducado. Cierre la sesión y vuelva a iniciarla. |
| `sftp-authentication-failed` | Error de autenticación para la conexión SFTP. |
| `sftp-connection-timeout` | Se ha agotado el tiempo de espera de la conexión SFTP. |
| `sftp-exception` | Se ha encontrado una excepción al usar SFTP para conectarse al servidor. |
| `sftp-status-exception` | Se encontró una excepción SFTP al intentar comunicarse con el servidor. |
| `socket-error` | Se encontró un error de socket al intentar comunicarse con el servidor. |
| `ssh-disconnect` | Se desconectó la sesión SSH. |
| `timeout-error` | Se agotó el tiempo de espera de la conexión con el servidor. |
| `unknown-error` | Error inesperado. Puede intentarlo más tarde o llamar al Servicio de atención al cliente para explicar qué estaba haciendo cuando se produjo. |
| `unsupported-custom-code-language` | Se ha proporcionado un idioma de código personalizado que no es compatible. |
| `upgraded-extension-required` | Una vez que haya instalado una actualización de extensión, debe incluirla en todas las bibliotecas hasta que la actualización llegue a Producción. La única excepción es que la extensión aún no se haya publicado. |
| `upstream-build-required` | Se requiere una compilación correcta para la biblioteca de flujo ascendente antes de poder crearla. |

{style="table-layout:auto"}
