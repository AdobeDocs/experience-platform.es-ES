---
keywords: Experience Platform;inicio;temas populares;asignación de csv;asignación de archivo csv;asignación de archivo csv a xdm;asignación de csv a xdm;guía de ui;asignador;asignación;preparación de datos;preparación de datos;preparación de datos;
solution: Experience Platform
title: Información general sobre la preparación de datos
topic-legacy: overview
description: Este documento presenta la preparación de datos dentro de Adobe Experience Platform.
exl-id: f15eeb50-a531-4560-a524-1a670fbda706
translation-type: tm+mt
source-git-commit: daefd977cd09bd9cd7f8d6101b45be98f30d24ae
workflow-type: tm+mt
source-wordcount: '437'
ht-degree: 0%

---


# Resumen de la preparación de datos

La preparación de datos permite a los ingenieros de datos asignar, transformar y validar datos desde y hacia el Modelo de datos de experiencia (XDM). La preparación de datos aparece como un paso de &quot;mapa&quot; en los procesos de ingesta de datos, incluido el flujo de trabajo de ingesta de CSV. Los ingenieros de datos pueden utilizar la preparación de datos para realizar la siguiente manipulación de datos durante la ingesta:

- Defina asignaciones de paso simples para asignar atributos de entrada a atributos XDM
- Crear campos calculados para realizar cálculos en fila que se puedan asignar a atributos XDM
- Transformar los datos aplicando funciones de manipulación de cadenas, números o fechas
- Construir jerarquías XDM utilizando funciones jerárquicas
- Obtener una vista previa de los datos tal y como están manipulados en la preparación de datos

La preparación de datos también aplica varias validaciones de datos intrínsecas para garantizar que la integridad de los datos se mantenga a medida que se incorporan. Siempre que sea posible, Data Prep asigna automáticamente los esquemas de datos entrantes a XDM. Los ingenieros de datos pueden cambiar, corregir y eliminar las asignaciones sugeridas y sustituirlas por las asignaciones según corresponda.

## Asignación

Una asignación es una asociación de un atributo de entrada o campo calculado a un atributo XDM. Un único atributo se puede asignar a varios atributos XDM creando asignaciones individuales.

Para obtener más información sobre las diferentes funciones de asignación, lea la [guía de funciones de asignación](./functions.md).

## Conjunto de asignaciones

Un conjunto de asignaciones que transforman un esquema en otro se conocen colectivamente como conjunto de asignaciones. Se crea un conjunto de asignaciones único como parte de cada flujo de datos. Un conjunto de asignaciones es una parte integral de los flujos de datos y se crea, edita y monitoriza como parte de los flujos de datos.

Para obtener más información sobre los conjuntos de asignaciones, incluido cómo utilizar los campos dentro de un conjunto de asignaciones, lea la [guía del conjunto de asignaciones](./mapping-set.md). Para aprender a crear un conjunto de asignaciones y utilizar otras llamadas de API relacionadas con conjuntos de asignaciones, lea la sección del conjunto de asignaciones en la [guía para desarrolladores](./api/mapping-set.md).

## Gestión del formato de datos

La preparación de datos puede gestionar de forma sólida diferentes formatos de datos introducidos en Platform. Para obtener más información sobre cómo gestiona la preparación de datos los distintos tipos de datos, lea la [información general sobre la administración del formato de datos](./data-handling.md).

## Pasos siguientes

Este documento abarcaba los conceptos básicos de la preparación de datos en Adobe Experience Platform. Para obtener más información sobre las diferentes funciones de asignación, lea la [guía de funciones de asignación](./functions.md). Para obtener más información sobre cómo gestiona la preparación de datos los distintos tipos de datos, consulte la [guía de administración del formato de datos](./data-handling.md#dates). Para aprender a utilizar la API de preparación de datos, lea la [Guía para desarrolladores de preparación de datos](api/overview.md).
