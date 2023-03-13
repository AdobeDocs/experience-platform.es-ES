---
keywords: Experience Platform;interfaz de usuario;IU;personalización;tablero de uso de licencias;tablero;uso de licencias;asignación de derechos;consumo
title: Guía del tablero de uso de licencias
description: Adobe Experience Platform proporciona un tablero a través del cual puede ver información importante acerca del uso de licencias de su organización.
type: Documentation
exl-id: 143d16bb-7dc3-47ab-9b93-9c16683b9f3f
source-git-commit: fa4fc154f57243250dec9bdf9557db13ef7768e8
workflow-type: tm+mt
source-wordcount: '935'
ht-degree: 1%

---

# Tablero de uso de licencias {#license-usage-dashboard}

La interfaz de usuario (IU) de Adobe Experience Platform proporciona un tablero a través del cual puede ver información importante acerca del uso de licencias de su organización, tal y como se captura durante una instantánea diaria. Esta guía describe cómo acceder y trabajar con el tablero de uso de licencias en la interfaz de usuario y proporciona más información sobre las visualizaciones que se muestran en el tablero.

Para obtener una descripción general de la IU de Platform, visite la [Guía de IU de Experience Platform](../../landing/ui-guide.md).

## Datos del tablero de uso de licencias

El panel de uso de licencias muestra una instantánea de los datos de licencias de su organización para Experience Platform. Los datos del tablero se muestran exactamente como aparecen en el momento específico en el que se tomó la instantánea. En otras palabras, la instantánea no es una aproximación o una muestra de los datos y el panel no se actualiza en tiempo real.

>[!NOTE]
>
>Los cambios o actualizaciones realizados en los datos desde que se tomó la instantánea no se reflejarán en el tablero hasta que se tome la siguiente instantánea.

## Exploración del tablero de uso de licencias

Para navegar al panel de uso de licencias dentro de la interfaz de usuario de Platform, seleccione **[!UICONTROL Uso de licencias]** en el carril izquierdo. Esto abre el **[!UICONTROL Información general]** pestaña que muestra el tablero.

>[!NOTE]
>
>El panel de uso de licencias no está habilitado de forma predeterminada. Los usuarios deben tener permiso para &quot;Ver tablero de uso de licencias&quot; para poder ver el tablero. Para ver los pasos sobre la concesión de permisos de acceso para ver el panel de uso de licencias, consulte la [guía de permisos del panel](../permissions.md).

![La pestaña Información general del tablero de uso de licencias.](../images/license-usage/dashboard-overview.png)

### Seleccionar una zona protegida

Para elegir una zona protegida para verla en el panel, seleccione [!UICONTROL Producción] o [!UICONTROL Desarrollo]. La zona protegida seleccionada se indica con el botón de opción situado junto al nombre de la zona protegida.

Los informes de consumo para las zonas protegidas son acumulativos para todas las zonas protegidas del mismo tipo. En otras palabras, seleccionar [!UICONTROL Producción] o [!UICONTROL Desarrollo] proporciona informes de consumo para todas las zonas protegidas de producción o desarrollo, respectivamente.

![La pestaña Información general del tablero Uso de licencias con el selector de zona protegida resaltado.](../images/license-usage/select-sandbox.png)

>[!WARNING]
>
>El permiso para ver el tablero de uso de licencias debe especificarse en el nivel de zona protegida. Esto significa que el permiso para ver el panel debe agregarse a cada zona protegida individual. Esta limitación se solucionará en una versión futura. Mientras tanto, está disponible la siguiente solución:
>
>1. Cree un perfil de producto en Adobe Admin Console.
>2. En Permiso en la categoría Zona protegida, agregue todas las zonas protegidas que desee ver en el panel de uso de licencias.
>3. En la categoría Permiso del tablero de usuarios, agregue el permiso &quot;Ver tablero de uso de licencias&quot;.


### Seleccionar un intervalo de fecha

Después de seleccionar una zona protegida, puede utilizar la lista desplegable de intervalo de fechas para seleccionar el período de tiempo que se mostrará en el panel. Hay varias opciones disponibles, incluido el valor predeterminado de los últimos 30 días.

![La pestaña Información general del tablero de uso de licencias con la lista desplegable de intervalos de fechas resaltada.](../images/license-usage/select-date-range.png)

También puede seleccionar **[!UICONTROL Fecha personalizada]** para elegir el período de tiempo que se muestra.

![La pestaña Información general del tablero de uso de licencias con las opciones de intervalo de fechas personalizadas resaltadas.](../images/license-usage/select-custom-date.png)

## Widgets

El tablero de uso de licencias está compuesto por widgets, que muestran métricas de solo lectura que proporcionan información importante sobre el uso de licencias de su organización. Las métricas visibles dependen de las licencias específicas de su organización (consulte la [métricas disponibles](#available-metrics) para obtener más información).

Cada widget muestra un gráfico de líneas que compara los números reales de su organización con el total disponible con las licencias de su organización y proporciona un porcentaje del uso total.

![La pestaña Información general del tablero de uso de licencias con el gráfico de líneas del widget de métrica de uso de licencias de muestra resaltado.](../images/license-usage/widgets.png)

## Métricas disponibles

El tablero de uso de licencias informa sobre cuatro métricas clave, con más métricas que se añadirán en versiones posteriores. Las métricas disponibles son:

* [!UICONTROL Audiencia a la que dirigirse]
* [!UICONTROL Promedio de riqueza de perfiles]
* [!UICONTROL Proporción de datos escaneados por segmentación]
* [!UICONTROL Almacenamiento consumido total]

La disponibilidad de estas métricas y la definición específica de cada una de ellas varían según la licencia que haya adquirido su organización. Para obtener definiciones detalladas de cada métrica, consulte la documentación de descripción del producto correspondiente:

| Licencia | Descripción del producto |
|---|---|
| <ul><li>ADOBE EXPERIENCE PLATFORM:OD LITE</li><li>ADOBE EXPERIENCE PLATFORM:ESTÁNDAR OD</li><li>ADOBE EXPERIENCE PLATFORM:PESADO OD</li></ul> | [Adobe Experience Platform](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-platform.html) |
| <ul><li>ADOBE EXPERIENCE PLATFORM:OD</li></ul> | [Experience Platform, servicios de aplicaciones y servicios inteligentes](https://helpx.adobe.com/legal/product-descriptions/exp-platform-app-svcs.html) |
| <ul><li>RT PLATAFORMA DE DATOS DEL CLIENTE:OD</li><li>RT PLATAFORMA DE DATOS DEL CLIENTE:OD PRFL A 10M</li><li>RT PLATAFORMA DE DATOS DEL CLIENTE:OD PRFL A 50M</li></ul> | [Adobe Real-time Customer Data Platform](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform.html) |
| <ul><li>AEP:ACTIVACIÓN DE OD</li><li>AEP:OD ACTIVATION PRFL A 10M</li><li>AEP: PERFIL DE ACTIVACIÓN DE OD DE HASTA 50 M</li></ul> | [Adobe Experience Platform Activation](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-platform0.html) |
| <ul><li>AEP:INTELIGENCIA OD</li></ul> | [Adobe Experience Platform Intelligence](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-platform-intelligence---product-description.html) |
| <ul><li>JOURNEY OPTIMIZER SELECT:OD</li><li>JOURNEY OPTIMIZER PRIME:OD</li><li>JOURNEY OPTIMIZER ULTIMATE:OD</li><li>DESACTIVAR AJO PRIME STARTER:OD</li><li>DESACTIVAR AJO ULTIMATE STARTER:OD</li><li>DESACTIVAR Real-Time CDP:ORQUESTACIÓN DE PERFILES OD</li></ul> | [Adobe Journey Optimizer](https://helpx.adobe.com/es/legal/product-descriptions/adobe-journey-optimizer.html) |

>[!WARNING]
>
>El tablero de uso de licencias solo informa de la licencia más reciente aprovisionada para su organización. Si la licencia más reciente aprovisionada para su organización no aparece en la tabla anterior, es posible que el panel de uso de licencias no se muestre correctamente. La compatibilidad con licencias adicionales y múltiples licencias en una sola organización está planificada para una versión futura.

## Pasos siguientes

Después de leer este documento, puede localizar el panel de uso de licencias y seleccionar una zona protegida para verla. También puede encontrar más información sobre las métricas disponibles para su organización, en función de las licencias que haya adquirido su organización.

Para obtener más información acerca de otras funciones disponibles en la interfaz de usuario de Experience Platform, consulte la [Guía de IU de Platform](../../landing/ui-guide.md).
