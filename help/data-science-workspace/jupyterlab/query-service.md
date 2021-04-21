---
keywords: Experience Platform;JupyterLab;blocs de notas;Data Science Workspace;temas populares;servicio de consultas
solution: Experience Platform
title: Servicio de consultas en el bloc de notas de Jupyter
topic-legacy: tutorial
type: Tutorial
description: Adobe Experience Platform le permite utilizar el lenguaje de consulta estructurado (SQL) en Data Science Workspace mediante la integración del servicio de consulta en JupyterLab como función estándar. Este tutorial muestra consultas SQL de ejemplo para casos de uso comunes para explorar, transformar y analizar datos de Adobe Analytics.
exl-id: c5ac7d11-a3bd-4ef8-a650-9f496a8bbaa7
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '810'
ht-degree: 1%

---

# Servicio de consultas en el bloc de notas de Jupyter

[!DNL Adobe Experience Platform] permite utilizar el lenguaje de consulta estructurado (SQL) en  [!DNL Data Science Workspace] integrándolo  [!DNL Query Service] en  [!DNL JupyterLab] como función estándar.

Este tutorial muestra consultas SQL de ejemplo para casos de uso comunes para explorar, transformar y analizar datos [!DNL Adobe Analytics].

## Primeros pasos

Antes de iniciar este tutorial, debe tener los siguientes requisitos previos:

- Acceso a [!DNL Adobe Experience Platform]. Si no tiene acceso a una organización de IMS en [!DNL Experience Platform], póngase en contacto con el administrador del sistema antes de continuar

- Un conjunto de datos [!DNL Adobe Analytics]

- Una explicación práctica de los siguientes conceptos clave utilizados en este tutorial:
   - [[!DNL Experience Data Model (XDM) and XDM System]](../../xdm/home.md)
   - [[!DNL Query Service]](../../query-service/home.md)
   - [[!DNL Query Service SQL Syntax]](../../query-service/sql/overview.md)
   - Adobe Analytics

## Acceso [!DNL JupyterLab] y [!DNL Query Service] {#access-jupyterlab-and-query-service}

1. En [[!DNL Experience Platform]](https://platform.adobe.com), vaya a **[!UICONTROL Notebooks]** desde la columna de navegación izquierda. Espere un momento para que JupyterLab se cargue.

   ![](../images/jupyterlab/query/jupyterlab-launcher.png)

   >[!NOTE]
   >
   >Si no aparece automáticamente una nueva ficha Iniciador, abra una nueva ficha Iniciador haciendo clic en **[!UICONTROL File]** y seleccione **[!UICONTROL New Launcher]**.

2. En la ficha Iniciador , haga clic en el icono **[!UICONTROL Blank]** de un entorno de Python 3 para abrir un bloc de notas vacío.

   ![](../images/jupyterlab/query/blank_notebook.png)

   >[!NOTE]
   >
   >Actualmente, Python 3 es el único entorno compatible con Query Service en portátiles.

3. En el carril de selección de la izquierda, haga clic en el icono **[!UICONTROL Data]** y haga doble clic en el directorio **[!UICONTROL Datasets]** para enumerar todos los conjuntos de datos.

   ![](../images/jupyterlab/query/dataset.png)

4. Busque un conjunto de datos [!DNL Adobe Analytics] para explorar y haga clic con el botón derecho en la lista, haga clic en **[!UICONTROL Query Data in Notebook]** para generar consultas SQL en el bloc de notas vacío.

5. Haga clic en la primera celda generada que contenga la función `qs_connect()` y ejecútela haciendo clic en el botón de reproducción. Esta función crea una conexión entre la instancia del bloc de notas y [!DNL Query Service].

   ![](../images/jupyterlab/query/execute.png)

6. Copie el nombre del conjunto de datos [!DNL Adobe Analytics] desde la segunda consulta SQL generada, será el valor después de `FROM`.

   ![](../images/jupyterlab/query/dataset_name.png)

7. Inserte una nueva celda del bloc de notas haciendo clic en el botón **+**.

   ![](../images/jupyterlab/query/insert_cell.gif)

8. Copie, pegue y ejecute las siguientes instrucciones de importación en una celda nueva. Estas instrucciones se utilizarán para visualizar los datos:

   ```python
   import plotly.plotly as py
   import plotly.graph_objs as go
   from plotly.offline import iplot
   ```

9. A continuación, copie y pegue las siguientes variables en una celda nueva. Modifique sus valores según sea necesario y luego ejecútelos.

   ```python
   target_table = "your Adobe Analytics dataset name"
   target_year = "2019"
   target_month = "04"
   target_day = "01"
   ```

   - `target_table` : Nombre del  [!DNL Adobe Analytics] conjunto de datos.
   - `target_year` : Año específico desde el que se obtiene el objetivo.
   - `target_month` : Mes específico desde el que proviene el objetivo.
   - `target_day` : Día específico desde el que se generan los datos de destinatario.

   >[!NOTE]
   >
   >Puede cambiar estos valores en cualquier momento. Al hacerlo, asegúrese de ejecutar la celda de variables para que se apliquen los cambios.

## Consulte sus datos {#query-your-data}

Introduzca las siguientes consultas SQL en celdas de bloc de notas individuales. Ejecute una consulta seleccionando en su celda seguido del botón **[!UICONTROL play]**. Los resultados de consulta o los registros de errores se muestran debajo de la celda ejecutada.

Cuando un bloc de notas está inactivo durante un período prolongado de tiempo, la conexión entre el bloc de notas y [!DNL Query Service] puede romperse. En estos casos, reinicie [!DNL JupyterLab] seleccionando el botón **Restart** ![restart button](../images/jupyterlab/user-guide/restart_button.png) situado en la esquina superior derecha junto al botón de encendido.

El núcleo del bloc de notas se restablece pero las celdas permanecerán, vuelva a ejecutar todas las celdas para continuar donde lo dejó.

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

En la consulta anterior, la marca de tiempo de la cláusula `WHERE` está configurada para ser el valor de `target_year`. Incluya variables en consultas SQL al contenerlas entre llaves (`{}`).

La primera línea de la consulta contiene la variable opcional `hourly_visitor`. Los resultados de la consulta se almacenan en esta variable como un dataframe de Pandas. El almacenamiento de resultados en un dataframe permite visualizar posteriormente los resultados de la consulta utilizando un paquete [!DNL Python] deseado. Ejecute el siguiente código [!DNL Python] en una nueva celda para generar un gráfico de barras:

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

Al ejecutar la consulta anterior, los resultados se almacenarán en `hourly_actions` como un nombre de datos. Ejecute la siguiente función en una celda nueva para obtener una vista previa de los resultados:

```python
hourly_actions.head()
```

La consulta anterior se puede modificar para devolver el recuento de acciones por hora para un intervalo de fechas especificado mediante operadores lógicos en la cláusula **WHERE**:

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

Al ejecutar la consulta modificada, se almacenan los resultados en `hourly_actions_date_range` como un nombre de datos. Ejecute la siguiente función en una celda nueva para obtener una vista previa de los resultados:

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

Ejecute el siguiente código [!DNL Python] para generar un histograma del número de eventos por sesión de visita:

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

### Páginas populares de un día determinado {#popular-pages-for-a-given-day}

La siguiente consulta devuelve las diez páginas más populares de una fecha especificada:

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

### Usuarios activos para un día determinado {#active-users-for-a-given-day}

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

### Ciudades activas por actividad del usuario {#active-cities-by-user-activity}

La siguiente consulta devuelve las diez ciudades que generan la mayoría de las actividades del usuario para una fecha especificada:

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

Este tutorial demostró algunos casos de uso de muestra para utilizar [!DNL Query Service] en los [!DNL Jupyter] blocs de notas. Siga el tutorial [Analice los datos con Jupyter Notebooks](./analyze-your-data.md) para ver cómo se realizan operaciones similares utilizando el SDK de acceso a datos.
