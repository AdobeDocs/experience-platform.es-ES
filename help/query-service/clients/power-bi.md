---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Conectar con Power BI
topic: connect
translation-type: tm+mt
source-git-commit: 7d5d98d8e32607abf399fdc523d2b3bc99555507

---


# Conectar con Power BI (PC)

Los usuarios de PC pueden instalar Power BI desde [https://powerbi.microsoft.com/en-us/desktop/](https://powerbi.microsoft.com/en-us/desktop/).

## Configuración de Power Bi

Después de tener Power BI instalado, debe configurar los componentes necesarios para admitir el conector PostgreSQL. Siga estos pasos:

- Busque e instale `npgsql`, un paquete de controladores .NET para PostgreSQL que es la forma oficial de conexión de PowerBI.

- Seleccione la versión 4.0.10 (las versiones más recientes dan como resultado un error).

- En &quot;Instalación de Npgsql GAC&quot; en la pantalla Configuración personalizada, seleccione **Se instalará en el disco duro** local. Si no instala GAC, Power BI fallará más tarde.

- Reinicie Windows.

- Busque la versión de evaluación de PowerBI Desktop.

## Conectar Power BI al servicio de Consulta

Después de realizar estos pasos preparatorios, puede conectar Power BI al servicio de Consulta:

- Abra Power BI.

- Haga clic en **Obtener datos** en la cinta del menú superior.

- Elija **Base de datos** PostgreSQL y, a continuación, haga clic en **Connect**.

- Introduzca valores para el servidor y la base de datos. **El servidor** es el host que se encuentra en los detalles de la conexión. Para producción, agregue el puerto `:80` al final de la cadena Host. **La base de datos** puede ser &quot;todo&quot; o un nombre de tabla de conjunto de datos. (Pruebe uno de los conjuntos de datos derivados de CTAS).

- Haga clic en Opciones **** avanzadas y, a continuación, desmarque **incluir columnas** de relación. No marque **Navegar con jerarquía** completa.

- *(Opcional pero recomendada cuando se declara &quot;todo&quot; para la base de datos)* Introduzca una instrucción SQL.

>[!NOTE] Si no se proporciona una instrucción SQL, Power BI previsualización todas las tablas de la base de datos. Para los datos jerárquicos, se debe utilizar una instrucción SQL personalizada. Si el esquema de tabla es plano, funcionará con o sin una instrucción SQL personalizada. Los tipos compuestos aún no son compatibles con Power BI: para obtener tipos primitivos de tipos compuestos, deberá escribir sentencias SQL para derivarlos.

```sql
SELECT web.webPageDetails.name AS Page_Name, 
SUM(web.webPageDetails.pageviews.value) AS Page_Views 
FROM _TABLE_ 
WHERE _ACP_YEAR=2018 AND _ACP_MONTH=11 AND _ACP_DAY=20 
GROUP BY web.webPageDetails.name 
ORDER BY SUM(web.webPageDetails.pageviews.value) DESC 
LIMIT 10
```

- Seleccione **DirectQuery** o el modo **Importar** . En el modo **Importar** , los datos se importarán en Power BI. En el modo **DirectQuery** , todas las consultas se enviarán al servicio de Consulta para su ejecución.

- Haga clic en **Aceptar**. Ahora, Power BI se conecta al servicio de Consulta y genera una previsualización si no hay errores. Hay un problema conocido con la Previsualización que procesa las columnas numéricas. Continúe con el paso siguiente.

- Haga clic en **Cargar** para traer el conjunto de datos a Power BI.
