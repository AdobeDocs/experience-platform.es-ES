---
title: Ingesta bajo demanda de flujos de datos de origen en la interfaz de usuario
description: Obtenga información sobre cómo crear flujos de datos bajo demanda para las conexiones de origen mediante la interfaz de usuario de Experience Platform.
exl-id: e5a70044-2484-416a-8098-48e6d99c2d98
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '552'
ht-degree: 0%

---

# Ingesta bajo demanda de flujos de datos de origen en la interfaz de usuario

Puede utilizar la ingesta bajo demanda para almacenar en déclencheur una iteración de ejecución de flujo de un flujo de datos existente mediante el espacio de trabajo de fuentes en la interfaz de usuario de Adobe Experience Platform.

Este documento proporciona pasos sobre cómo crear flujos de datos bajo demanda para orígenes, así como cómo reintentar ejecuciones de flujo que se han procesado o que han fallado.

>[!BEGINSHADEBOX]

**¿Qué es una ejecución de flujo?**

Las ejecuciones de flujo representan una instancia de ejecución de flujo de datos. Por ejemplo, si un flujo de datos está programado para ejecutarse por hora a las 9:00, 10:00 y 11:00 a.m., tendría tres instancias de ejecución de flujo. Las ejecuciones de flujo son específicas de su organización particular.

>[!ENDSHADEBOX]

## Introducción

>[!NOTE]
>
>Para crear una ejecución de flujo, primero debe tener el ID de flujo de un flujo de datos programado para una ingesta única.

Este documento requiere un entendimiento práctico de los siguientes componentes de Experience Platform:

* [Fuentes](../../home.md): Experience Platform permite la ingesta de datos de varias fuentes al tiempo que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de Experience Platform.
* [Flujos de datos](../../../dataflows/home.md): un flujo de datos es una representación de trabajos de datos que mueven datos a través de Experience Platform. Los flujos de datos se configuran en diferentes servicios, lo que ayuda a mover datos de los conectores de origen a los conjuntos de datos de destino, al servicio de identidad y al perfil del cliente en tiempo real, y a los destinos.
* [Zonas protegidas](../../../sandboxes/home.md): Experience Platform proporciona zonas protegidas virtuales que dividen una sola instancia de Experience Platform en entornos virtuales independientes para ayudar a desarrollar y evolucionar aplicaciones de experiencia digital.

## Creación de un flujo de datos bajo demanda {#create-a-dataflow-on-demand}

Vaya a la pestaña *[!UICONTROL Flujos de datos]* del área de trabajo de orígenes. Aquí, busque el flujo de datos que desea ejecutar bajo demanda y, a continuación, seleccione los puntos suspensivos (**`...`**) junto al nombre del flujo de datos.

![Una lista de flujos de datos en el área de trabajo de orígenes.](../../images/tutorials/on-demand/select-dataflow.png)

A continuación, seleccione **[!UICONTROL Ejecutar bajo demanda]** en el menú desplegable que aparece.

![Menú desplegable con la opción Ejecutar bajo demanda seleccionada.](../../images/tutorials/on-demand/run-on-demand.png)

Configure la programación de la ingesta bajo demanda. Seleccione la **[!UICONTROL hora de inicio de la ingesta]**, la **[!UICONTROL hora de inicio del intervalo de fechas]** y la **[!UICONTROL hora de finalización del intervalo de fechas]**.

| Configuración de programación | Descripción |
| --- | --- |
| [!UICONTROL Hora de inicio de la ingesta] | Hora programada en la que comenzará la ejecución del flujo bajo demanda. |
| [!UICONTROL Hora de inicio del intervalo de fecha] | La primera fecha y hora desde la que se recuperarán los datos. |
| [!UICONTROL Hora de finalización del intervalo de fecha] | La fecha y hora en que se recuperarán los datos hasta. |

Seleccione **[!UICONTROL Programar]** y deje pasar unos momentos para que su flujo de datos bajo demanda se almacene en déclencheur.

![Ventana de configuración de programación para la ingesta bajo demanda.](../../images/tutorials/on-demand/configure-schedule.png)

Seleccione el nombre del flujo de datos para ver su actividad. Aquí verá una lista de las ejecuciones del flujo de datos que se han procesado. Puede volver a ejecutar iteraciones individuales de las ejecuciones de flujo de datos independientemente de si han fallado o se han realizado correctamente. Para las iteraciones de ejecución que han fallado, puede usar **[!UICONTROL Reintentar]** para iniciar de nuevo la ejecución después de diagnosticar y corregir cualquier error que se haya encontrado durante el proceso de creación.

![Se ejecuta una lista de flujos procesados para un flujo de datos seleccionado.](../../images/tutorials/on-demand/processed.png)

Seleccione **[!UICONTROL Programado]** para ver una lista de las ejecuciones de flujo de datos programadas para una ingesta futura.

![Se ejecuta una lista de flujos programados para un flujo de datos seleccionado.](../../images/tutorials/on-demand/scheduled.png)

## Pasos siguientes

Al leer este documento, ha aprendido a crear ejecuciones de flujo bajo demanda para flujos de datos de fuentes existentes. Para obtener más información sobre las fuentes, lea [descripción general de las fuentes](../../home.md)
