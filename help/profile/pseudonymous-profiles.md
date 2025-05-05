---
keywords: Experience Platform;inicio;temas populares;conjunto de datos;Conjunto de datos;tiempo de vida;ttl;tiempo de vida;seudónimo;perfiles seudónimos;caducidad de datos;caducidad;
solution: Experience Platform
title: Caducidad de datos de perfil seudónimo
description: Este documento proporciona instrucciones generales para configurar la caducidad de los datos de los perfiles seudónimos en Adobe Experience Platform.
exl-id: e8d31718-0b50-44b5-a15b-17668a063a9c
source-git-commit: aeb9d6636f0d843bf13d09bcb4c12754e2890046
workflow-type: tm+mt
source-wordcount: '1245'
ht-degree: 4%

---

# Caducidad de los datos de perfiles seudónimos

En Adobe Experience Platform, puede configurar los tiempos de caducidad de los datos para perfiles seudónimos, lo que le permite eliminar automáticamente los datos del almacén de perfiles que ya no son válidos o útiles para sus casos de uso.

## Perfil seudónimo {#pseudonymous-profile}

>[!CONTEXTUALHELP]
>id="platform_profile_pseudonymousprofile"
>title="¿Qué es un perfil seudónimo?"
>abstract="Un perfil seudónimo es un perfil que tiene un espacio de nombres de identidad seudónima o desconocida o un perfil que no ha tenido actividad durante un período de tiempo determinado."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_profile_pseudonymousprofile_dataexpiration"
>title="Caducidad de los datos de perfil seudónimo"
>abstract="La caducidad de los datos del perfil seudónimo representa el número de días que un perfil seudónimo permanecerá en Adobe Experience Platform antes de eliminarse. Este valor debe establecerse como mínimo en 1. Tenga en cuenta que el perfil seudónimo puede tardar hasta tres días en eliminarse."

Un perfil se considera para la caducidad de datos seudónimos si cumple las siguientes condiciones:

- Las áreas de nombres de identidad del perfil vinculado coinciden con lo que el cliente ha especificado como área de nombres de identidad seudónima o desconocida.
   - Por ejemplo, si el área de nombres de identidad del perfil es `ECID`, `GAID` o `AAID`. El perfil identificado no tiene ID de ninguna otra área de nombres de identidad. En este ejemplo, un perfil vinculado **no** tiene una identidad de correo electrónico o CRM.
- No se ha realizado ninguna actividad en un período de tiempo definido por el usuario. La actividad se define mediante la ingesta de eventos de experiencia o mediante actualizaciones iniciadas por el cliente en los atributos de perfil.
   - Por ejemplo, un nuevo evento de vista de página o una actualización de atributo de página se consideran una actividad. Sin embargo, una actualización de pertenencia a audiencia iniciada por usuarios no se considera **no** como una actividad. Actualmente, para calcular la caducidad de los datos, el seguimiento a nivel de perfil se basa en el momento del evento para Eventos de experiencia y el momento de la ingesta para atributos de perfil.

## Acceso {#access}

>[!AVAILABILITY]
>
>Para acceder a esta función, debe tener los siguientes permisos:
>
>- Administrar configuración de perfil
>- Ver perfiles
>
>El permiso **Administrar configuración de perfil** le permite establecer la caducidad de los datos, mientras que el permiso **Ver perfiles** le permite ver la caducidad de los datos.
>
>Encontrará más información sobre los permisos de Experience Platform en la [descripción general del control de acceso](../access-control/home.md#permissions).

Para agregar la caducidad de los datos de perfil seudónimos a tu organización, ve al panel Perfil y selecciona **[!UICONTROL Configuración]**.

![El botón Configuración del panel Perfil está resaltado.](./images/pseudonymous-profiles/profile-settings.png)

Aparece la ventana emergente [!UICONTROL Configuración del perfil]. En esta ventana emergente, puede establecer el número de días para la caducidad de los datos de perfil seudónimos, así como el área de nombres de identidad utilizada para la caducidad de los datos.

Para los entornos limitados de producción, la caducidad predeterminada de los datos de perfil seudónimos es de 14 días, con un mínimo de 1 día y un máximo de 365 días. Para los entornos limitados de desarrollo, la caducidad predeterminada de los datos de perfil seudónimos es de 3 días, con un mínimo de 1 día y un máximo de 365 días.

Seleccione **[!UICONTROL Aplicar]** para guardar la configuración de caducidad de los datos.

![La ventana emergente para agregar la caducidad de datos de perfil seudónimos a los perfiles de su organización. El botón Aplicar está resaltado.](./images/pseudonymous-profiles/profile-settings-data-expiry.png){width="800" zoomable="yes"}

## Preguntas frecuentes {#faq}

La siguiente sección enumera las preguntas más frecuentes sobre la caducidad de los datos de perfiles seudónimos:

### ¿En qué se diferencia la caducidad de datos del perfil seudónimo de la caducidad de datos del evento de experiencia?

+++ Respuesta

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

+++

### ¿Cómo se puede usar la caducidad de datos de perfil seudónimo junto con la caducidad de datos de Experience Event?

+++ Respuesta

La caducidad de datos de perfil seudónimo y la caducidad de datos de evento de experiencia se pueden usar para complementarse entre sí.

**siempre** debe configurar la caducidad de datos del evento de experiencia en sus conjuntos de datos según sus necesidades de conservar datos sobre sus clientes conocidos. Una vez configurada la caducidad de datos del evento de experiencia, puede utilizar la caducidad de datos del perfil seudónimo para eliminar automáticamente los perfiles seudónimos. Normalmente, el periodo de caducidad de los datos de los perfiles seudónimos es inferior al periodo de caducidad de los datos de los eventos de experiencia.

En un caso de uso típico, puede establecer la caducidad de los datos de Experience Event en función de los valores de los datos de usuario conocidos y puede establecer la caducidad de los datos del perfil seudónimo en una duración mucho más corta para limitar el impacto de los perfiles seudónimos en el cumplimiento de la licencia de Experience Platform.

+++

### ¿Para qué tipos de casos de uso debo usar la caducidad de datos de perfiles seudónimos?

+++ Respuesta

- Si utiliza Web SDK para enviar datos directamente a Experience Platform.
- Si tiene un sitio web que sirve a clientes no autenticados en masa.
- Si tiene recuentos de perfiles excesivos en los conjuntos de datos y ha confirmado que este recuento excesivo de perfiles se debe a un área de nombres de identidad anónima basada en cookies.
   - Para determinarlo, debe utilizar el informe de superposición del área de nombres de identidad. Encontrará más información sobre este informe en la sección [informe de superposición de identidades](./api/preview-sample-status.md#identity-overlap-report) de la guía de API de estado de muestra de vista previa.

+++

### ¿Cuáles son algunas advertencias que debe tener en cuenta antes de utilizar la caducidad de datos de perfiles seudónimos?

+++ Respuesta

- La caducidad de los datos de perfil seudónimos se ejecuta en un nivel de **espacio aislado**. Puede elegir tener diferentes configuraciones para los entornos limitados de producción y desarrollo.
- Una vez que haya activado esta función, la eliminación de perfiles es **permanente**. Hay una forma **no** de revertir o restaurar los perfiles eliminados.
- Este es **no** un trabajo de limpieza único. La caducidad de los datos de perfil seudónimos se ejecutará una vez al día y eliminará los perfiles que coincidan con la entrada del cliente.
- **Todos** los perfiles definidos como perfiles seudónimos se verán afectados por la caducidad de los datos del perfil seudónimo. No importa **not** si el perfil es solo de evento de experiencia o si solo contiene atributos de perfil.
- Esta limpieza **solo** se producirá en el perfil. El servicio de identidad puede seguir mostrando las identidades eliminadas dentro del gráfico después de la limpieza en casos en los que el perfil tenga dos o más identidades seudónimas asociadas (como `AAID` y `ECID`). Esta discrepancia se solucionará en un futuro próximo.
- La caducidad de los datos del perfil seudónimo **no** se ejecuta inmediatamente y puede tardar hasta tres días en procesarse.

+++

### ¿Cómo interactúa la caducidad de datos de perfiles seudónimos con las protecciones de los datos del servicio de identidad?

+++ Respuesta

- El sistema de eliminación [&#128279;](../identity-service/guardrails.md) del servicio de identidad , que es el primero en entrar y el primero en salir, podría eliminar los ECID del gráfico de identidad, que están almacenados en el servicio de identidad.
- Si este comportamiento de eliminación provoca que se almacene un perfil solo de ECID en el Perfil del cliente en tiempo real (almacén de perfiles), la caducidad de los datos de perfil seudónimo eliminará este perfil del almacén de perfiles.

+++

## Pasos siguientes

Después de leer esta guía, sabe cómo ver y crear caducidades de datos de perfil seudónimos. Para obtener más información sobre la administración de datos en Experience Platform en su conjunto, lea la [Guía de prácticas recomendadas para la asignación de licencias de administración de datos](../landing/license-usage-and-guardrails/data-management-best-practices.md).

