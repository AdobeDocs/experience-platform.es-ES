---
keywords: Experience Platform;servicio de consultas;servicio de consultas;estructuras de datos anidadas;datos anidados;aplanar;aplanar datos anidados;
title: Acoplar estructuras de datos anidadas para usarlas con herramientas de BI
description: En este documento se explica cómo acoplar esquemas XDM para todas las tablas y vistas durante una sesión al utilizar herramientas de BI de terceros con el servicio de consulta.
exl-id: 7e534c0a-db6c-463e-85da-88d7b2534ece
source-git-commit: 5f2b44c364183b7becf69f491b41e9d5558accc2
workflow-type: tm+mt
source-wordcount: '857'
ht-degree: 0%

---

# Acoplar estructuras de datos anidadas para usarlas con herramientas de BI de terceros

El servicio de consultas de Adobe Experience Platform admite la configuración `FLATTEN` al conectarse a una base de datos mediante herramientas de BI de terceros. Esta función aplana las estructuras de datos anidadas en herramientas de BI de terceros para mejorar su facilidad de uso y reducir la carga de trabajo necesaria para recuperar, analizar, transformar y crear informes de datos.

Muchas herramientas de BI como [!DNL Tableau] y [!DNL Power BI] no admiten de forma nativa estructuras de datos anidadas. La configuración `FLATTEN` elimina la necesidad de crear vistas SQL sobre los datos para proporcionar una versión plana o de usar los trabajos del servicio de consultas `CTAS` o `INSERT INTO` para duplicar los conjuntos de datos en versiones planas al utilizar esquemas ad hoc.

La configuración `FLATTEN` extrae la estructura de cada campo de hoja en la raíz de la tabla y asigna un nombre al campo después del área de nombres original. Esto le permite utilizar la notación de puntos para hacer coincidir un campo con su ruta del Modelo de datos de experiencia (XDM), al mismo tiempo que conserva el contexto del campo.

## Requisitos previos

El uso de la configuración `FLATTEN` requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [Sistema XDM](../../xdm/home.md): Información general de alto nivel sobre XDM y su implementación en Experience Platform.

   * [Crear un esquema ad hoc](../../xdm/tutorials/ad-hoc.md): Un esquema XDM con campos que tienen un espacio de nombres para que lo utilice solo un único conjunto de datos se denomina esquema ad hoc. Los esquemas ad hoc se utilizan en varios flujos de trabajo de ingesta de datos para Experience Platform y para crear ciertos tipos de conexiones de origen.

* [Zonas protegidas](../../sandboxes/home.md): El Experience Platform proporciona zonas protegidas virtuales que dividen una sola instancia de Platform en entornos virtuales independientes para ayudar a desarrollar y evolucionar aplicaciones de experiencia digital.

* [Estructuras de datos anidadas](./nested-data-structures.md): este documento proporciona ejemplos de cómo crear, procesar o transformar conjuntos de datos con tipos de datos complejos, incluidas estructuras de datos anidadas.

## Conexión a una base de datos mediante la configuración APLANAR {#connect-with-flatten}

La configuración `FLATTEN` aplana las estructuras de datos anidadas en columnas independientes, donde el nombre del atributo se convierte en el nombre de columna que contiene los valores de fila. Cuando se trabaja con datos en herramientas de BI que no admiten estructuras de datos anidadas, esta configuración mejora la facilidad de uso de esquemas ad hoc y reduce la carga de trabajo necesaria.

Al conectarse al servicio de consultas con el cliente de terceros elegido, anexe la configuración `FLATTEN` al nombre de la base de datos. Para obtener información sobre cómo conectar una herramienta de BI específica, consulte su documentación correspondiente en la [descripción general de conexión de clientes al servicio de consultas](../clients/overview.md). La cadena de conexión debe contener:

* Nombre de la zona protegida.
* Dos puntos seguidos de `all` o un ID de conjunto de datos, ID de vista o nombre de base de datos específico.
* Un signo de interrogación (?) seguido de la palabra clave `FLATTEN`.

La entrada debe tener el siguiente formato:

```terminal
{sandbox_name}:{all/ID/database_name}?FLATTEN
```

Un ejemplo de cadena de conexión puede tener el siguiente aspecto:

```terminal
prod:all?FLATTEN
```

## Ejemplo {#example}

El esquema de ejemplo utilizado en esta guía emplea el grupo de campos estándar [!UICONTROL Commerce Details], que utiliza la estructura de objetos `commerce` y la matriz `productListItems`. Consulte la documentación de XDM para obtener [más información sobre el grupo de campos [!UICONTROL Detalles de Commerce]](../../xdm/field-groups/event/commerce-details.md). En la siguiente imagen se puede ver una representación de la estructura del esquema.

![Un diagrama de esquema del grupo de campos Detalles de Commerce que incluye las estructuras `commerce` y `productListItems`.](../images/key-concepts/commerce-details.png)

Si la herramienta de BI no admite estructuras de datos anidadas, puede resultar difícil hacer referencia a campos anidados si contienen valores serializados (como `commerce` y `productListItems` en el esquema de ejemplo). Estos valores pueden aparecer como partes de un único campo de cadena `commerce` codificado y no pueden utilizarse de forma realista.

Los siguientes valores representan `commerce.order.priceTotal` (3018.0), `commerce.order.purchaseID` (c9b5aff9-25de-450b-98f4-4484a2170180) y `commerce.purchases.value`(1.0) en campos anidados con formato incorrecto.

```terminal
("(3018.0,c9b5aff9-25de-450b-98f4-4484a2170180)","(1.0)")
```

Si usa la configuración `FLATTEN`, puede tener acceso a campos independientes dentro del esquema o a secciones completas de la estructura de datos anidada mediante la notación de puntos y su nombre de ruta original. A continuación se muestra un ejemplo de este formato utilizando el grupo de campos `commerce`.

```terminal
commerce.order.priceTotal
commerce.order.purchaseID
commerce.purchases.value
```

La configuración `FLATTEN` tiene ciertas limitaciones cuando se trata de otras estructuras de datos. Se proporcionan detalles completos en la [sección de limitaciones](#limitations).

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

La configuración `FLATTEN` actualmente no aplana las siguientes estructuras de datos:

| Estructura de datos | Limitación |
|---|---|
| Matrices | Utilice un índice de matriz explícito o la función `EXPLODE` para tener acceso a las matrices. |
| Mapas | Utilice la clave de cadena para acceder a un valor de un mapa y acceder a los mapas. |

Para resolver las limitaciones de Mapa y Matriz, debe utilizar las herramientas de BI para la edición de SQL sin procesar, como las Opciones avanzadas -> Instrucción SQL en Power BI.

Las herramientas de BI como la edición de SQL sin procesar son necesarias para resolver las limitaciones de asignaciones y matrices. Consulte la guía sobre cómo [usar las opciones avanzadas de Power BI para escribir una consulta SQL personalizada](../clients/power-bi.md#import-tables-using-custom-sql) en la sección de instrucciones SQL.

## Pasos siguientes

En este documento se explica cómo aplanar las estructuras de datos anidadas para utilizarlas con herramientas de BI de terceros. Si aún no ha conectado a su cliente, consulte [la descripción general de la conexión de cliente](../clients/overview.md) para obtener una lista de clientes de terceros admitidos.
