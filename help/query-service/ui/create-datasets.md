---
keywords: Experience Platform;inicio;temas populares;servicio de consulta;servicio de Consulta;generar conjuntos de datos;generar conjunto de datos;crear conjunto de datos;
solution: Experience Platform
title: Generar conjuntos de datos a partir de resultados en el servicio de Consulta
topic: queries
type: Tutorial
description: 'El servicio de Consulta de Adobe Experience Platform permite crear conjuntos de datos desde la interfaz de usuario. Después de crear un conjunto de datos, se puede acceder a él como cualquier otro conjunto de datos en el lago de datos y utilizarlo para una variedad de casos de uso. '
translation-type: tm+mt
source-git-commit: 97dc0b5fb44f5345fd89f3f56bd7861668da9a6e
workflow-type: tm+mt
source-wordcount: '327'
ht-degree: 1%

---


# Generar conjuntos de datos a partir de resultados en el servicio de Consulta

La verdadera potencia de [!DNL Query Service] se revela cuando se utilizan consultas para generar datasets en [!DNL Data Lake] que se utilizarán como entrada en más consultas o en otros servicios como [!DNL Data Science Workspace], [!DNL Real-time Customer Profile] o [!DNL Analysis Workspace].

[!DNL Query Service] permite la creación de conjuntos de datos desde la interfaz de usuario. Siga estos pasos:

1. Escriba la consulta con un cliente conectado y valide la salida.
2. Inicie sesión en la [!DNL Platform] interfaz de usuario y vaya a Consultas.
3. Busque su consulta en la lista y pase el ratón sobre la fila.
4. Haga clic en **[!UICONTROL Crear conjunto de datos]**. ![Imagen](../images/ui/output-dataset.png)
5. Escriba un nombre de conjunto de datos, precedido de su ID de LDAP (no tiene que ser único ni SQL seguro; el sistema genera un &quot;nombre de tabla&quot; basado en el nombre proporcionado aquí).
6. Escriba una descripción del conjunto de datos y haga clic en **[!UICONTROL Ejecutar Consulta]**.![Imagen](../images/ui/run-query.png)
7. Observe la consulta completa y luego vaya a la página de lista del conjunto de datos para ver el conjunto de datos que acaba de crear.

Después de crear un conjunto de datos, se puede acceder a él como cualquier otro conjunto de datos en [!DNL Data Lake] y utilizarlo para diversos casos de uso.

>[!NOTE]
>
>En una implementación dinámica, debe aplicar [!DNL Data Governance] etiquetas después de crear el conjunto de datos.

## Generar datasets con un esquema predefinido [!DNL Experience Data Model]

Para generar un conjunto de datos con un esquema predefinido [!DNL Experience Data Model] (XDM), deberá utilizar la sintaxis SQL. Para obtener más información sobre la sintaxis que debe utilizar, lea la [Guía de sintaxis de SQL](../sql/syntax.md#create-table-as-select).

## datasets de salida

Los conjuntos de datos creados mediante esta funcionalidad se generan con un esquema ad hoc que coincide con la estructura de los datos de salida definida en la instrucción SQL. Algunos servicios posteriores requieren conjuntos de datos con esquemas [!DNL Experience Data Model] (XDM) concretos. Antes de escribir las consultas, compruebe los requisitos de formato de datos para los servicios de flujo descendente.