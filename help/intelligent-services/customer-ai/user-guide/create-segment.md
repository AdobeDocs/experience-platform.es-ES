---
keywords: Experience Platform;perspectivas;inteligencia artificial aplicada al cliente;temas populares;segmentos de inteligencia artificial aplicada al cliente
solution: Experience Platform, Real-Time Customer Data Platform
feature: Customer AI
title: Creación de segmentos de clientes con puntuaciones previstas
description: Cuando se completa una ejecución de predicción, los perfiles consumen automáticamente las puntuaciones de tendencia predichas. El enriquecimiento de perfiles con puntuaciones de inteligencia artificial aplicada al cliente permite crear segmentos de clientes para encontrar audiencias en función de sus puntuaciones de tendencia. En esta sección se proporcionan los pasos para crear segmentos mediante el Generador de segmentos.
exl-id: ac81f798-f599-4a8d-af25-c00c92e74b4e
source-git-commit: 07a110f6d293abff38804b939014e28f308e3b30
workflow-type: tm+mt
source-wordcount: '318'
ht-degree: 0%

---

# Crear segmentos de clientes con puntuaciones predichas

Cuando se completa una ejecución de predicción, los perfiles consumen automáticamente las puntuaciones de tendencia predichas. El enriquecimiento de perfiles con puntuaciones de inteligencia artificial aplicada al cliente permite crear segmentos de clientes para encontrar audiencias en función de sus puntuaciones de tendencia. En esta sección se proporcionan los pasos para crear segmentos mediante el Generador de segmentos. Para ver un tutorial más completo sobre la creación de segmentos, consulte la [Guía del usuario del Generador de segmentos](../../../segmentation/ui/segment-builder.md).

>[!IMPORTANT]
>
>Para utilizar este método, el perfil del cliente en tiempo real debe estar habilitado para el conjunto de datos.

En la IU de Platform, haga clic en **[!UICONTROL Segmentos]** en el panel de navegación izquierdo y haga clic en **[!UICONTROL Crear segmento]**.

![](../images/user-guide/segments.png)

El **Generador de segmentos** aparece. Desde la izquierda **[!UICONTROL Campos]** y debajo de la **[!UICONTROL Atributos]** , haga clic en la carpeta denominada **[!UICONTROL Perfil individual de XDM]** y, a continuación, haga clic en la carpeta con el área de nombres de su organización. La carpeta denominada **[!UICONTROL Inteligencia artificial aplicada al cliente]** contiene los resultados de las ejecuciones de predicción y tiene el nombre de la instancia a la que pertenecen las puntuaciones. Haga clic en una carpeta de instancias para acceder a los resultados de la instancia deseada.

![](../images/user-guide/results.png)

Situado en el centro del Generador de segmentos, arrastre y suelte el **[!UICONTROL Puntuación]** en el *lienzo del generador de reglas* para definir una regla.

Debajo de la derecha *Propiedades del segmento* , proporcione un nombre para el segmento.

![](../images/user-guide/properties.png)

Encima de la mano izquierda *Campos* Haga clic en la columna **engranaje** y seleccione un *Política de combinación* de la lista desplegable. Clic **[!UICONTROL Guardar]** para crear el segmento.

![](../images/user-guide/merge_policy.png)

## Pasos siguientes

Al seguir este tutorial, ha encontrado correctamente audiencias basadas en sus puntuaciones de tendencia mediante el Generador de segmentos. Ahora puede segmentar las audiencias activándolas en destinos. Consulte la [información general sobre destinos](../../../destinations/home.md) para obtener más información.
