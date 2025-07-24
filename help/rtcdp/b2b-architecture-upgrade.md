---
title: Actualizaciones de arquitectura en Real-Time CDP B2B edition
description: Lea este documento para obtener más información sobre las completas actualizaciones de la arquitectura en Real-Time CDP B2B edition.
badgeB2B: label="B2B edition" type="Informative" url="https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html newtab=true"
hide: true
hidefromtoc: true
source-git-commit: 78444555178773a8305ba27aaaf7998fe279a71d
workflow-type: tm+mt
source-wordcount: '1135'
ht-degree: 0%

---

# Actualizaciones de arquitectura a Real-Time CDP B2B edition

>[!IMPORTANT]
>
>Este documento describe las actualizaciones arquitectónicas de las ediciones B2B y B2P de Real-Time CDP. **No se requiere ninguna acción por su parte** en este momento. Consulte este documento para obtener información sobre cómo las actualizaciones afectarán a las funciones existentes de Adobe Experience Platform. Si tiene alguna pregunta, póngase en contacto con el equipo de cuenta de Adobe.

Adobe ha rediseñado las ediciones B2B y B2P de Real-Time CDP para mejorar la escalabilidad, el rendimiento y la fiabilidad, a la vez que admite casos de uso B2B más avanzados. Para garantizar que todos los clientes se beneficien de estas mejoras, Adobe actualizará todos los clientes B2B y B2P existentes a la nueva arquitectura.

Utilice la arquitectura mejorada para las siguientes ventajas:

* **Escalabilidad de la ingesta de datos**: se ha mejorado la compatibilidad con las relaciones B2B de alta cardinalidad, como las cuentas conectadas a miles de personas.
* **Evaluación de audiencia fiable y eficaz**: Segmentación más rápida y resistente para audiencias B2B complejas.
* **resolución de entidades**: resolución de identidades mejorada para entidades B2B, calidad de datos mejorada y duplicación reducida para permitir una segmentación y agregación más precisas.

## Nuevas funciones

Lea lo siguiente para ver las mejoras clave incluidas en la actualización de la arquitectura.

### Instantáneas de cuenta para miembros de audiencia

Con la nueva arquitectura B2B, los detalles de pertenencia a audiencias ahora se incluyen para entidades de cuenta en exportaciones de instantáneas. Esta función le permite acceder a indicadores de estado de audiencia, marcas de tiempo y abono de nivel de cuenta.

Con esta actualización, ahora puede:

* Habilite a los equipos de marketing y operaciones para validar directamente la pertenencia a audiencias de cuenta.
* Lograr la paridad de características entre su perfil (persona) y los modelos de segmentación de cuenta, lo que garantiza una experiencia coherente entre las entidades.

Lea la documentación sobre [audiencias de cuenta](../segmentation/types/account-audiences.md) para obtener más información.

### Recuentos de audiencias para audiencias que incluyen entidades B2B

Las estimaciones de tamaño de audiencia para audiencias con entidades B2B ahora se calculan con precisión exacta. Estas estimaciones están disponibles durante la vista previa y proporcionan perspectivas más precisas y fiables para las audiencias que implican relaciones B2B complejas.

Con esta actualización, ahora puede:

* Utilice datos de estimaciones precisas del tamaño de la audiencia para mejorar la planificación y la toma de decisiones durante el proceso de creación de audiencias.
* Diseñe con confianza audiencias B2B complejas, con conocimientos de estimación de audiencias más precisa.
* Permiten una planificación de campañas más inteligente, una segmentación más precisa y una mejor asignación de recursos.

Lea la documentación sobre [audiencias de cuenta](../segmentation/types/account-audiences.md) para obtener más información.

### Retrospectiva completa para eventos de nivel de persona en audiencias de cuenta

Las audiencias de cuenta ahora pueden aprovechar el historial completo de eventos de nivel de persona, ampliándose más allá de la ventana retrospectiva de 30 días anterior.

Con esta actualización, ahora puede:

* Cree audiencias más completas basadas en el historial completo de eventos de nivel de persona asociados.
* Habilite definiciones de audiencia más completas y precisas aprovechando los datos de comportamiento a largo plazo.
* Identifique cuentas de alto valor basadas en patrones de participación más profundos a lo largo del tiempo.
* Casos de uso de soporte que requieren perspectivas de acciones históricas, como las que implican ciclos de venta largos o señales de compra demoradas.

Lea la documentación sobre [audiencias de cuenta](../segmentation/types/account-audiences.md) para obtener más información.

## Actualizaciones de funciones existentes

Las siguientes funciones se han actualizado como parte de las actualizaciones arquitectónicas de B2B.

### Actualizaciones de la audiencia de varias entidades con atributos B2B y eventos de experiencia

Como parte de la nueva actualización de la arquitectura, los filtros de Evento de experiencia ya no se pueden usar dentro de una sola audiencia de varias entidades que incluya atributos B2B.

Para lograr la misma lógica de audiencia, utilice el enfoque de segmento a segmento:

1. Crear una audiencia de evento de experiencia: defina la condición de comportamiento por separado. Por ejemplo: &quot;Personas que visitaron la página de precios en los últimos tres días&quot;.
2. Crear una audiencia de varias entidades con atributos B2B: Haga referencia a la audiencia de Experience Event como parte de los criterios de esta audiencia. Por ejemplo: &quot;Personas que son **&#39;Responsables de la toma de decisiones&#39;** de cualquier oportunidad donde la cuenta se encuentra en el sector **&#39;Finanzas&#39;** y miembro de la audiencia de personas que visitaron la página de precios en los últimos tres días.

Una vez completada la actualización, cualquier nueva audiencia de varias entidades con atributos B2B y eventos de experiencia debe crearse con el enfoque de segmento a segmento. Además, debe validar la pertenencia a audiencias para garantizar el comportamiento esperado.

### Resolución de entidades y combinación de prioridad de tiempo en audiencias B2B

Como parte de la actualización de la arquitectura, Adobe ha introducido la resolución de entidades para cuentas y oportunidades, que se ejecuta a diario. Esta mejora permite a Experience Platform identificar y consolidar varios registros que representan la misma entidad real, lo que mejora la coherencia de los datos y permite una segmentación de audiencia más precisa.

Con esta actualización, ahora puede:

* Utilice las API [!DNL Profile Access] para ver los perfiles de combinación más recientes una vez que se hayan completado los trabajos diarios de resolución de entidades.
* Utilice la precisión y coherencia mejoradas de los datos de cuentas y oportunidades para la segmentación, activación y análisis.

Lea la [[!DNL Profile Access] API](../profile/api/entities.md) para obtener más información.

### Compatibilidad con políticas de combinación en audiencias B2B de varias entidades

Las audiencias de varias entidades con atributos B2B ahora admiten una única política de combinación (la política de combinación predeterminada que configure) en lugar de varias políticas de combinación.

Las audiencias que anteriormente dependían de una política de combinación no predeterminada pueden producir resultados diferentes. Para comprender los cambios potenciales en la composición de la audiencia, revise y pruebe cualquiera de sus audiencias que dependa de una política de combinación no predeterminada. Además, supervise los resultados de activación para detectar cualquier cambio en la composición de la audiencia debido al cambio en la política de combinación.

Lea la guía del caso de uso de segmentación [para Real-Time CDP B2B edition](./segmentation/b2b.md) para obtener más información.

### Obsolescencia de la búsqueda y eliminación de entidades B2B en la API [!DNL Profile Access]

Las siguientes funcionalidades de búsqueda para entidades B2B que utilizan la API [!DNL Profile Access] están en desuso:

* Relación cuenta con la persona
* Relación entre oportunidad y la persona
* Campaign
* Miembro de campaña
* Lista de marketing
* Miembros de lista de marketing

Las solicitudes de eliminación para las siguientes entidades B2B que utilizan la API [!DNL Profile Access] están en desuso:

* Cuenta
* Relación cuenta con la persona
* Oportunidad
* Relación entre oportunidad y la persona
* Campaign
* Miembro de campaña
* Lista de marketing
* Miembros de lista de marketing

Lea la [[!DNL Profile Access] API](../profile/api/entities.md) para obtener más información.

### Búsquedas de perfil de cuenta y oportunidad

Ahora puede recuperar esquemas de cuenta y oportunidad como entidades de dimensión de consulta solo después de haber completado el proceso diario de resolución de entidades. Los registros recién introducidos no estarán disponibles para las definiciones de segmento o enriquecimiento de perfil hasta que se complete el siguiente ciclo de resolución de entidad (normalmente cada 24 horas).

Se recomienda revisar cualquier caso de uso que requiera acceso en tiempo real a la cuenta y a los datos de oportunidad. Además, se recomienda planificar el periodo de latencia hasta un máximo de 24 horas al diseñar o actualizar flujos de trabajo que dependan de la segmentación basada en búsquedas o la personalización con entidades de cuenta y de oportunidad.

### Obsolescencia de la creación de audiencias mediante API para entidades B2B

La creación de audiencias mediante entidades B2B a través de API está en desuso. La lista de entidades B2B afectadas incluye:

* Cuenta
* Oportunidad
* Relación cuenta con la persona
* Relación entre oportunidad y la persona
* Campaign
* Miembro de campaña
* Lista de marketing
* Miembro de lista de marketing

Lea la [guía de API de extremo de definiciones de segmento](../segmentation/api/segment-definitions.md) para obtener más información.

### Cambios en las importaciones de audiencias de varias entidades en las herramientas de zonas protegidas

Con las actualizaciones de arquitectura, ya no podrá importar audiencias de varias entidades con atributos B2B y eventos de experiencia si se exportaron antes de la actualización. Estas audiencias no se importarán correctamente y no se pueden convertir automáticamente a la nueva arquitectura. Para solucionar esta limitación, debe volver a exportar estas audiencias y luego importarlas en sus respectivas zonas protegidas de destino con las herramientas de zonas protegidas.

Lea la [guía de herramientas de espacio aislado](../sandboxes/ui/sandbox-tooling.md) para obtener más información.