---
keywords: Experience Platform;JupyterLab;blocs de notas;Data Science Workspace;temas populares;jupyterlab
solution: Experience Platform
title: Información general de JupyterLab
description: JupyterLab es una interfaz de usuario basada en web para el proyecto Jupyter y está totalmente integrada en Adobe Experience Platform. Proporciona un entorno de desarrollo interactivo para que los científicos de datos trabajen con Jupyter Notebooks, código y datos. Este documento proporciona información general sobre JupyterLab y sus funciones, así como instrucciones para realizar acciones comunes.
exl-id: 13786fbd-ef16-49cd-8bcf-46320c33e902
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1838'
ht-degree: 2%

---

# [!DNL JupyterLab] Información general de IU

>[!NOTE]
>
>Data Science Workspace ya no se puede adquirir.
>
>Esta documentación está destinada a clientes existentes con derechos anteriores a Data Science Workspace.

[!DNL JupyterLab] es una interfaz de usuario basada en la web para [Project Jupyter](https://jupyter.org/) y está totalmente integrada en Adobe Experience Platform. Proporciona un entorno de desarrollo interactivo para que los científicos de datos trabajen con Jupyter Notebooks, código y datos.

Este documento proporciona información general sobre [!DNL JupyterLab] y sus características, así como instrucciones para realizar acciones comunes.

## [!DNL JupyterLab] el [!DNL Experience Platform]

La integración de JupyterLab de Experience Platform se acompaña de cambios de arquitectura, consideraciones de diseño, extensiones de portátiles personalizadas, bibliotecas preinstaladas y una interfaz temática de Adobe.

La siguiente lista describe algunas de las funciones exclusivas de JupyterLab en Experience Platform:

| Función | Descripción |
| --- | --- |
| **Núcleos** | Los núcleos proporcionan al bloc de notas y a otros [!DNL JupyterLab] front-end la capacidad de ejecutar e inspeccionar código en diferentes lenguajes de programación. [!DNL Experience Platform] proporciona núcleos adicionales para admitir el desarrollo en [!DNL Python], R, PySpark y [!DNL Spark]. Consulte la sección [kernels](#kernels) para obtener más información. |
| **Acceso a datos** | Obtenga acceso a los conjuntos de datos existentes directamente desde [!DNL JupyterLab], con compatibilidad total con las capacidades de lectura y escritura. |
| **[!DNL Experience Platform]integración de servicio** | Las integraciones integradas le permiten utilizar otros servicios de [!DNL Experience Platform] directamente desde [!DNL JupyterLab]. Se proporciona una lista completa de las integraciones compatibles en la sección sobre [Integración con otros servicios de Experience Platform](#service-integration). |
| **Autenticación** | Además del modelo de seguridad integrado de <a href="https://jupyter-notebook.readthedocs.io/en/stable/security.html" target="_blank">JupyterLab</a>, cada interacción entre su aplicación y Experience Platform, incluida la comunicación entre el servicio y el servicio de Experience Platform, se cifra y se autentica mediante <a href="https://www.adobe.io/authentication/auth-methods.html" target="_blank">[!DNL Adobe Identity Management System] (IMS)</a>. |
| **Bibliotecas de desarrollo** | En [!DNL Experience Platform], [!DNL JupyterLab] proporciona bibliotecas preinstaladas para [!DNL Python], R y PySpark. Consulte el [apéndice](#supported-libraries) para obtener una lista completa de las bibliotecas admitidas. |
| **Controlador de biblioteca** | Cuando faltan las bibliotecas preinstaladas para sus necesidades, se pueden instalar bibliotecas adicionales para Python y R, y se almacenan temporalmente en contenedores aislados para mantener la integridad de [!DNL Experience Platform] y mantener sus datos a salvo. Consulte la sección [kernels](#kernels) para obtener más información. |

>[!NOTE]
>
>Las bibliotecas adicionales solo están disponibles para la sesión en la que se instalaron. Debe volver a instalar las bibliotecas adicionales que necesite al iniciar nuevas sesiones.

## Integración con otros [!DNL Experience Platform] servicios {#service-integration}

La estandarización y la interoperabilidad son conceptos clave detrás de [!DNL Experience Platform]. La integración de [!DNL JupyterLab] en [!DNL Experience Platform] como IDE incrustado le permite interactuar con otros servicios de [!DNL Experience Platform], lo que le permite utilizar [!DNL Experience Platform] todo su potencial. Los siguientes [!DNL Experience Platform] servicios están disponibles en [!DNL JupyterLab]:

* **[!DNL Catalog Service]:** Acceda y explore conjuntos de datos con funcionalidades de lectura y escritura.
* **[!DNL Query Service]:** Acceda y explore conjuntos de datos mediante SQL, lo que reduce los gastos generales de acceso a datos al tratar grandes cantidades de datos.
* **[!DNL Sensei ML Framework]:** Desarrollo de modelos con la capacidad de entrenar y puntuar datos, así como la creación de fórmulas con un solo clic.
* **[!DNL Experience Data Model (XDM)]:** La estandarización y la interoperabilidad son conceptos clave detrás de Adobe Experience Platform. [Modelo de datos de experiencia (XDM)](https://www.adobe.com/go/xdm-home-en), impulsado por Adobe, es un esfuerzo para estandarizar los datos de experiencia del cliente y definir esquemas para la administración de experiencias del cliente.

>[!NOTE]
>
>Algunas integraciones de servicio de [!DNL Experience Platform] en [!DNL JupyterLab] se limitan a núcleos específicos. Consulte la sección sobre [kernels](#kernels) para obtener más información.

## Funciones clave y operaciones comunes

En las secciones siguientes se proporciona información acerca de las características clave de [!DNL JupyterLab] e instrucciones para realizar operaciones comunes:

* [Acceder a JupyterLab](#access-jupyterlab)
* [Interfaz de JupyterLab](#jupyterlab-interface)
* [Celdas de código](#code-cells)
* [Núcleos](#kernels)
* [Sesiones de kernel](#kernel-sessions)
* [Lanzador](#launcher)

### Acceder a [!DNL JupyterLab] {#access-jupyterlab}

En [Adobe Experience Platform](https://platform.adobe.com), seleccione **[!UICONTROL Notebooks]** de la columna de navegación izquierda. Espere un tiempo para que [!DNL JupyterLab] se inicialice por completo.

![](../images/jupyterlab/user-guide/access_jupyterlab.png)

### Interfaz de [!DNL JupyterLab] {#jupyterlab-interface}

La interfaz [!DNL JupyterLab] consta de una barra de menús, una barra lateral izquierda contraíble y el área de trabajo principal que contiene fichas de documentos y actividades.

**Barra de menús**

La barra de menús de la parte superior de la interfaz tiene menús de nivel superior que exponen acciones disponibles en [!DNL JupyterLab] con sus métodos abreviados de teclado:

* **Archivo:** Acciones relacionadas con archivos y directorios
* **Editar:** acciones relacionadas con la edición de documentos y otras actividades
* **Ver:** acciones que modifican el aspecto de [!DNL JupyterLab]
* **Ejecutar:** Acciones para ejecutar código en diferentes actividades como blocs de notas y consolas de códigos
* **Núcleo:** acciones para administrar núcleos
* **Fichas:** Una lista de documentos y actividades abiertos
* **Configuración:** Configuración común y un editor de configuración avanzada
* **Ayuda:** Una lista de [!DNL JupyterLab] y vínculos de ayuda del núcleo

**Barra lateral izquierda**

La barra lateral izquierda contiene pestañas en las que se puede hacer clic y que proporcionan acceso a las siguientes funciones:

* **Explorador de archivos:** Lista de documentos y directorios guardados del bloc de notas
* **Explorador de datos:** Examine, acceda y explore conjuntos de datos y esquemas
* **Ejecución de kernels y terminales:** Una lista de sesiones activas de kernel y terminal con la capacidad de finalizar
* **Comandos:** Una lista de comandos útiles
* **Inspector de celdas:** Editor de celdas que proporciona acceso a herramientas y metadatos útiles para configurar un bloc de notas con fines de presentación
* **fichas:** Una lista de fichas abiertas

Seleccione una pestaña para exponer sus funciones o seleccione en una pestaña expandida para contraer la barra lateral izquierda como se muestra a continuación:

![](../images/jupyterlab/user-guide/left_sidebar_collapse.gif)

**Área de trabajo principal**

El área de trabajo principal de [!DNL JupyterLab] le permite organizar documentos y otras actividades en paneles de fichas que se pueden cambiar de tamaño o subdividir. Arrastre una pestaña al centro de un panel de pestañas para migrar la pestaña. Divida un panel arrastrando una pestaña a la izquierda, a la derecha, a la parte superior o a la parte inferior del panel:

![](../images/jupyterlab/user-guide/main_work_area.gif)

### Configuración de GPU y servidor de memoria en [!DNL Python]/R

En [!DNL JupyterLab], seleccione el icono de engranaje en la esquina superior derecha para abrir *Configuración del servidor de portátiles*. Puede activar la GPU y asignar la cantidad de memoria que necesite mediante el control deslizante. La cantidad de memoria que puede asignar depende de la cantidad que haya aprovisionado su organización. Seleccione **[!UICONTROL Actualizar configuraciones]** para guardar.

>[!NOTE]
>
>Solo se proporciona una GPU por organización para Notebooks. Si la GPU está en uso, tendrá que esperar a que la libere el usuario que la ha reservado actualmente. Esto se puede hacer cerrando la sesión o dejando la GPU en estado inactivo durante cuatro horas o más.

![](../images/jupyterlab/user-guide/notebook-gpu-config.png)

### Terminar y reiniciar [!DNL JupyterLab]

En [!DNL JupyterLab], puede finalizar su sesión para evitar que se usen más recursos. Comience por seleccionar el **icono de energía** ![icono de energía](/help/images/icons/power.png) y, a continuación, seleccione **[!UICONTROL Apagar]** de la ventana emergente que aparece para finalizar su sesión. Las sesiones de Notebook finalizan automáticamente después de 12 horas de inactividad.

Para reiniciar [!DNL JupyterLab], selecciona el **icono de reinicio** ![icono de reinicio](/help/images/icons/restart.png) que se encuentra directamente a la izquierda del icono de encendido y, a continuación, selecciona **[!UICONTROL Reiniciar]** de la ventana emergente que aparece.

![finalizar jupyterlab](../images/jupyterlab/user-guide/shutdown-jupyterlab.gif)

### Celdas de código {#code-cells}

Las celdas de código son el contenido principal de los blocs de notas. Contienen código fuente en el idioma del núcleo asociado del bloc de notas y la salida como resultado de la ejecución de la celda de código. Se muestra un recuento de ejecución a la derecha de cada celda de código que representa su orden de ejecución.

![](../images/jupyterlab/user-guide/code_cell.png)

Las acciones celulares comunes se describen a continuación:

* **Agregar una celda:** Haga clic en el símbolo más (**+**) del menú del bloc de notas para agregar una celda vacía. Las nuevas celdas se colocan debajo de la celda con la que se está interactuando actualmente, o al final del bloc de notas si no hay ninguna celda en particular enfocada.

* **Mover una celda:** Coloque el cursor a la derecha de la celda que desea mover y, a continuación, haga clic y arrastre la celda a una nueva ubicación. Además, al mover una celda de un bloc de notas a otro se replica la celda junto con su contenido.

* **Ejecutar una celda:** Haga clic en el cuerpo de la celda que desea ejecutar y, a continuación, haga clic en el icono **reproducir** (**▶**) del menú del bloc de notas. Se muestra un asterisco (**\***) en el contador de ejecución de la celda cuando el núcleo está procesando la ejecución y se reemplaza con un entero al finalizar.

* **Eliminar una celda:** Haga clic en el cuerpo de la celda que desea eliminar y, a continuación, haga clic en el icono **tijera**.

### Núcleos {#kernels}

Los núcleos de los portátiles son los motores informáticos específicos del idioma para el procesamiento de las celdas de los portátiles. Además de [!DNL Python], [!DNL JupyterLab] proporciona compatibilidad con idiomas adicional en R, PySpark y [!DNL Spark] (Scala). Al abrir un documento de bloc de notas, se inicia el núcleo asociado. Cuando se ejecuta una celda de cuaderno, el núcleo realiza el cálculo y produce resultados que pueden consumir recursos significativos de memoria y CPU. Tenga en cuenta que la memoria asignada no se libera hasta que se apaga el núcleo.

Ciertas características y funcionalidades están limitadas a núcleos particulares como se describe en la tabla siguiente:

| Núcleo | Compatibilidad con instalación de biblioteca | Integraciones de [!DNL Experience Platform] |
| :----: | :--------------------------: | :-------------------- |
| **[!DNL Python]** | Sí | <ul><li>[!DNL Sensei ML Framework]</li><li>[!DNL Catalog Service]</li><li>[!DNL Query Service]</li></ul> |
| **R** | Sí | <ul><li>[!DNL Sensei ML Framework]</li><li>[!DNL Catalog Service]</li></ul> |
| **Scala** | No | <ul><li>[!DNL Sensei ML Framework]</li><li>[!DNL Catalog Service]</li></ul> |

### Sesiones de kernel {#kernel-sessions}

Cada bloc de notas o actividad activa en [!DNL JupyterLab] utiliza una sesión del núcleo. Para encontrar todas las sesiones activas, expanda la pestaña **Terminales y núcleos en ejecución** de la barra lateral izquierda. El tipo y el estado del núcleo de un portátil se pueden identificar observando la parte superior derecha de la interfaz del portátil. En el diagrama siguiente, el núcleo asociado del bloc de notas es **[!DNL Python]3** y su estado actual está representado por un círculo gris a la derecha. Un círculo hueco implica un núcleo inactivo y un círculo sólido implica un núcleo ocupado.

![](../images/jupyterlab/user-guide/kernel_and_state_1.png)

Si el núcleo está apagado o inactivo durante un período prolongado, entonces **No hay núcleo.** se muestra con un círculo sólido. Active un núcleo haciendo clic en el estado del núcleo y seleccionando el tipo de núcleo apropiado como se muestra a continuación:

![](../images/jupyterlab/user-guide/switch_kernel.gif)

### Lanzador {#launcher}

[//]: # (Talk about the different Notebooks, introduce that certain starter notebooks are limited to particular kernels)

El *lanzador* personalizado le proporciona plantillas de bloc de notas útiles para los núcleos compatibles que le ayudarán a iniciar su tarea, entre las que se incluyen:

| Plantilla | Descripción |
| --- | --- |
| Vacío | Un archivo de bloc de notas vacío. |
| Starter | Un bloc de notas precargado que muestra la exploración de datos con datos de ejemplo. |
| Ventas minoristas | Un bloc de notas precargado con la [fórmula de venta minorista](../pre-built-recipes/retail-sales.md) y datos de ejemplo. |
| Generador de fórmulas | Plantilla de bloc de notas para crear una fórmula en [!DNL JupyterLab]. Está rellenado previamente con código y comentarios que muestran y describen el proceso de creación de la fórmula. Consulte el [bloc de notas para ver el tutorial de fórmulas](https://www.adobe.com/go/data-science-create-recipe-notebook-tutorial-en) para obtener un tutorial detallado. |
| [!DNL Query Service] | Un bloc de notas precargado que muestra el uso de [!DNL Query Service] directamente en [!DNL JupyterLab] con flujos de trabajo de ejemplo proporcionados que analizan los datos a escala. |
| Eventos de XDM | Un bloc de notas precargado que muestra la exploración de datos en datos de evento de experiencia de valor posterior, centrándose en las funciones comunes en toda la estructura de datos. |
| Consultas de XDM | Un portátil precargado que muestra ejemplos de consultas empresariales sobre los datos de Experience Event. |
| Agregación | Un portátil precargado que muestra flujos de trabajo de ejemplo para acumular grandes cantidades de datos en fragmentos más pequeños y manejables. |
| Clúster | Un bloc de notas precargado que muestra el proceso completo de modelado de aprendizaje automático mediante algoritmos de agrupación en clúster. |

Algunas plantillas de bloc de notas están limitadas a determinados núcleos. La disponibilidad de la plantilla para cada núcleo se asigna en la siguiente tabla:

<table>
    <tr>
        <td></td>
        <th><strong>Vacío</strong></th>
        <th><strong>Starter</strong></th>
        <th><strong>Ventas minoristas</strong></th>
        <th><strong>Generador de fórmulas</strong></th>
        <th><strong>[!DNL Query Service]</strong></th>
        <th><strong>Eventos de XDM</strong></th>
        <th><strong>Consultas de XDM</strong></th>
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

Para abrir un nuevo *lanzador*, haz clic en **Archivo > Nuevo lanzador**. También puede expandir **Explorador de archivos** desde la barra lateral izquierda y hacer clic en el símbolo de suma (**+**):

![](../images/jupyterlab/user-guide/new_launcher.gif)

## Pasos siguientes

Para obtener más información sobre cada uno de los blocs de notas compatibles y cómo utilizarlos, visite la guía para desarrolladores de [acceso a datos de los blocs de notas de Jupyterlab](./access-notebook-data.md). Esta guía se centra en cómo utilizar cuadernos de JupyterLab para acceder a sus datos, incluidos los datos de lectura, escritura y consulta. La guía de acceso a datos también contiene información sobre la cantidad máxima de datos que puede leer cada bloc de notas compatible.

## Bibliotecas compatibles {#supported-libraries}

Para obtener una lista de los paquetes admitidos en Python, R y PySpark, copie y pegue `!conda list` en una celda nueva y, a continuación, ejecute la celda. Una lista de paquetes admitidos se rellena en orden alfabético.

![ejemplo](../images/jupyterlab/user-guide/libraries.PNG)

Además, se utilizan las siguientes dependencias, pero no se enumeran:
* CUDA 11.2
* CUDNN 8.1

