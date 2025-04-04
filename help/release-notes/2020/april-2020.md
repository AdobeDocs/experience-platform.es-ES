---
title: 'Notas de la versión de Adobe Experience Cloud: abril de 2020'
description: Las notas de la versión de abril de 2020 de Adobe Experience Platform.
doc-type: release notes
last-update: April 13, 2020
author: ens71067
keywords: notas de la versión;
exl-id: 0f68c71e-3c9d-453b-a953-1cd1b6ca2e35
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '985'
ht-degree: 28%

---

# Notas de la versión de Adobe Experience Platform

**Fecha de publicación: jueves, 08 de abril de 2020**

Nuevas funciones de Adobe Experience Platform:
* [[!DNL Intelligent Services]](#intelligent)

Actualizaciones de funciones existentes:
* [[!DNL Experience Data Model (XDM)]](#xdm)
* [Gobernanza de datos](#governance)
* [[!DNL Destinations]](#destinations)
* [[!DNL Privacy Service]](#privacy)
* [[!DNL Sources]](#sources)

## [!DNL Intelligent Services] {#intelligent}

[!DNL Intelligent Services] permite a los analistas y profesionales de marketing aprovechar el poder de la inteligencia artificial y el aprendizaje automático en casos prácticos de experiencias del cliente. Esto permite a los analistas de marketing formular predicciones específicas de las necesidades de una empresa mediante configuraciones de negocio sin necesidad de tener experiencia en la ciencia de datos. Además, los profesionales de marketing pueden activar predicciones en aplicaciones de Adobe Experience Cloud, Adobe Experience Platform y de terceros.

**Funciones principales**

| Función | Descripción |
|---|---|
| [!DNL Customer AI] | [!DNL Customer AI] proporciona a los especialistas en marketing el poder de generar predicciones de clientes en el nivel individual con explicaciones. Con la ayuda de factores influyentes, [!DNL Customer AI] puede indicarle qué es lo más probable que haga un cliente y por qué. Además, los especialistas en marketing pueden beneficiarse de las predicciones y perspectivas de [!DNL Customer AI] para personalizar las experiencias de los clientes y ofrecerles las ofertas y los mensajes más adecuados. |
| [!DNL Attribution AI] | [!DNL Attribution AI] es un servicio de atribución algorítmica de varios canales que calcula la influencia y el impacto incremental de las interacciones de los clientes con los resultados especificados. Con [!DNL Attribution AI], los especialistas en marketing pueden medir y optimizar el gasto en marketing y publicidad al comprender el impacto de cada interacción individual con los clientes en cada fase de los recorridos de los clientes. |

**Problemas conocidos**

* No hay problemas conocidos actualmente.

Para obtener más información sobre [!DNL Intelligent Services] y lo que puede ofrecer, consulte la [descripción general de los servicios inteligentes](../../intelligent-services/home.md).

## Sistema [!DNL Experience Data Model] (XDM) {#xdm}

La estandarización y la interoperabilidad son conceptos clave detrás de [!DNL Experience Platform]. [!DNL Experience Data Model] (XDM), impulsado por Adobe, es un esfuerzo para estandarizar los datos de experiencia del cliente y definir esquemas para la administración de experiencias del cliente.

XDM es una especificación documentada públicamente y diseñada para mejorar la potencia de las experiencias digitales. Proporciona estructuras y definiciones comunes para cualquier aplicación para comunicarse con servicios en Adobe Experience Platform. Al adherirse a los estándares XDM, todos los datos de experiencia del cliente se pueden incorporar en una representación común que ofrece perspectivas de una manera más rápida e integrada. Puede obtener información valiosa de las acciones de los clientes, definir sus públicos mediante segmentos y utilizar sus atributos para fines de personalización.

**Nuevas funciones**

| Función | Descripción |
| --- | --- |
| Información de pantalla alternativa automática | [!DNL Schema Registry] aplica automáticamente los valores de título y descripción personalizados configurados en el descriptor `alternateDisplayInfo`. |
| Restricciones de campo escalar | [!DNL Schema Registry] no permite más de 6000 campos escalares en un solo esquema. |
| Revisión del rendimiento | Se ha revisado [!DNL Schema Registry] para que funcione mejor y cumpla mejor con las demandas de [!DNL Experience Platform]. |

**Corrección de errores**

* Se ha actualizado XDM a XED convertido para admitir un formato XED más limpio para los campos URI anidados en el XDM estándar.

**Problemas conocidos**

* Conocido

## Control de datos {#governance}

La gobernanza de datos de Adobe Experience Platform es una serie de estrategias y tecnologías que se utilizan para administrar los datos de los clientes y garantizar el cumplimiento de las regulaciones, restricciones y políticas aplicables al uso de datos. Desempeña una función clave dentro de [!DNL Experience Platform] en varios niveles, incluida la catalogación, el linaje de datos, el etiquetado del uso de los datos, las políticas de acceso a los datos y el control de acceso de los datos para las acciones de marketing.

Para empezar a usar el control de datos, es necesario comprender a fondo las regulaciones, las obligaciones contractuales y las políticas corporativas que se aplican a los datos de sus clientes. A partir de ahí, los datos se pueden clasificar aplicando las etiquetas de uso de datos adecuadas y su uso se puede controlar mediante la definición de políticas de uso de datos.

El marco de trabajo de control de datos simplifica y optimiza el proceso de categorizar los datos y crear directivas de uso de datos a través de la interfaz de usuario [!DNL Experience Platform] y la API [!DNL Policy Service].

**Nuevas funciones**

| Función | Descripción |
| -----------| ---------- |
| Administrar las políticas de uso de datos en la IU | Ahora, las directivas de uso de datos se pueden administrar en el área de trabajo **Políticas** de la interfaz de usuario de [!DNL Experience Platform]. Consulte la [guía de usuario de directivas](../../data-governance/policies/user-guide.md) para obtener más información. |

**Problemas conocidos**

* Ninguna.

Para obtener más información, consulte [Resumen de control de datos](../../data-governance/home.md).


## Destinos {#destinations}

En [Real-Time Customer Data Platform](../../rtcdp/overview.md), los destinos son integraciones prediseñadas con plataformas de destino que activan los datos para esos socios de una manera perfecta.

**Nuevos destinos**

Real-Time CDP ahora admite la activación de datos en más de cincuenta extensiones de [!DNL Experience Cloud Launch], lo que permite realizar análisis, personalizaciones y otros casos de uso. Consulte a continuación para obtener más información:

| Documentación | Descripción |
|--- | ---|
| [Tipos y categorías de destino](../../destinations/destination-types.md) | En este artículo se explica la diferencia entre conexiones y extensiones en la interfaz de Real-Time CDP y se recomienda cuándo utilizar cada uno de estos destinos. |
| [Extensiones de Experience Platform Launch](../../destinations/catalog/launch-extensions/overview.md) | En esta página se explica cuáles son las extensiones de [!DNL Launch], se enumeran los casos de uso para utilizarlas y se proporcionan vínculos a la documentación de cada extensión de [!DNL Launch] en Real-Time CDP. |

Para obtener más información, consulte [Información general sobre destinos](../../destinations/home.md).

## [!DNL Privacy Service] {#privacy}

Las nuevas regulaciones legales y organizativas otorgan a los usuarios el derecho de acceder o eliminar sus datos personales de sus almacenes de datos si así lo solicitan. Adobe Experience Platform [!DNL Privacy Service] proporciona una API de RESTful y una interfaz de usuario para ayudarle a administrar estas solicitudes de datos de los clientes. Con [!DNL Privacy Service], puede enviar solicitudes para acceder a datos personales de clientes y eliminarlos de aplicaciones de Adobe Experience Cloud, lo que facilita el cumplimiento automatizado de las regulaciones de privacidad legales y organizativas.

**Nuevas funciones**

| Función | Descripción |
| --- | --- |
| Compatibilidad con PDPA | Ahora, las solicitudes de privacidad se pueden crear y rastrear según la Ley de Protección de Datos Personales (PDPA) en Tailandia. Al realizar solicitudes de privacidad en la API, la matriz de `regulation` acepta el valor “pdpa_tha”. |
| Tipos de espacio de nombres en la IU | Ahora puede especificar diferentes tipos de espacio de nombres en el generador de solicitudes en la interfaz de usuario de [!DNL Privacy Service]. Si desea obtener más información, consulte la [Guía del usuario](../../privacy-service/ui/user-guide.md). |
| Obsolescencia del punto final anterior | El punto final de API anterior (`data/privacy/gdpr`) ha quedado obsoleto. |

Problemas conocidos

* Ninguna

Para obtener más información acerca de [!DNL Privacy Service], comience por leer la [descripción general de Privacy Service](../../privacy-service/home.md).

## Fuentes {#sources}

Adobe Experience Platform puede ingerir datos de orígenes externos y, al mismo tiempo, estructurarlos, etiquetarlos y mejorarlos mediante los servicios de [!DNL Experience Platform]. Puede introducir datos de una variedad de fuentes, como aplicaciones de Adobe, almacenamiento basado en la nube, software de terceros y su sistema CRM.

[!DNL Experience Platform] proporciona una API RESTful y una interfaz de usuario interactiva que le permite configurar conexiones de origen para varios proveedores de datos con facilidad. Estas conexiones de origen le permiten autenticarse y conectarse a sistemas de almacenamiento externos y servicios CRM, establecer tiempos para ejecuciones de ingesta y administrar el rendimiento de ingesta de datos.

**Nuevas funciones**

| Función | Descripción |
| ------- | ----------- |
| Compatibilidad de API e IU con bases de datos | Conectores de origen nuevos para [!DNL Apache Spark] (en HDInsights), [!DNL Azure Synapse Analytics], [!DNL Azure Table Storage], [!DNL Hive] (en HDInsights) y [!DNL Phoenix]. |
| Compatibilidad con API e IU para aplicaciones basadas en pagos | Conectores de origen nuevos para [!DNL PayPal]. |
| Compatibilidad con API e IU para aplicaciones basadas en protocolos | Conectores de origen nuevos para [!DNL Generic OData]. |

**Problemas conocidos**

* Ninguna

Para obtener más información sobre las fuentes, consulte [descripción general de las fuentes](../../sources/home.md).
