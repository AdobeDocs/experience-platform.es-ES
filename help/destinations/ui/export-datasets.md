---
title: (Beta) Exportar conjuntos de datos a destinos de almacenamiento en la nube
type: Tutorial
description: Obtenga información sobre cómo exportar conjuntos de datos de Adobe Experience Platform a su ubicación de almacenamiento en la nube preferida.
exl-id: e89652d2-a003-49fc-b2a5-5004d149b2f4
source-git-commit: d0de642eb6118e6597925c12c76917ffa98c3a5a
workflow-type: tm+mt
source-wordcount: '1359'
ht-degree: 5%

---

# (Beta) Exportar conjuntos de datos a destinos de almacenamiento en la nube

>[!IMPORTANT]
>
>* La funcionalidad para exportar conjuntos de datos está actualmente en versión beta y no está disponible para todos los usuarios. La documentación y las funciones están sujetas a cambios.
>* Esta funcionalidad beta admite la exportación de datos de primera generación, tal como se definen en la [descripción del producto](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2c-edition-prime-and-ultimate-packages.html).
>* Esta funcionalidad está disponible para los clientes que han adquirido el paquete Real-Time CDP Prime y Ultimate. Póngase en contacto con su representante del Adobe para obtener más información.


Este artículo explica el flujo de trabajo necesario para exportar [conjuntos de datos](/help/catalog/datasets/overview.md) de Adobe Experience Platform a su ubicación de almacenamiento en la nube preferida, como [!DNL Amazon S3], ubicaciones SFTP o [!DNL Google Cloud Storage] mediante la interfaz de usuario del Experience Platform.

También puede utilizar las API de Experience Platform para exportar conjuntos de datos. Lea el [tutorial de API de exportación de conjuntos de datos](/help/destinations/api/export-datasets.md) para obtener más información.

## Destinos admitidos {#supported-destinations}

Actualmente, puede exportar conjuntos de datos a los destinos de almacenamiento en la nube resaltados en la captura de pantalla y enumerados a continuación.

![Destinos que admiten exportaciones de conjuntos de datos](/help/destinations/assets/ui/export-datasets/destinations-supporting-dataset-exports.png)

* [[!DNL (Beta) Azure Data Lake Storage Gen2]](../../destinations/catalog/cloud-storage/adls-gen2.md)
* [[!DNL (Beta) Data Landing Zone]](../../destinations/catalog/cloud-storage/data-landing-zone.md)
* [[!DNL (Beta) Google Cloud Storage]](../../destinations/catalog/cloud-storage/google-cloud-storage.md)
* [[!DNL (Beta) Amazon S3]](../../destinations/catalog/cloud-storage/amazon-s3.md#changelog)
* [[!DNL (Beta) Azure Blob]](../../destinations/catalog/cloud-storage/azure-blob.md#changelog)
* [[!DNL (Beta) SFTP]](../../destinations/catalog/cloud-storage/sftp.md#changelog)

## Cuándo activar segmentos o exportar conjuntos de datos {#when-to-activate-segments-or-activate-datasets}

Algunos destinos basados en archivos del catálogo de Experience Platform admiten tanto la activación de segmentos como la exportación de conjuntos de datos.

* Considere la posibilidad de activar segmentos cuando desee que los datos se estructuren en perfiles agrupados por intereses o cualificaciones de audiencia.
* Alternativamente, considere las exportaciones de conjuntos de datos cuando busque exportar conjuntos de datos sin procesar, que no se agrupan ni estructuran por intereses o cualificaciones de audiencia. Puede utilizar estos datos para los informes, los flujos de trabajo de ciencia de datos, para satisfacer los requisitos de cumplimiento y muchos otros casos de uso.

Este documento contiene toda la información necesaria para exportar conjuntos de datos. Si desea activar segmentos en el almacenamiento en la nube o en destinos de marketing por correo electrónico, lea [Activar datos de audiencia en destinos de exportación de perfiles en lote](/help/destinations/ui/activate-batch-profile-destinations.md).

## Requisitos previos {#prerequisites}

Para exportar conjuntos de datos a destinos de almacenamiento en la nube, debe haber [conectado a un destino](./connect-destination.md). Si aún no lo ha hecho, vaya a la [catálogo de destinos](../catalog/overview.md), busque los destinos compatibles y configure el destino que desea utilizar.

### Permisos necesarios {#permissions}

Para exportar conjuntos de datos, necesita la variable **[!UICONTROL Administrar destinos]**, **[!UICONTROL Ver destinos]**, **[!UICONTROL Activar destinos]** y **[!UICONTROL Administrar y activar destinos de conjuntos de datos]** [permisos de control de acceso](/help/access-control/home.md#permissions). Lea el [información general sobre el control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Para asegurarse de que tiene los permisos necesarios para exportar conjuntos de datos y de que el destino admite la exportación de conjuntos de datos, busque el catálogo de destinos. Si un destino tiene un **[!UICONTROL Activar]** o **[!UICONTROL Exportación de conjuntos de datos]** y, a continuación, tiene los permisos adecuados.

## Seleccione el destino {#select-destination}

Siga las instrucciones para seleccionar un destino en el que pueda exportar sus conjuntos de datos:

1. Vaya a **[!UICONTROL Conexiones > Destinos]** y seleccione **[!UICONTROL Catálogo]** pestaña .

   ![Pestaña Catálogo de destino con el control Catálogo resaltado.](/help/destinations/assets/ui/export-datasets/catalog-tab.png)

1. Select **[!UICONTROL Activar]** o **[!UICONTROL Exportación de conjuntos de datos]** en la tarjeta correspondiente al destino en el que desea exportar conjuntos de datos.

   ![Pestaña Catálogo de destino con el control Activate resaltado.](/help/destinations/assets/ui/export-datasets/activate-button.png)

1. Select **[!UICONTROL Conjuntos de datos de tipo de datos]** y seleccione la conexión de destino a la que desea exportar conjuntos de datos y, a continuación, seleccione **[!UICONTROL Siguiente]**.

>[!TIP]
> 
>Si desea configurar un nuevo destino para exportar conjuntos de datos, seleccione **[!UICONTROL Configurar nuevo destino]** para el déclencheur de la variable [Conectarse al destino](/help/destinations/ui/connect-destination.md) flujo de trabajo.

![Flujo de trabajo de activación de destino con el control Conjuntos de datos resaltado.](/help/destinations/assets/ui/export-datasets/select-datatype-datasets.png)

1. La variable **[!UICONTROL Seleccionar conjuntos de datos]** se abre. Continúe con la siguiente sección para [seleccionar sus conjuntos de datos](#select-datasets) para la exportación.

## Seleccionar los conjuntos de datos {#select-datasets}

Utilice las casillas de verificación a la izquierda de los nombres de los conjuntos de datos para seleccionar los conjuntos de datos que desea exportar al destino y, a continuación, seleccione **[!UICONTROL Siguiente]**.

![Flujo de trabajo de exportación de conjuntos de datos que muestra el paso Seleccionar conjuntos de datos donde puede seleccionar qué conjuntos de datos desea exportar.](/help/destinations/assets/ui/export-datasets/select-datasets.png)

## Programar exportación de conjuntos de datos {#scheduling}

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_datasets_exportoptions"
>title="Opciones de exportación de archivos para conjuntos de datos"
>abstract="Seleccione **Exportar archivos incrementales** para exportar solo los datos que se añadieron al conjunto de datos desde la última exportación. <br> La primera exportación incremental de archivos incluye todos los datos del conjunto de datos, actuando como un relleno. Los futuros archivos incrementales incluyen solo los datos que se añadieron al conjunto de datos desde la primera exportación."

En el **[!UICONTROL Programación]** , puede establecer una fecha de inicio y una cadencia de exportación para sus exportaciones de conjuntos de datos.

La variable **[!UICONTROL Exportar archivos incrementales]** se selecciona automáticamente. Esto déclencheur una exportación en la que el primer archivo es una instantánea completa del conjunto de datos y los archivos posteriores son adiciones incrementales al conjunto de datos desde la exportación anterior.

>[!IMPORTANT]
>
>El primer archivo incremental exportado incluye todos los datos existentes en el conjunto de datos, que funcionan como un relleno.

![Flujo de trabajo de exportación de conjuntos de datos que muestra el paso de programación.](/help/destinations/assets/ui/export-datasets/export-incremental-datasets.png)

1. Utilice la variable **[!UICONTROL Frecuencia]** para seleccionar la frecuencia de exportación:

   * **[!UICONTROL Diario]**: Programe exportaciones de archivos incrementales una vez al día, todos los días, en el momento que especifique.
   * **[!UICONTROL Por hora]**: Programe las exportaciones de archivos incrementales cada 3, 6, 8 o 12 horas.

2. Utilice la variable **[!UICONTROL Tiempo]** para elegir la hora del día, en [!DNL UTC] , cuándo se debe realizar la exportación.

3. Utilice la variable **[!UICONTROL Fecha]** para elegir el intervalo en el que se debe realizar la exportación. Tenga en cuenta que en la versión beta de la función, no es posible establecer una fecha de finalización para las exportaciones. Para obtener más información, consulte [limitaciones conocidas](#known-limitations) para obtener más información.

4. Select **[!UICONTROL Siguiente]** para guardar la programación y continuar con el **[!UICONTROL Consulte]** paso a paso.

>[!NOTE]
> 
>Para las exportaciones de conjuntos de datos, los nombres de archivo tienen un formato preestablecido y predeterminado, que no se puede modificar. Consulte la sección [Comprobar la exportación correcta del conjunto de datos](#verify) para obtener más información y ejemplos de archivos exportados.

## Consulte {#review}

En el **[!UICONTROL Consulte]** , puede ver un resumen de su selección. Select **[!UICONTROL Cancelar]** para desglosar el flujo, **[!UICONTROL Atrás]** para modificar la configuración, o **[!UICONTROL Finalizar]** para confirmar la selección e iniciar la exportación de conjuntos de datos al destino.

![Flujo de trabajo de exportación de conjuntos de datos que muestra el paso de revisión.](/help/destinations/assets/ui/export-datasets/review.png)

## Comprobar la exportación correcta del conjunto de datos {#verify}

Al exportar conjuntos de datos, el Experience Platform crea un `.json` o `.parquet` en la ubicación de almacenamiento proporcionada. Espere a que se deposite un nuevo archivo en su ubicación de almacenamiento según la programación de exportación proporcionada.

El Experience Platform crea una estructura de carpetas en la ubicación de almacenamiento especificada, donde almacena los archivos de conjuntos de datos exportados. Se crea una nueva carpeta para cada hora de exportación, siguiendo el patrón a continuación:

`folder-name-you-provided/datasetID/exportTime=YYYYMMDDHHMM`

El nombre de archivo predeterminado se genera aleatoriamente y garantiza que los nombres de archivo exportados sean únicos.

### Archivos de conjunto de datos de muestra {#sample-files}

La presencia de estos archivos en su ubicación de almacenamiento es la confirmación de una exportación correcta. Para comprender la estructura de los archivos exportados, puede descargar una muestra [archivo .parquet](../assets/common/part-00000-tid-253136349007858095-a93bcf2e-d8c5-4dd6-8619-5c662e261097-672704-1-c000.parquet) o [archivo .json](../assets/common/part-00000-tid-4172098795867639101-0b8c5520-9999-4cff-bdf5-1f32c8c47cb9-451986-1-c000.json).

## Quitar conjunto de datos del destino {#remove-dataset}

Para eliminar un conjunto de datos de un flujo de datos existente, siga los pasos a continuación:

1. Inicie sesión en la [IU de Experience Platform](https://platform.adobe.com/) y seleccione **[!UICONTROL Destinos]** en la barra de navegación izquierda. Select **[!UICONTROL Examinar]** del encabezado superior para ver los flujos de datos de destino existentes.

   ![Vista de exploración de destino con una conexión de destino mostrada y el resto desdibujado.](../assets/ui/export-datasets/browse-dataset-connections.png)

   >[!TIP]
   > 
   >Seleccione el icono de filtro ![Icono de filtro](../assets/ui/edit-activation/filter.png) en la parte superior izquierda para iniciar el panel de ordenación. El panel de ordenación proporciona una lista de todos sus destinos. Puede seleccionar más de un destino de la lista para ver una selección filtrada de flujos de datos asociados al destino seleccionado.

1. En el **[!UICONTROL Datos de activación]** , seleccione el control datasets para ver todos los conjuntos de datos asignados a este flujo de datos de exportación.

   ![La opción de navegación de conjuntos de datos disponible resaltada en la columna Datos de activación .](../assets/ui/export-datasets/go-to-datasets-data.png)

1. La variable **[!UICONTROL Datos de activación]** para el destino. Select **[!UICONTROL Quitar conjunto de datos]** en el carril derecho para almacenar en déclencheur el cuadro de diálogo eliminar confirmación de conjunto de datos .

   ![El cuadro de diálogo Quitar conjunto de datos muestra el control Quitar conjunto de datos en el carril derecho.](../assets/ui/export-datasets/remove-dataset-control.png)

1. En el cuadro de diálogo de confirmación, seleccione **[!UICONTROL Eliminar]** para eliminar inmediatamente el conjunto de datos de las exportaciones al destino.

   ![Cuadro de diálogo que muestra la opción Confirmar eliminación de conjuntos de datos del flujo de datos.](../assets/ui/export-datasets/remove-dataset-confirm.png)

## Limitaciones conocidas {#known-limitations}

Tenga en cuenta las siguientes limitaciones para la versión beta de las exportaciones de conjuntos de datos:

* Actualmente hay un solo permiso (**[!UICONTROL Administrar y activar destinos de conjuntos de datos]**) que incluye administrar y activar permisos en destinos de conjuntos de datos. Estos controles se dividirán en permisos más granulares en el futuro. Consulte la [permisos necesarios](#permissions) para obtener una lista completa de los permisos que necesita para exportar conjuntos de datos.
* Actualmente, solo puede exportar archivos incrementales y no se puede seleccionar una fecha de finalización para las exportaciones del conjunto de datos.
* Los nombres de archivo exportados no se pueden personalizar actualmente.
* Actualmente, la interfaz de usuario no le impide eliminar un conjunto de datos que se está exportando a un destino. No elimine ningún conjunto de datos que se esté exportando a los destinos. [Eliminación del conjunto de datos](#remove-dataset) de un flujo de datos de destino antes de eliminarlo.
* Actualmente, las métricas de monitorización para exportaciones de conjuntos de datos están mezcladas con números para exportaciones de perfiles, por lo que no reflejan los números de exportación reales.
