---
keywords: Experience Platform;inicio;temas populares
solution: Experience Platform
title: Información general sobre gobernanza, privacidad y seguridad
topic: overview
description: Adobe Experience Platform proporciona varios servicios y herramientas que le permiten controlar con confianza los datos de experiencia recopilados para cumplir con sus prácticas comerciales, obligaciones legales y procesos de desarrollo.
translation-type: tm+mt
source-git-commit: 698639d6c2f7897f0eb4cce2a1f265a0f7bb57c9
workflow-type: tm+mt
source-wordcount: '811'
ht-degree: 0%

---


# Gobernanza, privacidad y seguridad en Adobe Experience Platform

Adobe Experience Platform le permite ingestar, analizar, optimizar y realizar acciones con sus datos para mejorar considerablemente las experiencias de los clientes. Estos datos son vastos, complejos e increíblemente valiosos. Según la naturaleza de sus operaciones de datos, las jurisdicciones legales en las que opera su negocio y las políticas de su organización con respecto al uso de datos, debe controlar y monitorear cuidadosamente la recopilación y el uso de datos de experiencia del cliente para proteger sus intereses comerciales.

Experience Platform proporciona varios servicios y herramientas que le permiten controlar con confianza los datos de experiencia recopilados para cumplir con sus prácticas comerciales, obligaciones legales y procesos de desarrollo. Las secciones que figuran a continuación proporcionan una introducción a cada uno de estos servicios, junto con vínculos a la documentación para obtener más información.

Los servicios se pueden clasificar en tres dominios:

* [Administración de datos](#governance)
* [Privacidad](#privacy)
* [Seguridad](#security)

## Administración de datos {#governance}

La gobernanza de los datos es un concepto esencial que está interrelacionado con todas las capacidades del Experience Platform. La administración de datos representa su capacidad para controlar y comprender sus datos a través de su recorrido a través de la plataforma. Esto implica mantener la calidad de los datos, el linaje de datos, la catalogación de datos y mucho más.

### Administración de datos de Adobe Experience Platform {#data-governance}

Como servicio de plataforma, Adobe Experience Platform Data Governance le permite administrar los datos de los clientes y garantizar el cumplimiento de las normativas, restricciones y políticas aplicables al uso de los datos. Desempeña un papel clave dentro del Experience Platform en varios niveles, incluido el etiquetado del uso de datos, las políticas de uso de datos, la aplicación de políticas y el linaje de datos.

Consulte la [información general sobre la administración de datos](../../data-governance/home.md) para obtener más información.

### Catálogo y datasets {#catalog}

El servicio de catálogo es el sistema de registro para la ubicación y linaje de datos dentro de la plataforma. Aunque todos los datos que se ingestan en el Experience Platform se almacenan en el Data Lake como archivos y directorios, Catalog guarda los metadatos y la descripción de esos archivos y directorios para fines de búsqueda y supervisión.

El catálogo organiza los datos ingestados en conjuntos de datos, con cada conjunto de datos que contiene metadatos que se pueden utilizar para etiquetar y categorizar los datos que contiene.

Consulte la [información general del servicio de catálogo](../../catalog/home.md) para obtener más información sobre el servicio. Para obtener información sobre cómo administrar datasets en Experience Platform, consulte la [información general de datasets](../../catalog/datasets/overview.md).

## Privacidad {#privacy}

La privacidad es un problema crítico para su negocio, los legisladores y sus clientes. Dado que los datos personales recopilados de sus clientes son el núcleo de casi todos los flujos de trabajo de Experience Platform, Platform proporciona servicios para respaldar estas iniciativas.

### Adobe Experience Platform Privacy Service {#privacy-service}

Las regulaciones legales de privacidad, como la Regulación General de Protección de Datos (RGPD) de la Unión Europea y la Ley de Privacidad del Consumidor de California (CCPA), otorgan a los ciudadanos dentro de sus jurisdicciones el derecho de acceder y eliminar los datos personales que recopila y almacena en ellos.

Adobe Experience Platform Privacy Service proporciona una API RESTful y una interfaz de usuario para ayudar a administrar estas solicitudes. Con Privacy Service, puede enviar solicitudes para acceder o eliminar datos de clientes personales o privados de las aplicaciones de Adobe Experience Cloud, lo que facilita el cumplimiento automatizado de las normativas de privacidad legales y de la organización.

Consulte la [información general del Privacy Service](../../privacy-service/home.md) para obtener más información.

### Recopilación de consentimiento {#consent}

Muchas regulaciones legales de privacidad han introducido requisitos para el consentimiento activo y específico cuando se trata de recopilación de datos, personalización y otros casos de uso de mercadotecnia. Para cumplir estos requisitos, Experience Platform le permite capturar la información de consentimiento en perfiles de clientes individuales y utilizar esas preferencias como factor determinante en la forma en que los datos de cada cliente se utilizan en los flujos de trabajo de plataforma descendente.

Para aprender a recopilar y procesar los datos de consentimiento del cliente de acuerdo con el Marco de Transparencia y Consentimiento de IAB (TCF) 2.0, consulte la información general sobre la compatibilidad con [TCF 2.0 de IAB en la plataforma](./consent/iab/overview.md).

<!-- For more information on the consent collection process using the Adobe standard, see the [consent collection overview]. -->

## Seguridad {#security}

La integridad y la seguridad de sus datos son indispensables para su negocio, y este riesgo requiere capacidades de seguridad líderes en la industria. Para cumplir con este desafío, Platform proporciona varias herramientas que ayudan a salvaguardar las operaciones de datos.

### Control de acceso {#access-control}

Experience Platform utiliza el Adobe Admin Console para proporcionar control de acceso basado en roles a diversas funciones de la Plataforma. Esta funcionalidad aprovecha los perfiles del producto en el Admin Console, que vinculan a los usuarios con permisos y entornos limitados.

Consulte la [información general del control de acceso](../../access-control/home.md) para obtener más información.

### Sandboxes {#sandboxes}

Experience Platform está diseñado para enriquecer las aplicaciones de experiencia digital a escala global. Las compañías suelen ejecutar varias aplicaciones de experiencia digital en paralelo y deben encargarse del desarrollo, la prueba y la implementación de estas aplicaciones al mismo tiempo que garantizan el cumplimiento de normas operacionales.

A fin de satisfacer la necesidad de flexibilidad de desarrollo, Experience Platform proporciona entornos limitados que dividen una instancia de plataforma única en entornos virtuales independientes para ayudarle a desarrollar sus aplicaciones de experiencia digital en función de su propio ciclo de vida de desarrollo.

Consulte la [información general de los entornos limitados](../../sandboxes/home.md) para obtener más información.

## Pasos siguientes

Este documento proporciona una visión general de los diversos servicios y herramientas de la Plataforma relacionados con la administración de datos, la privacidad y la seguridad. Consulte la documentación relacionada con esta guía para obtener más información sobre estas funciones.