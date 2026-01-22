---
title: Transmita Datos De Talon.One A Experience Platform Mediante La Interfaz De Usuario
description: Aprenda a transmitir datos de Talon.One a Adobe Experience Platform mediante la interfaz de usuario. Esta guía cubre la configuración, la selección de datos y la configuración del flujo de datos.
badge: Beta
hide: true
hidefromtoc: true
source-git-commit: 554d86e2f07966ee08940a30fe06050570129e41
workflow-type: tm+mt
source-wordcount: '961'
ht-degree: 2%

---

# Transmitir datos de [!DNL Talon.One] a Experience Platform mediante la interfaz de usuario

>[!AVAILABILITY]
>
>El origen [!DNL Talon.One] está en la versión beta. Lea los [términos y condiciones](../../../../home.md#terms-and-conditions) en la descripción general de orígenes para obtener más información sobre el uso de orígenes etiquetados como beta.

Lea esta guía para obtener información sobre cómo conectar y transmitir los datos de [!DNL Talon.One] a Adobe Experience Platform mediante el área de trabajo de orígenes en la interfaz de usuario.

## Introducción

Este tutorial requiere una comprensión práctica de los siguientes componentes de Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): El marco estandarizado mediante el cual Experience Platform organiza los datos de experiencia del cliente.
   * [Aspectos básicos de la composición de esquemas](../../../../../xdm/schema/composition.md): obtenga información sobre los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   * [Tutorial del editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): Aprenda a crear esquemas personalizados mediante la interfaz de usuario del editor de esquemas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): proporciona un perfil de consumidor unificado y en tiempo real basado en los datos agregados de varias fuentes.

>[!IMPORTANT]
>
>Lea la [[!DNL Talon.One] descripción general](../../../../connectors/loyalty/talon-one.md) para obtener información sobre los pasos previos que debe seguir antes de conectar su cuenta a Experience Platform.

## Navegar por el catálogo de fuentes

En la interfaz de usuario de Experience Platform, seleccione **[!UICONTROL Sources]** en el panel de navegación izquierdo para acceder al área de trabajo *[!UICONTROL Sources]*. Seleccione la categoría adecuada en el panel *[!UICONTROL Categories]*. También puede utilizar la barra de búsqueda para desplazarse hasta el origen específico que desee utilizar.

Para transmitir datos de [!DNL Talon.One], seleccione la tarjeta de origen **[!UICONTROL Talon.One Streaming Events]** en *[!UICONTROL Loyalty]* y, a continuación, seleccione **[!UICONTROL Add data]**.

>[!TIP]
>
>Los orígenes del catálogo de orígenes muestran la opción **[!UICONTROL Set up]** cuando un origen determinado aún no tiene una cuenta autenticada. Una vez creada una cuenta autenticada, esta opción cambia a **[!UICONTROL Add data]**.

![El catálogo de orígenes de la interfaz de usuario con la tarjeta Eventos de transmisión Talon.One seleccionada.](../../../../images/tutorials/create/talon-one-streaming/catalog.png)

## Seleccionar datos

A continuación, utilice la interfaz *[!UICONTROL Select data]* para cargar un archivo JSON de muestra y definir el esquema de origen. Durante este paso, puede utilizar la interfaz de vista previa para ver la estructura de archivos de la carga útil. Cuando termine, seleccione **[!UICONTROL Next]**.

![Paso para seleccionar datos del flujo de trabajo de orígenes](../../../../images/tutorials/create/talon-one-streaming/select-data.png)

## Detalles del flujo de datos

A continuación, debe proporcionar información sobre el conjunto de datos y el flujo de datos.

### Detalles del conjunto de datos

Un conjunto de datos es una construcción de almacenamiento y administración para una colección de datos, normalmente una tabla, que contiene un esquema (columnas/campos) y registros (filas). Los datos que se incorporan correctamente a Experience Platform se conservan dentro del lago de datos como conjuntos de datos.

Durante este paso, puede utilizar un conjunto de datos existente o crear uno nuevo.

>[!NOTE]
>
>Independientemente de si utiliza un conjunto de datos existente o crea uno nuevo, debe asegurarse de que el conjunto de datos esté **habilitado para la ingesta de Profile**.

+++Seleccione para habilitar la Ingesta de perfiles, diagnósticos de error e ingesta parcial.

Si el conjunto de datos está habilitado para Perfil del cliente en tiempo real, durante este paso, puede alternar **[!UICONTROL Profile dataset]** para habilitar los datos para la ingesta de perfiles. También puede utilizar este paso para habilitar **[!UICONTROL Error diagnostics]** y **[!UICONTROL Partial ingestion]**.

* **[!UICONTROL Error diagnostics]**: seleccione **[!UICONTROL Error diagnostics]** para indicar al origen que produzca diagnósticos de error a los que pueda hacer referencia posteriormente al supervisar la actividad del conjunto de datos y el estado del flujo de datos.
* **[!UICONTROL Partial ingestion]**: la ingesta parcial por lotes es la capacidad de ingerir datos que contengan errores, hasta un determinado umbral configurable. Esta función le permite introducir correctamente todos los datos exactos en Experience Platform, mientras que todos los datos incorrectos se agrupan por separado con información sobre los motivos por los que no son válidos.

+++

### Detalles del flujo de datos

Una vez configurado el conjunto de datos, debe proporcionar detalles sobre el flujo de datos, incluido un nombre, una descripción opcional y configuraciones de alerta.

![Interfaz de detalles del flujo de datos](../../../../images/tutorials/create/talon-one-streaming/dataflow-details.png)

| Configuraciones de flujo de datos | Descripción |
| --- | --- |
| Nombre de flujo de datos | Nombre del flujo de datos. De forma predeterminada, se utiliza el nombre del archivo que se está importando. |
| Descripción | (Opcional) Una breve descripción del flujo de datos. |
| Alertas | Experience Platform puede producir alertas basadas en eventos a las que los usuarios pueden suscribirse, estas opciones permiten que un flujo de datos en ejecución las almacene en déclencheur.  Para obtener más información, lea la [descripción general de las alertas](../../alerts.md) <ul><li>**Inicio de ejecución del flujo de datos de origen**: seleccione esta alerta para recibir una notificación cuando comience la ejecución del flujo de datos.</li><li>**Ejecución correcta del flujo de datos de origen**: seleccione esta alerta para recibir una notificación si el flujo de datos termina sin errores.</li><li>**Error al ejecutar el flujo de datos de origen**: seleccione esta alerta para recibir una notificación si la ejecución del flujo de datos termina con errores.</li></ul> |

{style="table-layout:auto"}

## Asignación

Utilice la interfaz de asignación para asignar los datos de origen a los campos de esquema adecuados antes de introducir datos en Experience Platform. Para obtener más información, lea la guía de asignación [en la interfaz de usuario](../../../../../data-prep/ui/mapping.md).

<!--
>[!TIP]
>
>You can download the [Events and Profile mappings](../../../../images/tutorials/create/capillary/mappings.zip) for [!DNL Capillary] and [import the files to Data Prep](../../../../../data-prep/ui/mapping.md#import-mapping) when you are ready to map your data.
-->

![Interfaz de asignación para la transmisión de Talon.One.](../../../../images/tutorials/create/talon-one-streaming/mapping.png)

## Revisar

Aparece el paso *[!UICONTROL Review]*, que le permite revisar los detalles del flujo de datos antes de crearlo. Los detalles se agrupan en las siguientes categorías:

* **[!UICONTROL Connection]**: muestra el nombre de cuenta, la plataforma de origen y el nombre de origen.
* **[!UICONTROL Assign dataset and map fields]**: muestra el conjunto de datos de destino y el esquema al que se adhiere el conjunto de datos.

Después de confirmar que los detalles son correctos, seleccione **[!UICONTROL Finish]**.

![Paso de revisión en el flujo de trabajo de orígenes.](../../../../images/tutorials/create/talon-one-streaming/review.png)

## Recupere la URL del extremo de flujo continuo

Con la conexión creada, aparecerá la página de detalles de orígenes. Esta página muestra detalles de la conexión recién creada, incluidos los flujos de datos ejecutados anteriormente, el ID y la URL del extremo de flujo continuo.

![La dirección URL del extremo de flujo continuo.](../../../../images/tutorials/create/talon-one-streaming/streaming-endpoint.png)

## Monitorización del flujo de datos

Una vez creado el flujo de datos, puede monitorizar los datos que se están ingiriendo a través de él para ver información sobre las tasas de ingesta, el éxito y los errores. Para obtener más información sobre cómo supervisar el flujo de datos, consulte el tutorial sobre [supervisar cuentas y flujos de datos en la interfaz de usuario](../../monitor-streaming.md).

## Limitaciones conocidas

Para garantizar una ingesta de datos precisa, debe enviar al conector los datos de los puntos de lealtad modificados, la actualización de los niveles y las notificaciones de reducción de categoría de [!DNL Talon.One]. Dado que la notificación de cambios de puntos de lealtad no incluye información de nivel, debe enviar estas notificaciones a un conjunto de datos de perfil independiente. Si combina datos de puntos cambiados con notificaciones de actualización o reducción de nivel en el mismo conjunto de datos, la información del nivel se perderá o sobrescribirá con valores nulos. Las notificaciones de actualización y reducción de categoría pueden utilizar el mismo conjunto de datos, ya que ambos incluyen detalles de categoría. Después de la ingesta, las reglas de combinación de perfiles actualizarán automáticamente el perfil combinado para reflejar los puntos y la información de nivel más recientes.