---
keywords: Experience Platform;inicio;temas populares; eliminar flujos de datos
description: El espacio de trabajo de orígenes permite eliminar flujos de datos de flujo y por lotes existentes que contienen errores o que han quedado obsoletos.
solution: Experience Platform
title: Eliminación de flujos de datos en la IU
type: Tutorial
exl-id: aa224467-7733-40de-aab7-0ff1c557abf2
source-git-commit: c2832821ea6f9f630e480c6412ca07af788efd66
workflow-type: tm+mt
source-wordcount: '367'
ht-degree: 1%

---

# Eliminación de flujos de datos en la IU

El área de trabajo [!UICONTROL Sources] le permite eliminar flujos de datos existentes por lotes y de flujo continuo que contienen errores o que han quedado obsoletos.

Este tutorial proporciona pasos para eliminar flujos de datos mediante el área de trabajo [!UICONTROL Sources].

## Introducción

Este tutorial requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

- [Fuentes](../../home.md): [!DNL Experience Platform] permite la ingesta de datos de varias fuentes al tiempo que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de [!DNL Platform].
- [Zonas protegidas](../../../sandboxes/home.md): [!DNL Experience Platform] proporciona zonas protegidas virtuales que dividen una sola instancia de [!DNL Platform] en entornos virtuales independientes para ayudar a desarrollar y evolucionar aplicaciones de experiencia digital.

## Eliminar flujos de datos

En la [interfaz de usuario del Experience Platform](https://platform.adobe.com), seleccione **[!UICONTROL Fuentes]** en el panel de navegación izquierdo para acceder al área de trabajo de [!UICONTROL Fuentes] y, a continuación, seleccione **[!UICONTROL Flujos de datos]** en el encabezado superior.

![catálogo](../../images/tutorials/delete/catalog.png)

Aparecerá la página **[!UICONTROL Flujos de datos]**. En esta página hay una lista de flujos de datos visibles, incluida la información sobre su conjunto de datos de destinatario, origen, nombre de cuenta y fecha de creación.

Seleccione el icono de filtro (![filter-icon](/help/images/icons/filter.png)) en la parte superior izquierda para iniciar el panel de ordenación.

![flujos de datos](../../images/tutorials/delete/dataflows.png)

El panel de ordenación proporciona una lista de todas las fuentes. Puede seleccionar más de un origen en la lista para acceder a una selección filtrada de flujos de datos asociados con los orígenes concretos seleccionados.

Seleccione la fuente con la que desea trabajar para ver una lista de sus flujos de datos existentes. Una vez identificado el flujo de datos que desea eliminar, seleccione los puntos suspensivos (`...`) junto al nombre del flujo de datos.

![filtro de flujos de datos](../../images/tutorials/delete/dataflows-filter.png)

Aparecerá un menú desplegable con opciones para editar la programación del flujo de datos, deshabilitarlo o eliminarlo por completo.

Seleccione **[!UICONTROL Delete]** para eliminar el flujo de datos.

![eliminar](../../images/tutorials/delete/delete.png)

Aparecerá un cuadro de diálogo de confirmación final. Seleccione **[!UICONTROL Eliminar]** para completar el proceso.

![confirmar](../../images/tutorials/delete/confirm.png)

Después de unos momentos, aparece un cuadro de confirmación en la parte inferior de la pantalla para confirmar que la eliminación se ha realizado correctamente.

![confirmado](../../images/tutorials/delete/confirmed.png)

## Pasos siguientes

Siguiendo este tutorial, ha utilizado correctamente el espacio de trabajo [!UICONTROL Sources] para eliminar un flujo de datos existente.

Consulte el tutorial sobre [eliminación de flujos de datos mediante la API de Flow Service](../../tutorials/api/delete-dataflows.md) para ver los pasos sobre cómo realizar estas operaciones mediante programación mediante llamadas a la API.
