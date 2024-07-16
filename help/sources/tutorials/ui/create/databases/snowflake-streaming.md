---
title: Transmita datos de la base de datos de Snowflake a Experience Platform mediante la interfaz de usuario
type: Tutorial
description: Aprenda a transmitir datos de su base de datos de Snowflake a Experience Platform
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 49d488f1-90d8-452a-9f3e-02afdcc79b09
source-git-commit: 62bcaa532cdec68a2f4f62e5784c35b91b7d5743
workflow-type: tm+mt
source-wordcount: '1604'
ht-degree: 3%

---

# Transmitir datos de la base de datos [!DNL Snowflake] al Experience Platform mediante la interfaz de usuario

Aprenda a utilizar la interfaz de usuario para transmitir datos de la base de datos [!DNL Snowflake] a Adobe Experience Platform siguiendo esta guía.

## Introducción 

Este tutorial requiere una comprensión práctica de los siguientes componentes de Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): El marco de trabajo estandarizado mediante el cual [!DNL Experience Platform] organiza los datos de la experiencia del cliente.
   * [Aspectos básicos de la composición de esquemas](../../../../../xdm/schema/composition.md): obtenga información sobre los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   * [Tutorial del editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): Aprenda a crear esquemas personalizados mediante la interfaz de usuario del editor de esquemas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): proporciona un perfil de consumidor unificado y en tiempo real basado en los datos agregados de varias fuentes.

### Autenticación

Lea la guía sobre la configuración de [requisitos previos para [!DNL Snowflake] datos de transmisión](../../../../connectors/databases/snowflake-streaming.md) para obtener información sobre los pasos que debe completar antes de poder ingerir datos de transmisión de [!DNL Snowflake] a Experience Platform.

## Usar el origen [!DNL Snowflake Streaming] para transmitir datos de [!DNL Snowflake] al Experience Platform

En la interfaz de usuario de Platform, seleccione **[!UICONTROL Sources]** en el panel de navegación izquierdo para acceder al área de trabajo [!UICONTROL Sources]. Puede seleccionar la categoría adecuada del catálogo en la parte izquierda de la pantalla. También puede encontrar la fuente específica con la que desea trabajar utilizando la opción de búsqueda.

En la categoría *Bases de datos*, seleccione **[!DNL Snowflake Streaming]** y, a continuación, seleccione **[!UICONTROL Agregar datos]**.

>[!TIP]
>
>Las fuentes que no tienen una cuenta autenticada en el catálogo de fuentes muestran la opción **[!UICONTROL Configurar]**. Una vez que existe una cuenta autenticada, esta opción cambia a **[!UICONTROL Agregar datos]**.

![El catálogo de orígenes en la interfaz de usuario de Experience Platform, con la tarjeta de origen de flujo de Snowflake seleccionada.](../../../../images/tutorials/create/snowflake-streaming/catalog.png)

Aparecerá la página **[!UICONTROL Conectar cuenta de flujo de Snowflake]**. En esta página, puede usar credenciales nuevas o existentes.

>[!BEGINTABS]

>[!TAB Crear una nueva cuenta]

Para crear una cuenta nueva, selecciona **[!UICONTROL Cuenta nueva]** y proporciona un nombre, una descripción opcional y tus credenciales.

Cuando termine, seleccione **[!UICONTROL Conectarse al origen]** y deje pasar un tiempo para que se establezca la nueva conexión.

![La nueva interfaz de creación de cuentas del flujo de trabajo de orígenes.](../../../../images/tutorials/create/snowflake-streaming/new.png)

| Credencial | Descripción |
| --- | --- |
| Cuenta | El nombre de su cuenta de [!DNL Snowflake]. |
| Almacén | Nombre de su almacén de [!DNL Snowflake]. Los almacenes administran la ejecución de consultas en [!DNL Snowflake]. Cada almacén de [!DNL Snowflake] es independiente entre sí y se debe tener acceso a él de forma individual para llevar los datos al Experience Platform. |
| Base de datos | Nombre de su base de datos [!DNL Snowflake]. La base de datos contiene los datos que desea llevar al Experience Platform. |
| Esquema | (Opcional) El esquema de base de datos asociado con su cuenta de [!DNL Snowflake]. |
| Nombre de usuario | El nombre de usuario de su cuenta de [!DNL Snowflake]. |
| Contraseña | Contraseña de su cuenta de [!DNL Snowflake]. |
| Función | (Opcional) Una función personalizada que se puede proporcionar a un usuario para una conexión determinada. Si no se proporciona, el valor predeterminado es `public`. |

Para obtener más información acerca de la creación de cuentas, lea la sección sobre [configuración de funciones](../../../../connectors/databases/snowflake-streaming.md#configure-role-settings) en la descripción general de [!DNL Snowflake Streaming].

>[!TAB Usar una cuenta existente]

Para usar una cuenta existente, seleccione **[!UICONTROL Cuenta existente]** y luego seleccione la cuenta que desee del catálogo de cuentas existente.

Seleccione **[!UICONTROL Siguiente]** para continuar.

![La página de selección de cuentas existente del catálogo de orígenes.](../../../../images/tutorials/create/snowflake-streaming/existing.png)

>[!ENDTABS]

## Seleccionar datos {#select-data}

>[!IMPORTANT]
>
>Debe existir una columna de marca de tiempo en la tabla de origen para poder crear un flujo de datos de flujo continuo. La marca de tiempo es necesaria para que el Experience Platform sepa cuándo se incorporarán los datos y cuándo se transmitirán los datos incrementales. Puede agregar de forma retroactiva una columna de marca de tiempo para una conexión existente y crear un nuevo flujo de datos.

Aparecerá el paso [!UICONTROL Seleccionar datos]. En este paso, debe seleccionar los datos que desea importar en Experience Platform, configurar las marcas de tiempo y las zonas horarias, y proporcionar un archivo de datos de origen de muestra para la ingesta de datos sin procesar.

Utilice el directorio de base de datos de la izquierda de la pantalla y seleccione la tabla que desea importar al Experience Platform.

![Interfaz de datos de selección con una tabla de base de datos seleccionada.](../../../../images/tutorials/create/snowflake-streaming/select-table.png)

A continuación, seleccione el tipo de columna de marca de tiempo de la tabla. Puede seleccionar entre dos tipos de columnas de marca de tiempo: `TIMESTAMP_NTZ` o `TIMESTAMP_LTZ`. Si selecciona un tipo de columna de `TIMESTAMP_NTZ`, también debe proporcionar una zona horaria. Las columnas no deben tener una restricción nula. Para obtener más información, lea la sección sobre [limitaciones y preguntas más frecuentes]

También puede configurar las opciones de relleno durante este paso. El relleno determina qué datos se incorporan inicialmente. Si el relleno está habilitado, todos los archivos actuales de la ruta especificada se introducirán durante la primera ingesta programada. Si no es así, solo se incorporarán los archivos que se carguen entre la primera ejecución de la ingesta y la hora de inicio. Los archivos cargados antes de la hora de inicio no se incorporarán.

Seleccione la opción **[!UICONTROL Relleno]** para habilitar el relleno.

![Los pasos de configuración de marca de tiempo, zona horaria y relleno.](../../../../images/tutorials/create/snowflake-streaming/timezone.png)

Finalmente, seleccione **[!UICONTROL Elegir archivo]** para cargar un origen de datos de ejemplo para ayudar a crear el conjunto de asignaciones, que se utilizará en un paso posterior para asignar los datos originales al modelo de datos de experiencia (XDM).

Cuando termine, seleccione **[!UICONTROL Siguiente]** para continuar.

![Vista previa de los datos de ejemplo de origen.](../../../../images/tutorials/create/snowflake-streaming/preview.png)

## Proporcionar detalles del conjunto de datos y flujo de datos {#provide-dataset-and-dataflow-details}

A continuación, debe proporcionar información sobre el conjunto de datos y el flujo de datos.

### Detalles del conjunto de datos {#dataset-details}

Un conjunto de datos es una construcción de almacenamiento y administración para una colección de datos, normalmente una tabla, que contiene un esquema (columnas) y campos (filas). Los datos que se incorporan correctamente al Experience Platform se conservan dentro del lago de datos como conjuntos de datos. Durante este paso, puede crear un nuevo conjunto de datos o utilizar uno existente.

>[!BEGINTABS]

>[!TAB Usar un nuevo conjunto de datos]

Para usar un nuevo conjunto de datos, seleccione **[!UICONTROL Nuevo conjunto de datos]** y, a continuación, proporcione un nombre y una descripción opcional para su conjunto de datos. También debe seleccionar un esquema del Modelo de datos de experiencia (XDM) al que se adhiera el conjunto de datos.

![La nueva interfaz de selección de conjuntos de datos.](../../../../images/tutorials/create/snowflake-streaming/new-dataset.png)

| Nuevos detalles del conjunto de datos | Descripción |
| --- | --- |
| Nombre del conjunto de datos de salida | Nombre del nuevo conjunto de datos. |
| Descripción | (Opcional) Una breve descripción general del nuevo conjunto de datos. |
| Esquema | Una lista desplegable de esquemas que existen en su organización. También puede crear su propio esquema antes del proceso de configuración de origen. Para obtener más información, lea la guía sobre [creación de un esquema XDM en la interfaz de usuario](../../../../../xdm/tutorials/create-schema-ui.md). |

>[!TAB Usar un conjunto de datos existente]

Si ya tiene un conjunto de datos, seleccione **[!UICONTROL Conjunto de datos existente]** y, a continuación, utilice la opción **[!UICONTROL Búsqueda avanzada]** para ver una ventana de todos los conjuntos de datos de su organización, incluidos sus detalles respectivos, como si están habilitados para su ingesta en el Perfil del cliente en tiempo real.

![Interfaz de selección de conjuntos de datos existente.](../../../../images/tutorials/create/snowflake-streaming/existing-dataset.png)

>[!ENDTABS]

+++Seleccione esta opción para habilitar la Ingesta de perfiles, los diagnósticos de error y la ingesta parcial.

Si el conjunto de datos está habilitado para Perfil del cliente en tiempo real, durante este paso, puede alternar **[!UICONTROL Conjunto de datos de perfil]** para habilitar los datos para la ingesta de perfiles. También puede usar este paso para habilitar **[!UICONTROL diagnósticos de error]** y **[!UICONTROL ingesta parcial]**.

* **[!UICONTROL Diagnósticos de error]**: seleccione **[!UICONTROL Diagnósticos de error]** para indicar a la fuente que produzca diagnósticos de error a los que pueda hacer referencia posteriormente al supervisar la actividad del conjunto de datos y el estado del flujo de datos.
* **[!UICONTROL Ingesta parcial]**: La ingesta parcial por lotes es la capacidad de ingerir datos que contengan errores, hasta un determinado umbral configurable. Esta función le permite introducir correctamente todos los datos precisos en Experience Platform, mientras que todos los datos incorrectos se agrupan por separado con información sobre los motivos por los que no son válidos.

+++

### Detalles del flujo de datos {#dataflow-details}

Una vez configurado el conjunto de datos, debe proporcionar detalles sobre el flujo de datos, incluido un nombre, una descripción opcional y configuraciones de alerta.

![El paso de configuración de detalles del flujo de datos.](../../../../images/tutorials/create/snowflake-streaming/dataflow-details.png)

| Configuraciones de flujo de datos | Descripción |
| --- | --- |
| Nombre de flujo de datos | Nombre del flujo de datos.  De forma predeterminada, se utiliza el nombre del archivo que se está importando. |
| Descripción | (Opcional) Una breve descripción del flujo de datos. |
| Alertas | El Experience Platform puede generar alertas basadas en eventos a las que los usuarios pueden suscribirse. Estas opciones requieren un flujo de datos en ejecución para almacenarlas en déclencheur. Para obtener más información, lea la [descripción general de las alertas](../../alerts.md) <ul><li>**Inicio de ejecución del flujo de datos de origen**: seleccione esta alerta para recibir una notificación cuando comience la ejecución del flujo de datos.</li><li>**Ejecución correcta del flujo de datos de origen**: seleccione esta alerta para recibir una notificación si el flujo de datos termina sin errores.</li><li>**Error al ejecutar el flujo de datos de origen**: seleccione esta alerta para recibir una notificación si la ejecución del flujo de datos termina con errores.</li></ul> |

Cuando termine, seleccione **[!UICONTROL Siguiente]** para continuar.

## Asignación de campos a un esquema XDM {#mapping}

Aparecerá el paso [!UICONTROL Mapping]. Use la interfaz de asignación para asignar los datos de origen a los campos de esquema adecuados antes de ingerir esos datos en el Experience Platform y, a continuación, seleccione **[!UICONTROL Siguiente]**. Para obtener una guía detallada sobre cómo usar la interfaz de asignación, lee la [guía de la interfaz de usuario de la preparación de datos](../../../../../data-prep/ui/mapping.md) para obtener más información.

![Interfaz de asignación del flujo de trabajo de orígenes.](../../../../images/tutorials/create/snowflake-streaming/mapping.png)

## Revisión del flujo de datos {#review}

El paso final del proceso de creación del flujo de datos es revisar el flujo de datos antes de ejecutarlo. Use el paso **[!UICONTROL Revisar]** para revisar los detalles del nuevo flujo de datos antes de que se ejecute. Los detalles se agrupan en las siguientes categorías:

* **Conexión**: muestra el tipo de origen, la ruta de acceso relevante del archivo de origen elegido y el número de columnas dentro de ese archivo de origen.
* **Asignar campos de conjunto de datos y asignación**: muestra en qué conjunto de datos se están ingiriendo los datos de origen, incluido el esquema al que se adhiere el conjunto de datos.

Una vez que haya revisado el flujo de datos, seleccione **[!UICONTROL Finalizar]** y espere un poco para que se cree el flujo de datos.

![Paso de revisión del flujo de trabajo de orígenes.](../../../../images/tutorials/create/snowflake-streaming/review.png)

## Pasos siguientes

Al seguir este tutorial, ha creado correctamente un flujo de datos de flujo continuo para [!DNL Snowflake] datos. Para obtener recursos adicionales, lea la documentación siguiente.

### Monitorización del flujo de datos

Una vez creado el flujo de datos, puede monitorizar los datos que se están ingiriendo a través de él para ver información sobre las tasas de ingesta, el éxito y los errores. Para obtener más información sobre cómo supervisar los flujos de datos de flujo continuo, visite el tutorial sobre [supervisión de flujos de datos de flujo continuo en la interfaz de usuario](../../monitor-streaming.md).

### Actualizar el flujo de datos

Para actualizar configuraciones para la programación, asignación e información general de los flujos de datos, visite el tutorial sobre [actualización de flujos de datos de origen en la interfaz de usuario](../../update-dataflows.md).

### Eliminar el flujo de datos

Puede eliminar flujos de datos que ya no sean necesarios o que se hayan creado incorrectamente mediante la función **[!UICONTROL Delete]** disponible en el área de trabajo **[!UICONTROL Flujos de datos]**. Para obtener más información sobre cómo eliminar flujos de datos, visite el tutorial sobre [eliminar flujos de datos en la interfaz de usuario](../../delete.md).
