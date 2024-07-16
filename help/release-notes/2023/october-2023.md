---
title: Notas de la versión de Adobe Experience Platform
description: Las notas de la versión de octubre de 2023 de Adobe Experience Platform.
exl-id: e9cf5299-8350-4b40-8f56-05e598846875
source-git-commit: f2d0848952902d94b441566da677ef174518192e
workflow-type: tm+mt
source-wordcount: '1052'
ht-degree: 32%

---

# Notas de la versión de Adobe Experience Platform

**Fecha de la versión: 25 de octubre de 2023**

Actualizaciones de funciones existentes en Experience Platform:

- [Paneles](#dashboards)
- [Recopilación de datos](#data-collection)
- [Destinos](#destinations)
- [Zonas protegidas](#sandboxes)
- [Servicio de segmentación](#segmentation)
- [Fuentes](#sources)

## Paneles {#dashboards}

Adobe Experience Platform proporciona varios paneles a través de los cuales puede ver información importante acerca de los datos de su organización, tal y como se captura durante las instantáneas diarias.

**Funciones nuevas o actualizadas**

| Función | Descripción |
| --- | --- |
| Métricas de uso de destinos | Se han añadido nuevas métricas de medición al panel de uso de licencias. Las métricas **[!UICONTROL Tamaño de Audience Activation]** y **[!UICONTROL Tamaño de exportación de datos]** proporcionan una forma cómoda de rastrear la cantidad de datos que ha exportado fuera de Platform en relación con sus derechos de uso de licencias. Consulte la documentación de [métricas disponibles](../../dashboards/guides/license-usage.md#available-metrics) para obtener descripciones de estas y otras métricas de uso de licencias. |

{style="table-layout:auto"}

Para obtener más información sobre los paneles, incluido cómo conceder permisos de acceso y crear widgets personalizados, comience por leer la [información general sobre paneles](../../dashboards/home.md).

## Recopilación de datos {#data-collection}

Adobe Experience Platform proporciona un conjunto de tecnologías que le permiten recopilar datos de experiencia del cliente del lado del cliente y enviarlos a la red perimetral de Adobe Experience Platform, donde se pueden enriquecer, transformar y distribuir a destinos de Adobe o que no sean de Adobe.

**Funciones nuevas o actualizadas**

| Tipo | Función | Descripción |
| --- | --- | --- |
| Extensiones | Mejora de la API de conversiones [!DNL Meta] | Hay tres mejoras en la extensión [Meta Conversions API](/help/tags/extensions/server/meta/overview.md): <ul><li>Integración con [[!DNL Meta Business Extension (MBE)]](/help/tags/extensions/server/meta/overview.md#integration-with-meta-business-extension-mbe): crea una experiencia de inicio de sesión fluida al permitirle compartir su pixelID y el token de acceso para la integración de la API de conversiones con Adobe.</li><li>Integración con [[!DNL Event Match Quality Score (EMQ)]](/help/tags/extensions/server/meta/overview.md#integration-with-event-quality-match-score-emq): permite enviar publicidad a las personas que tienen más probabilidades de completar una acción deseada y vincular la acción de nuevo a los anuncios enviados.</li><li>Integración con [[!DNL LiveRamp (Alpha)]](/help/tags/extensions/server/meta/overview.md#integration-with-liveramp-alpha): permite pasar el RampID de LiveRamp en el campo Transferencia fácil, lo que elimina la necesidad de compartir PII directamente con socios o Meta. </li></ul> |
| Extensiones | API de conversiones [!DNL LinkedIn] | La extensión de la API [[!DNL LinkedIn] Conversiones](../../tags/extensions/server/linkedin/overview.md) le permite evaluar la efectividad de sus campañas de marketing de LinkedIn reenviando datos de evento del Experience Platform a LinkedIn. |
| Secreto | Secreto de OAuth 2 de [!DNL LinkedIn] | El [[!DNL LinkedIn] Secreto de OAuth 2](../../tags/ui/event-forwarding/secrets.md#linkedin-oauth-2) le permite enviar interacciones servidor-servidor a [!DNL LinkedIn] en el reenvío de eventos. |
| Reenvío de eventos | Actualización de Etiquetas y Reenvío de eventos | Para conservar el rendimiento de [Etiquetas](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=es) y [Reenvío de eventos](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/overview.html) en Platform, solo se conservarán las compilaciones de desarrollo y fase más recientes, tanto las que se realizaron correctamente como las que no se realizaron correctamente. Se eliminarán todas las compilaciones que ya no estén en uso. Además, se han implementado restricciones de limitación de velocidad y limitación de restricción para garantizar que algunos usos intensos de la API no degraden el rendimiento de la API para otros. |
| Extensiones | Elementos, reglas y extensiones | [Los elementos, las reglas y las extensiones](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/overview.html) ahora se ordenan en el resultado de la biblioteca para garantizar una mayor coherencia entre varias compilaciones e implementaciones de la misma biblioteca. |

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
| (Beta) Compatibilidad con funciones hash en campos calculados | Además de las funciones específicas de [exportar matrices](../../destinations/ui/export-arrays-calculated-fields.md) o elementos de una matriz, ahora puede usar [funciones hash](../../destinations/ui/export-arrays-calculated-fields.md#hashing-functions) adicionales para hash atributos en los archivos exportados. Las funciones hash admitidas son: `sha`, `sha256`, `sha512`, `hash`, `md5`, `crc32`. |
| (GA limitado) Activar audiencias de cuenta en ciertos destinos | Los clientes de Real-Time CDP B2B ahora pueden activar [audiencias de cuenta](../../segmentation/ui/account-audiences.md) a ciertos destinos. Para obtener más información acerca de esta característica, lea el [tutorial para activar audiencias de cuenta](/help/destinations/ui/activate-account-audiences.md). |

{style="table-layout:auto"}

**Correcciones y mejoras** {#destinations-fixes-and-enhancements}

Para obtener información más general sobre los destinos, consulte la [información general sobre destinos](../../destinations/home.md).

## Zonas protegidas {#sandboxes}

Adobe Experience Platform está diseñado para enriquecer las aplicaciones de experiencia digital a escala global. Las empresas suelen ejecutar varias aplicaciones de experiencia digital en paralelo y necesitan encargarse del desarrollo, las pruebas y la implementación de estas aplicaciones, a la vez que garantizan el cumplimiento normativo. Para satisfacer esta necesidad, Experience Platform proporciona entornos limitados que dividen una sola instancia de Platform en entornos virtuales independientes para ayudarle a desarrollar aplicaciones de experiencia digital y hacer que evolucionen.

**Nueva funcionalidad**

| Función | Descripción |
| --- | --- |
| Herramientas de zona protegida | La función de herramientas de zona protegida le permite mejorar la precisión de la configuración en todas las zonas protegidas, así como exportar e importar sin problemas configuraciones de zonas protegidas entre zonas protegidas. Puede utilizar la función de herramientas de zona protegida para seleccionar diferentes objetos y exportarlos a un paquete. Para obtener más información, consulte la [guía de la interfaz de usuario de herramientas de zona protegida](../../sandboxes/ui/sandbox-tooling.md). |

Para obtener más información sobre las zonas protegidas, consulte la [descripción general de las zonas protegidas](../../sandboxes/home.md).

## Servicio de segmentación {#segmentation}

[!DNL Segmentation Service] le permite segmentar los datos almacenados en [!DNL Experience Platform] que se relacionan con personas (como clientes, clientes potenciales, usuarios u organizaciones) en públicos. Puede crear públicos a través de definiciones de segmentos u otras fuentes a partir de sus datos de [!DNL Real-Time Customer Profile]. Estos públicos se configuran de forma centralizada y se mantienen en [!DNL Platform] y son fácilmente accesibles desde cualquier solución de Adobe.

**Nueva funcionalidad**

| Función | Descripción |
| ------- | ----------- |
| Audiencias de cuenta (GA limitado) | En Real-time Customer Data Platform B2B Edition, ahora puede utilizar la segmentación de cuentas para ofrecer la total facilidad y sofisticación de la experiencia de segmentación de marketing de audiencias basadas en personas a audiencias basadas en cuentas. Para obtener más información acerca de esta característica, lea la [descripción general de las audiencias de la cuenta](../../segmentation/ui/account-audiences.md). |

Para obtener más información sobre el servicio de segmentación, lea la [descripción general del servicio de segmentación](../../segmentation/home.md).

## Fuentes {#sources}

Experience Platform proporciona una API RESTful y una IU interactiva que le permite configurar conexiones de origen para varios proveedores de datos con facilidad. Estas conexiones de origen le permiten autenticarse y conectarse a sistemas de almacenamiento externos y servicios CRM, establecer tiempos para ejecuciones de ingesta y administrar el rendimiento de ingesta de datos.

**Funciones nuevas o actualizadas**

| Función | Descripción |
| --- | --- |
| Autenticación actualizada para la zona de aterrizaje de datos | Ahora puede ver la fecha de caducidad designada de la zona de aterrizaje de datos al ver sus credenciales. Debe actualizar el token antes de la fecha de caducidad para poder utilizarlo en la aplicación. Si no actualiza manualmente el token antes de la fecha de caducidad indicada, se actualizará automáticamente y proporcionará un nuevo token la próxima vez que recupere las credenciales. Para obtener más información, lea la documentación sobre [usando la zona de aterrizaje de datos](../../sources/tutorials/ui/create/cloud-storage/data-landing-zone.md). |

{style="table-layout:auto"}

Para obtener más información sobre las fuentes, lea [información general de fuentes](../../sources/home.md).
