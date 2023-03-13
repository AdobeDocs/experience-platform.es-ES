---
title: Notas de la versión de Adobe Experience Platform, abril de 2020
description: Notas de la versión de abril de 2020 de Adobe Experience Platform.
doc-type: release notes
last-update: April 13, 2020
author: ens71067
keywords: notas de la versión;
exl-id: 0f68c71e-3c9d-453b-a953-1cd1b6ca2e35
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '983'
ht-degree: 10%

---

# Notas de la versión de Adobe Experience Platform

**Fecha de publicación: 8 de abril de 2020**

Nuevas funciones de Adobe Experience Platform:
* [[!DNL Intelligent Services]](#intelligent)

Actualizaciones de funciones existentes:
* [[!DNL Experience Data Model (XDM)]](#xdm)
* [Control de datos](#governance)
* [[!DNL Destinations]](#destinations)
* [[!DNL Privacy Service]](#privacy)
* [[!DNL Sources]](#sources)

## [!DNL Intelligent Services] {#intelligent}

[!DNL Intelligent Services] capacite a los analistas y profesionales de marketing para aprovechar el poder de la inteligencia artificial y el aprendizaje automático en casos prácticos de experiencias del cliente. Esto permite a los analistas de marketing formular predicciones específicas de las necesidades de una empresa mediante configuraciones de negocio sin necesidad de tener experiencia en la ciencia de datos. Además, los profesionales de marketing pueden activar predicciones en aplicaciones de Adobe Experience Cloud, Adobe Experience Platform y de terceros.

**Funciones principales**

| Función | Descripción |
|---|---|
| [!DNL Customer AI] | [!DNL Customer AI] proporciona a los especialistas en marketing el poder de generar predicciones de clientes a nivel individual con explicaciones. Con la ayuda de factores influyentes, [!DNL Customer AI] le puede decir qué es lo más probable que haga un cliente y por qué. Además, los especialistas en marketing pueden beneficiarse de [!DNL Customer AI] predicciones y perspectivas para personalizar las experiencias de los clientes y ofrecerles las ofertas y los mensajes más adecuados. |
| [!DNL Attribution AI] | [!DNL Attribution AI] es un servicio de atribución algorítmica de varios canales que calcula la influencia y el impacto incremental de las interacciones de los clientes con los resultados especificados. Con [!DNL Attribution AI], los especialistas en marketing pueden medir y optimizar el gasto en marketing y publicidad al comprender el impacto de cada interacción individual con los clientes en cada fase de los recorridos de los clientes. |

**Problemas conocidos**

* No hay problemas conocidos actualmente.

Para obtener más información sobre [!DNL Intelligent Services] y lo que tiene para ofrecer, vea la [Información general sobre servicios inteligentes](../../intelligent-services/home.md).

## [!DNL Experience Data Model] Sistema (XDM) {#xdm}

La estandarización y la interoperabilidad son conceptos clave [!DNL Experience Platform]. [!DNL Experience Data Model] (XDM), impulsado por Adobe, es un esfuerzo para estandarizar los datos de experiencia del cliente y definir esquemas para la administración de experiencias del cliente.

XDM es una especificación documentada públicamente y diseñada para mejorar la potencia de las experiencias digitales. Proporciona estructuras y definiciones comunes para cualquier aplicación para comunicarse con servicios en Adobe Experience Platform. Al adherirse a los estándares XDM, todos los datos de experiencia del cliente se pueden incorporar en una representación común que ofrece perspectivas de una manera más rápida e integrada. Puede obtener información valiosa de las acciones de los clientes, definir las audiencias de los clientes mediante segmentos y utilizar los atributos del cliente para fines de personalización.

**Nuevas funciones**

| Función | Descripción |
| --- | --- |
| Información de pantalla alternativa automática | El [!DNL Schema Registry] aplica automáticamente los valores de título y descripción personalizados configurados en la variable `alternateDisplayInfo` descriptor. |
| Restricciones de campo escalar | El [!DNL Schema Registry] no permite más de 6000 campos escalares en un solo esquema. |
| Revisión del rendimiento | El [!DNL Schema Registry] ha sido revisado para que funcione y cumpla las exigencias de [!DNL Experience Platform] mejor. |

**Corrección de errores**

* Se ha actualizado XDM a XED convertido para admitir un formato XED más limpio para los campos URI anidados en el XDM estándar.

**Problemas conocidos**

* Conocido

## Control de datos {#governance}

Administración de datos de Adobe Experience Platform es una serie de estrategias y tecnologías que se utilizan para administrar los datos de los clientes y garantizar el cumplimiento de las regulaciones, restricciones y políticas aplicables al uso de datos. Desempeña un papel clave dentro de [!DNL Experience Platform] en varios niveles, incluida la catalogación, el linaje de datos, el etiquetado del uso de datos, las políticas de acceso a datos y el control de acceso a los datos para acciones de marketing.

Para empezar a usar el control de datos, es necesario comprender a fondo las regulaciones, las obligaciones contractuales y las políticas corporativas que se aplican a los datos de sus clientes. A partir de ahí, los datos se pueden clasificar aplicando las etiquetas de uso de datos adecuadas y su uso se puede controlar mediante la definición de políticas de uso de datos.

El marco de trabajo de control de datos simplifica y optimiza el proceso de categorización de datos y creación de políticas de uso de datos a través de la [!DNL Experience Platform] interfaz de usuario y [!DNL Policy Service] API.

**Nuevas funciones**

| Función | Descripción |
| -----------| ---------- |
| Administrar las políticas de uso de datos en la IU | Ahora, las políticas de uso de datos se pueden administrar dentro del **Políticas** workspace en [!DNL Experience Platform] IU. Consulte la [guía del usuario de directivas](../../data-governance/policies/user-guide.md) para obtener más información. |

**Problemas conocidos**

* Ninguna.

Para obtener más información, consulte la [Resumen de gobernanza de datos](../../data-governance/home.md).


## Destinos {#destinations}

Entrada [Real-time Customer Data Platform](../../rtcdp/overview.md), los destinos son integraciones prediseñadas con plataformas de destino que activan los datos a dichos socios de forma fluida.

**Nuevos destinos**

Real-Time CDP ahora admite la activación de datos en más de cincuenta [!DNL Experience Cloud Launch] extensiones, lo que permite realizar análisis, personalizaciones y otros casos de uso. Consulte a continuación para obtener más información:

| Documentación | Descripción |
|--- | ---|
| [Tipos y categorías de destino](../../destinations/destination-types.md) | En este artículo se explica la diferencia entre conexiones y extensiones en la interfaz de Real-Time CDP y se recomienda cuándo utilizar cada uno de estos destinos. |
| [Extensiones de Experience Platform Launch](../../destinations/catalog/launch-extensions/overview.md) | Esta página explica lo que [!DNL Launch] las extensiones son, enumera casos de uso para y establece vínculos a la documentación de cada una [!DNL Launch] en Real-Time CDP. |

Para obtener más información, consulte la [Resumen de destinos](../../destinations/home.md).

## [!DNL Privacy Service] {#privacy}

Las nuevas regulaciones legales y organizativas otorgan a los usuarios el derecho de acceder o eliminar sus datos personales de sus almacenes de datos si así lo solicitan. Adobe Experience Platform [!DNL Privacy Service] proporciona una API de RESTful y una interfaz de usuario para ayudarle a administrar estas solicitudes de datos de sus clientes. Con [!DNL Privacy Service], puede enviar solicitudes para acceder a datos de clientes privados o personales y eliminarlos de aplicaciones de Adobe Experience Cloud, lo que facilita el cumplimiento automatizado de las regulaciones de privacidad legales y organizativas.

**Nuevas funciones**

| Función | Descripción |
| --- | --- |
| Compatibilidad con PDPA | Ahora, las solicitudes de privacidad se pueden crear y rastrear según la Ley de Protección de Datos Personales (PDPA) en Tailandia. Al realizar solicitudes de privacidad en la API, la variable `regulation` la matriz acepta el valor &quot;pdpa_tha&quot;. |
| Tipos de área de nombres en la IU | Ahora puede especificar diferentes tipos de áreas de nombres en el Generador de solicitudes en la variable [!DNL Privacy Service] IU. Consulte la [guía del usuario](../../privacy-service/ui/user-guide.md) para obtener más información. |
| Obsolescencia del punto final anterior | El antiguo extremo de la API (`data/privacy/gdpr`) se ha desaprobado. |

Problemas conocidos

* Ninguna

Para obtener más información acerca de [!DNL Privacy Service], empiece leyendo el [Introducción al Privacy Service](../../privacy-service/home.md).

## Fuentes {#sources}

Adobe Experience Platform puede introducir datos de fuentes externas, al tiempo que le permite estructurar, etiquetar y mejorar esos datos mediante [!DNL Platform] servicios. Puede introducir datos de una variedad de fuentes, como aplicaciones de Adobe, almacenamiento basado en la nube, software de terceros y su sistema CRM.

[!DNL Experience Platform] proporciona una API RESTful y una interfaz de usuario interactiva que le permite configurar conexiones de origen para varios proveedores de datos con facilidad. Estas conexiones de origen le permiten autenticarse y conectarse a sistemas de almacenamiento externos y servicios CRM, establecer tiempos para ejecuciones de ingesta y administrar el rendimiento de ingesta de datos.

**Nuevas funciones**

| Función | Descripción |
| ------- | ----------- |
| Compatibilidad de API e IU con bases de datos | Nuevos conectores de origen para [!DNL Apache Spark] (en HDInsights), [!DNL Azure Synapse Analytics], [!DNL Azure Table Storage], [!DNL Hive] (en HDInsights), y [!DNL Phoenix]. |
| Compatibilidad con API e IU para aplicaciones basadas en pagos | Nuevos conectores de origen para [!DNL PayPal]. |
| Compatibilidad con API e IU para aplicaciones basadas en protocolos | Nuevos conectores de origen para [!DNL Generic OData]. |

**Problemas conocidos**

* Ninguna

Para obtener más información sobre las fuentes, consulte la [información general de orígenes](../../sources/home.md).
