---
keywords: Experience Platform;inicio;temas populares
solution: Experience Platform
title: Información general sobre administración, privacidad y seguridad
description: Adobe Experience Platform proporciona varios servicios y herramientas que le permiten controlar con seguridad los datos de experiencia recopilados para cumplir con sus prácticas comerciales, obligaciones legales y procesos de desarrollo.
exl-id: 1ab5a436-c5dd-4e7a-aba1-549f0613f224
source-git-commit: 5a14eb5938236fa7186d1a27f28cee15fe6558f6
workflow-type: tm+mt
source-wordcount: '855'
ht-degree: 1%

---

# Gobernanza, privacidad y seguridad en Adobe Experience Platform

Adobe Experience Platform le permite ingerir, analizar, optimizar y realizar acciones en sus datos para mejorar en gran medida las experiencias de los clientes. Estos datos son vastos, complejos e increíblemente valiosos. Según la naturaleza de sus operaciones de datos, las jurisdicciones legales en las que opera su negocio y las políticas organizativas relativas al uso de datos, debe controlar y supervisar cuidadosamente la recopilación y el uso de los datos de experiencia del cliente para proteger sus intereses comerciales.

Experience Platform proporciona varios servicios y herramientas que le permiten controlar con seguridad los datos de experiencia recopilados para cumplir con sus prácticas comerciales, obligaciones legales y procesos de desarrollo. En las secciones siguientes se presenta una introducción a cada uno de estos servicios, junto con enlaces a la documentación para obtener más información.

Los servicios se pueden categorizar en tres dominios:

* [Administración de datos](#governance)
* [Privacidad](#privacy)
* [Seguridad](#security)

## Administración de datos {#governance}

La gobernanza de los datos es un concepto esencial que está vinculado a todas las capacidades del Experience Platform. El control de datos representa su capacidad de controlar y comprender sus datos a través de su recorrido a través de Platform. Esto implica mantener la calidad de los datos, el linaje de datos, la catalogación de datos y mucho más.

### Administración de datos de Adobe Experience Platform {#data-governance}

Como servicio de plataforma, la Administración de datos de Adobe Experience Platform le permite administrar los datos de los clientes y garantizar el cumplimiento de las regulaciones, restricciones y políticas aplicables al uso de los datos. Desempeña un papel clave dentro del Experience Platform en varios niveles, incluido el etiquetado del uso de los datos, las políticas de uso de los datos, la aplicación de políticas y el linaje de datos.

Consulte la [Información general sobre la administración de datos](../../data-governance/home.md) para obtener más información.

### Catálogo y conjuntos de datos {#catalog}

El servicio de catálogo es el sistema de registro para la ubicación y linaje de datos dentro de Platform. Aunque todos los datos que se incorporan en el Experience Platform se almacenan en el lago de datos como archivos y directorios, Catálogo guarda los metadatos y la descripción de esos archivos y directorios con fines de búsqueda y supervisión.

El catálogo organiza los datos ingestados en conjuntos de datos, cada uno de los cuales contiene metadatos que se pueden usar para etiquetar y categorizar los datos que contiene.

Consulte la [Información general del servicio de catálogo](../../catalog/home.md) para obtener más información sobre el servicio. Para obtener información sobre cómo administrar conjuntos de datos en Experience Platform, consulte la [información general sobre conjuntos de datos](../../catalog/datasets/overview.md).

## Privacidad {#privacy}

La privacidad es un problema crítico para su negocio, legisladores y sus clientes. Dado que los datos personales recopilados de sus clientes están en el centro de casi todos los flujos de trabajo de los Experience Platform, Platform proporciona servicios para admitir estas iniciativas.

### Adobe Experience Platform Privacy Service {#privacy-service}

Las regulaciones legales de privacidad, como el Reglamento General de Protección de Datos (RGPD) de la Unión Europea y la Ley de Privacidad del Consumidor de California (CCPA), otorgan a los ciudadanos dentro de sus jurisdicciones el derecho a acceder y eliminar los datos personales que recopile y almacene de ellos.

Adobe Experience Platform Privacy Service proporciona una API de RESTful y una interfaz de usuario para ayudar a administrar estas solicitudes. Con Privacy Service, puede enviar solicitudes para acceder a datos de clientes personales o privados desde aplicaciones de Adobe Experience Cloud, lo que facilita el cumplimiento automatizado de las normas de privacidad legales y organizativas.

Consulte la [Información general del Privacy Service](../../privacy-service/home.md) para obtener más información.

### Procesamiento de consentimiento {#consent}

Muchas regulaciones legales de privacidad han introducido requisitos para el consentimiento activo y específico cuando se trata de recopilación de datos, personalización y otros casos de uso de marketing. Para satisfacer estos requisitos, el Experience Platform le permite capturar información de consentimiento en perfiles de clientes individuales y utilizar esas preferencias como factor determinante en el modo en que los datos de cada cliente se utilizan en flujos de trabajo de Platform descendentes.

Para aprender a procesar el consentimiento del cliente y los datos de preferencias mediante el estándar de Adobe, consulte la descripción general de [procesamiento de consentimiento en el Experience Platform](./consent/adobe/overview.md).

Para obtener información sobre cómo procesar los datos de consentimiento del cliente de acuerdo con el marco de transparencia y consentimiento IAB (TCF) 2.0, consulte la descripción general de [Compatibilidad con IAB TCF 2.0 en Platform](./consent/iab/overview.md).

## Seguridad {#security}

La integridad y la seguridad de sus datos son indispensables para su negocio, y este riesgo requiere capacidades de seguridad líderes en la industria. Para enfrentar este desafío, Platform proporciona varias herramientas que ayudan a salvaguardar sus operaciones de datos.

### Cifrado de datos

Todos los datos de la plataforma se cifran en tránsito y en reposo. Consulte el documento en [cifrado de datos en Platform](./encryption.md) para obtener más información.

### Control de acceso {#access-control}

Experience Platform utiliza Adobe Admin Console para proporcionar control de acceso basado en funciones a diversas funcionalidades de Platform. Esta funcionalidad aprovecha los perfiles de producto del Admin Console, que vinculan a los usuarios con permisos y entornos limitados.

Consulte la [información general sobre el control de acceso](../../access-control/home.md) para obtener más información.

### Zonas protegidas {#sandboxes}

Experience Platform está diseñado para enriquecer las aplicaciones de experiencia digital a escala global. A menudo, las empresas ejecutan varias aplicaciones de experiencia digital en paralelo y deben encargarse del desarrollo, las pruebas y la implementación de estas aplicaciones, asegurando al mismo tiempo el cumplimiento de las normas operacionales.

Para satisfacer la necesidad de flexibilidad de desarrollo, Experience Platform proporciona entornos limitados que dividen una sola instancia de Platform en entornos virtuales independientes para ayudarle a desarrollar sus aplicaciones de experiencia digital en función de su propio ciclo de vida de desarrollo.

Consulte la [información general sobre los entornos limitados](../../sandboxes/home.md) para obtener más información.

## Pasos siguientes

Este documento proporciona información general sobre los distintos servicios y herramientas de Platform relacionados con el control de datos, la privacidad y la seguridad. Consulte la documentación vinculada a esta guía para obtener más información sobre estas funciones.
