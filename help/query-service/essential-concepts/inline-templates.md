---
title: Plantillas en línea
description: Aprenda a reutilizar varias condiciones en numerosas consultas con plantillas en línea.
source-git-commit: f8ec94b4c93e3b36667bdb179ce12c10d20fa30f
workflow-type: tm+mt
source-wordcount: '477'
ht-degree: 1%

---

# Plantillas en línea

Las plantillas en línea permiten reutilizar varias condiciones en varias consultas. Puede guardar criterios en una plantilla y luego reutilizarlos en varias consultas. Las plantillas SQL reutilizables reducen los esfuerzos de desarrollo y también el riesgo de errores al copiar instrucciones largas entre consultas. Con las plantillas en línea, puede realizar cambios en una ubicación y hacer que dichos cambios se reflejen en cualquier consulta que haga referencia a esta plantilla.

Este documento cubre el uso y las limitaciones de las plantillas en línea dentro del Editor de consultas.

## Requisitos previos

Las plantillas en línea son compatibles con la interfaz de usuario y con la API del servicio de consultas. Antes de continuar con esta guía, lea la documentación sobre cómo [crear una plantilla de consulta a través de la API](../api/query-templates.md#create-a-query-template) o con el [Editor de consultas](../ui/user-guide.md#query-authoring).

## Sintaxis de plantilla en línea {#syntax}

Una vez guardada una consulta, se conoce como plantilla. Cuando la plantilla hace referencia a otra plantilla dentro de la instrucción, se denomina plantilla dentro de la línea. Las plantillas en línea se indican en el SQL utilizando el símbolo hash (#) seguido del nombre de la plantilla. Un ejemplo de esta sintaxis es `#YOUR_TEMPLATE_NAME`.

## Caso de uso {#use-case}

Las siguientes plantillas SQL muestran la utilidad de las plantillas en línea, con un ejemplo para contar el número de clientes de EE. UU. de cualquier región que gastaron más que los &quot;ingresos máximos&quot; y realizaron pedidos antes de junio de 2023. La ventaja de la plantilla en línea es que puede editar fácilmente la plantilla secundaria (en este caso, los ingresos máximos y la fecha de pedido) y no tiene que cambiar la plantilla principal.

**Ejemplo**

```sql
#parent_template : SELECT count(*) FROM customer WHERE region=NA AND country=US AND revenue > #revenue_max
#revenue_max: SELECT max(revenue) FROM revenue_table WHERE order_date > '01-06-2023'
```

Al ejecutar la consulta, el servicio de consultas reemplaza el nombre de la plantilla que comienza por el símbolo hash con la instrucción SQL de la plantilla con nombre.

>[!NOTE]
>
>Las plantillas de consulta pueden llamar a cualquier número de otras plantillas en línea. No hay restricciones en el número de plantillas en línea que puede invocar desde una sola consulta. Las plantillas también se pueden anidar dentro de otras plantillas en línea.

Puede utilizar plantillas para almacenar una o varias condiciones. No es necesario que sean una consulta completa por sí mismas. Si la plantilla contiene una consulta válida, puede ejecutarla simplemente llamando al nombre de la plantilla precedido de un símbolo hash. Por ejemplo, si almacena `SELECT * FROM JUNE_2023_LOYALTY_MEMBERS;` como plantilla denominada `JUNE_2023_LOYALTY_MEMBERS`, el comando  `#JUNE_2023_LOYALTY_MEMBERS;` ejecutaría la consulta válida contenida dentro de la plantilla.

>
>
>En la interfaz de usuario de Adobe Experience Platform, las plantillas en línea en forma de consultas parametrizadas solo se admiten en el nivel principal. Esto significa que las consultas parametrizadas solo funcionan cuando se utilizan en la plantilla original. La plantilla secundaria debe ser una plantilla estática y no puede tener parámetros dinámicos.

## Pasos siguientes

Después de leer este documento, ahora sabe cómo hacer referencia a otras plantillas dentro de su SQL, ya sea en el Editor de consultas o a través de la API del servicio de consultas.

Además, debería leer el [guía de bloques anónimos](./anonymous-block.md), que explica cómo minimizar los gastos generales de desarrollo encadenando una o más sentencias SQL que se ejecutan en secuencia.
