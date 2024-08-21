---
title: Exportar conjuntos de datos a destinos de almacenamiento en la nube
type: Tutorial
description: Obtenga información sobre cómo exportar conjuntos de datos de Adobe Experience Platform a su ubicación de almacenamiento en la nube preferida.
exl-id: e89652d2-a003-49fc-b2a5-5004d149b2f4
source-git-commit: 85b69af6fd21cfa9712e9c57593cbf00a62837c8
workflow-type: tm+mt
source-wordcount: '1814'
ht-degree: 4%

---

# Exportar conjuntos de datos a destinos de almacenamiento en la nube

>[!AVAILABILITY]
>
>* Esta funcionalidad está disponible para los clientes que hayan adquirido el paquete Real-Time CDP Prime o Ultimate, Adobe Journey Optimizer o Customer Journey Analytics. Póngase en contacto con el representante del Adobe para obtener más información.

En este artículo se explica el flujo de trabajo necesario para exportar [conjuntos de datos](/help/catalog/datasets/overview.md) de Adobe Experience Platform a su ubicación de almacenamiento en la nube preferida, como [!DNL Amazon S3], ubicaciones SFTP o [!DNL Google Cloud Storage], mediante la interfaz de usuario del Experience Platform.

También puede utilizar las API de Experience Platform para exportar conjuntos de datos. Lea el [tutorial de API para exportar conjuntos de datos](/help/destinations/api/export-datasets.md) para obtener más información.

## Conjuntos de datos disponibles para exportar {#datasets-to-export}

Los conjuntos de datos que puede exportar varían en función de la aplicación del Experience Platform (Real-Time CDP, Adobe Journey Optimizer), el nivel (Prime o Ultimate) y cualquier complemento que haya adquirido (por ejemplo: Data Distiller).

Comprenda, a partir de la tabla siguiente, qué tipos de conjuntos de datos puede exportar según su aplicación, nivel de producto y cualquier complemento adquirido:

<table>
<thead>
  <tr>
    <th>Aplicación/complemento</th>
    <th>Nivel</th>
    <th>Conjuntos de datos disponibles para exportar</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td rowspan="2">Real-Time CDP</td>
    <td>Prime</td>
    <td>Conjuntos de datos de perfil y evento de experiencia creados en la interfaz de usuario de Experience Platform después de la ingesta o recopilación de datos mediante fuentes, SDK web, SDK móvil, conector de datos de Analytics y Audience Manager.</td>
  </tr>
  <tr>
    <td>Ultimate</td>
    <td><ul><li>Conjuntos de datos de perfil y evento de experiencia creados en la interfaz de usuario de Experience Platform después de la ingesta o recopilación de datos mediante fuentes, SDK web, SDK móvil, conector de datos de Analytics y Audience Manager.</li><li> <a href="https://experienceleague.adobe.com/docs/experience-platform/dashboards/query.html#profile-attribute-datasets">Conjunto de datos de instantánea de perfil generado por el sistema</a>.</li></td>
  </tr>
  <tr>
    <td rowspan="2">Adobe Journey Optimizer</td>
    <td>Prime</td>
    <td>Consulte la documentación de <a href="https://experienceleague.adobe.com/docs/journey-optimizer/using/data-management/datasets/export-datasets.html#datasets"> Adobe Journey Optimizer</a>.</td>
  </tr>
  <tr>
    <td>Ultimate</td>
    <td>Consulte la documentación de <a href="https://experienceleague.adobe.com/docs/journey-optimizer/using/data-management/datasets/export-datasets.html#datasets"> Adobe Journey Optimizer</a>.</td>
  </tr>
  <tr>
    <td>Customer Journey Analytics</td>
    <td>Todas</td>
    <td> Conjuntos de datos de perfil y evento de experiencia creados en la interfaz de usuario de Experience Platform después de la ingesta o recopilación de datos mediante fuentes, SDK web, SDK móvil, conector de datos de Analytics y Audience Manager.</td>
  </tr>
  <tr>
    <td>Data Distiller</td>
    <td>Data Distiller (complemento)</td>
    <td>Conjuntos de datos derivados creados mediante el servicio de consultas.</td>
  </tr>
</tbody>
</table>

## Tutorial de vídeo {#video-tutorial}

Vea el siguiente vídeo para obtener una explicación completa del flujo de trabajo descrito en esta página, los beneficios de utilizar la funcionalidad de exportar conjunto de datos y algunos casos de uso sugeridos.

>[!VIDEO](https://video.tv.adobe.com/v/3424392/)

## Destinos admitidos {#supported-destinations}

Actualmente, puede exportar conjuntos de datos a los destinos de almacenamiento en la nube resaltados en la captura de pantalla y que se enumeran a continuación.

![Página del catálogo de destinos que muestra qué destinos admiten exportaciones de conjuntos de datos.](/help/destinations/assets/ui/export-datasets/destinations-supporting-dataset-exports.png)

* [[!DNL Azure Data Lake Storage Gen2]](../../destinations/catalog/cloud-storage/adls-gen2.md)
* [[!DNL Data Landing Zone]](../../destinations/catalog/cloud-storage/data-landing-zone.md)
* [[!DNL Google Cloud Storage]](../../destinations/catalog/cloud-storage/google-cloud-storage.md)
* [[!DNL Amazon S3]](../../destinations/catalog/cloud-storage/amazon-s3.md#changelog)
* [[!DNL Azure Blob]](../../destinations/catalog/cloud-storage/azure-blob.md#changelog)
* [[!DNL SFTP]](../../destinations/catalog/cloud-storage/sftp.md#changelog)

## Cuándo activar audiencias o exportar conjuntos de datos {#when-to-activate-audiences-or-activate-datasets}

Algunos destinos basados en archivos del catálogo de Experience Platform admiten la activación de audiencias y la exportación de conjuntos de datos.

* Considere la posibilidad de activar audiencias cuando desee estructurar los datos en perfiles agrupados por intereses o cualificaciones de audiencia.
* Alternativamente, considere las exportaciones de conjuntos de datos cuando desee exportar conjuntos de datos sin procesar, que no están agrupados o estructurados por intereses o cualificaciones de audiencia. Puede utilizar estos datos para la creación de informes, los flujos de trabajo de ciencia de datos y muchos otros casos de uso. Por ejemplo, como administrador, ingeniero de datos o analista, puede exportar datos desde Experience Platform para sincronizarlos con el almacén de datos, usarlos en herramientas de análisis de BI, herramientas de ML de nube externas o almacenarlos en el sistema para necesidades de almacenamiento a largo plazo.

Este documento contiene toda la información necesaria para exportar conjuntos de datos. Si desea activar *audiencias* en destinos de marketing por correo electrónico o almacenamiento en la nube, lea [Activar datos de audiencia en destinos de exportación de perfiles por lotes](/help/destinations/ui/activate-batch-profile-destinations.md).

## Requisitos previos {#prerequisites}

Para exportar conjuntos de datos a destinos de almacenamiento en la nube, debe haber [conectado correctamente a un destino](./connect-destination.md). Si aún no lo ha hecho, vaya al [catálogo de destinos](../catalog/overview.md), examine los destinos admitidos y configure el destino que desee utilizar.

### Permisos necesarios {#permissions}

Para exportar conjuntos de datos, necesita **[!UICONTROL Ver destinos]**, **[!UICONTROL Ver conjuntos de datos]** y **[!UICONTROL Administrar y activar destinos de conjuntos de datos]** [permisos de control de acceso](/help/access-control/home.md#permissions). Lea la [descripción general del control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Para asegurarse de que tiene los permisos necesarios para exportar conjuntos de datos y de que el destino admite la exportación de conjuntos de datos, examine el catálogo de destinos. Si un destino tiene un control **[!UICONTROL Activar]** o **[!UICONTROL Exportar conjuntos de datos]**, tiene los permisos apropiados.

## Seleccione su destino {#select-destination}

Siga las instrucciones para seleccionar un destino al que exportar los conjuntos de datos:

1. Vaya a **[!UICONTROL Conexiones > Destinos]** y seleccione la pestaña **[!UICONTROL Catálogo]**.

   ![Pestaña Catálogo de destino con control de catálogo resaltado.](/help/destinations/assets/ui/export-datasets/catalog-tab.png)

1. Seleccione **[!UICONTROL Activar]** o **[!UICONTROL Exportar conjuntos de datos]** en la tarjeta correspondiente al destino al que desea exportar los conjuntos de datos.

   ![Ficha de catálogo de destino con el control Activar resaltado.](/help/destinations/assets/ui/export-datasets/activate-button.png)

1. Seleccione **[!UICONTROL Conjuntos de datos de tipo de datos]** y seleccione la conexión de destino a la que desea exportar los conjuntos de datos. A continuación, seleccione **[!UICONTROL Siguiente]**.

>[!TIP]
> 
>Si desea configurar un nuevo destino para exportar conjuntos de datos, seleccione **[!UICONTROL Configure new destination]** para almacenar en déclencheur el flujo de trabajo [Connect to destination](/help/destinations/ui/connect-destination.md).

![Flujo de trabajo de activación de destino con control de conjuntos de datos resaltado.](/help/destinations/assets/ui/export-datasets/select-datatype-datasets.png)

1. Aparece la vista **[!UICONTROL Seleccionar conjuntos de datos]**. Continúe con la siguiente sección para [seleccionar sus conjuntos de datos](#select-datasets) para la exportación.

## Seleccione sus conjuntos de datos {#select-datasets}

Utilice las casillas de verificación de la izquierda de los nombres de los conjuntos de datos para seleccionar los conjuntos de datos que desea exportar al destino y, a continuación, seleccione **[!UICONTROL Siguiente]**.

![Flujo de trabajo de exportación de conjuntos de datos que muestra el paso Seleccionar conjuntos de datos, donde puede seleccionar qué conjuntos de datos exportar.](/help/destinations/assets/ui/export-datasets/select-datasets.png)

## Programación de exportación del conjunto de datos {#scheduling}

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_datasets_exportoptions"
>title="Opciones de exportación de archivos para conjuntos de datos"
>abstract="Seleccione **Exportar archivos incrementales** para exportar solo los datos que se añadieron al conjunto de datos desde la última exportación. <br> La primera exportación incremental de archivos incluye todos los datos del conjunto de datos, actuando como un relleno. Los futuros archivos incrementales incluyen solo los datos que se añadieron al conjunto de datos desde la primera exportación."

En el paso **[!UICONTROL Programación]**, puede establecer una fecha de inicio y una cadencia de exportación para las exportaciones de conjuntos de datos.

La opción **[!UICONTROL Exportar archivos incrementales]** se selecciona automáticamente. Esto déclencheur la exportación de uno o varios archivos que representan una instantánea completa del conjunto de datos. Los archivos posteriores son adiciones incrementales al conjunto de datos desde la exportación anterior.

>[!IMPORTANT]
>
>La primera exportación de archivo incremental incluye todos los datos existentes en el conjunto de datos, y funciona como relleno. La exportación puede contener uno o varios archivos.

![Flujo de trabajo de exportación del conjunto de datos que muestra el paso de programación.](/help/destinations/assets/ui/export-datasets/export-incremental-datasets.png)

1. Utilice el selector **[!UICONTROL Frecuencia]** para seleccionar la frecuencia de exportación:

   * **[!UICONTROL Diario]**: Programe exportaciones de archivos incrementales una vez al día, todos los días y a la hora que especifique.
   * **[!UICONTROL Por hora]**: Programar exportaciones de archivos incrementales cada 3, 6, 8 o 12 horas.

2. Utilice el selector **[!UICONTROL Time]** para elegir la hora del día, en formato [!DNL UTC], en que debe realizarse la exportación.

3. Utilice el selector **[!UICONTROL Fecha]** para elegir el intervalo en el que debe realizarse la exportación. Tenga en cuenta que actualmente no puede establecer una fecha de finalización para las exportaciones. Para obtener más información, vea la sección [limitaciones conocidas](#known-limitations).

4. Seleccione **[!UICONTROL Siguiente]** para guardar la programación y continuar con el paso **[!UICONTROL Revisar]**.

>[!NOTE]
> 
>Para las exportaciones de conjuntos de datos, los nombres de archivo tienen un formato preestablecido predeterminado que no se puede modificar. Consulte la sección [Verificar la exportación correcta del conjunto de datos](#verify) para obtener más información y ejemplos de archivos exportados.

## Revisar {#review}

En la página **[!UICONTROL Revisar]**, puedes ver un resumen de tu selección. Seleccione **[!UICONTROL Cancelar]** para dividir el flujo, **[!UICONTROL Atrás]** para modificar la configuración o **[!UICONTROL Finalizar]** para confirmar su selección y comenzar a exportar conjuntos de datos al destino.

![Flujo de trabajo de exportación del conjunto de datos que muestra el paso de revisión.](/help/destinations/assets/ui/export-datasets/review.png)

## Verificar exportación correcta del conjunto de datos {#verify}

Al exportar conjuntos de datos, el Experience Platform crea uno o varios archivos de `.json` o `.parquet` en la ubicación de almacenamiento proporcionada. Espere que los nuevos archivos se depositen en su ubicación de almacenamiento según la programación de exportación proporcionada.

Experience Platform crea una estructura de carpetas en la ubicación de almacenamiento especificada, donde deposita los archivos del conjunto de datos exportados. Se crea una nueva carpeta para cada tiempo de exportación, siguiendo el patrón siguiente:

`folder-name-you-provided/datasetID/exportTime=YYYYMMDDHHMM`

El nombre de archivo predeterminado se genera de forma aleatoria y garantiza que los nombres de archivo exportados sean únicos.

### Archivos de conjuntos de datos de muestra {#sample-files}

La presencia de estos archivos en su ubicación de almacenamiento es la confirmación de una exportación correcta. Para comprender cómo se estructuran los archivos exportados, puede descargar un archivo de muestra [.parquet](../assets/common/part-00000-tid-253136349007858095-a93bcf2e-d8c5-4dd6-8619-5c662e261097-672704-1-c000.parquet) o [.json](../assets/common/part-00000-tid-4172098795867639101-0b8c5520-9999-4cff-bdf5-1f32c8c47cb9-451986-1-c000.json).

#### Archivos de conjuntos de datos comprimidos {#compressed-dataset-files}

En el flujo de trabajo [conectar con destino](/help/destinations/ui/connect-destination.md#file-formatting-and-compression-options), puede seleccionar los archivos del conjunto de datos exportados que se van a comprimir, como se muestra a continuación:

![Selección del tipo de archivo y la compresión al conectarse a un destino para exportar conjuntos de datos.](/help/destinations/assets/ui/export-datasets/compression-format-datasets.gif)

Tenga en cuenta la diferencia de formato de archivo entre los dos tipos de archivo al comprimirlos:

* Al exportar archivos JSON comprimidos, el formato de archivo exportado es `json.gz`
* Al exportar archivos de parquet comprimidos, el formato de archivo exportado es `gz.parquet`

## Eliminación de conjuntos de datos de destinos {#remove-dataset}

Para eliminar conjuntos de datos de un flujo de datos existente, siga los pasos a continuación:

1. Inicie sesión en la [interfaz de usuario del Experience Platform](https://experience.adobe.com/platform/) y seleccione **[!UICONTROL Destinos]** en la barra de navegación izquierda. Seleccione **[!UICONTROL Examinar]** en el encabezado superior para ver los flujos de datos de destino existentes.

   ![Vista de exploración de destino con una conexión de destino mostrada y el resto borroso.](../assets/ui/export-datasets/browse-dataset-connections.png)

   >[!TIP]
   > 
   >Seleccione el icono de filtro ![Filter-icon](/help/images/icons/filter.png) en la parte superior izquierda para iniciar el panel de ordenación. El panel de ordenación proporciona una lista de todos sus destinos. Puede seleccionar más de un destino de la lista para ver una selección filtrada de flujos de datos asociados al destino seleccionado.

2. En la columna **[!UICONTROL Datos de activación]**, seleccione el control de conjuntos de datos para ver todos los conjuntos de datos asignados a este flujo de datos de exportación.

   ![La opción de navegación de conjuntos de datos disponible resaltada en la columna de datos de activación.](../assets/ui/export-datasets/go-to-datasets-data.png)

3. Aparecerá la página **[!UICONTROL Datos de activación]** para el destino. Utilice las casillas de verificación del lado izquierdo de la lista de conjuntos de datos para seleccionar los conjuntos de datos que desea eliminar y, a continuación, seleccione **[!UICONTROL Eliminar conjuntos de datos]** en el carril derecho para almacenar en déclencheur el cuadro de diálogo de confirmación Eliminar conjunto de datos.

   ![Cuadro de diálogo Quitar conjunto de datos que muestra el control Quitar conjunto de datos en el carril derecho.](../assets/ui/export-datasets/bulk-remove-datasets.png)

4. En el cuadro de diálogo de confirmación, seleccione **[!UICONTROL Quitar]** para eliminar inmediatamente el conjunto de datos de las exportaciones al destino.

   ![Cuadro de diálogo que muestra la opción Confirmar eliminación del conjunto de datos del flujo de datos.](../assets/ui/export-datasets/remove-dataset-confirm.png)

## Derechos de exportación de conjuntos de datos {#licensing-entitlement}

Consulte los documentos de descripción del producto para comprender cuántos datos puede exportar por año para cada solicitud de Experience Platform. Por ejemplo, puede ver la Descripción de producto de Real-Time CDP [aquí](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2c-edition-prime-and-ultimate-packages.html).

Tenga en cuenta que los derechos de exportación de datos para diferentes aplicaciones no son aditivos. Por ejemplo, esto significa que si compra Real-Time CDP Ultimate y Adobe Journey Optimizer Ultimate, el derecho de exportación de perfil será el mayor de los dos, según las descripciones del producto. Las autorizaciones por volumen se calculan tomando el número total de perfiles con licencia y multiplicando por 500 KB para Real-Time CDP Prime o 700 KB para Real-Time CDP Ultimate para determinar el volumen de datos al que tiene derecho.

Por otro lado, si ha adquirido complementos como Data Distiller, el límite de exportación de datos al que está autorizado representa la suma del nivel de producto y el complemento.

Puede ver y rastrear sus exportaciones de perfil en relación con sus límites contractuales en el panel de licencias.

## Limitaciones conocidas {#known-limitations}

Tenga en cuenta las siguientes limitaciones para la publicación de disponibilidad general de las exportaciones de conjuntos de datos:

* Actualmente, solo puede exportar archivos incrementales y no se puede seleccionar una fecha de finalización para las exportaciones de conjuntos de datos.
* Los nombres de archivo exportados no se pueden personalizar en este momento.
* Actualmente, los conjuntos de datos creados mediante API no están disponibles para la exportación.
* Actualmente, la IU no impide eliminar un conjunto de datos que se exporta a un destino. No elimine ningún conjunto de datos que se esté exportando a destinos. [Quite el conjunto de datos](#remove-dataset) de un flujo de datos de destino antes de eliminarlo.
* Las métricas de monitorización para exportaciones de conjuntos de datos se mezclan actualmente con los números de las exportaciones de perfiles, de modo que no reflejan los números de exportación reales.
* Se excluyen de las exportaciones de conjuntos de datos los datos con una marca de tiempo anterior a 365 días. Para obtener más información, vea las [protecciones para las exportaciones de conjuntos de datos programados](/help/destinations/guardrails.md#guardrails-for-scheduled-dataset-exports)
