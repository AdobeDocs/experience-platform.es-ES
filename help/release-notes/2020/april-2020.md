---
title: 'Notas de la versión de Adobe Experience Platform '
description: Notas de la versión de la plataforma de experiencia 8 de abril de 2020
doc-type: release notes
last-update: March 4, 2020
author: ens71067
translation-type: tm+mt
source-git-commit: 3f3704cc1e11a4d11278a34800c8bfdc24a80753

---


# Notas de la versión de Adobe Experience Platform

## Fecha de publicación: 8 de abril de 2020

## Servicios inteligentes

Los servicios inteligentes potencian a los analistas de marketing y a los profesionales para que aprovechen el poder de la inteligencia artificial y el aprendizaje automático en casos de uso de la experiencia del cliente. Esto permite que los analistas de mercadotecnia configuren predicciones específicas de las necesidades de una compañía mediante configuraciones de nivel empresarial sin necesidad de conocimientos de ciencia de datos. Además, los profesionales de marketing pueden activar predicciones en Adobe Experience Cloud, Adobe Experience Platform y aplicaciones de terceros.

**Funciones principales**

| Función | Descripción |
|---|---|
| AI del cliente | La API de cliente proporciona a los especialistas en marketing la capacidad de generar predicciones de clientes a nivel individual con explicaciones. Con la ayuda de factores influyentes, la información sobre el cliente puede indicarle qué es lo que probablemente hará un cliente y por qué. Además, los especialistas en marketing pueden beneficiarse de las predicciones y perspectivas de la API del cliente para personalizar las experiencias de los clientes al ofrecer las ofertas y los mensajes más adecuados. |
| Atribución AI | La API de atribución es un servicio de atribución algorítmica de varios canales que calcula la influencia y el impacto incremental de las interacciones de los clientes con respecto a los resultados especificados. Con la API de atribución, los especialistas en mercadotecnia pueden medir y optimizar el gasto en mercadotecnia y publicidad al comprender el impacto de cada interacción del cliente en cada fase de los viajes de los clientes. |

**Problemas conocidos**

* Actualmente no hay problemas conocidos.

Para obtener más información sobre los servicios inteligentes y qué tiene que ver con la oferta, consulte la descripción general [de los servicios](../../intelligent-services/home.md)inteligentes.

## Privacy Service

Las nuevas regulaciones legales y organizativas otorgan a los usuarios el derecho de acceder a sus datos personales o eliminarlos de sus almacenes de datos si así lo solicitan. Adobe Experience Platform Privacy Service proporciona una API RESTful y una interfaz de usuario para ayudarle a administrar estas solicitudes de datos de sus clientes. Con Privacy Service, puede enviar solicitudes para acceder a los datos personales o privados de los clientes y eliminarlos de las aplicaciones de Adobe Experience Cloud, lo que facilita el cumplimiento automatizado de las normativas de privacidad legales y de la organización.

**Nuevas funciones**

| Función | Descripción |
| --- | --- |
| Compatibilidad con PDPA | Las solicitudes de privacidad ahora se pueden crear y rastrear bajo la Ley de Protección de Datos Personales (PDPA) en Tailandia. Al realizar solicitudes de privacidad en la API, la `regulation` matriz acepta el valor &quot;pdpa_tha&quot;. |
| Tipos de Área de nombres en la interfaz de usuario | Ahora puede especificar diferentes tipos de Área de nombres en el Creador de solicitudes en la interfaz de usuario de Privacy Service. Consulte la guía [del](../../privacy-service/ui/user-guide.md) usuario para obtener más información. |
| Desuso de punto final antiguo | El punto final (`data/privacy/gdpr`) de la API anterior ha quedado obsoleto. |

Problemas conocidos

* None

Para obtener más información acerca de Privacy Service, lea la información general [de](../../privacy-service/home.md)Privacy Service para obtener inicios.

## Fuentes

Adobe Experience Platform puede ingestar datos de fuentes externas y permitirle estructurarlos, etiquetarlos y mejorarlos mediante los servicios de plataforma. Puede ingestar datos de una variedad de fuentes, como aplicaciones de Adobe, almacenamiento basado en la nube, software de terceros y su sistema CRM.

La plataforma de experiencia proporciona una API RESTful y una interfaz de usuario interactiva que le permite configurar fácilmente las conexiones de origen para varios proveedores de datos. Estas conexiones de origen le permiten autenticarse y conectarse a sistemas de almacenamiento externos y servicios CRM, establecer tiempos para ejecuciones de ingestión y administrar el rendimiento de la ingesta de datos.

### Nuevas funciones

| Función | Descripción |
| ------- | ----------- |
| Compatibilidad de API e interfaz de usuario con bases de datos | Nuevos conectores de origen para Apache Spark (en HDInsights), Azure Synapse Analytics, Azure Table Almacenamiento, Hive (en HDInsights) y Phoenix. |
| Compatibilidad de API e interfaz de usuario para aplicaciones basadas en pagos | Nuevos conectores de origen para PayPal. |
| Compatibilidad de API e interfaz de usuario para aplicaciones basadas en protocolos | Nuevos conectores de origen para la OData genérica. |

### Problemas conocidos

* None

Para obtener más información sobre las fuentes, consulte la descripción general [de](../../source-connectors/home.md)las fuentes.

<!-- ## Access control

Experience Platform leverages [Adobe Admin Console](https://adminconsole.adobe.com) product profiles to link users with permissions and sandboxes. Permissions control access to a variety of Platform capabilities, including data modeling, profile management, and sandbox administration.

### Key features

|Feature | Description|
|--- | ---|
|Permissions | In the Admin Console, the _Permissions_ tab within a Platform product profile allows you customize which Platform capabilities are available for the users attached to that profile. Available permission categories include: Data Modeling, Data Management, Profile Management, Identities, Data Monitoring, Sandbox Administration, Destinations, Sources.|
|Access to sandboxes | The _Permissions_ tab within a Platform product profile can grant users access to specific sandboxes. See the section on [sandboxes](#sandboxes) below for more information.|

For more information, please see the [access control overview](../../access-control/home.md).

## Sandboxes

Experience Platform is built to enrich digital experience applications on a global scale. Companies often run multiple digital experience applications in parallel and need to cater for the development, testing, and deployment of these applications while ensuring operational compliance. In order to address this need, Experience Platform provides sandboxes which partition a single Platform instance into separate virtual environments to help develop and evolve digital experience applications.

### Key features

|Feature | Description|
|--- | ---|
|Production sandbox | Experience Platform provides a single production sandbox, which cannot be deleted or reset.|
|Non-production sandboxes | Multiple non-production sandboxes can be created for a single Platform instance, allowing you to test features, run experiments, and make custom configurations without impacting your production sandbox.|
|Sandbox switcher | In the Experience Platform user interface, the sandbox switcher in the top-left corner of the screen allows you to switch between available sandboxes through a dropdown menu.|
|`x-sandbox-name` header | All calls to Experience Platform APIs must now include the new `x-sandbox-name` header, whose value references the `name` attribute of the sandbox the operation will take place in.|

For more information, please see the [sandboxes overview](../../sandboxes/home.md). -->