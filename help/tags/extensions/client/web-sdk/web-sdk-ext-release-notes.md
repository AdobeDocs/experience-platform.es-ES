---
title: Notas de la versión de Adobe Experience Platform Web SDK Extension
description: Extensión de etiqueta de SDK web de Adobe Experience Platform
exl-id: 91de8c91-023a-45b6-9f67-ac75ee471e50
source-git-commit: 5086e6419c14356b47963b8445389a0048ad11d7
workflow-type: tm+mt
source-wordcount: '2158'
ht-degree: 30%

---


# Notas de la versión de la extensión Adobe Experience Platform Web SDK

Este documento describe las notas de la versión de la extensión de etiquetas Adobe Experience Platform Web SDK. Para obtener las últimas notas de la versión del SDK, consulte [Notas de la versión de Platform Web SDK](/help/web-sdk/release-notes.md).

## Versión 2.24.0: 5 de junio de 2024

**Correcciones y mejoras**

* Se ha corregido un error que se producía al modificar la configuración de la extensión cuando se definían las anulaciones de configuración.
* Permitir la configuración de valores vacíos para los intervalos de ping de la colección de medios.
* Se ha corregido un error que se producía al modificar una acción de actualización de variable.
* Permitir el restablecimiento del contenedor de sincronización de ID en las anulaciones de configuración.

Contiene la versión 2.20.0 del SDK web de Adobe Experience Platform.

## Versión 2.23.1: 28 de mayo de 2024

**Nuevas funciones**

* Se agregó compatibilidad con el componente [`Streaming Media Collection`](web-sdk-extension-configuration.md#streaming-media) en la configuración de la extensión.
* Se agregó la acción [`Send Media Event`](action-types.md#send-media-event) para la funcionalidad [!DNL Streaming Media Collection].
* Se agregó el elemento de datos [`Media: Quality of Experience`](data-element-types.md#quality-experience) para la funcionalidad [!DNL Streaming Media Collection].

Contiene la versión 2.20.0 del SDK web de Adobe Experience Platform.

**Correcciones y mejoras**

* Se ha corregido un error que se producía al buscar elementos de datos en la acción [Actualizar variable](action-types.md#update-variable).
* Se eliminaron los tipos de eventos [!UICONTROL Media] de los tipos de eventos sugeridos para ser usados en la acción `sendEvent`.

## Versión 2.22.0: 3 de mayo de 2024

**Nuevas funciones**

* Ampliar elemento de datos variable para admitir objetos de datos.
* La acción Actualizar variable ahora admite la modificación de datos de paso a través de Adobe Analytics, Adobe Audience Manager y Adobe Target.

Contiene la versión 2.19.2 del SDK web de Adobe Experience Platform.

## Versión 2.21.4: 10 de enero de 2024

**Correcciones y mejoras**

* Se ha corregido un problema en el cual guardar las anulaciones de configuración sin los 3 entornos establecidos colapsaba la interfaz de usuario de la extensión.
* Se ha corregido un problema en el cual la casilla de verificación de borrar el valor existente de la raíz no se rellenaba al editar una acción de actualización de variable.

Contiene la versión 2.19.2 del SDK web de Adobe Experience Platform.

## Versión 2.21.3: 10 de noviembre de 2023

Contiene la versión 2.19.1 del SDK web de Adobe Experience Platform.

**Correcciones y mejoras**

* Se corrigió un problema en el cual la matriz de propuestas disponible en `Send event complete` eventos siempre estaba vacía.

## Versión 2.21.2: 1 de noviembre de 2023

**Nuevas funciones**

* Se agregó la opción `Request default personalization` para enviar la acción de evento.
* Se añadió compatibilidad con los eventos superior e inferior de página en la acción de evento de envío.
* Se agregó la acción `Apply propositions`.
* Se agregaron la acción `Evaluate rulesets` y el evento `Subscribe ruleset items` para los mensajes en la aplicación.
* Se agregó `Decision context` a la acción de envío de evento.

**Correcciones y mejoras**

* Contiene la versión 2.19.0 del SDK web de Adobe Experience Platform.

## Versión 2.20.3: 8 de agosto de 2023

**Correcciones y mejoras**

* Se ha corregido un problema en el cual los elementos de datos no se podían guardar en el campo de anulación de ID del contenedor de sincronización de ID.

## Versión 2.20.1: 3 de agosto de 2023

**Correcciones y mejoras**

* Se ha mejorado la validación de la configuración de anulación de flujos de datos guardados.

## Versión 2.20.0: 31 de julio de 2023

**Nuevas funciones**

* Se agregó compatibilidad con [anulaciones por comando del ID de secuencia de datos](../../../../datastreams/overrides.md).

**Correcciones y mejoras**

* `edgeConfigId` quedará obsoleto en favor de `datastreamId` en la configuración del SDK.
* Varias mejoras en la experiencia del usuario para la configuración de la secuencia de datos anulan la interfaz de usuario.

## Versión 2.19.0: 21 de junio de 2023

* El elemento de datos **[!UICONTROL Variable]** y las acciones **[!UICONTROL Actualizar variable]** ya están disponibles de forma general.

## Versión 2.18.0: 18 de mayo de 2023

* Contiene la versión 2.17.0 del SDK web de Adobe Experience Platform.

## Versión 2.17.0: 25 de abril de 2023

**Nuevas funciones**

* Contiene la versión 2.16.0 del SDK web de Adobe Experience Platform.
* Se agregó compatibilidad con [anulaciones de configuración de secuencia de datos](/help/datastreams/overrides.md).
* Agregar aviso de obsolescencia a la opción `datasetId` en el comando `sendEvent`.


**Correcciones y mejoras**

* Se ha corregido un problema en el cual el desplazamiento en Safari cerraba el selector de flujo de datos.

## Versión 2.16.1: 14 de abril de 2023

* Se ha corregido un problema con los elementos de datos de objetos y variables XDM en el cual no se podía seleccionar un esquema de una zona protegida no predeterminada.

## Versión 2.16.0: 30 de marzo de 2023

**Nuevas funciones**

* (Beta) Se ha agregado la acción **[!UICONTROL Actualizar variable]** y el elemento de datos **[!UICONTROL Variable]**.
* Se agregó la configuración para la función de devolución de llamada [`onBeforeLinkClickSend`](/help/web-sdk/commands/configure/onbeforelinkclicksend.md).

**Correcciones y mejoras**

* Se ha corregido un problema que hacía que no funcionara hacer clic en elementos dentro de una etiqueta delimitadora cuando se usaba la acción **[!UICONTROL Redirigir con identidad]**.
* Se ha corregido un problema en el cual los elementos de datos de objeto XDM no funcionaban cuando solo había un esquema presente.
* Contiene la versión 2.15.0 del SDK web de Adobe Experience Platform.


## Versión 2.15.1: 26 de enero de 2023

* Se ha corregido un problema en el cual los usuarios sin acceso a flujos de datos no podían editar la configuración de la extensión.
* Se agregó compatibilidad con las superficies en la acción `sendEvent`.

Contiene la versión 2.14.0 del SDK web de Adobe Experience Platform.


## Versión 2.14.1: 13 de octubre de 2022

* Se ha corregido un problema en el cual el SDK web no respeta el ID del servicio de ID de Experience Cloud.

Contiene la versión 2.13.1 de la biblioteca del SDK web de Adobe Experience Platform.

## Versión 2.14.0: 28 de septiembre de 2022

* Se agregó la nueva configuración `targetMigrationEnabled` que habilita la migración página por página completa.
* Se ha añadido una acción de respuesta Aplicar para habilitar implementaciones híbridas de cliente-servidor.
* Se ha añadido la opción de contexto de sugerencias de cliente de agente de usuario de alta entropía.

Contiene la versión 2.13.0 de la biblioteca del SDK web de Adobe Experience Platform.

## Versión 2.13.0: 29 de junio de 2022

* Se ha corregido el orden de las propiedades numéricas en el elemento de datos del objeto XDM, como las eVars.

Contiene la versión 2.12.0 de la biblioteca del SDK web de Adobe Experience Platform.

## Versión 2.12.0: 13 de junio de 2022

* Se ha actualizado el elemento de datos `identityMap` para rellenar las opciones del área de nombres en función de los entornos limitados definidos por la configuración de la extensión.
* Se agregó la acción **[!UICONTROL Redireccionar con identidad]** para permitir el uso compartido de identidades entre dominios.
* Se agregaron vínculos de documentación a la acción `sendEvent`.
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

* Encontrará información adicional del Edge Network en el evento Enviar evento completado, incluidos `inferences` y `destinations`. El formato de estas propiedades puede cambiar a medida que estas funciones se implementan como parte de una Beta.

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

* Se agregó el campo `data` a la acción Enviar evento. La próxima documentación describirá cómo se puede utilizar en determinados casos.
* En la vista de elemento de datos del objeto XDM, se corrigió un problema en el que se producía un error si el usuario tenía acceso a las zonas protegidas de Adobe Experience Platform, pero no a la zona protegida configurada como predeterminada para la organización.
* En la vista de elemento de datos del objeto XDM, se corrigió un problema en el que un campo de esquema requerido se consideraría no válido aunque el objeto principal no contuviera valores.

## Versión 2.4.0: 9 de marzo de 2021

Contiene la versión 2.4.0 de la biblioteca del SDK web de Adobe Experience Platform.

* Se agregó la casilla de verificación [&quot;Descarga de documento&quot;](/help/web-sdk/commands/sendevent/documentunloading.md) a la interfaz de usuario de acción Enviar evento.
* Se agregó compatibilidad con la opción `out` al [configurar el consentimiento predeterminado](/help/web-sdk/commands/configure/defaultconsent.md), que anula todos los eventos hasta que se reciba el consentimiento (la opción `pending` existente pone en cola los eventos y los envía una vez que se recibe el consentimiento).
* Se ha añadido información de objeto al campo de consentimiento predeterminado.
* Se agregó compatibilidad con el estándar Consentimiento de Adobe 2.0 al usar el comando [`setConsent`](/help/web-sdk/commands/setconsent.md).
* Ahora aparece un error mejor en la IU del elemento de datos Objeto XDM si el token de acceso del usuario no es válido o está aprovisionado incorrectamente.
* Se ha corregido un error de origen cruzado (que no afecta al funcionamiento de la extensión) que se mostraba en la consola del desarrollador del explorador al ver un elemento de datos de objeto XDM.

## Versión 2.3.0: 4 de noviembre de 2020

Contiene la versión 2.3.0 de la biblioteca del SDK web de Adobe Experience Platform.

* Se añadió la compatibilidad con el uso de un elemento de datos al configurar el consentimiento predeterminado.
* Capacidad añadida para buscar esquemas XDM con el tipo de elemento de datos Objeto XDM.
* Se ha añadido la función de clonación de datos XDM dentro del tipo de acción Enviar evento para garantizar que los cambios posteriores en el objeto de datos XDM no se reflejen en la solicitud.

## Versión 2.2.0: 1 de octubre de 2020

* Cuando los clientes intentaban crear un objeto XDM a partir de esquemas de zona protegida, encontraban problemas de autenticación. La API que llama a Platform ahora conoce los entornos, por lo que los usuarios solo reciben los esquemas a los que tienen acceso para editar.
* Al utilizar el elemento de datos `identityMap`, las áreas de nombres ahora se rellenan previamente en un menú desplegable, por lo que no es necesario rellenarlas manualmente.
* Se ha modificado la interfaz de usuario del elemento de datos `xdmObject`. En la nueva interfaz de usuario, puede ver qué campos se han rellenado sin tener que introducir cada elemento en el objeto.

## Versión 2.1.1: 26 de agosto de 2020

* Se corrige un problema en el cual las zonas protegidas de Adobe Experience Platform de la vista de objetos XDM no se mostraban correctamente. Si, al utilizar esta versión de la extensión, no se muestra la zona protegida prevista en la lista, el usuario debe consultar al administrador de Adobe Experience Platform para asegurarse de que los permisos de acceso estén configurados correctamente.

## Versión 2.1.0: 5 de agosto de 2020

* Cambio radical: Elimine la acción `syncIdentity` y permita que se pasen esos ID en la acción `sendEvent`. Desactive cualquier regla existente que utilice esta acción antes de actualizar la extensión.
* Actualización a Alloy 2.1.0 ([Notas de la versión](/help/web-sdk/release-notes.md))
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
