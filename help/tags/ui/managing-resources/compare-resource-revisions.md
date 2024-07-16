---
title: Comparar revisiones de recursos
description: Obtenga información sobre cómo ver el historial de revisiones de un recurso de etiqueta en Adobe Experience Platform.
exl-id: 95b22641-9f6f-4aac-a727-d99098f040a4
source-git-commit: a8b0282004dd57096dfc63a9adb82ad70d37495d
workflow-type: tm+mt
source-wordcount: '912'
ht-degree: 98%

---

# Comparar revisiones de recursos

>[!NOTE]
>
>Adobe Experience Platform Launch se ha convertido en un conjunto de tecnologías de recopilación de datos en Adobe Experience Platform. Como resultado, se han implementado varios cambios terminológicos en la documentación del producto. Consulte el siguiente [documento](../../term-updates.md) para obtener una referencia consolidada de los cambios terminológicos.

Comparar revisiones de recursos para ver el historial de un recurso individual. Puede comparar el estado actual del recurso con versiones anteriores o comparar la versión de un recurso publicada actualmente con el conjunto más reciente de cambios que se han guardado.

## Inicio de una comparación

El inicio de una comparación es igual para todos los tipos de recursos. Abra la vista Edición de un recurso individual y, a continuación, busque el icono de tres puntos junto al botón **[!UICONTROL Guardar]** para ver las acciones disponibles para ese recurso. Seleccione **[!UICONTROL Comparar revisiones]** en la lista.

![Inicio de una comparación para una extensión](../../images/compare-initiate-extension.png)

Para las extensiones, acceda a la vista de detalles seleccionando el botón **[!UICONTROL Configurar]** mientras consulta la lista de extensiones instaladas. Para los elementos y las reglas de datos, seleccione uno de la lista.

## Uso de la vista Compare

Cuando inicia una comparación, la vista predeterminada muestra la última versión en el lado derecho. Esta versión incluye cualquier cambio no guardado que haya realizado sobre el recurso en la vista Edit. (Observe la etiqueta “Unsaved Changes” a la derecha de la imagen siguiente).

A la izquierda, puede elegir entre las revisiones existentes para compararlas con “Latest”.

![Comparación de versiones de la extensión de Analytics](../../images/compare-interpret-extension.png)

Seleccione **[!UICONTROL Usar estos cambios]** para copiar la configuración de la revisión seleccionada (izquierda) en la última versión (derecha). Esto copia la configuración de la anterior revisión a los cambios no guardados más recientes. Si desea mantener estos cambios, asegúrese de **[!UICONTROL Guardar]** tras salir de la vista de comparación.

>[!TIP]
>Los recursos individuales pueden tener atributos y configuración. Esta configuración se almacena como un bloque JSON, que es una forma estructurada de almacenar datos, pero que resulta suficientemente flexible como para que los desarrolladores de extensiones puedan añadir lo que necesiten para hacer que sus extensiones hagan lo que ellos deseen.
>La versión inicial de la vista Compare muestra los ajustes en formato sin procesar como JSON. Las futuras mejoras le permiten ver las versiones de diferentes maneras, lo que incluye comparaciones de código detalladas y mediante las vistas de extensión proporcionadas por los desarrolladores de extensiones.

## Comparación de extensiones

Las extensiones tienen una sola pantalla para mostrar las diferencias entre versiones.

En la vista Compare, se resaltan las diferencias entre las versiones de configuración.  Las adiciones y eliminaciones a la configuración individual se indican mediante una expansión de una línea en cualquier dirección.

![Comparación de distintas versiones de la extensión de Analytics](../../images/compare-extension.png)

Más arriba puede ver los cambios siguientes:

* [!DNL Adobe Analytics] La extensión se actualiza a una nueva versión, indicada por los números de versión en color naranja en la parte superior.
* El `orgID` y `currencyCode` se cambian a la configuración indicada por la expansión de la sección naranja de la configuración.

## Comparación de elementos de datos

Los elementos de datos tienen una sola pantalla para mostrar diferencias, pero como los elementos de datos tienen atributos adicionales además de su configuración, se muestra información adicional. Los atributos que se han cambiado aparecen resaltados en naranja.

![Comparación de distintas versiones de un elemento de datos](../../images/compare-data-element.png)

Más arriba puede ver los cambios siguientes:

* El nombre cambió de “Nombre de página 2” a “Mi nombre de página especial”, tal como indica la barra naranja.
* El tipo cambió de Variable JavaScript a Información de página.
* Se añadió el valor predeterminado “b”.
* Se seleccionó “Forzar valor en minúsculas”.
* Se seleccionó “Borrar texto”.
* La configuración ha cambiado. (La configuración del tipo Variable JavaScript es diferente del tipo Información de página).

En casos en los que el bloque de configuración sea grande, puede ampliar la sección de configuración para poder verlo mejor.

## Comparación de reglas

Las reglas constan de diversos componentes de regla. Para comprender los cambios realizados a una regla, debe saber cómo añadir y eliminar componentes, así como modificaciones de un componente individual. Por lo tanto, al comparar versiones de una regla, existen dos pantallas.

La primera pantalla muestra una vista de alto nivel que resalta los cambios en la organización de los componentes dentro de la regla. Los cambios aparecen resaltados. Se muestran varios tipos de cambios diferentes.

![Comparación de distintas versiones de una regla](../../images/compare-rule.png)

Más arriba puede ver los cambios siguientes:

* El nombre de la regla cambió de “Analytics” a “Baseline Analytics”, y el cambio se indica por la barra naranja junto a Name.
* Se añadió la condición “Core - Domain”, indicada por el icono “+” naranja y la adición del componente a la derecha.
* Se eliminó la acción “[!DNL Adobe Analytics] - Clear Variables”, indicada por el icono “-” naranja y la ausencia del componente a la derecha.
* Se modificó la acción “[!DNL Adobe Analytics] - Set Variables”, indicada por la línea naranja entre las versiones del componente en los lados izquierdo y derecho. Esta línea es recta si el orden de los componentes no ha cambiado.
* La acción “[!DNL Adobe Analytics] - Set Variables” y el orden de acciones “[!DNL Adobe Analytics] - Send Beacon” han cambiado, indicadas por las líneas curvas que conectan las distintas versiones de los componentes en los lados izquierdo y derecho.

Para ver las modificaciones específicas de uno de los componentes de la regla, seleccione el componente específico que desea ver. La línea cambia a azul cuando pasa con el ratón sobre ella.

![Seleccione el componente que desee ver con más detalle](../../images/compare-rule-component-click.png)

La comparación de un componente de regla individual se comporta igual que la comparación de un elemento de datos.

![Comparación de distintas versiones de un componente de regla individual](../../images/compare-rule-component.png)

Más arriba puede ver el siguiente cambio:

* El componente de regla ha cambiado para añadir eVar2 con el valor “1”.

En casos en los que el bloque de configuración sea grande, puede ampliar la sección de configuración para poder verlo mejor.
