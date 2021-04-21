---
keywords: Experience Platform;inicio;temas populares;monitorizar cuentas;monitorizar flujos de datos;flujos de datos;destinos
description: Los destinos le permiten activar sus datos desde Adobe Experience Platform a innumerables socios externos. Este tutorial proporciona instrucciones sobre cómo monitorizar los flujos de datos de los destinos mediante la interfaz de usuario del Experience Platform.
solution: Experience Platform
title: Monitorizar flujos de datos para destinos en la interfaz de usuario
topic-legacy: overview
type: Tutorial
exl-id: 8eb7bb3c-f2dc-4dbc-9cf5-3d5d3224f5f1
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '430'
ht-degree: 1%

---

# Monitorización de flujos de datos para destinos en la interfaz de usuario

Los destinos le permiten activar sus datos desde Adobe Experience Platform a innumerables socios externos. Este tutorial proporciona instrucciones sobre cómo monitorizar los flujos de datos de los destinos mediante la interfaz de usuario del Experience Platform.

## Primeros pasos

Este tutorial requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

- [Destinos](../../destinations/home.md): Los destinos son integraciones prediseñadas con aplicaciones de uso común que permiten la activación perfecta de datos de Platform para campañas de marketing multicanal, campañas de correo electrónico, publicidad de destino y muchos otros casos de uso.
- [Simuladores para pruebas](../../sandboxes/home.md):  [!DNL Experience Platform] proporciona entornos limitados virtuales que dividen una sola  [!DNL Platform] instancia en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

## Monitorizar flujos de datos

En el espacio de trabajo **[!UICONTROL Destinations]** dentro de la interfaz de usuario de Platform, vaya a la pestaña **[!UICONTROL Browse]** y seleccione el nombre de un destino que desea ver.

![](../assets/ui/monitor-destinations/select-destination.png)

Aparecerá una lista de flujos de datos existentes. En esta página hay una lista de flujos de datos visibles, que incluye información sobre su destino, nombre de usuario, número de flujos de datos y estado.

Consulte la siguiente tabla para obtener más información sobre los estados:

| Estado | Descripción |
| ------ | ----------- |
| Habilitado | El estado `Enabled` indica que un flujo de datos está activo y que está incorporando datos según la programación que se proporcionó. |
| Desactivado | El estado `Disabled` indica que un flujo de datos está inactivo y no está incorporando ningún dato. |
| Procesamiento | El estado `Processing` indica que un flujo de datos aún no está activo. Este estado se encuentra a menudo inmediatamente después de crear un nuevo flujo de datos. |
| Error | El estado `Error` indica que se ha interrumpido el proceso de activación de un flujo de datos. |

## [!UICONTROL Dataflow runs]

La pestaña [!UICONTROL Dataflow runs] proporciona datos de métricas sobre su flujo de datos que se ejecuta en destinos por lotes. Se muestra una lista de ejecuciones individuales y sus métricas particulares, junto con los siguientes totales de registros de perfil:

- **[!UICONTROL Profile records activated]**: Recuento total de registros de perfil creados o actualizados para la activación.
- **[!UICONTROL Profile records skipped]**: Recuento total de registros de perfil que se omiten para su activación según las salidas de perfil o los atributos que faltan.

![](../assets/ui/monitor-destinations/dataflow-runs.png)

>[!NOTE]
>
>Las ejecuciones de flujo de datos se generan en función de la frecuencia de programación del flujo de datos de destino. Se realiza una ejecución de flujo de datos independiente para cada política de combinación aplicada a un segmento.

Para ver los detalles de una ejecución de flujo de datos determinada, seleccione la hora de inicio de la ejecución en la lista. La página de detalles de una ejecución de flujo de datos contiene información adicional, como el tamaño de los datos procesados y una lista de cualquier error que se haya producido con detalles para el diagnóstico de errores.

![](../assets/ui/monitor-destinations/dataflow.png)
