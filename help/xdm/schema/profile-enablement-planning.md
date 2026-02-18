---
keywords: Experience Platform;perfil;perfil de cliente en tiempo real;esquema;conjunto de datos;planificación;habilitación
solution: Experience Platform
title: Planificación de la activación del perfil del cliente en tiempo real
description: Revise las consideraciones clave que debe evaluar antes de habilitar esquemas y conjuntos de datos para el perfil del cliente en tiempo real.
source-git-commit: da40dfde57b17b6a7387451eec48569174ad544b
workflow-type: tm+mt
source-wordcount: '1820'
ht-degree: 0%

---

# Planificación de la activación del perfil del cliente en tiempo real

Utilice esta página para confirmar que el esquema y el conjunto de datos están listos antes de activarlos para el Perfil del cliente en tiempo real. Complete esta revisión de planificación después de diseñar los campos de esquema, pero antes de habilitar el esquema para el perfil. La habilitación de perfiles aplica cambios de comportamiento permanentes al modelo de datos. No puede invertir la habilitación del esquema y habilitar un conjunto de datos afecta a cómo se procesan sus registros en el Perfil del cliente en tiempo real. Revise esta guía para evitar habilitaciones no deseadas, problemas de calidad de datos o restricciones a largo plazo en el diseño del esquema.

Un perfil de activación determina cómo se vinculan, combinan y activan los datos en Experience Platform. Planning garantiza que la estructura de esquema, la configuración de identidad y el propósito del conjunto de datos sean correctos antes de realizar el cambio. Después de completar esta revisión de planificación, puede continuar habilitando los datos del perfil en la interfaz de usuario de **[!UICONTROL Schema Editor]** o **[!UICONTROL Dataset]**.

## Requisitos previos

Antes de utilizar esta guía de planificación, asegúrese de lo siguiente:

* Se diseñó un esquema con la API **[!UICONTROL Schema Editor]** o Registro de esquemas. Consulte el [tutorial de creación de esquemas](../tutorials/create-schema-ui.md) para empezar.
* Se ha configurado al menos un campo de identidad en el esquema. Revise la [guía de configuración del campo de identidad](../ui/fields/identity.md) para obtener instrucciones.
* Comprensión básica de [Perfil del cliente en tiempo real](../../profile/home.md) y cómo utiliza esquemas para crear vistas unificadas del cliente.
* Permisos adecuados para habilitar esquemas y conjuntos de datos para el perfil. Póngase en contacto con el administrador del sistema si no tiene acceso a las opciones de habilitación de perfiles.

Si no ha completado estos requisitos previos, comience con el [tutorial de creación de esquemas](../tutorials/create-schema-ui.md) antes de continuar con esta guía de planificación.

## Por qué la planificación importa {#why-planning-matters}

La habilitación de perfiles cambia permanentemente la forma en que Experience Platform trata los datos. Los siguientes cambios permanentes se aplican a esquemas y conjuntos de datos.

**Esquemas**: cuando se habilita un esquema para el perfil, no se puede deshabilitar ni eliminar. Tampoco puede quitar ni cambiar el nombre de los campos del esquema después de introducir los datos. Esta permanencia significa que el diseño del esquema debe ser completo y estable antes de habilitar Perfil, ya que no puede revertir la decisión ni simplificar la estructura más adelante.

**Conjuntos de datos**: cuando se habilita un conjunto de datos para el perfil, el perfil del cliente en tiempo real utiliza sus registros para generar y actualizar perfiles. Revise el comportamiento de habilitación del conjunto de datos en la [guía de usuario del conjunto de datos](../../catalog/datasets/enable-for-profile.md). A diferencia de los esquemas, puede deshabilitar o eliminar el conjunto de datos más adelante, pero al hacerlo se eliminan los registros de perfil asociados y puede afectar a los flujos de trabajo de segmentación o activación. Tenga en cuenta el impacto descendente antes de realizar cambios en un conjunto de datos habilitado.

Dado que estos cambios afectan a los procesos descendentes, compruebe que un esquema y sus conjuntos de datos son adecuados para el perfil antes de habilitarlos.

### Explicación del flujo de trabajo de habilitación

Debe habilitar tanto el esquema como los conjuntos de datos que utilizan ese esquema para el perfil. Habilite los recursos en el siguiente orden:

1. **Habilite el esquema para el perfil**: primero, habilite el perfil en el esquema de **[!UICONTROL Schema Editor]**. Esto permite habilitar para el perfil cualquier conjunto de datos que utilice este esquema.
2. **Habilitar conjuntos de datos individuales para el perfil**: una vez habilitado el esquema, habilite el perfil en cada conjunto de datos que deba contribuir a los perfiles de cliente unificados.

No puede habilitar un conjunto de datos para el perfil si su esquema aún no está habilitado. El esquema actúa como un requisito previo para la habilitación del conjunto de datos. Este proceso de dos pasos garantiza que el modelo de datos se valide antes de que el perfil del cliente en tiempo real comience a procesar los registros.

## Cuándo habilitar un esquema o un conjunto de datos para el perfil {#when-to-enable}

Revise los criterios siguientes para confirmar que la habilitación del perfil es adecuada para sus datos.

Habilite el perfil en las siguientes situaciones:

* Los datos contribuyen a un perfil de cliente unificado.
* Los datos son necesarios para los flujos de trabajo de segmentación o activación.
* El esquema incluye campos de identidad que representan una clave de nivel de persona o cliente.
* El conjunto de datos contiene eventos de experiencia o atributos de perfil que deben vincularse entre canales. Revise la clase [XDM ExperienceEvent](../classes/experienceevent.md) para confirmar los requisitos de evento.

## Cuándo no habilitar un esquema o un conjunto de datos para el perfil {#when-not-to-enable}

Evite habilitar el perfil en los siguientes casos:

* El esquema representa los datos de búsqueda o de solo referencia.
* El conjunto de datos contiene datos de prueba, temporales o de no producción.
* Los datos no identifican a una persona o se utilizan únicamente para realizar informes.
* El esquema es experimental o estructuralmente incompleto.

Al habilitar Perfil en estos casos, se pueden crear perfiles innecesarios, aumentar el uso de licencias o introducir restricciones de esquema a largo plazo.

## Consideraciones clave antes de habilitar el perfil {#key-considerations}

Revise las consideraciones de esta sección para asegurarse de que el esquema y el conjunto de datos admiten casos de uso de perfil y administración de datos a largo plazo. Antes de habilitar el perfil, compruebe la estructura de esquema, la configuración de identidad y el propósito del conjunto de datos.

### Preparación del esquema

Revise la estructura de esquema para confirmar que admite los requisitos de perfil. El esquema debe contener los campos necesarios para la segmentación y la activación, al tiempo que excluye los campos que son experimentales o no necesarios a largo plazo. Recuerde que cualquier campo adicional que agregue después de la habilitación debe ser aditivo (consulte [restricciones de inmutabilidad de esquema](#why-planning-matters) para obtener detalles). Esta restricción significa que debe validar cuidadosamente la selección de campos antes de habilitar el perfil. Para obtener más información sobre las actualizaciones permitidas, consulte [reglas de evolución de esquema](./composition.md#evolution).

### Configuración de identidad

La configuración de identidad determina cómo el perfil vincula los registros entre conjuntos de datos. Comience por confirmar que se ha seleccionado una identidad principal válida: este campo debe ser estable, único y rellenarse de forma coherente en todos los registros. Compruebe que las áreas de nombres de identidad estén asignadas correctamente para evitar errores de vinculación. Si utiliza identidades secundarias, confirme que admiten sus casos de uso sin provocar conflictos de perfiles, que pueden producirse cuando diferentes personas comparten el mismo valor de identidad. El perfil del cliente en tiempo real resuelve conflictos mediante la aplicación de políticas de combinación que determinan qué datos tienen prioridad cuando se vinculan registros en conflicto.

### Propósito del conjunto de datos

Habilite un conjunto de datos para Perfil solo cuando contribuya directamente a los atributos de perfil o a los eventos de experiencia utilizados en flujos de trabajo descendentes. Evite habilitar conjuntos de datos que contengan datos de búsqueda o referencia que no se utilicen en la segmentación, datos de prueba o muestra o registros generados por el sistema operativo no destinados a la activación. Estos tipos de datos no contribuyen a los perfiles de cliente unificados y crean una sobrecarga de almacenamiento innecesaria. Si un conjunto de datos no contiene campos de identidad o datos de comportamiento del cliente que admitan la segmentación y la activación, no lo habilite para Perfil.

**Ejemplo**:

Habilita un conjunto de datos &quot;Eventos de compra de clientes&quot; que contiene datos de transacción con ID de cliente. El perfil del cliente en tiempo real utiliza estos eventos para crear cronologías de clientes y habilitar la segmentación basada en el comportamiento de compra.

NO habilita un conjunto de datos de catálogo de productos que solo contiene datos de referencia de SKU sin identificadores de cliente. Al habilitar este tipo de conjunto de datos, se crea una sobrecarga de almacenamiento innecesaria sin contribuir a los perfiles de cliente unificados.

## Lista de comprobación previa a la activación {#pre-enablement-checklist}

Utilice esta lista de comprobación para confirmar la preparación antes de habilitar un esquema o conjunto de datos para el perfil. Complete cada elemento antes de activar el Perfil.

### Comprobaciones a nivel de esquema

Comience por validar que el diseño del esquema es completo y estable. Revise el esquema para confirmar que todos los campos requeridos para el caso de uso están presentes y que no se incluyen campos experimentales o temporales. Consulte las [prácticas recomendadas de diseño de esquemas](./best-practices.md) para asegurarse de que su esquema sigue los patrones recomendados. Obtenga la aprobación de su equipo en la lista de campos final (consulte [restricciones de inmutabilidad de esquemas](#why-planning-matters)).

A continuación, compruebe que la configuración de identidad principal sea correcta. Abra el esquema en **[!UICONTROL Schema Editor]** y busque el campo marcado con el icono de identidad. Confirme que este campo se rellena de forma coherente en los datos de origen y que el área de nombres de identidad es adecuada para su caso de uso. La identidad principal debe ser estable, única y estar presente de forma fiable en todos los registros para garantizar la vinculación adecuada del perfil.

Finalmente, confirme que no necesita cambiar el nombre ni reorganizar la estructura del esquema. Los cambios en la estructura del esquema se limitan únicamente a actualizaciones adicionales (consulte [restricciones de inmutabilidad de esquema](#why-planning-matters)). Cualquier ambigüedad a largo plazo en la denominación o la organización no se puede corregir más adelante, por lo que debe resolver estos problemas antes de la activación.

### Comprobaciones a nivel de conjunto de datos

Para cada conjunto de datos que planea habilitar, comience por confirmar que contiene datos relevantes para el perfil. Revise los registros de muestra para comprobar que contienen datos de cliente o de evento, en lugar de información de referencia u operativa pura. Asegúrese de que los registros incluyan valores de identidad que se vinculen a perfiles de clientes. Los conjuntos de datos sin campos de identidad o datos de comportamiento del cliente no deben habilitarse para Perfil.

Determine si el conjunto de datos debe contribuir a la vinculación de identidad o a la segmentación mediante la comprensión de cómo se relacionan sus valores de identidad con otros conjuntos de datos en su entorno habilitado para perfiles. Considere si los registros de este conjunto de datos deben vincularse con perfiles existentes o crear nuevos fragmentos de perfil. Revise la [documentación de la política de combinación](../../profile/merge-policies/overview.md) para comprender cómo el perfil del cliente en tiempo real vincula los registros entre conjuntos de datos y cómo encaja este conjunto de datos en su estrategia de identidad general.

Antes de habilitar el conjunto de datos, estime el número de valores de identidad únicos que contiene y compruebe que estos valores de identidad representan clientes reales en lugar de cuentas de prueba o identificadores del sistema. Confirme que la activación de este conjunto de datos se ajusta a los derechos de licencia, ya que cada identidad única contribuye a su recuento de público direccionable. La habilitación de perfiles aumenta los costes de almacenamiento y procesamiento, por lo que debe asegurarse de que el conjunto de datos proporcione un valor que justifique esta inversión.

Completar esta lista de comprobación ayuda a evitar problemas que no se pueden revertir después de la activación.

## Habilitación del perfil para el esquema y el conjunto de datos {#enable-profile}

Después de completar la lista de comprobación de preactivación, siga estos pasos para habilitar el perfil. Como se explica en [Explicación del flujo de trabajo de habilitación](#why-planning-matters), debe habilitar el esquema antes de habilitar los conjuntos de datos que usen ese esquema.

### Habilite el esquema para el perfil

Habilite primero el perfil en el esquema:

1. Vaya a **[!UICONTROL Schemas]** en la interfaz de usuario de Experience Platform.
2. Seleccione el esquema de la lista para abrirlo en **[!UICONTROL Schema Editor]**.
3. Seleccione la opción **[!UICONTROL Profile]** en el carril derecho. El panel de propiedades del esquema muestra un cuadro de diálogo de confirmación.
4. Seleccione **[!UICONTROL Enable]** para confirmar. El esquema ahora está habilitado para el perfil.

Para obtener instrucciones detalladas, consulte la [guía de habilitación de esquemas](../ui/resources/schemas.md#profile) en la documentación del Editor de esquemas.

### Habilitar los conjuntos de datos para el perfil

Una vez habilitado el esquema para el perfil, habilite cada conjunto de datos que deba contribuir a los perfiles unificados:

1. Vaya a **[!UICONTROL Datasets]** en la interfaz de usuario de Experience Platform.
2. Seleccione un conjunto de datos de la lista para abrir la página de detalles del conjunto de datos.
3. Seleccione la opción **[!UICONTROL Profile]** en el carril derecho. El panel de propiedades del conjunto de datos se actualiza para mostrar El perfil está habilitado.

Repita este proceso para cada conjunto de datos que deba contribuir al Perfil del cliente en tiempo real. Para obtener instrucciones detalladas y opciones de habilitación de API, consulte la guía del usuario del conjunto de datos a la que se hace referencia en la sección Requisitos previos.

### Por qué importa el pedido

Como se explica en [Explicación del flujo de trabajo de habilitación](#why-planning-matters), debe habilitar el esquema antes de habilitar los conjuntos de datos. Esto garantiza que el perfil del cliente en tiempo real valide la estructura de esquema y admita operaciones de perfil antes de permitir la habilitación de conjuntos de datos, y que todos los conjuntos de datos que utilizan el esquema hereden las definiciones de campo correctas para la segmentación y la vinculación de identidad.

Después de habilitar el esquema y los conjuntos de datos, el Perfil del cliente en tiempo real comienza a procesar registros y a crear perfiles de cliente unificados. Los registros introducidos antes de la habilitación no se incluyen en los perfiles a menos que vuelva a introducir los datos.

## Próximos pasos {#next-steps}

Ha revisado los efectos permanentes de la habilitación de perfiles, ha confirmado que el esquema y los conjuntos de datos están listos y ha validado que la configuración de identidad admite sus casos de uso. Para comprender mejor la estructura del esquema y las relaciones de campo, revise los [conceptos básicos de la composición del esquema](../schema/composition.md), que explican las reglas de evolución del esquema y cómo los campos interactúan dentro del modelo de datos. Si encuentra problemas durante o después de la activación, consulte la [guía de solución de problemas de XDM](../troubleshooting-guide.md) para ver problemas y soluciones comunes. Para obtener más información acerca de cómo afectan las áreas de nombres de identidad a la vinculación y resolución de perfiles, revise la [descripción general de áreas de nombres de identidad](../../identity-service/features/namespaces.md).
