---
keywords: Experience Platform;inicio;temas populares
solution: Experience Platform
title: Información general sobre administración, privacidad y seguridad
description: Adobe Experience Platform proporciona varios servicios y herramientas que le permiten controlar con seguridad los datos de experiencia recopilados para cumplir con las prácticas comerciales, las obligaciones legales y el proceso de desarrollo.
exl-id: 1ab5a436-c5dd-4e7a-aba1-549f0613f224
source-git-commit: 5a14eb5938236fa7186d1a27f28cee15fe6558f6
workflow-type: tm+mt
source-wordcount: '855'
ht-degree: 2%

---

# Gobernanza, privacidad y seguridad en Adobe Experience Platform

Adobe Experience Platform le permite introducir, analizar, optimizar y actuar sobre sus datos para mejorar en gran medida las experiencias de los clientes. Estos datos son vastos, complejos e increíblemente valiosos. Según la naturaleza de las operaciones de datos, las jurisdicciones legales en las que opera su empresa y las políticas de su organización con respecto al uso de datos, debe controlar y supervisar cuidadosamente la recopilación y el uso de los datos de experiencia del cliente para proteger los intereses comerciales.

Experience Platform proporciona varios servicios y herramientas que le permiten controlar con seguridad los datos de experiencia recopilados para cumplir con las prácticas comerciales, las obligaciones legales y los procesos de desarrollo. Las secciones siguientes proporcionan una introducción a cada uno de estos servicios, junto con vínculos a documentación para obtener más información.

Los servicios se pueden clasificar en tres dominios:

* [Gobernanza de datos](#governance)
* [Privacidad](#privacy)
* [Seguridad](#security)

## Gobernanza de datos {#governance}

La gobernanza de datos es un concepto esencial que se entrelaza con todas las capacidades de Experience Platform. La gobernanza de datos representa su capacidad para controlar y comprender los datos a lo largo de su recorrido a través de Platform. Esto implica mantener la calidad de los datos, el linaje, la catalogación y mucho más.

### Gobernanza de datos de Adobe Experience Platform {#data-governance}

Como servicio de Platform, Adobe Experience Platform Data Governance le permite administrar los datos de los clientes y garantizar el cumplimiento de las regulaciones, restricciones y políticas aplicables al uso de los datos. Desempeña un papel clave dentro del Experience Platform en varios niveles, incluido el etiquetado del uso de datos, las políticas de uso de datos, la aplicación de políticas y el linaje de datos.

Consulte la [Resumen de gobernanza de datos](../../data-governance/home.md) para obtener más información.

### Catálogo y conjuntos de datos {#catalog}

El servicio de catálogo es el sistema de registro para la ubicación y el linaje de datos dentro de Platform. Mientras que todos los datos que se incorporan al Experience Platform se almacenan en el lago de datos como archivos y directorios, el catálogo contiene los metadatos y la descripción de esos archivos y directorios para fines de búsqueda y monitorización.

El catálogo organiza los datos ingeridos en conjuntos de datos, y cada conjunto de datos contiene metadatos que se pueden utilizar para etiquetar y categorizar los datos que contiene.

Consulte la [Resumen del servicio de catálogo](../../catalog/home.md) para obtener más información sobre el servicio. Para obtener información sobre cómo administrar conjuntos de datos en Experience Platform, consulte la [información general sobre conjuntos de datos](../../catalog/datasets/overview.md).

## Privacidad {#privacy}

La privacidad es un tema crítico para su empresa, legisladores y clientes. Dado que los datos personales recopilados de sus clientes son el núcleo de casi todos los flujos de trabajo de los Experience Platform, Platform proporciona servicios para apoyar estas iniciativas.

### Adobe Experience Platform Privacy Service {#privacy-service}

Las regulaciones legales de privacidad, como el Reglamento General de Protección de Datos (RGPD) de la Unión Europea y la Ley de Privacidad del Consumidor de California (CCPA), otorgan a los ciudadanos de sus jurisdicciones el derecho de acceder y eliminar los datos personales que recopile y almacene de ellos.

Adobe Experience Platform Privacy Service proporciona una API de RESTful y una interfaz de usuario para administrar estas solicitudes. Con Privacy Service, puede enviar solicitudes para acceder a datos privados o personales de clientes o eliminarlos de aplicaciones de Adobe Experience Cloud, lo que facilita el cumplimiento automatizado de las regulaciones de privacidad legales y organizativas.

Consulte la [Introducción al Privacy Service](../../privacy-service/home.md) para obtener más información.

### Procesamiento de consentimiento {#consent}

Muchas regulaciones legales de privacidad han introducido requisitos para un consentimiento activo y específico en lo que respecta a la recopilación de datos, personalización y otros casos de uso de marketing. Para cumplir estos requisitos, Experience Platform le permite capturar información de consentimiento en perfiles de clientes individuales y utilizar esas preferencias como un factor determinante en la forma en que se utilizan los datos de cada cliente en los flujos de trabajo de la plataforma descendente.

Para obtener información sobre cómo procesar los datos de preferencias y consentimiento del cliente mediante el estándar de Adobe, consulte la información general sobre [procesamiento de consentimiento en Experience Platform](./consent/adobe/overview.md).

Para obtener información sobre cómo procesar los datos de consentimiento del cliente de acuerdo con el marco de transparencia y consentimiento (TCF) 2.0 de IAB, consulte la información general sobre [Compatibilidad con IAB TCF 2.0 en Platform](./consent/iab/overview.md).

## Seguridad {#security}

La integridad y seguridad de sus datos es indispensable para su negocio, y este riesgo requiere capacidades de seguridad líderes en la industria. Para superar este desafío, Platform proporciona varias herramientas que le ayudarán a salvaguardar las operaciones de datos.

### Cifrado de datos

Todos los datos de Platform se cifran en tránsito y en reposo. Consulte el documento sobre [cifrado de datos en Platform](./encryption.md) para obtener más información.

### Control de acceso {#access-control}

Experience Platform utiliza Adobe Admin Console para proporcionar control de acceso basado en funciones a varias funciones de Platform. Esta funcionalidad aprovecha los perfiles de producto en Admin Console, que vinculan a los usuarios con permisos y entornos limitados.

Consulte la [información general de control de acceso](../../access-control/home.md) para obtener más información.

### Zonas protegidas {#sandboxes}

Experience Platform está diseñado para enriquecer las aplicaciones de experiencia digital a escala global. Las empresas suelen ejecutar varias aplicaciones de experiencia digital en paralelo y necesitan encargarse del desarrollo, las pruebas y la implementación de estas aplicaciones, a la vez que garantizan el cumplimiento normativo.

Para satisfacer la necesidad de flexibilidad de desarrollo, Experience Platform proporciona entornos limitados que dividen una sola instancia de Platform en entornos virtuales independientes para ayudarle a desarrollar aplicaciones de experiencia digital basadas en su propio ciclo de vida de desarrollo.

Consulte la [información general sobre las zonas protegidas](../../sandboxes/home.md) para obtener más detalles.

## Pasos siguientes

Este documento proporciona una visión general de los distintos servicios y herramientas de Platform relacionados con la gobernanza de datos, la privacidad y la seguridad. Consulte la documentación relacionada con esta guía para obtener más información sobre estas funciones.
