---
keywords: Experience Platform;insights;customer ai;popular topics
solution: Experience Platform
title: Crear segmentos de clientes con puntuaciones predichas
topic: Create a segment
description: Cuando se completa una ejecución de predicción, los Perfiles consumen automáticamente las puntuaciones de propensión predichas. El enriquecimiento de Perfiles con puntuaciones de AI de cliente permite crear segmentos de clientes para encontrar audiencias en función de sus puntuaciones de tendencia. Esta sección proporciona los pasos para crear segmentos mediante el Generador de segmentos.
translation-type: tm+mt
source-git-commit: c30bbaead775e68f869b080e24e18d4a23cda973
workflow-type: tm+mt
source-wordcount: '317'
ht-degree: 0%

---


# Crear segmentos de clientes con puntuaciones predichas

Cuando se completa una ejecución de predicción, los Perfiles consumen automáticamente las puntuaciones de propensión predichas. El enriquecimiento de Perfiles con puntuaciones de AI de cliente permite crear segmentos de clientes para encontrar audiencias en función de sus puntuaciones de tendencia. Esta sección proporciona los pasos para crear segmentos mediante el Generador de segmentos. Para ver un tutorial más sólido sobre la creación de segmentos, consulte la guía [de usuario del Generador](../../../segmentation/ui/segment-builder.md)de segmentos.

>[!IMPORTANT]
>
>Para utilizar este método, es necesario habilitar el Perfil del cliente en tiempo real para el conjunto de datos.

En la interfaz de usuario de la plataforma, haga clic en **[!UICONTROL Segmentos]** en el panel de navegación izquierdo y, a continuación, haga clic en **[!UICONTROL Crear segmento]**.

![](../images/user-guide/segments.png)

Aparece el Generador *de segmentos* . En la columna *Campos* de la izquierda y en la ficha *Atributos* , haga clic en la carpeta denominada Perfil **[!UICONTROL individual]** XDM y, a continuación, haga clic en la carpeta con la Área de nombres de su organización. La carpeta denominada **[!UICONTROL Customer AI]** contiene los resultados de las ejecuciones de predicciones y recibe el nombre de la instancia a la que pertenecen las puntuaciones. Haga clic en una carpeta de instancia para acceder a los resultados de la instancia deseada.

![](../images/user-guide/results.png)

Situado en el centro del Generador de segmentos, arrastre y suelte el atributo **[!UICONTROL Puntuación]** en el lienzo *del creador de* reglas para definir una regla.

En la columna de propiedades *del* segmento de la derecha, proporcione un nombre para el segmento.

![](../images/user-guide/properties.png)

Por encima de la columna *Campos* de la izquierda, haga clic en el icono de **engranaje** y seleccione una política *de* combinación en la lista desplegable. Click **[!UICONTROL Save]** to create the segment.

![](../images/user-guide/merge_policy.png)

## Pasos siguientes

Al seguir este tutorial, ha encontrado audiencias basadas en sus puntuaciones de tendencia mediante el Generador de segmentos. Ahora puede realizar el destinatario de sus audiencias activándolas en los destinos. Consulte la descripción general [de](https://docs.adobe.com/content/help/en/experience-platform/rtcdp/destinations/destinations-overview.html) destinos para obtener más información.