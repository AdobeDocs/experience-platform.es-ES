---
keywords: Experience Platform;inicio;temas populares;asignación de csv;asignación de archivo csv;asignación de archivo csv a xdm;asignación de csv a xdm;guía de ui;asignador;asignación;preparación de datos;preparación de datos;preparación de datos;
solution: Experience Platform
title: Información general sobre la preparación de datos
topic-legacy: overview
description: Este documento presenta la preparación de datos dentro de Adobe Experience Platform.
exl-id: f15eeb50-a531-4560-a524-1a670fbda706
source-git-commit: 61603d7516dbd859b0cce6c167c75aab42ca7171
workflow-type: tm+mt
source-wordcount: '788'
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

>[!NOTE]
>
>A menos que el mensaje resultante sea XDM no válido, cualquier error de transformación en la preparación de datos dará como resultado que esos atributos se establezcan en `null`, mientras que el resto de la fila se incorporará. Si la fila no se resuelve en un XDM no válido, la fila **not** ingeridos. En ambos casos, el error se documenta.

## Asignación

Una asignación es una asociación de un atributo de entrada o campo calculado a un atributo XDM. Un único atributo se puede asignar a varios atributos XDM creando asignaciones individuales.

Para obtener más información sobre las diferentes funciones de asignación, lea la [guía de funciones de asignación](./functions.md).

### Campos calculados

Los campos calculados permiten que se creen valores en función de los atributos del esquema de entrada. Estos valores se pueden asignar a atributos en el esquema de destino y se les puede proporcionar un nombre y una descripción para facilitar la referencia. Los campos calculados tienen una longitud máxima de 4096 caracteres.

Para obtener más información sobre los campos calculados, lea la [guía de campos calculados](./functions.md#calculated-fields).

### Omisión de caracteres especiales {#escape-special-characters}

Puede omitir los caracteres especiales de un campo utilizando `${...}`. Sin embargo, los archivos JSON que contienen campos con un punto (`.`) no son compatibles con este mecanismo. Cuando interactúa con jerarquías, si un atributo secundario tiene un punto (`.`), debe utilizar una barra invertida (`\`) para omitir caracteres especiales. Por ejemplo, `address` es un objeto que contiene el atributo `street.name`, esto puede denominarse `address.street\.name` en lugar de `address.street.name`.

## Conjunto de asignaciones

Un conjunto de asignaciones que transforman un esquema en otro se conocen colectivamente como conjunto de asignaciones. Se crea un conjunto de asignaciones único como parte de cada flujo de datos. Un conjunto de asignaciones es una parte integral de los flujos de datos y se crea, edita y monitoriza como parte de los flujos de datos.

Para obtener más información sobre los conjuntos de asignaciones, incluido cómo utilizar los campos dentro de un conjunto de asignaciones, lea la [guía de conjunto de asignaciones](./mapping-set.md). Para aprender a crear un conjunto de asignaciones y utilizar otras llamadas de API relacionadas con conjuntos de asignaciones, lea la sección del conjunto de asignaciones en la [guía para desarrolladores](./api/mapping-set.md).

## Gestión del formato de datos

La preparación de datos puede gestionar de forma sólida diferentes formatos de datos introducidos en Platform. Para obtener más información sobre cómo gestiona la preparación de datos los distintos tipos de datos, lea la [información general sobre la gestión del formato de datos](./data-handling.md).

## Enviar actualizaciones de filas parciales mediante [!DNL Data Prep]

Transmisión de fuentes en [!DNL Data Prep] permite enviar actualizaciones de fila parciales a [!DNL Profile Service] al mismo tiempo que crea y establece nuevos vínculos de identidad con una única solicitud de API. Para obtener más información sobre cómo retransmitir subidas en [!DNL Data Prep], consulte el documento en [envío de actualizaciones de fila parciales](./upserts.md).

## Control de acceso basado en atributos en [!DNL Data Prep]

El control de acceso basado en atributos en Adobe Experience Platform permite a los administradores controlar el acceso a objetos y/o funciones específicos según los atributos.

El control de acceso basado en atributos garantiza que solo puede asignar los atributos a los que tiene acceso. Los atributos a los que no tiene acceso no se pueden usar en asignaciones de paso y campos calculados. Por lo tanto, si no tiene acceso a un campo obligatorio, no puede guardar correctamente una asignación. Además, no puede asignar objetos ni matrices de objetos si no tiene acceso a ninguno de los atributos secundarios. Sin embargo, puede asignar otros elementos dentro de la matriz de objetos u objetos individualmente.

Consulte la [información general sobre el control de acceso basado en atributos](../access-control/abac/overview.md) para obtener más información.

## Pasos siguientes

Este documento abarcaba los conceptos básicos de la preparación de datos en Adobe Experience Platform. Para obtener más información sobre las diferentes funciones de asignación, lea la [guía de funciones de asignación](./functions.md). Para obtener más información sobre cómo gestiona la preparación de datos los distintos tipos de datos, lea la [guía de gestión del formato de datos](./data-handling.md#dates). Para aprender a utilizar la API de preparación de datos, lea la [Guía para desarrolladores de preparación de datos](api/overview.md).
