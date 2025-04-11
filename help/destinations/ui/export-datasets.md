---
title: Exportar conjuntos de datos a destinos de almacenamiento en la nube
type: Tutorial
description: Aprenda a exportar conjuntos de datos desde Adobe Experience Platform a su ubicación almacenamiento nube preferida.
exl-id: e89652d2-a003-49fc-b2a5-5004d149b2f4
source-git-commit: 29fb232ecfbd119ef84d62599fc79249513dca43
workflow-type: tm+mt
source-wordcount: '2703'
ht-degree: 7%

---

# Exportar conjuntos de datos a destinos almacenamiento nube

>[!AVAILABILITY]
>
>Este funcionalidad está disponible para los clientes que hayan adquirido el paquete Real-Time CDP Prime o Ultimate, Adobe Systems Journey Optimizer o Customer Journey Analytics. Póngase en contacto con su representante de Adobe para obtener más información.

>[!IMPORTANT]
>
>**Elemento de acción**: la versión de [septiembre de 2024 de Experience Platform](/help/release-notes/latest/latest.md#destinations) introdujo la opción de establecer una fecha de `endTime` para exportar flujos de datos del conjunto de datos. Adobe también ha introducido una fecha de finalización predeterminada del 1 de mayo de 2025 para todos los flujos de datos de exportación de conjuntos de datos creados *antes de la versión de septiembre de 2024*.
>
>Para cualquiera de estos flujos de datos, debe actualizar la fecha de finalización del flujo de datos manualmente antes de la fecha de finalización; de lo contrario, las exportaciones se detendrán en esa fecha. Utilice la IU de Experience Platform para ver qué flujos de datos se configurarán para detenerse el 1 de mayo de 2025.
>
>Consulte la [sección de programación](#scheduling) para obtener información sobre cómo editar la fecha de finalización de un flujo de datos de exportación de conjunto de datos.

Este artículo explica los flujo de trabajo necesarios para exportar [conjuntos](/help/catalog/datasets/overview.md) de datos desde Adobe Experience Platform a su ubicación de almacenamiento nube preferida, como [!DNL Amazon S3]ubicaciones SFTP o [!DNL Google Cloud Storage] mediante el IU Experience Platform.

También puede utilizar las API Experience Platform para exportar conjuntos de datos. Lea la tutorial](/help/destinations/api/export-datasets.md) de la API de conjuntos de [datos de exportación para obtener más información.

## Conjuntos de datos disponibles para exportar {#datasets-to-export}

Los conjuntos de datos que puede exportar varían en función del aplicación de Experience Platform (CDP en tiempo real, Adobe Systems Journey Optimizer), el nivel (Prime o Ultimate) y cualquier complemento que haya adquirido (por ejemplo: Data Distiller).

Use la siguiente tabla para conocer qué tipos de conjunto de datos puede exportar en función de su aplicación, nivel de producto y los complementos adquiridos:

<table>
<thead>
  <tr>
    <th>Aplicación/añadir-activado</th>
    <th>Nivel</th>
    <th>Conjuntos de datos disponibles para exportar</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td rowspan="2">Real-Time CDP</td>
    <td>Prime</td>
    <td>Los conjuntos de datos de eventos de perfil y experiencia creados en la IU de Experience Platform después de ingerir o recopilar datos a través de orígenes, SDK web, SDK móvil, conector de datos de Analytics y Audience Manager.</td>
  </tr>
  <tr>
    <td>Ultimate</td>
    <td><ul><li>Los conjuntos de datos de eventos de perfil y experiencia creados en la IU de Experience Platform después de ingerir o recopilar datos a través de orígenes, SDK web, SDK móvil, conector de datos de Analytics y Audience Manager.</li><li> <a href="https://experienceleague.adobe.com/docs/experience-platform/dashboards/query.html#profile-attribute-datasets">Instantánea de perfil generada por el sistema conjunto de datos</a>.</li></td>
  </tr>
  <tr>
    <td rowspan="2">Adobe Journey Optimizer</td>
    <td>Prime</td>
    <td>Consulte la documentación de <a href="https://experienceleague.adobe.com/docs/journey-optimizer/using/data-management/datasets/export-datasets.html#datasets"> Adobe Systems Journey Optimizer</a> .</td>
  </tr>
  <tr>
    <td>Ultimate</td>
    <td>Consulte la documentación de <a href="https://experienceleague.adobe.com/docs/journey-optimizer/using/data-management/datasets/export-datasets.html#datasets"> Adobe Journey Optimizer</a>.</td>
  </tr>
  <tr>
    <td>Customer Journey Analytics</td>
    <td>Todas</td>
    <td> Los conjuntos de datos de eventos de perfil y experiencia creados en la IU de Experience Platform después de ingerir o recopilar datos a través de orígenes, SDK web, SDK móvil, conector de datos de Analytics y Audience Manager.</td>
  </tr>
  <tr>
    <td>Data Distiller</td>
    <td>Distiller de datos (añadir activado)</td>
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

Algunos destinos basados en archivos del catálogo de Experience Platform admiten tanto la exportación audiencia activación como la exportación conjunto de datos.

* Considere activar audiencias cuando desee que sus datos se estructuren en perfiles agrupados por intereses o calificaciones audiencia.
* Alternativamente, considere conjunto de datos exportaciones cuando busque exportar conjuntos de datos sin procesar, que no estén agrupados o estructurados por intereses o calificaciones audiencia. Puede usar estos datos para sistema de informes, flujos de trabajo de ciencia de datos y muchos otros casos de uso. Por ejemplo, como administrador, ingeniero de datos o analista, puede exportar datos desde Experience Platform para sincronizarlos con su almacén de datos, usarlos en herramientas de análisis BI, herramientas externas nube de ML o tienda en su sistema para necesidades de almacenamiento a largo plazo.

Este documento contiene toda la información necesaria para exportar conjuntos de datos. Si desea activar *audiencias* para nube destinos almacenamiento o marketing por correo electrónico, lea [Activar datos de audiencia para agrupar perfil destinos](/help/destinations/ui/activate-batch-profile-destinations.md) de exportación.

## Requisitos previos {#prerequisites}

Para exportar conjuntos de datos a nube almacenamiento destinos, debe haberse conectado correctamente [a un destino](./connect-destination.md). Si aún no lo ha hecho, vaya al catálogo](../catalog/overview.md) de [destinos, explore los destinos admitidos y configure el destino que desea usar.

### Permisos necesarios {#permissions}

Para exportar conjuntos de datos, necesita los permisos Ver Destinos, Ver conjuntos de **[!UICONTROL datos]** y **[!UICONTROL Administrar y activar destinos]** [de conjuntos de datos control de acceso permisos](/help/access-control/home.md#permissions). **** Lea la control de acceso descripción general](/help/access-control/ui/overview.md) o póngase en contacto con el [administrador del producto para obtener los permisos necesarios.

Para asegurarse de que tiene los permisos necesarios para exportar conjuntos de datos y de que el destino admite la exportación de conjuntos de datos, examine el catálogo de destinos. Si un destino tiene un control **[!UICONTROL Activar]** o **[!UICONTROL Exportar conjuntos de datos]**, tiene los permisos apropiados.

## Seleccione su destino {#select-destination}

Siga las instrucciones para seleccionar un destino al que exportar los conjuntos de datos:

1. Vaya a **[!UICONTROL Conexiones > Destinos]** y seleccione la pestaña **[!UICONTROL Catálogo]**.

   ![Pestaña Catálogo de destino con control de catálogo resaltado.](/help/destinations/assets/ui/export-datasets/catalog-tab.png)

1. Seleccione **[!UICONTROL Activar]** o **[!UICONTROL Exportar conjuntos de datos]** en la tarjeta correspondiente al destino al que desea exportar los conjuntos de datos.

   ![Ficha de catálogo de destino con el control Activar resaltado.](/help/destinations/assets/ui/export-datasets/activate-button.png)

1. Seleccione **[!UICONTROL Datasets]** de tipo de datos, seleccione la conexión de destino a la que desea exportar los conjuntos de datos y, a continuación, seleccione **[!UICONTROL Siguiente]**.

>[!TIP]
> 
>Si desea configurar un nuevo destino para exportar conjuntos de datos, seleccione **[!UICONTROL Configurar nuevo destino]** para activar la flujo de trabajo Conectar con](/help/destinations/ui/connect-destination.md) destino[.

![El flujo de trabajo de activación de destino con el control de conjuntos de datos resaltado.](/help/destinations/assets/ui/export-datasets/select-datatype-datasets.png)

1. Aparece la vista **[!UICONTROL Seleccionar conjuntos de datos]**. Continúe con la siguiente sección para [seleccionar los conjuntos](#select-datasets) de datos para la exportación.

## Seleccione sus conjuntos de datos {#select-datasets}

Utilice las casillas de verificación de la izquierda de los nombres de los conjuntos de datos para seleccionar los conjuntos de datos que desea exportar al destino y, a continuación, seleccione **[!UICONTROL Siguiente]**.

![Flujo de trabajo de exportación de conjuntos de datos que muestra el paso Seleccionar conjuntos de datos, donde puede seleccionar qué conjuntos de datos exportar.](/help/destinations/assets/ui/export-datasets/select-datasets.png)

## Programación de exportación del conjunto de datos {#scheduling}

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_datasets_exportoptions"
>title="Opciones de exportación de archivos para conjuntos de datos"
>abstract="Seleccione **Exportar archivos incrementales** para exportar solo los datos que se añadieron al conjunto de datos desde la última exportación. <br> La primera exportación incremental de archivos incluye todos los datos del conjunto de datos, actuando como un relleno. Los futuros archivos incrementales incluyen solo los datos que se añadieron al conjunto de datos desde la primera exportación. <br> Seleccione **Exportar archivos completos** para exportar el abono completo de cada conjunto de datos en cada exportación. "

>[!CONTEXTUALHELP]
>id="dataset_dataflow_needs_schedule_end_date_header"
>title="Actualizar la fecha de finalización de este flujo de datos"
>abstract="Actualizar la fecha de finalización de este flujo de datos"

>[!CONTEXTUALHELP]
>id="dataset_dataflow_needs_schedule_end_date_body"
>title="Actualizar la fecha de finalización de este cuerpo de flujo de datos"
>abstract="Debido a las recientes actualizaciones en este destino, el flujo de datos ahora requiere una fecha de finalización. Adobe ha establecido una fecha de finalización predeterminada para el 1 de marzo de 2025. Actualice a la fecha de finalización deseada; de lo contrario, las exportaciones de datos se detendrán en la fecha predeterminada."

Utilice el **[!UICONTROL paso Programación]** para:

* Establezca una fecha inicio y una fecha de finalización, así como una cadencia de exportación para sus exportaciones conjunto de datos.
* Configure si los archivos de conjunto de datos exportados deben exportar el abono completo del conjunto de datos o simplemente cambios incrementales en el abono de cada Ocurrencia de exportación.
* Personalice la ruta de la carpeta en la ubicación del almacenamiento donde se deben exportar los conjuntos de datos. Obtenga más información sobre cómo [editar la ruta](#edit-folder-path) de la carpeta de exportación.

Utilice el control de **[!UICONTROL programación]** de Editar del Página para editar la cadencia de exportación de las exportaciones, así como para seleccionar si desea exportar archivos completos o incrementales.

![Editar control de programación resaltado en el paso Programación.](/help/destinations/assets/ui/export-datasets/edit-schedule-control-highlight.png)

La **[!UICONTROL opción Exportar archivos]** incrementales está seleccionada de forma predeterminada. Esto desencadena una exportación de uno o varios archivos, lo que representa una instantánea completa del conjunto de datos. Los archivos subsiguientes son adiciones incrementales al conjunto de datos desde la exportación anterior. También puede seleccionar **[!UICONTROL Exportar archivos completos]**. En este caso, seleccione la Frecuencia **[!UICONTROL Una vez]** para una exportación completa única del conjunto de datos.

>[!IMPORTANT]
>
>La primera exportación incremental de archivos incluye todos los datos existentes en el conjunto de datos, funcionando como un relleno. La exportación puede contener uno o varios archivos.

![flujo de trabajo de exportación de conjuntos de datos que muestran el paso de programación.](/help/destinations/assets/ui/export-datasets/export-incremental-datasets.png)

1. Utilice la **[!UICONTROL selector de frecuencia]** para seleccionar el Frecuencia de exportación:

   * **[!UICONTROL Diario]**: Programe exportaciones de archivos incrementales una vez al día, todos los días y a la hora que especifique.
   * **[!UICONTROL Por hora]**: programe exportaciones de archivos incrementales cada 3, 6, 8 o 12 horas.

2. Utilice el **[!UICONTROL selector de tiempo]** para elegir la hora del día, en [!DNL UTC] formato, en la que debe realizarse la exportación.

3. Utilice el **[!UICONTROL selector Fecha]** para elegir el intervalo en el que debe realizarse la exportación.

4. Seleccione **[!UICONTROL Guardar para guardar la programación y continuar con el paso Revisar]****[!UICONTROL .]**

>[!NOTE]
> 
>Para conjunto de datos exportaciones, los nombres de archivo tienen un formato predeterminado preestablecido que no se puede modificar. Consulte la sección [Verificar la exportación](#verify) conjunto de datos correcta para obtener más información y ejemplos de los archivos exportados.

## Editar ruta de la carpeta {#edit-folder-path}

>[!CONTEXTUALHELP]
>id="destinations_folder_name_template"
>title="Editar ruta de la carpeta"
>abstract="Utilice varias macros proporcionadas para personalizar la ruta de la carpeta donde se exportan los conjuntos de datos."

>[!CONTEXTUALHELP]
>id="destinations_folder_name_template_preview"
>title="Previsualización de ruta de carpeta de conjuntos de datos"
>abstract="Obtenga una previsualización de la estructura de carpetas que se crea en su ubicación de almacenamiento en función de las macros añadidas en esta ventana."

Seleccione **[!UICONTROL Editar ruta]** de carpeta para personalizar la estructura de carpetas en la ubicación almacenamiento donde se depositan los conjuntos de datos exportados.

![Editar control de ruta de carpeta resaltado en el paso de programación.](/help/destinations/assets/ui/export-datasets/edit-folder-path.png)

Puede utilizar varias macros disponibles para personalizar un nombre de carpeta deseado. Haga doble clic en una macro para agregarla a la ruta de acceso de la carpeta y utilícela `/` entre las macros para separar las carpetas.

![Selección de macros resaltada en la ventana modal de carpeta personalizada.](/help/destinations/assets/ui/export-datasets/custom-folder-path-macros.png)

Después de seleccionar las macros deseadas, puede ver un previsualización de la estructura de carpetas que se creará en su ubicación almacenamiento. El primer nivel de la estructura de carpetas representa la **[!UICONTROL ruta de la carpeta]** que indicó al [conectarse al destino](/help/destinations/ui/connect-destination.md##set-up-connection-parameters) para exportar conjuntos de datos.

![Vista previa de ruta de carpeta resaltada en la ventana modal de carpeta personalizada.](/help/destinations/assets/ui/export-datasets/custom-folder-path-preview.png)

## Revisar {#review}

En la **[!UICONTROL Página de revisión]** , puede ver un resumen de su selección. Seleccione **[!UICONTROL Cancelar]** para dividir el flujo **[!UICONTROL Atrás]** modificar la configuración o **[!UICONTROL Finalizar]** para confirmar la selección y inicio exportar los conjuntos de datos al destino.

![Los flujo de trabajo de exportación de conjuntos de datos que muestran el paso de revisión.](/help/destinations/assets/ui/export-datasets/review.png)

## Verificar que la exportación de conjunto de datos se haya realizado correctamente {#verify}

Al exportar conjuntos de datos, Experience Platform crea uno o varios archivos de `.json` o `.parquet` en la ubicación de almacenamiento proporcionada. Espere que los nuevos archivos se depositen en su ubicación de almacenamiento según la programación de exportación proporcionada.

Experience Platform crea una estructura de carpetas en la ubicación de almacenamiento especificada, donde deposita los archivos del conjunto de datos exportados. El patrón de exportación de carpetas predeterminado se muestra a continuación, pero puede [personalizar la estructura de carpetas con sus macros preferidas](#edit-folder-path).

>[!TIP]
> 
>El primer nivel de esta estructura de carpetas - `folder-name-you-provided` - representa la **[!UICONTROL ruta de la carpeta]** que indicó al [conectarse al destino](/help/destinations/ui/connect-destination.md##set-up-connection-parameters) para exportar conjuntos de datos.

`folder-name-you-provided/datasetID/exportTime=YYYYMMDDHHMM`

El nombre de archivo predeterminado se genera de forma aleatoria y garantiza que los nombres de archivo exportados sean únicos.

### Archivos de conjuntos de datos de muestra {#sample-files}

La presencia de estos archivos en su ubicación de almacenamiento es la confirmación de una exportación correcta. Para comprender cómo se estructuran los archivos exportados, puede descargar un archivo de muestra [.parquet](../assets/common/part-00000-tid-253136349007858095-a93bcf2e-d8c5-4dd6-8619-5c662e261097-672704-1-c000.parquet) o [.json](../assets/common/part-00000-tid-4172098795867639101-0b8c5520-9999-4cff-bdf5-1f32c8c47cb9-451986-1-c000.json).

#### Archivos de conjunto de datos comprimidos {#compressed-dataset-files}

En la [flujo de trabajo](/help/destinations/ui/connect-destination.md#file-formatting-and-compression-options) Conectar con destino puede seleccionar los archivos de conjunto de datos exportados que desea comprimir, como se muestra a continuación:

![Archivo tipo y selección de compresión al conectarse a un destino para exportar conjuntos de datos.](/help/destinations/assets/ui/export-datasets/compression-format-datasets.gif)

Tenga en cuenta la diferencia de formato de archivo entre los dos tipos de archivo al comprimirlos:

* Al exportar archivos JSON comprimidos, el formato de archivo exportado es `json.gz`. El formato del JSON exportado es NDJSON, que es el formato de intercambio estándar en el ecosistema de big data. Adobe recomienda utilizar un cliente compatible con NDJSON para leer los archivos exportados.
* Al exportar archivos de parquet comprimidos, el formato de archivo exportado es `gz.parquet`

Solo se admiten las exportaciones a archivos JSON *en modo comprimido*. Las exportaciones a archivos Parquet se admiten en modo comprimido y sin comprimir.

## Quitar conjuntos de datos de destinos {#remove-dataset}

Para eliminar conjuntos de datos de un flujo de datos existente, seguir los pasos siguientes:

1. Inicie sesión en la [Experience Platform IU](https://experience.adobe.com/platform/) y seleccione **[!UICONTROL Destinos]** en la barra de navegación izquierda. Seleccione **[!UICONTROL Examinar]** en el encabezado superior para vista los flujos de datos de destino existentes.

   ![Destino explore vista con una conexión de destino mostrada y el resto borrosa.](../assets/ui/export-datasets/browse-dataset-connections.png)

   >[!TIP]
   > 
   >Seleccione el icono ![de](/help/images/icons/filter.png) filtro Filtrar en la parte superior izquierda para iniciar el panel de clasificación. El panel de ordenación proporciona una lista de todos los destinos. Puede seleccionar más de un destino desde el lista para ver una selección filtrada de flujos de datos asociados con el destino seleccionado.

2. En la **[!UICONTROL columna de datos]** Activation, seleccione el control de conjuntos de datos para vista todos los conjuntos de datos asignados a este flujo de datos de exportación.

   ![Los conjuntos de datos disponibles navegación opción resaltada en la columna de datos Activation.](../assets/ui/export-datasets/go-to-datasets-data.png)

3. Aparece el **[!UICONTROL Página de datos]** Activation del destino. Utilice las casillas de verificación del lado izquierdo del lista de conjunto de datos para seleccionar los conjuntos de datos que desea eliminar y, a continuación, seleccione **[!UICONTROL Quitar conjuntos]** de datos en el carril derecho para activar el cuadro de diálogo de confirmación conjunto de datos eliminación.

   ![Quitar conjunto de datos cuadro de diálogo que muestre el Quitar conjunto de datos control en el carril derecho.](../assets/ui/export-datasets/bulk-remove-datasets.png)

4. En el cuadro de diálogo de confirmación, seleccione **[!UICONTROL Quitar]** para eliminar inmediatamente el conjunto de datos de las exportaciones al destino.

   ![Cuadro de diálogo que muestra la opción Confirmar conjunto de datos eliminación del flujo de datos.](../assets/ui/export-datasets/remove-dataset-confirm.png)

## Derechos de exportación de conjuntos de datos {#licensing-entitlement}

Consulte la descripción del producto documentos para comprender cuántos datos tiene derecho a exportar para cada Experience Platform aplicación, por año. Por ejemplo, puede vista el Descripción [del producto CDP en tiempo real aquí](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2c-edition-prime-and-ultimate-packages.html).

Tenga en cuenta que los derechos de exportación de datos para diferentes aplicaciones no son aditivos. Por ejemplo, esto significa que si adquiere Real-Time CDP Ultimate y Adobe Systems Journey Optimizer Ultimate, el perfil derecho de exportación será el mayor de los dos derechos, según las descripciones del producto. Sus derechos de volumen se calculan tomando el número total de perfiles con licencia y multiplicando por 500 KB para Real-Time CDP Prime o 700 KB para Real-Time CDP Ultimate para determinar cuánto volumen de datos tiene derecho.

Por otro lado, si compró complementos como Data Distiller, el límite de exportación de datos al que tiene derecho representa la suma del nivel de producto y el complemento.

Puede vista y realizar un seguimiento de sus exportaciones de perfil con respecto a sus límites contractuales en el panel](/help/landing/license-usage-and-guardrails/license-usage-dashboard.md) de uso de [licencias.

## Limitaciones conocidas {#known-limitations}

Tenga en cuenta las siguientes limitaciones para la versión de disponibilidad general de conjunto de datos exportaciones:

* Experience Platform puede exportar varios archivos igualado para conjuntos de datos pequeños. La exportación de conjuntos de datos está diseñada para la integración de sistema a sistema y optimizada para el rendimiento, por lo que el número de archivos exportados no es personalizable.
* Actualmente, los nombres de archivo exportados no se pueden personalizar.
* Los conjuntos de datos creados mediante API no están disponibles para exportar actualmente.
* En este momento, el IU no impide eliminar un conjunto de datos que se esté exportando a un destino. No elimine ningún conjunto de datos que se esté exportando a destinos. [Quitar la conjunto de datos](#remove-dataset) de un flujo de datos de destino antes de eliminarla.
* Las métricas de monitoreo para conjunto de datos exportaciones actualmente se mezclan con los números para perfil exportaciones, por lo que no reflejan los números reales de exportación.
* Los datos con una marca de tiempo anterior a 365 días se excluyen de conjunto de datos exportaciones. Para obtener más información, vista las [barandillas para las exportaciones de conjunto de datos programadas](/help/destinations/guardrails.md#guardrails-for-scheduled-dataset-exports)

## Preguntas frecuentes {#faq}

**¿Podemos generar un archivo sin carpeta si simplemente guardamos como `/` la ruta de la carpeta? Además, si no requerimos una ruta de carpeta, ¿cómo se generarán los archivos con nombres duplicado en una carpeta o ubicación?**

+++Respuesta
A partir de la versión de septiembre de 2024, es posible personalizar el nombre de la carpeta y igualado uso `/` para exportar archivos para todos los conjuntos de datos de la misma carpeta. Adobe Systems no recomienda esto para destinos que exportan varios conjuntos de datos, ya que los nombres de archivo generados por el sistema que pertenecen a diferentes conjuntos de datos se mezclarán en la misma carpeta.
+++

**¿Puede enrutar el archivo de manifiesto a una carpeta y los archivos de datos a otra carpeta?**

+++Respuesta
No, no es posible copiar el archivo de manifiesto en una ubicación diferente.
+++

**¿Podemos controlar la secuenciación o el tiempo de los envío de archivo?**

+++Respuesta
Hay opciones para programar la exportación. No hay opciones para retrasar o secuenciar la copia de los archivos. Se copian en la ubicación del almacenamiento en cuanto se generan.
+++

**¿Qué formatos hay disponibles para el archivo de manifiesto?**

+++Respuesta
El archivo de manifiesto se encuentra en .json formato.
+++

**¿Hay disponibilidad de API para el archivo de manifiesto?**

+++Respuesta
No hay ninguna API disponible para el archivo de manifiesto, pero incluye un lista de archivos que comprende la exportación.
+++

**¿Podemos agregar detalles adicionales al archivo de manifiesto (es decir, recuento de registros)? Si es así, ¿cómo?**

+++Respuesta
No es posible añadir información adicional al archivo de manifiesto. El recuento de registros está disponible a través de la entidad `flowRun` (consultable mediante API). Obtenga más información en la monitorización de destinos.
+++

**¿Cómo se dividen los archivos de datos? ¿Cuántos registros por archivo?**

+++Respuesta
Los archivos de datos se dividen según la partición predeterminada en el lago de datos de Experience Platform. Los conjuntos de datos más grandes tienen un número mayor de particiones. El usuario no puede configurar la partición predeterminada porque está optimizada para la lectura.
+++

**¿Podemos establecer un umbral (número de registros por archivo)?**

+++Respuesta
No, no es posible.
+++

**¿Cómo reenviamos un conjunto de datos en el evento en que el envío inicial es incorrecto?**

+++Respuesta
Los reintentos se realizan automáticamente para la mayoría de los tipos de errores del sistema.
+++