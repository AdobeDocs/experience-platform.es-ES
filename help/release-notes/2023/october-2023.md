---
title: Notas de la versión de Adobe Experience Platform
description: Las notas de la versión de octubre de 2023 para Adobe Experience Platform.
source-git-commit: 9009f56956f0719fb80d423a14b81a6dc7115d77
workflow-type: tm+mt
source-wordcount: '808'
ht-degree: 34%

---

# Notas de la versión de Adobe Experience Platform

**Fecha de la versión: 25 de octubre de 2023**

Actualizaciones de las funciones existentes en Experience Platform:

- [Recopilación de datos](#data-collection)
- [Destinos](#destinations)
- [Zonas protegidas](#sandboxes)
- [Servicio de segmentación](#segmentation)
- [Fuentes](#sources)

## Recopilación de datos {#data-collection}

Adobe Experience Platform proporciona un conjunto de tecnologías que le permiten recopilar datos de experiencia del cliente del lado del cliente y enviarlos a la red perimetral de Adobe Experience Platform, donde se pueden enriquecer, transformar y distribuir a destinos de Adobe o que no sean de Adobe.

**Funciones nuevas o actualizadas**

| Tipo | Función | Descripción |
| --- | --- | --- |
| Extensión | [!DNL Meta] Mejora de API de conversiones | Se han realizado tres mejoras en [API de metaconversiones](/help/tags/extensions/server/meta/overview.md) extensión: <ul><li>Integración con [[!DNL Meta Business Extension (MBE)]](/help/tags/extensions/server/meta/overview.md#integration-with-meta-business-extension-mbe): crea una experiencia de inicio de sesión perfecta, ya que le permite compartir su pixelID y el token de acceso para la integración de la API de conversiones con Adobe.</li><li>Integración con [[!DNL Event Match Quality Score (EMQ)]](/help/tags/extensions/server/meta/overview.md#integration-with-event-quality-match-score-emq): Permite enviar publicidad a las personas que tienen más probabilidades de completar una acción deseada y vincular la acción de nuevo a los anuncios enviados.</li><li>Integración con [[!DNL LiveRamp (Alpha)]](/help/tags/extensions/server/meta/overview.md#integration-with-liveramp-alpha): Permite pasar el RampID de LiveRamp en el campo CIP, lo que elimina la necesidad de compartir PII directamente con socios o Meta. </li></ul> |
| Extensión | [!DNL LinkedIn] API de conversiones | El [[!DNL LinkedIn] API de conversiones](../../tags/extensions/server/linkedin/overview.md) Esta extensión le permite evaluar la eficacia de sus campañas de marketing de LinkedIn reenviando datos de evento del Experience Platform a LinkedIn. |
| Secreto | [!DNL LinkedIn] Secreto de OAuth 2 | El [[!DNL LinkedIn] Secreto de OAuth 2](../../tags/ui/event-forwarding/secrets.md#linkedin-oauth-2) permite enviar interacciones servidor-servidor a [!DNL LinkedIn] en el reenvío de eventos. |

Para obtener más información sobre la recopilación de datos, lea la [Información general sobre recopilación de datos](../../tags/home.md).

## Destinos {#destinations}

[!DNL Destinations] son integraciones generadas previamente con plataformas de destino que permiten la activación perfecta de datos de Adobe Experience Platform. Puede utilizar los destinos para activar los datos conocidos y desconocidos para campañas de marketing entre canales, campañas por correo electrónico, publicidad segmentada y muchos otros casos de uso.

**Destinos nuevos o actualizados** {#new-updated-destinations}

| Destino | Nuevo o actualizado | Descripción |
| ----------- |----------------|----------- |
| [[!DNL MoEngage]](/help/destinations/catalog/mobile-engagement/moengage.md) | Nuevo | Utilice el destino Moengage para conectar y asignar los datos de Adobe (atributos de usuario, segmentos y eventos) a MoEngage en tiempo real. A continuación, los clientes pueden actuar sobre estos datos y ofrecer experiencias personalizadas y específicas. |
| [[!DNL Qualtrics Automations]](/help/destinations/catalog/survey/qualtrics-automations.md) | Nuevo | Utilice la agregación de varias fuentes de datos operativos en Adobe Experience Platform como entrada en el ID de experiencia de Qualtrics para comprender mejor a sus clientes y permitir que el alcance dirigido cierre la brecha cuando se trata de comprender los impulsores de la intención, la emoción y la experiencia. |

{style="table-layout:auto"}

**Funcionalidad nueva o actualizada** {#destinations-new-updated-functionality}

| Funcionalidad | Descripción |
| ----------- | ----------- |
| Compatibilidad con funciones hash en campos calculados | Además de las funciones específicas de [exportación de matrices](../../destinations/ui/export-arrays-calculated-fields.md) Para los elementos de una matriz, ahora puede utilizar [funciones hash](../../destinations/ui/export-arrays-calculated-fields.md#hashing-functions) para crear atributos hash en los archivos exportados. Las funciones hash admitidas son: `sha`, `sha256`, `sha512`, `hash`, `md5`, `crc32`. |

{style="table-layout:auto"}

**Correcciones y mejoras** {#destinations-fixes-and-enhancements}

Para obtener información más general sobre los destinos, consulte la [información general sobre destinos](../../destinations/home.md).

## Zonas protegidas {#sandboxes}

Adobe Experience Platform está diseñado para enriquecer las aplicaciones de experiencia digital a escala global. Las empresas suelen ejecutar varias aplicaciones de experiencia digital en paralelo y necesitan encargarse del desarrollo, las pruebas y la implementación de estas aplicaciones, a la vez que garantizan el cumplimiento normativo. Para satisfacer esta necesidad, Experience Platform proporciona entornos limitados que dividen una sola instancia de Platform en entornos virtuales independientes para ayudarle a desarrollar aplicaciones de experiencia digital y hacer que evolucionen.

**Nueva funcionalidad**

| Función | Descripción |
| --- | --- |
| Herramientas de espacio aislado | La función de herramientas de zona protegida le permite mejorar la precisión de la configuración en todas las zonas protegidas, así como exportar e importar sin problemas configuraciones de zonas protegidas entre zonas protegidas. Puede utilizar la función de herramientas de zona protegida para seleccionar diferentes objetos y exportarlos a un paquete. Para obtener más información, consulte la [guía de IU de herramientas de zona protegida](../../sandboxes/ui/sandbox-tooling.md). |

Para obtener más información sobre los entornos limitados, consulte la [información general sobre zonas protegidas](../../sandboxes/home.md).

## Servicio de segmentación {#segmentation}

[!DNL Segmentation Service] le permite segmentar los datos almacenados en [!DNL Experience Platform] que se relacionan con personas (como clientes, clientes potenciales, usuarios u organizaciones) en públicos. Puede crear públicos a través de definiciones de segmentos u otras fuentes a partir de sus datos de [!DNL Real-Time Customer Profile]. Estos públicos se configuran de forma centralizada y se mantienen en [!DNL Platform] y son fácilmente accesibles desde cualquier solución de Adobe.

**Nueva funcionalidad**

| Función | Descripción |
| ------- | ----------- |
| Audiencias de cuenta (GA limitado) | En Real-time Customer Data Platform B2B Edition, ahora puede utilizar la segmentación de cuentas para ofrecer la total facilidad y sofisticación de la experiencia de segmentación de marketing de audiencias basadas en personas a audiencias basadas en cuentas. Para obtener más información acerca de esta funcionalidad, lea la [resumen de audiencias de cuenta](../../segmentation/ui/account-audiences.md). |

Para obtener más información sobre el servicio de segmentación, lea la [Resumen del servicio de segmentación](../../segmentation/home.md).

## Fuentes {#sources}

Experience Platform proporciona una API RESTful y una IU interactiva que le permite configurar conexiones de origen para varios proveedores de datos con facilidad. Estas conexiones de origen le permiten autenticarse y conectarse a sistemas de almacenamiento externos y servicios CRM, establecer tiempos para ejecuciones de ingesta y administrar el rendimiento de ingesta de datos.

**Funciones nuevas o actualizadas**

| Función | Descripción |
| --- | --- |
| Autenticación actualizada para la zona de aterrizaje de datos | Ahora puede ver la fecha de caducidad designada de la zona de aterrizaje de datos al ver sus credenciales. Debe actualizar el token antes de la fecha de caducidad para poder utilizarlo en la aplicación. Si no actualiza manualmente el token antes de la fecha de caducidad indicada, se actualizará automáticamente y proporcionará un nuevo token la próxima vez que recupere las credenciales. Para obtener más información, lea la documentación sobre [uso de la zona de aterrizaje de datos](../../sources/tutorials/ui/create/cloud-storage/data-landing-zone.md). |

{style="table-layout:auto"}

Para obtener más información sobre las fuentes, lea la [información general de orígenes](../../sources/home.md).
