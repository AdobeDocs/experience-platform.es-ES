---
keywords: Experience Platform;JupyterLab;blocs de notas;Data Science Workspace;temas populares;jupyterlab
solution: Experience Platform
title: Información general sobre la interfaz de usuario de JupyterLab
description: JupyterLab es una interfaz de usuario basada en web para Project Jupyter y está estrechamente integrada en Adobe Experience Platform. Proporciona un entorno de desarrollo interactivo para que los científicos de datos trabajen con Jupyter Notebooks, código y datos. Este documento proporciona información general sobre JupyterLab y sus características, así como instrucciones para realizar acciones comunes.
exl-id: 13786fbd-ef16-49cd-8bcf-46320c33e902
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '1820'
ht-degree: 3%

---

# [!DNL JupyterLab] Información general sobre la IU

[!DNL JupyterLab] es una interfaz de usuario basada en web para [Júpiter del proyecto](https://jupyter.org/) y está estrechamente integrado en Adobe Experience Platform. Proporciona un entorno de desarrollo interactivo para que los científicos de datos trabajen con Jupyter Notebooks, código y datos.

Este documento proporciona información general sobre [!DNL JupyterLab] y sus características, así como instrucciones para realizar acciones comunes.

## [!DNL JupyterLab] en [!DNL Experience Platform]

La integración de JupyterLab de Experience Platform se acompaña de cambios de arquitectura, consideraciones de diseño, extensiones de bloc de notas personalizadas, bibliotecas preinstaladas y una interfaz temática de Adobe.

La siguiente lista describe algunas de las funciones exclusivas de JupyterLab en Platform:

| Función | Descripción |
| --- | --- |
| **Kernels** | Los kernels proporcionan portátiles y otros [!DNL JupyterLab] front-end de la capacidad de ejecutar e introspect código en diferentes lenguajes de programación. [!DNL Experience Platform] proporciona núcleos adicionales para admitir el desarrollo en [!DNL Python], R, PySpark y [!DNL Spark]. Consulte la [kernels](#kernels) para obtener más información. |
| **Acceso a datos** | Acceda a los conjuntos de datos existentes directamente desde dentro [!DNL JupyterLab] con compatibilidad total con funciones de lectura y escritura. |
| **[!DNL Platform]integración de servicios** | Las integraciones integradas le permiten utilizar otras [!DNL Platform] servicios directamente desde [!DNL JupyterLab]. En la sección de , encontrará una lista completa de las integraciones compatibles con [Integración con otros servicios de Platform](#service-integration). |
| **Autenticación** | Además de <a href="https://jupyter-notebook.readthedocs.io/en/stable/security.html" target="_blank">Modelo de seguridad integrado de JupyterLab</a>, todas las interacciones entre la aplicación y el Experience Platform, incluida la comunicación de servicio a servicio de Platform, se cifran y autentican a través de la variable <a href="https://www.adobe.io/authentication/auth-methods.html" target="_blank">[!DNL Adobe Identity Management System] (IMS)</a>. |
| **Bibliotecas de desarrollo** | En [!DNL Experience Platform], [!DNL JupyterLab] proporciona bibliotecas preinstaladas para [!DNL Python], R y PySpark. Consulte la [apéndice](#supported-libraries) para obtener una lista completa de las bibliotecas admitidas. |
| **Controlador de biblioteca** | Cuando faltan las bibliotecas preinstaladas para sus necesidades, se pueden instalar bibliotecas adicionales para Python y R, y se almacenan temporalmente en contenedores aislados para mantener la integridad de [!DNL Platform] y mantenga sus datos seguros. Consulte la [kernels](#kernels) para obtener más información. |

>[!NOTE]
>
>Las bibliotecas adicionales solo están disponibles para la sesión en la que se instalaron. Debe volver a instalar las bibliotecas adicionales que necesite al iniciar nuevas sesiones.

## Integración con otros [!DNL Platform] servicios {#service-integration}

La normalización y la interoperabilidad son conceptos clave [!DNL Experience Platform]. La integración de [!DNL JupyterLab] en [!DNL Platform] como un IDE integrado le permite interactuar con otros [!DNL Platform] servicios, permitiéndole utilizar [!DNL Platform] a todo su potencial. Lo siguiente [!DNL Platform] los servicios están disponibles en [!DNL JupyterLab]:

* **[!DNL Catalog Service]:** Acceda y explore conjuntos de datos con funcionalidades de lectura y escritura.
* **[!DNL Query Service]:** Acceda y explore conjuntos de datos mediante SQL, lo que proporciona un menor número de sobrecargas de acceso a los datos cuando se trata de grandes cantidades de datos.
* **[!DNL Sensei ML Framework]:** Desarrollo de modelos con la capacidad de entrenar y puntuar datos, así como la creación de fórmulas con un solo clic.
* **[!DNL Experience Data Model (XDM)]:** La estandarización y la interoperabilidad son conceptos clave detrás de Adobe Experience Platform. [Modelo de datos de experiencia (XDM)](https://www.adobe.com/go/xdm-home-en), impulsado por el Adobe, es un esfuerzo por estandarizar los datos de experiencia del cliente y definir esquemas para la administración de experiencias del cliente.

>[!NOTE]
>
>Algunas [!DNL Platform] integraciones de servicio en [!DNL JupyterLab] se limitan a núcleos específicos. Consulte la sección sobre [kernels](#kernels) para obtener más información.

## Funciones principales y operaciones comunes

Información sobre las características clave de [!DNL JupyterLab] En las secciones siguientes se proporcionan instrucciones sobre la realización de operaciones comunes:

* [Acceso a JupyterLab](#access-jupyterlab)
* [Interfaz de JupyterLab](#jupyterlab-interface)
* [Celdas de código](#code-cells)
* [Kernels](#kernels)
* [Sesiones del núcleo](#kernel-sessions)
* [Iniciador](#launcher)

### Acceso [!DNL JupyterLab] {#access-jupyterlab}

En [Adobe Experience Platform](https://platform.adobe.com), seleccione **[!UICONTROL Portátiles]** en la columna de navegación izquierda. Permitir un poco de tiempo [!DNL JupyterLab] para inicializar completamente.

![](../images/jupyterlab/user-guide/access_jupyterlab.png)

### [!DNL JupyterLab] interfaz {#jupyterlab-interface}

La variable [!DNL JupyterLab] La interfaz de consta de una barra de menús, una barra lateral izquierda contraíble y el área de trabajo principal que contiene pestañas de documentos y actividades.

**Barra de menú**

La barra de menús de la parte superior de la interfaz tiene menús de nivel superior que exponen acciones disponibles en [!DNL JupyterLab] con sus métodos abreviados del teclado:

* **Archivo:** Acciones relacionadas con archivos y directorios
* **Editar:** Acciones relacionadas con la edición de documentos y otras actividades
* **Ver:** Acciones que modifican el aspecto de [!DNL JupyterLab]
* **Ejecutar:** Acciones para ejecutar código en diferentes actividades, como blocs de notas y consolas de código
* **Núcleo:** Acciones para administrar los núcleos
* **Pestañas:** Una lista de documentos y actividades abiertos
* **Configuración:** Configuración común y editor de configuración avanzada
* **Ayuda:** Una lista de [!DNL JupyterLab] y enlaces de ayuda del núcleo

**Barra lateral izquierda**

La barra lateral izquierda contiene fichas en las que se puede hacer clic y que proporcionan acceso a las siguientes funciones:

* **Explorador de archivos:** Una lista de documentos y directorios del bloc de notas guardados
* **Explorador de datos:** Examinar, acceder y explorar conjuntos de datos y esquemas
* **Kernels y terminales en funcionamiento:** Una lista de sesiones activas de kernel y terminal con la capacidad de finalizar
* **Comandos:** Lista de comandos útiles
* **inspector de celdas:** Editor de celdas que proporciona acceso a herramientas y metadatos útiles para configurar un bloc de notas con fines de presentación
* **pestañas:** Una lista de pestañas abiertas

Seleccione una ficha para exponer sus funciones o seleccione en una ficha expandida para contraer la barra lateral izquierda como se muestra a continuación:

![](../images/jupyterlab/user-guide/left_sidebar_collapse.gif)

**Área de trabajo principal**

El área de trabajo principal de [!DNL JupyterLab] permite organizar documentos y otras actividades en paneles de pestañas que se pueden cambiar de tamaño o subdividir. Arrastre una pestaña al centro de un panel de pestañas para migrar la pestaña. Para dividir un panel, arrastre una ficha a la izquierda, la derecha, la parte superior o la parte inferior del panel:

![](../images/jupyterlab/user-guide/main_work_area.gif)

### Configuración de GPU y servidor de memoria en [!DNL Python]/R

En [!DNL JupyterLab] seleccione el icono de engranaje en la esquina superior derecha para abrir *Configuración del servidor portátil*. Puede activar la GPU y asignar la cantidad de memoria que necesita mediante el control deslizante. La cantidad de memoria que puede asignar depende de cuánto haya proporcionado su organización. Select **[!UICONTROL Actualizar configuraciones]** para guardar.

>[!NOTE]
>
>Solo se proporciona una GPU por organización para portátiles. Si la GPU está en uso, debe esperar a que el usuario que actualmente ha reservado la GPU la libere. Esto se puede hacer cerrando la sesión o dejando la GPU en estado inactivo durante cuatro o más horas.

![](../images/jupyterlab/user-guide/notebook-gpu-config.png)

### Finalización y reinicio [!DNL JupyterLab]

En [!DNL JupyterLab], puede finalizar la sesión para evitar que se utilicen más recursos. Comience por seleccionar la **icono de alimentación** ![icono de alimentación](../images/jupyterlab/user-guide/power_button.png)y, a continuación, seleccione **[!UICONTROL Apagar]** desde la ventana emergente que aparece para finalizar la sesión. Las sesiones de bloc de notas finalizan automáticamente después de 12 horas sin actividad.

Para reiniciar [!DNL JupyterLab], seleccione **icono reiniciar** ![icono reiniciar](../images/jupyterlab/user-guide/restart_button.png) situado directamente a la izquierda del icono de alimentación, seleccione **[!UICONTROL Restart]** de la ventana emergente que aparece.

![terminar jupyterlab](../images/jupyterlab/user-guide/shutdown-jupyterlab.gif)

### Celdas de código {#code-cells}

Las celdas de código son el contenido principal de los blocs de notas. Contienen código fuente en el idioma del núcleo asociado al bloc de notas y la salida como resultado de ejecutar la celda de código. Se muestra un recuento de ejecución a la derecha de cada celda de código que representa su orden de ejecución.

![](../images/jupyterlab/user-guide/code_cell.png)

A continuación se describen las acciones comunes de las celdas:

* **Agregue una celda:** Haga clic en el símbolo más (**+**) del menú del bloc de notas para añadir una celda vacía. Las celdas nuevas se colocan debajo de la celda con la que se está interactuando o al final del bloc de notas si no hay ninguna celda en concreto enfocada.

* **Mover una celda:** Sitúe el cursor a la derecha de la celda que desee mover y, a continuación, haga clic y arrastre la celda a una nueva ubicación. Además, al mover una celda de un bloc de notas a otro, se replica la celda junto con su contenido.

* **Ejecutar una celda:** Haga clic en el cuerpo de la celda que desea ejecutar y, a continuación, haga clic en el botón **play** icono (**>**) del menú del bloc de notas. Un asterisco (**\***) se muestra en el contador de ejecución de la celda cuando el núcleo está procesando la ejecución y se reemplaza con un número entero al completarse.

* **Eliminar una celda:** Haga clic en el cuerpo de la celda que desea eliminar y, a continuación, haga clic en el botón **tijera** icono.

### Kernels {#kernels}

Los núcleos de los portátiles son los motores informáticos específicos del lenguaje para procesar las celdas de los portátiles. Además de [!DNL Python], [!DNL JupyterLab] proporciona compatibilidad con idiomas adicionales en R, PySpark y [!DNL Spark] (Scala). Cuando abre un documento de bloc de notas, se inicia el núcleo asociado. Cuando se ejecuta una celda de un bloc de notas, el núcleo realiza el cálculo y produce resultados que pueden consumir importantes recursos de CPU y memoria. Tenga en cuenta que la memoria asignada no se libera hasta que se apaga el núcleo.

Algunas funciones y funcionalidades se limitan a núcleos particulares, como se describe en la siguiente tabla:

| Núcleo | Compatibilidad con la instalación de bibliotecas | [!DNL Platform] integraciones |
| :----: | :--------------------------: | :-------------------- |
| **[!DNL Python]** | Sí | <ul><li>[!DNL Sensei ML Framework]</li><li>[!DNL Catalog Service]</li><li>[!DNL Query Service]</li></ul> |
| **R** | Sí | <ul><li>[!DNL Sensei ML Framework]</li><li>[!DNL Catalog Service]</li></ul> |
| **Scala** | No | <ul><li>[!DNL Sensei ML Framework]</li><li>[!DNL Catalog Service]</li></ul> |

### Sesiones del núcleo {#kernel-sessions}

Cada bloc de notas o actividad activa en [!DNL JupyterLab] utiliza una sesión del núcleo. Para encontrar todas las sesiones activas, expanda el **Terminales y kernels en funcionamiento** de la barra lateral izquierda. El tipo y estado del núcleo para un bloc de notas se puede identificar observando la parte superior derecha de la interfaz del bloc de notas. En el diagrama siguiente, el núcleo asociado al bloc de notas es **[!DNL Python]3** y su estado actual se representa mediante un círculo gris a la derecha. Un círculo hueco implica un núcleo de ralentí y un círculo sólido implica un núcleo ocupado.

![](../images/jupyterlab/user-guide/kernel_and_state_1.png)

Si el núcleo está apagado o inactivo durante un período prolongado, entonces **¡Sin núcleo!** con un círculo sólido se muestra. Active un núcleo haciendo clic en el estado del núcleo y seleccionando el tipo de núcleo apropiado como se muestra a continuación:

![](../images/jupyterlab/user-guide/switch_kernel.gif)

### Iniciador {#launcher}

[//]: # (Talk about the different Notebooks, introduce that certain starter notebooks are limited to particular kernels)

El *Iniciador* le proporciona plantillas de bloc de notas útiles para sus kernels compatibles que le ayudarán a iniciar su tarea, incluidas:

| Plantilla | Descripción |
| --- | --- |
| En blanco | Un archivo de bloc de notas vacío. |
| Inicio | Un bloc de notas precargado que muestra la exploración de datos mediante datos de ejemplo. |
| Ventas minoristas | Un bloc de notas precargado que incluye el [fórmula de venta minorista](../pre-built-recipes/retail-sales.md) uso de datos de ejemplo. |
| Generador de fórmulas | Una plantilla de bloc de notas para crear una fórmula en [!DNL JupyterLab]. Está precargada con código y comentarios que muestran y describen el proceso de creación de fórmulas. Consulte la [tutorial de bloc de notas a fórmula](https://www.adobe.com/go/data-science-create-recipe-notebook-tutorial-en) para obtener una guía detallada. |
| [!DNL Query Service] | Un bloc de notas precargado que muestra el uso de [!DNL Query Service] directamente en [!DNL JupyterLab] con flujos de trabajo de ejemplo proporcionados que analizan los datos a escala. |
| Eventos XDM | Un bloc de notas precargado que muestra la exploración de datos en datos de Evento de Experiencia después de un valor, centrado en características comunes en la estructura de datos. |
| Consultas XDM | Un bloc de notas precargado que muestra consultas empresariales de muestra sobre datos de Experience Event. |
| Agregación | Un bloc de notas precargado que muestra flujos de trabajo de ejemplo para acumular grandes cantidades de datos en trozos más pequeños y manejables. |
| Clustering | Un bloc de notas precargado que muestra el proceso de modelado completo del aprendizaje automático mediante algoritmos de agrupación en clúster. |

Algunas plantillas de bloc de notas se limitan a ciertos núcleos. La disponibilidad de plantillas para cada núcleo se asigna en la siguiente tabla:

<table>
    <tr>
        <td></td>
        <th><strong>En blanco</strong></th>
        <th><strong>Inicio</strong></th>
        <th><strong>Ventas minoristas</strong></th>
        <th><strong>Generador de fórmulas</strong></th>
        <th><strong>[!DNL Query Service]</strong></th>
        <th><strong>Eventos XDM</strong></th>
        <th><strong>Consultas XDM</strong></th>
        <th><strong>Agregación</strong></th>
        <th><strong>Clustering</strong></th>
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

Para abrir una nueva *Iniciador*, haga clic en **Archivo > Nuevo iniciador**. También puede expandir el **Explorador de archivos** en la barra lateral izquierda y haga clic en el símbolo más (**+**):

![](../images/jupyterlab/user-guide/new_launcher.gif)

## Pasos siguientes

Para obtener más información sobre cada uno de los blocs de notas admitidos y cómo utilizarlos, visite [Acceso a los datos de los portátiles Jupyterlab](./access-notebook-data.md) guía para desarrolladores. Esta guía se centra en cómo utilizar los blocs de notas de JupyterLab para acceder a sus datos, incluyendo lectura, escritura y consulta de datos. La guía de acceso a datos también contiene información sobre la cantidad máxima de datos que puede leer cada bloc de notas compatible.

## Bibliotecas compatibles {#supported-libraries}

Para obtener una lista de paquetes compatibles con Python, R y PySpark, copie y pegue `!conda list` en una celda nueva, ejecute la celda. Una lista de paquetes compatibles se rellena en orden alfabético.

![ejemplo](../images/jupyterlab/user-guide/libraries.PNG)

Además, se utilizan las siguientes dependencias, pero no se enumeran:
* CUDA 11.2
* CUDNN 8.1

