---
keywords: Experience Platform;inicio;temas populares;asignar csv;asignar archivo csv;asignar archivo csv a xdm;asignar csv a xdm;guía ui;mapper;asignación;preparación de datos;preparación de datos;preparar datos;
solution: Experience Platform
title: Información general sobre la preparación de datos
topic: overview
description: Este documento presenta la preparación de datos dentro de Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: 37c1c98ccba50fa917acc5e93763294f4dde5c36
workflow-type: tm+mt
source-wordcount: '335'
ht-degree: 0%

---


# Información general sobre la preparación de datos

La preparación de datos permite a los ingenieros de datos asignar, transformar y validar datos desde y hacia el Modelo de datos de experiencia (XDM). La preparación de datos aparece como un paso de &quot;mapa&quot; en los procesos de inserción de datos, incluido el flujo de trabajo de ingestión de CSV. Los ingenieros de datos pueden utilizar la preparación de datos para realizar la siguiente manipulación de datos durante la ingestión:

- Definir asignaciones de paso simples para asignar atributos de entrada a atributos XDM
- Crear campos calculados para realizar cálculos en fila que se pueden asignar a atributos XDM
- Transformar los datos aplicando funciones de manipulación de cadenas, números o fechas
- Construir jerarquías XDM mediante funciones jerárquicas
- Previsualización de los datos tal como se manipulan dentro de la vista previa de datos

La preparación de datos también aplica varias validaciones de datos intrínsecas para garantizar que la integridad de los datos se mantenga durante la ingesta. Siempre que sea posible, la preparación de datos asigna automáticamente los esquemas de datos entrantes a XDM. Los ingenieros de datos pueden cambiar, corregir y eliminar las asignaciones sugeridas y sustituirlas por las asignaciones según corresponda.

## Asignación

Una asignación es una asociación de un atributo de entrada o campo calculado a un atributo XDM. Un solo atributo se puede asignar a varios atributos XDM creando asignaciones individuales.

Para obtener más información sobre las distintas funciones de asignación, lea la guía [funciones de asignación](./functions.md).

## Conjunto de asignaciones

Un conjunto de asignaciones que transforman un esquema a otro se conoce colectivamente como conjunto de asignaciones. Se crea un único conjunto de asignaciones como parte de cada flujo de datos. Un conjunto de asignaciones es una parte integral de los flujos de datos y se crea, edita y monitorea como parte de los flujos de datos.

## Pasos siguientes

Este documento abarcaba los conceptos básicos de la preparación de datos en Adobe Experience Platform. Para obtener más información sobre las distintas funciones de asignación, lea la guía [funciones de asignación](./functions.md). Para obtener más información sobre las diferentes cadenas de fecha y hora, lea la [guía de cadenas de fecha](./dates.md).