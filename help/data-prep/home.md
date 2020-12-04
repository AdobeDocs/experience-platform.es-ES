---
keywords: Experience Platform;home;popular topics;map csv;map csv file;map csv file to xdm;map csv to xdm;ui guide;mapper;mapping;data prep;data preparation;preparing data;
solution: Experience Platform
title: Funciones de asignación
topic: overview
description: Este documento presenta la preparación de datos dentro de Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: db38f0666f5c945461043ad08939ebda52c21855
workflow-type: tm+mt
source-wordcount: '304'
ht-degree: 1%

---


# Preparación de datos

La preparación de datos permite a los ingenieros de datos asignar, transformar y validar datos desde y hacia el Modelo de datos de experiencia (XDM). La preparación de datos aparece como un paso de &quot;mapa&quot; en los procesos de inserción de datos, incluido el flujo de trabajo de ingestión de CSV. Los ingenieros de datos pueden utilizar la preparación de datos para realizar la siguiente manipulación de datos durante la ingestión:

- Definir asignaciones de paso simples para asignar atributos de entrada a atributos XDM
- Crear campos calculados para realizar cálculos en fila que se pueden asignar a atributos XDM
- Transformar los datos aplicando funciones de manipulación de cadenas, números o fechas
- Construir jerarquías XDM mediante funciones jerárquicas
- Previsualización de los datos tal como se manipulan dentro de la vista previa de datos

La preparación de datos también aplica varias validaciones de datos intrínsecas para garantizar que la integridad de los datos se mantenga durante la ingesta. Siempre que sea posible, la preparación de datos asigna automáticamente los esquemas de datos entrantes a XDM. Los ingenieros de datos pueden cambiar, corregir y eliminar las asignaciones sugeridas y sustituirlas por las asignaciones según corresponda.

## Asignación

Una asignación es una asociación de un atributo de entrada o campo calculado a un atributo XDM. Un solo atributo se puede asignar a varios atributos XDM creando asignaciones individuales.

Para obtener más información sobre las distintas funciones de asignación, lea la guía [de funciones de](./functions.md)asignación.

## Conjunto de asignaciones

Un conjunto de asignaciones que transforman un esquema a otro se conoce colectivamente como conjunto de asignaciones. Se crea un único conjunto de asignaciones como parte de cada flujo de datos. Un conjunto de asignaciones es una parte integral de los flujos de datos y se crea, edita y monitorea como parte de los flujos de datos.

## Pasos siguientes

Este documento abarcaba los conceptos básicos de la preparación de datos en Adobe Experience Platform. Para obtener más información sobre las distintas funciones de asignación, lea la guía [de funciones de](./functions.md)asignación. Para obtener más información sobre las diferentes cadenas de fecha y hora, lea la guía [de cadenas de](./dates.md)fecha.