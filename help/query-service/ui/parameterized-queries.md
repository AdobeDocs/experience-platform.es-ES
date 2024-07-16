---
title: Consultas con parámetros
description: Aprenda a utilizar consultas parametrizadas en la interfaz de usuario de Adobe Experience Platform.
exl-id: 5c5ac691-5e29-4262-ba53-84dcc56e744f
source-git-commit: 9cf8dabfdf3f20f4032a79ba191bd2dc8123a369
workflow-type: tm+mt
source-wordcount: '690'
ht-degree: 11%

---

# Consultas parametrizadas {#parameterized-queries}

>[!CONTEXTUALHELP]
>id="platform_queryService_queryEditor_parameterizedQueries"
>title="Consultas parametrizadas"
>abstract="Utilice consultas parametrizadas para añadir valores de parámetro en el momento de la ejecución. Esto le permite trabajar con datos dinámicos y reutilizar consultas para diferentes casos de uso. Utilice el comienzo `'$'` para introducir un parámetro de consulta en su consulta del editor de texto. A continuación, añada un valor para la clave en la sección Parámetros de consulta debajo del editor."

El servicio de consultas admite el uso de consultas parametrizadas en el Editor de consultas. Con las consultas con parámetros, ahora puede utilizar marcadores de posición para parámetros y agregar los valores de parámetro en el momento de la ejecución. Los marcadores de posición permiten trabajar con datos dinámicos en los que no sabe cuáles serán los valores hasta que se ejecute la instrucción. También puede preparar sus consultas con antelación y reutilizarlas para fines similares. La reutilización de consultas ahorra un esfuerzo considerable ya que evita la creación de consultas SQL distintas para cada caso de uso.

## Requisitos previos

Antes de continuar con esta guía, lea la [guía de la interfaz de usuario del editor de consultas](./user-guide.md). La guía del Editor de consultas proporciona información detallada sobre cómo escribir, validar y ejecutar consultas para datos de experiencia del cliente en la interfaz de usuario de Experience Platform.

>[!NOTE]
>
>En la interfaz de usuario de Adobe Experience Platform, las consultas parametrizadas solo se admiten en el nivel principal de las plantillas en línea. Esto significa que las consultas parametrizadas solo funcionan cuando se utilizan en la plantilla original. Las plantillas secundarias deben ser una plantilla estática y no pueden tener parámetros dinámicos. Consulte la [documentación de plantillas en línea](../key-concepts/inline-templates.md) para obtener más información.

## Sintaxis de consulta parametrizada {#syntax}

Las consultas parametrizadas utilizan el formato `'$YOUR_PARAMETER_NAME'` y se pueden concatenar mediante notación de puntos. A continuación se muestra un ejemplo de una instrucción SQL que utiliza consultas parametrizadas.

```sql
INSERT INTO
   $Database_Name.Schema_Name.adwh_lkup_process_delta_log
   (process_name, merge_policy_id, process_status, process_date, create_ts, change_ts)
SELECT
   '$Table_Process_Name' process_name,
   hash('$Merge_PolicyID') merge_policy_id,
   '$process_status' process_status,
   to_date('$date_key') process_date,
   CURRENT_TIMESTAMP create_ts,
   CURRENT_TIMESTAMP change_ts;
```

## Creación de una consulta con parámetros {#create}

Para crear la consulta parametrizada en la interfaz de usuario de, vaya al Editor de consultas. Consulte la sección sobre [acceso al Editor de consultas](./user-guide.md#accessing-query-editor) para obtener más instrucciones.

Utilice el comienzo `'$'` para introducir un parámetro de consulta en su consulta del editor de texto. A continuación, seleccione la pestaña **[!UICONTROL Parámetros de consulta]** junto a la [!UICONTROL Consola] para agregar el valor que falta para la clave. La consulta no se puede ejecutar si no agrega un valor a ninguna de las claves requeridas. Un icono de alerta (![Un icono de alerta.](../images/ui/parameterized-queries/alert-icon.png)) aparece en la sección Parámetros de consulta junto a cualquier campo de entrada [!UICONTROL Value] vacío.

>[!NOTE]
>
>Si la consulta no acepta parámetros, aún puede introducir parámetros innecesarios dentro del Editor de consultas. El Editor de consultas ignora todos los pares clave-valor innecesarios y no tienen ningún efecto en la ejecución ni en los resultados de la consulta.

![Se resaltó el Editor de consultas con una consulta parametrizada y la sección Parámetros de consulta.](../images/ui/parameterized-queries/parameterized-query.png)

>[!TIP]
>
>Cambie las pestañas de [!UICONTROL Parámetros de consulta] a [!UICONTROL Consola] para ver el resultado de la consola de la consulta.

## Utilice los detalles de registros de consulta para comprobar los valores de parámetros {#check-parameter-values}

No se pueden guardar parámetros dentro de las plantillas porque los valores utilizados no son persistentes. Sin embargo, puede comprobar la página [!UICONTROL Detalles del registro de consultas] para encontrar los valores de parámetros utilizados en una ejecución de consulta. En este caso, los registros no indican que la consulta fuera una consulta parametrizada. Consulte la [documentación de registros de consulta](./query-logs.md) para obtener instrucciones sobre cómo encontrar los valores utilizados.

![La vista de registros de consulta con el SQL de una consulta parametrizada resaltada en la sección de detalles.](../images/ui/parameterized-queries/parameterized-query-logs.png)

<!-- improve screenshot above ^ I am waiting for a scheduled run to complete -->

## Programar una consulta parametrizada {#schedule}

Los valores de parámetro se guardan al programar una consulta parametrizada. Para programar una consulta parametrizada, siga el proceso típico para crear una consulta programada como se describe en la guía para [crear una programación de consulta](./query-schedules.md#create-schedule) y, a continuación, introduzca los valores de parámetro que se utilizarán en la ejecución de la consulta. Esta sección de la interfaz de usuario solo aparece para consultas parametrizadas. Consulte la sección sobre [configuración de parámetros para una consulta parametrizada programada](./query-schedules.md#set-parameters) para obtener instrucciones específicas.

>[!TIP]
>
>El servicio de consulta admite instrucciones preparadas mediante el uso de consultas parametrizadas. Consulte la [guía de sintaxis de instrucciones preparadas](../sql/prepared-statements.md) para obtener más información sobre la sintaxis SQL implicada.

## Pasos siguientes

Al leer este documento, ha aprendido a parametrizar consultas en la interfaz de usuario de Adobe Experience Platform y a utilizarlas en ejecuciones de consultas programadas. El documento también resaltaba cómo comprobar los registros para los valores de parámetro utilizados en las ejecuciones de consultas.

A continuación, se recomienda leer la guía sobre [supervisión de consultas programadas](./monitor-queries.md) para comprender mejor el estado de todos los trabajos de consulta a través de la interfaz de usuario de Platform.
