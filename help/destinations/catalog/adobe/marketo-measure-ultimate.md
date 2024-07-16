---
title: Destino de Marketo Measure Ultimate
description: Obtenga información sobre cómo conectar y activar datos en el destino de Marketo Measure Ultimate.
last-substantial-update: 2023-03-07T00:00:00Z
exl-id: b4220841-8908-41ff-b977-dbeebfa787c8
source-git-commit: c3ef732ee82f6c0d56e89e421da0efc4fbea2c17
workflow-type: tm+mt
source-wordcount: '643'
ht-degree: 2%

---

# Destino de Marketo Measure Ultimate {#mmu-destination}

## Información general {#overview}

Marketo Measure (anteriormente Bizible) ofrece a los especialistas en marketing un conocimiento detallado de las medidas de marketing más eficaces para generar ingresos y maximizar el retorno de la inversión para su compañía. Marketo Measure es una solución de atribución de marketing que realiza automáticamente un seguimiento e informa sobre el rendimiento del canal, lo que proporciona visibilidad sobre los canales que impulsan la mayor participación del cliente y le permite optimizar el gasto de marketing en consecuencia.

El destino permite los flujos de datos empresa a empresa (B2B) de Adobe Experience Platform a Marketo Measure. La tarjeta solo está disponible para los clientes de Marketo Measure Ultimate.

## Casos de uso {#use-cases}

Para ayudarle a comprender mejor cómo y cuándo debe utilizar el destino de Marketo Measure, aquí hay ejemplos de casos de uso que los clientes de Adobe Experience Platform pueden solucionar mediante este destino. Esta integración:

* Satisface los complejos requisitos de datos e informes de rendimiento de las grandes empresas.
* Permite la creación de informes de atribución B2B con varios sistemas de automatización de marketing y CRM.
* Proporciona la facilidad de incorporar datos de puntos de contacto sin conexión de terceros.

## Requisitos previos {#prerequisites}

Tenga en cuenta los siguientes requisitos previos para el destino de Marketo Measure:

* El administrador debe completar la asignación de la zona protegida del Experience Platform en la página de configuración de Marketo Measure. Sin la asignación de zona protegida, no puede completar el flujo de trabajo para conectarse al destino, guardar y activar datos.
* Solo se pueden exportar conjuntos de datos de clases XDM B2B (consulte, por ejemplo, las clases Cuenta empresarial de XDM y Oportunidad empresarial de XDM). No se pueden incluir varios conjuntos de datos de la misma clase XDM B2B para una fuente de datos determinada.
* Cada conjunto de datos solo se puede incluir en un flujo de datos al destino de Marketo Measure.

## Tipo y frecuencia de exportación {#export-type-frequency}

Consulte la tabla siguiente para obtener información sobre el tipo y la frecuencia de exportación de destino.

| Elemento | Tipo | Notas |
---------|----------|---------|
| Tipo de exportación | **[!UICONTROL Exportación de conjuntos de datos]** | Va a exportar conjuntos de datos sin procesar que no se agrupan ni estructuran por intereses o cualificaciones de audiencia. Más información sobre [exportaciones de conjuntos de datos](/help/destinations/destination-types.md#dataset-export-destinations). |
| Frecuencia de exportación | **[!UICONTROL Lote]** | Este destino de lote exporta archivos a la plataforma de Marketo Measure cada dos horas. Obtenga más información sobre [la programación de exportaciones de conjuntos de datos](/help/destinations/ui/export-datasets.md#scheduling). |

{style="table-layout:auto"}

## Conexión al destino {#connect}

>[!IMPORTANT]
> 
>Para conectarse al destino, necesita los **[!UICONTROL permisos de control de acceso](/help/access-control/home.md#permissions) de Ver destinos]** y **[!UICONTROL Administrar y activar destinos de conjuntos de datos]**[5}. Lea la [descripción general del control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Para conectarse a este destino, siga los pasos descritos en el [tutorial de configuración de destino](../../ui/connect-destination.md). En el flujo de trabajo de configuración de destino, rellene los campos enumerados en la sección siguiente.

### Rellenar detalles de destino {#destination-details}

Para configurar los detalles del destino, rellene los campos obligatorios y opcionales a continuación. Un asterisco junto a un campo en la interfaz de usuario indica que el campo es obligatorio.

* **[!UICONTROL Nombre]**: Un nombre por el cual reconocerá este destino en el futuro.
* **[!UICONTROL Descripción]**: Una descripción que le ayudará a identificar este destino en el futuro.

![Flujo de trabajo Conectar con destino para el destino de Marketo Measure.](/help/destinations/assets/catalog/adobe/marketo-measure-ultimate/marketo-measure-connect-to-destination.png)

### Habilitar alertas {#enable-alerts}

Puede activar alertas para recibir notificaciones sobre el estado del flujo de datos a su destino. Seleccione una alerta de la lista a la que suscribirse para recibir notificaciones sobre el estado del flujo de datos. Para obtener más información sobre las alertas, consulte la guía sobre [suscripción a alertas de destinos mediante la interfaz de usuario](../../ui/alerts.md).

Cuando termine de proporcionar detalles para la conexión de destino, seleccione **[!UICONTROL Siguiente]**.

## Exportar conjuntos de datos a este destino {#export-datasets}

>[!IMPORTANT]
> 
>Para activar los datos, necesita los **[!UICONTROL permisos de control de acceso](/help/access-control/home.md#permissions) de Ver destinos]** y **[!UICONTROL Administrar y activar destinos de conjuntos de datos]**[5}. Lea la [descripción general del control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Lea el tutorial [Exportar conjuntos de datos](/help/destinations/ui/export-datasets.md) para obtener instrucciones detalladas sobre cómo exportar conjuntos de datos a este destino.

## Validar exportación de datos {#exported-data}

Para validar una exportación correcta del conjunto de datos, puede comprobar que el conjunto de datos ha llegado correctamente al [almacén de datos del Snowflake](https://experienceleague.adobe.com/docs/marketo-measure/using/marketo-measure-data-warehouse/data-warehouse-access-reader-account.html).

## Uso de datos y gobernanza {#data-usage-governance}

Todos los destinos de [!DNL Adobe Experience Platform] cumplen con las políticas de uso de datos al administrar los datos. Para obtener información detallada sobre cómo [!DNL Adobe Experience Platform] aplica el control de datos, lea la [Información general sobre el control de datos](/help/data-governance/home.md).
