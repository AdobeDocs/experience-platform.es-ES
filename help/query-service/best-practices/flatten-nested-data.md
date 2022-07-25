---
keywords: Experience Platform;servicio de consulta;servicio de consulta;estructuras de datos anidadas;datos anidados;acoplar;datos anidados acoplados;
title: Acoplar Estructuras De Datos Anidadas Para Utilizarlas Con Herramientas De BI
description: En este documento se explica cómo acoplar esquemas XDM para todas las tablas y vistas durante una sesión al utilizar herramientas BI de terceros con servicio de consulta.
exl-id: 7e534c0a-db6c-463e-85da-88d7b2534ece
source-git-commit: a7f273383293359cf6adbcc0a508fb19d2789339
workflow-type: tm+mt
source-wordcount: '865'
ht-degree: 1%

---

# Acoplar estructuras de datos anidadas para usarlas con herramientas de BI de terceros

El servicio de consulta de Adobe Experience Platform es compatible con `FLATTEN` al conectarse a una base de datos mediante herramientas de BI de terceros. Esta función aplana las estructuras de datos anidadas en las herramientas de BI de terceros para mejorar su uso y reducir la carga de trabajo necesaria para recuperar, analizar, transformar y crear informes de datos.

Muchas herramientas de BI como [!DNL Tableau] y [!DNL Power BI] no admiten de forma nativa estructuras de datos anidadas. La variable `FLATTEN` elimina la necesidad de crear vistas SQL sobre los datos para proporcionar una versión plana o utilizar el servicio de consultas `CTAS` o `INSERT INTO` trabajos para duplicar los conjuntos de datos en versiones planas al usar esquemas ad hoc.

La variable `FLATTEN` rellena la estructura de cada campo de hoja en la raíz de la tabla y asigna un nombre al campo después del área de nombres original. Esto le permite utilizar la notación de puntos para hacer coincidir un campo con su ruta del Modelo de datos de experiencia (XDM) preservando al mismo tiempo el contexto del campo.

## Requisitos previos

Al usar la variable `FLATTEN` requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [Sistema XDM](../../xdm/home.md): Información general de alto nivel sobre XDM y su implementación en Experience Platform.

   * [Crear un esquema ad hoc](../../xdm/tutorials/ad-hoc.md): Un esquema XDM con campos a los que se asigna un nombre para su uso solamente mediante un conjunto de datos único, se denomina esquema ad hoc. Los esquemas específicos se utilizan en varios flujos de trabajo de consumo de datos para el Experience Platform y la creación de determinados tipos de conexiones de origen.

* [Sandboxes](../../sandboxes/home.md): Experience Platform proporciona entornos limitados virtuales que dividen una sola instancia de Platform en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

* [Estructuras de datos anidadas](./nested-data-structures.md): Este documento proporciona ejemplos de cómo crear, procesar o transformar conjuntos de datos con tipos de datos complejos, incluidas estructuras de datos anidadas.

## Conectarse a una base de datos mediante la configuración FLATTEN {#connect-with-flatten}

La variable `FLATTEN` esta configuración aplana las estructuras de datos anidadas en columnas independientes, donde el nombre del atributo se convierte en el nombre de columna que contiene los valores de fila. Al trabajar con datos en herramientas de BI que no admiten estructuras de datos anidadas, esta configuración mejora la capacidad de uso de esquemas ad hoc y reduce la carga de trabajo necesaria.

Al conectarse al servicio de consulta con el cliente de terceros elegido, añada la variable `FLATTEN` estableciendo en el nombre de la base de datos. Para obtener información sobre cómo conectar una herramienta BI específica, consulte su documentación correspondiente en la [información general sobre la conexión de clientes a Query Service](../clients/overview.md). La cadena de conexión debe contener:

* El nombre del simulador de pruebas.
* Dos puntos seguidos de `all` o un ID de conjunto de datos, ID de vista o nombre de base de datos específico.
* Un signo de interrogación (?) seguido de `FLATTEN` palabra clave.

La entrada debe tener el siguiente formato:

```terminal
{sandbox_name}:{all/ID/database_name}?FLATTEN
```

Una cadena de conexión de ejemplo puede tener el siguiente aspecto:

```terminal
prod:all?FLATTEN
```

## Ejemplo {#example}

El esquema de ejemplo utilizado en esta guía emplea el grupo de campos estándar [!UICONTROL Detalles del comercio], que utiliza el `commerce` estructura de objetos y `productListItems` matriz. Consulte la documentación de XDM para [más información sobre [!UICONTROL Detalles del comercio] grupo de campos](../../xdm/field-groups/event/commerce-details.md). En la imagen siguiente se puede ver una representación de la estructura del esquema.

![Un diagrama de esquema del grupo de campos Detalles del comercio que incluye la variable `commerce` y `productListItems` estructuras.](../images/best-practices/flatten-nested-data/commerce-details.png)

Si la herramienta BI no admite estructuras de datos anidadas, puede resultar difícil hacer referencia a campos anidados si contienen valores serializados (como `commerce` y `productListItems` en el esquema de ejemplo). Estos valores pueden aparecer como partes de una sola codificación `commerce` y no son realistas y no se pueden utilizar.

Los siguientes valores representan `commerce.order.priceTotal` (3018.0), `commerce.order.purchaseID` (c9b5aff9-25de-450b-98f4-4484a2170180), y `commerce.purchases.value`(1.0) en campos anidados con un formato incorrecto.

```terminal
("(3018.0,c9b5aff9-25de-450b-98f4-4484a2170180)","(1.0)")
```

Usando la variable `FLATTEN` , puede acceder a campos independientes dentro del esquema o secciones completas de la estructura de datos anidada mediante notación de puntos y su nombre de ruta original. Un ejemplo de este formato con la variable `commerce` a continuación se muestra el grupo de campos.

```terminal
commerce.order.priceTotal
commerce.order.purchaseID
commerce.purchases.value
```

La variable `FLATTEN` tiene ciertas limitaciones al tratar con otras estructuras de datos. Los detalles completos se proporcionan en la [sección de limitaciones](#limitations).

### Usar comillas para campos en consultas {#quotation-marks}

Los campos raíz acoplados ahora utilizan la notación de puntos para coincidir con sus rutas XDM. Cuando se utiliza en una consulta, los campos deben estar entre comillas (&quot; &quot;).

El ejemplo SQL siguiente muestra el estado original de la consulta anidada:

```sql
SELECT YEAR(timestamp) AS year,
       SUM(commerce.order.priceTotal) AS revenue
FROM purchase_events_dataset
WHERE commerce.purchases.value > 0
GROUP BY 1;
```

Al utilizar los campos de datos acoplados, la consulta se escribe con notación de puntos y entre comillas, como se ve a continuación:

```sql
SELECT YEAR(timestamp) AS year,
       SUM("commerce.order.priceTotal") AS revenue
FROM purchase_events_dataset
WHERE "commerce.purchases.value" > 0
GROUP BY 1;
```

## Limitaciones {#limitations}

La variable `FLATTEN` no aplana actualmente las siguientes estructuras de datos:

| Estructura de datos | Limitación |
|---|---|
| Matrices | Utilice un índice de matriz explícito o la variable `EXPLODE` para acceder a las matrices. |
| Mapas | Utilice la clave de cadena para acceder a un valor de un mapa y acceder a los mapas. |

Para resolver las limitaciones de Mapa y Matriz, debe utilizar las herramientas de BI para la edición de SQL sin procesar, como Opciones avanzadas -> Instrucción SQL en Power BI.

Las herramientas de BI, como la edición SQL sin procesar, son necesarias para resolver las limitaciones de las asignaciones y las matrices. Consulte la guía de cómo [utilizar opciones avanzadas de Power BI para introducir una consulta SQL personalizada](https://experienceleague.adobe.com/docs/experience-platform/query/clients/power-bi.html#import-tables-using-custom-sql) en la sección Instrucción SQL.

## Pasos siguientes

Este documento abarcaba cómo aplanar estructuras de datos anidadas para usarlas con herramientas de BI de terceros. Si aún no ha conectado el cliente, consulte [información general sobre la conexión del cliente](../clients/overview.md) para obtener una lista de clientes de terceros admitidos.
