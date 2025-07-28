---
title: Conectar Didomi a Experience Platform
description: Aprenda a conectar su cuenta de Didomi a Experience Platform mediante la interfaz de usuario.
hide: true
hidefromtoc: true
source-git-commit: 44c01678e96f2649dbf731dd4531004c1df28058
workflow-type: tm+mt
source-wordcount: '1142'
ht-degree: 3%

---

# Conectar [!DNL Didomi] a Experience Platform

Lea esta guía para obtener información sobre cómo conectar su cuenta de [!DNL Didomi] a Adobe Experience Platform mediante el área de trabajo de orígenes en la interfaz de usuario.

>[!IMPORTANT]
>
>* El equipo *Didomi* creó esta página de documentación. Para cualquier consulta o solicitud de actualización, comuníquese directamente con ellos en *support@didomi.io*.
>* Para obtener instrucciones paso a paso sobre cómo generar la conexión, consulte la [documentación del conector de origen de Didomi Adobe](https://developers.didomi.io/integrations/third-party-apps/preference-management-platform-integrations/Adobe-source-connector).

## Introducción 

Este tutorial requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): El marco estandarizado mediante el cual Experience Platform organiza los datos de experiencia del cliente.
   * [Aspectos básicos de la composición de esquemas](../../../../../xdm/schema/composition.md): obtenga información sobre los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   * [Tutorial del editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): Aprenda a crear esquemas personalizados mediante la interfaz de usuario del editor de esquemas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): proporciona un perfil de consumidor unificado y en tiempo real basado en los datos agregados de varias fuentes.

### Configurar su cuenta de [!DNL Didomi]

Antes de continuar, asegúrese de leer y completar los pasos de requisitos previos descritos en la [[!DNL Didomi] descripción general](../../../../connectors/consent-and-preferences/didomi.md#prerequisites) para conectar correctamente su cuenta a Experience Platform.

## Navegar por el catálogo de fuentes

En la interfaz de usuario de Experience Platform, seleccione **[!UICONTROL Fuentes]** en el panel de navegación izquierdo para acceder al área de trabajo *[!UICONTROL Fuentes]*. Elija una categoría o utilice la barra de búsqueda para encontrar el origen.

Para conectarse a [!DNL Didomi], vaya a la categoría *[!UICONTROL Bases de datos]*, seleccione la tarjeta de origen **[!UICONTROL Didomi]** y, a continuación, seleccione **[!UICONTROL Configurar]**.

>[!TIP]
>
>Los orígenes del catálogo de orígenes muestran la opción **[!UICONTROL Set up]** cuando un origen determinado aún no tiene una cuenta autenticada. Una vez creada una cuenta autenticada, esta opción cambia a **[!UICONTROL Agregar datos]**.

![source-connector-list](../../../../images/tutorials/create/didomi/source-connector-list.png)

## Añadir el esquema de datos de origen

A continuación, use la interfaz *[!UICONTROL Select data]* para cargar el archivo JSON [descargado en los pasos previos](../../../../connectors/consent-and-preferences/didomi.md#download-the-sample-payload-file).

Puede utilizar la interfaz de vista previa para ver la estructura de archivos de la carga útil. Cuando termine, seleccione **[!UICONTROL Siguiente]**.

![add-data-schema](../../../../images/tutorials/create/didomi/add-data-schema.png)

## Proporcionar detalles del flujo de datos

A continuación, debe proporcionar información sobre el conjunto de datos y el flujo de datos.

### Detalles del conjunto de datos

Un conjunto de datos es una construcción de almacenamiento y administración para una colección de datos, normalmente una tabla, que contiene un esquema (columnas) y campos (filas). Los datos que se incorporan correctamente a Experience Platform se conservan dentro del lago de datos como conjuntos de datos.

Durante este paso, puede utilizar un conjunto de datos existente o crear uno nuevo.

>[!NOTE]
>
>Independientemente de si utiliza un conjunto de datos existente o crea uno nuevo, debe asegurarse de que el conjunto de datos esté **habilitado para la ingesta de Profile**.

+++Seleccione esta opción para habilitar la Ingesta de perfiles, los diagnósticos de error y la ingesta parcial.

Si el conjunto de datos está habilitado para Perfil del cliente en tiempo real, durante este paso, puede alternar **[!UICONTROL Conjunto de datos de perfil]** para habilitar los datos para la ingesta de perfiles. También puede usar este paso para habilitar **[!UICONTROL diagnósticos de error]** y **[!UICONTROL ingesta parcial]**.

* **[!UICONTROL Diagnósticos de error]**: seleccione **[!UICONTROL Diagnósticos de error]** para indicar a la fuente que produzca diagnósticos de error a los que pueda hacer referencia posteriormente al supervisar la actividad del conjunto de datos y el estado del flujo de datos.
* **[!UICONTROL Ingesta parcial]**: La ingesta parcial por lotes es la capacidad de ingerir datos que contengan errores, hasta un determinado umbral configurable. Esta función le permite introducir correctamente todos los datos exactos en Experience Platform, mientras que todos los datos incorrectos se agrupan por separado con información sobre los motivos por los que no son válidos.

+++

### Detalles del flujo de datos

Una vez configurado el conjunto de datos, debe proporcionar detalles sobre el flujo de datos, incluido un nombre, una descripción opcional y configuraciones de alerta.

![detalles del flujo de datos](../../../../images/tutorials/create/didomi/dataflow-details.png)

| Configuraciones de flujo de datos | Descripción |
| --- | --- |
| Nombre de flujo de datos | Nombre del flujo de datos.  De forma predeterminada, se utiliza el nombre del archivo que se está importando. |
| Descripción | (Opcional) Una breve descripción del flujo de datos. |
| Alertas | Experience Platform puede producir alertas basadas en eventos a las que los usuarios pueden suscribirse; todas estas opciones incluyen un flujo de datos en ejecución para almacenarlas en déclencheur.  Para obtener más información, lea la [descripción general de las alertas](../../alerts.md) <ul><li>**Inicio de ejecución del flujo de datos de origen**: seleccione esta alerta para recibir una notificación cuando comience la ejecución del flujo de datos.</li><li>**Ejecución correcta del flujo de datos de origen**: seleccione esta alerta para recibir una notificación si el flujo de datos termina sin errores.</li><li>**Error al ejecutar el flujo de datos de origen**: seleccione esta alerta para recibir una notificación si la ejecución del flujo de datos termina con errores.</li></ul> |

{style="table-layout:auto"}

## Asignación

Utilice la interfaz de asignación para asignar los datos de origen a los campos de esquema adecuados antes de introducir datos en Experience Platform.  Para obtener más información, lea la guía de asignación [en la interfaz de usuario](../../../../../data-prep/ui/mapping.md)

La asignación se usa específicamente para transferir **datos de propósito** de [!DNL Didomi] al conjunto de datos de Experience Platform. Estos fines representan las opciones de consentimiento del usuario (como, por ejemplo, análisis, personalización, publicidad, etc.) y son los únicos campos de asignación aceptados en esta integración.

Use la carga útil de [webhook de muestra descargada](../../../../connectors/consent-and-preferences/didomi.md#download-the-sample-payload-file) desde la configuración de [!DNL Didomi] webhook para asignar cada propósito de [!DNL Didomi] a los campos correspondientes de su conjunto de datos de Adobe.

Cuando termine, seleccione **[!UICONTROL Siguiente]**.

![detalles de asignación](../../../../images/tutorials/create/didomi/mapping-details.png)

## Revisión

Aparece el paso *[!UICONTROL Revisar]*, que le permite revisar los detalles del flujo de datos antes de crearlo. Los detalles se agrupan en las siguientes categorías:

* **[!UICONTROL Conexión]**: muestra el nombre de cuenta, la plataforma de origen y el nombre de origen.
* **[!UICONTROL Asignar campos de conjunto de datos y asignación]**: muestra el conjunto de datos de destino y el esquema al que se adhiere el conjunto de datos.

Después de confirmar que los detalles son correctos, seleccione **[!UICONTROL Finalizar]**.

## Recupere la URL del extremo de flujo continuo

Con la conexión creada, aparecerá la página de detalles de orígenes. Esta página muestra detalles de la conexión recién creada, incluidos los flujos de datos ejecutados anteriormente, el ID y la URL del extremo de flujo continuo.

## Finalizar la configuración en Adobe

Una vez que haya creado el flujo de datos, vaya al catálogo *[!UICONTROL Sources]* y seleccione **[!UICONTROL Dataflows]**. Utilice el directorio de flujos de datos para localizar su flujo de datos [!DNL Didomi] y acceder a la interfaz de *[!UICONTROL actividad de flujo de datos]*. A continuación, utilice el panel *[!UICONTROL Properties]* en el carril derecho y recupere los valores de lo siguiente:

* [!UICONTROL Extremo de streaming]
* [!UICONTROL ID de flujo de datos]

En la IU de Experience Platform:

1. Después de completar la configuración, revise los parámetros de configuración que faltaban en la configuración inicial del gancho web.
2. Una vez que estos valores estén disponibles, vuelva a Didomi y actualice la configuración del webhook.

![configuración terminada](../../../../images/tutorials/create/didomi/configuration-done.png)

## Actualizar la configuración del webhook

Una vez completada la configuración, vuelva a la consola [!DNL Didomi] y actualice la configuración del gancho web con la **URL del extremo de transmisión** y la **ID del flujo de datos**.

Una vez que se complete esto, [!DNL Didomi] empezará a enviar eventos de administración de consentimiento y de preferencias a través de la integración y los datos se almacenarán en el conjunto de datos de Adobe.

## Próximos pasos

Al seguir este tutorial, ha creado correctamente un flujo de datos para traer datos por lotes de su origen de [!DNL Didomi] a Experience Platform. Para obtener recursos adicionales, visite la documentación descrita a continuación.

### Monitorización del flujo de datos

Una vez creado el flujo de datos, puede monitorizar los datos que se están ingiriendo a través de él para ver información sobre las tasas de ingesta, el éxito y los errores. Para obtener más información sobre cómo supervisar el flujo de datos, visite el tutorial sobre [supervisar cuentas y flujos de datos en la interfaz de usuario](../../../../../dataflows/ui/monitor-sources.md).

### Actualizar el flujo de datos

Para actualizar configuraciones para la programación, asignación e información general de los flujos de datos, visite el tutorial sobre [actualización de flujos de datos de origen en la interfaz de usuario](../../update-dataflows.md).

### Eliminar el flujo de datos

Puede eliminar flujos de datos que ya no sean necesarios o que se hayan creado incorrectamente mediante la función **[!UICONTROL Delete]** disponible en el área de trabajo **[!UICONTROL Flujos de datos]**. Para obtener más información sobre cómo eliminar flujos de datos, visite el tutorial sobre [eliminar flujos de datos en la interfaz de usuario](../../delete.md).