---
keywords: Experience Platform;perspectivas;ai del cliente;temas populares;segmentos de ayuda del cliente
solution: Experience Platform, Intelligent Services, Real-time Customer Data Platform
title: Crear segmentos del cliente con puntuaciones previstas
topic: Create a segment
description: Cuando se completa una ejecución de predicción, los Perfiles consumen automáticamente las puntuaciones de propensión predichas. El enriquecimiento de Perfiles con puntuaciones de AI de cliente permite crear segmentos de clientes para encontrar audiencias en función de sus puntuaciones de tendencia. Esta sección proporciona los pasos para crear segmentos mediante el Generador de segmentos.
translation-type: tm+mt
source-git-commit: 698639d6c2f7897f0eb4cce2a1f265a0f7bb57c9
workflow-type: tm+mt
source-wordcount: '318'
ht-degree: 0%

---


# Crear segmentos de clientes con puntuaciones predichas

Cuando se completa una ejecución de predicción, los Perfiles consumen automáticamente las puntuaciones de propensión predichas. El enriquecimiento de Perfiles con puntuaciones de AI de cliente permite crear segmentos de clientes para encontrar audiencias en función de sus puntuaciones de tendencia. Esta sección proporciona los pasos para crear segmentos mediante el Generador de segmentos. Para ver un tutorial más sólido sobre la creación de segmentos, consulte la [guía del usuario del Generador de segmentos](../../../segmentation/ui/segment-builder.md).

>[!IMPORTANT]
>
>Para utilizar este método, es necesario habilitar el Perfil del cliente en tiempo real para el conjunto de datos.

En la interfaz de usuario de la plataforma, haga clic en **[!UICONTROL Segmentos]** en el panel de navegación izquierdo y, a continuación, haga clic en **[!UICONTROL Crear segmento]**.

![](../images/user-guide/segments.png)

Aparece el **Generador de segmentos**. En la columna **[!UICONTROL Campos]** de la izquierda y en la ficha **[!UICONTROL Atributos]**, haga clic en la carpeta denominada **[!UICONTROL Perfil individual XDM]** y, a continuación, haga clic en la carpeta con la Área de nombres de su organización. La carpeta denominada **[!UICONTROL AI del cliente]** contiene los resultados de las ejecuciones de predicción y recibe el nombre de la instancia a la que pertenecen las puntuaciones. Haga clic en una carpeta de instancia para acceder a los resultados de la instancia deseada.

![](../images/user-guide/results.png)

Ubicado en el centro del Generador de segmentos, arrastre y suelte el atributo **[!UICONTROL Puntuación]** en el lienzo *Generador de reglas* para definir una regla.

En la columna *Propiedades del segmento* de la derecha, proporcione un nombre para el segmento.

![](../images/user-guide/properties.png)

Por encima de la columna *Campos* de la izquierda, haga clic en el icono **engranaje** y seleccione una *directiva de combinación* en la lista desplegable. Haga clic en **[!UICONTROL Guardar]** para crear el segmento.

![](../images/user-guide/merge_policy.png)

## Pasos siguientes

Al seguir este tutorial, ha encontrado audiencias basadas en sus puntuaciones de tendencia mediante el Generador de segmentos. Ahora puede realizar el destinatario de sus audiencias activándolas en los destinos. Consulte la [descripción general de destinos](../../../destinations/home.md) para obtener más información.