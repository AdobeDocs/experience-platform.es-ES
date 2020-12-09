---
keywords: Experience Platform;home;popular topics; delete dataflows
description: El espacio de trabajo de orígenes le permite eliminar flujos de datos de flujo y lote existentes que contengan errores o que se hayan vuelto obsoletos.
solution: Experience Platform
title: Eliminar flujos de datos
topic: overview
type: Tutorial
translation-type: tm+mt
source-git-commit: 7cb5862112c80e386e697aa2bd503abe49f11a3f
workflow-type: tm+mt
source-wordcount: '358'
ht-degree: 1%

---


# Eliminar flujos de datos en la interfaz de usuario

El espacio de trabajo [!UICONTROL Fuentes] le permite eliminar flujos de datos de flujo y lotes existentes que contengan errores o se hayan vuelto obsoletos.

Este tutorial proporciona pasos para eliminar flujos de datos mediante el espacio de trabajo [!UICONTROL Fuentes] .

## Primeros pasos

Este tutorial requiere un conocimiento práctico de los siguientes componentes de Adobe Experience Platform:

- [Fuentes](../../home.md): [!DNL Experience Platform] permite la ingesta de datos desde varias fuentes, al tiempo que le permite estructurar, etiquetar y mejorar los datos entrantes mediante [!DNL Platform] servicios.
- [Simuladores](../../../sandboxes/home.md): [!DNL Experience Platform] proporciona entornos limitados virtuales que dividen una sola [!DNL Platform] instancia en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

## Eliminar flujos de datos

En la interfaz de usuario [del](https://platform.adobe.com)Experience Platform, seleccione **[!UICONTROL Fuentes]** en el panel de navegación izquierdo para acceder al espacio de trabajo [!UICONTROL Fuentes] y, a continuación, seleccione **[!UICONTROL Flujos]** de datos en el encabezado superior.

![catálogo](../../images/tutorials/delete/catalog.png)

Aparece la página **[!UICONTROL Flujos]** de datos. En esta página hay una lista de flujos de datos visualizables, incluida información sobre su conjunto de datos de destinatario, fuente, nombre de cuenta y fecha de creación.

Seleccione el icono de filtro (icono![de](../../images/tutorials/delete/filter.png)filtro) en la parte superior izquierda para iniciar el panel de ordenación.

![flujos de datos](../../images/tutorials/delete/dataflows.png)

El panel Ordenar proporciona una lista de todas las fuentes. Puede seleccionar más de un origen de la lista para acceder a una selección filtrada de flujos de datos asociados a los orígenes concretos que ha seleccionado.

Seleccione el origen con el que desea trabajar para ver una lista de sus flujos de datos existentes. Una vez identificado el flujo de datos que desea eliminar, seleccione las elipses (`...`) junto al nombre del flujo de datos.

![dataflows-filter](../../images/tutorials/delete/dataflows-filter.png)

Aparece un menú desplegable con opciones para editar la programación del flujo de datos, deshabilitar el flujo de datos o eliminarlo por completo.

Seleccione **[!UICONTROL Eliminar]** para eliminar el flujo de datos.

![delete](../../images/tutorials/delete/delete.png)

Aparecerá un cuadro de diálogo de confirmación final. Seleccione **[!UICONTROL Eliminar]** para completar el proceso.

![confirm](../../images/tutorials/delete/confirm.png)

Al cabo de unos minutos, aparece un cuadro de confirmación en la parte inferior de la pantalla para confirmar que la eliminación se ha realizado correctamente.

![confirmado](../../images/tutorials/delete/confirmed.png)

## Pasos siguientes

Siguiendo este tutorial, ha utilizado correctamente el espacio de trabajo [!UICONTROL Fuentes] para eliminar un flujo de datos existente.

Consulte el tutorial sobre la [eliminación de flujos de datos mediante la API](../../tutorials/api/delete-dataflows.md) de servicio de flujo para ver los pasos para realizar estas operaciones mediante programación mediante llamadas a API.