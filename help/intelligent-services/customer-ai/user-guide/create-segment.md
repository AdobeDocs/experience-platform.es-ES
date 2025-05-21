---
keywords: Experience Platform;perspectivas;inteligencia artificial aplicada al cliente;temas populares;segmentos de inteligencia artificial aplicada al cliente
solution: Experience Platform, Real-Time Customer Data Platform
feature: Customer AI
title: Creación de segmentos de clientes con puntuaciones previstas
description: Cuando se completa una ejecución de predicción, los perfiles consumen automáticamente las puntuaciones de tendencia predichas. El enriquecimiento de perfiles con puntuaciones de inteligencia artificial aplicada al cliente permite crear segmentos de clientes para encontrar audiencias en función de sus puntuaciones de tendencia. En esta sección se proporcionan los pasos para crear segmentos mediante el Generador de segmentos.
exl-id: ac81f798-f599-4a8d-af25-c00c92e74b4e
source-git-commit: 73dea391f8fcb1d2d491c814b453afb4e538459d
workflow-type: tm+mt
source-wordcount: '337'
ht-degree: 0%

---

# Crear segmentos de clientes con puntuaciones predichas

Cuando se completa una ejecución de predicción, los perfiles consumen automáticamente las puntuaciones de tendencia predichas. El enriquecimiento de perfiles con puntuaciones de inteligencia artificial aplicada al cliente permite crear segmentos de clientes para encontrar audiencias en función de sus puntuaciones de tendencia. En esta sección se proporcionan los pasos para crear segmentos mediante el Generador de segmentos. Para obtener un tutorial más sólido sobre la creación de segmentos, consulte la [guía del usuario del Generador de segmentos](../../../segmentation/ui/segment-builder.md).

>[!IMPORTANT]
>
>Para utilizar este método, el perfil del cliente en tiempo real debe estar habilitado para el conjunto de datos.

En la interfaz de usuario de Experience Platform, haga clic en **[!UICONTROL Segmentos]** en el panel de navegación izquierdo y luego haga clic en **[!UICONTROL Crear segmento]**.

![Captura de pantalla de la página Segmentos en la interfaz de usuario de Experience Platform, que muestra la opción de crear un nuevo segmento.](../images/user-guide/segments_new.png)

Aparecerá **Generador de segmentos**. En la columna izquierda de **[!UICONTROL Campos]** y debajo de la ficha **[!UICONTROL Atributos]**, haga clic en la carpeta denominada **[!UICONTROL Perfil individual de XDM]** y, a continuación, haga clic en la carpeta con el área de nombres de su organización. La carpeta **[!UICONTROL Customer AI]** contiene los resultados de las ejecuciones de predicción y recibe el nombre de la instancia a la que pertenecen las puntuaciones. Haga clic en una carpeta de instancias para acceder a los resultados de la instancia deseada.

![](../images/user-guide/results_new.png)

Ubicado en el centro del Generador de segmentos, arrastre y suelte el atributo **[!UICONTROL Score]** en el *lienzo del generador de reglas* para definir una regla.

En la columna derecha *Propiedades del segmento*, proporcione un nombre para el segmento.

![](../images/user-guide/properties_new.png)

Encima de la columna izquierda de *Campos*, haz clic en el icono de **engranaje** y selecciona una *política de combinación* en la lista desplegable. Haga clic en **[!UICONTROL Guardar]** para crear el segmento.

![](../images/user-guide/merge_policy_new.png)

## Pasos siguientes

Al seguir este tutorial, ha encontrado correctamente audiencias basadas en sus puntuaciones de tendencia mediante el Generador de segmentos. Ahora puede segmentar las audiencias activándolas en destinos. Consulte la [descripción general de destinos](../../../destinations/home.md) para obtener más información.
