---
title: Crear una conexión y un flujo de datos de Source de resolución de identidad empresarial de Mercury en la IU de
description: Obtenga información sobre cómo crear una conexión de origen de resolución de identidad empresarial de Mercury mediante la IU de Adobe Experience Platform.
last-substantial-update: 2023-12=12
badge: Beta
exl-id: 2af48c18-76f9-4615-8e76-8f030a312a8f
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '2146'
ht-degree: 1%

---

# Crear una conexión de origen y un flujo de datos de [!DNL Merkury Enterprise Identity Resolution] en la interfaz de usuario

>[!NOTE]
>
>El origen [!DNL Merkury Enterprise Identity Resolution] está en la versión beta. Lea [información general de orígenes](../../../../home.md#terms-and-conditions) para obtener más información sobre el uso de orígenes etiquetados como beta.

Este tutorial proporciona los pasos para crear una conexión de origen y un flujo de datos de [!DNL Merkury Enterprise Identity Resolution] mediante la interfaz de usuario de Adobe Experience Platform.

## Introducción 

Este tutorial requiere una comprensión práctica de los siguientes componentes de Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): El marco estandarizado mediante el cual Experience Platform organiza los datos de experiencia del cliente.
   * [Aspectos básicos de la composición de esquemas](../../../../../xdm/schema/composition.md): obtenga información sobre los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   * [Tutorial del editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): Aprenda a crear esquemas personalizados mediante la interfaz de usuario del editor de esquemas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): proporciona un perfil de consumidor unificado y en tiempo real basado en los datos agregados de varias fuentes.

### Recopilar credenciales necesarias

Para acceder a su bloque en Experience Platform, debe proporcionar valores válidos para las siguientes credenciales:

| Credencial | Descripción |
| --- | --- |
| Clave de acceso | ID de clave de acceso para el bloque. Puede recuperar este valor de su equipo [!DNL Merkury]. |
| Clave secreta | El ID de clave secreta de su cubo. Puede recuperar este valor de su equipo [!DNL Merkury]. |
| Nombre del segmento | Este es su espacio de Mercury donde se compartirán los archivos. Puede recuperar este valor de su equipo [!DNL Merkury]. |

Para obtener más información sobre la configuración de [!DNL Merkury] y otros requisitos previos, lea la [[!DNL Merkury] descripción general del origen](../../../../connectors/data-partners/merkury.md).

## Conecta tu cuenta de Merkury

En la interfaz de usuario de Experience Platform, seleccione **[!UICONTROL Fuentes]** en la barra de navegación izquierda para acceder al área de trabajo de [!UICONTROL Fuentes]. La pantalla [!UICONTROL Catálogo] muestra una variedad de orígenes con los que puede crear una cuenta.

Puede seleccionar la categoría adecuada del catálogo en la parte izquierda de la pantalla. También puede encontrar la fuente específica con la que desea trabajar utilizando la opción de búsqueda.

En la categoría **[!UICONTROL Socios de datos]**, seleccione **[!UICONTROL Merkury]** y luego **[!UICONTROL Configurar]**.

![El catálogo de orígenes con el origen de Merkury seleccionado.](../../../../images/tutorials/create/merkury-enterprise-identity-resolution-assets/catalog.png)

Aparecerá la página **[!UICONTROL Conectar con Merkury]**. En esta página, puede usar credenciales nuevas o existentes.

### Crear una nueva cuenta

Si está usando credenciales nuevas, seleccione **[!UICONTROL Nueva cuenta]**. En el formulario de entrada que aparece, proporcione un nombre, una descripción opcional y sus credenciales de [!DNL Merkury]. Cuando termine, seleccione **[!UICONTROL Conectarse al origen]** y deje pasar un tiempo para que se establezca la nueva conexión.

![Interfaz de la nueva cuenta para Merkury.](../../../../images/tutorials/create/merkury-enterprise-identity-resolution-assets/new-account.png)

### Usar una cuenta existente

Para usar una cuenta existente, seleccione **[!UICONTROL Cuenta existente]** y luego seleccione la cuenta [!DNL Merkury] que desee usar. Seleccione **[!UICONTROL Siguiente]** para continuar.

![Interfaz de cuenta existente para Merkury.](../../../../images/tutorials/create/merkury-enterprise-identity-resolution-assets/existing-account.png)

>[!BEGINSHADEBOX]

**Formatos de archivo compatibles**

Puede ingerir los siguientes formatos de archivo con el origen [!DNL Merkury]:

* Valores separados por delimitadores (DSV): cualquier valor de un solo carácter puede utilizarse como delimitador para archivos de datos con formato DSV.
* [!DNL JavaScript Object Notation] (JSON): los archivos de datos con formato JSON deben ser compatibles con XDM.
* [!DNL Apache Parquet]: los archivos de datos con formato de parquet deben ser compatibles con XDM.
* Archivos comprimidos: los archivos JSON y delimitados se pueden comprimir como: `bzip2`, `gzip`, `deflate`, `zipDeflate`, `tarGzip` y `tar`.

>[!ENDSHADEBOX]

## Adición de datos

Después de crear la cuenta de [!DNL Merkury], aparece el paso **[!UICONTROL Agregar datos]**, que proporciona una interfaz para explorar la jerarquía de archivos de [!DNL Merkury] y seleccionar la carpeta o el archivo específico que desea llevar a Experience Platform.

* La parte izquierda de la interfaz es un explorador de directorios que muestra la jerarquía de archivos de [!DNL Merkury].
* La parte derecha de la interfaz permite obtener una vista previa de hasta 100 filas de datos desde una carpeta o archivo compatible.

![Directorio de archivos y carpetas del flujo de trabajo de orígenes donde puede seleccionar los datos que desea introducir.](../../../../images/tutorials/create/merkury-enterprise-identity-resolution-assets/add-data.png)

Seleccione la carpeta raíz para acceder a la jerarquía de carpetas. Desde aquí, puede seleccionar una sola carpeta para introducir todos los archivos de la carpeta de forma recursiva. Al ingerir una carpeta completa, debe asegurarse de que todos los archivos de esa carpeta compartan el mismo formato de datos y esquema.

Una vez seleccionada una carpeta, la interfaz correcta se actualiza a una vista previa del contenido y la estructura del primer archivo de la carpeta seleccionada.

![Los datos seleccionados para la ingesta y la interfaz de vista previa de archivos.](../../../../images/tutorials/create/merkury-enterprise-identity-resolution-assets/selected-data.png)


Durante este paso, puede realizar varias configuraciones en los datos antes de continuar. En primer lugar, selecciona **[!UICONTROL Formato de datos]** y, a continuación, selecciona el formato de datos apropiado para el archivo en el panel desplegable que aparece.

La siguiente tabla muestra los formatos de datos adecuados para los tipos de archivo admitidos:

| Tipo de archivo | Formato de datos |
| --- | --- |
| CSV | [!UICONTROL Delimitado] |
| JSON | [!UICONTROL JSON] |
| Parquet | [!UICONTROL XDM Parquet] |

### Seleccionar un delimitador de columna

+++Seleccione esta opción para ver los pasos sobre cómo establecer un delimitador

Después de configurar el formato de datos, puede establecer un delimitador de columna al ingerir archivos delimitados. Seleccione la opción **[!UICONTROL Delimitador]** y, a continuación, seleccione un delimitador en el menú desplegable. El menú muestra las opciones utilizadas con más frecuencia para delimitadores, como una coma (`,`), una tabulación (`\t`) y una barra vertical (`|`).

Si prefiere usar un delimitador personalizado, seleccione **[!UICONTROL Personalizado]** e introduzca un delimitador de un solo carácter de su elección en la barra de entrada emergente.

+++

### Ingesta de archivos comprimidos

+++ Seleccione esta opción para ver los pasos de ingesta de archivos comprimidos

También puede introducir archivos JSON comprimidos o delimitados especificando su tipo de compresión.

En el paso [!UICONTROL Seleccionar datos], seleccione un archivo comprimido para su ingesta y, a continuación, seleccione su tipo de archivo adecuado, y si es compatible con XDM o no. A continuación, seleccione **[!UICONTROL Tipo de compresión]** y, a continuación, seleccione el tipo de archivo comprimido apropiado para los datos de origen.

Para llevar un archivo específico a Experience Platform, seleccione una carpeta y, a continuación, el archivo que desea introducir. Durante este paso, también puede obtener una vista previa del contenido de otros archivos de una carpeta determinada mediante el icono de vista previa junto a un nombre de archivo.

Cuando termine, seleccione **[!UICONTROL Siguiente]**.

+++

## Proporcionar detalles del flujo de datos

La página [!UICONTROL Detalles del flujo de datos] le permite seleccionar si desea utilizar un conjunto de datos existente o uno nuevo. Durante este proceso, también puede configurar los datos para que se incorporen al perfil y habilitar opciones como [!UICONTROL Diagnóstico de errores], [!UICONTROL Ingesta parcial] y [!UICONTROL Alertas].

### Usar un conjunto de datos existente

Para introducir datos en un conjunto de datos existente, seleccione **[!UICONTROL Conjunto de datos existente]**. Puede recuperar un conjunto de datos existente mediante la opción [!UICONTROL Búsqueda avanzada] o desplazándose por la lista de conjuntos de datos existentes en el menú desplegable. Una vez seleccionado un conjunto de datos, proporcione un nombre y una descripción para el flujo de datos.

![Interfaz de conjunto de datos existente.](../../../../images/tutorials/create/merkury-enterprise-identity-resolution-assets/existing-dataset.png)

### Usar un nuevo conjunto de datos

Para ingerir en un nuevo conjunto de datos, seleccione **[!UICONTROL Nuevo conjunto de datos]** y, a continuación, proporcione un nombre de conjunto de datos de salida y una descripción opcional. A continuación, seleccione un esquema al que asignar con la opción [!UICONTROL Búsqueda avanzada] o desplazándose por la lista de esquemas existentes en el menú desplegable. Una vez seleccionado un esquema, proporcione un nombre y una descripción para el flujo de datos.

![La nueva interfaz del conjunto de datos.](../../../../images/tutorials/create/merkury-enterprise-identity-resolution-assets/new-dataset.png)

### Habilitar diagnósticos de perfil y error

+++Seleccione esta opción para ver los pasos para habilitar el diagnóstico de errores y la ingesta de perfiles

A continuación, seleccione la opción **[!UICONTROL Conjunto de datos del perfil]** para habilitar su conjunto de datos para el perfil del cliente en tiempo real. Esto le permite crear una vista integral de los atributos y comportamientos de una entidad. Los datos de todos los conjuntos de datos habilitados para perfiles se incluirán en el perfil y los cambios se aplicarán al guardar el flujo de datos.

[!UICONTROL Diagnósticos de error] permite la generación detallada de mensajes de error para cualquier registro erróneo que ocurra en su flujo de datos, mientras que [!UICONTROL Ingesta parcial] le permite ingerir datos que contengan errores, hasta un determinado umbral que usted defina manualmente. Consulte la [descripción general de la ingesta parcial por lotes](../../../../../ingestion/batch-ingestion/partial.md) para obtener más información.

+++

### Habilitar alertas

+++Seleccione esta opción para ver los pasos necesarios para activar las alertas

Puede activar alertas para recibir notificaciones sobre el estado del flujo de datos. Seleccione una alerta de la lista a la que suscribirse para recibir notificaciones sobre el estado del flujo de datos. Para obtener más información sobre las alertas, consulte la guía sobre [suscripción a alertas de fuentes mediante la interfaz de usuario](../../alerts.md).

Cuando termine de proporcionar detalles al flujo de datos, seleccione **[!UICONTROL Siguiente]**.

+++

## Asignación de campos de datos a un esquema XDM

Aparecerá el paso [!UICONTROL Mapping], que le proporcionará una interfaz para asignar los campos de origen del esquema de origen a sus campos XDM de destino adecuados en el esquema de destino.

Experience Platform proporciona recomendaciones inteligentes para campos asignados automáticamente en función del esquema o conjunto de datos de destino seleccionado. Puede ajustar manualmente las reglas de asignación para adaptarlas a sus casos de uso. En función de sus necesidades, puede elegir asignar campos directamente o utilizar funciones de preparación de datos para transformar los datos de origen y derivar valores calculados o calculados. Para ver los pasos detallados sobre el uso de la interfaz de asignador y los campos calculados, consulte la [guía de la interfaz de usuario de la preparación de datos](../../../../../data-prep/ui/mapping.md).

Una vez que los datos de origen estén asignados correctamente, seleccione **[!UICONTROL Siguiente]**.

![Interfaz de asignación.](../../../../images/tutorials/create/merkury-enterprise-identity-resolution-assets/mapping.png)

## Programar ejecuciones de ingesta

Aparece el paso [!UICONTROL Programación], que le permite configurar una programación de ingesta para introducir automáticamente los datos de origen seleccionados mediante las asignaciones configuradas. De manera predeterminada, la programación se establece en `Once`. Para ajustar la frecuencia de ingesta, seleccione **[!UICONTROL Frecuencia]** y luego seleccione una opción en el menú desplegable.

>[!TIP]
>
>El intervalo y el relleno no son visibles durante una ingesta única.

![Interfaz de programación](../../../../images/tutorials/create/merkury-enterprise-identity-resolution-assets/schedule.png)

Si establece la frecuencia de ingesta en `Minute`, `Hour`, `Day` o `Week`, debe establecer un intervalo para establecer un intervalo de tiempo establecido entre cada ingesta. Por ejemplo, una frecuencia de ingesta establecida en `Day` y un intervalo establecido en `15` significa que el flujo de datos está programado para ingerir datos cada 15 días.

Durante este paso, también puede habilitar **relleno** y definir una columna para la ingesta incremental de datos. El relleno se utiliza para introducir datos históricos, mientras que la columna que defina para la ingesta incremental permite diferenciar los nuevos datos de los datos existentes.

Consulte la tabla siguiente para obtener más información sobre las configuraciones de programación.

| Configuración de programación | Descripción |
| --- | --- |
| Frecuencia | Configure la frecuencia para indicar con qué frecuencia debe ejecutarse el flujo de datos. Puede establecer su frecuencia en: <ul><li>**Una vez**: establezca su frecuencia en `once` para crear una ingesta única. Las configuraciones para intervalo y relleno no están disponibles al crear un flujo de datos de ingesta único. De forma predeterminada, la frecuencia de programación se establece en una vez.</li><li>**Minuto**: establezca su frecuencia en `minute` para programar el flujo de datos e ingerir datos por minuto.</li><li>**Hora**: establezca su frecuencia en `hour` para programar el flujo de datos e ingerir datos por hora.</li><li>**Día**: Establezca su frecuencia en `day` para programar su flujo de datos e ingerir datos por día.</li><li>**Semana**: establezca su frecuencia en `week` para programar el flujo de datos e ingerir datos por semana.</li></ul> |
| Intervalo | Una vez seleccionada una frecuencia, puede configurar la configuración del intervalo para establecer el lapso de tiempo entre cada ingesta. Por ejemplo, si establece la frecuencia en día y configura el intervalo en 15, el flujo de datos se ejecutará cada 15 días. No puede establecer el intervalo en cero. El valor mínimo del intervalo aceptado para cada frecuencia es el siguiente:<ul><li>**Una vez**: n/a</li><li>**Minuto**: 15</li><li>**Hora**: 1</li><li>**Día**: 1</li><li>**Semana**: 1</li></ul> |
| Hora de inicio | La marca de tiempo de la ejecución proyectada, presentada en la zona horaria UTC. |
| Relleno | El relleno determina qué datos se incorporan inicialmente. Si el relleno está habilitado, todos los archivos actuales de la ruta especificada se introducirán durante la primera ingesta programada. Si se desactiva el relleno, solo se incorporarán los archivos que se carguen entre la primera ejecución de la ingesta y la hora de inicio. Los archivos cargados antes de la hora de inicio no se incorporarán. |

>[!NOTE]
>
>Para la ingesta por lotes, cada flujo de datos subsiguiente selecciona los archivos que se van a ingerir de su origen en función de su marca de tiempo **última modificación**. Esto significa que los flujos de datos por lotes seleccionan archivos del origen que son nuevos o que se han modificado desde la última ejecución del flujo. Además, debe asegurarse de que haya un lapso de tiempo suficiente entre la carga del archivo y una ejecución de flujo programada, ya que es posible que los archivos que no se han cargado completamente en su cuenta de almacenamiento en la nube antes del tiempo de ejecución del flujo programado no se recojan para su ingesta.

Cuando termine de configurar la programación de ingesta, seleccione **[!UICONTROL Siguiente]**.

## Revisión del flujo de datos

Aparece el paso **[!UICONTROL Revisar]**, que le permite revisar el nuevo flujo de datos antes de crearlo. Los detalles se agrupan en las siguientes categorías:

* **[!UICONTROL Conexión]**: muestra el tipo de origen, la ruta de acceso relevante del archivo de origen elegido y la cantidad de columnas dentro de ese archivo de origen.
* **[!UICONTROL Asignar campos de conjunto de datos y asignación]**: muestra en qué conjunto de datos se están ingiriendo los datos de origen, incluido el esquema al que se adhiere el conjunto de datos.
* **[!UICONTROL Programación]**: muestra el período activo, la frecuencia y el intervalo de la programación de ingesta.

Una vez que haya revisado el flujo de datos, haga clic en **[!UICONTROL Finalizar]** y espere un poco para que se cree el flujo de datos.

![La página de revisión.](../../../../images/tutorials/create/merkury-enterprise-identity-resolution-assets/review.png)

## Pasos siguientes

Al seguir este tutorial, ha creado correctamente un flujo de datos para traer datos por lotes de su origen de [!DNL Merkury] a Experience Platform. Para obtener recursos adicionales, visite la documentación descrita a continuación.

### Monitorización del flujo de datos

Una vez creado el flujo de datos, puede monitorizar los datos que se están ingiriendo a través de él para ver información sobre las tasas de ingesta, el éxito y los errores. Para obtener más información sobre cómo supervisar el flujo de datos, visite el tutorial sobre [supervisar cuentas y flujos de datos en la interfaz de usuario](../../monitor.md).

### Actualizar el flujo de datos

Para actualizar las configuraciones para la programación, asignación e información general de los flujos de datos, visite el tutorial sobre [actualización de flujos de datos de origen en la interfaz de usuario](../../update-dataflows.md)

### Eliminar el flujo de datos

Puede eliminar flujos de datos que ya no sean necesarios o que se hayan creado incorrectamente mediante la función **[!UICONTROL Delete]** disponible en el área de trabajo **[!UICONTROL Flujos de datos]**. Para obtener más información sobre cómo eliminar flujos de datos, visite el tutorial sobre [eliminar flujos de datos en la interfaz de usuario](../../delete.md).
