---
keywords: Experience Platform;inicio;temas populares;conjunto de datos;Conjunto de datos;tiempo de vida;ttl;tiempo de vida;seudónimo;perfiles seudónimos;caducidad de datos;caducidad;
solution: Experience Platform
title: Caducidad de datos de perfil seudónimo
description: Este documento proporciona instrucciones generales para configurar la caducidad de los datos de los perfiles seudónimos en Adobe Experience Platform.
hide: true
hidefromtoc: true
source-git-commit: a6173860adda4bd71c94750e5cce6dd4cbe820c6
workflow-type: tm+mt
source-wordcount: '886'
ht-degree: 0%

---


# Caducidad de datos de perfiles seudónimos [!BADGE Versión limitada]

En Adobe Experience Platform, un perfil se considera para la caducidad de datos seudónimos si cumple las siguientes condiciones:

- Los tipos de identidad del perfil identificado coinciden con lo que el cliente ha especificado como tipo de identidad pseudónimo o desconocido.
   - Por ejemplo, si el tipo de identidad del perfil es `ECID`, `GAID`, o `AAID`. El perfil identificado no tiene ID de ningún otro tipo de identidad. En este ejemplo, un perfil identificado hace lo siguiente **no** tiene una identidad de correo electrónico o CRM.
- No se ha realizado ninguna actividad en un período de tiempo definido por el usuario. La actividad se define mediante la ingesta de eventos de experiencia o mediante actualizaciones iniciadas por el cliente en los atributos de perfil.
   - Por ejemplo, un nuevo evento de vista de página o una actualización de atributo de página se consideran una actividad. Sin embargo, una actualización de abono de segmentos iniciada por un no usuario es **no** se considera una actividad de. Actualmente, para calcular la caducidad de los datos, el seguimiento a nivel de perfil se basa en el momento de la ingesta.

## Acceso {#access}

La caducidad de los datos del perfil seudónimo no se puede configurar mediante la interfaz de usuario o las API de Platform. En su lugar, debe ponerse en contacto con el servicio de asistencia para habilitar esta función. Cuando contacte con el servicio de asistencia, incluya la siguiente información:

- Los tipos de identidad que se deben tener en cuenta para las eliminaciones de perfiles seudónimos.
   - Por ejemplo: `ECID` solo, `AAID` solo, o una combinación de `ECID` y `AAID`.
- Cantidad de tiempo que se debe esperar antes de eliminar un perfil seudónimo. La recomendación predeterminada para los clientes de es de 14 días. Sin embargo, este valor puede diferir según el caso de uso.
- El recuento de perfiles actual comparado con el recuento de perfiles de licencia.

## Preguntas frecuentes {#faq}

La siguiente sección enumera las preguntas más frecuentes sobre la caducidad de los datos de perfiles seudónimos:

### ¿Qué usuarios deben utilizar la caducidad de datos de perfiles seudónimos?

- Si utiliza una fuente de flujo continuo que envíe datos directamente a Platform.
- Si tiene un sitio web que sirve a clientes no autenticados en masa.
- Si tiene recuentos de perfiles excesivos en los conjuntos de datos y ha confirmado que este recuento excesivo de perfiles se debe a un tipo de identidad anónimo basado en cookies.
   - Para determinarlo, debe utilizar el informe de superposición de tipo de identidad. Encontrará más información sobre este informe en la [sección de informe de superposición de identidad](./api/preview-sample-status.md#identity-overlap-report) de la guía de API de estado de muestra de previsualización.

### ¿Cuáles son algunas advertencias que debe tener en cuenta antes de utilizar la caducidad de datos de perfiles seudónimos?

- La caducidad de los datos de perfil seudónimos se ejecutará en el **producción** zona protegida.
- Una vez activada esta función, la eliminación de perfiles es **permanente**. No hay **no** forma de revertir o restaurar los perfiles eliminados.
- Esto es **no** un trabajo de limpieza único. La caducidad de los datos de perfil seudónimos se ejecutará continuamente una vez al día y eliminará los perfiles que coincidan con los datos introducidos por el cliente.
- **Todo** Los perfiles definidos como perfiles seudónimos se verán afectados por la caducidad de los datos de perfil seudónimos. Sí lo tiene **no** no importa si el perfil es solo Evento de experiencia o si solo contiene atributos de perfil.
- Esta limpieza **solamente** se producen en el perfil. El servicio de identidad puede seguir mostrando las identidades eliminadas dentro del gráfico después de la limpieza en casos en los que el perfil tenga dos o más identidades seudónimas asociadas (como `AAID` y `ECID`). Esta discrepancia se solucionará en un futuro próximo.

### ¿En qué se diferencia la caducidad de datos del perfil seudónimo de la caducidad de datos del evento de experiencia existente?

La caducidad de datos de perfil seudónimo y la caducidad de datos de evento de experiencia son funciones complementarias.

#### Granularidad

La caducidad de los datos del Experience Event funciona en una **conjunto de datos** nivel. Como resultado, cada conjunto de datos puede tener una configuración de caducidad de datos diferente.

La caducidad de datos del perfil seudónimo funciona en un **espacio aislado** nivel. Como resultado, la caducidad de los datos afectará a todos los perfiles de la zona protegida.

#### Tipos de identidad

La caducidad de datos de Experience Event elimina los eventos **solamente** se basa en la marca de tiempo del registro de evento. Los tipos de identidad incluidos son **ignorado** para fines de caducidad.

Caducidad de datos de perfil seudónimo **solamente** considera los perfiles que tienen gráficos de identidad que contienen tipos de identidad seleccionados por el cliente, como `ECID`, `AAID`u otros tipos de cookies. Si el perfil contiene **cualquiera** tipo de identidad adicional que se ha **no** en la lista seleccionada por el cliente, el perfil **no** se eliminarán.

#### Elementos eliminados

Caducidad de datos de Experience Event **solamente** elimina eventos y hace **no** quitar datos de clase de perfil. Los datos de clase de perfil solo se eliminan cuando se eliminan todos los datos en **todo** conjuntos de datos y hay **no** registros de clase de perfil restantes para el perfil.

Eliminación de la caducidad de datos de perfil seudónimo **ambos** registros de eventos y perfiles. Como resultado, los datos de clase de perfil también se eliminarán.

### ¿Cómo se puede usar la caducidad de datos de perfil seudónimo junto con la caducidad de datos de Experience Event?

La caducidad de datos de perfil seudónimo y la caducidad de datos de evento de experiencia se pueden utilizar para complementarse.

Usted debe **siempre** configure la caducidad de datos de Experience Event en sus conjuntos de datos, en función de sus necesidades de retención de datos sobre sus clientes conocidos. Una vez configurada la caducidad de datos del Evento de experiencia, puede utilizar la caducidad de datos del Perfil seudónimo para eliminar automáticamente los Perfiles seudónimos. Normalmente, el periodo de caducidad de los datos de los perfiles seudónimos es menor que el periodo de caducidad de los datos de los eventos de experiencia.

En un caso de uso típico, puede establecer la caducidad de los datos de Experience Event en función de los valores de los datos de usuario conocidos y puede establecer la caducidad de los datos del perfil seudónimo en una duración mucho más corta para limitar el impacto de los perfiles seudónimos en el cumplimiento de la licencia de Platform.
