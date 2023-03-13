---
keywords: Experience Platform;inicio;temas populares; eliminar flujos de datos
description: El espacio de trabajo de orígenes permite eliminar flujos de datos de flujo y por lotes existentes que contienen errores o que han quedado obsoletos.
solution: Experience Platform
title: Eliminación de flujos de datos en la IU
type: Tutorial
exl-id: aa224467-7733-40de-aab7-0ff1c557abf2
source-git-commit: 90eb6256179109ef7c445e2a5a8c159fb6cbfe28
workflow-type: tm+mt
source-wordcount: '368'
ht-degree: 1%

---

# Eliminación de flujos de datos en la IU

El [!UICONTROL Fuentes] workspace le permite eliminar flujos de datos de flujo y lote existentes que contienen errores o que han quedado obsoletos.

Este tutorial proporciona pasos para eliminar flujos de datos mediante la variable [!UICONTROL Fuentes] workspace.

## Primeros pasos

Este tutorial requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

- [Fuentes](../../home.md): [!DNL Experience Platform] permite la ingesta de datos desde varias fuentes, al tiempo que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante [!DNL Platform] servicios.
- [Zonas protegidas](../../../sandboxes/home.md): [!DNL Experience Platform] proporciona zonas protegidas virtuales que dividen una sola [!DNL Platform] en entornos virtuales independientes para ayudar a desarrollar y evolucionar aplicaciones de experiencia digital.

## Eliminar flujos de datos

En el [IU de Experience Platform](https://platform.adobe.com), seleccione **[!UICONTROL Fuentes]** desde la navegación izquierda para acceder a [!UICONTROL Fuentes] workspace y, a continuación, seleccione **[!UICONTROL Flujos de datos]** desde el encabezado superior.

![catalogar](../../images/tutorials/delete/catalog.png)

El **[!UICONTROL Flujos de datos]** página. En esta página hay una lista de flujos de datos visibles, incluida la información sobre su conjunto de datos de destinatario, origen, nombre de cuenta y fecha de creación.

Seleccione el icono de filtro (![filter-icon](../../images/tutorials/delete/filter.png)) en la parte superior izquierda para iniciar el panel de ordenación.

![flujos de datos](../../images/tutorials/delete/dataflows.png)

El panel de ordenación proporciona una lista de todas las fuentes. Puede seleccionar más de un origen en la lista para acceder a una selección filtrada de flujos de datos asociados con los orígenes concretos seleccionados.

Seleccione la fuente con la que desea trabajar para ver una lista de sus flujos de datos existentes. Una vez identificado el flujo de datos que desea eliminar, seleccione los puntos suspensivos (`...`) junto al nombre del flujo de datos.

![dataflows-filter](../../images/tutorials/delete/dataflows-filter.png)

Aparecerá un menú desplegable con opciones para editar la programación del flujo de datos, deshabilitarlo o eliminarlo por completo.

Seleccionar **[!UICONTROL Eliminar]** para eliminar el flujo de datos.

![eliminar](../../images/tutorials/delete/delete.png)

Aparecerá un cuadro de diálogo de confirmación final. Seleccionar **[!UICONTROL Eliminar]** para completar el proceso.

![confirm](../../images/tutorials/delete/confirm.png)

Después de unos momentos, aparece un cuadro de confirmación en la parte inferior de la pantalla para confirmar que la eliminación se ha realizado correctamente.

![confirmado](../../images/tutorials/delete/confirmed.png)

## Pasos siguientes

Al seguir este tutorial, ha utilizado correctamente la variable [!UICONTROL Fuentes] workspace para eliminar un flujo de datos existente.

Consulte el tutorial sobre [eliminación de flujos de datos mediante la API de Flow Service](../../tutorials/api/delete-dataflows.md) para obtener información sobre cómo realizar estas operaciones mediante programación utilizando llamadas a la API.
