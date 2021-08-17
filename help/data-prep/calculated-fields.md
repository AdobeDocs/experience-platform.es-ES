---
keywords: Experience Platform;inicio;temas populares;asignación de csv;asignación de archivo csv;asignación de archivo csv a xdm;asignación de csv a xdm;guía de ui;asignador;asignación;preparación de datos;preparación de datos;preparación de datos;
solution: Experience Platform
title: Información general sobre la preparación de datos
topic-legacy: overview
description: Este documento presenta la preparación de datos dentro de Adobe Experience Platform.
exl-id: f15eeb50-a531-4560-a524-1a670fbda706
source-git-commit: 2cc72708b77396e70d006ecd1e21fd2d495ddf61
workflow-type: tm+mt
source-wordcount: '241'
ht-degree: 2%

---


# Campos calculados

Los campos calculados permiten que se creen valores en función de los atributos del esquema de entrada. Estos valores se pueden asignar a atributos en el esquema de destino y se les puede proporcionar un nombre y una descripción para facilitar la referencia.

Para crear un campo calculado, seleccione **[!UICONTROL Add calculated field]**.

![](./images/calculated-fields/add-calculated-field.png)

Aparece el panel **[!UICONTROL Crear campo calculado]**. El cuadro de diálogo izquierdo contiene los campos, las funciones y los operadores admitidos en los campos calculados. Seleccione una de las pestañas para empezar a añadir funciones, campos u operadores al editor de expresiones.

![](./images/calculated-fields/create-calculated-field.png)

| Tabulación | Descripción |
| --- | ----------- |
| Función | La pestaña funciones enumera las funciones disponibles para transformar los datos. Para obtener más información sobre las funciones que puede utilizar en los campos calculados, lea la guía sobre el uso de las funciones [de preparación de datos (Mapper)](./functions.md). |
| Campo | La pestaña fields enumera los campos y atributos disponibles en el esquema de origen. |
| Operador | La pestaña operadores enumera los operadores disponibles para transformar los datos. |

Puede añadir manualmente campos, funciones y operadores con el editor de expresiones del centro. Seleccione el editor para comenzar a crear una expresión.

![](./images/calculated-fields/write-calculated-field.png)

Seleccione **[!UICONTROL Save]** para continuar.

La pantalla de asignación vuelve a aparecer con el campo de origen recién creado. Aplique el campo de destino correspondiente correspondiente y seleccione **[!UICONTROL Finish]** para completar la asignación.

![](./images/calculated-fields/new-calculated-field.png)