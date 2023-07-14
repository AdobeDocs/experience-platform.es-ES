---
title: (Beta) Exportar conjuntos de datos a destinos de almacenamiento en la nube
type: Tutorial
description: Obtenga información sobre cómo exportar conjuntos de datos de Adobe Experience Platform a su ubicación de almacenamiento en la nube preferida.
exl-id: e89652d2-a003-49fc-b2a5-5004d149b2f4
source-git-commit: 6627953aba4f1cd665c3d5c4bc8711c48064374f
workflow-type: tm+mt
source-wordcount: '1425'
ht-degree: 5%

---

# (Beta) Exportar conjuntos de datos a destinos de almacenamiento en la nube

>[!IMPORTANT]
>
>* La funcionalidad para exportar conjuntos de datos está actualmente en versión beta y no está disponible para todos los usuarios. La documentación y las funciones están sujetas a cambios.
>* Esta funcionalidad beta admite la exportación de datos de primera generación, tal como se definen en Real-time Customer Data Platform [descripción del producto](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2c-edition-prime-and-ultimate-packages.html).
>* Esta funcionalidad está disponible para los clientes que han adquirido el paquete Real-Time CDP Prime y Ultimate. Póngase en contacto con el representante del Adobe para obtener más información.

Este artículo explica el flujo de trabajo necesario para exportar [conjuntos de datos](/help/catalog/datasets/overview.md) desde Adobe Experience Platform hasta su ubicación de almacenamiento en la nube preferida, como [!DNL Amazon S3], ubicaciones SFTP o [!DNL Google Cloud Storage] mediante la interfaz de usuario de Experience Platform.

También puede utilizar las API de Experience Platform para exportar conjuntos de datos. Lea el [tutorial de API de exportar conjuntos de datos](/help/destinations/api/export-datasets.md) para obtener más información.

## Destinos admitidos {#supported-destinations}

Actualmente, puede exportar conjuntos de datos a los destinos de almacenamiento en la nube resaltados en la captura de pantalla y que se enumeran a continuación.

![Destinos que admiten exportaciones de conjuntos de datos](/help/destinations/assets/ui/export-datasets/destinations-supporting-dataset-exports.png)

* [[!DNL (Beta) Azure Data Lake Storage Gen2]](../../destinations/catalog/cloud-storage/adls-gen2.md)
* [[!DNL (Beta) Data Landing Zone]](../../destinations/catalog/cloud-storage/data-landing-zone.md)
* [[!DNL (Beta) Google Cloud Storage]](../../destinations/catalog/cloud-storage/google-cloud-storage.md)
* [[!DNL (Beta) Amazon S3]](../../destinations/catalog/cloud-storage/amazon-s3.md#changelog)
* [[!DNL (Beta) Azure Blob]](../../destinations/catalog/cloud-storage/azure-blob.md#changelog)
* [[!DNL (Beta) SFTP]](../../destinations/catalog/cloud-storage/sftp.md#changelog)

## Cuándo activar audiencias o exportar conjuntos de datos {#when-to-activate-audiences-or-activate-datasets}

Algunos destinos basados en archivos del catálogo de Experience Platform admiten la activación de audiencias y la exportación de conjuntos de datos.

* Considere la posibilidad de activar audiencias cuando desee estructurar los datos en perfiles agrupados por intereses o cualificaciones de audiencia.
* Alternativamente, considere las exportaciones de conjuntos de datos cuando desee exportar conjuntos de datos sin procesar, que no están agrupados o estructurados por intereses o cualificaciones de audiencia. Puede utilizar estos datos para la creación de informes, los flujos de trabajo de ciencia de datos, para satisfacer los requisitos de cumplimiento y muchos otros casos de uso.

Este documento contiene toda la información necesaria para exportar conjuntos de datos. Si desea activar audiencias en destinos de marketing por correo electrónico o almacenamiento en la nube, lea [Activar datos de audiencia en destinos de exportación de perfiles por lotes](/help/destinations/ui/activate-batch-profile-destinations.md).

## Requisitos previos {#prerequisites}

Para exportar conjuntos de datos a destinos de almacenamiento en la nube, debe tener [conectado a un destino](./connect-destination.md). Si aún no lo ha hecho, vaya al [catálogo de destinos](../catalog/overview.md), examine los destinos admitidos y configure el destino que desee utilizar.

### Permisos necesarios {#permissions}

Para exportar conjuntos de datos, necesita el **[!UICONTROL Administrar destinos]**, **[!UICONTROL Ver destinos]**, **[!UICONTROL Activar destinos]**, y **[!UICONTROL Administrar y activar destinos de conjuntos de datos]** [permisos de control de acceso](/help/access-control/home.md#permissions). Lea el [información general de control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Para asegurarse de que tiene los permisos necesarios para exportar conjuntos de datos y de que el destino admite la exportación de conjuntos de datos, examine el catálogo de destinos. Si un destino tiene un **[!UICONTROL Activar]** o un **[!UICONTROL Exportar conjuntos de datos]** control y, a continuación, dispone de los permisos adecuados.

## Seleccione su destino {#select-destination}

Siga las instrucciones para seleccionar un destino al que exportar los conjuntos de datos:

1. Ir a **[!UICONTROL Conexiones > Destinos]** y seleccione la opción **[!UICONTROL Catálogo]** pestaña.

   ![Pestaña Catálogo de destino con control de catálogo resaltado.](/help/destinations/assets/ui/export-datasets/catalog-tab.png)

1. Seleccionar **[!UICONTROL Activar]** o **[!UICONTROL Exportar conjuntos de datos]** en la tarjeta correspondiente al destino al que desee exportar los conjuntos de datos.

   ![Pestaña Catálogo de destino con el control Activar resaltado.](/help/destinations/assets/ui/export-datasets/activate-button.png)

1. Seleccionar **[!UICONTROL Conjuntos de datos de tipo]** y seleccione la conexión de destino a la que desea exportar conjuntos de datos y, a continuación, seleccione **[!UICONTROL Siguiente]**.

>[!TIP]
> 
>Si desea configurar un nuevo destino para exportar conjuntos de datos, seleccione **[!UICONTROL Configurar nuevo destino]** para almacenar en déclencheur el [Conectar con destino](/help/destinations/ui/connect-destination.md) flujo de trabajo.

![Flujo de trabajo de activación de destino con control Datasets resaltado.](/help/destinations/assets/ui/export-datasets/select-datatype-datasets.png)

1. El **[!UICONTROL Seleccionar conjuntos de datos]** aparece la vista. Continúe con la siguiente sección para [seleccione sus conjuntos de datos](#select-datasets) para la exportación.

## Seleccione sus conjuntos de datos {#select-datasets}

Utilice las casillas de verificación de la izquierda de los nombres de los conjuntos de datos para seleccionar los conjuntos de datos que desea exportar al destino y, a continuación, seleccione **[!UICONTROL Siguiente]**.

![Flujo de trabajo de exportación de conjuntos de datos que muestra el paso Seleccionar conjuntos de datos, donde puede seleccionar qué conjuntos de datos exportar.](/help/destinations/assets/ui/export-datasets/select-datasets.png)

## Programar exportación del conjunto de datos {#scheduling}

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_datasets_exportoptions"
>title="Opciones de exportación de archivos para conjuntos de datos"
>abstract="Seleccione **Exportar archivos incrementales** para exportar solo los datos que se añadieron al conjunto de datos desde la última exportación. <br> La primera exportación incremental de archivos incluye todos los datos del conjunto de datos, actuando como un relleno. Los futuros archivos incrementales incluyen solo los datos que se añadieron al conjunto de datos desde la primera exportación."

En el **[!UICONTROL Programación]** paso, puede establecer una fecha de inicio y una cadencia de exportación para las exportaciones de conjuntos de datos.

El **[!UICONTROL Exportar archivos incrementales]** se selecciona automáticamente. Esto déclencheur una exportación en la que el primer archivo es una instantánea completa del conjunto de datos y los archivos posteriores son adiciones incrementales al conjunto de datos desde la exportación anterior.

>[!IMPORTANT]
>
>El primer archivo incremental exportado incluye todos los datos existentes en el conjunto de datos, y funciona como relleno.

![Flujo de trabajo de exportación de conjuntos de datos que muestra el paso de programación.](/help/destinations/assets/ui/export-datasets/export-incremental-datasets.png)

1. Utilice el **[!UICONTROL Frecuencia]** selector para seleccionar la frecuencia de exportación:

   * **[!UICONTROL Diario]**: programe exportaciones de archivos incrementales una vez al día, todos los días y a la hora especificada.
   * **[!UICONTROL Por hora]**: Programar exportaciones de archivos incrementales cada 3, 6, 8 o 12 horas.

2. Utilice el **[!UICONTROL Hora]** selector para elegir la hora del día, en [!DNL UTC] formato, momento en el que se debe realizar la exportación.

3. Utilice el **[!UICONTROL Fecha]** selector para elegir el intervalo en el que debe realizarse la exportación. Tenga en cuenta que en la versión beta de la función no es posible establecer una fecha de finalización para las exportaciones. Para obtener más información, consulte [limitaciones conocidas](#known-limitations) sección.

4. Seleccionar **[!UICONTROL Siguiente]** para guardar la programación y continuar con la **[!UICONTROL Revisar]** paso.

>[!NOTE]
> 
>Para las exportaciones de conjuntos de datos, los nombres de archivo tienen un formato preestablecido predeterminado que no se puede modificar. Consulte la sección [Verificar exportación correcta del conjunto de datos](#verify) para obtener más información y ejemplos de archivos exportados.

## Consulte {#review}

En el **[!UICONTROL Revisar]** , puede ver un resumen de su selección. Seleccionar **[!UICONTROL Cancelar]** para romper el flujo, **[!UICONTROL Atrás]** para modificar la configuración, o **[!UICONTROL Finalizar]** para confirmar la selección y comenzar a exportar conjuntos de datos al destino.

![Flujo de trabajo de exportación del conjunto de datos que muestra el paso de revisión.](/help/destinations/assets/ui/export-datasets/review.png)

## Verificar exportación correcta del conjunto de datos {#verify}

Al exportar conjuntos de datos, el Experience Platform crea un `.json` o `.parquet` en la ubicación de almacenamiento proporcionada. Se espera que se deposite un nuevo archivo en su ubicación de almacenamiento según el programa de exportación proporcionado.

Experience Platform crea una estructura de carpetas en la ubicación de almacenamiento especificada, donde deposita los archivos del conjunto de datos exportados. Se crea una nueva carpeta para cada tiempo de exportación, siguiendo el patrón siguiente:

`folder-name-you-provided/datasetID/exportTime=YYYYMMDDHHMM`

El nombre de archivo predeterminado se genera de forma aleatoria y garantiza que los nombres de archivo exportados sean únicos.

### Archivos de conjuntos de datos de muestra {#sample-files}

La presencia de estos archivos en su ubicación de almacenamiento es la confirmación de una exportación correcta. Para comprender cómo se estructuran los archivos exportados, puede descargar un ejemplo [archivo .parquet](../assets/common/part-00000-tid-253136349007858095-a93bcf2e-d8c5-4dd6-8619-5c662e261097-672704-1-c000.parquet) o [archivo .json](../assets/common/part-00000-tid-4172098795867639101-0b8c5520-9999-4cff-bdf5-1f32c8c47cb9-451986-1-c000.json).

#### Archivos de conjuntos de datos comprimidos {#compressed-dataset-files}

En el [flujo de trabajo conectar con destino](/help/destinations/ui/connect-destination.md#file-formatting-and-compression-options), puede seleccionar los archivos del conjunto de datos exportados que se van a comprimir, como se muestra a continuación:

![Tipo de archivo y selección de compresión al conectarse a un destino para exportar conjuntos de datos.](/help/destinations/assets/ui/export-datasets/compression-format-datasets.gif)

Tenga en cuenta la diferencia de formato de archivo entre los dos tipos de archivo al comprimirlos:

* Al exportar archivos JSON comprimidos, el formato de archivo exportado es `json.gz`
* Al exportar ficheros de parquet comprimidos, el formato de fichero exportado es `gz.parquet`

## Quitar conjunto de datos de destino {#remove-dataset}

Para eliminar un conjunto de datos de un flujo de datos existente, siga los pasos a continuación:

1. Inicie sesión en [IU de Experience Platform](https://experience.adobe.com/platform/) y seleccione **[!UICONTROL Destinos]** en la barra de navegación izquierda. Seleccionar **[!UICONTROL Examinar]** en el encabezado superior para ver los flujos de datos de destino existentes.

   ![Vista de exploración de destino con una conexión de destino mostrada y el resto borroso.](../assets/ui/export-datasets/browse-dataset-connections.png)

   >[!TIP]
   > 
   >Seleccione el icono de filtro ![Icono de filtro](../assets/ui/edit-activation/filter.png) en la parte superior izquierda para iniciar el panel ordenar. El panel de ordenación proporciona una lista de todos sus destinos. Puede seleccionar más de un destino de la lista para ver una selección filtrada de flujos de datos asociados al destino seleccionado.

1. Desde el **[!UICONTROL Datos de activación]** , seleccione el control datasets para ver todos los conjuntos de datos asignados a este flujo de datos de exportación.

   ![La opción de navegación de conjuntos de datos disponible resaltada en la columna de datos de activación.](../assets/ui/export-datasets/go-to-datasets-data.png)

1. El **[!UICONTROL Datos de activación]** página para el destino. Seleccionar **[!UICONTROL Eliminar conjunto de datos]** en el carril derecho para almacenar en déclencheur el cuadro de diálogo de confirmación eliminar conjunto de datos.

   ![Cuadro de diálogo Quitar conjunto de datos que muestra el control Quitar conjunto de datos en el carril derecho.](../assets/ui/export-datasets/remove-dataset-control.png)

1. En el cuadro de diálogo de confirmación, seleccione **[!UICONTROL Eliminar]** para eliminar inmediatamente el conjunto de datos de las exportaciones al destino.

   ![Cuadro de diálogo que muestra la opción Confirmar eliminación del conjunto de datos del flujo de datos.](../assets/ui/export-datasets/remove-dataset-confirm.png)

## Limitaciones conocidas {#known-limitations}

Tenga en cuenta las siguientes limitaciones para la versión beta de las exportaciones de conjuntos de datos:

* Actualmente hay un solo permiso (**[!UICONTROL Administrar y activar destinos de conjuntos de datos]**) que incluye permisos de administración y activación en destinos de conjuntos de datos. Estos controles se dividirán en el futuro en permisos más granulares. Revise la [permisos necesarios](#permissions) para obtener una lista completa de los permisos que necesita para exportar conjuntos de datos.
* Actualmente, solo puede exportar archivos incrementales y no se puede seleccionar una fecha de finalización para las exportaciones de conjuntos de datos.
* Los nombres de archivo exportados no se pueden personalizar en este momento.
* Actualmente, la IU no impide eliminar un conjunto de datos que se exporta a un destino. No elimine ningún conjunto de datos que se esté exportando a destinos. [Eliminar el conjunto de datos](#remove-dataset) de un flujo de datos de destino antes de eliminarlo.
* Las métricas de monitorización para exportaciones de conjuntos de datos se mezclan actualmente con los números de las exportaciones de perfiles, de modo que no reflejan los números de exportación reales.
