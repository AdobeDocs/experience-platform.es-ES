---
title: Notas de la versión de Adobe Experience Platform, abril de 2020
description: Notas de la versión de abril de 2020 para Adobe Experience Platform.
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
* [Gobierno de datos](#governance)
* [[!DNL Destinations]](#destinations)
* [[!DNL Privacy Service]](#privacy)
* [[!DNL Sources]](#sources)

## [!DNL Intelligent Services] {#intelligent}

[!DNL Intelligent Services] faculte a los analistas y profesionales de marketing para aprovechar el poder de la inteligencia artificial y el aprendizaje automático en casos de uso de experiencias del cliente. Esto permite que los analistas de marketing configuren predicciones específicas de las necesidades de una empresa mediante configuraciones de nivel empresarial sin necesidad de experiencia en ciencia de datos. Además, los profesionales de marketing pueden activar las predicciones en Adobe Experience Cloud, Adobe Experience Platform y aplicaciones de terceros.

**Funciones principales**

| Función | Descripción |
|---|---|
| [!DNL Customer AI] | [!DNL Customer AI] proporciona a los especialistas en marketing la capacidad para generar predicciones de clientes a nivel individual con explicaciones. Con la ayuda de factores influyentes, [!DNL Customer AI] puede indicarle lo que un cliente probablemente haga y por qué. Además, los especialistas en marketing pueden beneficiarse de [!DNL Customer AI] predicciones y perspectivas para personalizar las experiencias de los clientes al ofrecer las ofertas y los mensajes más adecuados. |
| [!DNL Attribution AI] | [!DNL Attribution AI] es un servicio de atribución algorítmica de varios canales que calcula la influencia y el impacto incremental de las interacciones de los clientes con los resultados especificados. Con [!DNL Attribution AI], los especialistas en marketing pueden medir y optimizar el gasto en marketing y publicidad al comprender el impacto de cada interacción individual con los clientes en cada fase de los recorridos de los clientes. |

**Problemas conocidos**

* Actualmente no hay problemas conocidos.

Para obtener más información, consulte [!DNL Intelligent Services] y lo que tiene que ofrecer, consulte la [Resumen de servicios inteligentes](../../intelligent-services/home.md).

## [!DNL Experience Data Model] Sistema (XDM) {#xdm}

La estandarización y la interoperabilidad son conceptos clave [!DNL Experience Platform]. [!DNL Experience Data Model] (XDM), impulsado por el Adobe, es un esfuerzo para estandarizar los datos de experiencia del cliente y definir esquemas para la administración de experiencias del cliente.

XDM es una especificación públicamente documentada diseñada para mejorar el poder de las experiencias digitales. Proporciona estructuras y definiciones comunes para que cualquier aplicación se comunique con los servicios de Adobe Experience Platform. Al cumplir con los estándares XDM, todos los datos de experiencia del cliente se pueden incorporar a una representación común que ofrezca perspectivas de una manera más rápida e integrada. Puede obtener perspectivas valiosas a partir de las acciones de los clientes, definir audiencias de clientes a través de segmentos y utilizar atributos de clientes con fines de personalización.

**Nuevas funciones**

| Función | Descripción |
| --- | --- |
| Información de visualización alternativa automática | La variable [!DNL Schema Registry] aplica automáticamente los valores de título y descripción personalizados configurados en la variable `alternateDisplayInfo` descriptor. |
| Restricciones del campo escalar | La variable [!DNL Schema Registry] no permite más de 6000 campos escalares en un solo esquema. |
| Revisión general del rendimiento | La variable [!DNL Schema Registry] se ha revisado para que cumpla las exigencias de [!DNL Experience Platform] mejor. |

**Corrección de errores**

* XDM actualizado a XED convertido para admitir un formato XED más limpio para campos URI anidados en XDM estándar.

**Problemas conocidos**

* Conocido

## Gobierno de datos {#governance}

Administración de datos de Adobe Experience Platform es una serie de estrategias y tecnologías que se utilizan para administrar los datos de los clientes y garantizar el cumplimiento de las normativas, restricciones y políticas aplicables al uso de los datos. Desempeña un papel clave en [!DNL Experience Platform] en varios niveles, incluida la catalogación, el linaje de datos, el etiquetado del uso de datos, las políticas de acceso a datos y el control de acceso a los datos para las acciones de marketing.

Para comenzar con el control de datos es necesario comprender a fondo las regulaciones, las obligaciones contractuales y las políticas corporativas que se aplican a los datos de sus clientes. A partir de ahí, los datos se pueden clasificar aplicando las etiquetas de uso de datos apropiadas, y su uso se puede controlar mediante la definición de políticas de uso de datos.

El marco de control de datos simplifica y optimiza el proceso de categorización de datos y creación de políticas de uso de datos a través del [!DNL Experience Platform] interfaz de usuario y [!DNL Policy Service] API.

**Nuevas funciones**

| Función | Descripción |
| -----------| ---------- |
| Administrar políticas de uso de datos en la interfaz de usuario | Ahora, las políticas de uso de datos se pueden administrar dentro de la variable **Políticas** espacio de trabajo [!DNL Experience Platform] IU. Consulte la [guía del usuario de directivas](../../data-governance/policies/user-guide.md) para obtener más información. |

**Problemas conocidos**

* Ninguna.

Para obtener más información, consulte la [Información general sobre la administración de datos](../../data-governance/home.md).


## Destinos {#destinations}

En [Real-time Customer Data Platform](../../rtcdp/overview.md), los destinos son integraciones prediseñadas con plataformas de destino que activan los datos para esos socios de una manera sencilla.

**Nuevos destinos**

Real-Time CDP ahora admite la activación de datos a más de cincuenta [!DNL Experience Cloud Launch] , habilitando analytics, personalización y otros casos de uso. Consulte a continuación los detalles:

| Documentación | Descripción |
|--- | ---|
| [Tipos y categorías de destino](../../destinations/destination-types.md) | Este artículo explica la diferencia entre las conexiones y las extensiones en la interfaz de Real-Time CDP y recomienda cuándo utilizar cada uno de estos destinos. |
| [extensiones de Experience Platform Launch](../../destinations/catalog/launch-extensions/overview.md) | Esta página explica qué [!DNL Launch] son las extensiones, listas casos de uso para utilizarlas y vínculos a documentación para cada [!DNL Launch] en Real-Time CDP. |

Para obtener más información, consulte la [Información general sobre destinos](../../destinations/home.md).

## [!DNL Privacy Service] {#privacy}

Las nuevas regulaciones legales y organizativas otorgan a los usuarios el derecho de acceder o eliminar sus datos personales de sus almacenes de datos si así lo solicitan. Adobe Experience Platform [!DNL Privacy Service] proporciona una API de RESTful y una interfaz de usuario para ayudarle a administrar estas solicitudes de datos de sus clientes. con [!DNL Privacy Service], puede enviar solicitudes para acceder y eliminar datos de clientes personales o privados de aplicaciones de Adobe Experience Cloud, lo que facilita el cumplimiento automatizado de las normas de privacidad legales y organizativas.

**Nuevas funciones**

| Función | Descripción |
| --- | --- |
| Compatibilidad con PDPA | Las solicitudes de privacidad ahora se pueden crear y rastrear bajo la Ley de Protección de Datos Personales (PDPA) en Tailandia. Al realizar solicitudes de privacidad en la API, la variable `regulation` array acepta el valor &quot;pdpa_tha&quot;. |
| Tipos de área de nombres en la interfaz de usuario | Ahora puede especificar diferentes tipos de área de nombres en el Creador de solicitudes en el [!DNL Privacy Service] IU. Consulte la [guía del usuario](../../privacy-service/ui/user-guide.md) para obtener más información. |
| Desaprobación de punto final antiguo | El antiguo extremo de la API (`data/privacy/gdpr`) está en desuso. |

Problemas conocidos

* Ninguna

Para obtener más información, consulte [!DNL Privacy Service], empiece leyendo el [Información general del Privacy Service](../../privacy-service/home.md).

## Fuentes {#sources}

Adobe Experience Platform puede ingerir datos de fuentes externas y, al mismo tiempo, permitirle estructurarlos, etiquetarlos y mejorarlos mediante [!DNL Platform] servicios. Puede ingerir datos de una variedad de fuentes, como aplicaciones de Adobe, almacenamiento basado en la nube, software de terceros y su sistema CRM.

[!DNL Experience Platform] proporciona una API de RESTful y una interfaz de usuario interactiva que le permite configurar conexiones de origen para varios proveedores de datos con facilidad. Estas conexiones de origen le permiten autenticarse y conectarse a sistemas de almacenamiento externos y servicios CRM, establecer tiempos para ejecutar la ingesta y administrar el rendimiento de ingesta de datos.

**Nuevas funciones**

| Función | Descripción |
| ------- | ----------- |
| Compatibilidad de API e IU con bases de datos | Nuevos conectores de origen para [!DNL Apache Spark] (en HDInsights), [!DNL Azure Synapse Analytics], [!DNL Azure Table Storage], [!DNL Hive] (en HDInsights), y [!DNL Phoenix]. |
| Compatibilidad de API y IU para aplicaciones basadas en pagos | Nuevos conectores de origen para [!DNL PayPal]. |
| Compatibilidad de API y IU para aplicaciones basadas en protocolos | Nuevos conectores de origen para [!DNL Generic OData]. |

**Problemas conocidos**

* Ninguna

Para obtener más información sobre las fuentes, consulte la [información general sobre fuentes](../../sources/home.md).
