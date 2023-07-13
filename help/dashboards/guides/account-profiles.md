---
title: Guía del panel de perfiles de cuenta
description: Adobe Experience Platform proporciona un tablero a través del cual puede ver información importante acerca de los perfiles de cuenta B2B de su organización.
exl-id: c9a3d786-6240-4ba4-96c8-05f658e1150c
source-git-commit: 79966442f5333363216da17342092a71335a14f0
workflow-type: tm+mt
source-wordcount: '1052'
ht-degree: 0%

---

# [!UICONTROL Perfiles de cuenta] tablero

La interfaz de usuario (IU) de Adobe Experience Platform proporciona un tablero a través del cual puede ver información importante acerca de los perfiles de la cuenta, tal como se capturan durante una instantánea diaria. Esta guía describe cómo acceder a y trabajar con [!UICONTROL Perfiles de cuenta] en la interfaz de usuario de y proporciona más información sobre las visualizaciones que se muestran en el panel.

Para obtener una descripción general de todas las funciones de la interfaz de usuario del perfil de la cuenta, visite la [guía de IU del perfil de cuenta](../../rtcdp/accounts/account-profile-ui-guide.md).

## Primeros pasos

Debe tener derecho a [Adobe Real-time Customer Data Platform B2B Edition](../../rtcdp/b2b-overview.md) para acceder al B2B [!UICONTROL Perfiles de cuenta] panel.

## Datos de perfiles de cuenta

El [!UICONTROL Perfiles de cuenta] el tablero muestra una instantánea de la información de cuentas unificadas de las distintas fuentes de los canales de marketing y los distintos sistemas que utiliza su organización actualmente para almacenar la información de cuentas de clientes.

Los datos de perfil de la instantánea muestran los datos exactamente como aparecen en el momento específico en el que se tomó la instantánea. En otras palabras, la instantánea no es una aproximación o una muestra de los datos y la variable [!UICONTROL Perfiles de cuenta] el tablero no se actualiza en tiempo real.

>[!NOTE]
>
>Los cambios o actualizaciones realizados en los datos desde que se tomó la instantánea no se reflejarán en el tablero hasta que se tome la siguiente instantánea.

## Explore la [!UICONTROL Perfiles de cuenta] tablero

Para ir a [!UICONTROL Perfiles de cuenta] en la IU de Platform, seleccione **[!UICONTROL Perfiles]** bajo [!UICONTROL Cuentas] en el panel de navegación izquierdo.

![La interfaz de usuario de Platform con perfiles de cuenta en la navegación izquierda resaltada y se muestra la pestaña de información general.](../images/account-profiles/account-profiles-dashboard.png)

Desde el [!UICONTROL Perfiles de cuenta] tablero puede hacer lo siguiente [examine los perfiles de cuenta introducidos en su organización](#browse-account-profiles), o [vea la totalidad de los datos de perfil de la cuenta de un vistazo mediante widgets](#standard-widgets) que visualizan aspectos de los datos.

## Examinar perfiles de cuenta {#browse-account-profiles}

El [!UICONTROL Examinar] permite buscar y ver los perfiles de cuenta de solo lectura introducidos en su organización mediante un ID de cuenta de una fuente empresarial conectada o introduciendo directamente los detalles de la fuente. Desde aquí puede ver información importante que pertenece al perfil de la cuenta, como su nombre, sector, ingresos y audiencia, entre otros.

Seleccione el [!UICONTROL ID de perfil] de los resultados mostrados en la [!UICONTROL Examinar] para abrir el [!UICONTROL Detalles] para el perfil de cuenta.

![La pestaña de exploración Perfiles de cuenta muestra los resultados y el ID de perfil se resalta.](../images/account-profiles/account-profiles-browse-tab.png)

La información de perfil de cuenta mostrada en la [!UICONTROL Detalles] se ha combinado desde varios fragmentos de perfil para formar una sola vista de la cuenta individual. Consulte la documentación sobre [exploración de perfiles de cuenta en Adobe Real-time Customer Data Platform](../../rtcdp/accounts/account-profile-ui-guide.md#browse-account-profiles) para obtener más información acerca de las funcionalidades de visualización de perfiles de cuenta en la IU de Platform.

## El [!UICONTROL Perfiles de cuenta] [!UICONTROL Información general] {#overview}

El [!UICONTROL Información general] está compuesta por widgets que proporcionan métricas de solo lectura para transmitir información importante sobre los perfiles de la cuenta. Seleccionar **[!UICONTROL Modificar tablero]** para cambiar el aspecto del [!UICONTROL Información general] moviendo y cambiando el tamaño de los widgets.

![La pestaña Información general de perfiles de cuenta con el panel Modificar resaltado.](../images/account-profiles/modify-dashboard.png)

Consulte el documento sobre [modificación de paneles](../customize/modify.md) y el [Resumen de biblioteca de widgets](../customize/widget-library.md) para obtener más información.

## Widgets estándar {#standard-widgets}

Adobe proporciona widgets estándar que puede utilizar para visualizar diferentes métricas relacionadas con los perfiles de la cuenta.

Para obtener más información sobre cada uno de los widgets estándar disponibles, seleccione el nombre de un widget en la siguiente lista:

* [Cuentas totales por sector](#total-accounts-by-industry)
* [Perfiles de cuenta añadidos](#account-profiles-added)
* [Distribución de puntuación predictiva](#predictive-scoring-distribution)
* [Factores más influyentes de la puntuación predictiva](#predictive-scoring-top-influential-factors)

### Cuentas totales por sector {#total-accounts-by-industry}

Este widget muestra el número total de cuentas en una sola métrica y utiliza un gráfico de anillo para ilustrar los tamaños proporcionales de los recuentos de las industrias que conforman el número total. La clave proporciona información de codificación de color para las diferentes industrias que conforman el gráfico circular.

Los recuentos individuales de las diferentes industrias se muestran en un cuadro de diálogo cuando el cursor se pasa por encima de la sección correspondiente del gráfico circular.

![El total de cuentas por widget de sector.](../images/account-profiles/total-accounts-by-industry-widget.png)

### Perfiles de cuenta añadidos {#account-profiles-added}

Este widget utiliza un gráfico de barras con códigos de color para ilustrar el recuento de perfiles agregados a una cuenta durante un período de tiempo determinado y la proporción de diferentes industrias que constituyen estos perfiles agregados. Las industrias están codificadas por colores, y una clave proporciona la información de codificación por colores para las diferentes industrias que conforman el gráfico de barras. El periodo de análisis se selecciona en el menú desplegable de widgets. El gráfico de barras se puede visualizar durante un periodo de 30 días, 90 días y 12 meses.

>[!NOTE]
>
>Como los perfiles solo se añaden a una cuenta y nunca se eliminan, el número más bajo posible de perfiles añadidos durante un periodo de tiempo es cero.

![El widget Perfiles de cuenta agregados.](../images/account-profiles/accounts-profiles-added-widget.png)

### Distribución de puntuación predictiva {#predictive-scoring-distribution}

El [!UICONTROL Distribución de puntuación predictiva] Este widget muestra la distribución de puntuación de todos los perfiles de cuenta para ayudarle a comprender el estado de su canal de ventas de un vistazo. Los datos de puntuación se transmiten mediante un gráfico circular y un gráfico de columnas.

El gráfico de anillo ilustra la proporción de los perfiles totales de la cuenta en cada uno de los bloques de compra alta, media y baja. La clave proporciona más detalles sobre las secciones con códigos de color, incluidos los intervalos del bloque de puntuación y el número de perfiles de cuenta en ese intervalo.

El gráfico de columnas proporciona un desglose de puntuación más granular. Cada columna muestra el número de perfiles de cuenta en cada uno de los 20 bloques de incremento de cinco puntos.

El menú desplegable dentro del widget permite seleccionar el modelo de puntuación de la cuenta.

![El widget de distribución de puntuación predictiva.](../images/account-profiles/predictive-scoring-distribution.png)

### Factores más influyentes de la puntuación predictiva {#predictive-scoring-top-influential-factors}

El [!UICONTROL Factores más influyentes de la puntuación predictiva] Este widget le ayuda a comprender los factores más significativos que impulsan las puntuaciones de cada bloque de tendencia.

Este widget muestra los principales factores influyentes para cada uno de los bloques de alta, media y baja tendencia. Una barra para cada factor influyente indica el porcentaje de los perfiles de cuenta en ese bloque de tendencia que contiene el factor influyente específico.

El menú desplegable dentro del widget permite seleccionar el modelo de puntuación de la cuenta.

![El widget de factores influyentes principales de puntuación predictiva.](../images/account-profiles/predictive-scoring-top-influential-factors.png)

## Pasos siguientes

Si sigue este documento, debería saber cómo localizar el [!UICONTROL Perfiles de cuenta] panel. También debe comprender las métricas que se muestran en los widgets disponibles. Para obtener más información sobre cómo trabajar con perfiles de cuenta como parte de los datos B2B en la IU de Experience Platform, consulte la [resumen de perfiles de cuenta](../../rtcdp/accounts/account-profile-overview.md) para Adobe Real-Time CDP, edición B2B.
