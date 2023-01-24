---
keywords: Experience Platform;interfaz de usuario;IU;personalización;panel de uso de licencias;panel;uso de licencias;derecho;consumo
title: Guía del panel de uso de licencias
description: Adobe Experience Platform proporciona un tablero en el que puede ver información importante sobre el uso de licencias de su organización.
type: Documentation
exl-id: 143d16bb-7dc3-47ab-9b93-9c16683b9f3f
source-git-commit: fa4fc154f57243250dec9bdf9557db13ef7768e8
workflow-type: tm+mt
source-wordcount: '935'
ht-degree: 1%

---

# Panel de uso de licencias {#license-usage-dashboard}

La interfaz de usuario (IU) de Adobe Experience Platform proporciona un tablero en el que puede ver información importante sobre el uso de licencias de su organización, tal como se captura durante una instantánea diaria. Esta guía describe cómo acceder y trabajar con el panel de uso de licencias en la interfaz de usuario y proporciona más información sobre las visualizaciones que se muestran en el panel.

Para obtener una descripción general de la interfaz de usuario de Platform, visite la [Guía de la interfaz de usuario del Experience Platform](../../landing/ui-guide.md).

## Datos del panel de uso de licencias

El panel de uso de licencias muestra una instantánea de los datos de su organización relacionados con las licencias para el Experience Platform. Los datos del tablero se muestran exactamente como aparecen en el momento concreto en que se tomó la instantánea. En otras palabras, la instantánea no es una aproximación o muestra de los datos y el panel no se actualiza en tiempo real.

>[!NOTE]
>
>Los cambios o actualizaciones realizados en los datos desde que se tomó la instantánea no se reflejarán en el panel hasta que se tome la siguiente instantánea.

## Exploración del panel de uso de licencias

Para ir al panel de uso de licencias dentro de la interfaz de usuario de Platform, seleccione **[!UICONTROL Uso de licencias]** en el carril izquierdo. Esto abre el **[!UICONTROL Información general]** que muestra el tablero.

>[!NOTE]
>
>El panel de uso de licencias no está habilitado de forma predeterminada. A los usuarios se les debe conceder permiso &quot;Ver panel de uso de licencias&quot; para poder ver el tablero. Para ver los pasos sobre la concesión de permisos de acceso para ver el panel de uso de licencias, consulte la [guía de permisos del panel](../permissions.md).

![La pestaña Información general del tablero de uso de licencias .](../images/license-usage/dashboard-overview.png)

### Seleccionar un simulador de pruebas

Para elegir un simulador para pruebas para verlo en el tablero, seleccione [!UICONTROL Producción] o [!UICONTROL Desarrollo]. El simulador de pruebas seleccionado se indica mediante el botón de opción situado junto al nombre del simulador de pruebas.

Los informes de consumo para entornos limitados son acumulativos para todos los entornos limitados del mismo tipo. En otras palabras, seleccionar [!UICONTROL Producción] o [!UICONTROL Desarrollo] proporciona informes de consumo para todos los entornos limitados de producción o desarrollo, respectivamente.

![La pestaña Información general del tablero de uso de licencias con el selector de simulación de pruebas resaltado.](../images/license-usage/select-sandbox.png)

>[!WARNING]
>
>El permiso para ver el panel de uso de la licencia debe especificarse en el simulador de pruebas. Esto significa que se debe añadir permiso para ver el panel a cada simulador de pruebas individual. Esta limitación se solucionará en una versión futura. Mientras tanto, está disponible la siguiente solución:
>
>1. Cree un perfil de producto en Adobe Admin Console.
>2. En Permiso en la categoría Simulador para pruebas , agregue todos los entornos limitados que desee ver en el panel de uso de licencias.
>3. En la categoría Permiso del tablero de usuarios , agregue el permiso &quot;Ver tablero de uso de licencias&quot;.


### Seleccionar un intervalo de fechas

Después de seleccionar un simulador para pruebas, puede utilizar la lista desplegable de intervalos de fechas para seleccionar el período de tiempo que se mostrará en el tablero. Hay varias opciones disponibles, incluido el valor predeterminado de los últimos 30 días.

![La pestaña Información general del tablero de uso de licencias con el menú desplegable de intervalo de fechas resaltado.](../images/license-usage/select-date-range.png)

También puede seleccionar **[!UICONTROL Fecha personalizada]** para elegir el período de tiempo que se muestra.

![La pestaña Información general del tablero de uso de licencias con las opciones de intervalo de fechas personalizadas resaltadas.](../images/license-usage/select-custom-date.png)

## Widgets

El panel de uso de licencias está compuesto por utilidades, que muestran métricas de solo lectura que proporcionan información importante sobre el uso de licencias de su organización. Las métricas visibles dependen de las licencias específicas de su organización (consulte la [métricas disponibles](#available-metrics) para obtener más información).

Cada utilidad muestra gráficos de líneas en los que se comparan los números reales de su organización con el total disponible con las licencias de su organización y se proporciona un porcentaje del uso total.

![La pestaña Descripción general del tablero de uso de licencias con el gráfico de líneas del widget de métrica de uso de licencias de muestra resaltado.](../images/license-usage/widgets.png)

## Métricas disponibles

El tablero de uso de licencias informa sobre cuatro métricas clave, con más métricas que agregar en versiones posteriores. Las métricas disponibles son:

* [!UICONTROL Audiencia a la que se puede dirigir]
* [!UICONTROL Promedio de riqueza del perfil]
* [!UICONTROL Datos analizados por proporción de segmentación]
* [!UICONTROL Almacenamiento consumido total]

La disponibilidad de estas métricas y la definición específica de cada una de ellas varían en función de las licencias que haya adquirido su organización. Para obtener definiciones detalladas de cada métrica, consulte la documentación apropiada sobre la Descripción del producto:

| Licencia | Descripción del producto |
|---|---|
| <ul><li>Adobe Experience Platform:OD LITE</li><li>Adobe Experience Platform:OD STANDARD</li><li>Adobe Experience Platform:OD HEAVY</li></ul> | [Adobe Experience Platform](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-platform.html) |
| <ul><li>Adobe Experience Platform:OD</li></ul> | [Experience Platform, servicios de aplicaciones y servicios inteligentes](https://helpx.adobe.com/legal/product-descriptions/exp-platform-app-svcs.html) |
| <ul><li>RT PLATAFORMA DE DATOS DEL CLIENTE:OD</li><li>RT PLATAFORMA DE DATOS DEL CLIENTE:OD PRFL A 10M</li><li>RT PLATAFORMA DE DATOS DEL CLIENTE:OD PRFL A 50M</li></ul> | [Adobe Real-time Customer Data Platform](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform.html) |
| <ul><li>AEP:OD ACTIVATION</li><li>AEP:OD ACTIVATION PRFL A 10M</li><li>AEP:OD ACTIVATION PRFL HASTA 50 M</li></ul> | [Activación de Adobe Experience Platform](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-platform0.html) |
| <ul><li>AEP:OD INTELLIGENCE</li></ul> | [Inteligencia de Adobe Experience Platform](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-platform-intelligence---product-description.html) |
| <ul><li>Journey Optimizer SELECT:OD</li><li>Journey Optimizer PRIME:OD</li><li>Journey Optimizer ULTIMATE:OD</li><li>UNP AJO PRIME STARTER:OD</li><li>UNP AJO ULTIMATE STARTER:OD</li><li>UNP Real-Time CDP:OD PROFILE ORCHESTRATION</li></ul> | [Adobe Journey Optimizer](https://helpx.adobe.com/es/legal/product-descriptions/adobe-journey-optimizer.html) |

>[!WARNING]
>
>El panel de uso de licencias solo informa sobre la licencia más reciente aprovisionada para su organización. Si la licencia más reciente aprovisionada para su organización no aparece en la tabla anterior, es posible que el panel de uso de licencias no se muestre correctamente. Está previsto que se admitan licencias adicionales y varias licencias en una sola organización para una versión futura.

## Pasos siguientes

Después de leer este documento, puede localizar el panel de uso de licencias y seleccionar un simulador para pruebas que ver. También puede encontrar más información sobre las métricas disponibles para su organización, en función de las licencias adquiridas por su organización.

Para obtener más información sobre otras funciones disponibles en la interfaz de usuario del Experience Platform, consulte la [Guía de la interfaz de usuario de Platform](../../landing/ui-guide.md).
