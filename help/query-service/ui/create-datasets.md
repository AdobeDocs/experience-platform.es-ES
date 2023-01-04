---
keywords: Experience Platform;inicio;temas populares;servicio de consulta;servicio de consulta;generar conjuntos de datos;generar conjunto de datos;crear conjunto de datos;
solution: Experience Platform
title: Generar conjuntos de datos a partir de resultados en el servicio de consulta
topic-legacy: queries
type: Tutorial
description: El servicio de consulta de Adobe Experience Platform permite crear conjuntos de datos desde la interfaz de usuario. Una vez creado un conjunto de datos, se puede acceder a él como a cualquier otro conjunto de datos en el lago de datos y se puede utilizar para una variedad de casos de uso.
exl-id: 6f6c049d-f19f-4161-aeb4-3a01eca7dc75
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '493'
ht-degree: 0%

---

# Generar conjuntos de datos a partir de resultados en [!DNL Query Service]

[!DNL Query Service] permite utilizar consultas para generar conjuntos de datos en la variable [!DNL Data Lake]. Estos conjuntos de datos se pueden usar luego como entrada para más consultas o en otros servicios como [!DNL Data Science Workspace], Perfil del cliente en tiempo real, o [!DNL Analysis Workspace].

## Generar conjuntos de datos desde la interfaz de usuario de Adobe Experience Platform

Para crear conjuntos de datos desde la interfaz de usuario (IU) de Adobe Experience Platform, siga estos pasos:

1. Cree una consulta con un cliente conectado y valide el resultado. Para aprender a escribir consultas mediante [!DNL Query Editor], lea la [!DNL Query Editor] Guía de la interfaz de usuario [sobre la escritura de consultas](./user-guide.md#writing-queries).

2. En la interfaz de usuario de Platform, vaya a **[!UICONTROL Consultas]** seguido de **[!UICONTROL Plantillas]** y seleccione la consulta que ha creado. Para obtener más información sobre cómo ver las consultas creadas y guardadas para su organización en la interfaz de usuario de Platform, lea la [[!DNL Query Service] información general](./overview.md#browse).

3. En el panel Detalles de la consulta , seleccione **[!UICONTROL Conjunto de datos de salida]**.

   ![La ficha Plantillas del espacio de trabajo Consultas con Seleccionar conjunto de datos de salida resaltado.](../images/ui/create-datasets/output-dataset.png)

4. En el cuadro de diálogo que aparece, introduzca un nombre de conjunto de datos precedido de su ID LDAP. El nombre del conjunto de datos no tiene que ser único ni seguro para SQL. Tenga en cuenta que el nombre de tabla de su conjunto de datos se generará en función del nombre del conjunto de datos que cree aquí.

5. A continuación, introduzca una descripción para su conjunto de datos en la [!UICONTROL Descripción] y seleccione **[!UICONTROL Ejecutar consulta]**.

   ![El cuadro de diálogo Conjunto de datos de salida con los detalles del conjunto de datos y la consulta de ejecución resaltada](../images/ui/create-datasets/run-query.png)

6. Una vez finalizada la ejecución de la consulta, vaya a **[!UICONTROL Conjuntos de datos]** para ver el conjunto de datos que ha creado. Para obtener más información sobre cómo realizar acciones comunes al trabajar con conjuntos de datos en la interfaz de usuario de Platform, consulte la [Guía de la interfaz de usuario de conjuntos de datos](../../catalog/datasets/user-guide.md).

Una vez creado un conjunto de datos, se puede acceder a él como a cualquier otro conjunto de datos en la [!DNL Data Lake] y se utiliza para una variedad de casos de uso.

>[!NOTE]
>
>En una implementación activa, debe aplicar etiquetas de control de datos después de crear el conjunto de datos. Para obtener más información sobre cómo aplicar etiquetas de uso de datos a conjuntos de datos, consulte la [Información general sobre las etiquetas de uso de datos](../../data-governance/labels/overview.md).

## Generar conjuntos de datos con una [!DNL Experience Data Model] esquema

Utilice la sintaxis SQL para generar un conjunto de datos con un [!DNL Experience Data Model] (XDM). Para obtener más información sobre la sintaxis admitida por [!DNL Query Service], lea la [Guía de sintaxis SQL](../sql/syntax.md#create-table-as-select).

## Conjuntos de datos de salida

Los conjuntos de datos creados mediante esta funcionalidad se generan con un esquema ad hoc que coincide con la estructura de los datos de salida definida en la instrucción SQL. Algunos servicios descendentes requieren conjuntos de datos con esquemas XDM particulares. Compruebe los requisitos de formato de datos para los servicios descendentes antes de escribir las consultas.

## Pasos siguientes

Después de leer este documento, ahora debe comprender cómo usar [!DNL Query Service] para generar conjuntos de datos desde la interfaz de usuario de Platform. Para obtener más información sobre cómo acceder, escribir y ejecutar consultas dentro de la interfaz de usuario de Platform, consulte la [[!DNL Query Service] Información general sobre la IU](./overview.md).
