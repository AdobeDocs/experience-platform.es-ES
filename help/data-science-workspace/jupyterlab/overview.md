---
keywords: Experience Platform;JupyterLab;blocs de notas;Área de trabajo de ciencia de datos;temas populares;jupyterlab
solution: Experience Platform
title: Descripción general de la interfaz de usuario de JupyterLab
topic: Overview
description: JupyterLab es una interfaz de usuario basada en web para Project Jupyter y está estrechamente integrada en Adobe Experience Platform. Proporciona un entorno de desarrollo interactivo para que los científicos de datos trabajen con portátiles Jupyter, código y datos. Este documento proporciona información general sobre JupyterLab y sus características, así como instrucciones para realizar acciones comunes.
translation-type: tm+mt
source-git-commit: 698639d6c2f7897f0eb4cce2a1f265a0f7bb57c9
workflow-type: tm+mt
source-wordcount: '1950'
ht-degree: 9%

---


# [!DNL JupyterLab] Información general de la interfaz de usuario

[!DNL JupyterLab] es una interfaz de usuario basada en web para  [Project ](https://jupyter.org/) Jupyterand, y está estrechamente integrada en Adobe Experience Platform. Proporciona un entorno de desarrollo interactivo para que los científicos de datos trabajen con portátiles Jupyter, código y datos.

Este documento proporciona información general sobre [!DNL JupyterLab] y sus características, así como instrucciones para realizar acciones comunes.

## [!DNL JupyterLab] en [!DNL Experience Platform]

La integración de JupyterLab de Experience Platform va acompañada de cambios arquitectónicos, consideraciones de diseño, extensiones personalizadas de portátiles, bibliotecas preinstaladas y una interfaz temática de Adobe.

La siguiente lista describe algunas de las características exclusivas de JupyterLab en la plataforma:

| Función | Descripción |
| --- | --- |
| **Kernels** | Los kernels proporcionan al portátil y otros [!DNL JupyterLab] front-end la capacidad de ejecutar e introducir código en diferentes lenguajes de programación. [!DNL Experience Platform] proporciona núcleos adicionales para admitir el desarrollo en  [!DNL Python], R, PySpark y  [!DNL Spark]. Consulte la sección [kernels](#kernels) para obtener más detalles. |
| **Acceso a datos** | Obtenga acceso a los datasets existentes directamente desde [!DNL JupyterLab] con soporte completo para capacidades de lectura y escritura. |
| **[!DNL Platform]integración de servicios** | Las integraciones integradas le permiten utilizar otros [!DNL Platform] servicios directamente desde [!DNL JupyterLab]. En la sección sobre [Integración con otros servicios de la plataforma](#service-integration) se proporciona una lista completa de las integraciones admitidas. |
| **Autenticación** | Además del <a href="https://jupyter-notebook.readthedocs.io/en/latest/security.html" target="_blank">modelo de seguridad integrado de JupyterLab</a>, todas las interacciones entre la aplicación y el Experience Platform, incluida la comunicación de servicio a servicio de la plataforma, se cifran y autentican mediante <a href="https://www.adobe.io/authentication/auth-methods.html" target="_blank">[!DNL Adobe Identity Management System] (IMS)</a>. |
| **Bibliotecas de desarrollo** | En [!DNL Experience Platform], [!DNL JupyterLab] proporciona bibliotecas preinstaladas para [!DNL Python], R y PySpark. Consulte el [apéndice](#supported-libraries) para obtener una lista completa de las bibliotecas admitidas. |
| **Controlador de biblioteca** | Cuando las bibliotecas preinstaladas no están disponibles para sus necesidades, se pueden instalar bibliotecas adicionales para Python y R, y se almacenan temporalmente en contenedores aislados para mantener la integridad de [!DNL Platform] y mantener los datos seguros. Consulte la sección [kernels](#kernels) para obtener más detalles. |

>[!NOTE]
>
>Las bibliotecas adicionales solo están disponibles para la sesión en la que se instalaron. Debe reinstalar las bibliotecas adicionales que necesite al iniciar sesiones nuevas.

## Integración con otros [!DNL Platform] servicios {#service-integration}

La estandarización y la interoperabilidad son conceptos clave que sustentan [!DNL Experience Platform]. La integración de [!DNL JupyterLab] en [!DNL Platform] como un IDE integrado le permite interactuar con otros [!DNL Platform] servicios, lo que le permite utilizar [!DNL Platform] todo su potencial. Los siguientes [!DNL Platform] servicios están disponibles en [!DNL JupyterLab]:

* **[!DNL Catalog Service]:** Acceda y explore conjuntos de datos con funcionalidades de lectura y escritura.
* **[!DNL Query Service]:** Acceda y explore conjuntos de datos mediante SQL, proporcionando un acceso a los datos más bajo en los costes generales cuando se trata de grandes cantidades de datos.
* **[!DNL Sensei ML Framework]:Desarrollo** de modelos con la capacidad de entrenar y anotar datos, así como creación de fórmulas con un solo clic.
* **[!DNL Experience Data Model (XDM)]:** La estandarización y la interoperabilidad son conceptos clave detrás de Adobe Experience Platform. [El modelo de datos de experiencia (XDM)](https://www.adobe.com/go/xdm-home-en), impulsado por el Adobe, es un esfuerzo para estandarizar los datos de experiencia del cliente y definir esquemas para la administración de la experiencia del cliente.

>[!NOTE]
>
>Algunas [!DNL Platform] integraciones de servicio en [!DNL JupyterLab] están limitadas a núcleos específicos. Consulte la sección sobre [núcleos](#kernels) para obtener más detalles.

## Funciones clave y operaciones comunes

En las secciones siguientes se proporciona información sobre las características clave de [!DNL JupyterLab] y las instrucciones para realizar operaciones comunes:

* [Access JupyterLab](#access-jupyterlab)
* [Interfaz JupyterLab](#jupyterlab-interface)
* [Celdas de código](#code-cells)
* [Kernels](#kernels)
* [Sesiones de núcleo](#kernel-sessions)
* [Iniciador](#launcher)

### Acceso [!DNL JupyterLab] {#access-jupyterlab}

En [Adobe Experience Platform](https://platform.adobe.com), seleccione **Equipos portátiles** en la columna de navegación izquierda. Deje que [!DNL JupyterLab] se inicialice completamente.

![](../images/jupyterlab/user-guide/access_jupyterlab.png)

### [!DNL JupyterLab] interfaz {#jupyterlab-interface}

La interfaz [!DNL JupyterLab] consta de una barra de menús, una barra lateral izquierda contraíble y el área de trabajo principal que contiene fichas de documentos y actividades.

**Barra de menús**

La barra de menús situada en la parte superior de la interfaz tiene menús de nivel superior que exponen las acciones disponibles en [!DNL JupyterLab] con sus métodos abreviados de teclado:

* **Archivo:** Acciones relacionadas con archivos y directorios
* **Editar:** Acciones relacionadas con la edición de documentos y otras actividades
* **Vista:** Acciones que modifican el aspecto de  [!DNL JupyterLab]
* **Ejecutar:** acciones para ejecutar código en diferentes actividades, como blocs de notas y consolas de código
* **Núcleo:** Acciones para administrar núcleos
* **Fichas:** Una lista de documentos y actividades abiertos
* **Configuración:configuración** común y un editor de configuración avanzada
* **Ayuda:** Una lista de vínculos de ayuda  [!DNL JupyterLab] y del núcleo

**Barra lateral izquierda**

La barra lateral izquierda contiene fichas en las que se puede hacer clic que proporcionan acceso a las siguientes funciones:

* **Navegador de archivos:** lista de documentos y directorios de portátiles guardados
* **Explorador de datos:** Examinar, acceder y explorar conjuntos de datos y esquemas
* **Kernels en funcionamiento y terminales:** una lista de sesiones activas de kernel y terminal con la capacidad de finalizar
* **Comandos:** lista de comandos útiles
* **Inspector de celdas:** editor de celdas que proporciona acceso a herramientas y metadatos útiles para configurar un bloc de notas con fines de presentación
* **fichas:** Una lista de fichas abiertas

Haga clic en una ficha para exponer sus funciones o haga clic en una ficha expandida para contraer la barra lateral izquierda como se muestra a continuación:

![](../images/jupyterlab/user-guide/left_sidebar_collapse.gif)

**Área de trabajo principal**

El área de trabajo principal de [!DNL JupyterLab] le permite organizar documentos y otras actividades en paneles de fichas que se pueden cambiar de tamaño o subdividir. Arrastre una ficha al centro de un panel de fichas para migrarla. Para dividir un panel, arrastre una ficha a la izquierda, a la derecha, a la parte superior o a la parte inferior del panel:

![](../images/jupyterlab/user-guide/main_work_area.gif)

### Celdas de código {#code-cells}

Las celdas de código son el contenido principal de los blocs de notas. Contienen código fuente en el idioma del núcleo asociado al bloc de notas y la salida como resultado de la ejecución de la celda de código. Se muestra un recuento de ejecución a la derecha de cada celda de código que representa su orden de ejecución.

![](../images/jupyterlab/user-guide/code_cell.png)

Las acciones comunes de las células se describen a continuación:

* **Añadir una celda:** haga clic en el símbolo más (**+**) del menú del bloc de notas para agregar una celda vacía. Las celdas nuevas se colocan debajo de la celda con la que se está interactuando o al final del bloc de notas si no hay ninguna celda en particular enfocada.

* **Mover una celda:** coloque el cursor a la derecha de la celda que desee mover y, a continuación, haga clic y arrastre la celda a una nueva ubicación. Además, al mover una celda de un bloc de notas a otro se replica la celda junto con su contenido.

* **Ejecutar una celda:** haga clic en el cuerpo de la celda que desee ejecutar y, a continuación, haga clic en el  **** icono de reproducción (**▶**) en el menú del bloc de notas. Se muestra un asterisco (**\***) en el contador de ejecución de la celda cuando el núcleo está procesando la ejecución y se reemplaza por un entero al finalizar.

* **Eliminar una celda:** haga clic en el cuerpo de la celda que desee eliminar y, a continuación, haga clic en el icono de  **** tijera.

### Kernels {#kernels}

Los núcleos de los portátiles son los motores informáticos específicos del idioma para procesar las celdas de los portátiles. Además de [!DNL Python], [!DNL JupyterLab] proporciona soporte de idioma adicional en R, PySpark y [!DNL Spark] (Scala). Al abrir un documento portátil, se inicia el núcleo asociado. Cuando se ejecuta una celda portátil, el núcleo realiza el cálculo y produce resultados que pueden consumir recursos significativos de CPU y memoria. Tenga en cuenta que la memoria asignada no se libera hasta que se cierre el núcleo.

Algunas funciones y características se limitan a determinados núcleos, como se describe en la tabla siguiente:

| Kernel | Compatibilidad con la instalación de la biblioteca | [!DNL Platform] integraciones |
| :----: | :--------------------------: | :-------------------- |
| **[!DNL Python]** | Sí | <ul><li>[!DNL Sensei ML Framework]</li><li>[!DNL Catalog Service]</li><li>[!DNL Query Service]</li></ul> |
| **R** | Sí | <ul><li>[!DNL Sensei ML Framework]</li><li>[!DNL Catalog Service]</li></ul> |
| **Scala** | No | <ul><li>[!DNL Sensei ML Framework]</li><li>[!DNL Catalog Service]</li></ul> |

### Sesiones de núcleo {#kernel-sessions}

Cada portátil o actividad activa en [!DNL JupyterLab] utiliza una sesión del núcleo. Todas las sesiones activas se pueden encontrar expandiendo la ficha **Terminales en ejecución y kernels** desde la barra lateral izquierda. El tipo y estado del núcleo para un portátil se puede identificar observando la parte superior derecha de la interfaz del bloc de notas. En el diagrama siguiente, el núcleo asociado del bloc de notas es **[!DNL Python]3** y su estado actual está representado por un círculo gris a la derecha. Un círculo hueco implica un núcleo de ralentí y un círculo sólido implica un núcleo ocupado.

![](../images/jupyterlab/user-guide/kernel_and_state_1.png)

Si el núcleo está apagado o inactivo durante un período prolongado, entonces **No Kernel!** con un círculo sólido. Active un núcleo haciendo clic en el estado del núcleo y seleccionando el tipo de núcleo apropiado como se muestra a continuación:

![](../images/jupyterlab/user-guide/switch_kernel.gif)

### Iniciador {#launcher}

[//]: # (Talk about the different Notebooks, introduce that certain starter notebooks are limited to particular kernels)

El *iniciador* personalizado le proporciona plantillas de bloc de notas útiles para sus núcleos admitidos a fin de ayudarle a iniciar su tarea, entre las que se incluyen:

| Plantilla | Descripción |
| --- | --- |
| En blanco | Un archivo de bloc de notas vacío. |
| Inicio | Un bloc de notas precargado que muestra la exploración de datos mediante datos de ejemplo. |
| Ventas minoristas | Un bloc de notas precargado que presenta la [fórmula de ventas minoristas](https://adobe.ly/2wOgO3L) usando datos de muestra. |
| Generador de fórmulas | Una plantilla de bloc de notas para crear una fórmula en [!DNL JupyterLab]. Se rellena previamente con código y comentarios que muestran y describen el proceso de creación de fórmulas. Consulte el [bloc de notas para obtener un tutorial de fórmula](https://www.adobe.com/go/data-science-create-recipe-notebook-tutorial-en) para obtener un tutorial detallado. |
| [!DNL Query Service] | Un bloc de notas precargado que muestra el uso de [!DNL Query Service] directamente en [!DNL JupyterLab] con flujos de trabajo de muestra proporcionados que analizan los datos a escala. |
| Eventos XDM | Un bloc de notas precargado que muestra la exploración de datos en datos de Evento de experiencias con valor posterior, centrado en características comunes en la estructura de datos. |
| Consultas XDM | Un bloc de notas precargado que muestra consultas empresariales de muestra sobre los datos de Experience Evento. |
| Agregación | Un bloc de notas precargado que muestra flujos de trabajo de muestra a grandes cantidades acumuladas de datos en trozos más pequeños y manejables. |
| Clustering | Un bloc de notas precargado que muestra el proceso de modelado integral del aprendizaje automático mediante algoritmos de agrupamiento. |

Algunas plantillas de bloc de notas están limitadas a ciertos núcleos. La disponibilidad de plantillas para cada núcleo se asigna en la siguiente tabla:

<table>
    <tr>
        <td></td>
        <th><strong>En blanco</strong></th>
        <th><strong>Inicio</strong></th>
        <th><strong>Ventas minoristas</strong></th>
        <th><strong>Generador de fórmulas</strong></th>
        <th><strong>[!Servicio de Consulta DNL]</strong></th>
        <th><strong>Eventos XDM</strong></th>
        <th><strong>Consultas XDM</strong></th>
        <th><strong>Agregación</strong></th>
        <th><strong>Clúster</strong></th>
    </tr>
    <tr>
        <th><strong>[!DNL Python]</strong></th>
        <td >sí</td>
        <td >sí</td>
        <td >sí</td>
        <td >sí</td>
        <td >sí</td>
        <td >sí</td>
        <td >no</td>
        <td >no</td>
        <td >no</td>
    </tr>
    <tr>
        <th ><strong>R</strong></th>
        <td >sí</td>
        <td >sí</td>
        <td >sí</td>
        <td >no</td>
        <td >no</td>
        <td >no</td>
        <td >no</td>
        <td >no</td>
        <td >no</td>
    </tr>
      <tr>
        <th  ><strong>PySpark 3 ([!DNL Spark] 2.4)</strong></th>
        <td >no</td>
        <td >sí</td>
        <td >no</td>
        <td >no</td>
        <td >no</td>
        <td >no</td>
        <td >sí</td>
        <td >sí</td>
        <td >no</td>
    </tr>
    <tr>
        <th ><strong>Scala</strong></th>
        <td >sí</td>
        <td >sí</td>
        <td >no</td>
        <td >no</td>
        <td >no</td>
        <td >no</td>
        <td >no</td>
        <td >no</td>
        <td >sí</td>
    </tr>
</table>

Para abrir un nuevo *iniciador*, haga clic en **Archivo > Nuevo iniciador**. También puede expandir el **explorador de archivos** desde la barra lateral izquierda y hacer clic en el símbolo más (**+**):

![](../images/jupyterlab/user-guide/new_launcher.gif)

### Configuración de GPU y servidor de memoria en [!DNL Python]/R

En [!DNL JupyterLab] seleccione el icono de engranaje en la esquina superior derecha para abrir la *configuración del servidor de portátiles*. Puede activar la GPU y asignar la cantidad de memoria que necesita con el control deslizante. La cantidad de memoria que puede asignar depende de cuánto haya proporcionado su organización. Seleccione **[!UICONTROL Actualizar configuraciones]** para guardar.

>[!NOTE]
>
>Solo se aprovisiona una GPU por organización para equipos portátiles. Si la GPU está en uso, debe esperar a que el usuario que la haya reservado en ese momento la publique. Esto se puede hacer cerrando la sesión o dejando la GPU en estado inactivo durante cuatro o más horas.

![](../images/jupyterlab/user-guide/notebook-gpu-config.png)

## Pasos siguientes

Para obtener más información sobre cada uno de los blocs de notas admitidos y cómo utilizarlos, visite la [guía para desarrolladores de Acceso a datos de blocs de notas de Jupyterlab](./access-notebook-data.md). Esta guía se centra en cómo utilizar los blocs de notas de JupyterLab para acceder a sus datos, incluida la lectura, escritura y consulta de datos. La guía de acceso a datos también contiene información sobre la cantidad máxima de datos que puede leer cada bloc de notas compatible.

## Bibliotecas admitidas {#supported-libraries}

### [!DNL Python] / R

| Biblioteca | Versión |
| :------ | :------ |
| portátil | 6.0.0 |
| solicitudes | 2.22.0 |
| tríptico | 4.0.0 |
| folium | 0.10.0 |
| ipywidgets | 7.5.1 |
| bokeh | 1.3.1 |
| gensim | 3.7.3 |
| ipyparalelo | 0.5.2 |
| jq | 1,6 |
| keras | 2.2.4 |
| nltk | 3.2.5 |
| pandas | 0.22.0 |
| pandasql | 0,7,3 |
| almohada | 6.0.0 |
| scikit-image | 0.15.0 |
| scikit-learn | 0,21,3 |
| scipy | 1.3.0 |
| scrapy | 1.3.0 |
| seaborn | 0.9.0 |
| modelos de estado | 0.10.1 |
| elástico | 5.1.0.17 |
| gráfico | 0.11.5 |
| py-xgboox | 0,90 |
| opencv | 3.4.1 |
| pyspark | 2.4.3 |
| pytorch | 1.0.1 |
| wxpython | 4.0.6 |
| colorlover | 0.3.0 |
| geopandas | 0.5.1 |
| pyshp | 2.1.0 |
| de forma | 1.6.4 |
| rpy2 | 2.9.4 |
| r-essentials | 3,6 |
| r-arules | 1.6_3 |
| r-fpc | 2.2_3 |
| r-e1071 | 1.7_2 |
| r-gam | 1.16.1 |
| r-gbm | 2.1.5 |
| r-temas | 4.2.0 |
| r-ggvis | 0.4.4 |
| r-igraph | 1.2.4.1 |
| r-saltos | 3,0 |
| volver a manipular | 1.0.1 |
| r-rocr | 1.0_7 |
| r-rmysql | 0.10.17 |
| r-rodbc | 1.3_15 |
| r-rsqlite | 2.1.2 |
| r-rstan | 2.19.2 |
| r-sqldf | 0.4_11 |
| r-supervivencia | 2.44_1.1 |
| r-zoo | 1.8_6 |
| r-stringdist | 0.9.5.2 |
| r-quadprog | 1.5_7 |
| r-rjson | 0,2,20 |
| r-previsión | 8,7 |
| r-resolnp | 1,16 |
| r-reticulate | 1,12 |
| r-mlr | 2.14.0 |
| r-viridis | 0.5.1 |
| r-corplot | 0,84 |
| r-fnn | 1.1.3 |
| r-lubridate | 1.7.4 |
| r-randomforest | 4.6_14 |
| r-tidyverse | 1.2.1 |
| r-tree | 1.0_39 |
| pymongo | 3.8.0 |
| pyarrow | 0.14.1 |
| boto3 | 1.9.1999 |
| ipyvolumen | 0.5.2 |
| fastparquet | 0.3.2 |
| python-sndish | 0,5,4 |
| ipywebrtc | 0.5.0 |
| jupyter_client | 5.3.1 |
| wordcloud | 1.5.0 |
| grafviz | 2.40.1 |
| python-graphviz | 0.11.1 |
| azure-almacenamiento | 0,36,0 |
| [!DNL jupyterlab] | 1.0.4 |
| pandas_ml | 0.6.1 |
| tensorflow-gpu | 1.14.0 |
| nodejs | 12.3.0 |
| mock | 3.0.5 |
| ipympl | 0.3.3 |
| fonts-anacond | 1.0 |
| psicopg2 | 2.8.3 |
| nariz | 1.3.7 |
| autovizwidget | 0.12.9 |
| altair | 3.1.0 |
| vega_datasets | 0.7.0 |
| papermill | 1.0.1 |
| sql_Magic | 0.0.4 |
| iso3166 | 1.0 |
| nbimporter | 0.3.1 |

### PySpark

| Biblioteca | Versión |
| :------ | :------ |
| solicitudes | 2.18.4 |
| gensim | 2.3.0 |
| keras | 2.0.6 |
| nltk | 3.2.4 |
| pandas | 0.20.1 |
| pandasql | 0,7,3 |
| almohada | 5.3.0 |
| scikit-image | 0.13.0 |
| scikit-learn | 0.19.0 |
| scipy | 0.19.1 |
| scrapy | 1.3.3 |
| modelos de estado | 0.8.0 |
| elástico | 4.0.30.44 |
| py-xgboox | 0,60 |
| opencv | 3.1.0 |
| pyarrow | 0.8.0 |
| boto3 | 1.5.18 |
| azure-almacenamiento-blob | 1.4.0 |
| [!DNL python] | 3.6.7 |
| mkl-rt | 11.1 |