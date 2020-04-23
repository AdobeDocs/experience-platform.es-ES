---
title: 'Notas de la versión de Adobe Experience Platform '
description: Notas de la versión de la plataforma de experiencia 8 de abril de 2020
doc-type: release notes
last-update: April 13, 2020
author: ens71067
keywords: release notes;
translation-type: tm+mt
source-git-commit: 8cc3b63fc91877ca1337f65e8f5c0e949b7ef01f

---


# Notas de la versión de Adobe Experience Platform

## Fecha de publicación: 8 de abril de 2020

Nuevas funciones de Adobe Experience Platform:
* [Servicios inteligentes](#intelligent)

Actualizaciones de funciones existentes:
* [Modelo de datos de experiencia (XDM)](#xdm)
* [Gobierno de datos](#governance)
* [Destinos](#destinations)
* [Privacy Service](#privacy)
* [Fuentes](#sources)

## Servicios inteligentes {#intelligent}

Los servicios inteligentes potencian a los analistas de marketing y a los profesionales para que aprovechen el poder de la inteligencia artificial y el aprendizaje automático en casos de uso de la experiencia del cliente. Esto permite que los analistas de mercadotecnia configuren predicciones específicas de las necesidades de una compañía mediante configuraciones de nivel empresarial sin necesidad de conocimientos de ciencia de datos. Además, los profesionales de marketing pueden activar predicciones en Adobe Experience Cloud, Adobe Experience Platform y aplicaciones de terceros.

**Funciones principales**

| Función | Descripción |
|---|---|
| AI del cliente | La API de cliente proporciona a los especialistas en marketing la capacidad de generar predicciones de clientes a nivel individual con explicaciones. Con la ayuda de factores influyentes, la información sobre el cliente puede indicarle qué es lo que probablemente hará un cliente y por qué. Además, los especialistas en marketing pueden beneficiarse de las predicciones y perspectivas de la API del cliente para personalizar las experiencias de los clientes al ofrecer las ofertas y los mensajes más adecuados. |
| Atribución AI | La API de atribución es un servicio de atribución algorítmica de varios canales que calcula la influencia y el impacto incremental de las interacciones de los clientes con respecto a los resultados especificados. Con la API de atribución, los especialistas en mercadotecnia pueden medir y optimizar el gasto en mercadotecnia y publicidad al comprender el impacto de cada interacción del cliente en cada fase de los viajes de los clientes. |

**Problemas conocidos**

* Actualmente no hay problemas conocidos.

Para obtener más información sobre los servicios inteligentes y qué tiene que ver con la oferta, consulte la descripción general [de los servicios](../../intelligent-services/home.md)inteligentes.

## Sistema de modelo de datos de experiencia (XDM) {#xdm}

La estandarización y la interoperabilidad son conceptos clave que sustentan la plataforma de experiencia. El modelo de datos de experiencia (XDM), impulsado por Adobe, es un esfuerzo para estandarizar los datos de experiencia del cliente y definir esquemas para la administración de la experiencia del cliente.

XDM es una especificación públicamente documentada diseñada para mejorar el poder de las experiencias digitales. Proporciona estructuras y definiciones comunes para que cualquier aplicación se comunique con los servicios de la plataforma Adobe Experience. Al cumplir con los estándares XDM, todos los datos de experiencia del cliente se pueden incorporar a una representación común que ofrece perspectivas de una manera más rápida e integrada. Puede obtener perspectivas valiosas de las acciones de los clientes, definir audiencias de clientes a través de segmentos y utilizar atributos de clientes para fines de personalización.

**Nuevas funciones**

| Función | Descripción |
| --- | --- |
| Información de visualización alternativa automática | El Registro de Esquemas aplica automáticamente los valores personalizados de título y descripción configurados en el `alternateDisplayInfo` descriptor. |
| Restricciones de campo escalar | El Registro de Esquemas no permite más de 6000 campos escalares en un solo esquema. |
| Revisión general del rendimiento | Se ha revisado el Registro de Esquemas para que cumpla mejor las exigencias de la Plataforma de experiencias. |

**Corrección de errores**

* Se ha actualizado XDM a XED para que admita un formato XED más nítido para campos URI anidados en XDM estándar.

**Problemas conocidos**

* Conocido

## Gobierno de datos {#governance}

La Administración de datos de la plataforma de experiencia de Adobe es una serie de estrategias y tecnologías que se utilizan para administrar los datos de los clientes y garantizar el cumplimiento de las normativas, restricciones y políticas aplicables al uso de los datos. Desempeña un papel clave dentro de la plataforma de experiencias en varios niveles, incluyendo la catalogación, el linaje de datos, el etiquetado del uso de datos, las políticas de acceso a datos y el control de acceso en los datos para las acciones de marketing.

Para comenzar con la administración de datos, es necesario comprender a fondo las regulaciones, las obligaciones contractuales y las políticas corporativas que se aplican a los datos del cliente. Desde allí, los datos pueden clasificarse aplicando las etiquetas de uso de datos correspondientes, y su uso puede controlarse mediante la definición de políticas de uso de datos.

El marco DULE simplifica y racionaliza el proceso de categorización de datos y creación de políticas de uso de datos a través de la interfaz de usuario de la plataforma de experiencia y la API del servicio de políticas DULE.

**Nuevas funciones**

| Función | Descripción |
| -----------| ---------- |
| Administrar directivas de uso de datos en la interfaz de usuario | Las directivas de uso de datos ahora se pueden administrar dentro del espacio de trabajo _Directivas_ en la interfaz de usuario de la plataforma de experiencia. Consulte la guía del usuario de [directivas](../../data-governance/policies/user-guide.md) para obtener más información. |

**Problemas conocidos**

* None.

Para obtener más información, consulte la información general [sobre el Gobierno](../../data-governance/home.md)de datos.


## Destinos {#destinations}

En la plataforma [de datos del cliente en tiempo real de](../../rtcdp/overview.md)Adobe, los destinos son integraciones prediseñadas con plataformas de destino que activan los datos a dichos socios de forma transparente.

**Nuevos destinos**

Ahora, CDP en tiempo real de Adobe admite la activación de datos a más de cincuenta extensiones de Experience Cloud Launch, lo que permite análisis, personalización y otros casos de uso. Consulte a continuación los detalles:

| Documentación | Descripción |
|--- | ---|
| [Tipos y categorías de destino](/help/rtcdp/destinations/destination-types.md) | En este artículo se explica la diferencia entre las conexiones y las extensiones en la interfaz CDP en tiempo real de Adobe y se recomienda cuándo utilizar cada uno de estos destinos. |
| [Extensiones de Experience Platform Launch](/help/rtcdp/destinations/experience-platform-launch-extensions.md) | En esta página se explica qué son las extensiones de Launch, las listas usan casos para utilizarlas y los vínculos a la documentación de cada extensión Launch en Adobe Real-time CDP. |

Para obtener más información, consulte la información general sobre [los destinos](/help/rtcdp/destinations/destinations-overview.md).

## Privacy Service {#privacy}

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

## Fuentes {#sources}

Adobe Experience Platform puede ingestar datos de fuentes externas y permitirle estructurarlos, etiquetarlos y mejorarlos mediante los servicios de plataforma. Puede ingestar datos de una variedad de fuentes, como aplicaciones de Adobe, almacenamiento basado en la nube, software de terceros y su sistema CRM.

La plataforma de experiencia proporciona una API RESTful y una interfaz de usuario interactiva que le permite configurar fácilmente las conexiones de origen para varios proveedores de datos. Estas conexiones de origen le permiten autenticarse y conectarse a sistemas de almacenamiento externos y servicios CRM, establecer tiempos para ejecuciones de ingestión y administrar el rendimiento de la ingesta de datos.

**Nuevas funciones**

| Función | Descripción |
| ------- | ----------- |
| Compatibilidad de API e interfaz de usuario con bases de datos | Nuevos conectores de origen para Apache Spark (en HDInsights), Azure Synapse Analytics, Azure Table Almacenamiento, Hive (en HDInsights) y Phoenix. |
| Compatibilidad de API e interfaz de usuario para aplicaciones basadas en pagos | Nuevos conectores de origen para PayPal. |
| Compatibilidad de API e interfaz de usuario para aplicaciones basadas en protocolos | Nuevos conectores de origen para la OData genérica. |

**Problemas conocidos**

* None

Para obtener más información sobre las fuentes, consulte la descripción general [de](../../sources/home.md)las fuentes.
