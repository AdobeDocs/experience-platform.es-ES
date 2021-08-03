---
title: Notas de la versión de la extensión del SDK web de Adobe Experience Platform
description: Extensión de etiquetas de SDK web de Adobe Experience Platform
exl-id: 91de8c91-023a-45b6-9f67-ac75ee471e50
source-git-commit: 7c30df7ea126ec7c7c794b8daaf3d2b813873b98
workflow-type: tm+mt
source-wordcount: '1105'
ht-degree: 53%

---

# Notas de la versión de Adobe Experience Platform Web SDK

Este documento cubre las notas de la versión de la extensión de etiqueta del SDK web de Adobe Experience Platform. Para ver las notas de la última versión del SDK, consulte las [Notas de la versión del SDK web de Platform](https://experienceleague.adobe.com/docs/experience-platform/edge/release-notes.html).

## Versión 2.6.2: 4 de agosto de 2021

Contiene la versión 2.6.2 de la biblioteca del SDK web de Adobe Experience Platform.

## Versión 2.6.1: 29 de julio de 2021

Contiene la versión 2.6.1 de la biblioteca del SDK web de Adobe Experience Platform.

## Versión 2.6.0: 27 de julio de 2021

Contiene la versión 2.6.0 de la biblioteca del SDK web de Adobe Experience Platform.

* Las etiquetas, las descripciones y los mensajes de error que utilizan el término &quot;configuración perimetral&quot; se han cambiado para que el término &quot;conjunto de datos&quot; se ajuste a la terminología más reciente de Adobe Experience Platform.
* En la vista de configuración de la extensión, se agregó compatibilidad para gestionar grandes cantidades de conjuntos de datos y entornos de conjuntos de datos.
* En la vista de elementos de datos de objeto XDM, se agregó compatibilidad para administrar grandes cantidades de esquemas.
* Se ha añadido un tipo de evento Send Event Complete , que se puede utilizar para ejecutar una regla después de enviar un evento al servidor y recibir una respuesta. Próximamente habrá más documentación disponible.
* El tipo de evento Decisiones recibidas está en desuso. En su lugar, utilice el tipo de evento Enviar evento completado .
* La interfaz de usuario y la gestión de errores se han mejorado en general.

## Versión 2.5.0: 1 de junio de 2021

Contiene la versión 2.5.0 de la biblioteca del SDK web de Adobe Experience Platform.

* Se ha agregado un campo `data` a la acción Enviar evento. La siguiente documentación describirá cómo se puede utilizar en determinados casos.
* En la vista de elementos de datos de objeto XDM, se corrigió un problema en el que se generaba un error si el usuario tenía acceso a entornos limitados de Adobe Experience Platform pero no al entorno limitado configurado como predeterminado para la organización.
* En la vista de elementos de datos de objeto XDM, se corrigió un problema en el que un campo de esquema requerido se consideraría no válido aunque el objeto principal no contuviera valores.

## Versión 2.4.0: 9 de marzo de 2021

Contiene la versión 2.4.0 de la biblioteca del SDK web de Adobe Experience Platform.

* Se ha añadido la casilla de verificación [&quot;descarga de documento&quot;](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/tracking-events.html?lang=en#using-the-sendbeacon-api) a la interfaz de usuario de acción Enviar evento .
* Se agregó compatibilidad con una opción `out` al [configurar el consentimiento predeterminado](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html#default-consent), que descarta todos los eventos hasta que se recibe el consentimiento (la opción `pending` existente coloca en cola los eventos y los envía una vez que se recibe el consentimiento).
* Se ha añadido una información sobre herramientas al campo de consentimiento predeterminado.
* Se agregó compatibilidad con el estándar [Consent 2.0 del Adobe](https://experienceleague.adobe.com/docs/experience-platform/edge/consent/supporting-consent.html?communicating-consent-preferences-via-the-adobe-standard).
* Ahora aparece un mejor error en la interfaz de usuario del elemento de datos Objeto XDM si el token de acceso del usuario no es válido o está aprovisionado incorrectamente.
* Se ha corregido un error de origen cruzado (que no afecta al funcionamiento de la extensión) que se mostraba en la consola del desarrollador del explorador al ver un elemento de datos de objeto XDM.

## Versión 2.3.0: 4 de noviembre de 2020

Contiene la versión 2.3.0 de la biblioteca del SDK web de Adobe Experience Platform.

* Se añadió la compatibilidad con el uso de un elemento de datos al configurar el consentimiento predeterminado.
* Capacidad añadida para buscar esquemas XDM con el tipo de elemento de datos Objeto XDM.
* Se ha añadido la función de clonación de datos XDM dentro del tipo de acción Enviar evento para garantizar que los cambios posteriores en el objeto de datos XDM no se reflejen en la solicitud.

## Versión 2.2.0 - 1 de octubre de 2020

* Cuando los clientes intentaban crear un objeto XDM a partir de esquemas de simulación de pruebas, se topaban con problemas de autenticación. La API que llama a Platform ahora conoce los entornos, por lo que los usuarios solo reciben los esquemas a los que tienen acceso para editar.
* Al utilizar el elemento de datos `identityMap`, las Áreas de nombres ahora se rellenan previamente en un menú desplegable, por lo que no es necesario rellenarlas en forma manual.
* Se ha modificado la interfaz de usuario del elemento de datos `xdmObject`. En la nueva interfaz de usuario, puede ver qué campos se han rellenado sin tener que introducir cada elemento en el objeto.

## Versión 2.1.1: 26 de agosto de 2020

* Se corrige un problema en el cual los entornos limitados de Adobe Experience Platform de la vista de objetos XDM no se mostraban correctamente. Si, al utilizar esta versión de la extensión, no se muestra el simulador para pruebas previsto en la lista, el usuario debe consultar al administrador de Adobe Experience Platform para asegurarse de que los permisos de acceso estén configurados correctamente.

## Versión 2.1.0: 5 de agosto de 2020

* Cambio radical: Elimine la acción `syncIdentity` y permita que se pasen esos ID en la acción `sendEvent`. Desactive cualquier regla existente que utilice esta acción antes de actualizar la extensión.
* Actualización a Alloy 2.1.0 ([Notas de la versión](https://experienceleague.adobe.com/docs/experience-platform/edge/release-notes.html))
* Compatibilidad con el estándar de consentimiento IAB 2.0 en la acción `setConsent`.
* Compatibilidad con la anulación del ID del conjunto de datos en la acción `sendEvent`.
* Añada un nuevo elemento de datos del tipo `IdentityMap` que se pueda utilizar para rellenar la entrada de `identityMap` en el elemento de datos de objeto XDM que ahora está activado y en la acción `setConsent`.
* Compatibilidad para pasar un mapa de identidad en la acción `setConsent`.
* Compatibilidad con la selección de un simulador para pruebas de Platform en el elemento de datos de objeto XDM.

## Versión 1.0.0: 26 de mayo de 2020

* Compatibilidad con la selección del entorno desde el servicio de configuración.

## Versión 0.1.2: 4 de mayo de 2020

* Se cambió el nombre `configId` a `edgeConfigId`.
* Se cambió el nombre `viewStart` a `renderDecisions`, que se establece en «false» de forma predeterminada. Si se establece en «true», las ofertas de Personalización se recuperan y se procesan de manera automática.
* Cambios relacionados con `Get Decisions`:
   * Se ha eliminado el comando `getDecisions`.
   * Se ha añadido una opción de `scopes` al comando `sendEvent`. Las decisiones se muestran en la promesa `sendEvent` resuelta.
   * Se ha añadido un ámbito integrado `__view__` que arrojará ofertas de toda la página o vista. (Ofertas de VEC en Target, por ejemplo).
Estas decisiones se arrojan desde el comando `sendEvent` solo si `renderDecisions` se establece en «false».
   * Se ha añadido un evento `Decisions Received` que se activa cuando las decisiones están disponibles.
* Se han combinado varias notificaciones de Personalización en una sola llamada al servidor.
* Se ha corregido un problema en el ID de combinación de eventos que se restablecía cada vez que se hacía referencia al elemento de datos.
* Se ha cambiado el nombre de la acción de `setCustomerIds` a `syncIdentity`.
* Se ha añadido un comando `getIdentity`. Esto se puede consumir mediante Custom Code, solo por ahora.
* Al habilitar la depuración mediante `_satellite` , ahora se habilita la depuración en el SDK web de Adobe Experience Platform.
* Mayor compatibilidad con valores ingresados en el objeto XDM: booleanos, números y decimales.

## Versión 0.0.10: 16 de marzo de 2020

* Combinó los conceptos de inclusión y exclusión en `Consent`, y agregó un nuevo comando `setConsent`.
* Se añadió un nuevo elemento de datos de tipo `XDM Object` que permite la asignación de JavaScript/JSON a XDM.

## Versión 0.0.7: 18 de febrero de 2020

* Se eliminaron las opciones idSyncContainerId, datasetId, schemaId, urlDestinationsEnabled y cookieDestinationsEnabled
* Se agregó la compatibilidad con guiones en el valor de opciones de edgeDomain
* La solicitud realizada durante la migración de ID se envía al extremo demdex para mejorar la identificación entre dominios cuando no se define la cookie demdex
* La solicitud realizada durante la migración de ID siempre espera una respuesta para confirmar que se definió la cookie de identidad
* Al ejecutar un comando no válido, se registrará una lista de nombres de comando válidos en la consola
* Se ha añadido la casilla de verificación para alternar la compatibilidad con cookies de terceros con la extensión de etiquetas. Esto deshabilita las llamadas a demdex.net

## Versión 0.0.5: 20 de diciembre de 2019

* Agregar configuraciones del Rastreador de actividades a la extensión de etiquetas
* Exponer EventType y EventMergeId en el comando de eventos
* Agregar la configuración onBeforeEventSend a la extensión de etiquetas
* Agregar la configuración edgeBasePath a la extensión de etiquetas

## Versión 0.0.3: 25 de noviembre de 2019

* Nuevos campos de ID de combinación y Tipo en la acción Enviar evento. El ID de combinación se asigna a `xdm.eventMergeID` en el esquema XDM y Tipo se asigna a `xdm.eventType` en el esquema XDM.

## Versión 0.0.2: 18 de noviembre de 2019

* Versión inicial
