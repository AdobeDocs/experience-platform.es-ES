---
keywords: Experience Platform;inicio;temas populares;servicio de consulta;servicio de consulta;generar conjuntos de datos;generar conjunto de datos;crear conjunto de datos;
solution: Experience Platform
title: Generar conjuntos de datos a partir de resultados en el servicio de consulta
topic-legacy: queries
type: Tutorial
description: El servicio de consulta de Adobe Experience Platform permite crear conjuntos de datos desde la interfaz de usuario. Una vez creado un conjunto de datos, se puede acceder a él como a cualquier otro conjunto de datos en el lago de datos y se puede utilizar para una variedad de casos de uso.
exl-id: 6f6c049d-f19f-4161-aeb4-3a01eca7dc75
source-git-commit: 03e7863f38b882a2fbf6ba0de1755e1924e8e228
workflow-type: tm+mt
source-wordcount: '329'
ht-degree: 1%

---

# Generar conjuntos de datos a partir de resultados en el servicio de consulta

El verdadero poder de [!DNL Query Service] se muestra cuando se utilizan consultas para generar conjuntos de datos en la variable [!DNL Data Lake] para su uso como entrada en más consultas o en otros servicios como [!DNL Data Science Workspace], [!DNL Real-time Customer Profile]o [!DNL Analysis Workspace].

[!DNL Query Service] permite la creación de conjuntos de datos desde la interfaz de usuario. Siga estos pasos:

1. Escriba la consulta utilizando un cliente conectado y valide el resultado.
2. Inicie sesión en la [!DNL Platform] Interfaz de usuario y vaya a Consultas.
3. Busque la consulta en la lista y pase el ratón por encima de la fila .
4. Select **[!UICONTROL Crear conjunto de datos]**. ![Imagen](../images/ui/create-datasets/output-dataset.png)
5. Introduzca un nombre de conjunto de datos, precedido de su ID LDAP (no tiene que ser único ni seguro para SQL; el sistema genera un &quot;nombre de tabla&quot; basado en el nombre dado aquí).
6. Introduzca una descripción del conjunto de datos y seleccione **[!UICONTROL Ejecutar consulta]**.![Imagen](../images/ui/create-datasets/run-query.png)
7. Observe la consulta completada y, a continuación, vaya a la página de lista de conjuntos de datos para ver el conjunto de datos que acaba de crear.

Una vez creado un conjunto de datos, se puede acceder a él como a cualquier otro conjunto de datos en la [!DNL Data Lake] y se utiliza para una variedad de casos de uso.

>[!NOTE]
>
>En una implementación activa, debe aplicar etiquetas de control de datos después de crear el conjunto de datos.

## Generar conjuntos de datos con una [!DNL Experience Data Model] esquema

Para generar un conjunto de datos con una [!DNL Experience Data Model] (XDM), debe utilizar la sintaxis SQL. Para obtener más información sobre la sintaxis que debe utilizar, lea la [Guía de sintaxis SQL](../sql/syntax.md#create-table-as-select).

## Conjuntos de datos de salida

Los conjuntos de datos creados mediante esta funcionalidad se generan con un esquema ad hoc que coincide con la estructura de los datos de salida definida en la instrucción SQL. Algunos servicios descendentes requieren conjuntos de datos con [!DNL Experience Data Model] esquemas (XDM). Compruebe los requisitos de formato de datos para los servicios descendentes antes de escribir las consultas.
