---
keywords: Experience Platform;home;popular topics;monitor accounts;monitor dataflows;dataflows;destinations
description: Los destinos le permiten activar sus datos desde Adobe Experience Platform a innumerables socios externos. Este tutorial proporciona instrucciones sobre cómo puede supervisar los flujos de datos de los destinos mediante la interfaz de usuario del Experience Platform.
solution: Experience Platform
title: Monitoreo de flujos de datos
topic: overview
type: Tutorial
translation-type: tm+mt
source-git-commit: 12a6682b6e28e656899aee5c38d3bb4a84bcdd2f
workflow-type: tm+mt
source-wordcount: '426'
ht-degree: 1%

---


# Monitorear flujos de datos para destinos en la interfaz de usuario

Los destinos le permiten activar sus datos desde Adobe Experience Platform a innumerables socios externos. Este tutorial proporciona instrucciones sobre cómo puede supervisar los flujos de datos de los destinos mediante la interfaz de usuario del Experience Platform.

## Primeros pasos

Este tutorial requiere un conocimiento práctico de los siguientes componentes de Adobe Experience Platform:

- [Destinos](../../destinations/home.md): Los destinos son integraciones prediseñadas con aplicaciones de uso común que permiten la activación sin fisuras de datos de la Plataforma para campañas de marketing en canal cruzado, campañas por correo electrónico, publicidad de destino y muchos otros casos de uso.
- [Simuladores](../../sandboxes/home.md): [!DNL Experience Platform] proporciona entornos limitados virtuales que dividen una sola [!DNL Platform] instancia en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

## Monitoreo de flujos de datos

En el espacio de trabajo **[!UICONTROL Destinos]** de la interfaz de usuario de la plataforma, vaya a la ficha **[!UICONTROL Examinar]** y seleccione el nombre de un destino al que desee realizar la vista.

![](../assets/ui/monitor-destinations/select-destination.png)

Aparece una lista de flujos de datos existentes. En esta página hay una lista de flujos de datos visualizables, incluida información sobre su destino, nombre de usuario, número de flujos de datos y estado.

Consulte la siguiente tabla para obtener más información sobre los estados:

| Estado | Descripción |
| ------ | ----------- |
| Habilitado | El `Enabled` estado indica que un flujo de datos está activo y que está invirtiendo datos según la programación que se proporcionó. |
| Desactivado | El estado `Disabled` indica que un flujo de datos está inactivo y no está invirtiendo ningún dato. |
| Procesamiento | El estado `Processing` indica que un flujo de datos aún no está activo. Este estado suele encontrarse inmediatamente después de crear un nuevo flujo de datos. |
| Error | El `Error` estado indica que se ha interrumpido el proceso de activación de un flujo de datos. |

## [!UICONTROL Ejecuciones de flujo de datos]

La ficha Ejecuciones [!UICONTROL de flujo de] datos proporciona datos de métricas sobre las ejecuciones de flujo de datos a destinos por lotes. Se muestra una lista de ejecuciones individuales y sus métricas específicas, junto con los siguientes totales para los registros de perfiles:

- **[!UICONTROL Registros de perfil activados]**: Recuento total de registros de perfiles que se crearon o actualizaron para la activación.
- **[!UICONTROL Se omitieron]** los registros de perfil:  Recuento total de registros de perfiles que se omiten para la activación en función de las salidas de perfiles o los atributos que faltan.

![](../assets/ui/monitor-destinations/dataflow-runs.png)

>[!NOTE]
>
>Las ejecuciones de flujo de datos se generan en función de la frecuencia de programación del flujo de datos de destino. Se realiza una ejecución de flujo de datos independiente para cada directiva de combinación aplicada a un segmento.

Para vista de los detalles de una ejecución de flujo de datos concreta, seleccione la hora de inicio de la ejecución en la lista. La página de detalles de una ejecución de flujo de datos contiene información adicional, como el tamaño de los datos procesados y una lista de los errores que se han producido con detalles de los diagnósticos de error.

![](../assets/ui/monitor-destinations/dataflow.png)