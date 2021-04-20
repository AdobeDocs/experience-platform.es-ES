---
keywords: Experience Platform;JupyterLab;blocs de notas;Data Science Workspace;temas populares;jupyterlab
solution: Experience Platform
title: Información general sobre la interfaz de usuario de JupyterLab
topic: Overview
description: JupyterLab es una interfaz de usuario basada en web para Project Jupyter y está estrechamente integrada en Adobe Experience Platform. Proporciona un entorno de desarrollo interactivo para que los científicos de datos trabajen con Jupyter Notebooks, código y datos. Este documento proporciona información general sobre JupyterLab y sus características, así como instrucciones para realizar acciones comunes.
translation-type: tm+mt
source-git-commit: 9d84fc1eb898020ed4b154c091fcc9fc4933c7de
workflow-type: tm+mt
source-wordcount: '1820'
ht-degree: 3%

---


# [!DNL JupyterLab] Información general sobre la IU

[!DNL JupyterLab] es una interfaz de usuario basada en web para  [Project ](https://jupyter.org/) Jupytery está estrechamente integrada en Adobe Experience Platform. Proporciona un entorno de desarrollo interactivo para que los científicos de datos trabajen con Jupyter Notebooks, código y datos.

Este documento proporciona información general sobre [!DNL JupyterLab] y sus características, así como instrucciones para realizar acciones comunes.

## [!DNL JupyterLab] en [!DNL Experience Platform]

La integración de JupyterLab de Experience Platform se acompaña de cambios de arquitectura, consideraciones de diseño, extensiones de bloc de notas personalizadas, bibliotecas preinstaladas y una interfaz temática de Adobe.

La siguiente lista describe algunas de las funciones exclusivas de JupyterLab en Platform:

| Función | Descripción |
| --- | --- |
| **Kernels** | Los kernels proporcionan portátiles y otros [!DNL JupyterLab] front-end de la capacidad de ejecutar e introspeccionar código en diferentes lenguajes de programación. [!DNL Experience Platform] proporciona núcleos adicionales para admitir el desarrollo en  [!DNL Python], R, PySpark y  [!DNL Spark]. Consulte la sección [kernels](#kernels) para obtener más información. |
| **Acceso a datos** | Acceda a los conjuntos de datos existentes directamente desde [!DNL JupyterLab] con compatibilidad total con capacidades de lectura y escritura. |
| **[!DNL Platform]integración de servicios** | Las integraciones integradas le permiten utilizar otros servicios [!DNL Platform] directamente desde [!DNL JupyterLab]. En la sección [Integration with other Platform services](#service-integration) se proporciona una lista completa de las integraciones compatibles. |
| **Autenticación** | Además del modelo de seguridad integrado de <a href="https://jupyter-notebook.readthedocs.io/en/latest/security.html" target="_blank">JupyterLab</a>, cada interacción entre su aplicación y el Experience Platform, incluida la comunicación de servicio a servicio de Platform, se cifra y autentica a través de <a href="https://www.adobe.io/authentication/auth-methods.html" target="_blank">[!DNL Adobe Identity Management System] (IMS)</a>. |
| **Bibliotecas de desarrollo** | En [!DNL Experience Platform], [!DNL JupyterLab] proporciona bibliotecas preinstaladas para [!DNL Python], R y PySpark. Consulte el [apéndice](#supported-libraries) para obtener una lista completa de las bibliotecas admitidas. |
| **Controlador de biblioteca** | Cuando faltan las bibliotecas preinstaladas para sus necesidades, se pueden instalar bibliotecas adicionales para Python y R, y se almacenan temporalmente en contenedores aislados para mantener la integridad de [!DNL Platform] y mantener los datos seguros. Consulte la sección [kernels](#kernels) para obtener más información. |

>[!NOTE]
>
>Las bibliotecas adicionales solo están disponibles para la sesión en la que se instalaron. Debe volver a instalar las bibliotecas adicionales que necesite al iniciar nuevas sesiones.

## Integración con otros [!DNL Platform] servicios {#service-integration}

La estandarización y la interoperabilidad son conceptos clave detrás de [!DNL Experience Platform]. La integración de [!DNL JupyterLab] en [!DNL Platform] como un IDE integrado le permite interactuar con otros [!DNL Platform] servicios, lo que le permite utilizar [!DNL Platform] a todo su potencial. Los siguientes [!DNL Platform] servicios están disponibles en [!DNL JupyterLab]:

* **[!DNL Catalog Service]:** Acceda y explore conjuntos de datos con funcionalidades de lectura y escritura.
* **[!DNL Query Service]:** Acceda y explore conjuntos de datos mediante SQL, lo que proporciona un menor número de sobrecargas de acceso a los datos cuando se trata de grandes cantidades de datos.
* **[!DNL Sensei ML Framework]:** Desarrollo de modelos con la capacidad de entrenar y puntuar datos, así como creación de fórmulas con un solo clic.
* **[!DNL Experience Data Model (XDM)]:** La estandarización y la interoperabilidad son conceptos clave detrás de Adobe Experience Platform. [Experience Data Model (XDM)](https://www.adobe.com/go/xdm-home-en), impulsado por el Adobe, es un esfuerzo por estandarizar los datos de experiencia del cliente y definir esquemas para la administración de experiencias del cliente.

>[!NOTE]
>
>Algunas [!DNL Platform] integraciones de servicio en [!DNL JupyterLab] se limitan a núcleos específicos. Consulte la sección [kernels](#kernels) para obtener más información.

## Funciones principales y operaciones comunes

En las secciones siguientes se proporciona información sobre las características clave de [!DNL JupyterLab] e instrucciones para realizar operaciones comunes:

* [Acceso a JupyterLab](#access-jupyterlab)
* [Interfaz de JupyterLab](#jupyterlab-interface)
* [Celdas de código](#code-cells)
* [Kernels](#kernels)
* [Sesiones del núcleo](#kernel-sessions)
* [Iniciador](#launcher)

### Acceso [!DNL JupyterLab] {#access-jupyterlab}

En [Adobe Experience Platform](https://platform.adobe.com), seleccione **[!UICONTROL Notebooks]** en la columna de navegación izquierda. Espere un tiempo para que [!DNL JupyterLab] se inicialice completamente.

![](../images/jupyterlab/user-guide/access_jupyterlab.png)

### [!DNL JupyterLab] interfaz {#jupyterlab-interface}

La interfaz [!DNL JupyterLab] consta de una barra de menús, una barra lateral izquierda contraíble y el área de trabajo principal que contiene pestañas de documentos y actividades.

**Barra de menús**

La barra de menús de la parte superior de la interfaz tiene menús de nivel superior que exponen las acciones disponibles en [!DNL JupyterLab] con sus métodos abreviados de teclado:

* **Archivo:** Acciones relacionadas con archivos y directorios
* **Editar:** acciones relacionadas con la edición de documentos y otras actividades
* **Vista:** Acciones que modifican el aspecto de  [!DNL JupyterLab]
* **Ejecutar:** acciones para ejecutar código en diferentes actividades, como blocs de notas y consolas de código
* **Núcleo:** Acciones para administrar núcleos
* **Pestañas:** una lista de documentos y actividades abiertos
* **Configuración:** configuración común y editor de configuración avanzada
* **Ayuda:** Una lista de vínculos de ayuda  [!DNL JupyterLab] y del núcleo

**Barra lateral izquierda**

La barra lateral izquierda contiene fichas en las que se puede hacer clic y que proporcionan acceso a las siguientes funciones:

* **Explorador de archivos:**  lista de documentos y directorios del bloc de notas guardados
* **Explorador de datos:** Examinar, acceder y explorar conjuntos de datos y esquemas
* **Ejecución de kernels y terminales:**  una lista de sesiones activas del núcleo y de los terminales con capacidad para finalizar
* **Comandos:** lista de comandos útiles
* **inspector de celdas:**  editor de celdas que proporciona acceso a herramientas y metadatos útiles para configurar un bloc de notas con fines de presentación.
* **fichas:** una lista de fichas abiertas

Seleccione una ficha para exponer sus funciones o seleccione en una ficha expandida para contraer la barra lateral izquierda como se muestra a continuación:

![](../images/jupyterlab/user-guide/left_sidebar_collapse.gif)

**Área de trabajo principal**

El área de trabajo principal de [!DNL JupyterLab] le permite organizar documentos y otras actividades en paneles de pestañas que se pueden cambiar de tamaño o subdividir. Arrastre una pestaña al centro de un panel de pestañas para migrar la pestaña. Para dividir un panel, arrastre una ficha a la izquierda, la derecha, la parte superior o la parte inferior del panel:

![](../images/jupyterlab/user-guide/main_work_area.gif)

### Configuración de GPU y servidor de memoria en [!DNL Python]/R

En [!DNL JupyterLab] seleccione el icono de engranaje en la esquina superior derecha para abrir la *Configuración del servidor de portátiles*. Puede activar la GPU y asignar la cantidad de memoria que necesita mediante el control deslizante. La cantidad de memoria que puede asignar depende de cuánto haya proporcionado su organización. Seleccione **[!UICONTROL Update configs]** para guardar.

>[!NOTE]
>
>Solo se proporciona una GPU por organización para portátiles. Si la GPU está en uso, debe esperar a que el usuario que actualmente ha reservado la GPU la libere. Esto se puede hacer cerrando la sesión o dejando la GPU en estado inactivo durante cuatro o más horas.

![](../images/jupyterlab/user-guide/notebook-gpu-config.png)

### Finalizar y reiniciar [!DNL JupyterLab]

En [!DNL JupyterLab], puede finalizar la sesión para evitar que se utilicen más recursos. Comience por seleccionar el **icono de energía** ![icono de energía](../images/jupyterlab/user-guide/power_button.png) y, a continuación, seleccione **[!UICONTROL Apagar]** en la ventana emergente que aparece para finalizar la sesión. Las sesiones de bloc de notas finalizan automáticamente después de 12 horas sin actividad.

Para reiniciar [!DNL JupyterLab], seleccione el **icono de reinicio** ![icono de reinicio](../images/jupyterlab/user-guide/restart_button.png) situado directamente a la izquierda del icono de energía y, a continuación, seleccione **[!UICONTROL Restart]** en la ventana emergente que aparece.

![terminar jupyterlab](../images/jupyterlab/user-guide/shutdown-jupyterlab.gif)

### Celdas de código {#code-cells}

Las celdas de código son el contenido principal de los blocs de notas. Contienen código fuente en el idioma del núcleo asociado al bloc de notas y la salida como resultado de ejecutar la celda de código. Se muestra un recuento de ejecución a la derecha de cada celda de código que representa su orden de ejecución.

![](../images/jupyterlab/user-guide/code_cell.png)

A continuación se describen las acciones comunes de las celdas:

* **Agregar una celda:** haga clic en el símbolo más (**+**) del menú del bloc de notas para agregar una celda vacía. Las celdas nuevas se colocan debajo de la celda con la que se está interactuando o al final del bloc de notas si no hay ninguna celda en concreto enfocada.

* **Mover una celda:** coloque el cursor a la derecha de la celda que desee mover y, a continuación, haga clic y arrastre la celda a una nueva ubicación. Además, al mover una celda de un bloc de notas a otro, se replica la celda junto con su contenido.

* **Ejecutar una celda:** haga clic en el cuerpo de la celda que desea ejecutar y, a continuación, haga clic en el  **** icono de reproducción (**▶**) del menú del bloc de notas. Se muestra un asterisco (**\***) en el contador de ejecución de la celda cuando el núcleo está procesando la ejecución y se reemplaza con un número entero al completarse.

* **Eliminar una celda:** haga clic en el cuerpo de la celda que desee eliminar y, a continuación, haga clic en el icono de  **** scissoricon.

### Kernels {#kernels}

Los núcleos de los portátiles son los motores informáticos específicos del lenguaje para procesar las celdas de los portátiles. Además de [!DNL Python], [!DNL JupyterLab] proporciona soporte de idioma adicional en R, PySpark y [!DNL Spark] (Scala). Cuando abre un documento de bloc de notas, se inicia el núcleo asociado. Cuando se ejecuta una celda de un bloc de notas, el núcleo realiza el cálculo y produce resultados que pueden consumir importantes recursos de CPU y memoria. Tenga en cuenta que la memoria asignada no se libera hasta que se apaga el núcleo.

Algunas funciones y funcionalidades se limitan a núcleos particulares, como se describe en la siguiente tabla:

| Núcleo | Compatibilidad con la instalación de bibliotecas | [!DNL Platform] integraciones |
| :----: | :--------------------------: | :-------------------- |
| **[!DNL Python]** | Sí | <ul><li>[!DNL Sensei ML Framework]</li><li>[!DNL Catalog Service]</li><li>[!DNL Query Service]</li></ul> |
| **R** | Sí | <ul><li>[!DNL Sensei ML Framework]</li><li>[!DNL Catalog Service]</li></ul> |
| **Scala** | No | <ul><li>[!DNL Sensei ML Framework]</li><li>[!DNL Catalog Service]</li></ul> |

### Sesiones del núcleo {#kernel-sessions}

Cada bloc de notas o actividad activa en [!DNL JupyterLab] utiliza una sesión del núcleo. Para encontrar todas las sesiones activas, expanda la pestaña **Running terminales and kernels** desde la barra lateral izquierda. El tipo y estado del núcleo para un bloc de notas se puede identificar observando la parte superior derecha de la interfaz del bloc de notas. En el diagrama siguiente, el núcleo asociado del bloc de notas es **[!DNL Python]3** y su estado actual está representado por un círculo gris a la derecha. Un círculo hueco implica un núcleo de ralentí y un círculo sólido implica un núcleo ocupado.

![](../images/jupyterlab/user-guide/kernel_and_state_1.png)

Si el núcleo está apagado o inactivo durante un período prolongado, entonces **No Kernel!** con un círculo sólido se muestra. Active un núcleo haciendo clic en el estado del núcleo y seleccionando el tipo de núcleo apropiado como se muestra a continuación:

![](../images/jupyterlab/user-guide/switch_kernel.gif)

### Iniciador {#launcher}

[//]: # (Talk about the different Notebooks, introduce that certain starter notebooks are limited to particular kernels)

El *Iniciador* personalizado le proporciona plantillas de bloc de notas útiles para sus núcleos compatibles que le ayudarán a iniciar su tarea, entre las que se incluyen:

| Plantilla | Descripción |
| --- | --- |
| En blanco | Un archivo de bloc de notas vacío. |
| Inicio | Un bloc de notas precargado que muestra la exploración de datos mediante datos de ejemplo. |
| Ventas minoristas | Un bloc de notas precargado que presenta la [fórmula de ventas minoristas](https://adobe.ly/2wOgO3L) utilizando datos de ejemplo. |
| Generador de fórmulas | Una plantilla de bloc de notas para crear una fórmula en [!DNL JupyterLab]. Está precargada con código y comentarios que muestran y describen el proceso de creación de fórmulas. Consulte el tutorial [bloc de notas a fórmula](https://www.adobe.com/go/data-science-create-recipe-notebook-tutorial-en) para obtener un tutorial detallado. |
| [!DNL Query Service] | Un bloc de notas precargado que muestra el uso de [!DNL Query Service] directamente en [!DNL JupyterLab] con flujos de trabajo de muestra proporcionados que analizan los datos a escala. |
| Eventos XDM | Un bloc de notas precargado que muestra la exploración de datos en datos de Evento de Experiencia después de un valor, centrado en características comunes en la estructura de datos. |
| Consultas XDM | Un bloc de notas precargado que muestra consultas empresariales de muestra sobre datos de Experience Event. |
| Agregación | Un bloc de notas precargado que muestra flujos de trabajo de ejemplo para acumular grandes cantidades de datos en trozos más pequeños y manejables. |
| Clustering | Un bloc de notas precargado que muestra el proceso de modelado completo del aprendizaje automático mediante algoritmos de agrupación en clúster. |

Algunas plantillas de bloc de notas están limitadas a ciertos núcleos. La disponibilidad de plantillas para cada núcleo se asigna en la siguiente tabla:

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

Para abrir un nuevo *Iniciador*, haga clic en **Archivo > Nuevo Iniciador**. También puede expandir el **File browser** desde la barra lateral izquierda y hacer clic en el símbolo más (**+**):

![](../images/jupyterlab/user-guide/new_launcher.gif)

## Pasos siguientes

Para obtener más información sobre cada uno de los blocs de notas compatibles y cómo utilizarlos, visite la [guía para desarrolladores de ](./access-notebook-data.md) acceso a los datos de los blocs de notas de Jupyterlab. Esta guía se centra en cómo utilizar los blocs de notas de JupyterLab para acceder a sus datos, incluyendo lectura, escritura y consulta de datos. La guía de acceso a datos también contiene información sobre la cantidad máxima de datos que puede leer cada bloc de notas compatible.

## Bibliotecas compatibles {#supported-libraries}

Para obtener una lista de paquetes compatibles con Python, R y PySpark, copie y pegue `!pip list --format=columns` en una celda nueva y, a continuación, ejecute la celda. Una lista de paquetes compatibles se rellena en orden alfabético.

![ejemplo](../images/jupyterlab/user-guide/libraries.PNG)