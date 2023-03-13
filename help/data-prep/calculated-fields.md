---
keywords: Experience Platform;inicio;temas populares;asignar csv;asignar archivo csv;asignar archivo csv a xdm;asignar csv a xdm;guía de iu;asignador;asignación;preparación de datos;preparación de datos;
solution: Experience Platform
title: Resumen de preparación de datos
description: Este documento presenta la preparación de datos en Adobe Experience Platform.
exl-id: 9bef5c3b-368d-4492-bdef-64e67fc25bfd
source-git-commit: d39ae3a31405b907f330f5d54c91b95c0f999eee
workflow-type: tm+mt
source-wordcount: '241'
ht-degree: 2%

---

# Campos calculados

Los campos calculados permiten crear valores basados en los atributos del esquema de entrada. Estos valores se pueden asignar a atributos en el esquema de destino y se les puede proporcionar un nombre y una descripción para facilitar la referencia.

Para crear un campo calculado, seleccione **[!UICONTROL Añadir campo calculado]**.

![](./images/calculated-fields/add-calculated-field.png)

El **[!UICONTROL Crear campo calculado]** aparece el panel. El cuadro de diálogo de la izquierda contiene los campos, funciones y operadores admitidos en los campos calculados. Seleccione una de las pestañas para empezar a añadir funciones, campos u operadores al editor de expresiones.

![](./images/calculated-fields/create-calculated-field.png)

| Tabulación | Descripción |
| --- | ----------- |
| Función | La pestaña functions enumera las funciones disponibles para transformar los datos. Para obtener más información sobre las funciones que puede utilizar en los campos calculados, lea la guía de [Uso de funciones de preparación de datos (asignador)](./functions.md). |
| Campo | La pestaña fields enumera los campos y atributos disponibles en el esquema de origen. |
| Operador | La pestaña operadores enumera los operadores disponibles para transformar los datos. |

Puede añadir manualmente campos, funciones y operadores utilizando el editor de expresiones en el centro. Seleccione el editor para empezar a crear una expresión.

![](./images/calculated-fields/write-calculated-field.png)

Seleccionar **[!UICONTROL Guardar]** para continuar.

La pantalla de asignación vuelve a aparecer con el campo de origen recién creado. Aplique el campo de destino correspondiente y seleccione **[!UICONTROL Finalizar]** para completar la asignación.

![](./images/calculated-fields/new-calculated-field.png)
