---
title: Marketo Measure Ultimate destination
description: Obtenga información sobre cómo conectar y activar datos en el destino de Marketo Measure Ultimate.
last-substantial-update: 2023-03-07T00:00:00Z
exl-id: b4220841-8908-41ff-b977-dbeebfa787c8
source-git-commit: 58f69a78fb3c622c8741d7a1618f15509c160a5b
workflow-type: tm+mt
source-wordcount: '782'
ht-degree: 3%

---

# Destino de Marketo Measure Ultimate {#mmu-destination}

## Información general {#overview}

Marketo Measure (anteriormente Bizible) proporciona a los especialistas en marketing insight, en la que los esfuerzos de marketing son los más eficaces para generar ingresos y maximizar el retorno de la inversión para su compañía. Marketo Measure es una solución de atribución de marketing que realiza automáticamente un seguimiento e informa sobre el rendimiento del canal, lo que proporciona visibilidad sobre los canales que impulsan la mayor participación del cliente y le permite optimizar el gasto de marketing en consecuencia.

El destino habilita los flujos de datos de empresa a empresa (B2B) de [!DNL Adobe Experience Platform] a Marketo Measure. La tarjeta solo está disponible para los clientes de Marketo Measure Ultimate.

## Casos de uso {#use-cases}

Para ayudarle a comprender mejor cómo y cuándo debe utilizar el destino de Marketo Measure, aquí hay casos de uso de ejemplo que los clientes de [!DNL Adobe Experience Platform] pueden resolver mediante este destino. Esta integración:

* Satisface los complejos requisitos de datos e informes de rendimiento de las grandes empresas.
* Permite la creación de informes de atribución B2B con varios sistemas de automatización de marketing y CRM.
* Proporciona la facilidad de incorporar datos de puntos de contacto sin conexión de terceros.

## Requisitos previos {#prerequisites}

Tenga en cuenta los siguientes requisitos previos para el destino de Marketo Measure:

* El administrador debe completar la asignación de la zona protegida de Experience Platform en la página de configuración de Marketo Measure. Sin la asignación de zona protegida, no puede completar el flujo de trabajo para conectarse al destino, guardar y activar datos.
* Solo se pueden exportar conjuntos de datos de clases XDM B2B (consulte, por ejemplo, las clases Cuenta empresarial de XDM y Oportunidad empresarial de XDM). No se pueden incluir varios conjuntos de datos de la misma clase XDM B2B para una fuente de datos determinada.
* Cada conjunto de datos solo se puede incluir en un flujo de datos al destino de Marketo Measure.

## Audiencias compatibles {#supported-audiences}

Esta sección describe qué tipos de audiencias puede exportar a este destino.

| Origen de audiencia | Admitido | Descripción |
|---------|----------|----------|
| [!DNL Segmentation Service] | Sí | Audiencias generadas a través del [servicio de segmentación](../../../segmentation/home.md) de Experience Platform. |
| Todos los demás orígenes de audiencia | No | Esta categoría incluye todos los orígenes de audiencia fuera de las audiencias generadas a través de [!DNL Segmentation Service]. Obtenga información acerca de [varios orígenes de audiencia](/help/segmentation/ui/audience-portal.md#customize). Algunos ejemplos son: <ul><li> audiencias de carga personalizadas [importadas](../../../segmentation/ui/audience-portal.md#import-audience) a Experience Platform desde archivos CSV,</li><li> audiencias de similitud, </li><li> audiencias federadas, </li><li> audiencias generadas en otras aplicaciones de Experience Platform, como [!DNL Adobe Journey Optimizer], </li><li> y más. </li></ul> |

{style="table-layout:auto"}



Audiencias compatibles por tipo de datos de audiencia:

| Tipo de datos de audiencia | Admitido | Descripción | Casos de uso |
|--------------------|-----------|-------------|-----------|
| [Audiencias de personas](/help/segmentation/types/people-audiences.md) | No | Basado en perfiles de clientes, lo que le permite dirigirse a grupos específicos de personas para campañas de marketing. | Compradores frecuentes, abandonadores del carro de compras |
| [Audiencias de la cuenta](/help/segmentation/types/account-audiences.md) | No | Segmente a individuos dentro de organizaciones específicas para estrategias de marketing basadas en cuentas. | Marketing B2B |
| [Audiencias potenciales](/help/segmentation/types/prospect-audiences.md) | No | Dirija la actividad a personas que aún no sean clientes, pero que compartan características con la audiencia a la que va dirigida. | Prospección con datos de terceros |
| [Exportaciones de conjuntos de datos](/help/catalog/datasets/overview.md) | Sí | Colecciones de datos estructurados almacenados en el lago de datos [!DNL Adobe Experience Platform]. | Informes, flujos de trabajo de ciencia de datos |

{style="table-layout:auto"}


## Tipo y frecuencia de exportación {#export-type-frequency}

Consulte la tabla siguiente para obtener información sobre el tipo y la frecuencia de exportación de destino.

| Elemento | Tipo | Notas |
|---------|----------|---------|
| Tipo de exportación | **[!UICONTROL Dataset export]** | Va a exportar conjuntos de datos sin procesar que no se agrupan ni estructuran por intereses o cualificaciones de audiencia. Más información sobre [exportaciones de conjuntos de datos](/help/destinations/destination-types.md#dataset-export-destinations). |
| Frecuencia de exportación | **[!UICONTROL Batch]** | Este destino de lote exporta archivos a la plataforma de Marketo Measure cada dos horas. Obtenga más información sobre [la programación de exportaciones de conjuntos de datos](/help/destinations/ui/export-datasets.md#scheduling). |

{style="table-layout:auto"}

## Conectar con el destino {#connect}

>[!IMPORTANT]
>
>Para conectarse al destino, necesita los **[!UICONTROL View Destinations]** y **[!UICONTROL Manage and Activate Dataset Destinations]** [permisos de control de acceso](/help/access-control/home.md#permissions). Lea la [descripción general del control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Para conectarse a este destino, siga los pasos descritos en el [tutorial de configuración de destino](../../ui/connect-destination.md). En el flujo de trabajo de configuración de destino, rellene los campos enumerados en la sección siguiente.

### Rellenar detalles de destino {#destination-details}

Para configurar los detalles del destino, rellene los campos obligatorios y opcionales a continuación. Un asterisco junto a un campo en la interfaz de usuario indica que el campo es obligatorio.

* **[!UICONTROL Name]**: un nombre con el cual reconocerá este destino en el futuro.
* **[!UICONTROL Description]**: una descripción que le ayudará a identificar este destino en el futuro.

![Flujo de trabajo Conectar con destino para el destino de Marketo Measure.](/help/destinations/assets/catalog/adobe/marketo-measure-ultimate/marketo-measure-connect-to-destination.png)

### Habilitar alertas {#enable-alerts}

Puede activar alertas para recibir notificaciones sobre el estado del flujo de datos a su destino. Seleccione una alerta de la lista a la que suscribirse para recibir notificaciones sobre el estado del flujo de datos. Para obtener más información sobre las alertas, consulte la guía sobre [suscripción a alertas de destinos mediante la interfaz de usuario](../../ui/alerts.md).

Cuando termine de proporcionar detalles para la conexión de destino, seleccione **[!UICONTROL Next]**.

## Exportar conjuntos de datos a este destino {#export-datasets}

>[!IMPORTANT]
>
>Para activar los datos, necesita los **[!UICONTROL View Destinations]** y **[!UICONTROL Manage and Activate Dataset Destinations]** [permisos de control de acceso](/help/access-control/home.md#permissions). Lea la [descripción general del control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Lea el tutorial [Exportar conjuntos de datos](/help/destinations/ui/export-datasets.md) para obtener instrucciones detalladas sobre cómo exportar conjuntos de datos a este destino.

## Validar exportación de datos {#exported-data}

Para validar una exportación correcta del conjunto de datos, puede comprobar que el conjunto de datos ha llegado correctamente a [Snowflake Data Warehouse](https://experienceleague.adobe.com/docs/marketo-measure/using/marketo-measure-data-warehouse/data-warehouse-access-reader-account.html?lang=es).

## Uso de datos y gobernanza {#data-usage-governance}

Todos los destinos de [!DNL Adobe Experience Platform] cumplen con las políticas de uso de datos al administrar los datos. Para obtener información detallada sobre cómo [!DNL Adobe Experience Platform] aplica el control de datos, lea la [Información general sobre el control de datos](/help/data-governance/home.md).
