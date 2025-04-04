---
keywords: Experience Platform;inicio;temas populares;asignar csv;asignar archivo csv;asignar archivo csv a xdm;asignar csv a xdm;guía de iu;asignador;asignación;preparación de datos;preparación de datos;
solution: Experience Platform
title: Resumen de preparación de datos
description: Este documento presenta la preparación de datos en Adobe Experience Platform.
exl-id: f15eeb50-a531-4560-a524-1a670fbda706
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '790'
ht-degree: 0%

---


# Resumen de preparación de datos

La preparación de datos permite a los ingenieros de datos asignar, transformar y validar datos desde y hacia el modelo de datos de experiencia (XDM). La preparación de datos aparece como un paso de &quot;mapa&quot; en los procesos de ingesta de datos, incluido el flujo de trabajo de ingesta de CSV. Los ingenieros de datos pueden utilizar la preparación de datos para realizar la siguiente manipulación de datos durante la ingesta:

- Defina asignaciones de paso a través simples para asignar atributos de entrada a atributos XDM
- Cree campos calculados para realizar cálculos en fila que se puedan asignar a atributos XDM
- Transformar los datos mediante la aplicación de funciones de manipulación de cadenas, números o fechas
- Creación de jerarquías XDM mediante funciones jerárquicas
- Vista previa de los datos mientras se manipulan en la preparación de datos

La preparación de datos también aplica varias validaciones de datos intrínsecas para garantizar que la integridad de los datos se mantenga a medida que se incorpora. Cuando sea posible, la preparación de datos asignará automáticamente los esquemas de datos entrantes a XDM. Los ingenieros de datos pueden cambiar, corregir y eliminar las asignaciones sugeridas y reemplazarlas con las asignaciones según corresponda.

>[!NOTE]
>
>A menos que el mensaje resultante sea un XDM no válido, cualquier error de transformación en la preparación de datos hará que esos atributos se establezcan en `null`, mientras que el resto de la fila se ingestará. Si la fila se resuelve en un XDM no válido, se ingestará **no**. En ambos casos, el error se documenta.

## Asignación

Una asignación es una asociación de un atributo de entrada o campo calculado a un atributo XDM. Un solo atributo se puede asignar a varios atributos XDM creando asignaciones individuales.

Para obtener más información acerca de las diferentes funciones de asignación, lea la [guía de funciones de asignación](./functions.md).

### Campos calculados

Los campos calculados permiten crear valores basados en los atributos del esquema de entrada. Estos valores se pueden asignar a atributos en el esquema de destino y se les puede proporcionar un nombre y una descripción para facilitar la referencia. Los campos calculados tienen una longitud máxima de 4096 caracteres.

Para obtener más información sobre los campos calculados, lea la [guía de campos calculados](./functions.md#calculated-fields).

### Escapar de caracteres especiales {#escape-special-characters}

Puede aplicar secuencias de escape a los caracteres especiales de un campo usando `${...}`. Sin embargo, este mecanismo no admite archivos JSON que contengan campos con un punto (`.`). Al interactuar con jerarquías, si un atributo secundario tiene un punto (`.`), debe utilizar una barra invertida (`\`) para omitir los caracteres especiales. Por ejemplo, `address` es un objeto que contiene el atributo `street.name`, entonces se puede hacer referencia a este como `address.street\.name` en lugar de `address.street.name`.

## Conjunto de asignaciones

Un conjunto de asignaciones que transforman un esquema en otro se conocen colectivamente como un conjunto de asignaciones. Se crea un único conjunto de asignaciones como parte de cada flujo de datos. Un conjunto de asignaciones es una parte integral de los flujos de datos y se crea, edita y supervisa como parte de los flujos de datos.

Para obtener más información sobre los conjuntos de asignaciones, incluido cómo usar los campos de un conjunto de asignaciones, lea la [guía del conjunto de asignaciones](./mapping-set.md). Para obtener información sobre cómo crear un conjunto de asignaciones y utilizar otras llamadas de API relacionadas con conjuntos de asignaciones, lea la sección conjunto de asignaciones en la [guía para desarrolladores](./api/mapping-set.md).

## Administración del formato de datos

La preparación de datos puede gestionar de forma fiable diferentes formatos de datos introducidos en Experience Platform. Para obtener más información sobre cómo la preparación de datos administra diferentes tipos de datos, lea la [descripción general de la administración del formato de datos](./data-handling.md).

## Enviar actualizaciones parciales de fila utilizando [!DNL Data Prep]

La transmisión de actualizaciones en [!DNL Data Prep] le permite enviar actualizaciones parciales de fila a los datos de [!DNL Profile Service], al mismo tiempo que crea y establece nuevos vínculos de identidad con una sola solicitud de API. Para obtener más información sobre cómo transmitir actualizaciones en [!DNL Data Prep], consulte el documento sobre [envío de actualizaciones parciales de fila](./upserts.md).

## Control de acceso basado en atributos en [!DNL Data Prep]

El control de acceso basado en atributos en Adobe Experience Platform permite a los administradores controlar el acceso a objetos específicos o funcionalidades basadas en atributos.

El control de acceso basado en atributos garantiza que sólo puede asignar los atributos a los que tiene acceso. Los atributos a los que no tiene acceso no se pueden utilizar en asignaciones de paso a través y campos calculados. De este modo, si no tiene acceso a un campo obligatorio, no podrá guardar correctamente una asignación. Además, no se pueden asignar objetos ni matrices de objetos si no se tiene acceso a ninguno de los atributos secundarios. Sin embargo, puede asignar otros elementos dentro del objeto o de la matriz de objetos individualmente.

Consulte la [descripción general del control de acceso basado en atributos](../access-control/abac/overview.md) para obtener más información.

## Pasos siguientes

Este documento abarcaba los conceptos básicos de la preparación de datos en Adobe Experience Platform. Para obtener más información acerca de las diferentes funciones de asignación, lea la [guía de funciones de asignación](./functions.md). Para obtener más información sobre cómo la preparación de datos administra diferentes tipos de datos, lea la [guía de administración de formato de datos](./data-handling.md#dates). Para aprender a usar la API de preparación de datos, lea la [Guía para desarrolladores de preparación de datos](api/overview.md).
