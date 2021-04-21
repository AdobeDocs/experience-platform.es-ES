---
keywords: Experience Platform;inicio;temas populares;servicio de consulta;servicio de consulta;generar conjuntos de datos;generar conjunto de datos;crear conjunto de datos;
solution: Experience Platform
title: Generar conjuntos de datos a partir de resultados en el servicio de consulta
topic-legacy: queries
type: Tutorial
description: El servicio de consulta de Adobe Experience Platform permite crear conjuntos de datos desde la interfaz de usuario. Una vez creado un conjunto de datos, se puede acceder a él como a cualquier otro conjunto de datos en el lago de datos y se puede utilizar para una variedad de casos de uso.
exl-id: 6f6c049d-f19f-4161-aeb4-3a01eca7dc75
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '323'
ht-degree: 1%

---

# Generar conjuntos de datos a partir de resultados en el servicio de consulta

El verdadero poder de [!DNL Query Service] se revela cuando las consultas se utilizan para generar conjuntos de datos en el [!DNL Data Lake] que se utilizarán como entrada en más consultas o en otros servicios como [!DNL Data Science Workspace], [!DNL Real-time Customer Profile] o [!DNL Analysis Workspace].

[!DNL Query Service] permite la creación de conjuntos de datos desde la interfaz de usuario. Siga estos pasos:

1. Escriba la consulta utilizando un cliente conectado y valide el resultado.
2. Inicie sesión en la interfaz de usuario de [!DNL Platform] y vaya a Consultas.
3. Busque la consulta en la lista y pase el ratón por encima de la fila .
4. Haga clic en **[!UICONTROL Create Dataset]**. ![Imagen](../images/ui/output-dataset.png)
5. Introduzca un nombre de conjunto de datos, precedido de su ID LDAP (no tiene que ser único ni seguro para SQL; el sistema genera un &quot;nombre de tabla&quot; basado en el nombre dado aquí).
6. Introduzca una descripción del conjunto de datos y haga clic en **[!UICONTROL Run Query]**.![Imagen](../images/ui/run-query.png)
7. Observe la consulta completada y, a continuación, vaya a la página de lista de conjuntos de datos para ver el conjunto de datos que acaba de crear.

Después de crear un conjunto de datos, se puede acceder a él como a cualquier otro conjunto de datos en [!DNL Data Lake] y se puede utilizar para una variedad de casos de uso.

>[!NOTE]
>
>En una implementación activa, debe aplicar etiquetas [!DNL Data Governance] después de crear el conjunto de datos.

## Generar conjuntos de datos con un esquema [!DNL Experience Data Model] predefinido

Para generar un conjunto de datos con un esquema predefinido [!DNL Experience Data Model] (XDM), debe utilizar la sintaxis SQL. Para obtener más información sobre la sintaxis que debe utilizar, lea la [Guía de sintaxis SQL](../sql/syntax.md#create-table-as-select).

## Conjuntos de datos de salida

Los conjuntos de datos creados mediante esta funcionalidad se generan con un esquema ad hoc que coincide con la estructura de los datos de salida definida en la instrucción SQL. Algunos servicios descendentes requieren conjuntos de datos con esquemas [!DNL Experience Data Model] (XDM) particulares. Compruebe los requisitos de formato de datos para los servicios descendentes antes de escribir las consultas.
