---
title: Cargar e implementar pruebas de extremo a extremo para una extensión
description: Obtenga información sobre cómo validar, cargar y probar la extensión en Adobe Experience Platform.
source-git-commit: 7e27735697882065566ebdeccc36998ec368e404
workflow-type: tm+mt
source-wordcount: '2392'
ht-degree: 35%

---

# Carga e implementación de pruebas de extremo a extremo

>[!NOTE]
>
>Adobe Experience Platform Launch se ha convertido en un conjunto de tecnologías de recopilación de datos en Adobe Experience Platform. Como resultado, se han implementado varios cambios terminológicos en la documentación del producto. Consulte el siguiente [documento](../../term-updates.md) para obtener una referencia consolidada de los cambios terminológicos.

Para probar las extensiones de etiquetas en Adobe Experience Platform, utilice la API de etiquetas o las herramientas de línea de comandos para cargar los paquetes de extensión. A continuación, utilice la interfaz de usuario de recopilación de datos para instalar el paquete de extensión en una propiedad y ejercer sus capacidades dentro de una biblioteca de etiquetas y crear.

Este documento explica cómo implementar pruebas de extremo a extremo para la extensión.

>[!NOTE]
>
>Esta guía presupone que está utilizando MacOS con Node.js y npm instalados y disponibles.

## Validación de la extensión {#validate}

Una vez que su equipo esté satisfecho con el rendimiento de la extensión y los resultados que ven en la herramienta [Sandbox](https://www.npmjs.com/package/@adobe/reactor-sandbox#running-the-sandbox), debe estar listo para cargar el paquete de extensión en etiquetas.

Antes de cargar, compruebe que estén presentes los campos o la configuración requeridos. Por ejemplo, es recomendable revisar el [manifiesto de extensión](../manifest.md), la [configuración de extensión](../configuration.md), las [vistas](../web/views.md) y los [módulos de biblioteca](../web/format.md) (como mínimo).

Un ejemplo específico es el archivo de logotipo: añada una línea `"iconPath": "example.svg",` al archivo `extension.json` e incluya ese archivo de imagen de logotipo en el proyecto. Esta es la ruta relativa al icono que se mostrará para la extensión. No debería comenzar con una barra oblicua. Debe hacer referencia a un archivo SVG con una extensión `.svg`. El SVG debe aparecer normalmente cuando se procesa en forma cuadrada y la interfaz de usuario puede escalarlo. Consulte el [How to Scale SVG article](https://css-tricks.com/scale-svg/) para obtener más información.

>[!NOTE]
>
>En el caso de las extensiones públicas, incluya un elemento en su `extension.json` con un vínculo a su listado de Exchange. El [manifiesto de extensión](../manifest.md) debe incluir una entrada como esta: `"exchangeUrl":"https://www.adobeexchange.com/experiencecloud.details.12345.html"` que apunte a la dirección URL de su listado de Exchange.

## Creación de una integración de Adobe I/O {#integration}

Para utilizar la API o las herramientas de línea de comandos, necesita una cuenta técnica con Adobe I/O. Debe crear la cuenta técnica en la consola de E/S y, a continuación, utilizar la herramienta Cargar para cargar el paquete de extensión.

Para obtener información sobre la creación de una cuenta técnica para su uso con etiquetas en Adobe Experience Platform, consulte la guía [Tokens de acceso](https://developer.adobelaunch.com/api/guides/access_tokens/).

>[!IMPORTANT]
>
>Para crear una integración en Adobe I/O, debe ser administrador de organización de Experience Cloud o desarrollador de organización de Experience Cloud.

Si no puede crear una integración, es probable que no tenga los permisos correctos. Esto requerirá que un administrador de organización complete los pasos o que le asigne como desarrollador.

## Carga del paquete de extensión {#upload}

Ahora que tiene credenciales, está listo para probar el paquete de extensión de principio a fin.

Cuando carga el paquete de extensión por primera vez, pasa a un estado de `development`. Esto significa que solo es visible para su propia organización y solo con una propiedad que se haya marcado para el desarrollo de extensiones.

Utilice la línea de comandos para ejecutar el siguiente comando dentro del directorio que contiene su paquete .zip.

```bash
npx @adobe/reactor-uploader
```

`npx` le permite descargar y ejecutar un paquete npm sin instalarlo realmente en su equipo. Es la forma más sencilla de ejecutar el Uploader.

El Cargador requiere que introduzca varias informaciones. El ID de cuenta técnica, la clave de API y otros fragmentos de información se pueden recuperar desde la consola de Adobe I/O. Vaya a la [página Integraciones](https://console.adobe.io/integrations) en la consola de I/O. Seleccione la organización correcta en el menú desplegable, busque la integración correcta y seleccione **[!UICONTROL View]**.

- ¿Cuál es la ruta a la clave privada? /path/to/private.key. Este es el lugar donde guardó la clave privada en el paso 2 anterior.
- ¿Cuál es su ID de organización? Copie y pegue esto desde la página de información general de la consola de E/S que dejó abierta anteriormente.
- ¿Cuál es su ID de cuenta técnica? Copie y pegue esto desde la consola de E/S.
- ¿Cuál es su clave de API? Copie y pegue esto desde la consola de E/S.
- ¿Cuál es el secreto del cliente? Copie y pegue esto desde la consola de E/S.
- ¿Cuál es la ruta al extension_package que desea cargar? /path/to/extension_package.zip. Si invoca el cargador desde el directorio que contiene el paquete .zip, solo puede seleccionarlo en la lista en lugar de escribir la ruta.

El paquete de extensión se cargará y el cargador le proporcionará el ID del extension_package.

>[!NOTE]
>
>Al cargar o aplicar parches, los paquetes de extensión se colocan en un estado pendiente mientras el sistema extrae el paquete y lo implementa de forma asíncrona. Mientras se lleva a cabo este proceso, puede sondear el `extension_package` ID para su estado mediante la API y dentro de la interfaz de usuario de la recopilación de datos. Verá una tarjeta de extensión en el catálogo marcado como Pendiente.

>[!NOTE]
>
>Si planea ejecutar el cargador a menudo, poner toda esta información en cada momento puede ser una carga. También puede pasarlos como argumentos desde la línea de comandos. Consulte la sección [Command Line Arguments (argumentos de la línea de comandos)](https://www.npmjs.com/package/@adobe/reactor-uploader#command-line-arguments) de los documentos de NPM para obtener más información.

## Creación de una propiedad de desarrollo {#property}

Después de iniciar sesión en la interfaz de usuario de la recopilación de datos, se muestra la pantalla Propiedades . Una propiedad es un contenedor para las etiquetas que desea implementar y se puede utilizar en uno o varios sitios.

![](../images/getting-started/properties-screen.png)

La primera vez que inicie sesión no verá ninguna propiedad en la pantalla. Seleccione **Nueva propiedad** para crear una. Escriba un nombre y una dirección URL. Utilice la dirección URL del sitio de prueba o la página donde probará la extensión. Este campo de dominio lo pueden utilizar algunas extensiones o una condición de con la extensión principal.

>[!NOTE]
>
>`localhost` no funcionará como un valor de URL. En su lugar, utilice cualquier valor de prueba si utiliza una dirección URL `localhost`. Por ejemplo, ejemplo.com.

Para utilizar esta propiedad para pruebas de desarrollo de extensiones, debe expandir los **OPTIONS AVANZADOS** y asegurarse de marcar la casilla **Configure for extension development**.

![](../images/getting-started/launch-create-a-dev-property.png)

Seleccione **Guardar** en la parte inferior para guardar la nueva propiedad.

Aparecerá la pantalla Propiedades. Seleccione el nombre de la propiedad que acaba de crear. Aparece la pantalla Información general de la propiedad . Proporciona vínculos a cada área del sistema con los vínculos de navegación global en la columna de la izquierda.

## Instalación de la extensión {#install-extension}

Para instalar la extensión en esta propiedad, seleccione el vínculo **Extensions** en los vínculos de navegación principales en la columna izquierda. La extensión **Core** se muestra en la pantalla **Installed**. La Extensión principal contiene toda la funcionalidad de administración de etiquetas dentro de la recopilación de datos.

![](../images/getting-started/extensions.png)

Para añadir la extensión, seleccione la pestaña **Catalog**.

![](../images/getting-started/catalog.png)

El catálogo muestra los iconos de tarjeta de cada extensión disponible. Si la extensión no se muestra en el catálogo, asegúrese de haber completado los pasos anteriores en las secciones Configuración de la consola de administración de Adobe y Creación del paquete de extensión . El paquete de extensión también puede aparecer como Pendiente si Platform no ha completado el procesamiento inicial.

Si ha seguido los pasos anteriores y aún no ve un paquete de extensión Pendiente o Fallido en el catálogo, debe comprobar el estado del paquete de extensión directamente mediante la API. Para obtener información sobre cómo realizar la llamada de API adecuada, lea [Buscar un ExtensionPackage](https://developer.adobelaunch.com/api/reference/1.0/extension_packages/fetch/) en la documentación de la API.

Una vez que el paquete de extensión haya terminado de procesarse, seleccione **Install** en la parte inferior de la tarjeta.

![](../images/getting-started/install-extension.png)

Se abre la pantalla de configuración (siempre que la extensión tenga una). Añada la información necesaria para configurar la extensión y seleccione **Guardar** en la parte inferior. El ejemplo de pantalla de configuración que se ve aquí utiliza la extensión de Facebook que requiere un ID de píxel.

![](../images/getting-started/fb-extension.png)

Ahora debería ver la pantalla **Extensiones instaladas** con la extensión Core y la extensión.

![](../images/getting-started/extension-installed.png)

## Creación de recursos para probar la extensión {#resources}

Las extensiones proporcionan nuevas funciones a los usuarios de Adobe Experience Platform. Normalmente se muestran en Elementos de datos o en el Generador de reglas.

### Elementos de datos

El propósito de los elementos de datos de etiquetas es ayudar a los usuarios a mantener los valores. Cada elemento de datos es una asignación o un indicador a los datos de origen. Un solo elemento de datos es una variable cuyo valor puede asignarse a cadenas de consulta, direcciones URL, valores de cookies, variables JavaScript, etc. Seleccione **Elementos de datos** en la barra de navegación izquierda y **Crear nuevo elemento de datos**.

![](../images/getting-started/data-element-create-new-link.png)

Las extensiones pueden definir tipos de elementos de datos si es necesario para que funcione la extensión o simplemente por comodidad para los usuarios. Cuando una extensión proporciona tipos de elementos de datos, aparecen en una lista desplegable para los usuarios en la pantalla **Crear elemento de datos**:

![](../images/getting-started/create-data-element.png)

Cuando un usuario selecciona la extensión desde la lista desplegable **Extension**, la lista desplegable **Tipo de elemento de datos** se rellena con cualquier tipo de elemento de datos proporcionado por la extensión. A continuación, el usuario puede asignar cada elemento de datos a su valor de origen. Los elementos de datos se pueden utilizar cuando se generan reglas en el Evento de cambio de elemento de datos o en el Evento de código personalizado para activar una regla que se va a ejecutar. Un elemento de datos también se puede utilizar en la condición del elemento de datos u otras condiciones, excepciones o acciones de una regla.

Una vez creado el elemento de datos (con la asignación configurada), los usuarios pueden hacer referencia a los datos de origen simplemente haciendo referencia al elemento de datos. Si el origen del valor cambia alguna vez (rediseños del sitio, etc.) los usuarios solo deben actualizar la asignación una vez en la interfaz de usuario de recopilación de datos y todos los elementos de datos recibirán automáticamente el nuevo valor de origen.

### Reglas

Seleccione el vínculo **Rules** en el panel de navegación izquierdo y, a continuación, **Crear nueva regla**.

![](../images/getting-started/rules-link.png)

En primer lugar, escriba un nombre descriptivo para la regla. La pantalla **Crear regla** está configurada como una instrucción `if-then`.

![](../images/getting-started/create-new-rule.png)

Si se produce un evento, las condiciones pasan y no hay excepciones, la acción se activa. Este mismo flujo existe en extensiones donde puede crear o aprovechar eventos, condiciones, excepciones, elementos de datos o acciones.

Con el ejemplo de la extensión de Facebook, añada un evento cada vez que se cargue una página en el sitio de prueba.

![](../images/getting-started/load-event.png)

El `Window Loaded` **Tipo de evento** garantiza que esta regla se active cada vez que una página se cargue en el sitio de prueba. Seleccione **Conservar cambios**. Para este ejemplo, ignore **Conditions** ya que la regla debe activarse para cualquier página del sitio de prueba.

En **ACTIONS** seleccione **Add**. Aparece la pantalla **Action Configuration**. A continuación, debe elegir la extensión a la que se aplicará la regla y la acción que se producirá cuando se active la regla. Seleccione **Facebook Pixel** en la lista desplegable **Extension** y **Enviar vista de página** en la lista desplegable **Tipo de acción**. Seleccione **Conservar cambios** y luego **Guardar** en la siguiente pantalla **Editar regla**.

![](../images/getting-started/action-configuration.png)

Al probar la extensión, seleccione cualquier evento, condición, etc. relevantes. que proporcione la extensión en cualquier número de reglas.

## Publicación de los cambios {#publish}

En la navegación principal, seleccione **Publicación** y, a continuación, seleccione el vínculo **Añadir nueva biblioteca**:

![](../images/getting-started/add-new-library.png)

Una biblioteca es un conjunto de instrucciones que indican cómo interactúan las extensiones, los elementos de datos y las reglas entre sí y con el sitio web. Las bibliotecas se compilan en compilaciones. Una biblioteca puede contener tantos cambios como desee aplicar o probar a la vez.

En la pantalla **Crear biblioteca**, añada un nombre en el campo de texto **Nombre**. Las etiquetas proporcionan un entorno de desarrollo predeterminado denominado **Development**. Seleccione **Desarrollo** en la lista desplegable **Entorno**. Para simplificar, añada todos los recursos disponibles. Seleccione **Agregar todos los recursos modificados** y, a continuación, seleccione **Guardar**.

>[!NOTE]
>
>Cuando se añade un recurso a una biblioteca, se toma una instantánea de dicho recurso en ese momento exacto y se añade a la biblioteca. Cuando realice cambios en los recursos más adelante (por ejemplo, como resultado de las correcciones que necesita), también deberá actualizar la biblioteca para incluir los cambios más recientes en los recursos. El botón **Añadir todos los recursos cambiados** también es útil para este propósito.

![](../images/getting-started/create-new-library.png)

Ahora que todos los cambios se han incluido en la biblioteca recién creada (denominada **dev** en el ejemplo proporcionado), seleccione **Guardar y crear en desarrollo**.

![](../images/getting-started/build-for-dev.png)

Una vez completado el proceso de compilación, aparece un indicador de éxito **verde** junto al nombre de la biblioteca.

![](../images/getting-started/successful-build.png)

La biblioteca de etiquetas ya está publicada y disponible para su uso. La página de prueba debe utilizar la biblioteca recién creada para probar el comportamiento de la página para el usuario final en un explorador.

## Instalación de etiquetas en un sitio de prueba {#install-data-collection-tags}

Las instrucciones de instalación están disponibles en la pestaña Entornos . Esta página muestra todos los entornos disponibles y también le permite crear más. Cuando la biblioteca se haya publicado en el entorno de desarrollo, seleccione el icono de cuadro en la columna **INSTALL** de la fila **Development**.

![](../images/getting-started/launch-installation-instructions.png)

Aparece el cuadro de diálogo **Web Install Instructions** para el entorno de desarrollo. Seleccione el icono de copia para copiar toda la etiqueta `<script>`.

![](../images/getting-started/launch-installation-instructions-dialogue.png)

Complete la instalación colocando esta única etiqueta `<script>` dentro de la sección `<head>` del documento o la plantilla del sitio. A continuación, visite el sitio de prueba para examinar el comportamiento de la biblioteca de etiquetas publicada.

## Prueba {#test}

A continuación se muestra una lista de comandos de consola útiles para validar la extensión en la página o el sitio de prueba.

- `_satellite.setDebug(true);` habilitará el modo de depuración y emitirá instrucciones de registro útiles a la consola.
- El objeto `_satellite._container` contiene información útil sobre la biblioteca implementada, incluidos detalles sobre la compilación, los elementos de datos, las reglas y las extensiones incluidas.

El objetivo de esta prueba es comprobar la funcionalidad de la biblioteca implementada y garantizar que el paquete de extensión se comporta como se espera después de que se haya cumplido en una biblioteca.

Cuando descubre cambios que deben realizarse en el paquete de extensión, el proceso de iteración es similar al proceso de desarrollo.

1. Modifique el código del proyecto..
1. Valide los cambios con la herramienta Simulador para pruebas.
1. Utilice la herramienta Packager para crear un nuevo paquete .zip
1. Utilice la herramienta Cargar para cargar el nuevo paquete .zip. El proceso sigue las mismas instrucciones que antes con respecto a la carga inicial. Sin embargo, observará que, como ya hay un paquete de extensión de ese nombre en el modo de desarrollo, este nuevo paquete sobrescribirá la versión anterior en lugar de crear una nueva.

   >[!NOTE]
   >
   >Los argumentos se pueden pasar en la línea de comandos para ahorrar tiempo evitando la introducción repetida de credenciales. Para obtener más información sobre esto, lea la [documentación del reactor-cargador](https://www.npmjs.com/package/@adobe/reactor-uploader).
1. El paso de instalación se puede omitir al actualizar un paquete existente.
1. Modificar recursos : si se ha cambiado la configuración de cualquiera de los componentes de la extensión, deberá actualizar esos recursos en la interfaz de usuario de la recopilación de datos.
1. Agregue los cambios más recientes a la biblioteca y vuelva a compilar.
1. Complete otra ronda de pruebas.
