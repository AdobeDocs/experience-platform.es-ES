---
title: Notas de la versión de Adobe Experience Platform
description: Las notas de la versión de octubre de 2023 para Adobe Experience Platform.
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: 4ab89ef7cabc9d808fd9dab24b6dbe3fe23e53f3
workflow-type: tm+mt
source-wordcount: '577'
ht-degree: 35%

---

# Notas de la versión de Adobe Experience Platform

**Fecha de la versión: 25 de octubre de 2023**

Actualizaciones de las funciones existentes en Experience Platform:

- [Recopilación de datos](#data-collection)
- [Zonas protegidas](#sandboxes)
- [Servicio de segmentación](#segmentation)
- [Fuentes](#sources)

## Recopilación de datos {#data-collection}

Adobe Experience Platform proporciona un conjunto de tecnologías que le permiten recopilar datos de experiencia del cliente del lado del cliente y enviarlos a la red perimetral de Adobe Experience Platform, donde se pueden enriquecer, transformar y distribuir a destinos de Adobe o que no sean de Adobe.

**Funciones nuevas o actualizadas**

| Tipo | Función | Descripción |
| --- | --- | --- |
| Extensión | [!DNL Meta] Mejora de API de conversiones | Se han realizado tres mejoras en [API de metaconversiones](/help/tags/extensions/server/meta/overview.md) extensión: <ul><li>Integración con [[!DNL Meta Business Extension (MBE)]](/help/tags/extensions/server/meta/overview.md#integration-with-meta-business-extension-mbe): crea una experiencia de inicio de sesión perfecta, ya que le permite compartir su pixelID y el token de acceso para la integración de la API de conversiones con Adobe.</li><li>Integración con [[!DNL Event Match Quality Score (EMQ)]](/help/tags/extensions/server/meta/overview.md#integration-with-event-quality-match-score-emq): Permite enviar publicidad a las personas que tienen más probabilidades de completar una acción deseada y vincular la acción de nuevo a los anuncios enviados.</li><li>Integración con [[!DNL LiveRamp (Alpha)]](/help/tags/extensions/server/meta/overview.md#integration-with-liveramp-alpha): Permite pasar el RampID de LiveRamp en el campo CIP, lo que elimina la necesidad de compartir PII directamente con socios o Meta. </li></ul> |

Para obtener más información sobre la recopilación de datos, lea la [Información general sobre recopilación de datos](../../tags/home.md).

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
