---
title: Eliminación de recursos de una biblioteca
description: Obtenga información sobre cómo quitar recursos de una biblioteca de etiquetas.
exl-id: ad1dd093-962c-4f6d-85eb-c5ed1b644927
source-git-commit: 44e2b8241a8c348d155df3061d398c4fa43adcea
workflow-type: tm+mt
source-wordcount: '268'
ht-degree: 100%

---

# Eliminación de recursos de una biblioteca

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
   1. Seleccione **[!UICONTROL Disable]**.
1. Cree una nueva biblioteca de desarrollo.
1. Añada la versión `latest` del recurso deshabilitado.
1. Guárdelo y compílelo.
1. Siga el proceso normal de traslado de bibliotecas a producción.
1. Publique en producción para eliminar el recurso.
