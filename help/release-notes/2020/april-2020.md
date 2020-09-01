---
title: 'Notas de la versión de Adobe Experience Platform '
description: Notas de la versión del Experience Platform 8 de abril de 2020
doc-type: release notes
last-update: April 13, 2020
author: ens71067
keywords: release notes;
translation-type: tm+mt
source-git-commit: 0f3a4ba6ad96d2226ae5094fa8b5073152df90f7
workflow-type: tm+mt
source-wordcount: '991'
ht-degree: 5%

---


# Notas de la versión de Adobe Experience Platform

**Fecha de publicación: 8 de abril de 2020**

Nuevas funciones de Adobe Experience Platform:
* [[!Servicios inteligentes DNL]](#intelligent)

Actualizaciones de funciones existentes:
* [[!Modelo de datos de experiencia DNL (XDM)]](#xdm)
* [[!Gobierno de datos DNL]](#governance)
* [[!Destinos DNL]](#destinations)
* [[!Privacy Service DNL]](#privacy)
* [[!Fuentes DNL]](#sources)

## [!DNL Intelligent Services] {#intelligent}

[!DNL Intelligent Services] empoderar a los analistas de mercadotecnia y a los profesionales para que aprovechen el poder de la inteligencia artificial y el aprendizaje automático en casos de uso de la experiencia del cliente. Esto permite que los analistas de mercadotecnia configuren predicciones específicas de las necesidades de una compañía mediante configuraciones de nivel empresarial sin necesidad de conocimientos de ciencia de datos. Además, los profesionales de marketing pueden activar predicciones en aplicaciones de Adobe Experience Cloud, Adobe Experience Platform y terceros.

**Funciones principales**

| Función | Descripción |
|---|---|
| [!DNL Customer AI] | [!DNL Customer AI] proporciona a los especialistas en mercadotecnia la capacidad para generar predicciones de clientes a nivel individual con explicaciones. Con la ayuda de factores influyentes, [!DNL Customer AI] puede decirle qué es lo más probable que un cliente haga y por qué. Además, los especialistas en mercadotecnia pueden beneficiarse de [!DNL Customer AI] las predicciones y perspectivas para personalizar las experiencias de los clientes al proporcionar las ofertas y los mensajes más adecuados. |
| [!DNL Attribution AI] | [!DNL Attribution AI] es un servicio de atribución algorítmica de varios canales que calcula la influencia y el impacto incremental de las interacciones de los clientes con respecto a los resultados especificados. Con [!DNL Attribution AI], los especialistas en mercadotecnia pueden medir y optimizar el gasto en mercadotecnia y publicidad al comprender el impacto de cada interacción individual de los clientes en cada fase de los viajes de los clientes. |

**Problemas conocidos**

* Actualmente no hay problemas conocidos.

Para obtener más información [!DNL Intelligent Services] y qué tiene que ver con la oferta, consulte la descripción general [de los servicios](../../intelligent-services/home.md)inteligentes.

## [!DNL Experience Data Model] Sistema (XDM) {#xdm}

La estandarización y la interoperabilidad son conceptos clave que sustentan [!DNL Experience Platform]. [!DNL Experience Data Model] (XDM), impulsado por el Adobe, es un esfuerzo para estandarizar los datos de experiencia del cliente y definir esquemas para la administración de la experiencia del cliente.

XDM es una especificación públicamente documentada diseñada para mejorar el poder de las experiencias digitales. Proporciona estructuras y definiciones comunes para que cualquier aplicación se comunique con los servicios de Adobe Experience Platform. Al cumplir con los estándares XDM, todos los datos de experiencia del cliente se pueden incorporar a una representación común que ofrece perspectivas de una manera más rápida e integrada. Puede obtener perspectivas valiosas de las acciones de los clientes, definir audiencias de clientes a través de segmentos y utilizar atributos de clientes para fines de personalización.

**Nuevas funciones**

| Función | Descripción |
| --- | --- |
| Información de visualización alternativa automática | El [!DNL Schema Registry] aplica automáticamente los valores personalizados de título y descripción configurados en el `alternateDisplayInfo` descriptor. |
| Restricciones de campo escalar | El [!DNL Schema Registry] no permite más de 6000 campos escalares en un solo esquema. |
| Revisión general del rendimiento | El [!DNL Schema Registry] ha sido revisado para cumplir y satisfacer las demandas de [!DNL Experience Platform] mejor. |

**Corrección de errores**

* Se ha actualizado XDM a XED para que admita un formato XED más nítido para campos URI anidados en XDM estándar.

**Problemas conocidos**

* Conocido

## [!DNL Data Governance] {#governance}

Adobe Experience Platform [!DNL Data Governance] es una serie de estrategias y tecnologías que se utilizan para administrar los datos de los clientes y garantizar el cumplimiento de las normativas, restricciones y políticas aplicables al uso de los datos. Desempeña un papel clave en [!DNL Experience Platform] varios niveles, incluyendo catalogación, linaje de datos, etiquetado de uso de datos, políticas de acceso a datos e controles de acceso en datos para acciones de mercadotecnia.

Para comenzar con la administración de datos, es necesario comprender a fondo las regulaciones, las obligaciones contractuales y las políticas corporativas que se aplican a los datos del cliente. Desde allí, los datos pueden clasificarse aplicando las etiquetas de uso de datos correspondientes, y su uso puede controlarse mediante la definición de políticas de uso de datos.

El [!DNL Data Governance] marco simplifica y racionaliza el proceso de categorización de datos y creación de políticas de uso de datos a través de la interfaz de [!DNL Experience Platform] usuario y la [!DNL Policy Service] API.

**Nuevas funciones**

| Función | Descripción |
| -----------| ---------- |
| Administrar directivas de uso de datos en la interfaz de usuario | Las directivas de uso de datos ahora se pueden administrar dentro del espacio de trabajo _Directivas_ de la [!DNL Experience Platform] IU. Consulte la guía del usuario de [directivas](../../data-governance/policies/user-guide.md) para obtener más información. |

**Problemas conocidos**

* None.

Para obtener más información, consulte la información general [sobre el Gobierno](../../data-governance/home.md)de datos.


## Destinos {#destinations}

En la plataforma [de datos del cliente en tiempo real de](../../rtcdp/overview.md)Adobe, los destinos son integraciones prediseñadas con plataformas de destino que activan los datos a dichos socios de forma transparente.

**Nuevos destinos**

Adobe Real-time CDP ahora admite la activación de datos a más de cincuenta [!DNL Experience Cloud Launch] extensiones, lo que permite análisis, personalización y otros casos de uso. Consulte a continuación los detalles:

| Documentación | Descripción |
|--- | ---|
| [Tipos y categorías de destino](/help/rtcdp/destinations/destination-types.md) | Este artículo explica la diferencia entre las conexiones y las extensiones en la interfaz CDP en tiempo real de Adobe y recomienda cuándo usar cada uno de estos destinos. |
| [Extensiones de Experience Platform Launch](/help/rtcdp/destinations/experience-platform-launch-extensions.md) | Esta página explica cuáles son las extensiones, las listas utilizan casos para utilizarlas y los vínculos a la documentación de cada [!DNL Launch] [!DNL Launch] extensión en Adobe Real-time CDP. |

Para obtener más información, consulte la información general sobre [los destinos](/help/rtcdp/destinations/destinations-overview.md).

## [!DNL Privacy Service] {#privacy}

Las nuevas regulaciones legales y organizativas otorgan a los usuarios el derecho de acceder a sus datos personales o eliminarlos de sus almacenes de datos si así lo solicitan. Adobe Experience Platform [!DNL Privacy Service] proporciona una API RESTful y una interfaz de usuario para ayudarle a administrar estas solicitudes de datos de sus clientes. Con [!DNL Privacy Service], puede enviar solicitudes para acceder y eliminar datos personales o privados de clientes desde las aplicaciones de Adobe Experience Cloud, lo que facilita el cumplimiento automatizado de las normativas legales y de privacidad de la organización.

**Nuevas funciones**

| Función | Descripción |
| --- | --- |
| Compatibilidad con PDPA | Las solicitudes de privacidad ahora se pueden crear y rastrear bajo la Ley de Protección de Datos Personales (PDPA) en Tailandia. Al realizar solicitudes de privacidad en la API, la `regulation` matriz acepta el valor &quot;pdpa_tha&quot;. |
| Tipos de Área de nombres en la interfaz de usuario | Ahora puede especificar diferentes tipos de Área de nombres en el Creador de solicitudes en la [!DNL Privacy Service] interfaz de usuario. Consulte la guía [del](../../privacy-service/ui/user-guide.md) usuario para obtener más información. |
| Desuso de punto final antiguo | El punto final (`data/privacy/gdpr`) de la API anterior ha quedado obsoleto. |

Problemas conocidos

* None

Para obtener más información sobre [!DNL Privacy Service], lea la descripción general [del](../../privacy-service/home.md)Privacy Service y inicio.

## Fuentes {#sources}

Adobe Experience Platform puede ingerir datos de fuentes externas y, al mismo tiempo, puede estructurarlos, etiquetarlos y mejorarlos mediante [!DNL Platform] servicios. Puede ingestar datos de una variedad de fuentes, como aplicaciones de Adobe, almacenamiento basado en la nube, software de terceros y su sistema CRM.

[!DNL Experience Platform] proporciona una API RESTful y una interfaz de usuario interactiva que le permite configurar fácilmente las conexiones de origen para varios proveedores de datos. Estas conexiones de origen le permiten autenticarse y conectarse a sistemas de almacenamiento externos y servicios CRM, establecer tiempos para ejecuciones de ingestión y administrar el rendimiento de la ingesta de datos.

**Nuevas funciones**

| Función | Descripción |
| ------- | ----------- |
| Compatibilidad de API e interfaz de usuario con bases de datos | Nuevos conectores de origen para [!DNL Apache Spark] (en HDInsights), [!DNL Azure Synapse Analytics], [!DNL Azure Table Storage], [!DNL Hive] (en HDInsights) y [!DNL Phoenix]. |
| Compatibilidad de API e interfaz de usuario para aplicaciones basadas en pagos | Conectores de origen nuevos para [!DNL PayPal]. |
| Compatibilidad de API e interfaz de usuario para aplicaciones basadas en protocolos | Conectores de origen nuevos para [!DNL Generic OData]. |

**Problemas conocidos**

* None

Para obtener más información sobre las fuentes, consulte la descripción general [de](../../sources/home.md)las fuentes.
