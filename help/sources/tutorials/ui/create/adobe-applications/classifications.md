---
description: Obtenga información sobre cómo crear un conector de origen de Adobe Analytics en la interfaz de usuario para introducir datos de clasificaciones en Adobe Experience Platform.
title: Creación de una conexión de Adobe Analytics Source para datos de clasificaciones en la IU
exl-id: d606720d-f1ca-47cc-919b-643a8fc61e07
source-git-commit: dfc8a1d51e6dd25210a0b6f24dad4d0f00052414
workflow-type: tm+mt
source-wordcount: '508'
ht-degree: 0%

---

# Crear una conexión de origen de Adobe Analytics para datos de clasificaciones en la interfaz de usuario

>[!TIP]
>
>De forma predeterminada, los datos de clasificaciones de Adobe Analytics se actualizan semanalmente. La ingesta de datos para los datos de sus clasificaciones se procesará siete días después de la configuración inicial del flujo de datos. La primera carga ingiere todos los datos y la siguiente ingesta semanal ejecuta datos incrementales.

Lea este tutorial para ver los pasos sobre cómo introducir los datos de clasificaciones de Adobe Analytics en Adobe Experience Platform a través de la interfaz de usuario.

## Introducción

Este tutorial requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): El marco estandarizado mediante el cual Experience Platform organiza los datos de experiencia del cliente.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): proporciona un perfil de consumidor unificado y en tiempo real basado en los datos agregados de varias fuentes.
* [[!DNL Sandboxes]](../../../../../sandboxes/home.md): Experience Platform proporciona zonas protegidas virtuales que dividen una sola instancia de Experience Platform en entornos virtuales independientes para ayudar a desarrollar y evolucionar aplicaciones de experiencia digital.

El conector de origen de clasificaciones de Analytics requiere que los datos se hayan migrado a la nueva infraestructura de clasificaciones de Adobe Analytics antes de su uso. Para confirmar el estado de migración de sus datos, póngase en contacto con el equipo de su cuenta de Adobe.

## Seleccionar las clasificaciones

En la interfaz de usuario de Experience Platform, seleccione **[!UICONTROL Sources]** en el panel de navegación izquierdo para acceder al área de trabajo [!UICONTROL Sources]. Puede seleccionar la categoría adecuada del catálogo en la parte izquierda de la pantalla. También puede encontrar la fuente específica con la que desea trabajar utilizando la opción de búsqueda.

En la categoría *aplicaciones de Adobe*, seleccione **[!UICONTROL Adobe Analytics]** y, a continuación, seleccione **[!UICONTROL Set up]**.

>[!TIP]
>
>Los orígenes del catálogo de orígenes muestran la opción **[!UICONTROL Set up]** si no hay una cuenta autenticada. Una vez autenticada una cuenta, la opción cambia a **[!UICONTROL Add data]**.

![Catálogo de orígenes en la interfaz de usuario de Experience Platform con el origen de Adobe Analytics seleccionado.](../../../../images/tutorials/create/classifications/catalog.png)

A continuación, seleccione [!UICONTROL Classifications] y luego seleccione los conjuntos de datos de clasificaciones que desea introducir en Experience Platform. También puede utilizar la búsqueda para filtrar y seleccionar clasificaciones específicas.

Puede seleccionar hasta 30 conjuntos de datos de clasificaciones diferentes para incluirlos en Experience Platform. Los conjuntos de datos que seleccione aparecerán en el carril derecho. Cuando haya terminado, seleccione [!UICONTROL Next] para continuar.

![La página de clasificaciones con varios conjuntos de datos de clasificaciones seleccionados.](../../../../images/tutorials/create/classifications/select.png)

## Revise sus clasificaciones

Aparece el paso **[!UICONTROL Review]**, que le permite revisar los conjuntos de datos de clasificaciones seleccionados antes de crearlos. Los detalles se agrupan en las siguientes categorías:

* **[!UICONTROL Connection]**: muestra la plataforma de origen y el estado de la conexión.
* **[!UICONTROL Data type]**: muestra el número de clasificaciones seleccionadas.
* **[!UICONTROL Scheduling]**: muestra la frecuencia de sincronización de los datos de las clasificaciones. **Nota**: los datos de las clasificaciones se actualizan semanalmente.

Una vez que haya revisado el flujo de datos, haga clic en **[!UICONTROL Finish]** y espere un poco para que se cree el flujo de datos.

![Página de revisión de datos de clasificaciones de Adobe Analytics.](../../../../images/tutorials/create/classifications/review.png)

## Próximos pasos

Al seguir este tutorial, ha creado un conector de datos de clasificaciones de Analytics que lleva los datos de las clasificaciones a Experience Platform. Consulte los siguientes documentos para obtener más información sobre [!DNL Analytics] y los datos de clasificaciones:

* [Información general sobre el conector de origen Adobe Analytics](../../../../connectors/adobe-applications/analytics.md)
* [Crear una conexión de origen de Analytics para los datos del grupo de informes en la IU](./analytics.md)
* [Acerca de las clasificaciones](https://experienceleague.adobe.com/docs/analytics/components/classifications/c-classifications.html?lang=es)
