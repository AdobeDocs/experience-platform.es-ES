---
keywords: Experience Platform;inicio;temas populares;conjunto de datos;conjunto de datos;tiempo de vida;ttl;tiempo de vida;seudónimo;perfiles seudónimos;caducidad de datos;caducidad;
solution: Experience Platform
title: Pseudónimo Caducidad de datos de perfil
description: Este documento proporciona una guía general sobre la configuración de la caducidad de los datos para los perfiles seudónimos dentro de Adobe Experience Platform.
hide: true
hidefromtoc: true
source-git-commit: 6ba219162f6fde37d8bd258c43ed1bdbbbcdf569
workflow-type: tm+mt
source-wordcount: '875'
ht-degree: 0%

---


# Caducidad de datos de perfiles seudónimos [!BADGE Versión limitada]

En Adobe Experience Platform, un perfil se considera para la caducidad de datos seudónimos si cumple las siguientes condiciones:

- Las áreas de nombres de identidad del perfil enlazado coinciden con lo que el cliente ha especificado como un área de nombres de identidad seudónima o desconocida.
   - Por ejemplo, si el área de nombres de identidad del perfil es `ECID`, `GAID`o `AAID`. El perfil identificado no tiene ID de ningún otro espacio de nombres de identidad. En este ejemplo, un perfil identificado sí **not** tienen una identidad de correo electrónico o CRM.
- No se ha producido ninguna actividad en una cantidad de tiempo definida por el usuario. La actividad se define mediante cualquier evento de experiencia que se ingrese o actualizaciones iniciadas por el cliente de los atributos de perfil.
   - Por ejemplo, un nuevo evento de vista de página o una actualización de atributo de página se consideran una actividad. Sin embargo, una actualización de pertenencia a segmentos no iniciada por el usuario es **not** se considera una actividad. Actualmente, para calcular la caducidad de los datos, el seguimiento a nivel de perfil se basa en el momento de la ingesta.

## Acceso {#access}

La caducidad de los datos del perfil pseudoanónima no se puede configurar a través de la interfaz de usuario de Platform o las API. En su lugar, debe ponerse en contacto con el servicio de asistencia técnica para habilitar esta función. Al ponerse en contacto con el servicio de asistencia técnica, incluya la siguiente información:

- Los espacios de nombres de identidad que se deben tener en cuenta para las eliminaciones de perfiles seudónimos.
   - Por ejemplo: `ECID` solo, `AAID` solo, o una combinación de `ECID` y `AAID`.
- Cantidad de tiempo de espera antes de eliminar un perfil seudónomo. La recomendación predeterminada para los clientes es de 14 días. Sin embargo, este valor puede variar en función del caso de uso.

## Preguntas frecuentes {#faq}

La siguiente sección enumera las preguntas más frecuentes sobre la caducidad de datos de perfiles seudónimos:

### ¿Qué usuarios deberían utilizar la caducidad de datos de perfiles seudónimos?

- Si utiliza el SDK web para enviar datos directamente a Platform.
- Si tiene un sitio web que sirve a clientes no autenticados en masa.
- Si tiene recuentos de perfiles excesivos en sus conjuntos de datos y ha confirmado que este recuento excesivo de perfiles se debe a un espacio de nombres de identidad basado en cookies anónimas.
   - Para determinarlo, debe utilizar el informe de superposición de área de nombres de identidad. Puede encontrar más información sobre este informe en la sección [sección de informe de superposición de identidad](./api/preview-sample-status.md#identity-overlap-report) de la guía de API de vista previa del estado de muestra.

### ¿Cuáles son algunas advertencias que debe tener en cuenta antes de utilizar la caducidad de datos de perfiles seudónimos?

- La caducidad de los datos de perfil pseudoanónimos se ejecutará en la variable **producción** simulador de pruebas.
- Una vez activada esta función, la eliminación de perfiles se realiza **permanente**. Hay **no** forma de restaurar o revertir los perfiles eliminados.
- Esto es **not** un trabajo de limpieza de una sola vez. La caducidad de los datos de perfil pseudonimous se ejecutará continuamente una vez al día y eliminará los perfiles que coincidan con la entrada del cliente.
- **Todo** los perfiles definidos como perfiles seudónimos se verán afectados por la caducidad de los datos del perfil seudónimos. Sí **not** importa si el perfil es solo Evento de experiencia o si solo contiene atributos de perfil.
- Esta limpieza **only** en Perfil. El servicio de identidad puede seguir mostrando las identidades eliminadas dentro del gráfico después de la limpieza en los casos en que el perfil tenga dos o más identidades seudónimas asociadas (como `AAID` y `ECID`). Esta discrepancia se solucionará en un futuro próximo.

### ¿En qué se diferencia la caducidad de los datos del perfil seudónimo de la caducidad de los datos del evento de experiencia existente?

La caducidad de los datos del perfil y la caducidad de los datos del evento de experiencia son características complementarias.

#### Granularidad

La caducidad de datos de Evento de experiencia funciona en un evento **conjunto de datos** nivel. Como resultado, cada conjunto de datos puede tener una configuración de caducidad de datos diferente.

La caducidad de datos de perfil pseudoanónima funciona en un **entorno limitado** nivel. Como resultado, la caducidad de los datos afectará a todos los perfiles del simulador para pruebas.

#### Tipos de identidad

La caducidad de los datos del evento de experiencia elimina eventos **only** en función de la marca de tiempo del registro de evento. Las áreas de nombres de identidad incluidas son **ignorado** para fines de caducidad.

Pseudónimo Caducidad de datos de perfil **only** considera perfiles que tienen gráficos de identidad que contienen áreas de nombres de identidad seleccionadas por el cliente, como `ECID`, `AAID`, u otros tipos de cookies. Si el perfil contiene **any** área de nombres de identidad adicional que era **not** en la lista seleccionada del cliente, el perfil **not** se eliminará.

#### Elementos eliminados

Caducidad de datos de Evento de experiencia **only** elimina eventos y hace **not** quitar datos de clase de perfil. Los datos de la clase de perfil solo se eliminan cuando se eliminan todos los datos de **all** conjuntos de datos y hay **no** registros de clase de perfil restantes para el perfil.

La caducidad de datos de perfil pseudonímica elimina **both** registros de evento y perfil. Como resultado, también se eliminarán los datos de la clase de perfil.

### ¿Cómo se puede utilizar la caducidad de datos de perfil seudónimos junto con la caducidad de datos de eventos de experiencia?

La caducidad de los datos del perfil y la caducidad de los datos del evento de experiencia pueden utilizarse para complementarse.

Debería **always** configure la caducidad de los datos de Experience Event en sus conjuntos de datos, según sus necesidades de retención de datos sobre sus clientes conocidos. Una vez configurada la caducidad de los datos de los eventos de experiencia, puede utilizar la caducidad de los datos de perfil seudónimos para eliminar automáticamente los perfiles seudónimos. Normalmente, el periodo de caducidad de los datos para los perfiles seudónimos es inferior al periodo de caducidad de los eventos de experiencia.

En un caso de uso típico, puede configurar la caducidad de los datos de los eventos de experiencia en función de los valores de los datos de usuario conocidos y puede establecer la caducidad de los datos de perfil seudónimos en una duración mucho más corta para limitar el impacto de los perfiles seudónimos en el cumplimiento de las licencias de Platform.
