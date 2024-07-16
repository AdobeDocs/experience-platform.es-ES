---
keywords: Experience Platform;inicio;temas populares;servicio de consultas;servicio de consultas;generar conjuntos de datos;generar conjunto de datos;crear conjunto de datos;
solution: Experience Platform
title: Generar conjuntos de datos de salida a partir de resultados de consulta
type: Tutorial
description: El servicio de consulta de Adobe Experience Platform permite crear conjuntos de datos desde la interfaz de usuario. Una vez creado un conjunto de datos, se puede acceder a él como cualquier otro conjunto de datos del lago de datos y utilizarlo en una variedad de casos de uso.
exl-id: 6f6c049d-f19f-4161-aeb4-3a01eca7dc75
source-git-commit: 59d2d74b2d77f3bbaca381af908de5295af24e5b
workflow-type: tm+mt
source-wordcount: '497'
ht-degree: 0%

---

# Generar conjuntos de datos de salida a partir de resultados de consulta

[!DNL Query Service] le permite usar consultas para generar conjuntos de datos en [!DNL Data Lake]. Estos conjuntos de datos se pueden usar como entrada para más consultas o en otros servicios como [!DNL Data Science Workspace], Perfil del cliente en tiempo real o [!DNL Analysis Workspace].

## Generar conjuntos de datos desde la interfaz de usuario de Adobe Experience Platform

Para crear conjuntos de datos desde la interfaz de usuario (IU) de Adobe Experience Platform, siga estos pasos:

1. Cree una consulta con un cliente conectado y valide el resultado. Para aprender a escribir consultas con [!DNL Query Editor], lea la guía de la interfaz de usuario de [!DNL Query Editor] [sobre cómo escribir consultas](./user-guide.md#writing-queries).

2. En la interfaz de usuario de Platform, vaya a **[!UICONTROL Consultas]** seguida de la pestaña **[!UICONTROL Plantillas]** y seleccione la consulta que ha creado. Para obtener más información sobre cómo ver las consultas que se crearon y guardaron para su organización en la interfaz de usuario de Platform, lea la [[!DNL Query Service] descripción general](./overview.md#browse).

3. En el panel Detalles de la consulta, seleccione **[!UICONTROL Ejecutar como CTAS]**.

   ![Se ha resaltado la pestaña del área de trabajo de consultas [!UICONTROL Plantillas] con la opción Seleccionar [!UICONTROL Ejecutar como CTAS].](../images/ui/create-datasets/run-as-ctas.png)

4. En el cuadro de diálogo que aparece, introduzca un nombre de conjunto de datos precedido de su ID de LDAP. El nombre del conjunto de datos no tiene que ser único ni seguro para SQL. Tenga en cuenta que el nombre de tabla del conjunto de datos se generará en función del nombre del conjunto de datos que cree aquí.

5. A continuación, escriba una descripción para su conjunto de datos en el campo [!UICONTROL Descripción] y seleccione **[!UICONTROL Ejecutar como CTAS]**.

   ![Se ha resaltado el cuadro de diálogo Conjunto de datos de salida con los detalles del conjunto de datos y [!UICONTROL Ejecutar como CTAS]](../images/ui/create-datasets/run-query.png)

6. Una vez finalizada la ejecución de la consulta, vaya a **[!UICONTROL Conjuntos de datos]** para ver el conjunto de datos que ha creado. Para obtener más información sobre cómo realizar acciones comunes al trabajar con conjuntos de datos en la interfaz de usuario de Platform, consulte la [Guía de la interfaz de usuario de conjuntos de datos](../../catalog/datasets/user-guide.md).

Una vez creado un conjunto de datos, se puede tener acceso a él como a cualquier otro conjunto de datos del [!DNL Data Lake] y utilizarlo en diversos casos de uso.

>[!NOTE]
>
>En una implementación activa, debe aplicar las etiquetas de Control de datos después de crear el conjunto de datos. Para obtener más información sobre cómo aplicar etiquetas de uso de datos a conjuntos de datos, consulte la [Información general sobre las etiquetas de uso de datos](../../data-governance/labels/overview.md).

## Generar conjuntos de datos con un esquema [!DNL Experience Data Model] predefinido

Utilice la sintaxis SQL para generar un conjunto de datos con un esquema [!DNL Experience Data Model] (XDM) predefinido. Para obtener más información acerca de la sintaxis admitida por [!DNL Query Service], lea la [Guía de sintaxis SQL](../sql/syntax.md#create-table-as-select).

## Conjuntos de datos de salida

Los conjuntos de datos creados a través de esta funcionalidad se generan con un esquema ad hoc que coincide con la estructura de los datos de salida tal como se definen en la instrucción SQL. Algunos servicios descendentes requieren conjuntos de datos con esquemas XDM específicos. Compruebe los requisitos de formato de datos para los servicios descendentes antes de escribir las consultas.

## Pasos siguientes

Después de leer este documento, debería saber cómo usar [!DNL Query Service] para generar conjuntos de datos desde la interfaz de usuario de Platform. Para obtener más información sobre cómo tener acceso, escribir y ejecutar consultas en la interfaz de usuario de Platform, consulte la [[!DNL Query Service] descripción general de la interfaz de usuario](./overview.md).
