---
title: Mejoras en la composición de audiencias
description: Obtenga información acerca de las mejoras realizadas en la Composición de audiencia con enriquecimiento de audiencia y activación más rápida.
hide: true
hidefromtoc: true
source-git-commit: 9c790f0b47161301fa8c02c4afb7edfb925e1499
workflow-type: tm+mt
source-wordcount: '470'
ht-degree: 0%

---


# Mejoras de Composición de audiencia

Ahora tiene acceso a **dos** mejoras para la composición de audiencias:

- [Enriquecimiento de audiencia](#audience-enrichment)
- [Activación más rápida](#faster-activation)

## Enriquecimiento de audiencia {#audience-enrichment}

El enriquecimiento de audiencia le permite generar la matriz de valores que permiten que sus perfiles cumplan los requisitos de la audiencia que ha creado.

Para agregar enriquecimientos de audiencia a la composición, seleccione el bloque superior **[!UICONTROL Audience]** dentro del lienzo. Después de asignar un nombre a la audiencia, seleccione **[!UICONTROL Build rule]** para abrir el lienzo del generador de reglas.

![El bloque Audiencia está resaltado, así como el botón Generar regla.](/help/segmentation/images/ui/composition-enhancements/select-build-rule.png)

Aparecerá el lienzo del generador de reglas. Ahora puede crear criterios de filtro para el enriquecimiento de audiencia. Los criterios de filtro **debe** incluir un atributo que se encuentre dentro de una matriz. El atributo que es una matriz depende de la estructura de esquema de su organización. Después de crear los criterios de filtro, seleccione **[!UICONTROL Delivery]** en el panel derecho.

![El lienzo del generador de reglas muestra un ejemplo de una audiencia que puede tener enriquecimientos. El botón Entrega también está resaltado.](/help/segmentation/images/ui/composition-enhancements/view-delivery.png)

Elija la matriz de objetos que desee utilizar para el enriquecimiento en la lista del panel izquierdo. Si solo hay una matriz en el perfil, la matriz se selecciona automáticamente. Seleccione **[!UICONTROL Save]** para volver a la composición de audiencias.

<!-- , as well as the fields you want to be used in the enrichment. -->

![Se muestra el árbol de esquema para el árbol de enriquecimiento.](/help/segmentation/images/ui/composition-enhancements/view-schema-tree.png)

Dentro de la composición de audiencias, el bloque [!UICONTROL Audience] es ahora de tipo &quot;[!UICONTROL Rule builder with enhancement]&quot;. Seleccione **[!UICONTROL Publish]** para activar su audiencia con el siguiente lote diario.

![Se resalta el bloque Audiencia, que muestra que se agrega una audiencia con enriquecimiento.](/help/segmentation/images/ui/composition-enhancements/rule-builder-with-enrichment.png)

### Detalles y protecciones del comportamiento

Tenga en cuenta los siguientes detalles y protecciones al utilizar el enriquecimiento de audiencia:

- Solo puede usar el enriquecimiento de audiencia dentro de audiencias creadas dentro de Composición de audiencia
- El primer bloque utilizado en la composición **debe** ser una audiencia basada en reglas.
- Usted **no puede** utilizar ninguna otra operación dentro de la composición.
- Una vez publicado, **no puede** editar la composición en la audiencia basada en reglas.
   - Usted *puede* copiar la composición en un borrador y editar el borrador si desea realizar cambios en la composición base o en la audiencia basada en reglas.
- Solo se puede usar la matriz de objetos **one** para generar la carga útil de enriquecimiento en una sola audiencia
   - La matriz de carga útil se puede anidar dentro de un objeto (hasta siete capas dentro del esquema de perfil), pero **no se puede** contener en otra matriz.
   - La matriz de carga útil **debe** tener 50 filas o menos.
   - Todas las columnas de salida de la carga **deben** ser de un tipo primitivo.
   - Solo se muestran las primeras **veinte** columnas de la matriz.
- Solo hay **diez** composiciones de audiencia disponibles para usar en este momento

## Activación más rápida {#faster-activation}

Una activación más rápida permite activar la audiencia en un destino descendente inmediatamente después de que se haya evaluado la composición. Como resultado, si el destino está configurado para activarse después de la evaluación de segmentos, ya no necesita esperar 24 horas para que finalice el trabajo de evaluación.

Para obtener más información, lea la guía [activar audiencias en destinos de perfil por lotes](/help/destinations/ui/activate-batch-profile-destinations.md#export-full-files).
