---
keywords: Experience Platform;JupyterLab;blocs de notas;Data Science Workspace;temas populares;servicio de consultas
solution: Experience Platform
title: Servicio de consultas en Jupyter Notebook
type: Tutorial
description: Adobe Experience Platform le permite utilizar el Lenguaje de consulta estructurado (SQL) en el espacio de trabajo de ciencia de datos integrando el Servicio de consulta en JupyterLab como función estándar. Este tutorial muestra consultas SQL de ejemplo para casos de uso comunes para explorar, transformar y analizar datos de Adobe Analytics.
exl-id: c5ac7d11-a3bd-4ef8-a650-9f496a8bbaa7
source-git-commit: 81f48de908b274d836f551bec5693de13c5edaf1
workflow-type: tm+mt
source-wordcount: '821'
ht-degree: 1%

---

# Servicio de consultas en Jupyter Notebook

[!DNL Adobe Experience Platform] permite utilizar el Lenguaje de consulta estructurado (SQL) en [!DNL Data Science Workspace] al integrar [!DNL Query Service] en [!DNL JupyterLab] como función estándar.

Este tutorial muestra consultas SQL de ejemplo para casos de uso comunes para explorar, transformar y analizar [!DNL Adobe Analytics] datos.

## Primeros pasos

Antes de iniciar este tutorial, debe cumplir los siguientes requisitos previos:

- Acceso a [!DNL Adobe Experience Platform]. Si no tiene acceso a una organización en [!DNL Experience Platform], hable con el administrador del sistema antes de continuar

- Un [!DNL Adobe Analytics] conjunto de datos

- Una comprensión práctica de los siguientes conceptos clave utilizados en este tutorial:
   - [[!DNL Experience Data Model (XDM) and XDM System]](../../xdm/home.md)
   - [[!DNL Query Service]](../../query-service/home.md)
   - [[!DNL Query Service SQL Syntax]](../../query-service/sql/overview.md)
   - Adobe Analytics

## Acceso [!DNL JupyterLab] y [!DNL Query Service] {#access-jupyterlab-and-query-service}

1. Entrada [[!DNL Experience Platform]](https://platform.adobe.com), vaya a **[!UICONTROL Notebooks]** en la columna de navegación izquierda. Espere un momento para que JupyterLab se cargue.

   ![](../images/jupyterlab/query/jupyterlab-launcher.png)

   >[!NOTE]
   >
   >Si no aparece automáticamente una nueva pestaña de lanzador, abra una nueva pestaña de lanzador haciendo clic en **[!UICONTROL Archivo]** luego seleccione **[!UICONTROL Nuevo lanzador]**.

2. En la pestaña Lanzador, haga clic en **[!UICONTROL Vacío]** en un entorno de Python 3 para abrir un bloc de notas vacío.

   ![](../images/jupyterlab/query/blank_notebook.png)

   >[!NOTE]
   >
   >Python 3 es actualmente el único entorno compatible con el servicio de consultas en portátiles.

3. En el carril de selección izquierdo, haga clic en **[!UICONTROL Datos]** y haga doble clic en el **[!UICONTROL Conjuntos de datos]** para enumerar todos los conjuntos de datos.

   ![](../images/jupyterlab/query/dataset.png)

4. Buscar un [!DNL Adobe Analytics] conjunto de datos para explorar y hacer clic con el botón derecho en el listado, haga clic en **[!UICONTROL Consultar datos en Notebook]** para generar consultas SQL en el bloc de notas vacío.

5. Haga clic en la primera celda generada que contenga la función `qs_connect()` y ejecutarlo haciendo clic en el botón de reproducción. Esta función crea una conexión entre la instancia del bloc de notas y el [!DNL Query Service].

   ![](../images/jupyterlab/query/execute.png)

6. Copie hacia abajo el [!DNL Adobe Analytics] Nombre del conjunto de datos de la segunda consulta SQL generada, será el valor después de `FROM`.

   ![](../images/jupyterlab/query/dataset_name.png)

7. Inserte una nueva celda de bloc de notas haciendo clic en **+** botón.

   ![](../images/jupyterlab/query/insert_cell.gif)

8. Copie, pegue y ejecute las siguientes instrucciones de importación en una nueva celda. Estas instrucciones se utilizarán para visualizar los datos:

   ```python
   import plotly.plotly as py
   import plotly.graph_objs as go
   from plotly.offline import iplot
   ```

9. A continuación, copie y pegue las siguientes variables en una nueva celda. Modifique sus valores según sea necesario y luego ejecútelos.

   ```python
   target_table = "your Adobe Analytics dataset name"
   target_year = "2019"
   target_month = "04"
   target_day = "01"
   ```

   - `target_table`: Nombre de su [!DNL Adobe Analytics] conjunto de datos.
   - `target_year`: Año específico del que proceden los datos de destinatario.
   - `target_month`: mes específico del que procede el objetivo.
   - `target_day`: día específico del que proceden los datos de destinatario.

   >[!NOTE]
   >
   >Puede cambiar estos valores en cualquier momento. Al hacerlo, asegúrese de ejecutar la celda de variables para que se apliquen los cambios.

## Consulta de datos {#query-your-data}

Introduzca las siguientes consultas SQL en celdas individuales del bloc de notas. Ejecute una consulta seleccionando en su celda seguida de la opción **[!UICONTROL play]** botón. Los resultados de la consulta o los registros de errores correctos se muestran debajo de la celda ejecutada.

Cuando un portátil está inactivo durante un período de tiempo prolongado, la conexión entre el portátil y [!DNL Query Service] puede romperse. En estos casos, reinicie [!DNL JupyterLab] seleccionando la opción **Restart** botón ![botón reiniciar](../images/jupyterlab/user-guide/restart_button.png) situado en la esquina superior derecha junto al botón de encendido.

El núcleo del bloc de notas se restablece, pero las celdas permanecen, vuelva a ejecutar todas las celdas para continuar donde lo dejó.

### Recuento de visitantes por hora {#hourly-visitor-count}

La siguiente consulta devuelve el recuento de visitantes por hora para una fecha especificada:

#### Consulta

```sql
%%read_sql hourly_visitor -c QS_CONNECTION
SELECT Substring(timestamp, 1, 10)                               AS Day,
       Substring(timestamp, 12, 2)                               AS Hour, 
       Count(DISTINCT concat(enduserids._experience.aaid.id, 
                             _experience.analytics.session.num)) AS Visit_Count 
FROM   {target_table}
WHERE TIMESTAMP = to_timestamp('{target_year}-{target_month}-{target_day}')
GROUP  BY Day, Hour
ORDER  BY Hour;
```

En la consulta anterior, la marca de tiempo en la variable `WHERE` La cláusula está configurada para ser el valor de `target_year`. Incluya variables en consultas SQL al contenerlas entre llaves (`{}`).

La primera línea de la consulta contiene la variable opcional `hourly_visitor`. Los resultados de la consulta se almacenarán en esta variable como un marco de datos Pandas. El almacenamiento de resultados en un marco de datos permite visualizar posteriormente los resultados de la consulta utilizando un [!DNL Python] paquete. Ejecute lo siguiente [!DNL Python] codifique en una nueva celda para generar un gráfico de barras:

```python
trace = go.Bar(
    x = hourly_visitor['Hour'],
    y = hourly_visitor['Visit_Count'],
    name = "Visitor Count"
)
layout = go.Layout(
    title = 'Visit Count by Hour of Day',
    width = 1200,
    height = 600,
    xaxis = dict(title = 'Hour of Day'),
    yaxis = dict(title = 'Count')
)
fig = go.Figure(data = [trace], layout = layout)
iplot(fig)
```

### Recuento de actividades por hora {#hourly-activity-count}

La siguiente consulta devuelve el recuento de acciones por hora para una fecha especificada:

#### Consulta <!-- omit in toc -->

```sql
%%read_sql hourly_actions -d -c QS_CONNECTION
SELECT Substring(timestamp, 1, 10)                        AS Day,
       Substring(timestamp, 12, 2)                        AS Hour, 
       Count(concat(enduserids._experience.aaid.id, 
                    _experience.analytics.session.num,
                    _experience.analytics.session.depth)) AS Count 
FROM   {target_table}
WHERE TIMESTAMP = to_timestamp('{target_year}-{target_month}-{target_day}')
GROUP  BY Day, Hour
ORDER  BY Hour;
```

Al ejecutar la consulta anterior, se almacenarán los resultados en `hourly_actions` como un marco de datos. Ejecute la siguiente función en una nueva celda para previsualizar los resultados:

```python
hourly_actions.head()
```

La consulta anterior se puede modificar para devolver el recuento de acciones por hora para un intervalo de fechas especificado utilizando operadores lógicos en **DONDE** Cláusula:

#### Consulta <!-- omit in toc -->

```sql
%%read_sql hourly_actions_date_range -d -c QS_CONNECTION
SELECT Substring(timestamp, 1, 10)                        AS Day,
       Substring(timestamp, 12, 2)                        AS Hour, 
       Count(concat(enduserids._experience.aaid.id, 
                    _experience.analytics.session.num,
                    _experience.analytics.session.depth)) AS Count 
FROM   {target_table}
WHERE  timestamp >= TO_TIMESTAMP('2019-06-01 00', 'YYYY-MM-DD HH')
       AND timestamp <= TO_TIMESTAMP('2019-06-02 23', 'YYYY-MM-DD HH')
GROUP  BY Day, Hour
ORDER  BY Hour;
```

Al ejecutar la consulta modificada, se almacenan los resultados en `hourly_actions_date_range` como un marco de datos. Ejecute la siguiente función en una nueva celda para previsualizar los resultados:

```python
hourly_actions_date_rage.head()
```

### Número de eventos por sesión de visitante {#number-of-events-per-visitor-session}

La siguiente consulta devuelve el número de eventos por sesión de visitante para una fecha especificada:

#### Consulta <!-- omit in toc -->

```sql
%%read_sql events_per_session -c QS_CONNECTION
SELECT concat(enduserids._experience.aaid.id, 
              '-#', 
              _experience.analytics.session.num) AS aaid_sess_key, 
       Count(timestamp)                          AS Count 
FROM   {target_table}
WHERE TIMESTAMP = to_timestamp('{target_year}-{target_month}-{target_day}')
GROUP BY aaid_sess_key
ORDER BY Count DESC;
```

Ejecute lo siguiente [!DNL Python] código para generar un histograma del número de eventos por sesión de visita:

```python
data = [go.Histogram(x = events_per_session['Count'])]

layout = go.Layout(
    title = 'Histogram of Number of Events per Visit Session',
    xaxis = dict(title = 'Number of Events'),
    yaxis = dict(title = 'Count')
)

fig = go.Figure(data = data, layout = layout)
iplot(fig)
```

### Páginas populares para un día determinado {#popular-pages-for-a-given-day}

La siguiente consulta devuelve las diez páginas más populares para una fecha especificada:

#### Consulta <!-- omit in toc -->

```sql
%%read_sql popular_pages -c QS_CONNECTION
SELECT web.webpagedetails.name                 AS Page_Name, 
       Sum(web.webpagedetails.pageviews.value) AS Page_Views 
FROM   {target_table}
WHERE TIMESTAMP = to_timestamp('{target_year}-{target_month}-{target_day}')
GROUP  BY web.webpagedetails.name 
ORDER  BY page_views DESC 
LIMIT  10;
```

### Usuarios activos durante un día determinado {#active-users-for-a-given-day}

La siguiente consulta devuelve los diez usuarios más activos para una fecha especificada:

#### Consulta <!-- omit in toc -->

```sql
%%read_sql active_users -c QS_CONNECTION
SELECT enduserids._experience.aaid.id AS aaid, 
       Count(timestamp)               AS Count
FROM   {target_table}
WHERE TIMESTAMP = to_timestamp('{target_year}-{target_month}-{target_day}')
GROUP  BY aaid
ORDER  BY Count DESC
LIMIT  10;
```

### Ciudades activas por actividad de usuario {#active-cities-by-user-activity}

La siguiente consulta devuelve las diez ciudades que están generando la mayoría de las actividades de usuario para una fecha especificada:

#### Consulta <!-- omit in toc -->

```sql
%%read_sql active_cities -c QS_CONNECTION
SELECT concat(placeContext.geo.stateProvince, ' - ', placeContext.geo.city) AS state_city, 
       Count(timestamp)                                                     AS Count
FROM   {target_table}
WHERE TIMESTAMP = to_timestamp('{target_year}-{target_month}-{target_day}')
GROUP  BY state_city
ORDER  BY Count DESC
LIMIT  10;
```

## Pasos siguientes

Este tutorial muestra algunos casos de uso de muestra para utilizar [!DNL Query Service] in [!DNL Jupyter] cuadernos. Siga las [Analice sus datos con Jupyter Notebooks](./analyze-your-data.md) tutorial para ver cómo se realizan operaciones similares mediante el SDK de acceso a datos.
