---
title: Eliminación de recursos de una biblioteca
description: Obtenga información sobre cómo eliminar recursos de una biblioteca de etiquetas.
source-git-commit: 7e27735697882065566ebdeccc36998ec368e404
workflow-type: tm+mt
source-wordcount: '314'
ht-degree: 87%

---

# Eliminación de recursos de una biblioteca

>[!NOTE]
>
>Adobe Experience Platform Launch se ha convertido en un conjunto de tecnologías de recopilación de datos en Adobe Experience Platform. Como resultado, se han implementado varios cambios terminológicos en la documentación del producto. Consulte el siguiente [documento](../../term-updates.md) para obtener una referencia consolidada de los cambios terminológicos.

Cuando ya no desee que un recurso afecte a una compilación, debe eliminarlo de la biblioteca que contiene ese recurso y crear una nueva compilación.

>[!IMPORTANT]
>
>Los recursos de las bibliotecas son interdependientes. La eliminación de un recurso de una compilación puede cambiar el comportamiento de otros recursos dentro de la compilación.

El proceso de eliminación funciona de un modo ligeramente distinto según el estado de la biblioteca.

## Bibliotecas de desarrollo

Los recursos de bibliotecas de desarrollo pueden manipularse directamente.

1. Abra la biblioteca.
1. Elimine el recurso.
1. Guarde la biblioteca.
1. Compile la biblioteca.

## Bibliotecas enviadas y aprobadas

Los recursos que se encuentran en bibliotecas enviadas o aprobadas no pueden manipularse directamente. Debe volver a llevar la biblioteca al estado de desarrollo.

1. Rechace la biblioteca (mueve la biblioteca a desarrollo).
1. Siga los pasos de “Bibliotecas de desarrollo”, más arriba, para eliminar recursos de las bibliotecas de desarrollo.

## Bibliotecas de producción

La eliminación de recursos de una biblioteca de producción es el caso más complejo. No puede manipular los recursos de la biblioteca en este estado y tampoco puede volver a mover estas bibliotecas al estado de desarrollo.

En su lugar, debe deshabilitar el recurso. Esta deshabilitación es un cambio que se añade a una biblioteca de desarrollo como cualquier otro cambio. Una vez que este cambio se introduce en Producción, el recurso se mueve de la biblioteca de producción.

1. Deshabilite el recurso.
   1. Seleccione el recurso en la vista de lista.
   1. Seleccione **[!UICONTROL Deshabilitar]**.
1. Cree una nueva biblioteca de desarrollo.
1. Añada la versión `latest` del recurso deshabilitado.
1. Guárdelo y compílelo.
1. Siga el proceso normal de traslado de bibliotecas a producción.
1. Publique en producción para eliminar el recurso.
