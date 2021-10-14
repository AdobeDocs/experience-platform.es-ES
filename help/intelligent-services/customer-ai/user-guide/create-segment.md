---
keywords: Experience Platform;perspectivas;ai del cliente;temas populares;segmentos de ai del cliente
solution: Experience Platform, Intelligent Services, Real-time Customer Data Platform
feature: Customer AI
title: Creación de segmentos de clientes con puntuaciones predichas
topic-legacy: Create a segment
description: Cuando se completa una ejecución de predicción, los perfiles consumen automáticamente las puntuaciones de tendencia predichas. El enriquecimiento de perfiles con puntuaciones de Customer AI permite la creación de segmentos de clientes para encontrar audiencias en función de sus puntuaciones de tendencia. En esta sección se proporcionan los pasos para crear segmentos mediante el Generador de segmentos.
exl-id: ac81f798-f599-4a8d-af25-c00c92e74b4e
source-git-commit: c3320f040383980448135371ad9fae583cfca344
workflow-type: tm+mt
source-wordcount: '318'
ht-degree: 0%

---

# Crear segmentos de clientes con puntuaciones predichas

Cuando se completa una ejecución de predicción, los perfiles consumen automáticamente las puntuaciones de tendencia predichas. El enriquecimiento de perfiles con puntuaciones de Customer AI permite la creación de segmentos de clientes para encontrar audiencias en función de sus puntuaciones de tendencia. En esta sección se proporcionan los pasos para crear segmentos mediante el Generador de segmentos. Para ver un tutorial más robusto sobre la creación de segmentos, consulte la [guía del usuario del Generador de segmentos](../../../segmentation/ui/segment-builder.md).

>[!IMPORTANT]
>
>Para utilizar este método, es necesario habilitar el perfil del cliente en tiempo real para el conjunto de datos.

En la interfaz de usuario de Platform, haga clic en **[!UICONTROL Segmentos]** en el panel de navegación izquierdo y, a continuación, haga clic en **[!UICONTROL Crear segmento]**.

![](../images/user-guide/segments.png)

Aparece el **Generador de segmentos**. En la columna izquierda **[!UICONTROL Fields]** y en la pestaña **[!UICONTROL Attributes]**, haga clic en la carpeta denominada **[!UICONTROL XDM Individual Profile]** y, a continuación, haga clic en la carpeta con el área de nombres de su organización. La carpeta denominada **[!UICONTROL Customer AI]** contiene los resultados de las ejecuciones de predicción y recibe el nombre de la instancia a la que pertenecen las puntuaciones. Haga clic en una carpeta de instancia para acceder a los resultados de la instancia deseada.

![](../images/user-guide/results.png)

Ubicado en el centro del Generador de segmentos, arrastre y suelte el atributo **[!UICONTROL Score]** en el *lienzo del Generador de reglas* para definir una regla.

En la columna derecha *Segment properties*, proporcione un nombre para el segmento.

![](../images/user-guide/properties.png)

Sobre la columna *Fields* a la izquierda, haga clic en el icono **engranaje** y seleccione una *Política de combinación* en la lista desplegable. Haga clic en **[!UICONTROL Guardar]** para crear el segmento.

![](../images/user-guide/merge_policy.png)

## Pasos siguientes

Al seguir este tutorial, ha encontrado correctamente audiencias basadas en sus puntuaciones de tendencia mediante el Generador de segmentos. Ahora puede dirigirse a las audiencias activándolas en destinos. Consulte [información general sobre destinos](../../../destinations/home.md) para obtener más información.
