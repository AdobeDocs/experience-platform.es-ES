---
keywords: Experience Platform;servicio de consultas;servicio de consultas;estructuras de datos anidadas;datos anidados;aplanar;aplanar datos anidados;
title: Acoplar estructuras de datos anidadas para usarlas con herramientas de BI
description: En este documento se explica cómo acoplar esquemas XDM para todas las tablas y vistas durante una sesión al utilizar herramientas de BI de terceros con el servicio de consulta.
exl-id: 7e534c0a-db6c-463e-85da-88d7b2534ece
source-git-commit: 1c590350c9d519dba60375b92de7bbbbd77961dc
workflow-type: tm+mt
source-wordcount: '857'
ht-degree: 1%

---

# Acoplar estructuras de datos anidadas para usarlas con herramientas de BI de terceros

El servicio de consultas de Adobe Experience Platform admite `FLATTEN` configuración al conectarse a una base de datos a través de herramientas de BI de terceros. Esta función aplana las estructuras de datos anidadas en herramientas de BI de terceros para mejorar su facilidad de uso y reducir la carga de trabajo necesaria para recuperar, analizar, transformar y crear informes de datos.

Muchas herramientas de BI como [!DNL Tableau] y [!DNL Power BI] no admiten de forma nativa estructuras de datos anidadas. El `FLATTEN` Esta configuración elimina la necesidad de crear vistas SQL sobre los datos para proporcionar una versión plana o para utilizar el servicio de consulta `CTAS` o `INSERT INTO` trabajos para duplicar los conjuntos de datos en versiones planas al utilizar esquemas ad hoc.

El `FLATTEN` esta configuración extrae la estructura de cada campo hoja en la raíz de la tabla y asigna al campo el nombre del área de nombres original. Esto le permite utilizar la notación de puntos para hacer coincidir un campo con su ruta del Modelo de datos de experiencia (XDM), al mismo tiempo que conserva el contexto del campo.

## Requisitos previos

Uso del `FLATTEN` La configuración de requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [Sistema XDM](../../xdm/home.md): Información general de alto nivel sobre XDM y su implementación en Experience Platform.

   * [Creación de un esquema ad hoc](../../xdm/tutorials/ad-hoc.md): un esquema XDM con campos que están separados por espacios de nombres para que los utilice solo un conjunto de datos, se denomina esquema ad hoc. Los esquemas ad hoc se utilizan en varios flujos de trabajo de ingesta de datos para Experience Platform y para crear ciertos tipos de conexiones de origen.

* [Zonas protegidas](../../sandboxes/home.md): Experience Platform proporciona zonas protegidas virtuales que dividen una sola instancia de Platform en entornos virtuales independientes para ayudar a desarrollar y evolucionar aplicaciones de experiencia digital.

* [Estructuras de datos anidadas](./nested-data-structures.md): este documento proporciona ejemplos de cómo crear, procesar o transformar conjuntos de datos con tipos de datos complejos, incluidas estructuras de datos anidadas.

## Conexión a una base de datos mediante la configuración APLANAR {#connect-with-flatten}

El `FLATTEN` al establecer, se acoplan las estructuras de datos anidadas en columnas independientes, donde el nombre del atributo se convierte en el nombre de columna que contiene los valores de fila. Cuando se trabaja con datos en herramientas de BI que no admiten estructuras de datos anidadas, esta configuración mejora la facilidad de uso de esquemas ad hoc y reduce la carga de trabajo necesaria.

Al conectarse al servicio de consultas con el cliente de terceros elegido, anexe el `FLATTEN` al nombre de la base de datos. Para obtener información sobre cómo conectar una herramienta de BI específica, consulte su documentación correspondiente en la [información general de conexión de clientes al servicio de consultas](../clients/overview.md). La cadena de conexión debe contener:

* Nombre de la zona protegida.
* Dos puntos seguidos de `all` o un ID de conjunto de datos, ID de vista o nombre de base de datos específico.
* Un signo de interrogación (?) seguido del `FLATTEN` palabra clave.

La entrada debe tener el siguiente formato:

```terminal
{sandbox_name}:{all/ID/database_name}?FLATTEN
```

Un ejemplo de cadena de conexión puede tener el siguiente aspecto:

```terminal
prod:all?FLATTEN
```

## Ejemplo {#example}

El esquema de ejemplo utilizado en esta guía emplea el grupo de campos estándar [!UICONTROL Detalles de comercio], que utiliza el `commerce` la estructura del objeto y el `productListItems` matriz. Consulte la documentación de XDM para [más información sobre la [!UICONTROL Detalles de comercio] grupo de campos](../../xdm/field-groups/event/commerce-details.md). En la siguiente imagen se puede ver una representación de la estructura del esquema.

![Un diagrama de esquema del grupo de campos Detalles de comercio que incluye `commerce` y `productListItems` estructuras.](../images/essential-concepts/commerce-details.png)

Si la herramienta BI no admite estructuras de datos anidadas, puede resultar difícil hacer referencia a campos anidados si contienen valores serializados (como `commerce` y `productListItems` en el esquema de ejemplo). Estos valores pueden aparecer como partes de una sola codificación `commerce` Campo de cadena y no son realistas inutilizables.

Los siguientes valores representan `commerce.order.priceTotal` (3018.0), `commerce.order.purchaseID` (c9b5aff9-25de-450b-98f4-4484a2170180), y `commerce.purchases.value`(1.0) en campos anidados con formato incorrecto.

```terminal
("(3018.0,c9b5aff9-25de-450b-98f4-4484a2170180)","(1.0)")
```

Mediante el uso de `FLATTEN` Con esta configuración, puede acceder a campos independientes dentro del esquema o a secciones completas de la estructura de datos anidada mediante la notación de puntos y su nombre de ruta original. Un ejemplo de este formato con la variable `commerce` grupo de campos se indica a continuación.

```terminal
commerce.order.priceTotal
commerce.order.purchaseID
commerce.purchases.value
```

El `FLATTEN` La configuración de tiene ciertas limitaciones al tratar con otras estructuras de datos. Encontrará toda la información en la [sección de limitaciones](#limitations).

### Utilice comillas para los campos de las consultas {#quotation-marks}

Los campos raíz aplanados ahora utilizan la notación de puntos para hacer coincidir sus rutas XDM. Cuando se utilizan en una consulta, los campos deben ir entre comillas (&quot; &quot;).

El ejemplo de SQL siguiente muestra el estado original de la consulta anidada:

```sql
SELECT YEAR(timestamp) AS year,
       SUM(commerce.order.priceTotal) AS revenue
FROM purchase_events_dataset
WHERE commerce.purchases.value > 0
GROUP BY 1;
```

Al utilizar los campos de datos aplanados, la consulta se escribe con notación de puntos y se encierra entre comillas como se muestra a continuación:

```sql
SELECT YEAR(timestamp) AS year,
       SUM("commerce.order.priceTotal") AS revenue
FROM purchase_events_dataset
WHERE "commerce.purchases.value" > 0
GROUP BY 1;
```

## Limitaciones {#limitations}

El `FLATTEN` actualmente, esta configuración no aplana las siguientes estructuras de datos:

| Estructura de datos | Limitation |
|---|---|
| Matrices | Utilice un índice de matriz explícito para `EXPLODE` para acceder a las cabinas. |
| Mapas | Utilice la clave de cadena para acceder a un valor de un mapa y acceder a los mapas. |

Para resolver las limitaciones de Mapa y Matriz, debe utilizar las herramientas de BI para la edición de SQL sin procesar, como las Opciones avanzadas -> Instrucción SQL en Power BI.

Las herramientas de BI como la edición de SQL sin procesar son necesarias para resolver las limitaciones de asignaciones y matrices. Consulte la guía sobre cómo [utilice las opciones avanzadas de Power BI para introducir una consulta SQL personalizada](../clients/power-bi.md#import-tables-using-custom-sql) en la sección instrucción SQL.

## Pasos siguientes

En este documento se explica cómo aplanar las estructuras de datos anidadas para utilizarlas con herramientas de BI de terceros. Si aún no ha conectado a su cliente, consulte [información general sobre la conexión de cliente](../clients/overview.md) para obtener una lista de clientes de terceros admitidos.
