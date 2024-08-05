---
keywords: Experience Platform; JupyterLab; Cuadernos; Data Science Espacio de trabajo; temas populares; Jupyterlab
solution: Experience Platform
title: Información general de JupyterLab
description: JupyterLab es una interfaz de usuario basada en web para el proyecto Jupyter y está totalmente integrada en Adobe Experience Platform. Proporciona un entorno de desarrollo interactivo para que los científicos de datos trabajen con Jupyter Notebooks, código y datos. Este documento proporciona información general sobre JupyterLab y sus funciones, así como instrucciones para realizar acciones comunes.
exl-id: 13786fbd-ef16-49cd-8bcf-46320c33e902
source-git-commit: 5d98dc0cbfaf3d17c909464311a33a03ea77f237
workflow-type: tm+mt
source-wordcount: '1835'
ht-degree: 2%

---

# [!DNL JupyterLab] Información general de IU

>[!NOTE]
>
>La Espacio de trabajo de ciencia de datos ya no está disponible para su compra.
>
>Esta documentación está destinada a clientes existentes con derechos previos a Data Science Espacio de trabajo.

[!DNL JupyterLab] es una interfaz de usuario basada en web para [Project Jupyter](https://jupyter.org/) y está estrechamente integrada en Adobe Experience Platform. Proporciona un entorno de desarrollo interactivo para que los científicos de datos trabajen con Jupyter Notebooks, código y datos.

Este documento proporciona información general de [!DNL JupyterLab] sus funciones, así como instrucciones para realizar acciones comunes.

## [!DNL JupyterLab] en [!DNL Experience Platform]

La integración de JupyterLab de Experience Platform se acompaña de cambios arquitectónicos, consideraciones de diseño, extensiones de bloc de notas personalizadas, bibliotecas preinstalados y una interfaz con temas de Adobe Systems.

La siguiente lista describe algunas de las características exclusivas de JupyterLab en Platform:

| Función | Descripción |
| --- | --- |
| **Núcleos** | Los kernels proporcionan a los cuadernos y otros [!DNL JupyterLab] front-ends la capacidad de ejecutar e introspección de código en diferentes lenguajes de programación. [!DNL Experience Platform] proporciona kernels adicionales para admitir el desarrollo en [!DNL Python], R, PySpark y [!DNL Spark]. Consulte la [sección kernels](#kernels) para obtener más detalles. |
| **Acceso a datos** | Obtenga acceso a los conjuntos de datos existentes directamente desde [!DNL JupyterLab], con compatibilidad total con las capacidades de lectura y escritura. |
| **[!DNL Platform]integración de servicio** | Las integraciones integradas le permiten utilizar otros servicios de [!DNL Platform] directamente desde [!DNL JupyterLab]. Se proporciona una lista completa de las integraciones compatibles en la sección sobre [Integración con otros servicios de Platform](#service-integration). |
| **Autenticación** | Además del modelo de seguridad integrado de <a href="https://jupyter-notebook.readthedocs.io/en/stable/security.html" target="_blank">JupyterLab</a>, todas las interacciones entre su aplicación y el Experience Platform, incluida la comunicación de servicio a servicio de Platform, se cifran y se autentican mediante <a href="https://www.adobe.io/authentication/auth-methods.html" target="_blank">[!DNL Adobe Identity Management System] (IMS)</a>. |
| **Bibliotecas de desarrollo** | En [!DNL Experience Platform], [!DNL JupyterLab] proporciona bibliotecas preinstaladas para [!DNL Python], R y PySpark. Consulte el [apéndice](#supported-libraries) para obtener una lista completa de las bibliotecas admitidas. |
| **Controlador de biblioteca** | Cuando faltan los bibliotecas preinstalados para sus necesidades, se pueden instalar bibliotecas adicionales para Python y R, y se almacenan temporalmente en contenedores aislados para mantener la integridad y [!DNL Platform] mantener sus datos seguros. Consulte la sección [kernels](#kernels) para obtener más información. |

>[!NOTE]
>
>Las bibliotecas adicionales solo están disponibles para la sesión en la que se instalaron. Debe volver a instalar las bibliotecas adicionales que necesite al iniciar nuevas sesiones.

## Integración con otros [!DNL Platform] servicios {#service-integration}

La estandarización y la interoperabilidad son conceptos clave detrás de [!DNL Experience Platform]. La integración de [!DNL JupyterLab] en [!DNL Platform] como IDE incrustado le permite interactuar con otros servicios de [!DNL Platform], lo que le permite utilizar [!DNL Platform] todo su potencial. Los siguientes [!DNL Platform] servicios están disponibles en [!DNL JupyterLab]:

* **[!DNL Catalog Service]:** Acceda a conjuntos de datos y explórelos con funcionalidades de lectura y escritura.
* **[!DNL Query Service]:** Acceda y explore conjuntos de datos mediante SQL, lo que proporciona una menor sobrecarga de acceso a los datos cuando se trata de grandes cantidades de datos.
* **[!DNL Sensei ML Framework]:** Desarrollo de modelos con la capacidad de entrenar y puntuar datos, así como fórmula creación con un solo clic.
* **[!DNL Experience Data Model (XDM)]:** La estandarización y la interoperabilidad son conceptos clave detrás de Adobe Experience Platform. [El Modelo de datos de experiencia (XDM),](https://www.adobe.com/go/xdm-home-en) impulsado por Adobe Systems, es un esfuerzo para estandarizar experiencia del cliente datos y definir esquemas para administración de experiencias del cliente.

>[!NOTE]
>
>Algunas [!DNL Platform] integraciones de servicios están [!DNL JupyterLab] limitadas a kernels específicos. Consulte la sección sobre [kernels](#kernels) para obtener más detalles.

## Características clave y operaciones comunes

En las secciones siguientes se proporciona información sobre las características clave y las instrucciones sobre la realización de [!DNL JupyterLab] operaciones comunes:

* [Acceso a JupyterLab](#access-jupyterlab)
* [Interfaz de JupyterLab](#jupyterlab-interface)
* [Code celdas](#code-cells)
* [Núcleos](#kernels)
* [Sesiones de kernel](#kernel-sessions)
* [Lanzadera](#launcher)

### Acceder a [!DNL JupyterLab] {#access-jupyterlab}

En [Adobe Experience Platform](https://platform.adobe.com), seleccione **[!UICONTROL Notebooks]** de la columna de navegación izquierda. Espere un tiempo para que [!DNL JupyterLab] se inicialice por completo.

![](../images/jupyterlab/user-guide/access_jupyterlab.png)

### [!DNL JupyterLab] interfaz {#jupyterlab-interface}

La [!DNL JupyterLab] interfaz consta de una barra de menú, una barra lateral izquierda plegable y el área de trabajo principal que contiene pestañas de documentos y actividades.

**Barra de menús**

La barra de menús en la parte superior de la interfaz tiene menús de nivel superior que exponen las acciones disponibles en [!DNL JupyterLab] con sus métodos abreviados de teclado:

* **Archivo:** Acciones relacionadas con archivos y directorios
* **Editar:** Acciones relacionadas con la edición de documentos y otras actividades
* **Ver:** Acciones que alteran el aspecto de [!DNL JupyterLab]
* **Ejecutar:** acciones para ejecutar código en diferentes actividades, como blocs de notas y consolas de código.
* **Kernel:** Acciones para administrar kernels
* **Fichas:** Una lista de documentos y actividades abiertos
* **Configuración:** Configuración común y un editor de configuración avanzada
* **Ayuda:** Una lista de [!DNL JupyterLab] y vínculos de ayuda del núcleo

**Barra lateral izquierda**

La barra lateral izquierda contiene pestañas en las que se puede hacer clic y que proporcionan acceso a las siguientes funciones:

* **Archivo explorador:** lista de documentos y directorios de blocs de notas guardados
* **Explorador de datos:** Examinar, acceda y explore conjuntos de datos y esquemas
* **Ejecución de kernels y terminales:** Un lista de sesiones activas de kernel y terminal con la capacidad de terminar
* **Comandos:** lista de comandos útiles
* **Inspector de celdas: editor de celda que proporciona acceso a herramientas y metadatos útiles para configurar un bloc de notas con fines de presentación.**
* **pestañas:** lista de pestañas abiertas

Seleccione una pestaña para exponer sus funciones, o seleccione en un pestaña expandido contraer la barra lateral izquierda como se muestra a continuación:

![](../images/jupyterlab/user-guide/left_sidebar_collapse.gif)

**Área de trabajo principal**

El área de trabajo principal le [!DNL JupyterLab] permite organizar documentos y otras actividades en paneles de pestañas que se pueden cambiar de tamaño o subdividir. Arrastre un pestaña al centro de un panel de pestaña para migrar el pestaña. Para dividir un panel, arrastre un pestaña a la izquierda, derecha, parte superior o inferior del panel:

![](../images/jupyterlab/user-guide/main_work_area.gif)

### Configuración de GPU y servidor de memoria en [!DNL Python]/R

En [!DNL JupyterLab] ella, seleccione el icono de engranaje en la esquina superior derecha para abrir *la configuración* del servidor Notebook. Puede activar la GPU y asignar la cantidad de memoria que necesite mediante el control deslizante. La cantidad de memoria que puede asignar depende de la cantidad que haya aprovisionado su organización. Seleccione **[!UICONTROL Actualizar configuraciones]** para guardar.

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

A continuación se describen las acciones de celda comunes:

* **Agregar una celda:** Haga clic en el símbolo más (**+**) del menú del bloc de notas para agregar una celda vacía. Las nuevas celdas se colocan debajo de la celda con la que se está interactuando actualmente, o al final del bloc de notas si no hay ninguna celda en particular enfocada.

* **Mover una celda:** Coloque el cursor a la derecha de la celda que desea mover y, a continuación, haga clic y arrastre la celda a una nueva ubicación. Además, al mover una celda de un bloc de notas a otro se replica la celda junto con su contenido.

* **Ejecutar una celda:** Haga clic en el cuerpo de la celda que desea ejecutar y, a continuación, haga clic en el icono **reproducir** (**▶**) del menú del bloc de notas. Se muestra un asterisco (**\***) en el contador de ejecución de la celda cuando el núcleo está procesando la ejecución y se reemplaza con un entero al finalizar.

* **Eliminar una celda:** Haga clic en el cuerpo de la celda que desea eliminar y, a continuación, haga clic en el icono **tijera**.

### Núcleos {#kernels}

Los núcleos de los portátiles son los motores informáticos específicos del idioma para el procesamiento de las celdas de los portátiles. Además de [!DNL Python], [!DNL JupyterLab] proporciona compatibilidad con idiomas adicional en R, PySpark y [!DNL Spark] (Scala). Al abrir un documento de bloc de notas, se inicia el núcleo asociado. Cuando se ejecuta una celda de un bloc de notas, el núcleo realiza el cálculo y produce resultados que pueden consumir recursos significativos de CPU y memoria. Tenga en cuenta que la memoria asignada no se libera hasta que se apaga el núcleo.

Ciertas características y funcionalidades están limitadas a núcleos particulares como se describe en la tabla siguiente:

| Núcleo | Compatibilidad con instalación de biblioteca | Integraciones de [!DNL Platform] |
| :----: | :--------------------------: | :-------------------- |
| **[!DNL Python]** | Sí | <ul><li>[!DNL Sensei ML Framework]</li><li>[!DNL Catalog Service]</li><li>[!DNL Query Service]</li></ul> |
| **R** | Sí | <ul><li>[!DNL Sensei ML Framework]</li><li>[!DNL Catalog Service]</li></ul> |
| **Scala** | No | <ul><li>[!DNL Sensei ML Framework]</li><li>[!DNL Catalog Service]</li></ul> |

### Sesiones de kernel {#kernel-sessions}

Cada bloc de notas o actividad activa en [!DNL JupyterLab] utiliza una sesión del núcleo. Para encontrar todas las sesiones activas, expanda la pestaña **Terminales y núcleos en ejecución** de la barra lateral izquierda. El tipo y el estado del núcleo de un portátil se pueden identificar observando la parte superior derecha de la interfaz del portátil. En el diagrama siguiente, el núcleo asociado del bloc de notas es **[!DNL Python]3** y su estado actual está representado por un círculo gris a la derecha. Un círculo hueco implica un núcleo inactivo y un círculo sólido implica un núcleo ocupado.

![](../images/jupyterlab/user-guide/kernel_and_state_1.png)

Si el kernel está apagado o inactivo durante un período prolongado, entonces **¡No Kernel!** con un círculo sólido se muestra. Active un kernel haciendo clic en el estado del kernel y seleccionando el tipo de kernel apropiado como se muestra a continuación:

![](../images/jupyterlab/user-guide/switch_kernel.gif)

### Lanzadera {#launcher}

[//]: # (Talk about the different Notebooks, introduce that certain starter notebooks are limited to particular kernels)

El lanzador *personalizado* le proporciona plantillas de bloc de notas útiles para sus kernels compatibles con el fin de ayudarle a poner en marcha su tarea, incluyendo:

| Plantilla | Descripción |
| --- | --- |
| Espacio en blanco | Un archivo de bloc de notas vacío. |
| Iniciador | Un bloc de notas precargado que muestra la exploración de datos con datos de ejemplo. |
| Ventas minoristas | Un bloc de notas precargado con la [fórmula de venta minorista](../pre-built-recipes/retail-sales.md) y datos de ejemplo. |
| Generador de recetas | Un bloc de notas plantilla para crear un fórmula en [!DNL JupyterLab]. Está precargado con código y comentarios que demuestran y describen el proceso de creación de fórmula. Consulte el [bloc de notas para obtener fórmula tutorial](https://www.adobe.com/go/data-science-create-recipe-notebook-tutorial-en) un recorrido detallado. |
| [!DNL Query Service] | Un cuaderno precargado que demuestra el uso de [!DNL Query Service] directamente con [!DNL JupyterLab] el flujos de trabajo de muestra proporcionado que analiza los datos a escala. |
| Eventos XDM | Un bloc de notas precargado que muestra la exploración de datos en datos de eventos de experiencia posvalor, centrándose en las características comunes en toda la estructura de datos. |
| Consultas XDM | Un bloc de notas rellenado previamente que muestra consultas comerciales de muestra sobre datos de eventos de experiencia. |
| Agregación | Un cuaderno precargado que muestra flujos de trabajo de muestra para agregado grandes cantidades de datos en trozos más pequeños y manejables. |
| Agrupamiento | Un bloc de notas precargado que muestra el proceso de modelado de aprendizaje automático de extremo a extremo mediante algoritmos de agrupación en clústeres. |

Algunas plantillas de bloc de notas están limitadas a determinados núcleos. La disponibilidad de plantillas para cada kernel se asigna en la tabla siguiente:

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
        <th><strong>Agrupamiento</strong></th>
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

Para abrir un nuevo *iniciador*, haga clic en **Archivo > Nuevo iniciador**. También puede expandir **Explorador de archivos** desde la barra lateral izquierda y hacer clic en el símbolo de suma (**+**):

![](../images/jupyterlab/user-guide/new_launcher.gif)

## Pasos siguientes

Para obtener más información sobre cada uno de los blocs de notas compatibles y cómo usarlos, visita el [guía del desarrollador de acceso](./access-notebook-data.md) a datos de blocs de notas de Jupyterlab. Este guía se centra en cómo usar los blocs de notas de JupyterLab para acceder a los datos, incluidos los datos de lectura, escritura y consulta. La guía de acceso a datos también contiene información sobre la cantidad máxima de datos que puede leer cada bloc de notas compatible.

## bibliotecas admitido {#supported-libraries}

Para obtener una lista de paquetes compatibles con Python, R y PySpark, copie y pegue `!conda list` en una nueva celda y, a continuación, ejecute la celda. La lista de paquetes admitidos se rellena en orden alfabético.

![ejemplo](../images/jupyterlab/user-guide/libraries.PNG)

Además, se usan las siguientes dependencias, pero no se enumeran:
* CUDA 11.2
* CUDNN 8.1

