---
title: Eliminación de recursos
description: Obtenga información sobre cómo eliminar recursos en Adobe Experience Platform.
exl-id: c8e26720-1976-48ec-8490-3d4ce587831e
source-git-commit: 8ded2aed32dffa4f0923fedac7baf798e68a9ec9
workflow-type: tm+mt
source-wordcount: '558'
ht-degree: 90%

---

# Eliminación de recursos

>[!NOTE]
>
>Adobe Experience Platform Launch se ha convertido en un conjunto de tecnologías de recopilación de datos en Adobe Experience Platform. Como resultado, se han implementado varios cambios terminológicos en la documentación del producto. Consulte el siguiente [documento](../../term-updates.md) para obtener una referencia consolidada de los cambios terminológicos.

La eliminación de un recurso es la eliminación permanente de ese recurso de Adobe Experience Platform. Si desea eliminar un recurso de una biblioteca de etiquetas específica, pero desea que dicho recurso esté disponible para su uso en otras bibliotecas, consulte la guía de [eliminación de recursos de una biblioteca](remove-resources-from-library.md).

Puede eliminar elementos, reglas, extensiones, hosts, entornos y propiedades de datos. Una vez eliminados, estos recursos no se pueden recuperar.

Los recursos que se añaden a las bibliotecas (elementos de datos, reglas y extensiones) implican consideraciones especiales al eliminarlos.

## Preparación de un recurso para su eliminación

Los recursos existen en diferentes estados y dependen unos de otros. Antes de eliminar un recurso, debe asegurarse de que este está en un estado que permita su eliminación.

La preparación de un recurso para su eliminación consiste en dos pasos básicos:

1. Resolución de dependencias.
1. Eliminación de las bibliotecas.

### Resolución de dependencias

Las reglas, los elementos de datos y las extensiones son interdependientes, por lo que la mayoría de las veces, al eliminar una, se produce un efecto en cascada que implica que debe limpiar más elementos.

#### Reglas

Las reglas dependen de otros recursos (extensiones y elementos de datos), pero no tienen ningún recurso que dependa de ellos. Si elimina una regla, ya no puede utilizarla en una biblioteca o incluso verla, pero no tiene dependencias que limpiar posteriormente.

#### Elementos de datos

Los elementos de datos dependen de las extensiones, pero a diferencia de las reglas, los elementos de datos pueden tener reglas y extensiones que dependan de ellos. La eliminación de un elemento de datos afecta a cualquier regla o extensión que dependa de este elemento de datos.

Una vez eliminado, el elemento de datos ya no devuelve el valor correcto en el tiempo de ejecución. Devuelve una cadena vacía o el nombre del elemento de datos eliminado entre los símbolos “%%” (ejemplo: `%data-element-name%`). Este comportamiento se puede configurar en Configuración de propiedad.

Puede resolver estas dependencias antes o después de eliminar el elemento de datos.

#### Extensiones

Las extensiones proporcionan todos los demás recursos (reglas, componentes de regla y elementos de datos).

Los componentes de regla y los elementos de datos dependen de las extensiones de su comportamiento, pero también para mostrarse en la interfaz de usuario de recopilación de datos. Si elimina la extensión antes de resolver las dependencias, deja de poder ver estos recursos huérfanos. Estos recursos huérfanos aparecen en vistas de lista, pero la interfaz devuelve un error si intenta abrir la vista de detalles.

Por este motivo, debe tener cuidado al eliminar las extensiones y debe resolver las dependencias antes de eliminarlas.

### Eliminar de las bibliotecas

Para poder eliminar un recurso, debe eliminarlo de las bibliotecas que lo contengan. Este proceso es diferente según el estado de la biblioteca.

#### Desarrollo

1. Abra la biblioteca.
1. Elimine el recurso.
1. Guarde la biblioteca.
1. Elimine el recurso.

#### Enviado o aprobado

1. Rechace la biblioteca (la mueve a Desarrollo).
1. Siga los pasos anteriores para eliminar un recurso de una biblioteca de desarrollo.

#### Producción

1. Deshabilite el recurso.
1. Publique el recurso deshabilitado en Producción.
1. Elimine el recurso.

## Elimine un recurso

En la vista de la lista adecuada, seleccione el recurso que desee eliminar y, a continuación, seleccione **[!UICONTROL Eliminar]**.
