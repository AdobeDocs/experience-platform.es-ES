---
title: Notas
description: Aprenda a añadir anotaciones a determinados recursos de etiquetas en Adobe Experience Platform.
source-git-commit: 39d9468e5d512c75c9d540fa5d2bcba4967e2881
workflow-type: tm+mt
source-wordcount: '308'
ht-degree: 78%

---

# Notas

>[!NOTE]
>
>Adobe Experience Platform Launch se está convirtiendo en un conjunto de tecnologías de recopilación de datos en Experience Platform. Como resultado, se han implementado varios cambios terminológicos en la documentación del producto. Consulte el siguiente [documento](../../term-updates.md) para obtener una referencia consolidada de los cambios terminológicos.

Las notas son anotaciones que se pueden agregar a determinados recursos de etiquetas en Adobe Experience Platform. Las notas se pueden adjuntar a los siguientes recursos:

* Extensiones
* Elementos de datos
* Reglas
* Regla componentes
* Bibliotecas
* Propiedades

Las notas pueden contener hasta 512 caracteres Unicode.

Las notas son comentarios que no afectan al comportamiento de los recursos a los que están adjuntos. No se incluyen en las bibliotecas creadas. Puede utilizar las notas para:

* Proporcionar información básica sobre un recurso
* Que funcionen como una lista de tareas pendientes para futuras mejoras
* Pasar consejos de uso del recursos a otros usuarios
* Dar instrucciones a otros integrantes del equipo
* Registrar el contexto histórico
* Recordar lo que hace un recurso, por qué está creado de esa forma o dónde se utiliza

## Crear una nota

Los recursos a los que se puede adjuntar notas muestran un carril estrecho en el lado derecho de la pantalla. Este carril incluye un icono para las notas. Este icono muestra el número actual de notas adjuntas al recurso.

Seleccione **[!UICONTROL Notas]** para expandir el carril derecho y mostrar las notas, con las notas más recientes en la parte superior. Para añadir una nota nueva, escriba el texto de la nota en el cuadro de la parte superior y seleccione **[!UICONTROL Añadir nota]**.

## Otras

* Las notas sobre los recursos de etiquetas coinciden con el comportamiento de las notas en la DTM, ya que son inmutables y no se pueden editar ni eliminar.
* Al examinar las revisiones anteriores de un recurso, solo se muestran las notas que se crearon antes de la fecha de `created_at` de esa revisión.
* Al eliminar un recurso, también se eliminan todas las notas adjuntas al recurso.
