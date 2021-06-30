---
title: Notas de la versión de Adobe Experience Platform
description: Notas de la versión del Experience Platform para el 30 de junio de 2021.
doc-type: release notes
last-update: June 30, 2021
author: ens60013
exl-id: 8f2c9bf8-1487-46e4-993b-bd9b63774cab
source-git-commit: fc916f87bf07e5eabf7d1681059406e2fea362e0
workflow-type: tm+mt
source-wordcount: '530'
ht-degree: 6%

---


# Notas de la versión de Adobe Experience Platform

**Fecha de publicación: 30 de junio de 2021**

Actualizaciones de funciones existentes en Adobe Experience Platform:

- [Perfil del cliente en tiempo real](#profile)
- [Entornos aislados](#sandboxes)
- [Fuentes](#sources)

## Perfil del cliente en tiempo real {#profile}

Adobe Experience Platform le permite ofrecer experiencias coordinadas, coherentes y relevantes a sus clientes, independientemente de dónde o cuándo interactúen con su marca. Con Perfil del cliente en tiempo real, puede ver una vista holística de cada cliente individual que combina datos de varios canales, incluidos datos en línea, sin conexión, CRM y de terceros. [!DNL Profile] le permite consolidar los datos de los clientes en una vista unificada, que ofrece una cuenta procesable con marca de tiempo de cada interacción con los clientes.

| Función | Descripción |
| ------- | ----------- |
| Combinar actualizaciones del flujo de trabajo de directivas | Al crear y actualizar políticas de combinación en la interfaz de usuario, los usuarios ahora pueden obtener una vista previa de 20 perfiles de muestra basados en el esquema de unión. Esto permite a los usuarios obtener una vista previa del aspecto que tendrán los perfiles de cliente antes de guardar las configuraciones de directivas de combinación. Para obtener más información, consulte la [guía de interfaz de usuario de políticas de combinación](../../profile/merge-policies/ui-guide.md). |
| Informe de superposición de identidad | El informe de superposición de identidad forma parte de la API del perfil del cliente en tiempo real y proporciona visibilidad sobre la composición del almacén de perfiles. Con el extremo `/previewsamplestatus` , el informe de superposición de identidad expone las identidades que más contribuyen a la audiencia a la que se puede dirigir. Para obtener más información, visite la [vista previa de la guía de extremo de la API de estado de muestra](../../profile/api/preview-sample-status.md). |

Para obtener más información sobre el Perfil del cliente en tiempo real, incluidos tutoriales y prácticas recomendadas para trabajar con datos [!DNL Profile], lea en primer lugar la [información general del Perfil del cliente en tiempo real](../../profile/home.md).

## Entornos aislados {#sandboxes}

Adobe Experience Platform está diseñado para enriquecer las aplicaciones de experiencia digital a escala global. A menudo, las empresas ejecutan varias aplicaciones de experiencia digital en paralelo y deben encargarse del desarrollo, las pruebas y la implementación de estas aplicaciones, asegurando al mismo tiempo el cumplimiento de las normas operacionales. Para satisfacer esta necesidad, Experience Platform proporciona entornos limitados que dividen una sola instancia de Platform en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

| Función | Descripción |
| ------- | ----------- |
| Mejoras en el restablecimiento del entorno limitado de producción | Ahora puede restablecer los entornos limitados de producción que se utilizan para el uso compartido bidireccional de segmentos con Adobe Audience Manager o el servicio principal de audiencia. Esto se puede hacer desde la interfaz de usuario o utilizando los nuevos parámetros `validationOnly` y `ignoreWarnings` en la API. Para obtener más información, consulte los tutoriales sobre [cómo restablecer un simulador de pruebas en la interfaz de usuario](../../sandboxes/ui/user-guide.md) y [cómo restablecer un simulador de pruebas en la API](../../sandboxes/api/sandboxes.md). |

## Fuentes {#sources}

Adobe Experience Platform puede ingerir datos de fuentes externas, al mismo tiempo que le permite estructurarlos, etiquetarlos y mejorarlos mediante los servicios de Platform. Puede ingerir datos de una variedad de fuentes, como aplicaciones de Adobe, almacenamiento basado en la nube, software de terceros y su sistema CRM.

Experience Platform proporciona una API de RESTful y una interfaz de usuario interactiva que le permite configurar conexiones de origen para varios proveedores de datos con facilidad. Estas conexiones de origen le permiten autenticarse y conectarse a sistemas de almacenamiento externos y servicios CRM, establecer tiempos para ejecutar la ingesta y administrar el rendimiento de ingesta de datos.

| Función | Descripción |
| ------- | ----------- |
| [!DNL Veeva CRM] (Beta) | Ahora puede conectar [!DNL Veeva CRM] al Experience Platform mediante la API [!DNL Flow Service] o la interfaz de usuario. Consulte la [[!DNL Veeva CRM] descripción general del conector](../../sources/connectors/crm/veeva.md) para obtener más información. |
| Compatibilidad con la monitorización de flujos de datos de flujo continuo | Ahora puede utilizar el espacio de trabajo de la IU de fuentes para supervisar las actividades de consumo de datos de fuentes de flujo continuo con las métricas y el estado correspondientes. Consulte el tutorial sobre [monitorización de flujos de datos de flujo continuo](../../sources/tutorials/ui/monitor-streaming.md) para obtener más información. |

Para obtener más información sobre las fuentes, consulte [sources overview](../../sources/home.md).
