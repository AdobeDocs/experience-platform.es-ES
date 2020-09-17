---
keywords: Experience Platform;home;popular topics;query service;Query service;Power BI;power bi;connect to query service;
solution: Experience Platform
title: Conectar con Power BI
topic: connect
translation-type: tm+mt
source-git-commit: f9749dbc5f2e3ac15be50cc5317ad60586b2c07e
workflow-type: tm+mt
source-wordcount: '333'
ht-degree: 1%

---


# Conectar con [!DNL Power BI] (PC)

Los usuarios de PC pueden realizar la instalación [!DNL Power BI] desde [https://powerbi.microsoft.com/en-us/desktop/](https://powerbi.microsoft.com/en-us/desktop/).

## Set up [!DNL Power BI]

Una vez [!DNL Power BI] instalado, debe configurar los componentes necesarios para admitir el conector PostgreSQL. Siga estos pasos:

- Busque e instale `npgsql`, un paquete de controladores .NET para PostgreSQL que es la forma oficial de conexión de PowerBI.

- Seleccione la versión 4.0.10 (las versiones más recientes dan como resultado un error).

- En &quot;Instalación de Npgsql GAC&quot; en la pantalla Configuración personalizada, seleccione **[!UICONTROL Se instalará en el disco duro]** local. Si no instala el GAC, el Power BI fallará más tarde.

- Reinicie Windows.

- Busque la versión de evaluación de [!DNL PowerBI] Desktop.

## Conectar [!DNL Power BI] a [!DNL Query Service]

Después de realizar estos pasos preparatorios, puede conectarse [!DNL Power BI] a [!DNL Query Service]:

- Open [!DNL Power BI].

- Haga clic en **[!UICONTROL Obtener datos]** en la cinta del menú superior.

- Elija **[!UICONTROL Base de datos]** PostgreSQL y, a continuación, haga clic en **[!UICONTROL Connect]**.

- Introduzca valores para el servidor y la base de datos. **[!UICONTROL El servidor]** es el host que se encuentra en los detalles de la conexión. Para producción, agregue el puerto `:80` al final de la cadena Host. **[!UICONTROL La base de datos]** puede ser &quot;todo&quot; o un nombre de tabla de conjunto de datos. (Pruebe uno de los conjuntos de datos derivados de CTAS).

- Haga clic en Opciones **** avanzadas y, a continuación, desmarque **[!UICONTROL incluir columnas]** de relación. No marque **[!UICONTROL Navegar con jerarquía]** completa.

- *(Opcional pero recomendada cuando se declara &quot;todo&quot; para la base de datos)* Introduzca una instrucción SQL.

>[!NOTE]
>
>Si no se proporciona una instrucción SQL, [!DNL Power BI] se previsualización todas las tablas de la base de datos. Para los datos jerárquicos, se debe utilizar una instrucción SQL personalizada. Si el esquema de tabla es plano, funcionará con o sin una instrucción SQL personalizada. Los tipos compuestos aún no son compatibles con [!DNL Power BI] - para obtener tipos primitivos de tipos compuestos, deberá escribir sentencias SQL para derivarlos.

```sql
SELECT web.webPageDetails.name AS Page_Name, 
SUM(web.webPageDetails.pageviews.value) AS Page_Views 
FROM _TABLE_ 
WHERE TIMESTAMP >= to_timestamp('2018-11-20')
GROUP BY web.webPageDetails.name 
ORDER BY SUM(web.webPageDetails.pageviews.value) DESC 
LIMIT 10
```

- Seleccione **[!UICONTROL DirectQuery]** o el modo **[!UICONTROL Importar]** . En el modo **[!UICONTROL Importar]** , los datos se importarán en [!DNL Power BI]. En el modo **[!UICONTROL DirectQuery]** , todas las consultas se enviarán a [!DNL Query Service] para su ejecución.

- Haga clic en **[!UICONTROL Aceptar]**. Ahora, [!DNL Power BI] se conecta al [!DNL Query Service] y produce una previsualización si no hay errores. Hay un problema conocido con la Previsualización que procesa las columnas numéricas. Continúe con el paso siguiente.

- Haga clic en **[!UICONTROL Cargar]** para introducir el conjunto de datos en [!DNL Power BI].
