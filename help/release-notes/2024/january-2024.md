---
title: Notas de la versión de Adobe Experience Platform, enero de 2024
description: Las notas de la versión de enero de 2024 de Adobe Experience Platform.
exl-id: d4b3c5b2-3adb-41fd-91ad-f4c0f21d2325
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1662'
ht-degree: 95%

---

# Notas de la versión de Adobe Experience Platform

**Fecha de la versión: 30 de enero de 2024**

Nuevas funciones de Adobe Experience Platform:

- [Manuales de tácticas de casos de uso](#use-case-playbooks)

Actualizaciones de funciones existentes en Experience Platform:

- [Control de acceso basado en atributos](#abac)
- [Preparación de los datos](#data-prep)
- [Paneles](#dashboards)
- [Destinos](#destinations)
- [Servicio de identidad](#identity-service)
- [Real-Time Customer Data Platform](#rtcdp)
- [Perfil del cliente en tiempo real](#profile)
- [Servicio de segmentación](#segmentation)
- [Fuentes](#sources)

## Manuales de tácticas de casos de uso {#use-case-playbooks}

La funcionalidad [!UICONTROL Manuales de tácticas de casos de uso] ya está disponible de forma general para todos los clientes de Real-Time CDP y Adobe Journey Optimizer. Los [!UICONTROL manuales de tácticas de casos de uso] están diseñados para ayudar a los usuarios a superar los desafíos al comenzar con Real-time Customer Data Platform o Adobe Journey Optimizer. Cuando no está seguro de por dónde empezar o cómo crear los recursos adecuados para los casos de uso deseados, los manuales de tácticas de casos de uso proporcionan inspiración y crean diferentes recursos para probarlos e importarlos en entornos de producción cuando estén listos.

Para empezar a usar [!UICONTROL Manuales de tácticas de casos de uso], lea las siguientes páginas de documentación:

- Lea la [página de información general](/help/use-case-playbooks/playbooks/overview.md) para comprender el propósito, la información de disponibilidad y obtener una demostración completa de cómo funcionan los manuales de tácticas, desde la detección hasta la creación de instancias y la importación de recursos generados en otros entornos de zona protegida.
- Obtenga una lista de [manuales de tácticas disponibles](/help/use-case-playbooks/playbooks/playbooks-list.md), agrupados por producto (Real-Time CDP o Journey Optimizer)
- Obtenga información sobre todos los [permisos necesarios](/help/use-case-playbooks/playbooks/get-started.md#grant-your-team-the-required-access-permissions) para usar manuales de tácticas y los recursos generados por los manuales de tácticas.
- Comprenda la [funcionalidad de reconocimiento de datos](/help/use-case-playbooks/playbooks/data-awareness.md) que le permite copiar recursos generados en otros entornos de zona protegida
- Obtenga [sugerencias para la solución de problemas](/help/use-case-playbooks/playbooks/troubleshooting.md) si encuentra errores o dificultades al usar los manuales de tácticas de casos de uso.

## Control de acceso basado en atributos {#abac}

El control de acceso basado en atributos es una función de Adobe Experience Platform que proporciona a las marcas conscientes de la privacidad una mayor flexibilidad para administrar el acceso de los usuarios. Los objetos individuales, como los campos de esquema y los segmentos, se pueden asignar a funciones de usuario. Esta función le permite conceder o revocar el acceso a objetos individuales para usuarios de Experience Platform específicos de su organización.

Mediante el control de acceso basado en atributos, los administradores de su organización pueden controlar el acceso de los usuarios a los datos personales confidenciales (SPD), la información de identificación personal (PII) y otros tipos personalizados de datos en todos los flujos de trabajo y recursos de Experience Platform. Los administradores pueden definir funciones de usuario que solo tengan acceso a campos y datos específicos que correspondan a esos campos.

**Documentación nueva o actualizada**

| Actualización de documentación  | Descripción |
| --- | --- |
| Nuevos puntos finales de API documentados para el control de acceso basado en atributos | La [documentación de referencia de la API de control de acceso](https://developer.adobe.com/experience-platform-apis/references/access-control/) ahora incluye funciones, directivas y puntos finales de producto de API de control de acceso basados en atributos. Estos puntos finales se pueden utilizar para recuperar funciones, directivas y productos relevantes para un usuario en recursos determinados de una zona protegida especificada. |

{style="table-layout:auto"}

Para obtener más información sobre el control de acceso basado en atributos, consulte la [información general del control de acceso basado en atributos](../../access-control/abac/overview.md). Para obtener una guía completa sobre el flujo de trabajo de control de acceso basado en atributos, lea la [guía completa de control de acceso basado en atributos](../../access-control/abac/end-to-end-guide.md).

## Preparación de los datos {#data-prep}

La preparación de datos permite a los ingenieros de datos asignar, transformar y validar datos desde y hacia el modelo de datos de experiencia (XDM).

**Funciones nuevas o actualizadas**

| Función | Descripción |
| --- | --- |
| Nuevas funciones de asignación | <ul><li>`object_to_map`: utilice la función `object_to_map` para crear tipos de datos de asignación. Esta función admite varias sintaxis diferentes. Para obtener más información, lea la guía de [funciones para jerarquías: objetos](../../data-prep/functions.md#objects). </li><li>`to_map`: utilice la función `to_map` para crear un mapa con pares de nombre de campo y valor dados mediante objetos. Para obtener más información, lea la guía de [funciones para jerarquías - mapas](../../data-prep/functions.md#map). </li><li>`array_to_map`: utilice la función `array_to_map` para crear un mapa con pares de nombre de campo y valor determinados mediante matrices de objetos. Para obtener más información, lea la guía de [funciones para jerarquías: mapas](../../data-prep/functions.md#map). |

{style="table-layout:auto"}

Para obtener más información sobre la preparación de datos, lea [Información general de preparación de datos](../../data-prep/home.md).

## Paneles {#dashboards}

Adobe Experience Platform proporciona varios paneles a través de los cuales puede ver información importante acerca de los datos de su organización, tal y como se captura durante las instantáneas diarias.

**Funciones nuevas o actualizadas**

| Función | Descripción |
| --- | --- |
| Ver SQL | Ahora puede ver el SQL subyacente a sus perfiles, audiencias, destinos y perspectivas personalizadas con la opción Ver SQL y, a continuación, ejecutar la consulta bajo demanda mediante el Editor de consultas. El acceso al SQL que alimenta las perspectivas de Real-time Customer Data Platform le ayuda a comprender la lógica detrás del análisis del modelo de datos. Esta transparencia hace que los datos de Real-time CDP de su Adobe sean más accesibles, comprensibles e impactantes para la toma de decisiones.<br>Inspírese con el SQL de más de 40 perspectivas existentes para crear nuevas consultas que obtengan perspectivas únicas de los datos de Experience Platform en función de sus necesidades comerciales. El SQL también está disponible para las perspectivas de [Perfiles](../../dashboards/insights/profiles.md), [Públicos](../../dashboards/insights/audiences.md) y [Destinos](../../dashboards/insights/destinations.md) de la documentación de Experience League. Estos documentos destacan los casos de uso empresarial que se pueden responder con las perspectivas estándar. Para obtener más información, lea la guía de [visualización de SQL de datos](../../dashboards/view-sql.md). |

{style="table-layout:auto"}

Para obtener más información sobre los paneles, incluido cómo conceder permisos de acceso y crear widgets personalizados, comience por leer la [información general sobre paneles](../../dashboards/home.md).

## Destinos {#destinations}

[!DNL Destinations] son integraciones generadas previamente con plataformas de destino que permiten la activación perfecta de datos de Adobe Experience Platform. Puede utilizar los destinos para activar los datos conocidos y desconocidos para campañas de marketing entre canales, campañas por correo electrónico, publicidad segmentada y muchos otros casos de uso.

**Nuevos destinos** {#new-destinations}

| Destino | Descripción |
| ----------- | ----------- |
| [Conexión Pubmatic](../../destinations/catalog/advertising/pubmatic.md) | Utilice este destino para enviar datos de público a la plataforma [!DNL PubMatic Connect]. |

{style="table-layout:auto"}

**Funcionalidad nueva o actualizada** {#destinations-new-updated-functionality}

| Funcionalidad | Descripción |
| ----------- | ----------- |
| Se ha asumido el nuevo tipo de autenticación de **función** para los destinos de Amazon S3 | Utilice el nuevo tipo de autenticación de función asumida al conectar Experience Platform a los contenedores de Amazon S3 si no desea compartir claves de cuenta y claves secretas con Experience Platform. Obtenga más información acerca del nuevo método de autenticación en la [sección de autenticación](/help/destinations/catalog/cloud-storage/amazon-s3.md#assumed-role-authentication) de la documentación de Amazon S3. |

{style="table-layout:auto"}

Para obtener información más general sobre los destinos, consulte la [información general sobre destinos](../../destinations/home.md).

## Servicio de identidad {#identity-service}

El servicio de identidad de Adobe Experience Platform le ofrece una vista completa de sus clientes y de su comportamiento al unir identidades entre dispositivos y sistemas, lo que le permite ofrecer experiencias digitales personales impactantes en tiempo real.

**Documentación nueva o actualizada**

| Actualización de documentación  | Descripción |
| --- | --- |
| Reestructuración de documentación | La documentación del servicio de identidad se ha reestructurado para mejorar la presentación y la claridad de los conceptos dentro del servicio de identidad:<ul><li>Visite la [página de información general del servicio de identidad](../../identity-service/home.md) para obtener una guía terminológica ampliada, un ejemplo de caso de uso que detalle un recorrido típico del cliente, un desglose de cómo el servicio de identidad vincula las identidades y un resumen de la función que el servicio de identidad asigna dentro del ecosistema de Experience Platform.</li><li>Lea la guía sobre [la relación entre el Servicio de identidad y el Perfil del cliente en tiempo real](../../identity-service/identity-and-profile.md) para obtener un resumen detallado de cómo funcionan juntos los dos servicios y las diferencias entre sus propósitos, procesos, entradas y salidas.</li><li>Consulte la [Guía lógica de vinculación del Servicio de identidad](../../identity-service/features/identity-linking-logic.md) para obtener explicaciones y visualizaciones sobre cómo se comporta el gráfico de identidad en función de los distintos escenarios y las marcas de tiempo.</li></ul> |

{style="table-layout:auto"}

Para obtener más información acerca del Servicio de identidad, lea la [Información general del Servicio de identidad](../../identity-service/home.md).

## Real-Time Customer Data Platform {#rtcdp}

El compilado en Experience Platform, Real-time Customer Data Platform ([!DNL Real-Time CDP]) ayuda a las empresas a reunir datos conocidos y desconocidos para activar perfiles de clientes con decisiones inteligentes a través del recorrido del cliente. [!DNL Real-Time CDP] combina varias fuentes de datos empresariales para crear perfiles de clientes en tiempo real. Los segmentos creados a partir de estos perfiles se pueden enviar a destinos de flujo descendente para ofrecer experiencias de cliente personalizadas en todos los canales y dispositivos.

**Funciones nuevas o actualizadas**

| Función | Descripción |
| --- | --- |
| Actualizaciones a la [página principal de Real-Time CDP](https://experience.adobe.com) | <ul><li>**Widget de perfiles**: ahora puede usar el widget de perfiles para ir a la página de información general de perfiles y ver las métricas de perfil de su organización.</li><li>**Tarjeta de Métricas de perfil**: la tarjeta de Métricas de perfil del panel de la página de inicio ahora muestra el recuento total de perfiles de su organización, en función de su política de combinación respectiva.</li><li>**Widget de esquemas**: ahora puede usar el widget de esquemas para ir al flujo de trabajo de creación de esquemas en la interfaz de usuario.</li></ul> |

{style="table-layout:auto"}

**Documentación nueva o actualizada**

| Actualización de documentación  | Descripción |
| --- | --- |
| Nueva página de inicio de documentación de Real-Time CDP | Visite la [nueva página de inicio de documentación de Real-Time CDP](/help/rtcdp/home.md) para obtener información rápida sobre cómo empezar a usar el producto, las protecciones, los casos de uso de muestra y mucho más. |
| Información general de casos de uso de ejemplo de Real-Time CDP | Visite la [nueva página de información general de casos de uso de ejemplo](/help/rtcdp/use-case-guides/overview.md) para ver una colección de casos de uso de ejemplo que su organización puede lograr con Real-Time CDP. |

{style="table-layout:auto"}

Para obtener más información sobre Real-Time CDP, lea la [Información general de Real-Time CDP](../../rtcdp/overview.md).

## Perfil del cliente en tiempo real {#profile}

Adobe Experience Platform le permite impulsar experiencias coordinadas, coherentes y relevantes para sus clientes, independientemente de dónde o cuándo interactúen con su marca. Con el perfil del cliente en tiempo real, puede ver una vista integral de cada cliente individual combinando datos de varios canales, incluidos los canales en línea, sin conexión, CRM y de terceros. El perfil le permite consolidar los datos de sus clientes en una vista unificada que ofrece una cuenta procesable con marca de tiempo de cada interacción del cliente.

**Funciones actualizadas**

| Función | Descripción |
| --- | --- |
| Mejoras en la localización de las tarjetas de panel predeterminadas del visualizador de perfiles | Las tarjetas de perfil predeterminadas ahora tendrán nombres localizados dinámicamente. Las tarjetas de perfil personalizadas pueden seguir teniendo nombres personalizados que se pueden editar. |

{style="table-layout:auto"}

Para obtener más información sobre el perfil del cliente en tiempo real, lea la [descripción general del perfil](../../profile/home.md)

## Servicio de segmentación {#segmentation}

[!DNL Segmentation Service] define un subconjunto particular de perfiles mediante la descripción de los criterios que distinguen a un grupo comercializable de personas dentro de su base de clientes. Los segmentos pueden basarse en datos de registro (como información demográfica) o en eventos de series temporales que representen las interacciones de los clientes con su marca.

**Funciones nuevas o actualizadas**

| Función | Descripción |
| ------- | ----------- |
| Carga de público generada externamente | El número máximo de columnas se ha aumentado a **25**. |
| Estimaciones del Generador de segmentos | Las estimaciones y los perfiles cualificados ahora se muestran en la sección de propiedades de público. Para obtener más información sobre este cambio, lea la [Guía de la IU del Generador de segmentos](../../segmentation/ui/segment-builder.md). |

{style="table-layout:auto"}

Para obtener más información sobre [!DNL Segmentation Service], consulte la [Información general sobre segmentación](../../segmentation/home.md).

## Fuentes {#sources}

Experience Platform proporciona una API RESTful y una IU interactiva que le permite configurar conexiones de origen para varios proveedores de datos con facilidad. Estas conexiones de origen le permiten autenticarse y conectarse a sistemas de almacenamiento externos y servicios CRM, establecer tiempos para ejecuciones de ingesta y administrar el rendimiento de ingesta de datos.

**Funciones nuevas o actualizadas**

| Función | Descripción |
| --- | --- |
| [!BADGE Beta]{type=Informative} [!DNL Oracle NetSuite] fuentes | Utilice las integraciones de [!DNL Oracle NetSuite] en el catálogo de fuentes para llevar los datos de sus cuentas de [[!DNL Oracle NetSuite Activities]](../../sources/tutorials/ui/create/marketing-automation/oracle-netsuite-activities.md) y [[!DNL Oracle NetSuite Entities]](../../sources/tutorials/ui/create/marketing-automation/oracle-netsuite-entities.md) a Experience Platform. |
| [!BADGE Beta]{type=Informative} [!DNL Braze Currents] origen | Utilice la integración de [[!DNL Braze Currents]](../../sources/tutorials/ui/create/marketing-automation/braze.md) en el catálogo de fuentes para llevar los datos de su cuenta de [!DNL Braze] a Experience Platform. |
| Compatibilidad con la autenticación de par de claves para la fuente por lotes de [!DNL Snowflake] | Ahora puede usar la autenticación de par de claves al crear una nueva cuenta de [!DNL Snowflake] para los datos por lotes. Para obtener más información, lea la guía de [creación de una cuenta de [!DNL Snowflake] mediante la API](../../sources/tutorials/api/create/databases/snowflake.md) o la guía de [creación de una cuenta de [!DNL Snowflake] mediante la IU](../../sources/tutorials/ui/create/databases/snowflake.md). |

{style="table-layout:auto"}

Para obtener más información acerca de las fuentes, lea la [Información general de fuentes](../../sources/home.md).
