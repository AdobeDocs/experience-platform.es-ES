---
title: Actualizaciones de arquitectura en Real-Time CDP B2B edition
description: Lea este documento para obtener más información sobre las completas actualizaciones de la arquitectura en Real-Time CDP B2B edition.
badgeB2B: label="B2B edition" type="Informative" url="https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html?lang=es#rtcdp-editions" newtab=true
exl-id: d958a947-e195-4dd4-a04c-63ad82829728
source-git-commit: a48196d369cec9e9927d9320475e06457e575691
workflow-type: tm+mt
source-wordcount: '1094'
ht-degree: 1%

---

# Actualizaciones de arquitectura a Real-Time CDP B2B edition

>[!IMPORTANT]
>
>Este documento describe las actualizaciones arquitectónicas de las ediciones B2B y B2P de Real-Time CDP. Las actualizaciones no requerirán acciones por parte de la mayoría de los clientes. Sin embargo, hay audiencias que no se pueden actualizar automáticamente. Adobe trabajará directamente con usted para abordar estos escenarios. Consulte este documento para obtener información sobre cómo las actualizaciones afectarán a las funciones existentes de Adobe Experience Platform. Si tiene alguna pregunta, póngase en contacto con el equipo de cuenta de Adobe.

Adobe ha rediseñado las ediciones B2B y B2P de Real-Time CDP para mejorar la escalabilidad, el rendimiento y la fiabilidad, a la vez que admite casos de uso B2B más avanzados. Para garantizar que todos los clientes se beneficien de estas mejoras, Adobe actualizará todos los clientes B2B y B2P existentes a la nueva arquitectura.

Utilice la arquitectura mejorada para las siguientes ventajas:

* **Escalabilidad de la ingesta de datos**: se ha mejorado la compatibilidad con las relaciones B2B de alta cardinalidad, como las cuentas conectadas a miles de personas.
* **Evaluación de audiencia fiable y eficaz**: Segmentación más rápida y resistente para audiencias B2B complejas.
* **resolución de entidades**: resolución de identidades mejorada para entidades B2B, calidad de datos mejorada y duplicación reducida para permitir una segmentación y agregación más precisas.

## Nuevas funciones

Lea lo siguiente para ver las mejoras clave incluidas en la actualización de la arquitectura.

### Instantáneas de cuenta del abono de público

Con la nueva arquitectura B2B, los detalles de pertenencia a audiencias ahora se incluyen para entidades de cuenta en exportaciones de instantáneas. Esta función le permite acceder a indicadores de estado de audiencia, marcas de tiempo y abono de nivel de cuenta.

Con esta actualización, ahora puede:

* Habilite a los equipos de marketing y operaciones para validar directamente la pertenencia a audiencias de cuenta.
* Lograr la paridad de características entre su perfil (persona) y los modelos de segmentación de cuenta, lo que garantiza una experiencia coherente entre las entidades.

Lea la documentación sobre [audiencias de cuenta](../segmentation/types/account-audiences.md) para obtener más información.

### Recuentos de público para audiencias que incluyen entidades B2B

Las estimaciones de tamaño de audiencia para audiencias con entidades B2B ahora se calculan con precisión exacta. Estas estimaciones están disponibles durante la vista previa y proporcionan perspectivas más precisas y fiables para las audiencias que implican relaciones B2B complejas.

Con esta actualización, ahora puede:

* Utilice datos de estimaciones precisas del tamaño de la audiencia para mejorar la planificación y la toma de decisiones durante el proceso de creación de audiencias.
* Diseñe con confianza audiencias B2B complejas, con conocimientos de estimación de audiencias más precisa.
* Permiten una planificación de campañas más inteligente, una segmentación más precisa y una mejor asignación de recursos.

Lea la documentación sobre [audiencias de cuenta](../segmentation/types/account-audiences.md) para obtener más información.

## Actualizaciones de funciones existentes

Las siguientes funciones se han actualizado como parte de las actualizaciones arquitectónicas de B2B.

### Actualizaciones de la audiencia de varias entidades con atributos B2B y eventos de experiencia

Como parte de la nueva actualización de la arquitectura, los filtros de Evento de experiencia ya no se pueden usar dentro de una sola audiencia de varias entidades que incluya atributos B2B.

Para lograr la misma lógica de audiencia, puede usar el generador de segmentos para [agregar audiencias y referenciar audiencias](../segmentation/ui/segment-builder.md#adding-audiences)

Por ejemplo:

* Crear una audiencia de evento de experiencia
   * Defina la condición de comportamiento por separado. Por ejemplo: &quot;Personas que visitaron la página de precios en los últimos tres días&quot;.
* Cree una audiencia de varias entidades con atributos B2B.
   * Desde aquí puede hacer referencia a la audiencia de Experience Event como parte de los criterios de esta audiencia. Por ejemplo: &quot;Personas que son **&#39;Responsables de la toma de decisiones&#39;** de cualquier oportunidad donde la cuenta se encuentra en el sector **&#39;Finanzas&#39;** y miembro de la audiencia de personas que visitaron la página de precios en los últimos tres días.

Una vez completada la actualización, cualquier nueva audiencia de varias entidades con atributos B2B y eventos de experiencia debe crearse con el enfoque [segmento de segmento](../segmentation/methods/edge-segmentation.md#edge-segmentation-query-types).

>[!TIP]
>
>Un **segmento de segmentos** es cualquier definición de segmento que contiene uno o más segmentos de lote o de borde. **Nota**: si usa un segmento de segmentos, la descalificación del perfil se producirá **cada 24 horas**.

### Resolución de entidades y combinación de prioridad de tiempo en audiencias B2B

Como parte de la actualización de la arquitectura, Adobe presenta la resolución de entidades para Cuentas y oportunidades. La resolución de la entidad se basa en la coincidencia de ID determinística y en los datos más recientes. El trabajo de resolución de entidades se ejecuta a diario durante la segmentación por lotes, antes de evaluar audiencias de varias entidades con atributos B2B.

>[!BEGINSHADEBOX]

#### ¿Cómo funciona la resolución de entidades?

* **Antes**: Si se usó un número del Sistema de numeración universal de datos (DUNS) como identidad adicional y el número DUNS de la cuenta se actualizó en un sistema de origen como CRM, el identificador de la cuenta se vincula a los números DUNS antiguos y nuevos.
* **Después**: Si el número DUNS se usó como identidad adicional y el número DUNS de la cuenta se actualizó en un sistema de origen como un CRM, el ID de cuenta solo se vincula al nuevo número DUNS, reflejando así el estado actual de la cuenta con mayor precisión.

>[!ENDSHADEBOX]

Con esta actualización, ahora puede:

* Utilice las API [!DNL Profile Access] para ver los perfiles de combinación más recientes una vez que se hayan completado los trabajos diarios de resolución de entidades.
* Utilice la precisión y coherencia mejoradas de los datos de cuentas y oportunidades para la segmentación, activación y análisis.

Lea la [[!DNL Profile Access] API](../profile/api/entities.md) para obtener más información.

### Compatibilidad con políticas de combinación en audiencias B2B de varias entidades

Las audiencias de varias entidades con atributos B2B ahora admiten una única política de combinación (la política de combinación predeterminada que configure) en lugar de varias políticas de combinación.

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

### Obsolescencia de la API de trabajos de segmentos

En la nueva arquitectura, el punto final &quot;crear un trabajo de segmentación&quot; y la evaluación de audiencia flexible *no son compatibles.

### Búsquedas de perfil de cuenta y oportunidad

Ahora puede recuperar esquemas de cuenta y oportunidad como entidades de dimensión de consulta solo después de haber completado el proceso diario de resolución de entidades. Los registros recién introducidos no estarán disponibles para las definiciones de segmento o enriquecimiento de perfil hasta que se complete el siguiente ciclo de resolución de entidad (normalmente cada 24 horas).

<!-- ### Deprecation of audience creation via API for B2B entities

Creation of audiences using B2B entities via API is being deprecated. The list of affected B2B entities include:

* Account
* Opportunity
* Account-Person Relation
* Opportunity-Person Relation
* Campaign
* Campaign Member
* Marketing List
* Marketing List Member

Read the [segment definitions endpoint API guide](../segmentation/api/segment-definitions.md) for more information. -->

### Cambios en las importaciones de audiencias de varias entidades en las herramientas de zonas protegidas

Con las actualizaciones de la arquitectura, ya no podrá importar audiencias de varias entidades con atributos B2B y eventos de experiencia si el paquete que incluía estas audiencias se publicó antes de la actualización. Estas audiencias no se importarán correctamente y no se pueden convertir automáticamente a la nueva arquitectura. Para solucionar esta limitación, debe crear un nuevo paquete con las audiencias actualizadas y luego importarlas a sus respectivas zonas protegidas de destino con las herramientas de zonas protegidas.

Los entornos limitados de desarrollo se actualizarán a la nueva arquitectura. Se actualizarán las audiencias que se puedan actualizar automáticamente; las que no se puedan actualizar se deshabilitarán. Las audiencias deshabilitadas deben volver a crearse después de la actualización.

Lea la [guía de herramientas de espacio aislado](../sandboxes/ui/sandbox-tooling.md) para obtener más información.
