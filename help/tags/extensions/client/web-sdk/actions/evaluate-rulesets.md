---
title: Evaluar conjuntos de reglas
description: Almacenar en déclencheur manualmente una evaluación de conjunto de reglas.
source-git-commit: 46e5d007b27eaa67c9ee49e35a711424de383d68
workflow-type: tm+mt
source-wordcount: '138'
ht-degree: 0%

---

# Evaluar conjuntos de reglas

El tipo de acción **[!UICONTROL Evaluate rulesets]** le permite almacenar manualmente en déclencheur las evaluaciones del conjunto de reglas. Adobe Journey Optimizer devuelve los conjuntos de reglas para que sean compatibles con funciones como los mensajes en el explorador.

1. Inicie sesión en [experience.adobe.com](https://experience.adobe.com) con sus credenciales de Adobe ID.
1. Vaya a **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Seleccione la propiedad de etiquetas que desee.
1. Vaya a **[!UICONTROL Rules]** y, a continuación, seleccione la regla que desee.
1. En [!UICONTROL Actions], seleccione una acción existente o cree una acción.
1. Establezca el campo desplegable [!UICONTROL Extension] en **[!UICONTROL Adobe Experience Platform Web SDK]**, luego establezca [!UICONTROL Action type] en **[!UICONTROL Evaluate rulesets]**.

![Imagen de la interfaz de usuario de Experience Platform que muestra el tipo de acción de respuesta Evaluar conjuntos de reglas.](../assets/evaluate-rulesets.png)

## Campos disponibles

Este tipo de acción admite las siguientes opciones:

* **[!UICONTROL Render visual personalization decisions]**: una casilla de verificación que, cuando está habilitada, procesa decisiones de personalización visuales para los elementos del conjunto de reglas que coinciden.
* **[!UICONTROL Decision context]**: asignación de clave-valor que se usa al evaluar conjuntos de reglas de Adobe Journey Optimizer para la toma de decisiones en el dispositivo. Puede proporcionar el contexto de decisión manualmente o mediante un elemento de datos.
