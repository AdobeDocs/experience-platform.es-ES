---
title: Panel de perfiles de cuenta
description: Adobe Experience Platform proporciona un tablero a través del cual puede ver información importante sobre los perfiles de cuenta B2B de su organización.
exl-id: c9a3d786-6240-4ba4-96c8-05f658e1150c
source-git-commit: 8de94d38fd1d2c001935180851d6877dfe2a8941
workflow-type: tm+mt
source-wordcount: '822'
ht-degree: 0%

---

# [!UICONTROL Perfiles de la cuenta] tablero

La interfaz de usuario (IU) de Adobe Experience Platform proporciona un tablero en el que puede ver información importante sobre los perfiles de su cuenta, tal como se captura durante una instantánea diaria. Esta guía describe cómo acceder y trabajar con el [!UICONTROL Perfiles de la cuenta] tablero en la interfaz de usuario y proporciona más información sobre las visualizaciones que se muestran en el tablero.

Para obtener una descripción general de todas las funciones de la interfaz de usuario del perfil de la cuenta, visite la [guía de interfaz de usuario del perfil de cuenta](../../rtcdp/accounts/account-profile-ui-guide.md).

## Primeros pasos

Debe tener derecho a [Real-time Customer Data Platform B2B Edition](../../rtcdp/b2b-overview.md) para acceder al B2B [!UICONTROL Perfiles de la cuenta] tablero.

## Datos de perfiles de cuenta

La variable [!UICONTROL Perfiles de la cuenta] tablero muestra una instantánea de la información de cuenta unificada de las múltiples fuentes de sus canales de marketing y de los diversos sistemas que su organización utiliza actualmente para almacenar información de cuentas de clientes.

Los datos de perfil de la instantánea muestran los datos exactamente como aparecen en el momento concreto en que se tomó la instantánea. En otras palabras, la instantánea no es una aproximación o muestra de los datos, y la variable [!UICONTROL Perfiles de la cuenta] el tablero no se actualiza en tiempo real.

>[!NOTE]
>
>Los cambios o actualizaciones realizados en los datos desde que se tomó la instantánea no se reflejarán en el panel hasta que se tome la siguiente instantánea.

## Explorar el [!UICONTROL Perfiles de la cuenta] tablero

Para ir a la [!UICONTROL Perfiles de la cuenta] tablero en la interfaz de usuario de Platform, seleccione **[!UICONTROL Perfiles]** under [!UICONTROL Cuentas] en el panel de navegación izquierdo.

![La interfaz de usuario de Platform con Perfiles de cuenta en el panel de navegación izquierdo resaltado y se muestra la pestaña Información general .](../images/account-profiles/account-profiles-dashboard.png)

En el [!UICONTROL Perfiles de la cuenta] tablero, puede: [examinar los perfiles de cuenta introducidos en su organización](#browse-account-profiles)o [ver la totalidad de los datos de perfil de su cuenta de un vistazo mediante widgets](#standard-widgets) que visualizan aspectos de los datos.

## Explorar perfiles de cuenta {#browse-account-profiles}

La variable [!UICONTROL Examinar] permite buscar y ver los perfiles de cuenta de solo lectura introducidos en la organización mediante un ID de cuenta de un origen empresarial conectado o introduciendo directamente los detalles del origen. Desde aquí puede ver información importante que pertenece al perfil de la cuenta, como su nombre, sector, ingresos y segmento, entre otros.

Seleccione el [!UICONTROL ID de perfil] de los resultados mostrados en la [!UICONTROL Examinar] para abrir la pestaña [!UICONTROL Detalles] para el perfil de cuenta.

![La ficha Examinar Perfiles de cuenta muestra los resultados y el ID de perfil resaltado.](../images/account-profiles/account-profiles-browse-tab.png)

La información de perfil de cuenta que se muestra en la variable [!UICONTROL Detalles] se ha combinado desde varios fragmentos de perfil para formar una sola vista de la cuenta individual. Consulte la documentación sobre [exploración de perfiles de cuenta en Real-time Customer Data Platform](../../rtcdp/accounts/account-profile-ui-guide.md#browse-account-profiles) para obtener más información sobre las capacidades de visualización de perfiles de cuenta en la interfaz de usuario de Platform.

## La variable [!UICONTROL Perfiles de la cuenta] [!UICONTROL Información general] {#overview}

La variable [!UICONTROL Información general] está compuesta por utilidades que proporcionan métricas de solo lectura para transmitir información importante sobre los perfiles de su cuenta. Select **[!UICONTROL Modificar tablero]** para cambiar el aspecto del [!UICONTROL Información general] moviendo y cambiando el tamaño de las utilidades.

![La ficha Información general de perfiles de cuenta con el panel Modificar resaltado.](../images/account-profiles/modify-dashboard.png)

Consulte el documento de [modificación de tableros](../customize/modify.md) y [Información general de la biblioteca de utilidades](../customize/widget-library.md) para obtener más información.

## Widgets estándar {#standard-widgets}

Adobe proporciona utilidades estándar que puede utilizar para visualizar distintas métricas relacionadas con los perfiles de su cuenta.

Para obtener más información sobre cada uno de los widgets estándar disponibles, seleccione el nombre de un widget en la siguiente lista:

* [Total de cuentas por sector](#total-accounts-by-industry)
* [Perfiles de cuenta agregados](#account-profiles-added)

### Total de cuentas por sector {#total-accounts-by-industry}

Este widget muestra el número total de cuentas en una única métrica y utiliza un gráfico circular para ilustrar los tamaños proporcionales de los recuentos para las industrias que conforman el número total. La clave proporciona información de codificación de color para las diferentes industrias que conforman el gráfico circular.

Los recuentos individuales de las diferentes industrias se muestran en un cuadro de diálogo cuando el cursor pasa el ratón sobre la sección correspondiente del gráfico circular.

![Total de cuentas por widget de sector.](../images/account-profiles/total-accounts-by-industry-widget.png)

### Perfiles de cuenta agregados {#account-profiles-added}

Esta utilidad utiliza un gráfico de barras con códigos de color para ilustrar el recuento de perfiles agregados a una cuenta durante un período de tiempo determinado y la proporción de diferentes industrias que constituyen estos perfiles añadidos. Las industrias están codificadas por colores y una clave proporciona la información de codificación de color para las diferentes industrias que conforman el gráfico de barras. El periodo de análisis se selecciona en el menú desplegable de la utilidad. El gráfico de barras se puede visualizar a lo largo de 30 días, 90 días y un período de 12 meses.

>[!NOTE]
>
>Como los perfiles solo se agregan a una cuenta y nunca se eliminan, el número más bajo posible de perfiles agregados durante un período de tiempo es cero.

![Se ha agregado la utilidad Perfiles de cuenta .](../images/account-profiles/accounts-profiles-added-widget.png)

## Pasos siguientes

Al seguir este documento, debería poder localizar la variable [!UICONTROL Perfiles de la cuenta] tablero. También debe comprender las métricas que se muestran en los widgets disponibles. Para obtener más información sobre cómo trabajar con perfiles de cuenta como parte de los datos B2B en la interfaz de usuario del Experience Platform, consulte la [información general sobre perfiles de cuenta](../../rtcdp/accounts/account-profile-overview.md) para Adobe Real-Time CDP, B2B Edition.
