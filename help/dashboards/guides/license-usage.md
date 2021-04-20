---
keywords: Experience Platform;interfaz de usuario;IU;personalización;panel de uso de licencias;panel;uso de licencias;derecho;consumo
title: Tablero de uso de licencias
description: Adobe Experience Platform proporciona un tablero en el que puede ver información importante sobre el uso de licencias de su organización.
topic: guide
type: Documentation
translation-type: tm+mt
source-git-commit: 6baf1fbff20a02cd599d9ad9102d56db5a9004c3
workflow-type: tm+mt
source-wordcount: '660'
ht-degree: 2%

---


# (Beta) Panel de uso de licencias {#license-usage-dashboard}

>[!IMPORTANT]
>
>La funcionalidad de tablero descrita en este documento está actualmente en fase beta y no está disponible para todos los usuarios. La documentación y las funciones están sujetas a cambios.

La interfaz de usuario (IU) de Adobe Experience Platform proporciona un tablero en el que puede ver información importante sobre el uso de licencias de su organización, tal como se captura durante una instantánea diaria. Esta guía describe cómo acceder y trabajar con el panel de uso de licencias en la interfaz de usuario y proporciona más información sobre las visualizaciones que se muestran en el panel.

Para obtener una descripción general de la interfaz de usuario de Platform, visite la [guía de la interfaz de usuario del Experience Platform](../../landing/ui-guide.md).

## Datos del panel de uso de licencias

El panel de uso de licencias muestra una instantánea de los datos de su organización relacionados con las licencias para el Experience Platform. Los datos del tablero se muestran exactamente como aparecen en el momento concreto en que se tomó la instantánea. En otras palabras, la instantánea no es una aproximación o muestra de los datos y el panel no se actualiza en tiempo real.

>[!NOTE]
>
>Los cambios o actualizaciones realizados en los datos desde que se tomó la instantánea no se reflejarán en el panel hasta que se tome la siguiente instantánea.

## Exploración del panel de uso de licencias

Para ir al panel de uso de licencias dentro de la interfaz de usuario de Platform, seleccione **[!UICONTROL Licencia de uso]** en el carril izquierdo. Se abre con la pestaña **[!UICONTROL Overview]** que muestra el tablero.

![](../images/license-usage/dashboard-overview.png)

### Seleccionar un simulador de pruebas

Para elegir un simulador para pruebas para ver en el tablero, seleccione [!UICONTROL Producción] o [!UICONTROL Desarrollo]. El simulador de pruebas seleccionado se indica mediante el botón de opción situado junto al nombre del simulador de pruebas.

>[!NOTE]
>
>Los informes de consumo para entornos limitados son acumulativos para todos los entornos limitados del mismo tipo. En otras palabras, seleccionar [!UICONTROL Producción] o [!UICONTROL Desarrollo] proporciona informes de consumo para todos los entornos limitados de producción o desarrollo, respectivamente.

![](../images/license-usage/select-sandbox.png)

### Seleccionar un intervalo de fechas

Después de seleccionar un simulador para pruebas, puede utilizar la lista desplegable de intervalos de fechas para seleccionar el período de tiempo que se mostrará en el tablero. Hay tres opciones disponibles: [!UICONTROL Últimos 30 días], [!UICONTROL Últimos 90 días] y [!UICONTROL Últimos 12 meses]. Los últimos 30 días están seleccionados de forma predeterminada.

![](../images/license-usage/select-date-range.png)

## Widgets

El panel de uso de licencias está compuesto por utilidades, que muestran métricas de solo lectura que proporcionan información importante sobre el uso de licencias de su organización. Las métricas visibles dependen de las licencias específicas de su organización (consulte la sección [métricas disponibles](#available-metrics) para obtener más información).

Cada utilidad muestra gráficos de líneas en los que se comparan los números reales de su organización con el total disponible con las licencias de su organización y se proporciona un porcentaje del uso total.

![](../images/license-usage/widgets.png)

## Métricas disponibles

Actualmente hay cuatro métricas disponibles en el panel de uso de licencias:

* [!UICONTROL Audiencia a la que se puede dirigir]  (medida por el número de perfiles)
* [!UICONTROL Promedio de riqueza del perfil]
* [!UICONTROL Almacenamiento consumido total]
* [!UICONTROL Datos analizados por proporción de segmentación]

La definición de cada una de estas métricas varía según la licencia que haya adquirido su organización. Para obtener definiciones detalladas de cada métrica, consulte la documentación apropiada sobre la Descripción del producto:

| Licencia | Descripción del producto |
|---|---|
| <ul><li>Adobe Experience Platform:OD LITE</li><li>Adobe Experience Platform:OD STANDARD</li><li>Adobe Experience Platform:OD HEAVY</li></ul> | [Adobe Experience Platform](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-platform.html) |
| <ul><li>Adobe Experience Platform:OD</li></ul> | [Experience Platform, servicios de aplicaciones y servicios inteligentes](https://helpx.adobe.com/legal/product-descriptions/exp-platform-app-svcs.html) |
| <ul><li>RT PLATAFORMA DE DATOS DEL CLIENTE:OD</li><li>RT PLATAFORMA DE DATOS DEL CLIENTE:OD PRFL A 10M</li><li>RT PLATAFORMA DE DATOS DEL CLIENTE:OD PRFL A 50M</li></ul> | [Plataforma de datos de clientes en tiempo real](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform.html) |
| <ul><li>AEP:OD ACTIVATION</li><li>AEP:OD ACTIVATION PRFL A 10M</li><li>AEP:OD ACTIVATION PRFL HASTA 50 M</li></ul> | [Activación de Adobe Experience Platform](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-platform0.html) |
| <ul><li>AEP:OD INTELLIGENCE</li></ul> | [Inteligencia de Adobe Experience Platform](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-platform-intelligence---product-description.html) |

## Pasos siguientes

Después de leer este documento, puede localizar el panel de uso de licencias y seleccionar un simulador para pruebas que ver. También puede encontrar más información sobre las métricas disponibles para su organización, en función de las licencias adquiridas por su organización.

Para obtener más información sobre otras funciones disponibles en la interfaz de usuario del Experience Platform, consulte la [Guía de la interfaz de usuario de la plataforma](../../landing/ui-guide.md).