---
title: Notas
description: Obtenga información sobre cómo añadir anotaciones de texto a determinados recursos de etiquetas en Adobe Experience Platform.
exl-id: 14d6b6a1-3bd0-4181-8181-e6b35c197a44
source-git-commit: 44e2b8241a8c348d155df3061d398c4fa43adcea
workflow-type: tm+mt
source-wordcount: '262'
ht-degree: 99%

---

# Notas

Las notas son anotaciones de texto que se pueden añadir a determinados recursos de etiquetas en Adobe Experience Platform. Las notas se pueden adjuntar a los siguientes recursos:

* Extensiones
* Elementos de datos
* Reglas
* Componentes de regla
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

Seleccione **[!UICONTROL Notes]** para expandir el carril derecho y mostrar las notas, con las notas más recientes en la parte superior.  Para añadir una nota nueva, escriba el texto de la nota en el cuadro de la parte superior y seleccione **[!UICONTROL Add Note]**.

## Otras

* Las notas en los recursos de etiquetas se comportan de la misma manera que las notas en DTM, ya que son inmutables y no se pueden editar ni eliminar.
* Al examinar las revisiones anteriores de un recurso, solo se muestran las notas que se crearon antes de la fecha de `created_at` de esa revisión.
* Al eliminar un recurso, también se eliminan todas las notas adjuntas al recurso.
