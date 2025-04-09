---
title: Conexión de perfiles de usuario de Algolia a Experience Platform mediante la IU
description: Aprenda a conectar la intención de los usuarios de Algolia a Experience Platform
hide: true
hidefromtoc: true
source-git-commit: a55f0b37614bb43a66d7d2e9cf106484b4d6e8dc
workflow-type: tm+mt
source-wordcount: '1133'
ht-degree: 1%

---

# Ingesta de datos de [!DNL Algolia User Profiles] en Experience Platform mediante la IU

Lea este tutorial para aprender a ingerir datos de pagos de su cuenta de [!DNL Algolia User Profiles] en Adobe Experience Platform mediante la interfaz de usuario.

## Introducción 

>[!IMPORTANT]
>
>Antes de comenzar, asegúrese de completar los pasos de requisitos previos descritos en la [[!DNL Algolia User Profiles] descripción general](../../../../connectors/data-partners/algolia-user-profiles.md#prerequisites).

Este tutorial requiere una comprensión práctica de los siguientes componentes de Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): El marco estandarizado mediante el cual Experience Platform organiza los datos de experiencia del cliente.
   * [Aspectos básicos de la composición de esquemas](../../../../../xdm/schema/composition.md): obtenga información sobre los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   * [Tutorial del editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): Aprenda a crear esquemas personalizados mediante la interfaz de usuario del editor de esquemas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): proporciona un perfil de consumidor unificado y en tiempo real basado en los datos agregados de varias fuentes.
* [Fuentes](../../../../home.md): Experience Platform permite la ingesta de datos de varias fuentes al tiempo que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de Experience Platform.

### Recopilar credenciales necesarias

Para conectar [!DNL Algolia] a Experience Platform, debe proporcionar valores para las siguientes credenciales:

| Credencial | Descripción |
| --- | --- |
| ID de aplicación | El id. de aplicación [!DNL Algolia] es un identificador único asignado a su cuenta [!DNL Algolia]. |
| Clave de API | La clave de API [!DNL Algolia] es una credencial que se usa para autenticar y autorizar solicitudes de API para los servicios de búsqueda e indexación de [!DNL Algolia]. |

Para obtener más información sobre estas credenciales, consulte la [!DNL Algolia] [documentación de autenticación](https://www.algolia.com/doc/tools/cli/get-started/authentication/).

## Conectar su cuenta de [!DNL Algolia]

En la interfaz de usuario de Experience Platform, seleccione **[!UICONTROL Fuentes]** en el panel de navegación izquierdo para acceder al área de trabajo *[!UICONTROL Fuentes]*. Puede seleccionar la categoría adecuada en el panel *[!UICONTROL Categorías]*. También puede utilizar la barra de búsqueda para desplazarse al origen específico que desee utilizar.

Para usar [!DNL Algolia], selecciona la tarjeta de origen de **[!UICONTROL Algolia]** en *[!UICONTROL Socios de datos e identidad]* y, a continuación, selecciona **[!UICONTROL Configurar]**.

>[!TIP]
>
>Los orígenes del catálogo de orígenes muestran la opción **[!UICONTROL Set up]** cuando un origen determinado aún no tiene una cuenta autenticada. Una vez que existe una cuenta autenticada, esta opción cambia a **[!UICONTROL Agregar datos]**.

![El catálogo de orígenes con el origen de Perfiles de usuario de Algolia seleccionado.](../../../../images/tutorials/create/algolia/user-profiles/catalog.png)

## Autenticación

### Cuenta existente

Para usar una cuenta existente, seleccione **[!UICONTROL Cuenta existente]** y luego seleccione la cuenta [!DNL Algolia User Profiles] que desee usar. Para continuar, seleccione **[!UICONTROL Siguiente]**.

![Interfaz de cuenta existente.](../../../../images/tutorials/create/algolia/user-profiles/existing-account.png)

### Nueva cuenta

Si va a crear una cuenta nueva, seleccione **[!UICONTROL Cuenta nueva]** y, a continuación, proporcione un nombre, una descripción opcional y [!DNL Algolia] credenciales. Cuando termine, seleccione **[!UICONTROL Conectarse al origen]** y deje pasar un tiempo para que se establezca la nueva conexión.

![Interfaz de la nueva cuenta.](../../../../images/tutorials/create/algolia/user-profiles/new-account.png)

## Adición de datos

Después de crear su cuenta de [!DNL Algolia User Profiles], aparece el paso **[!UICONTROL Agregar datos]**, que proporciona una interfaz para que explore los perfiles de usuario de [!DNL Algolia] que desee llevar a Experience Platform.

* La parte izquierda de la interfaz es para que usted ingrese los campos **[!UICONTROL Índices]** y **[!UICONTROL Afinidad(es)]** opcionales.
* La parte derecha de la interfaz de usuario permite previsualizar hasta 100 filas de perfiles de usuario.

Una vez que termine de seleccionar y obtener una vista previa de los datos para su ingesta, seleccione **[!UICONTROL Siguiente]**.

![Paso para seleccionar datos del flujo de trabajo.](../../../../images/tutorials/create/algolia/user-profiles/select-data.png)

### Proporcionar detalles del flujo de datos

Si está usando un conjunto de datos existente, seleccione un conjunto de datos asociado a un esquema que esté usando el grupo de campos [!DNL Algolia Profile].

![Paso del conjunto de datos existente del flujo de trabajo de orígenes.](../../../../images/tutorials/create/algolia/user-profiles/dataflow-detail-existing-dataset.png)

Si está creando un nuevo conjunto de datos, seleccione un esquema que esté utilizando el grupo de campos [!DNL Algolia Profile] que es necesario en el paso de asignación.

![El nuevo paso del conjunto de datos del flujo de trabajo de orígenes.](../../../../images/tutorials/create/algolia/user-profiles/dataflow-detail-new-dataset.png)

### Asignación de campos de datos a un esquema XDM

Utilice la interfaz de asignación para asignar los datos de origen a los campos de esquema adecuados antes de introducir datos en Experience Platform.  Para obtener más información, lea la guía de asignación [en la interfaz de usuario](../../../../../data-prep/ui/mapping.md).

![Paso de asignación del flujo de trabajo de orígenes.](../../../../images/tutorials/create/algolia/user-profiles/mapping.png)

### Programar ejecuciones de ingesta

A continuación, utilice la interfaz de programación para definir la programación de ingesta del flujo de datos.

<!-- The Scheduling step allows for configuration of the data/time to execute the [!DNL Algolia Uer Profiles] Source connector. There is configuration to backfill the data from [!DNL Algolia] which will pull all the profiles from the source system.  If the source is scheduled, then it will retrieve modified profiles from the [!DNL Algolia] based on the configured time interval. -->

![Paso de programación del flujo de trabajo de orígenes.](../../../../images/tutorials/create/algolia/user-profiles/scheduling.png)

| Configuración de programación | Descripción |
| --- | --- |
| Frecuencia | Configure la frecuencia para indicar con qué frecuencia debe ejecutarse el flujo de datos. Puede establecer su frecuencia en: <ul><li>**Una vez**: establezca su frecuencia en `once` para crear una ingesta única. Las configuraciones para intervalo y relleno no están disponibles al crear un flujo de datos de ingesta único. De forma predeterminada, la frecuencia de programación se establece en una vez.</li><li>**Minuto**: establezca su frecuencia en `minute` para programar el flujo de datos e ingerir datos por minuto.</li><li>**Hora**: establezca su frecuencia en `hour` para programar el flujo de datos e ingerir datos por hora.</li><li>**Día**: Establezca su frecuencia en `day` para programar su flujo de datos e ingerir datos por día.</li><li>**Semana**: establezca su frecuencia en `week` para programar el flujo de datos e ingerir datos por semana.</li></ul> |
| Intervalo | Una vez seleccionada una frecuencia, puede configurar la configuración del intervalo para establecer el lapso de tiempo entre cada ingesta. Por ejemplo, si establece la frecuencia en día y configura el intervalo en 15, el flujo de datos se ejecutará cada 15 días. No puede establecer el intervalo en cero. El valor mínimo del intervalo aceptado para cada frecuencia es el siguiente:<ul><li>**Una vez**: n/a</li><li>**Minuto**: 15</li><li>**Hora**: 1</li><li>**Día**: 1</li><li>**Semana**: 1</li></ul> |
| Hora de inicio | La marca de tiempo de la ejecución proyectada, presentada en la zona horaria UTC. |
| Relleno | El relleno determina qué datos se incorporan inicialmente. Si el relleno está habilitado, todos los archivos actuales de la ruta especificada se introducirán durante la primera ingesta programada. Si se desactiva el relleno, solo se incorporarán los archivos que se carguen entre la primera ejecución de la ingesta y la hora de inicio. Los archivos cargados antes de la hora de inicio no se incorporarán. |

### Revisión del flujo de datos

Utilice la página Revisar para obtener un resumen del flujo de datos antes de la ingesta. Los detalles se agrupan en las siguientes categorías:

* **Conexión**: muestra el tipo de origen, la ruta de acceso relevante del archivo de origen elegido y el número de columnas dentro de ese archivo de origen.
* **Asignar campos de conjunto de datos y asignación**: muestra en qué conjunto de datos se están ingiriendo los datos de origen, incluido el esquema al que se adhiere el conjunto de datos.
* **Programación**: muestra ese período, frecuencia e intervalo activos de la programación de ingesta.

Una vez que haya revisado el flujo de datos, seleccione **[!UICONTROL Finalizar]** y espere un poco para que se cree el flujo de datos.

![Paso de revisión del flujo de trabajo de orígenes.](../../../../images/tutorials/create/algolia/user-profiles/review.png)

## Pasos siguientes

Al seguir este tutorial, ha creado correctamente un flujo de datos para llevar los datos de intención de su origen de [!DNL Algolia] a Experience Platform. Para obtener recursos adicionales, visite la documentación descrita a continuación.

### Monitorización del flujo de datos

Una vez creado el flujo de datos, puede monitorizar los datos que se están ingiriendo a través de él para ver información sobre las tasas de ingesta, el éxito y los errores. Para obtener más información sobre cómo supervisar el flujo de datos, visite el tutorial sobre [supervisar cuentas y flujos de datos en la interfaz de usuario](../../../../../dataflows/ui/monitor-sources.md).

### Actualizar el flujo de datos

Para actualizar configuraciones para la programación, asignación e información general de los flujos de datos, visite el tutorial sobre [actualización de flujos de datos de origen en la interfaz de usuario](../../update-dataflows.md).

### Eliminar el flujo de datos

Puede eliminar flujos de datos que ya no sean necesarios o que se hayan creado incorrectamente mediante la función **[!UICONTROL Delete]** disponible en el área de trabajo **[!UICONTROL Flujos de datos]**. Para obtener más información sobre cómo eliminar flujos de datos, visite el tutorial sobre [eliminar flujos de datos en la interfaz de usuario](../../delete.md).
