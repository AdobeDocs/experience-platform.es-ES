---
keywords: Experience Platform;perspectivas;ai del cliente;temas populares;segmentos de ai del cliente
solution: Experience Platform, Real-time Customer Data Platform
feature: Customer AI
title: Creación de segmentos de clientes con puntuaciones predichas
topic-legacy: Create a segment
description: Cuando se completa una ejecución de predicción, los perfiles consumen automáticamente las puntuaciones de tendencia predichas. El enriquecimiento de perfiles con puntuaciones de Customer AI permite la creación de segmentos de clientes para encontrar audiencias en función de sus puntuaciones de tendencia. En esta sección se proporcionan los pasos para crear segmentos mediante el Generador de segmentos.
exl-id: ac81f798-f599-4a8d-af25-c00c92e74b4e
source-git-commit: 165e5ccae5ca78b3912fef1ba0b3fd4567e231fb
workflow-type: tm+mt
source-wordcount: '318'
ht-degree: 0%

---

# Crear segmentos de clientes con puntuaciones predichas

Cuando se completa una ejecución de predicción, los perfiles consumen automáticamente las puntuaciones de tendencia predichas. El enriquecimiento de perfiles con puntuaciones de Customer AI permite la creación de segmentos de clientes para encontrar audiencias en función de sus puntuaciones de tendencia. En esta sección se proporcionan los pasos para crear segmentos mediante el Generador de segmentos. Para ver un tutorial más robusto sobre la creación de segmentos, consulte la [Guía del usuario del Generador de segmentos](../../../segmentation/ui/segment-builder.md).

>[!IMPORTANT]
>
>Para utilizar este método, es necesario habilitar el perfil del cliente en tiempo real para el conjunto de datos.

En la interfaz de usuario de Platform, haga clic en **[!UICONTROL Segmentos]** en la navegación izquierda y, a continuación, haga clic en **[!UICONTROL Crear segmento]**.

![](../images/user-guide/segments.png)

La variable **Generador de segmentos** aparece. De la izquierda **[!UICONTROL Campos]** y debajo de **[!UICONTROL Atributos]** , haga clic en la carpeta denominada **[!UICONTROL Perfil individual XDM]** y, a continuación, haga clic en la carpeta con el espacio de nombres de su organización. La carpeta denominada **[!UICONTROL Customer AI]** contiene los resultados de las ejecuciones de predicción y reciben el nombre de la instancia a la que pertenecen las puntuaciones. Haga clic en una carpeta de instancia para acceder a los resultados de la instancia deseada.

![](../images/user-guide/results.png)

Situado en el centro del Generador de segmentos, arrastre y suelte el **[!UICONTROL Puntuación]** en la variable *lienzo del generador de reglas* para definir una regla.

Bajo la derecha *Propiedades del segmento* , proporcione un nombre para el segmento.

![](../images/user-guide/properties.png)

Sobre la izquierda *Campos* , haga clic en el botón **engranaje** y seleccione un *Combinar directiva* en la lista desplegable . Haga clic en **[!UICONTROL Guardar]** para crear el segmento.

![](../images/user-guide/merge_policy.png)

## Pasos siguientes

Al seguir este tutorial, ha encontrado correctamente audiencias basadas en sus puntuaciones de tendencia mediante el Generador de segmentos. Ahora puede dirigirse a las audiencias activándolas en destinos. Consulte la [información general sobre destinos](../../../destinations/home.md) para obtener más información.
