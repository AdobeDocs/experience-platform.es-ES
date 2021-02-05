---
solution: Experience Platform
title: Generar datos de ejemplo para un Esquema XDM en la interfaz de usuario
description: Obtenga información sobre cómo generar datos JSON de muestra basados en un esquema existente en la interfaz de usuario de Adobe Experience Platform.
topic: user guide
translation-type: tm+mt
source-git-commit: 87497ef8a0ebf8de8b6c2dff1650c0b982299e8a
workflow-type: tm+mt
source-wordcount: '336'
ht-degree: 0%

---


# Generar datos de ejemplo para un esquema XDM en la interfaz de usuario

Para poder transferir datos a Adobe Experience Platform, el formato y la estructura de los datos deben cumplir un esquema existente del Modelo de datos de experiencia (XDM). En función de la complejidad del esquema para un conjunto de datos en particular, puede resultar difícil determinar la forma exacta de los datos que el conjunto de datos espera tras la ingestión.

Para cualquier esquema que defina en la interfaz de usuario del Experience Platform, puede generar un objeto JSON de muestra que se ajuste a la estructura del esquema. Este objeto puede servir de plantilla para cualquier dato que se ingrese en conjuntos de datos que empleen el esquema en cuestión.

En la interfaz de usuario de la plataforma, seleccione **[!UICONTROL Esquemas]** en el panel de navegación izquierdo. En la ficha **[!UICONTROL Examinar]**, busque el esquema para el que desea generar datos de ejemplo. Selecciónelo en la lista y actualice el carril correcto para mostrar detalles sobre el esquema. Desde aquí, seleccione **[!UICONTROL Descargar archivo de muestra].**

![](../images/ui/sample/sample-data.png)

El explorador descarga un archivo JSON de muestra. Ahora puede utilizar este archivo como referencia para estructurar los datos al realizar la ingesta en conjuntos de datos que emplean este esquema.

## Pasos siguientes

En esta guía se explica cómo generar un archivo JSON de muestra a partir de un esquema XDM en la interfaz de usuario de la plataforma. Para obtener más información sobre cómo generar datos de muestra mediante la API del Registro de Esquema, consulte la [guía del extremo de datos de muestra](../api/sample-data.md).

Una vez que esté listo para el inicio de la ingesta de datos, consulte el tutorial sobre [asignación de un archivo CSV a XDM](../../ingestion/tutorials/map-a-csv-file.md) para obtener información sobre cómo asignar un archivo de datos plano (como un archivo CSV) a un esquema XDM e ingerirlo en la plataforma. También puede establecer una [conexión de origen](../../sources/home.md) para traer los datos de un origen externo y asignarlos a XDM.

Para obtener más información sobre las capacidades del espacio de trabajo [!UICONTROL Esquemas] en la interfaz de usuario, consulte la información general del [[!UICONTROL espacio de trabajo Esquemas]](./overview.md).