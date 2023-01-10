---
solution: Experience Platform
title: Generar datos de ejemplo para un esquema XDM en la interfaz de usuario
description: Obtenga información sobre cómo generar datos JSON de muestra basados en un esquema existente en la interfaz de usuario de Adobe Experience Platform.
exl-id: e60eedb2-2245-42cd-b574-43caf9e3426c
source-git-commit: 5caa4c750c9f786626f44c3578272671d85b8425
workflow-type: tm+mt
source-wordcount: '336'
ht-degree: 0%

---

# Generar datos de ejemplo para un esquema XDM en la interfaz de usuario

Para poder introducir datos en Adobe Experience Platform, el formato y la estructura de los datos deben cumplir con un esquema del Modelo de datos de experiencia (XDM) existente. Dependiendo de la complejidad del esquema para un conjunto de datos en particular, puede ser difícil determinar la forma exacta de los datos que el conjunto de datos espera al ingerirlos.

Para cualquier esquema que defina en la interfaz de usuario del Experience Platform, puede generar un objeto JSON de muestra que se ajuste a la estructura del esquema. Este objeto puede servir de plantilla para cualquier dato que se incorpore en conjuntos de datos que empleen el esquema en cuestión.

En la interfaz de usuario de Platform, seleccione **[!UICONTROL Esquemas]** en el panel de navegación izquierdo. En el **[!UICONTROL Examinar]** , busque el esquema para el que desea generar datos de ejemplo. Selecciónela en la lista y el carril derecho se actualiza para mostrar detalles sobre el esquema. Desde aquí, seleccione **[!UICONTROL Descargar archivo de muestra]**.

![](../images/ui/sample/sample-data.png)

El explorador descarga un archivo JSON de muestra. Ahora puede utilizar este archivo como referencia para estructurar los datos al ingerirlos en conjuntos de datos que empleen este esquema.

## Pasos siguientes

Esta guía explica cómo generar un archivo JSON de muestra a partir de un esquema XDM en la interfaz de usuario de Platform. Para obtener información sobre cómo generar datos de ejemplo mediante la API del Registro de esquemas, consulte la [guía de extremo de datos de ejemplo](../api/sample-data.md).

Una vez que esté listo para empezar a introducir datos, consulte el tutorial en [asignación de un archivo CSV a XDM](../../ingestion/tutorials/map-csv/overview.md) para obtener información sobre cómo asignar un archivo de datos plano (como un CSV) a un esquema XDM e incorporarlo en Platform. También puede establecer un [conexión de origen](../../sources/home.md) para introducir los datos de un origen externo y asignarlos a XDM.

Para obtener más información sobre las capacidades de la variable [!UICONTROL Esquemas] en la interfaz de usuario, consulte [[!UICONTROL Esquemas] información general del espacio de trabajo](./overview.md).
