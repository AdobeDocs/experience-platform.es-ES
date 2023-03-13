---
title: Notas de la versión de la extensión Core
description: Últimas notas de la versión de la extensión Core en Adobe Experience Platform.
exl-id: a049b2d5-7a00-435d-bcc7-112658a53a1e
source-git-commit: 88939d674c0002590939004e0235d3da8b072118
workflow-type: tm+mt
source-wordcount: '1565'
ht-degree: 74%

---

# Notas de la versión de la extensión Core

>[!NOTE]
>
>Adobe Experience Platform Launch se ha convertido en un conjunto de tecnologías de recopilación de datos en Adobe Experience Platform. Como resultado, se han implementado varios cambios terminológicos en la documentación del producto. Consulte el siguiente [documento](../../../term-updates.md) para obtener una referencia consolidada de los cambios terminológicos.

## 4 de enero de 2022

Versión 3.3.0

* Modifica el [Acción de llamada directa de déclencheur](./overview.md#direct-call-action) para poder proporcionar información de evento personalizada para enviar a reglas de llamada directa.

## 8 de octubre de 2021

Versión 3.2.2

* Corrija el esquema JSON del elemento de datos de valor condicional para todos los operadores disponibles.
* Corregir https://github.com/adobe/reactor-extension-core/issues/64.

## 23 de septiembre de 2021

Versión 3.2.1

* Se corrigió un error en el cual la inicialización de la vista del elemento de datos de valor condicional no funcionaba correctamente cuando los valores de campo eran 0.

## 23 de septiembre de 2021

Versión 3.2.0

Se introdujeron los siguientes cambios en el elemento de datos Valor condicional:

* Agregue una casilla de verificación para los valores condicionales y de reserva que permita al usuario elegir si desea que el valor devuelto sea indefinido.
* Los valores de número se exponen como números en el objeto de configuración.
* El valor condicional ya no es necesario para que pueda comportarse del mismo modo que el valor de reserva.

## 17 de septiembre de 2021

Versión 3.1.1

* Se ha corregido un error de JS que impedía cargar la vista de condición de intervalo de fechas.

## 16 de septiembre de 2021

Versión 3.1.0

Se han añadido nuevos elementos de datos:

* Objeto combinado: seleccione varios elementos de datos que proporcionarán un objeto cada uno. Estos objetos se combinarán profunda (recursivamente) para producir un nuevo objeto.
* Valor condicional: Devuelva uno de los dos valores (conditionalValue o fallbackValue) en función del resultado de la comparación.
* Entorno de tiempo de ejecución: devuelva una de las siguientes variables de entorno de Launch: fase de entorno, fecha de compilación de la biblioteca, nombre de propiedad, ID de propiedad, nombre de regla, ID de regla, tipo de evento, carga útil de detalle del evento, identificador de llamada directa.
* Herramientas de JavaScript: contenedor para operaciones comunes de JavaScript: manipulación básica de cadenas (reemplazar, subcadena, coincidencia de regex, primer y último índice, división, fracción), operaciones básicas de matrices (división, unión, desplazamiento) y operaciones básicas universales (división, longitud).
* Atributos del dispositivo: devuelven atributos del dispositivo como el tamaño de la ventana o el tamaño de la pantalla.

## 11 de agosto de 2021

Versión 3.0.0

* PDCL-6153: Añade compatibilidad para extraer de forma fiable la URL completa para acciones de código personalizado en caché.

La versión 3.0.0 de la extensión Core está asociada con cambios en [Versión 27.2.0 del tiempo de ejecución web de Turbine](https://github.com/adobe/reactor-turbine/releases/tag/v27.2.0), que permite a los usuarios cargar su biblioteca entre muchas regiones de alojamiento administradas por Adobe si la empresa del usuario admite CDN Premium.

Esta actualización es opcional y compatible con versiones anteriores para usuarios sin CDN Premium, y obligatoria para los clientes que tienen CDN Premium habilitado en su empresa.

## 20 de mayo de 2021

Versión 2.0.7

* Corrige un problema por el que las interacciones del ratón en las entradas de texto ya no funcionaban correctamente.
* Vuelve obsoleto el uso de las condiciones del explorador y del sistema operativo.

## 4 de mayo de 2021

Versión 2.0.6

* Pequeña actualización para corregir los iconos que se distorsionan cuando cambia el tamaño de la pantalla.

## 11 de marzo de 2021

Versión 2.0.5

* Se ha actualizado el código de la evaluación en tiempo de ejecución de eventos y acciones que tienen una opción de retardo, que ahora son compatibles con los valores de los elementos de datos añadidos en la versión 2.0.4, para convertir correctamente las cadenas en números.

## 9 de marzo de 2021

Versión 2.0.4

* Se ha agregado compatibilidad con elementos de datos en varios campos. La compatibilidad con elementos de datos se ha añadido a los siguientes eventos: Tiempo en la página, Entra en la ventanilla, Pase de ratón y Tiempo de reproducción de medios. Así como las siguientes condiciones: Tiempo en el sitio y Comparación de valor
* Añade compatibilidad con el comportamiento predeterminado para ctrl/cmd + clic y para clic con el botón central del ratón cuando se utiliza Demora del vínculo
* **Se ha marcado la demora del vínculo en el evento de clic como que ya no es compatible.**: puede encontrar más información en el [Blog de recopilación de datos ](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/explainer-link-delay/ba-p/398403)para Adobe Experience Platform.

## 6 de enero de 2021

Versión 1.9.0

* **Nueva acción “Trigger Direct Call”**: la extensión principal ahora incluye un nuevo tipo de acción llamado `Trigger Direct Call`. Esto se puede utilizar cuando se desea activar una regla de llamada directa a través de una acción desde una regla diferente. Esta se asigna directamente al método `_satellite.track()`. Muchas gracias a [Jan Exner](https://twitter.com/jexner) por esta contribución.

## 8 de diciembre de 2020

Versión 1.8.4

* Se ha corregido un error por el cual un usuario no podía borrar ni anular el nonce de una CSP.

## 28 de julio de 2020

Versión 1.8.3

* Se ha corregido un error por el cual el número CSP solo se leía una vez al iniciar la extensión en lugar de recuperarse durante la invocación de acción de código personalizado.

## 13 de julio de 2020

Versión 1.8.2

* Se ha corregido un error en el cual la acción de código personalizado generaba un error en el código HTML que contenía tokens sin un nombre de etiqueta (p. ej. comentarios).

## 10 de julio de 2020

Versión 1.8.1

* Se corrigió un error en el cual las entidades HTML personalizadas dentro de atributos de `script` y `style` etiquetas no se descodificaban correctamente antes de registrarse en la página.
* Se corrigió un error que se producía cuando una acción de código personalizado externo no tenía contenido. La acción de código personalizado externo es la acción que se carga desde un archivo diferente de la biblioteca (esto sucede cuando el evento que activa la regla no es libraryLoaded o pageBottom)

## 6 de julio de 2020

Versión 1.8.0

* **Promesas en Custom Code**: las condiciones de Custom Code y las acciones de JavaScript que no se ejecutan en el ámbito global ahora pueden arrojar Promesas. Puede utilizarlos para que las condiciones y acciones subsiguientes esperen a que se complete un proceso asincrónico en Custom Code antes de pasar al siguiente elemento.
* **Llamadas de retorno en Acciones de Custom Code HTML**: puede lograr lo mismo en las acciones de Custom Code HTML con las llamadas de retorno `onCustomCodeSuccess()` y `onCustomCodeFailure()`.

Consulte la [referencia de Core Extension](./overview.md) en Condiciones > Código personalizado y acciones > Código personalizado para obtener información más detallada.

## 7 de abril de 2020

Versión 1.7.3

* **Aumento de la longitud del campo de texto**: los campos de entrada de texto se cambiaron a una presentación flexible para utilizar mejor el ancho de pantalla del usuario y dejar más espacio para cadenas de texto más largas.

## 1 de noviembre de 2019

Versión 1.7.0

* **Acceso a la variable `event` dentro del elemento de datos de Custom Code**: Ahora puede hacer referencia un evento desde un elemento de datos de Custom Code cuando se ejecuta en el contexto de una regla. El objeto contendrá información útil sobre el evento que activó la regla. Muchas gracias a [Stewart Schilling](https://twitter.com/sdi_stewart) por esta contribución.

## 7 de octubre de 2019

v1.6.2

* **Nuevo tipo de elemento de datos “Constant”**: la extensión principal ahora incluye un nuevo elemento de datos llamado `Constant`. Se puede utilizar cuando necesite almacenar un valor constante al que se hará referencia en varias condiciones, acciones o Custom Code. Muchas gracias a [Jan Exner](https://twitter.com/jexner) por esta contribución.

## 11 de septiembre de 2019

v1.6.1

* **Compatibilidad con el nonce de CSP**: La extensión principal ahora tiene un parámetro de configuración opcional. Puede añadir un elemento de datos que haga referencia a un nonce. En el caso de estar configurados, todos los scripts internos que una etiqueta añade a la página utilizan el nonce que ha configurado. Este cambio admite el uso de una directiva de seguridad de contenido con un nonce para que los scripts de etiquetas se puedan seguir cargando en un entorno CSP. Puede obtener más información sobre el uso de etiquetas con un CSP [aquí](../../../ui/client-side/content-security-policy.md).

## 18 de junio de 2019

v1.5.0

* **Registro de Direct Call**: El registro de Browser para reglas de Direct Call ahora proporciona detalles adicionales cuando se pasa.

## 8 de mayo de 2019

v1.4.3

* **Campos de entrada**: Los campos de entrada son mucho más largos.
* **Custom Event**: Ahora se puede utilizar el tipo de Custom Event con eventos distribuidos fuera de ventana.
* **Corrección de errores**: Se ha corregido un error en el que la condición de Value Comparison no tenía un valor 0.
* **Corrección de errores**: Se ha actualizado el campo exhange\_url, por lo que ahora puede ver el listado de la extensión principal en Adobe Exchange.

## 8 de enero de 2019

v1.4.2

* **Evento Enters Viewport**: Anteriormente, el evento Enters Viewport solo se activaba una vez por página. Este comportamiento se puede configurar para que se active cada vez que el elemento entre en la ventanilla.
* **Evento Custom Event**: Los eventos personalizados ahora pueden contener datos contextuales que pueden utilizarse dentro de condiciones y acciones.
* **Evento Click**: Cuando establece un retraso de vínculo en el evento Click, este se registrará ahora correctamente para descendientes del anclaje y no solo para el anclaje.

## 8 de noviembre de 2018

* **Opción Persist Cohort**: La opción para mantener una cohorte se ha añadido a la condición de Muestreo. Esto causa que se mantenga a un usuario dentro o fuera de la cohorte de muestra entre sesiones. Por ejemplo, si la casilla “persist cohort” está marcada y la condición devuelve el valor “True” la primera vez que se ejecute para un visitante determinado, devolverá ese valor en todas las ejecuciones posteriores de la condición para el mismo visitante. De forma similar, si la casilla “persist cohort” está marcada y la condición devuelve el valor “False” la primera vez que se ejecuta para un visitante determinado, devolverá el mismo valor en todas las ejecuciones posteriores de la condición para el mismo visitante.
* **Corrección de errores**: Se ha corregido un problema por el que una regla con un evento Page Bottom y una acción Custom Code en una página donde se estaban cargando etiquetas síncronas, pero incorrectamente (sin llamada a `_satellite.pageBottom()`) borraba el contenido del sitio web.
* **Corrección de errores**: Se ha corregido un problema en el que Enters Viewpoint no funcionaba si la biblioteca de etiquetas se cargaba de forma asíncrona y terminaba de cargarse después de activarse el evento DOMContentLoaded del explorador.

## 24 de mayo de 2018

* **Funcionalidad**: Se ha agregado una condición de Value Comparison, que compara dos valores utilizando cualquiera de los operadores disponibles. Esto reemplaza la funcionalidad de varias condiciones antiguas que eran demasiado específicas.
* **Funcionalidad**: Se ha añadido una condición de Max Frequency, esta condición le permite especificar el número de veces que la condición debe devolver true en un período de tiempo o en una incidencia de evento. Ejemplos: 5 veces al día, 2 veces por visita.

## 11 de abril de 2018

* **Funcionalidad**: Ahora los Data Elements pueden hacer referencia a otros Data Elements.

## 20 de marzo de 2018

* **Corrección de errores**: Las ventanas de Custom Code arrojaban errores de `document.write` y no se ejecutaban en implementaciones asíncronas
* **Corrección de errores**: Los módulos principales no se incluían en una biblioteca
* **Corrección de errores**: Se produjeron problemas con los valores mínimo y máximo del elemento de datos Random Number

## 10 de enero de 2018

* **Funcionalidad**: Elemento de datos Random Number
* **Funcionalidad**: Elemento de datos Page Info
* **Funcionalidad**: Condición de la fecha
* **Funcionalidad**: Condición de Muestreo
