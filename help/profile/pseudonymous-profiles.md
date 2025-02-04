---
keywords: Experience Platform;inicio;temas populares;conjunto de datos;Conjunto de datos;tiempo de vida;ttl;tiempo de vida;seudónimo;perfiles seudónimos;caducidad de datos;caducidad;
solution: Experience Platform
title: Caducidad de datos de perfil seudónimo
description: Este documento proporciona instrucciones generales para configurar la caducidad de los datos de los perfiles seudónimos en Adobe Experience Platform.
exl-id: e8d31718-0b50-44b5-a15b-17668a063a9c
source-git-commit: 208f327d35749c97ac77f337493d8759e8622dcd
workflow-type: tm+mt
source-wordcount: '1039'
ht-degree: 0%

---

# Caducidades de los datos de perfiles seudónimos

En Adobe Experience Platform, puede configurar los tiempos de caducidad de los datos para perfiles seudónimos, lo que le permite eliminar automáticamente los datos del almacén de perfiles que ya no son válidos o útiles para sus casos de uso.

## Perfil seudónimo {#pseudonymous-profile}

>[!CONTEXTUALHELP]
>id="platform_profile_pseudonymousprofile"
>title="¿Qué es un perfil seudónimo?"
>abstract="Un perfil seudónimo es un perfil que tiene un área de nombres de identidad seudónima o desconocida o un perfil que no ha tenido actividad durante un período de tiempo determinado."
>text="Learn more in documentation"

Un perfil se considera para la caducidad de datos seudónimos si cumple las siguientes condiciones:

- Las áreas de nombres de identidad del perfil vinculado coinciden con lo que el cliente ha especificado como área de nombres de identidad seudónima o desconocida.
   - Por ejemplo, si el área de nombres de identidad del perfil es `ECID`, `GAID` o `AAID`. El perfil identificado no tiene ID de ninguna otra área de nombres de identidad. En este ejemplo, un perfil vinculado **no** tiene una identidad de correo electrónico o CRM.
- No se ha realizado ninguna actividad en un período de tiempo definido por el usuario. La actividad se define mediante la ingesta de eventos de experiencia o mediante actualizaciones iniciadas por el cliente en los atributos de perfil.
   - Por ejemplo, un nuevo evento de vista de página o una actualización de atributo de página se consideran una actividad. Sin embargo, una actualización de pertenencia a audiencia iniciada por usuarios no se considera **no** como una actividad. Actualmente, para calcular la caducidad de los datos, el seguimiento a nivel de perfil se basa en el momento del evento para Eventos de experiencia y el momento de la ingesta para atributos de perfil.

## Acceso {#access}

La caducidad de los datos del perfil seudónimo no se puede configurar mediante la interfaz de usuario o las API de Platform. En su lugar, debe ponerse en contacto con el servicio de asistencia para habilitar esta función. Cuando contacte con el servicio de asistencia, incluya la siguiente información:

- Las áreas de nombres de identidad que se deben tener en cuenta para las eliminaciones de perfiles seudónimos.
   - Por ejemplo: solo `ECID`, solo `AAID` o una combinación de `ECID` y `AAID`.
- Cantidad de tiempo que se debe esperar antes de eliminar un perfil seudónimo. La recomendación predeterminada para los clientes de es de 14 días. Sin embargo, este valor puede diferir según el caso de uso.

## Preguntas frecuentes {#faq}

La siguiente sección enumera las preguntas más frecuentes sobre la caducidad de los datos de perfiles seudónimos:

### ¿En qué se diferencia la caducidad de datos del perfil seudónimo de la caducidad de datos del evento de experiencia?

La caducidad de datos de perfil seudónimo y la caducidad de datos de evento de experiencia son funciones complementarias.

#### Granularidad

La caducidad de los datos del perfil seudónimo funciona en un nivel de **espacio aislado**. Como resultado, la caducidad de los datos afectará a todos los perfiles de la zona protegida.

La caducidad de datos del evento de experiencia funciona en un nivel de **conjunto de datos**. Como resultado, cada conjunto de datos puede tener una configuración de caducidad de datos diferente.

#### Tipos de identidad

La caducidad de datos de perfil seudónimos **solamente** considera los perfiles que tienen gráficos de identidad que contienen áreas de nombres de identidad seleccionadas por el cliente, como `ECID`, `AAID` u otros tipos de cookies. Si el perfil contiene **cualquier** área de nombres de identidad adicional que era **no** en la lista seleccionada por el cliente, el perfil **no** se eliminará.

La caducidad de datos de Experience Event elimina los eventos **solamente** en función de la marca de tiempo del registro de evento. Las áreas de nombres de identidad incluidas son **ignoradas** con fines de caducidad.

#### Elementos eliminados

La caducidad de datos de perfil seudónimos elimina **ambos** registros de evento y de perfil. Como resultado, los datos de clase de perfil también se eliminarán.

La caducidad de datos de Experience Event **only** elimina eventos y **not** elimina datos de clase de perfil. Los datos de la clase de perfil solo se eliminan cuando se eliminan todos los datos de **todos** los conjuntos de datos y no quedan **ningún** registro de clase de perfil para el perfil.

### ¿Cómo se puede usar la caducidad de datos de perfil seudónimo junto con la caducidad de datos de Experience Event?

La caducidad de datos de perfil seudónimo y la caducidad de datos de evento de experiencia se pueden usar para complementarse entre sí.

**siempre** debe configurar la caducidad de datos del evento de experiencia en sus conjuntos de datos según sus necesidades de conservar datos sobre sus clientes conocidos. Una vez configurada la caducidad de datos del evento de experiencia, puede utilizar la caducidad de datos del perfil seudónimo para eliminar automáticamente los perfiles seudónimos. Normalmente, el periodo de caducidad de los datos de los perfiles seudónimos es inferior al periodo de caducidad de los datos de los eventos de experiencia.

En un caso de uso típico, puede establecer la caducidad de los datos de Experience Event en función de los valores de los datos de usuario conocidos y puede establecer la caducidad de los datos del perfil seudónimo en una duración mucho más corta para limitar el impacto de los perfiles seudónimos en el cumplimiento de la licencia de Platform.

### ¿Qué usuarios deben utilizar la caducidad de datos de perfiles seudónimos?

- Si utiliza Web SDK para enviar datos directamente a Platform.
- Si tiene un sitio web que sirve a clientes no autenticados en masa.
- Si tiene recuentos de perfiles excesivos en los conjuntos de datos y ha confirmado que este recuento excesivo de perfiles se debe a un área de nombres de identidad anónima basada en cookies.
   - Para determinarlo, debe utilizar el informe de superposición del área de nombres de identidad. Encontrará más información sobre este informe en la sección [informe de superposición de identidades](./api/preview-sample-status.md#identity-overlap-report) de la guía de API de estado de muestra de vista previa.

### ¿Cuáles son algunas advertencias que debe tener en cuenta antes de utilizar la caducidad de datos de perfiles seudónimos?

- La caducidad de los datos de perfil seudónimos se ejecuta en un nivel de **espacio aislado**. Puede elegir tener diferentes configuraciones para los entornos limitados de producción y desarrollo.
- Una vez que haya activado esta función, la eliminación de perfiles es **permanente**. Hay una forma **no** de revertir o restaurar los perfiles eliminados.
- Este es **no** un trabajo de limpieza único. La caducidad de los datos de perfil seudónimos se ejecutará una vez al día y eliminará los perfiles que coincidan con la entrada del cliente.
- **Todos** los perfiles definidos como perfiles seudónimos se verán afectados por la caducidad de los datos del perfil seudónimo. No importa **not** si el perfil es solo de evento de experiencia o si solo contiene atributos de perfil.
- Esta limpieza **solo** se producirá en el perfil. El servicio de identidad puede seguir mostrando las identidades eliminadas dentro del gráfico después de la limpieza en casos en los que el perfil tenga dos o más identidades seudónimas asociadas (como `AAID` y `ECID`). Esta discrepancia se solucionará en un futuro próximo.
- La caducidad de los datos del perfil seudónimo **no** se ejecuta inmediatamente y puede tardar hasta tres días en procesarse.

### ¿Cómo interactúa la caducidad de datos de perfiles seudónimos con las protecciones de los datos del servicio de identidad?

- El sistema de eliminación ](../identity-service/guardrails.md) del servicio de identidad [, que es el primero en entrar y el primero en salir, podría eliminar los ECID del gráfico de identidad, que están almacenados en el servicio de identidad.
- Si este comportamiento de eliminación provoca que se almacene un perfil solo de ECID en el Perfil del cliente en tiempo real (almacén de perfiles), la caducidad de los datos de perfil seudónimo eliminará este perfil del almacén de perfiles.
