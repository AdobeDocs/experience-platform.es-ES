---
title: Notas de la versión de la extensión de Adobe Analytics
description: Últimas notas de la versión de la extensión de etiquetas de Adobe Analytics en Adobe Experience Platform.
exl-id: 3c7b4ec0-4b81-4ef4-b15f-6ad102525840
source-git-commit: c783906b20db2b86d58aea7b3a94bde007c0a465
workflow-type: tm+mt
source-wordcount: '1451'
ht-degree: 72%

---

# Notas de la versión de la extensión de Adobe Analytics

A continuación se muestra una lista de notas de la versión de la extensión de etiquetas de Adobe Analytics.

>[!NOTE]
>
>La extensión de etiquetas de Analytics si se actualiza con frecuencia en respuesta a las actualizaciones de la [biblioteca JavaScript de AppMeasurement](https://experienceleague.adobe.com/docs/analytics/implementation/js/overview.html?lang=es). Consulte las [notas de la versión del AppMeasurement](https://experienceleague.adobe.com/docs/analytics/implementation/appmeasurement-updates.html?lang=es) para obtener más información sobre las versiones específicas que se mencionan a continuación.

## 12 de agosto de 2024

**Extensión de Adobe Analytics 1.9.5**

**Características**:

* Se ha actualizado el AppMeasurement [a la versión 2.27.0](https://github.com/adobe/appmeasurement/releases/tag/v2.27.0).

## 4 de marzo de 2024

**Extensión de Adobe Analytics 1.9.4**

**Características**:

* Se ha actualizado el AppMeasurement [a la versión 2.26.0](https://github.com/adobe/appmeasurement/releases/tag/v2.26.0).

## 15 de septiembre de 2023

**Extensión de Adobe Analytics 1.9.3**

**Características**:

* Se ha actualizado el AppMeasurement [a la versión 2.25.0](https://github.com/adobe/appmeasurement/releases/tag/v2.25.0).


## 19 de julio de 2023

**Extensión de Adobe Analytics 1.9.2**

**Características**:

* Se ha actualizado a [AppMeasurement v2.24.0](https://github.com/adobe/appmeasurement/releases/tag/v2.24.0).
* Se ha agregado una configuración opcional (`decodeLinkParameters` valor predeterminado `false`) que descodifica las direcciones URL de los vínculos que incluyen caracteres codificados de doble byte.

**Correcciones de errores**:

* Se ha agregado administración de errores adicional para exploradores con [sugerencias del cliente del agente de usuario](https://experienceleague.adobe.com/docs/analytics/technotes/client-hints.html) de alta entropía defectuosas.
* Se ha cambiado el encabezado Content-Type de [POST](https://developer.mozilla.org/es-ES/docs/Web/HTTP/Methods/POST) de forma predeterminada para que utilice `x-www-form-urlencoded`.

## 23 de septiembre de 2022

**Extensión de Adobe Analytics 1.9.1**

**Características**:

* Se ha actualizado a la versión 2.23.0 del AppMeasurement.
* La extensión ahora puede recopilar [sugerencias del cliente user-agent](https://developer.mozilla.org/en-US/docs/Web/HTTP/Client_hints#user-agent_client_hints) de alta entropía según la versión más reciente de AppMeasurement.

## 28 de febrero de 2022

**Extensión de Adobe Analytics 1.9.0**

**Correcciones de errores**:

* Se han eliminado algunas instrucciones de depuración en la AppMeasurement.

## martes, 29 de noviembre de 2021

**Extensión de Adobe Analytics 1.8.8**

**Correcciones de errores**:

* Se ha actualizado el AppMeasurement a la versión 2.22.3.

## 16 de septiembre de 2021

**Extensión de Adobe Analytics 1.8.7**

**Correcciones de errores**:

* Se ha actualizado el AppMeasurement a la versión 2.22.2.
* Se ha eliminado buildInfo.environment obsoleto

## 24 de agosto de 2021

**Extensión de Adobe Analytics 1.8.6**

**Correcciones de errores**:

* Se ha actualizado el AppMeasurement [a la versión 2.22.1](https://experienceleague.adobe.com/docs/analytics/implementation/appmeasurement-updates.html?lang=es).
* Se ha actualizado linkName de reserva para reflejar la lógica del Activity Map en lugar de utilizar innerHTML.

## 6 de agosto de 2020

**Extensión de Adobe Analytics 1.8.5**

**Correcciones de errores**:

* El nombre incorrecto de la cookie en la configuración del módulo de AAM se estaba configurando cuando este campo se dejó en blanco. Este problema se ha corregido.

**Características**:

* Se ha actualizado [AppMeasurement a la versión 2.22.0](https://experienceleague.adobe.com/docs/analytics/implementation/appmeasurement-updates.html?lang=es).
* La IU pequeña cambia para que la configuración adicional aparezca contraída en un acordeón en lugar de una casilla de verificación.

## 2 de junio de 2020

**Extensión de Adobe Analytics 1.8.4**

**Correcciones de errores**:

* Se ha corregido un error en el cual los eventos del carro de compras (prodView, scAdd, scView, etc.) no se mostraban en el menú desplegable de eventos. Todos estos elementos deberían poder seleccionarse del menú desplegable.

**Características**:

* Ahora puede desactivar el Activity Map en la extensión sin tener que usar código personalizado. El Activity Map se carga como un módulo independiente (como el módulo AAM) y puede desactivarlo si lo desea.
* Se ha limpiado la interfaz de usuario minimizando las variables de jerarquía y otras opciones.
* Se ha agregado un campo para establecer los ID de compra desde la interfaz de usuario de configuración de la extensión.

## 10 de marzo de 2020

**Extensión de Adobe Analytics 1.8.3**

**Correcciones de errores**:

* Se ha corregido un error que afectaba la configuración de regla y que generaba un error al intentar establecer variables si estaba utilizando una biblioteca personalizada y si los grupos de informes no estaban configurados en Analytics.
* Al crear una eVar, había un error que no le mostraba la opción de &quot;duplicar desde&quot; una propiedad o viceversa. Esto se ha corregido para reflejar el comportamiento en versiones anteriores.

**Características**:

* Se ha actualizado [AppMeasurement a la versión 2.20.0](https://experienceleague.adobe.com/docs/analytics/implementation/appmeasurement-updates.html?lang=es)

## 2 de marzo de 2020

**Extensión de Adobe Analytics 1.8.2**

**Correcciones de errores**:

* Se corrigió un problema por el cual una sintaxis incorrecta se usaba para eventos numéricos y moneda serializada

**Características**:

* Se ha actualizado [AppMeasurement a la versión 2.18.0](https://experienceleague.adobe.com/docs/analytics/implementation/appmeasurement-updates.html?lang=es)
* Se ha actualizado la biblioteca DIL del módulo de Audience Manager a 9.4
* Se ha aumentado la longitud de los campos de entrada en la extensión
* Las eVars y props de las configuraciones de extensión y acción ahora muestran el nombre reconocible de Analytics
* Se ha agregado una casilla de verificación en la sección “Cookies” de la configuración de la extensión que permite escribir cookies seguras
* Se agregaron tres nuevas configuraciones al módulo de Audience Manager. Se ha agregado una configuración para habilitar el registro, los destinos de URL y los destinos de cookies

## 13 de noviembre de 2019

**Extensión de Adobe Analytics 1.8.1**

**Correcciones de errores**:

* Se corrigió un error en el cual las eVars y props prémium no se guardaban.

## 1 de noviembre de 2019

**Extensión de Adobe Analytics 1.8.0**

**Correcciones de errores**:

* Se ha corregido un error por el cual un pequeño número de clientes no podía ver las opciones del grupo de informes en la lista desplegable
* Se ha arreglado un error por el que algunas variables se configuraban de forma correcta al usar ECID

**Características**:

* Ordena numéricamente eVars, props y eventos en la vista Extensión
* Se han realizado cambios en el esquema back end para admitir datos de contexto de Magento

## 6 de septiembre de 2019

**Extensión de Adobe Analytics 1.7.8**

**Correcciones de errores**:

* Se corrigió un error en el cual algunos usuarios no veían las opciones de grupos de informes en el menú desplegable
* Se corrigió un error en el cual los eventos no se activaban correctamente

## 5 de septiembre de 2019

**Extensión de Adobe Analytics 1.7.7**

**Características**:

* AppMeasurement actualizada a 2.17
* Módulo de Gestión de público actualizado para admitir DIL 9.3
* Se han actualizado los anchos de campo para darle más espacio

**Correcciones de errores**:

* Se corrigió un error que se producía al configurar la inclusión y la exclusión
* Se corrigió un error en el cual las variables no se configuraban correctamente al usar ECID

## 18 de julio de 2019

**Extensión de Adobe Analytics 1.7.6**

**Características**:

* Actualización de la extensión de Adobe Analytics para admitir DIL 9.2 en Audience Manager

* Se ha actualizado la extensión para admitir [AppMeasurement 2.15.0](https://experienceleague.adobe.com/docs/analytics/implementation/appmeasurement-updates.html#version-2.15.0)
* Se ha eliminado la siguiente casilla de verificación porque ya no es compatible: &quot;No adjunte el IFRAME de publicación de destino al DOM o a los destinos de activación&quot;

## 4 de junio de 2019

**Extensión de Adobe Analytics 1.7.5**

**Características**:

* Actualización de la extensión de Adobe Analytics a [AppMeasurement 2.14.0](https://experienceleague.adobe.com/docs/analytics/implementation/appmeasurement-updates.html#version-2.14.0), que incluye una corrección de un problema conocido de clearVars
* Se ha añadido un vínculo Exchange a la extensión. Se puede acceder a la lista de Exchange haciendo clic en el menú desplegable y seleccionando “Información de extensión”

**Correcciones de errores**:

* Se ha corregido un error en la interfaz de usuario que mostraba la eVar incorrecta eliminada de una lista
* Se ha corregido un error que requería un servidor de seguimiento SSL al intentar agregar varios grupos de informes. Al agregar varios grupos de informes, es necesario un servidor de seguimiento, pero el campo Servidor de seguimiento SSL es opcional.

## 15 de abril de 2019

**Extensión de Adobe Analytics 1.7.4**

**Correcciones de errores**:

* Se volvió a ejecutar la extensión después de que se encontrara un error en AppMeasurement 2.13.0. estaba ocasionando un problema que no enviaba el ECID, por lo que si instaló 1.7.3 recomendamos actualizar a 1.7.4 para evitar este problema. Tenga en cuenta que clearVars se seguirán usando hasta que se publique una versión actualizada de AppMeasurement

## 12 de abril de 2019

**Extensión de Adobe Analytics 1.7.3**

**Correcciones de errores**:

* Se ha actualizado la extensión de Adobe Analytics Extension a AppMeasurement 2.13.0, que incluye una corrección de un problema conocido de clearVars.

## 21 de marzo de 2019

**Extensión de Adobe Analytics 1.7.2**

**Características**:

* Se ha actualizado la extensión de Adobe Analytics a DIL 9.1.
* Se ha actualizado la extensión de Adobe Analytics a AppMeasurement 2.12.
* Se ha actualizado la vista de extensión de Adobe Analytics a React-Spectrum.
* Al configurar los grupos de informes en la página de configuración, ahora verá una lista desplegable de todos los grupos de informes de su empresa para que sea más fácil seleccionar el grupo de informes adecuado.

## 7 de marzo de 2019

**Extensión de Adobe Analytics 1.7.1**

**Correcciones de errores**:

* Se ha vuelto a la versión 1.6 de la extensión porque se encontró un error en la versión 1.7.

## 11 de febrero de 2019

**Extensión de Adobe Analytics 1.6**

**Características**:

* Se ha actualizado la extensión de Adobe Analytics a DIL 9.0, que admitirá la funcionalidad de Inclusión.
* Se ha actualizado la extensión de Adobe Analytics a AppMeasurement 2.11, que admitirá la funcionalidad Opt-in.

**Correcciones de errores**:

* Se ha corregido un conflicto con Prototype JS. La extensión de Analytics ahora admitirá bibliotecas estándar prototype.js.

## 9 de noviembre de 2018

**Extensión de Adobe Analytics 1.5.1**

**Correcciones de errores**:

* Se ha vuelto a la versión 7.0 del módulo DIL para solucionar problemas que provocaban que las señalizaciones de Analytics no se activasen

## 5 de noviembre de 2018

**Extensión de Adobe Analytics 1.5**

**Características**:

* Actualización de la extensión de Adobe Analytics para admitir DIL 8.0 en Audience Manager
* Se separó el campo “Serialize from value” en dos: “Event ID” y “Event Value”. Esto solucionará el problema que asignaba un valor en lugar de serializar un evento
   * Nota: Si utiliza el campo actual para agregar un ID usando una cadena (por ejemplo, Event7=3:abc123) deberá actualizar la entrada para reflejar el ID en el campo “Event ID”

**Correcciones de errores**:

* Se ha corregido un error que no permitía que el código de divisa se rellenara correctamente

## 11 de octubre de 2018

**Extensión de Adobe Analytics 1.4**

**Características**:

* Se migró el nombre de cookie de seguimiento a la configuración de la extensión.

**Correcciones de errores**:

* Se ha corregido un error por el que las variables definidas no se bloqueaban cuando no estaba disponible ningún objeto trackerProperties.

## 5 de junio de 2018

**Extensión de Adobe Analytics 1.3**

**Características**:

* Se ha actualizado la extensión de Adobe Analytics para que admita AppMeasurement 2.9.
* Se ha añadido la funcionalidad “Make tracker globally accessible” en la extensión de Adobe Analytics, lo que permite al rastreador tener ámbitos globales en `windows.s`.

**Correcciones de errores**:

* Se ha corregido un error que provocaba que la vista de lista se restableciera al volver de la vista de detalles
* Se han corregido algunos errores para mejorar la carga de recursos en el selector de revisiones
* Se ha corregido un error por el que varias reglas sobrescribían s.events en la extensión de Adobe Analytics.

## 20 de marzo de 2018

**Extensión de Adobe Analytics 1.2**

**Características**:

* Actualiza AppMeasurement.js a 2.8.0
* Añade compatibilidad con el reenvío del lado del servidor

## 8 de febrero de 2018

**Extensión de Adobe Analytics 1.1**

**Características**:

* AppMeasurement se ha actualizado a la versión 2.6
* El rastreador de Analytics inicializado ahora se expone a través de un módulo compartido en la extensión de etiquetas de Adobe Experience Platform, de modo que otras extensiones puedan incluir código para interactuar con él.

**Correcciones de errores**:

* Se ha corregido un error en la extensión de Adobe Analytics que provocaba que apareciera el mensaje “Error, missing Report Suite ID in AppMeasurement initialization” en la consola del explorador.
