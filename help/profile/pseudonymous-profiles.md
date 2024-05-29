---
keywords: Experience Platform;inicio;temas populares;conjunto de datos;Conjunto de datos;tiempo de vida;ttl;tiempo de vida;seudónimo;perfiles seudónimos;caducidad de datos;caducidad;
solution: Experience Platform
title: Caducidad de datos de perfil seudónimo
description: Este documento proporciona instrucciones generales para configurar la caducidad de los datos de los perfiles seudónimos en Adobe Experience Platform.
exl-id: e8d31718-0b50-44b5-a15b-17668a063a9c
source-git-commit: e52eb90b64ae9142e714a46017cfd14156c78f8b
workflow-type: tm+mt
source-wordcount: '1004'
ht-degree: 0%

---

# Caducidad de datos de perfiles seudónimos

En Adobe Experience Platform, puede configurar los tiempos de caducidad de los perfiles seudónimos, lo que le permite eliminar automáticamente los datos del almacén de perfiles que ya no son válidos o útiles para sus casos de uso.

## Perfil seudónimo {#pseudonymous-profile}

Un perfil se considera para la caducidad de datos seudónimos si cumple las siguientes condiciones:

- Las áreas de nombres de identidad del perfil vinculado coinciden con lo que el cliente ha especificado como área de nombres de identidad seudónima o desconocida.
   - Por ejemplo, si el área de nombres de identidad del perfil es `ECID`, `GAID`, o `AAID`. El perfil identificado no tiene ID de ninguna otra área de nombres de identidad. En este ejemplo, un perfil identificado hace lo siguiente **no** tiene una identidad de correo electrónico o CRM.
- No se ha realizado ninguna actividad en un período de tiempo definido por el usuario. La actividad se define mediante la ingesta de eventos de experiencia o mediante actualizaciones iniciadas por el cliente en los atributos de perfil.
   - Por ejemplo, un nuevo evento de vista de página o una actualización de atributo de página se consideran una actividad. Sin embargo, se actualiza la pertenencia a la audiencia de los usuarios que no hayan iniciado **no** se considera una actividad de. Actualmente, para calcular la caducidad de los datos, el seguimiento a nivel de perfil se basa en el momento del evento para Eventos de experiencia y el momento de la ingesta para atributos de perfil.

## Acceso {#access}

La caducidad de los datos del perfil seudónimo no se puede configurar mediante la interfaz de usuario o las API de Platform. En su lugar, debe ponerse en contacto con el servicio de asistencia para habilitar esta función. Cuando contacte con el servicio de asistencia, incluya la siguiente información:

- Las áreas de nombres de identidad que se deben tener en cuenta para las eliminaciones de perfiles seudónimos.
   - Por ejemplo: `ECID` solo, `AAID` solo, o una combinación de `ECID` y `AAID`.
- Cantidad de tiempo que se debe esperar antes de eliminar un perfil seudónimo. La recomendación predeterminada para los clientes de es de 14 días. Sin embargo, este valor puede diferir según el caso de uso.

## Preguntas frecuentes {#faq}

La siguiente sección enumera las preguntas más frecuentes sobre la caducidad de los datos de perfiles seudónimos:

### ¿En qué se diferencia la caducidad de datos del perfil seudónimo de la caducidad de datos del evento de experiencia?

La caducidad de datos de perfil seudónimo y la caducidad de datos de evento de experiencia son funciones complementarias.

#### Granularidad

La caducidad de datos del perfil seudónimo funciona en un **espacio aislado** nivel. Como resultado, la caducidad de los datos afectará a todos los perfiles de la zona protegida.

La caducidad de los datos del Experience Event funciona en una **conjunto de datos** nivel. Como resultado, cada conjunto de datos puede tener una configuración de caducidad de datos diferente.

#### Tipos de identidad

Caducidad de datos de perfil seudónimo **solamente** considera los perfiles que tienen gráficos de identidad que contienen áreas de nombres de identidad seleccionadas por el cliente, como `ECID`, `AAID`u otros tipos de cookies. Si el perfil contiene **cualquiera** área de nombres de identidad adicional que se **no** en la lista seleccionada por el cliente, el perfil **no** se eliminarán.

La caducidad de datos de Experience Event elimina los eventos **solamente** se basa en la marca de tiempo del registro de evento. Las áreas de nombres de identidad incluidas son **ignorado** para fines de caducidad.

#### Elementos eliminados

Eliminación de la caducidad de datos de perfil seudónimo **ambos** registros de eventos y perfiles. Como resultado, los datos de clase de perfil también se eliminarán.

Caducidad de datos de Experience Event **solamente** elimina eventos y hace **no** quitar datos de clase de perfil. Los datos de clase de perfil solo se eliminan cuando se eliminan todos los datos en **todo** conjuntos de datos y hay **no** registros de clase de perfil restantes para el perfil.

### ¿Cómo se puede usar la caducidad de datos de perfil seudónimo junto con la caducidad de datos de Experience Event?

La caducidad de datos de perfil seudónimo y la caducidad de datos de evento de experiencia se pueden utilizar para complementarse.

Usted debe **siempre** configure la caducidad de datos de Experience Event en sus conjuntos de datos, en función de sus necesidades de retención de datos sobre sus clientes conocidos. Una vez configurada la caducidad de datos del Evento de experiencia, puede utilizar la caducidad de datos del Perfil seudónimo para eliminar automáticamente los Perfiles seudónimos. Normalmente, el periodo de caducidad de los datos de los perfiles seudónimos es menor que el periodo de caducidad de los datos de los eventos de experiencia.

En un caso de uso típico, puede establecer la caducidad de los datos de Experience Event en función de los valores de los datos de usuario conocidos y puede establecer la caducidad de los datos del perfil seudónimo en una duración mucho más corta para limitar el impacto de los perfiles seudónimos en el cumplimiento de la licencia de Platform.

### ¿Qué usuarios deben utilizar la caducidad de datos de perfiles seudónimos?

- Si utiliza el SDK web para enviar datos directamente a Platform.
- Si tiene un sitio web que sirve a clientes no autenticados en masa.
- Si tiene recuentos de perfiles excesivos en los conjuntos de datos y ha confirmado que este recuento excesivo de perfiles se debe a un área de nombres de identidad anónima basada en cookies.
   - Para determinarlo, debe utilizar el informe de superposición del área de nombres de identidad. Encontrará más información sobre este informe en la [sección de informe de superposición de identidad](./api/preview-sample-status.md#identity-overlap-report) de la guía de API de estado de muestra de previsualización.

### ¿Cuáles son algunas advertencias que debe tener en cuenta antes de utilizar la caducidad de datos de perfiles seudónimos?

- La caducidad de los datos de perfil seudónimos se ejecuta a las **espacio aislado** nivel. Puede elegir tener diferentes configuraciones para los entornos limitados de producción y desarrollo.
- Una vez activada esta función, la eliminación de perfiles es **permanente**. No hay **no** forma de revertir o restaurar los perfiles eliminados.
- Esto es **no** un trabajo de limpieza único. La caducidad de los datos de perfil seudónimos se ejecutará una vez al día y eliminará los perfiles que coincidan con la entrada del cliente.
- **Todo** Los perfiles definidos como perfiles seudónimos se verán afectados por la caducidad de los datos de perfil seudónimos. Sí lo tiene **no** no importa si el perfil es solo Evento de experiencia o si solo contiene atributos de perfil.
- Esta limpieza **solamente** se producen en el perfil. El servicio de identidad puede seguir mostrando las identidades eliminadas dentro del gráfico después de la limpieza en casos en los que el perfil tenga dos o más identidades seudónimas asociadas (como `AAID` y `ECID`). Esta discrepancia se solucionará en un futuro próximo.
- La caducidad de datos de perfil seudónimos sí **no** ejecutar inmediatamente y puede tardar hasta tres días en procesarse.

### ¿Cómo interactúa la caducidad de datos de perfiles seudónimos con las protecciones de los datos del servicio de identidad?

- El servicio de identidad [sistema de eliminación de &quot;primer ingreso y primer envío&quot;](../identity-service/guardrails.md) No se han podido eliminar los ECID del gráfico de identidad, que están almacenados en el servicio de identidad.
- Si este comportamiento de eliminación provoca que se almacene un perfil solo de ECID en el Perfil del cliente en tiempo real (almacén de perfiles), la caducidad de los datos de perfil seudónimo eliminará este perfil del almacén de perfiles.
