---
title: Ingesta de datos de pagos de su cuenta de Stripe a Experience Platform mediante la interfaz de usuario de.
description: Aprenda a introducir datos de pagos de su cuenta de Stripe a Experience Platform mediante la interfaz de usuario.
badge: Beta
exl-id: f20c5935-a7c0-4387-b29e-73e78cab4972
source-git-commit: 62bcaa532cdec68a2f4f62e5784c35b91b7d5743
workflow-type: tm+mt
source-wordcount: '1636'
ht-degree: 3%

---

# Ingresar datos de pagos de su cuenta de [!DNL Stripe] al Experience Platform mediante la interfaz de usuario

>[!NOTE]
>
>El origen [!DNL Stripe] está en la versión beta. Lea los [términos y condiciones](../../../../home.md#terms-and-conditions) en la descripción general de orígenes para obtener más información sobre el uso de orígenes etiquetados como beta.

Lea el siguiente tutorial para aprender a ingerir datos de pagos de su cuenta de [!DNL Stripe] en Adobe Experience Platform mediante la interfaz de usuario.

## Introducción 

Este tutorial requiere una comprensión práctica de los siguientes componentes de Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): El marco de trabajo estandarizado mediante el cual [!DNL Experience Platform] organiza los datos de la experiencia del cliente.
   * [Aspectos básicos de la composición de esquemas](../../../../../xdm/schema/composition.md): obtenga información sobre los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   * [Tutorial del editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): Aprenda a crear esquemas personalizados mediante la interfaz de usuario del editor de esquemas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): proporciona un perfil de consumidor unificado y en tiempo real basado en los datos agregados de varias fuentes.

### Autenticación

Lea la [[!DNL Stripe] descripción general](../../../../connectors/payments/stripe.md) para obtener información sobre cómo recuperar sus credenciales de autenticación.

## Conectar su cuenta de [!DNL Stripe] {#connect}

En la interfaz de usuario de Platform, seleccione **[!UICONTROL Sources]** en el panel de navegación izquierdo para acceder al área de trabajo [!UICONTROL Sources]. Puede seleccionar la categoría adecuada del catálogo en la parte izquierda de la pantalla. También puede encontrar la fuente específica con la que desea trabajar utilizando la opción de búsqueda.

En la categoría *Pagos*, seleccione **[!DNL Stripe]** y, a continuación, seleccione **[!UICONTROL Configurar]**.

>[!TIP]
>
>Los orígenes del catálogo de orígenes muestran la opción **[!UICONTROL Set up]** cuando un origen determinado aún no tiene una cuenta autenticada. Una vez que existe una cuenta autenticada, esta opción cambia a **[!UICONTROL Agregar datos]**.

![El catálogo de orígenes en la interfaz de usuario del Experience Platform, con la tarjeta de origen del Stripe seleccionada.](../../../../images/tutorials/create/stripe/catalog.png)

Aparecerá la página **[!UICONTROL Conectar cuenta de Stripe]**. En esta página, puede usar credenciales nuevas o existentes.

>[!BEGINTABS]

>[!TAB Crear una nueva cuenta]

Para crear una cuenta nueva, selecciona **[!UICONTROL Cuenta nueva]** y proporciona un nombre, una descripción opcional y tus credenciales.

Cuando termine, seleccione **[!UICONTROL Conectarse al origen]** y deje pasar un tiempo para que se establezca la nueva conexión.

![La nueva interfaz de creación de cuentas del flujo de trabajo de orígenes.](../../../../images/tutorials/create/stripe/new.png)

| Credencial | Descripción |
| --- | --- |
| Token de acceso | Su token de acceso de [!DNL Stripe]. Para obtener información sobre cómo recuperar el token de acceso, lea la [[!DNL Stripe] guía de autenticación](../../../../connectors/payments/stripe.md). |

>[!TAB Usar una cuenta existente]

Para usar una cuenta existente, seleccione **[!UICONTROL Cuenta existente]** y luego seleccione la cuenta que desee usar del catálogo de cuentas existente.

Seleccione **[!UICONTROL Siguiente]** para continuar.

![La página de selección de cuentas existente del catálogo de orígenes.](../../../../images/tutorials/create/stripe/existing.png)

>[!ENDTABS]

## Seleccionar datos {#select-data}

Ahora que tiene acceso a su cuenta, debe identificar la ruta adecuada a los datos de [!DNL Stripe] que desea introducir. Seleccione **[!UICONTROL Ruta del recurso]** y, a continuación, seleccione el extremo desde el que desea introducir los datos. Los extremos disponibles de [!DNL Stripe] son:

* Cargos
* Suscripciones
* Reembolsos
* Transacciones de Saldo
* Clientes
* Precios

![Ventana desplegable de ruta de recursos.](../../../../images/tutorials/create/stripe/select-resource-path.png)

Una vez seleccionado el punto de conexión, la interfaz se actualiza a una pantalla de vista previa que muestra la estructura de datos del punto de conexión [!DNL Stripe] que ha seleccionado. Seleccione **[!UICONTROL Siguiente]** para continuar.

![Ventana de vista previa de los datos del Stripe.](../../../../images/tutorials/create/stripe/preview.png)

## Proporcionar detalles del conjunto de datos y flujo de datos {#provide-dataset-and-dataflow-details}

A continuación, debe proporcionar información sobre el conjunto de datos y el flujo de datos.

### Detalles del conjunto de datos {#dataset-details}

Un conjunto de datos es una construcción de almacenamiento y administración para una colección de datos, normalmente una tabla, que contiene un esquema (columnas) y campos (filas). Los datos que se incorporan correctamente en Experience Platform se almacenan dentro del lago de datos como conjuntos de datos. Durante este paso, puede crear un nuevo conjunto de datos o utilizar uno existente.

>[!BEGINTABS]

>[!TAB Usar un nuevo conjunto de datos]

Para usar un nuevo conjunto de datos, seleccione **[!UICONTROL Nuevo conjunto de datos]** y proporcione un nombre y una descripción opcional para su conjunto de datos. También debe seleccionar un esquema del Modelo de datos de experiencia (XDM) al que se adhiera el conjunto de datos.

![La nueva interfaz de selección de conjuntos de datos.](../../../../images/tutorials/create/stripe/new-dataset.png)

| Nuevos detalles del conjunto de datos | Descripción |
| --- | --- |
| Nombre del conjunto de datos de salida | Nombre del nuevo conjunto de datos. |
| Descripción | (Opcional) Una breve explicación del nuevo conjunto de datos. |
| Esquema | Una lista desplegable de esquemas que existen en su organización. También puede crear su propio esquema antes del proceso de configuración de origen. Para obtener más información, lea la guía sobre [creación de un esquema XDM en la interfaz de usuario](../../../../../xdm/tutorials/create-schema-ui.md). |

>[!TAB Usar un conjunto de datos existente]

Si ya tiene un conjunto de datos, seleccione **[!UICONTROL Conjunto de datos existente]** y, a continuación, utilice la opción **[!UICONTROL Búsqueda avanzada]** para ver una ventana de todos los conjuntos de datos de su organización, incluidos sus detalles respectivos, como si están habilitados para la ingesta en el Perfil del cliente en tiempo real o no.

![Interfaz de selección de conjuntos de datos existente.](../../../../images/tutorials/create/stripe/existing-dataset.png)

>[!ENDTABS]

+++Seleccione esta opción para habilitar la Ingesta de perfiles, los diagnósticos de error y la ingesta parcial.

Si el conjunto de datos está habilitado para Perfil del cliente en tiempo real, durante este paso, puede alternar **[!UICONTROL Conjunto de datos de perfil]** para habilitar los datos para la ingesta de perfiles. También puede usar este paso para habilitar **[!UICONTROL diagnósticos de error]** y **[!UICONTROL ingesta parcial]**.

* **[!UICONTROL Diagnósticos de error]**: seleccione **[!UICONTROL Diagnósticos de error]** para indicar a la fuente que produzca diagnósticos de error a los que pueda hacer referencia posteriormente al supervisar la actividad del conjunto de datos y el estado del flujo de datos.
* **[!UICONTROL Ingesta parcial]**: La ingesta parcial por lotes es la capacidad de ingerir datos que contengan errores, hasta un determinado umbral configurable. Esta función le permite introducir correctamente todos los datos precisos en Experience Platform, mientras que todos los datos incorrectos se agrupan por separado con información sobre los motivos por los que no son válidos.

+++

### Detalles del flujo de datos {#dataflow-details}

Una vez configurado el conjunto de datos, debe proporcionar detalles sobre el flujo de datos, incluido un nombre, una descripción opcional y configuraciones de alerta.

![El paso de configuración de detalles del flujo de datos.](../../../../images/tutorials/create/stripe/dataflow-detail.png)

| Configuraciones de flujo de datos | Descripción |
| --- | --- |
| Nombre de flujo de datos | Nombre del flujo de datos.  De forma predeterminada, se utiliza el nombre del archivo que se está importando. |
| Descripción | (Opcional) Una breve descripción del flujo de datos. |
| Alertas | El Experience Platform puede generar alertas basadas en eventos a las que los usuarios pueden suscribirse. Todas estas opciones requieren un flujo de datos en ejecución para almacenarlas en déclencheur.  Para obtener más información, lea la [descripción general de las alertas](../../alerts.md) <ul><li>**Inicio de ejecución del flujo de datos de origen**: seleccione esta alerta para recibir una notificación cuando comience la ejecución del flujo de datos.</li><li>**Ejecución correcta del flujo de datos de origen**: seleccione esta alerta para recibir una notificación si el flujo de datos termina sin errores.</li><li>**Error al ejecutar el flujo de datos de origen**: seleccione esta alerta para recibir una notificación si la ejecución del flujo de datos termina con errores.</li></ul> |

Cuando termine, seleccione **[!UICONTROL Siguiente]** para continuar.

## Asignación de campos a un esquema XDM {#mapping}

Aparecerá el paso **[!UICONTROL Mapping]**. Utilice la interfaz de asignación para asignar los datos de origen a los campos de esquema adecuados antes de introducir esos datos en Experience Platform. Para obtener una guía detallada sobre cómo usar la interfaz de asignación, lee la [guía de la interfaz de usuario de la preparación de datos](../../../../../data-prep/ui/mapping.md) para obtener más información.

![Interfaz de asignación del flujo de trabajo de orígenes.](../../../../images/tutorials/create/stripe/mapping.png)

## Configurar programación de ingesta {#scheduling}

A continuación, utilice la interfaz de programación para crear una programación de ingesta para el flujo de datos.

Seleccione el menú desplegable de frecuencia para configurar la frecuencia de ingesta del flujo de datos.

![Menú desplegable de frecuencia.](../../../../images/tutorials/create/stripe/frequency.png)

También puede seleccionar el icono de calendario y utilizar un calendario emergente para configurar la hora de inicio de la ingesta.

![Calendario configurable para la programación.](../../../../images/tutorials/create/stripe/calendar.png)

| Configuración de programación | Descripción |
| --- | --- |
| Frecuencia | Configure la frecuencia para indicar con qué frecuencia debe ejecutarse el flujo de datos. Puede establecer su frecuencia en: <ul><li>**Una vez**: establezca su frecuencia en `once` para crear una ingesta única. Las configuraciones para intervalo y relleno no están disponibles al crear un flujo de datos de ingesta único. De forma predeterminada, la frecuencia de programación se establece en una vez.</li><li>**Minuto**: establezca su frecuencia en `minute` para programar el flujo de datos e ingerir datos por minuto.</li><li>**Hora**: Establezca su frecuencia en `hour` para programar su flujo de datos e ingerir datos por hora.</li><li>**Día**: Establezca su frecuencia en `day` para programar su flujo de datos e ingerir datos por día.</li><li>**Semana**: establezca su frecuencia en `week` para programar el flujo de datos e ingerir datos por semana.</li></ul> |
| Intervalo | Una vez seleccionada una frecuencia, puede configurar la configuración del intervalo para establecer el lapso de tiempo entre cada ingesta. Por ejemplo, si establece la frecuencia en día y configura el intervalo en 15, el flujo de datos se ejecutará cada 15 días. **Nota**: No puede establecer el intervalo en cero. |
| Hora de inicio | La marca de tiempo de la ejecución proyectada, presentada en la zona horaria UTC. |
| Relleno | El relleno determina qué datos se incorporan inicialmente. Si el relleno está habilitado, todos los archivos actuales de la ruta especificada se introducirán durante la primera ingesta programada. Si se desactiva el relleno, solo se incorporarán los archivos que se carguen entre la primera ejecución de la ingesta y la hora de inicio. Los archivos cargados antes de la hora de inicio no se incorporarán. |

Una vez que haya configurado la programación de ingesta del flujo de datos, seleccione **[!UICONTROL Siguiente]**.

![Interfaz de programación del flujo de trabajo de orígenes.](../../../../images/tutorials/create/stripe/scheduling.png)


## Revisión del flujo de datos

El paso final del proceso de creación del flujo de datos es revisar el flujo de datos antes de ejecutarlo. Use el paso **[!UICONTROL Revisar]** para revisar los detalles del nuevo flujo de datos antes de que se ejecute. Los detalles se agrupan en las siguientes categorías:

* **Conexión**: muestra el tipo de origen, la ruta de acceso relevante del archivo de origen elegido y el número de columnas dentro de ese archivo de origen.
* **Asignar campos de conjunto de datos y asignación**: muestra en qué conjunto de datos se están ingiriendo los datos de origen, incluido el esquema al que se adhiere el conjunto de datos.
* **Programación**: muestra el período activo, la frecuencia y el intervalo de la programación de ingesta.

Una vez que haya revisado el flujo de datos, seleccione **[!UICONTROL Finalizar]** y espere un poco para que se cree el flujo de datos.

![Paso de revisión del flujo de trabajo de orígenes.](../../../../images/tutorials/create/stripe/review.png)

## Pasos siguientes

Al seguir este tutorial, ha creado correctamente un flujo de datos para llevar los datos de pagos de su origen de [!DNL Stripe] al Experience Platform. Para obtener recursos adicionales, visite la documentación descrita a continuación.

### Monitorización del flujo de datos

Una vez creado el flujo de datos, puede monitorizar los datos que se están ingiriendo a través de él para ver información sobre las tasas de ingesta, el éxito y los errores. Para obtener más información sobre cómo supervisar el flujo de datos, visite el tutorial sobre [supervisar cuentas y flujos de datos en la interfaz de usuario](../../../../../dataflows/ui/monitor-sources.md).

### Actualizar el flujo de datos

Para actualizar configuraciones para la programación, asignación e información general de los flujos de datos, visite el tutorial sobre [actualización de flujos de datos de origen en la interfaz de usuario](../../update-dataflows.md).

### Eliminar el flujo de datos

Puede eliminar flujos de datos que ya no sean necesarios o que se hayan creado incorrectamente mediante la función **[!UICONTROL Delete]** disponible en el área de trabajo **[!UICONTROL Flujos de datos]**. Para obtener más información sobre cómo eliminar flujos de datos, visite el tutorial sobre [eliminar flujos de datos en la interfaz de usuario](../../delete.md).
