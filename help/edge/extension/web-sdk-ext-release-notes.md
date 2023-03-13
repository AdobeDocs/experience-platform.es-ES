---
title: Notas de la versión de Adobe Experience Platform Web SDK Extension
description: Extensión de etiqueta de SDK web de Adobe Experience Platform
exl-id: 91de8c91-023a-45b6-9f67-ac75ee471e50
source-git-commit: 5ec1ede39489ce48fc20739030884ec3811a8426
workflow-type: tm+mt
source-wordcount: '1528'
ht-degree: 40%

---


# Notas de la versión de la extensión Adobe Experience Platform Web SDK

Este documento describe las notas de la versión de la extensión de etiquetas Adobe Experience Platform Web SDK. Para obtener las últimas notas de la versión del propio SDK, consulte la [Notas de la versión de Platform Web SDK](https://experienceleague.adobe.com/docs/experience-platform/edge/release-notes.html).

## Versión 2.15.1: 26 de enero de 2023

* Se ha corregido un problema en el cual los usuarios sin acceso a flujos de datos no podían editar la configuración de la extensión.
* Se ha añadido compatibilidad con las superficies de `sendEvent` acción.

Contiene la versión 2.14.0 del SDK web de Adobe Experience Platform.


## Versión 2.14.1: 13 de octubre de 2022

* Se ha corregido un problema en el cual el SDK web no respeta el ID del servicio de ID de Experience Cloud.

Contiene la versión 2.13.1 de la biblioteca del SDK web de Adobe Experience Platform.

## Versión 2.14.0: 28 de septiembre de 2022

* Añadido nuevo `targetMigrationEnabled` que habilita la migración completa de página a página.
* Se ha añadido una acción de respuesta Aplicar para habilitar implementaciones híbridas de cliente-servidor.
* Se ha añadido la opción de contexto de sugerencias de cliente de agente de usuario de alta entropía.

Contiene la versión 2.13.0 de la biblioteca del SDK web de Adobe Experience Platform.

## Versión 2.13.0: 29 de junio de 2022

* Se ha corregido el orden de las propiedades numéricas en el elemento de datos del objeto XDM, como las eVars.

Contiene la versión 2.12.0 de la biblioteca del SDK web de Adobe Experience Platform.

## Versión 2.12.0: 13 de junio de 2022

* Se ha actualizado el `identityMap` Elemento de datos para rellenar las opciones del área de nombres en función de los entornos limitados definidos por la configuración de extensión.
* Añadido **[!UICONTROL Redirigir con identidad]** acción para permitir el uso compartido de identidades entre dominios.
* Se han añadido vínculos de documentación a `sendEvent` acción.
* Se ha actualizado la biblioteca de IU de React Spectrum.
* Varias mejoras en la interfaz de usuario.

Contiene la versión 2.11.0 de la biblioteca del SDK web de Adobe Experience Platform.

## Versión 2.11.2: 3 de mayo de 2022

Contiene la versión 2.10.1 de la biblioteca del SDK web de Adobe Experience Platform.

## Versión 2.11.1: 22 de abril de 2022

* Se ha corregido el error de comando configure de la versión 2.11.0.

Contiene la versión 2.10.0 de la biblioteca del SDK web de Adobe Experience Platform.

## Versión 2.11.0: 22 de abril de 2022

* Rendimiento mejorado de la IU de Etiquetas.
* Añada selectores de zona protegida a la configuración de extensión de flujos de datos.

Contiene la versión 2.10.0 de la biblioteca del SDK web de Adobe Experience Platform.

## Versión 2.10.0: 10 de marzo de 2022

* Actualice el fragmento de preocultación que está disponible para copiar en la página de configuración para trabajar con el editor de VEC de Adobe Target actualizado.

Contiene la versión 2.9.0 de la biblioteca del SDK web de Adobe Experience Platform.

## Versión 2.9.0: 19 de enero de 2022

Contiene la versión 2.8.0 de la biblioteca del SDK web de Adobe Experience Platform.

## Versión 2.8.0: 26 de octubre de 2021

Contiene la versión 2.7.0 de la biblioteca del SDK web de Adobe Experience Platform.

* Encontrará información adicional de Experience Edge en el evento Enviar evento completado, que incluye `inferences` y `destinations`. El formato de estas propiedades puede cambiar a medida que estas funciones se implementan como parte de una versión beta. Para obtener más información, consulte [Seguimiento de eventos.](../fundamentals/tracking-events.md)

## Versión 2.7.3: 7 de septiembre de 2021

Contiene la versión 2.6.4 de la biblioteca del SDK web de Adobe Experience Platform.

* Ya no aparece una advertencia de obsolescencia para `container.buildInfo.environment.`

## Versión 2.7.0: 16 de agosto de 2021

Contiene la versión 2.6.3 de la biblioteca del SDK web de Adobe Experience Platform.

* Al utilizar el tipo de elemento de datos del mapa de identidad, los identificadores cuyos ID se resuelven en valores que no son cadenas rellenadas ahora se eliminan automáticamente del mapa de identidad.
* Se ha corregido un error que se producía al intentar guardar un elemento de datos con el tipo de elemento de datos Objeto XDM y no se seleccionó ningún esquema.
* Tipografía de interfaz de usuario mejorada.

## Versión 2.6.2: 4 de agosto de 2021

Contiene la versión 2.6.2 de la biblioteca del SDK web de Adobe Experience Platform.

## Versión 2.6.1: 29 de julio de 2021

Contiene la versión 2.6.1 de la biblioteca del SDK web de Adobe Experience Platform.

## Versión 2.6.0: 27 de julio de 2021

Contiene la versión 2.6.0 de la biblioteca del SDK web de Adobe Experience Platform.

* Se han cambiado las etiquetas, las descripciones y los mensajes de error con el término &quot;configuración de Edge&quot; para utilizar el término &quot;secuencia de datos&quot; y alinearlos con la terminología de Adobe Experience Platform más reciente.
* En la vista de configuración de la extensión, se añadió compatibilidad para gestionar grandes cantidades de flujos de datos y entornos de flujos de datos.
* En la vista de elemento de datos del objeto XDM, se ha añadido compatibilidad con la gestión de una gran cantidad de esquemas.
* Se ha agregado un tipo de evento Enviar evento completo, que se puede utilizar para ejecutar una regla después de enviar un evento al servidor y recibir una respuesta. Pronto habrá más documentación disponible.
* El tipo de evento Decisiones recibidas ha quedado obsoleto. Utilice el tipo de evento Enviar evento completado en su lugar.
* La interfaz de usuario y el control de errores se han mejorado en general.

## Versión 2.5.0: 1 de junio de 2021

Contiene la versión 2.5.0 de la biblioteca del SDK web de Adobe Experience Platform.

* Se ha añadido un `data` a la acción Enviar evento. La próxima documentación describirá cómo se puede utilizar en determinados casos.
* En la vista de elemento de datos del objeto XDM, se corrigió un problema en el que se producía un error si el usuario tenía acceso a las zonas protegidas de Adobe Experience Platform, pero no a la zona protegida configurada como predeterminada para la organización.
* En la vista de elemento de datos del objeto XDM, se corrigió un problema en el que un campo de esquema requerido se consideraría no válido aunque el objeto principal no contuviera valores.

## Versión 2.4.0: 9 de marzo de 2021

Contiene la versión 2.4.0 de la biblioteca del SDK web de Adobe Experience Platform.

* Añadido [&quot;descarga de documentos&quot;](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/tracking-events.html?lang=en#using-the-sendbeacon-api) casilla de verificación para Enviar IU de acción de evento.
* Se ha añadido la compatibilidad con `out` opción cuando [configuración del consentimiento predeterminado](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html#default-consent) que descarta todos los eventos hasta que se reciba el consentimiento (el existente `pending` la opción pone en cola eventos y los envía una vez recibido el consentimiento).
* Se ha añadido información de objeto al campo de consentimiento predeterminado.
* Se ha añadido la compatibilidad con [Estándar de consentimiento de Adobe 2.0](https://experienceleague.adobe.com/docs/experience-platform/edge/consent/supporting-consent.html?communicating-consent-preferences-via-the-adobe-standard).
* Ahora aparece un error mejor en la IU del elemento de datos Objeto XDM si el token de acceso del usuario no es válido o está aprovisionado incorrectamente.
* Se ha corregido un error de origen cruzado (que no afecta al funcionamiento de la extensión) que se mostraba en la consola del desarrollador del explorador al ver un elemento de datos de objeto XDM.

## Versión 2.3.0: 4 de noviembre de 2020

Contiene la versión 2.3.0 de la biblioteca del SDK web de Adobe Experience Platform.

* Se añadió la compatibilidad con el uso de un elemento de datos al configurar el consentimiento predeterminado.
* Capacidad añadida para buscar esquemas XDM con el tipo de elemento de datos Objeto XDM.
* Se ha añadido la función de clonación de datos XDM dentro del tipo de acción Enviar evento para garantizar que los cambios posteriores en el objeto de datos XDM no se reflejen en la solicitud.

## Versión 2.2.0: 1 de octubre de 2020

* Cuando los clientes intentaban crear un objeto XDM a partir de esquemas de zona protegida, encontraban problemas de autenticación. La API que llama a Platform ahora conoce los entornos, por lo que los usuarios solo reciben los esquemas a los que tienen acceso para editar.
* Al usar el `identityMap` , las áreas de nombres ahora se rellenan previamente en un menú desplegable, por lo que no tiene que rellenarlas manualmente.
* Se ha modificado la interfaz de usuario del elemento de datos `xdmObject`. En la nueva interfaz de usuario, puede ver qué campos se han rellenado sin tener que introducir cada elemento en el objeto.

## Versión 2.1.1: 26 de agosto de 2020

* Se corrige un problema en el cual las zonas protegidas de Adobe Experience Platform de la vista de objetos XDM no se mostraban correctamente. Si, al utilizar esta versión de la extensión, no se muestra la zona protegida prevista en la lista, el usuario debe consultar al administrador de Adobe Experience Platform para asegurarse de que los permisos de acceso estén configurados correctamente.

## Versión 2.1.0: 5 de agosto de 2020

* Cambio radical: Elimine la acción `syncIdentity` y permita que se pasen esos ID en la acción `sendEvent`. Desactive cualquier regla existente que utilice esta acción antes de actualizar la extensión.
* Actualización a Alloy 2.1.0 ([Notas de la versión](https://experienceleague.adobe.com/docs/experience-platform/edge/release-notes.html))
* Compatibilidad con el estándar de consentimiento IAB 2.0 en la acción `setConsent`.
* Compatibilidad con la anulación del ID del conjunto de datos en la acción `sendEvent`.
* Añada un nuevo elemento de datos del tipo `IdentityMap` que se pueda utilizar para rellenar la entrada de `identityMap` en el elemento de datos de objeto XDM que ahora está activado y en la acción `setConsent`.
* Compatibilidad para pasar un mapa de identidad en la acción `setConsent`.
* Compatibilidad con la selección de una zona protegida de Platform en el elemento de datos del objeto XDM.

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
* Habilitar la depuración mediante `_satellite` ahora habilita la depuración en el SDK web de Adobe Experience Platform.
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
* Añadir la configuración onBeforeEventSend a la extensión de etiquetas
* Agregar la configuración edgeBasePath a la extensión de etiquetas

## Versión 0.0.3: 25 de noviembre de 2019

* Nuevos campos de ID de combinación y Tipo en la acción Enviar evento. El ID de combinación se asigna a `xdm.eventMergeID` en el esquema XDM y Tipo se asigna a `xdm.eventType` en el esquema XDM.

## Versión 0.0.2: 18 de noviembre de 2019

* Versión inicial
