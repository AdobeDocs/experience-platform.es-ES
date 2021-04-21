---
keywords: Experience Platform;inicio;temas populares; eliminar flujos de datos
description: El espacio de trabajo de orígenes le permite eliminar flujos de datos de flujo continuo y por lotes existentes que contengan errores o se hayan vuelto obsoletos.
solution: Experience Platform
title: Eliminar flujos de datos en la interfaz de usuario
topic-legacy: overview
type: Tutorial
exl-id: aa224467-7733-40de-aab7-0ff1c557abf2
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '359'
ht-degree: 1%

---

# Eliminar flujos de datos en la interfaz de usuario

El espacio de trabajo [!UICONTROL Sources] le permite eliminar flujos de datos de flujo y lote existentes que contengan errores o se hayan vuelto obsoletos.

Este tutorial proporciona pasos para eliminar flujos de datos mediante el espacio de trabajo [!UICONTROL Sources].

## Primeros pasos

Este tutorial requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

- [Fuentes](../../home.md):  [!DNL Experience Platform] permite la ingesta de datos de varias fuentes, al mismo tiempo que permite estructurar, etiquetar y mejorar los datos entrantes mediante  [!DNL Platform] servicios.
- [Simuladores para pruebas](../../../sandboxes/home.md):  [!DNL Experience Platform] proporciona entornos limitados virtuales que dividen una sola  [!DNL Platform] instancia en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

## Eliminar flujos de datos

En la [interfaz de usuario del Experience Platform](https://platform.adobe.com), seleccione **[!UICONTROL Sources]** en el panel de navegación izquierdo para acceder al espacio de trabajo [!UICONTROL Sources] y, a continuación, seleccione **[!UICONTROL Dataflows]** en el encabezado superior.

![catálogo](../../images/tutorials/delete/catalog.png)

Aparece la página **[!UICONTROL Dataflows]**. En esta página hay una lista de flujos de datos visibles, que incluye información sobre su conjunto de datos de destino, fuente, nombre de cuenta y fecha de creación.

Seleccione el icono de filtro (![filter-icon](../../images/tutorials/delete/filter.png)) en la parte superior izquierda para iniciar el panel de ordenación.

![flujos de datos](../../images/tutorials/delete/dataflows.png)

El panel de ordenación proporciona una lista de todas las fuentes. Puede seleccionar más de una fuente de la lista para acceder a una selección filtrada de flujos de datos asociados a las fuentes particulares seleccionadas.

Seleccione el origen con el que desea trabajar para ver una lista de sus flujos de datos existentes. Una vez identificado el flujo de datos que desea eliminar, seleccione los puntos suspensivos (`...`) junto al nombre del flujo de datos.

![dataflows-filter](../../images/tutorials/delete/dataflows-filter.png)

Aparece un menú desplegable que le ofrece las opciones para editar la programación del flujo de datos, desactivarlo o eliminarlo por completo.

Seleccione **[!UICONTROL Delete]** para eliminar el flujo de datos.

![delete](../../images/tutorials/delete/delete.png)

Aparece un cuadro de diálogo de confirmación final. Seleccione **[!UICONTROL Delete]** para completar el proceso.

![confirm](../../images/tutorials/delete/confirm.png)

Después de unos momentos, aparece un cuadro de confirmación en la parte inferior de la pantalla para confirmar que la eliminación se ha realizado correctamente.

![confirmado](../../images/tutorials/delete/confirmed.png)

## Pasos siguientes

Al seguir este tutorial, ha utilizado correctamente el espacio de trabajo [!UICONTROL Sources] para eliminar un flujo de datos existente.

Consulte el tutorial sobre la [eliminación de flujos de datos mediante la API de servicio de flujo](../../tutorials/api/delete-dataflows.md) para ver los pasos para realizar estas operaciones mediante programación mediante llamadas a API.
