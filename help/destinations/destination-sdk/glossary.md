---
solution: Experience Platform
title: Glosario de Adobe Experience Platform Destination SDK
description: Comprender la terminología importante al crear un destino con Experience Platform Destination SDK.
exl-id: d65f390a-a980-49b8-9570-840f03534553
source-git-commit: 20427c4c8826905a77fac04d055d523b12a6f739
workflow-type: tm+mt
source-wordcount: '669'
ht-degree: 2%

---

# Glosario de Destination SDK [!DNL Adobe Experience Platform]

Consulte este glosario para ver las definiciones de los términos utilizados en Destination SDK. Para ver otros términos de [!DNL Adobe Experience Platform], consulte el [glosario de Experience Platform](/help/landing/glossary.md).

## A {#a}

**Política de agregación**: al configurar cómo se deben exportar los datos a su destino de flujo continuo en tiempo real, puede definir cómo se agregan los datos de perfil antes de enviarlos a su plataforma de destino. Esto ayuda a optimizar la entrega de datos mediante la agrupación de registros de datos basados en criterios específicos, la reducción de la frecuencia de las llamadas de API y la mejora de la eficacia general. Se pueden configurar diferentes políticas para satisfacer varios requisitos de destino, lo que garantiza que los datos se empaqueten y entreguen de la manera más eficaz. [Más información](/help/destinations/destination-sdk/functionality/destination-configuration/aggregation-policy.md).

**Configuración de metadatos de audiencia**: una configuración de metadatos de audiencia hace referencia a la configuración estructurada y a los parámetros definidos en [!DNL Adobe Experience Platform] que habilitan la creación, actualización y eliminación mediante programación de segmentos de audiencia en un destino especificado. Esta configuración utiliza plantillas de metadatos de audiencia para alinearse con las especificaciones de la API de marketing de la plataforma de destino. Obtenga más información acerca de la [configuración de metadatos de audiencia](/help/destinations/destination-sdk/functionality/audience-metadata-management.md) y las [macros disponibles](/help/destinations/destination-sdk/functionality/audience-metadata-management.md#macros).

## D {#d}

**Extremo de configuración de destino**: un extremo de configuración de destino en [!DNL Adobe Experience Platform], específicamente el extremo de API `/authoring/destinations`, crea, recupera, actualiza y elimina configuraciones para destinos. Estas configuraciones definen cómo se entregan los datos de [!DNL Adobe Experience Platform] a varios sistemas o destinos externos, como plataformas de marketing, servicios de almacenamiento en la nube u otros extremos de procesamiento de datos. Obtenga más información sobre [opciones de configuración disponibles](/help/destinations/destination-sdk/functionality/configuration-options.md#destination-configuration) y vea la [documentación de referencia](/help/destinations/destination-sdk/authoring-api/destination-configuration/create-destination-configuration.md).

**Instancia de destino**: una configuración específica de una configuración de destino en [!DNL Adobe Experience Platform], creada y administrada mediante la interfaz de usuario de Experience Platform. Incluye todos los parámetros y credenciales necesarios para conectar y enviar datos al destino. Después de establecer la conexión con su destino, puede obtener el identificador de la instancia de destino al [explorar una conexión con su destino](/help/destinations/ui/destination-details-page.md).

![Imagen de interfaz de usuario sobre cómo obtener el identificador de instancia de destino](/help/destinations/destination-sdk/assets/testing-api/get-destination-instance-id.png)

## P {#p}

**[!DNL Pebble]plantilla**: una plantilla [!DNL Pebble] transforma los datos exportados de [!DNL Adobe Experience Platform] en el formato requerido por la plataforma de destino. Utiliza el lenguaje de plantilla [!DNL Pebble], que permite la transformación dinámica de datos mediante funciones como `filter`, `for`, `if` y `set`. [!DNL Adobe Experience Platform] incluye funciones personalizadas adicionales como `addedSegments` y `removedSegments`. Estas plantillas ayudan a dar formato a los elementos de datos, como las marcas de tiempo y las suscripciones a audiencias, para satisfacer las especificaciones del destino. Más información [aquí](/help/destinations/destination-sdk/functionality/destination-server/message-format.md) y [aquí](/help/destinations/destination-sdk/functionality/destination-server/templating-specs.md).

**Destino privado**: integraciones personalizadas creadas por clientes individuales de [!DNL Adobe Experience Platform]. Están diseñadas para satisfacer necesidades comerciales específicas y solo son accesibles dentro de la organización del cliente, lo que ofrece flexibilidad en las configuraciones de exportación de datos. Los destinos privados solo están disponibles para [!DNL Real-Time CDP] clientes de Ultimate. [Más información](/help/destinations/destination-sdk/overview.md#productized-custom-integrations).

**Destino público**: una integración disponible públicamente en el catálogo [!DNL Adobe Experience Platform]. Estos destinos están estandarizados, tienen marca y simplifican la configuración del cliente al proporcionar parámetros preconfigurados. Son accesibles para todos los clientes que utilizan [!DNL Adobe Experience Platform]. [Más información](/help/destinations/destination-sdk/overview.md#productized-custom-integrations).

## S {#s}

**Plantilla de documentación de autoservicio**: La plantilla de documentación de autoservicio proporciona un formato estructurado que puede utilizar para documentar el destino. Incluye secciones para obtener una descripción general, casos de uso, requisitos previos, identidades admitidas, audiencias, tipos de exportación y frecuencia, así como pasos para conectarse al destino, activar audiencias y asignar atributos. Utilice esta plantilla para garantizar una documentación completa y coherente, lo que permite a los clientes empezar rápidamente a utilizar su destino y comprender los casos de uso proporcionados. Obtenga más información sobre [cómo documentar tu destino](/help/destinations/destination-sdk/docs-framework/documentation-instructions.md), [descargar la última plantilla de documentación de autoservicio](/help/destinations/destination-sdk/assets/docs-framework/yourdestination-template.zip) y [ver cómo se procesa](/help/destinations/destination-sdk/docs-framework/self-service-template.md).

## T {#t}

**Especificaciones de plantilla y estrategias de creación de plantillas**: Las especificaciones de plantilla son configuraciones utilizadas para dar formato a las solicitudes HTTP enviadas desde [!DNL Adobe Experience Platform] a un destino. Transforman los campos de atributos de perfil del esquema XDM en un formato compatible con la plataforma de destino. Usando un lenguaje de plantilla similar a [!DNL Jinja], estas especificaciones permiten transformaciones de datos dinámicas basadas en reglas específicas y datos de entrada. [Más información](/help/destinations/destination-sdk/functionality/destination-server/templating-specs.md).

**API de prueba**: use la API de prueba para validar las configuraciones de destino antes de enviar una solicitud de publicación. Proporciona herramientas para generar perfiles de muestra y probar el flujo de datos, asegurándose de que la configuración coincida con los requisitos del destino. La API admite destinos de flujo continuo y basados en archivos (por lotes), lo que ofrece una forma de simular datos y solucionar posibles problemas en el proceso de configuración. Obtenga más información acerca de la API de prueba para [streaming](/help/destinations/destination-sdk/testing-api/streaming-destinations/streaming-destination-testing-overview.md) y [destinos basados en archivos](/help/destinations/destination-sdk/testing-api/batch-destinations/file-based-destination-testing-overview.md).

**Plantilla de transformación**: Una plantilla de transformación personaliza el formato de datos del esquema XDM de Adobe al formato esperado del destino. [Más información](/help/destinations/destination-sdk/functionality/destination-server/message-format.md).
