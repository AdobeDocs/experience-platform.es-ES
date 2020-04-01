---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Generar conjuntos de datos a partir de resultados de consulta
topic: queries
translation-type: tm+mt
source-git-commit: 7d5d98d8e32607abf399fdc523d2b3bc99555507

---


# Generar conjuntos de datos a partir de resultados de consulta

El verdadero poder del servicio de Consulta se revela cuando se utilizan consultas para generar conjuntos de datos en el lago de datos que se utilizarán como entrada en más consultas o en otros servicios como Área de trabajo de ciencia de datos, Perfil de clientes en tiempo real o Espacio de trabajo de Análisis.

El servicio de Consulta permite crear conjuntos de datos desde la interfaz de usuario. Siga estos pasos:

1. Escriba la consulta con un cliente conectado y valide la salida.
2. Inicie sesión en la interfaz de usuario de la plataforma y vaya a Consultas.
3. Busque su consulta en la lista y pase el ratón sobre la fila.
4. Haga clic en **Crear conjunto de datos**. ![Imagen](../images/queries/create-datasets/click-create-dataset.png)
5. Escriba un nombre de conjunto de datos, precedido de su ID de LDAP (no tiene que ser único ni SQL seguro; el sistema genera un &quot;nombre de tabla&quot; basado en el nombre proporcionado aquí).
6. Introduzca una descripción del conjunto de datos y haga clic en **Ejecutar Consulta**.![Imagen](../images/queries/create-datasets/run-query.png)
7. Observe la consulta completa y luego vaya a la página de lista del conjunto de datos para ver el conjunto de datos que acaba de crear.

Después de crear un conjunto de datos, se puede acceder a él como cualquier otro conjunto de datos en el lago de datos y utilizarlo para diversos casos de uso.

>[!NOTE] En una implementación dinámica, debe aplicar etiquetas de Administración de datos después de crear el conjunto de datos.

## Generar conjuntos de datos con un esquema predefinido del modelo de datos de experiencia

Para generar un conjunto de datos con un esquema predefinido de modelo de datos de experiencia (XDM), deberá utilizar la sintaxis SQL. Para obtener más información sobre la sintaxis que debe utilizar, lea la guía Sintaxis [SQL](../sql/syntax.md#create-table-as-select).

## datasets de salida

Los conjuntos de datos creados mediante esta funcionalidad se generan con un esquema ad hoc que coincide con la estructura de los datos de salida definida en la instrucción SQL. Algunos servicios posteriores requieren conjuntos de datos con esquemas del Modelo de datos de experiencia (XDM) concretos. Antes de escribir las consultas, compruebe los requisitos de formato de datos para los servicios de flujo descendente.