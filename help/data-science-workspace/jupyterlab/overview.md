---
keywords: Experience Platform;JupyterLab;notebooks;Data Science Workspace;popular topics
solution: Experience Platform
title: Guía del usuario de JupyterLab
topic: Overview
translation-type: tm+mt
source-git-commit: c48079ba997a7b4c082253a0b2867df76927aa6d
workflow-type: tm+mt
source-wordcount: '3647'
ht-degree: 11%

---


# [!DNL JupyterLab] guía del usuario

[!DNL JupyterLab] es una interfaz de usuario basada en web para <a href="https://jupyter.org/" target="_blank">Project Jupyter</a> y está estrechamente integrada en [!DNL Adobe Experience Platform]. Proporciona un entorno de desarrollo interactivo para que los científicos de datos trabajen con portátiles Jupyter, código y datos.

Este documento proporciona información general sobre [!DNL JupyterLab] y sus características, así como instrucciones para realizar acciones comunes.

## [!DNL JupyterLab] en [!DNL Experience Platform]

La integración de JupyterLab de Experience Platform se acompaña de cambios en la arquitectura, consideraciones de diseño, extensiones de bloc de notas personalizadas, bibliotecas preinstaladas y una interfaz temática de Adobe.

La siguiente lista describe algunas de las funciones exclusivas de JupyterLab en Platform:

| Función | Descripción |
| --- | --- |
| **Kernels** | Los kernels proporcionan al portátil y a otros [!DNL JupyterLab] front-end la capacidad de ejecutar e introducir código en diferentes lenguajes de programación. [!DNL Experience Platform] proporciona núcleos adicionales para admitir el desarrollo en [!DNL Python], R, PySpark y [!DNL Spark]. Consulte la sección [kernels](#kernels) para obtener más detalles. |
| **Acceso a datos** | Acceda directamente a los conjuntos de datos existentes desde dentro [!DNL JupyterLab] con compatibilidad total con las capacidades de lectura y escritura. |
| **[!DNL Platform]integración de servicios ** | Las integraciones integradas le permiten utilizar otros [!DNL Platform] servicios directamente desde dentro [!DNL JupyterLab]. En la sección sobre [Integración con otros servicios](#service-integration)de Platform se proporciona una lista completa de las integraciones admitidas. |
| **Autenticación** | Además del modelo <a href="https://jupyter-notebook.readthedocs.io/en/latest/security.html" target="_blank">de seguridad integrado de</a>JupyterLab, todas las interacciones entre la aplicación y el Experience Platform, incluida la comunicación de servicio a servicio de Platform, se cifran y autentican a través del <a href="https://www.adobe.io/authentication/auth-methods.html" target="_blank">[!DNL Adobe Identity Management System] (IMS)</a>. |
| **Bibliotecas de desarrollo** | En [!DNL Experience Platform], [!DNL JupyterLab] proporciona bibliotecas preinstaladas para [!DNL Python], R y PySpark. Consulte el [apéndice](#supported-libraries) para obtener una lista completa de las bibliotecas admitidas. |
| **Controlador de biblioteca** | Cuando las bibliotecas preinstaladas no están adaptadas a sus necesidades, se pueden instalar bibliotecas adicionales para Python y R, y se almacenan temporalmente en contenedores aislados para mantener la integridad de [!DNL Platform] los datos y mantenerlos seguros. Consulte la sección [kernels](#kernels) para obtener más detalles. |

>[!NOTE] Las bibliotecas adicionales solo están disponibles para la sesión en la que se instalaron. Debe reinstalar las bibliotecas adicionales que necesite al iniciar sesiones nuevas.

## Integración con otros [!DNL Platform] servicios {#service-integration}

La estandarización y la interoperabilidad son conceptos clave que sustentan [!DNL Experience Platform]. La integración de [!DNL JupyterLab] on [!DNL Platform] como un IDE integrado le permite interactuar con otros [!DNL Platform] servicios, permitiéndole utilizar [!DNL Platform] todo su potencial. Los siguientes [!DNL Platform] servicios están disponibles en [!DNL JupyterLab]:

* **[!DNL Catalog Service]::**Acceda y explore conjuntos de datos con funcionalidades de lectura y escritura.
* **[!DNL Query Service]::**Acceda y explore conjuntos de datos mediante SQL, proporcionando un acceso a los datos más bajo en los costes generales cuando se trata de grandes cantidades de datos.
* **[!DNL Sensei ML Framework]::**Desarrollo de modelos con la capacidad de entrenar y marcar datos, así como la creación de fórmulas con un solo clic.
* **[!DNL Experience Data Model (XDM)]::**La estandarización y la interoperabilidad son conceptos clave que sustentan el Adobe Experience Platform.[El modelo de datos de experiencia (XDM)](https://www.adobe.com/go/xdm-home-en), dirigido por Adobe, es un esfuerzo para estandarizar los datos de experiencia del cliente y definir esquemas para la administración de la experiencia del cliente.

>[!NOTE] Algunas integraciones [!DNL Platform] de servicios en [!DNL JupyterLab] están limitadas a núcleos específicos. Consulte la sección sobre [núcleos](#kernels) para obtener más detalles.

## Funciones clave y operaciones comunes

En las secciones siguientes se proporciona información sobre las características clave [!DNL JupyterLab] y las instrucciones para realizar operaciones comunes:

* [Access JupyterLab](#access-jupyterlab)
* [Interfaz JupyterLab](#jupyterlab-interface)
* [Celdas de código](#code-cells)
* [Kernels](#kernels)
* [Sesiones de núcleo](#kernel-sessions)
* [Recurso de ejecución de PySpark/Spark](#execution-resource)
* [Iniciador](#launcher)

### Acceso [!DNL JupyterLab] {#access-jupyterlab}

En [Adobe Experience Platform](https://platform.adobe.com), seleccione **Equipos portátiles** en la columna de navegación izquierda. Deje que transcurra algún tiempo para que se inicialice [!DNL JupyterLab] completamente.

![](../images/jupyterlab/user-guide/access_jupyterlab.png)

### [!DNL JupyterLab] interfaz {#jupyterlab-interface}

La [!DNL JupyterLab] interfaz consta de una barra de menús, una barra lateral izquierda contraíble y el área de trabajo principal que contiene fichas de documentos y actividades.

**Barra de menús**

La barra de menús situada en la parte superior de la interfaz tiene menús de nivel superior que exponen las acciones disponibles [!DNL JupyterLab] con los métodos abreviados de teclado:

* **Archivo:** Acciones relacionadas con archivos y directorios
* **Editar:** Acciones relacionadas con la edición de documentos y otras actividades
* **Vista:** Acciones que modifican el aspecto de [!DNL JupyterLab]
* **Ejecutar:** Acciones para ejecutar código en diferentes actividades, como blocs de notas y consolas de código
* **Núcleo:** Acciones para administrar los núcleos
* **Fichas:** Una lista de documentos y actividades abiertos
* **Configuración:** Configuración común y editor de configuración avanzada
* **Ayuda:** Una lista de vínculos de ayuda [!DNL JupyterLab] y del núcleo

**Barra lateral izquierda**

La barra lateral izquierda contiene fichas en las que se puede hacer clic que proporcionan acceso a las siguientes funciones:

* **Explorador de archivos:** Una lista de documentos y directorios de portátiles guardados
* **Explorador de datos:** Examinar, acceder y explorar conjuntos de datos y esquemas
* **Kernels de funcionamiento y terminales:** Una lista de las sesiones activas del núcleo y de terminal con la capacidad de finalizar
* **Comandos:** Una lista de comandos útiles
* **Inspector de celdas:** Editor de celdas que proporciona acceso a herramientas y metadatos útiles para configurar un bloc de notas con fines de presentación
* **fichas:** Una lista de fichas abiertas

Haga clic en una ficha para exponer sus funciones o haga clic en una ficha expandida para contraer la barra lateral izquierda como se muestra a continuación:

![](../images/jupyterlab/user-guide/left_sidebar_collapse.gif)

**Área de trabajo principal**

El área de trabajo principal de [!DNL JupyterLab] permite organizar documentos y otras actividades en paneles de fichas que se pueden cambiar de tamaño o subdividir. Arrastre una ficha al centro de un panel de fichas para migrarla. Para dividir un panel, arrastre una ficha a la izquierda, a la derecha, a la parte superior o a la parte inferior del panel:

![](../images/jupyterlab/user-guide/main_work_area.gif)

### Celdas de código {#code-cells}

Las celdas de código son el contenido principal de los blocs de notas. Contienen código fuente en el idioma del núcleo asociado al bloc de notas y la salida como resultado de la ejecución de la celda de código. Se muestra un recuento de ejecución a la derecha de cada celda de código que representa su orden de ejecución.

![](../images/jupyterlab/user-guide/code_cell.png)

Las acciones comunes de las células se describen a continuación:

* **Añadir una celda:** Haga clic en el símbolo más (**+**) del menú del bloc de notas para agregar una celda vacía. Las celdas nuevas se colocan debajo de la celda con la que se está interactuando o al final del bloc de notas si no hay ninguna celda en particular enfocada.

* **Mover una celda:** Sitúe el cursor a la derecha de la celda que desee mover y, a continuación, haga clic y arrastre la celda a una nueva ubicación. Además, al mover una celda de un bloc de notas a otro se replica la celda junto con su contenido.

* **Ejecutar una celda:** Haga clic en el cuerpo de la celda que desee ejecutar y, a continuación, haga clic en el icono de **reproducción** (**▶**) en el menú del bloc de notas. Se muestra un asterisco (**\***) en el contador de ejecución de la celda cuando el núcleo está procesando la ejecución y se reemplaza por un entero al finalizar.

* **Eliminar una celda:** Haga clic en el cuerpo de la celda que desee eliminar y, a continuación, haga clic en el icono de la **tijera** .

### Kernels {#kernels}

Los núcleos de los portátiles son los motores informáticos específicos del idioma para procesar las celdas de los portátiles. Además de [!DNL Python], [!DNL JupyterLab] proporciona compatibilidad con idiomas adicionales en R, PySpark y [!DNL Spark] (Scala). Al abrir un documento portátil, se inicia el núcleo asociado. Cuando se ejecuta una celda portátil, el núcleo realiza el cálculo y produce resultados que pueden consumir recursos significativos de CPU y memoria. Tenga en cuenta que la memoria asignada no se libera hasta que se cierre el núcleo.

Algunas funciones y características se limitan a determinados núcleos, como se describe en la tabla siguiente:

| Kernel | Compatibilidad con la instalación de la biblioteca | [!DNL Platform] integraciones |
| :----: | :--------------------------: | :-------------------- |
| **[!DNL Python]** | Sí | <ul><li>[!DNL Sensei ML Framework]</li><li>[!DNL Catalog Service]</li><li>[!DNL Query Service]</li></ul> |
| **R** | Sí | <ul><li>[!DNL Sensei ML Framework]</li><li>[!DNL Catalog Service]</li></ul> |
| **Scala** | No | <ul><li>[!DNL Sensei ML Framework]</li><li>[!DNL Catalog Service]</li></ul> |

### Sesiones de núcleo {#kernel-sessions}

Cada portátil o actividad activa en [!DNL JupyterLab] utiliza una sesión del núcleo. Todas las sesiones activas se pueden encontrar expandiendo la ficha Terminales de **ejecución y núcleos** desde la barra lateral izquierda. El tipo y estado del núcleo para un portátil se puede identificar observando la parte superior derecha de la interfaz del bloc de notas. En el diagrama siguiente, el núcleo asociado al bloc de notas es **[!DNL Python]3 **y su estado actual está representado por un círculo gris a la derecha. Un círculo hueco implica un núcleo de ralentí y un círculo sólido implica un núcleo ocupado.

![](../images/jupyterlab/user-guide/kernel_and_state_1.png)

Si el núcleo está apagado o inactivo durante un período prolongado, entonces ¡ **Sin núcleo!** con un círculo sólido. Active un núcleo haciendo clic en el estado del núcleo y seleccionando el tipo de núcleo apropiado como se muestra a continuación:

![](../images/jupyterlab/user-guide/switch_kernel.gif)

### Iniciador {#launcher}

[//]: # (Talk about the different Notebooks, introduce that certain starter notebooks are limited to particular kernels)

El *iniciador* personalizado le proporciona plantillas de bloc de notas útiles para sus núcleos admitidos que le ayudarán a iniciar su tarea, como:

| Plantilla | Descripción |
| --- | --- |
| En blanco | Un archivo de bloc de notas vacío. |
| Inicio | Un bloc de notas precargado que muestra la exploración de datos mediante datos de ejemplo. |
| Ventas minoristas | Un bloc de notas previamente rellenado que presenta la fórmula <a href="https://adobe.ly/2wOgO3L" target="_blank">de venta al</a> por menor utilizando datos de ejemplo. |
| Generador de fórmulas | Plantilla de bloc de notas para crear una fórmula en [!DNL JupyterLab]. Se rellena previamente con código y comentarios que muestran y describen el proceso de creación de fórmulas. Consulte el tutorial <a href="https://www.adobe.com/go/data-science-create-recipe-notebook-tutorial-en" target="_blank">de fórmula del</a> bloc de notas para obtener un tutorial detallado. |
| [!DNL Query Service] | Un bloc de notas precargado que muestra el uso de [!DNL Query Service] directamente [!DNL JupyterLab] con flujos de trabajo de muestra proporcionados que analizan los datos a escala. |
| Eventos XDM | Un bloc de notas precargado que muestra la exploración de datos en datos de Evento de experiencias con valor posterior, centrado en características comunes en la estructura de datos. |
| Consultas XDM | Un bloc de notas precargado que muestra consultas empresariales de muestra sobre los datos de Experience Evento. |
| Agregación | Un bloc de notas precargado que muestra flujos de trabajo de muestra a grandes cantidades acumuladas de datos en trozos más pequeños y manejables. |
| Clúster | Un bloc de notas precargado que muestra el proceso de modelado integral del aprendizaje automático mediante algoritmos de agrupamiento. |

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

Para abrir un nuevo *iniciador*, haga clic en **Archivo > Nuevo iniciador**. También puede expandir el navegador **de** archivos desde la barra lateral izquierda y hacer clic en el símbolo más (**+**):

![](../images/jupyterlab/user-guide/new_launcher.gif)

### Configuración de GPU y servidor de memoria en [!DNL Python]/R

En [!DNL JupyterLab] seleccione el icono de engranaje en la esquina superior derecha para abrir la configuración *del servidor* portátil. Puede activar la GPU y asignar la cantidad de memoria que necesita con el control deslizante. La cantidad de memoria que puede asignar depende de cuánto haya proporcionado su organización. Seleccione **[!UICONTROL Actualizar configuraciones]** para guardar.

>[!NOTE]
>Solo se aprovisiona una GPU por organización para equipos portátiles. Si la GPU está en uso, debe esperar a que el usuario que la haya reservado en ese momento la publique. Esto se puede hacer cerrando la sesión o dejando la GPU en estado inactivo durante cuatro o más horas.

![](../images/jupyterlab/user-guide/notebook-gpu-config.png)

## Acceso a [!DNL Platform] datos mediante equipos portátiles

Cada núcleo soportado proporciona funcionalidades integradas que permiten leer [!DNL Platform] datos desde un conjunto de datos dentro de un bloc de notas. Sin embargo, la compatibilidad con la paginación de datos está limitada a los blocs de notas [!DNL Python] y R.

### Límites de datos de equipos portátiles

La siguiente información define la cantidad máxima de datos que se pueden leer, qué tipo de datos se han utilizado y el intervalo de tiempo estimado que se tarda en leer los datos. Para [!DNL Python] y R, se utilizó un servidor portátil configurado con 40 GB de RAM para los análisis de rendimiento. Para PySpark y Scala, se utilizó un clúster de databricks configurado en 64 GB de RAM, 8 núcleos, 2 DBU con un máximo de 4 trabajadores para los puntos de referencia que se describen a continuación.

Los datos de esquema de ExperienceEvent utilizados varían en tamaño desde mil (1K) filas hasta mil millones (1B). Tenga en cuenta que para PySpark y las [!DNL Spark] métricas, se utilizó un período de 10 días para los datos XDM.

Los datos de esquemas específicos se preprocesaron mediante [!DNL Query Service] Crear tabla como selección (CTAS). Estos datos también variaron en el tamaño desde mil filas (1K) hasta mil millones (1B).

#### [!DNL Python] límites de datos del bloc de notas

**esquema de ExperienceEvent XDM:** Debería poder leer un máximo de 2 millones de filas (aproximadamente 6,1 GB de datos en disco) de datos XDM en menos de 22 minutos. Añadir filas adicionales puede provocar errores.

| Número de filas | 1K | 10K | 100K | 1M | 2M |
| ----------------------- | ------ | ------ | ----- | ----- | ----- |
| Tamaño en disco (MB) | 18.73 | 187.5 | 308 | 3000 | 6050 |
| SDK (en segundos) | 20.3 | 86.8 | 63 | 659 | 1315 |

**esquema ad-hoc:** Debería poder leer un máximo de 5 millones de filas (unos 5,6 GB de datos en disco) de datos no XDM (ad-hoc) en menos de 14 minutos. Añadir filas adicionales puede provocar errores.

| Número de filas | 1K | 10K | 100K | 1M | 2M | 3M | 5M |
| ----------------------- | ------- | ------- | ----- | ----- | ----- | ----- | ------ |
| Tamaño en disco (en MB) | 1.21 | 11.72 | 115 | 1120 | 2250 | 3380 | 5630 |
| SDK (en segundos) | 7.27 | 9.04 | 27.3 | 180 | 346 | 487 | 819 |

#### Límites de datos del portátil R

**esquema de ExperienceEvent XDM:** Debería poder leer un máximo de 1 millón de filas de datos XDM (datos de 3 GB en disco) en menos de 13 minutos.

| Número de filas | 1K | 10K | 100K | 1M |
| ----------------------- | ------ | ------ | ----- | ----- |
| Tamaño en disco (MB) | 18.73 | 187.5 | 308 | 3000 |
| Núcleo R (en segundos) | 14.03 | 69.6 | 86.8 | 775 |

**esquema ad-hoc:** Debería poder leer un máximo de 3 millones de filas de datos ad-hoc (datos de 293 MB en disco) en unos 10 minutos.

| Número de filas | 1K | 10K | 100K | 1M | 2M | 3M |
| ----------------------- | ------- | ------- | ----- | ----- | ----- | ----- |
| Tamaño en disco (en MB) | 0.082 | 0.612 | 9.0 | 91 | 188 | 293 |
| SDK R (en segundos) | 7.7 | 4.58 | 35.9 | 233 | 470.5 | 603 |

#### Límites de datos de portátiles PySpark ([!DNL Python] núcleo):

**esquema de ExperienceEvent XDM:** En el modo interactivo, debe poder leer un máximo de 5 millones de filas (unos 13,42 GB de datos en disco) de datos XDM en unos 20 minutos. El modo interactivo solo admite hasta 5 millones de filas. Si desea leer conjuntos de datos más grandes, se sugiere cambiar al modo Lote. En el modo Lote, debería poder leer un máximo de 500 millones de filas (unos 1,31 TB de datos en disco) de datos XDM en unas 14 horas.

| Número de filas | 1K | 10K | 100K | 1M | 2M | 3M | 5M | 10M | 50M | 100M | 500M |
|-------------------------|--------|--------|-------|-------|-------|-------|---------|---------|----------|--------|--------|
| Tamaño en disco | 2.93MB | 4.38MB | 29.02 | 2.69 GB   | 5.39 GB   | 8.09 GB   | 13.42 GB   | 26.82 GB   | 134.24 GB   | 268.39 GB   | 1.31TB |
| SDK (modo interactivo) | 33s | 32.4s | 55.1s | 253.5s | 489.2s | 729.6s | 1206.8s | - | - | - | - |
| SDK (modo Lote) | 815.8s | 492.8s | 379.1s | 637.4s | 624.5s | 869.2s | 1104.1s | 1786s | 5387.2s | 10624.6s | 50547s |

**esquema ad-hoc:** En el modo interactivo, debe poder leer un máximo de mil millones de filas (unos 1,05 TB de datos en disco) de datos que no sean XDM en menos de 3 minutos. En el modo Lote, debería poder leer un máximo de mil millones de filas (unos 1,05 TB de datos en disco) de datos que no sean XDM en unos 18 minutos.

| Número de filas | 1K | 10K | 100K | 1M | 2M | 3M | 5M | 10M | 50M | 100M | 500M | 1B |
|--------------|--------|---------|---------|-------|-------|-------|--------|--------|---------|--------|---------|-------|
| Tamaño en disco | 1.12MB | 11.24MB | 109.48MB | 2.69 GB   | 2.14 GB   | 3.21 GB   | 5.36 GB   | 10.71 GB   | 53.58 GB   | 107.52 GB   | 535.88 GB   | 1.05TB |
| Modo interactivo de SDK (en segundos) | 28.2s | 18.6s | 20.8s | 20.9s | 23.8s | 21.7s | 24.7s | 22s | 28.4s | 40s | 97.4s | 154.5s |
| Modo de lotes de SDK (en segundos) | 428.8s | 578.8s | 641.4s | 538.5s | 630.9s | 467.3s | 411s | 675s | 702s | 719.2s | 1022.1s | 1122.3s |

#### [!DNL Spark] Límites de datos de portátiles (kernel Scala):

**esquema de ExperienceEvent XDM:** En el modo interactivo, debe poder leer un máximo de 5 millones de filas (unos 13,42 GB de datos en disco) de datos XDM en unos 18 minutos. El modo interactivo solo admite hasta 5 millones de filas. Si desea leer conjuntos de datos más grandes, se sugiere cambiar al modo Lote. En el modo Lote, debería poder leer un máximo de 500 millones de filas (unos 1,31 TB de datos en disco) de datos XDM en unas 14 horas.

| Número de filas | 1K | 10K | 100K | 1M | 2M | 3M | 5M | 10M | 50M | 100M | 500M |
|---------------|--------|--------|-------|-------|-------|-------|---------|---------|----------|--------|--------|
| Tamaño en disco | 2.93MB | 4.38MB | 29.02 | 2.69 GB   | 5.39 GB   | 8.09 GB   | 13.42 GB   | 26.82 GB   | 134.24 GB   | 268.39 GB   | 1.31TB |
| Modo interactivo de SDK (en segundos) | 37.9s | 22.7s | 45.6s | 231.7s | 444.7s | 660.6s | 1100s | - | - | - | - |
| Modo de lotes de SDK (en segundos) | 374.4s | 398.5s | 527s | 487.9s | 588.9s | 829s | 939.1s | 1441s | 5473.2s | 10118.8 | 49207.6 |

**esquema ad-hoc:** En el modo interactivo, debe poder leer un máximo de mil millones de filas (unos 1,05 TB de datos en disco) de datos que no sean XDM en menos de 3 minutos. En el modo Lote, debería poder leer un máximo de mil millones de filas (unos 1,05 TB de datos en disco) de datos que no sean XDM en unos 16 minutos.

| Número de filas | 1K | 10K | 100K | 1M | 2M | 3M | 5M | 10M | 50M | 100M | 500M | 1B |
|--------------|--------|---------|---------|-------|-------|-------|---------|---------|---------|--------|---------|-------|
| Tamaño en disco | 1.12MB | 11.24MB | 109.48MB | 2.69 GB   | 2.14 GB   | 3.21 GB   | 5.36 GB   | 10.71 GB   | 53.58 GB   | 107.52 GB   | 535.88 GB   | 1.05TB |
| Modo interactivo de SDK (en segundos) | 35.7s | 31s | 19.5s | 25.3s | 23s | 33.2s | 25.5s | 29.2s | 29.7s | 36.9s | 83.5s | 139s |
| Modo de lotes de SDK (en segundos) | 448.8s | 459.7s | 519s | 475.8s | 599.9s | 347.6s | 407.8s | 397s | 518.8s | 487.9s | 760.2s | 975.4s |

### Leer desde un conjunto de datos en [!DNL Python]/R

[!DNL Python] Los blocs de notas y R permiten paginar datos al acceder a conjuntos de datos. A continuación se muestra el código de muestra para leer datos con o sin paginación.

[//]: # (In the following samples, the first step is currently required but once the SDK is complete, users are no longer required to explicitly define client_context)

#### Leer desde un conjunto de datos en [!DNL Python]/R sin paginación

Al ejecutar el siguiente código se leerá todo el conjunto de datos. Si la ejecución se realiza correctamente, los datos se guardarán como un nombre de datos de Pandas al que la variable hace referencia `df`.

```python
# Python

client_context = PLATFORM_SDK_CLIENT_CONTEXT
from platform_sdk.dataset_reader import DatasetReader
dataset_reader = DatasetReader(client_context, "{DATASET_ID}")
df = dataset_reader.read()
df.head()
```

```R
# R

library(reticulate)
use_python("/usr/local/bin/ipython")
psdk <- import("platform_sdk")
py_run_file("../.ipython/profile_default/startup/platform_sdk_context.py")
client_context <- py$PLATFORM_SDK_CLIENT_CONTEXT
DatasetReader <- psdk$dataset_reader$DatasetReader
dataset_reader <- DatasetReader(client_context, "{DATASET_ID}") 
df <- dataset_reader$read() 
df
```

* `{DATASET_ID}`:: Identidad única del conjunto de datos al que se accede

#### Leer desde un conjunto de datos en [!DNL Python]/R con paginación

Al ejecutar el siguiente código se leerán los datos del conjunto de datos especificado. La paginación se logra limitando y compensando los datos a través de las funciones `limit()` y `offset()` respectivamente. La limitación de datos se refiere al número máximo de puntos de datos que se van a leer, mientras que la compensación se refiere al número de puntos de datos que se deben omitir antes de leer los datos. Si la operación de lectura se ejecuta correctamente, los datos se guardarán como un juego de datos de Pandas al que hace referencia la variable `df`.

```python
# Python

client_context = PLATFORM_SDK_CLIENT_CONTEXT
from platform_sdk.dataset_reader import DatasetReader

dataset_reader = DatasetReader(client_context, "{DATASET_ID}")
df = dataset_reader.limit(100).offset(10).read()
```

```R
# R

library(reticulate)
use_python("/usr/local/bin/ipython")
psdk <- import("platform_sdk")
py_run_file("../.ipython/profile_default/startup/platform_sdk_context.py")
client_context <- py$PLATFORM_SDK_CLIENT_CONTEXT

DatasetReader <- psdk$dataset_reader$DatasetReader
dataset_reader <- DatasetReader(client_context, "{DATASET_ID}") 
df <- dataset_reader$limit(100L)$offset(10L)$read() 
```

* `{DATASET_ID}`:: Identidad única del conjunto de datos al que se accede

### Leer desde un conjunto de datos en PySpark/[!DNL Spark]/Scala

Con un bloc de notas PySpark o Scala activo abierto, expanda la ficha Explorador **de** datos desde la barra lateral izquierda y haga clic en **Conjuntos** de datos para vista de una lista de conjuntos de datos disponibles. Haga clic con el botón derecho en la lista de conjuntos de datos a la que desea acceder y haga clic en **Explorar datos en el bloc de notas**. Se generan las siguientes celdas de código:

#### PySpark ([!DNL Spark] 2.4) {#pyspark2.4}

Con la introducción de Spark 2.4, se proporciona [`%dataset`](#magic) magia personalizada.

```python
# PySpark 3 (Spark 2.4)

%dataset read --datasetId {DATASET_ID} --dataFrame pd0
pd0.describe()
pd0.show(10, False)
```

#### Scala ([!DNL Spark] 2.4) {#spark2.4}

```scala
// Scala (Spark 2.4)

// initialize the session
import org.apache.spark.sql.{Dataset, SparkSession}
val spark = SparkSession.builder().master("local").getOrCreate()

val dataFrame = spark.read.format("com.adobe.platform.query")
    .option("user-token", sys.env("PYDASDK_IMS_USER_TOKEN"))
    .option("ims-org", sys.env("IMS_ORG_ID"))
    .option("api-key", sys.env("PYDASDK_IMS_CLIENT_ID"))
    .option("service-token", sys.env("PYDASDK_IMS_SERVICE_TOKEN"))
    .option("mode", "batch")
    .option("dataset-id", "{DATASET_ID}")
    .load()
dataFrame.printSchema()
dataFrame.show()
```

>[!TIP]
>En Scala, puede utilizar `sys.env()` para declarar y devolver un valor desde dentro `option`.

### Uso de la magia de %dataset en los blocs de notas PySpark 3 ([!DNL Spark] 2.4) {#magic}

Con la introducción de [!DNL Spark] 2.4, `%dataset` la magia personalizada se suministra para su uso en los nuevos portátiles PySpark 3 ([!DNL Spark] 2.4) ([!DNL Python] 3 kernel).

**Uso**

`%dataset {action} --datasetId {id} --dataFrame {df}`

**Descripción**

Un comando [!DNL Data Science Workspace] mágico personalizado para leer o escribir un conjunto de datos desde un [!DNL Python] portátil ([!DNL Python] núcleo 3).

* **{action}**: Tipo de acción que se realizará en el conjunto de datos. Hay dos acciones disponibles: &quot;lectura&quot; o &quot;escritura&quot;.
* **—datasetId {id}**: Se utiliza para proporcionar la identificación del conjunto de datos que se va a leer o escribir. Este es un argumento requerido.
* **—dataFrame {df}**: El juego de datos pandas. Este es un argumento requerido.
   * Cuando la acción es &quot;leída&quot;, {df} es la variable donde están disponibles los resultados de la operación de lectura del conjunto de datos.
   * Cuando la acción es &quot;write&quot;, este dataframe {df} se escribe en el conjunto de datos.
* **—mode (opcional)**: Los parámetros permitidos son &quot;batch&quot; e &quot;interactive&quot;. De forma predeterminada, el modo se establece en &quot;interactivo&quot;. Se recomienda utilizar el modo &quot;por lotes&quot; al leer grandes cantidades de datos.

**Ejemplos**

* **Leer ejemplo**: `%dataset read --datasetId 5e68141134492718af974841 --dataFrame pd0`
* **Ejemplo** de escritura: `%dataset write --datasetId 5e68141134492718af974842 --dataFrame pd0`

### Consulta de datos mediante [!DNL Query Service] la [!DNL Python]

[!DNL JupyterLab] on [!DNL Platform] permite utilizar SQL en un [!DNL Python] bloc de notas para acceder a los datos a través del servicio <a href="https://www.adobe.com/go/query-service-home-en" target="_blank">de Consulta de</a>Adobe Experience Platform. El acceso a los datos a través de [!DNL Query Service] puede ser útil para tratar con conjuntos de datos grandes debido a sus tiempos de ejecución superiores. Se debe tener en cuenta que la consulta de datos mediante [!DNL Query Service] el uso tiene un límite de tiempo de procesamiento de diez minutos.

Antes de usar [!DNL Query Service] en [!DNL JupyterLab], asegúrese de comprender bien la sintaxis <a href="https://www.adobe.com/go/query-service-sql-syntax-en" target="_blank">[!DNL Query Service]</a>SQL.

La consulta de datos mediante [!DNL Query Service] requiere que proporcione el nombre del conjunto de datos de destinatario. Puede generar las celdas de código necesarias buscando el conjunto de datos deseado mediante el explorador **de datos**. Haga clic con el botón secundario en la lista de conjuntos de datos y haga clic en Datos de **Consulta en el bloc de notas** para generar las dos celdas de código siguientes en el bloc de notas:


Para utilizar [!DNL Query Service] en [!DNL JupyterLab], primero debe crear una conexión entre su [!DNL Python] portátil de trabajo y [!DNL Query Service]. Esto se puede lograr ejecutando la primera celda generada.

```python
qs_connect()
```

En la segunda celda generada, la primera línea debe definirse antes de la consulta SQL. De forma predeterminada, la celda generada define una variable opcional (`df0`) que guarda los resultados de la consulta como un dataframe de Pandas. <br>El `-c QS_CONNECTION` argumento es obligatorio y le indica al núcleo que ejecute la consulta SQL contra [!DNL Query Service]. Consulte el [apéndice](#optional-sql-flags-for-query-service) para ver una lista de argumentos adicionales.

```python
%%read_sql df0 -c QS_CONNECTION
SELECT *
FROM name_of_the_dataset
LIMIT 10
/* Querying table "name_of_the_dataset" (datasetId: {DATASET_ID})*/
```

Se puede hacer referencia a las variables Python directamente dentro de una consulta SQL utilizando sintaxis con formato de cadena y ajustando las variables entre llaves (`{}`), como se muestra en el siguiente ejemplo:

```python
table_name = 'name_of_the_dataset'
table_columns = ','.join(['col_1','col_2','col_3'])
```

```python
%%read_sql demo -c QS_CONNECTION
SELECT {table_columns}
FROM {table_name}
```

### Filtrar datos de ExperienceEvent en [!DNL Python]/R

Para acceder y filtrar un conjunto de datos de ExperienceEvent en un bloc de notas [!DNL Python] o R, debe proporcionar el ID del conjunto de datos (`{DATASET_ID}`) junto con las reglas de filtro que definen un intervalo de tiempo específico mediante operadores lógicos. Cuando se define un intervalo de tiempo, se ignora cualquier paginación especificada y se considera todo el conjunto de datos.

A continuación se describe una lista de los operadores de filtrado:

* `eq()`: Equal to
* `gt()`: Greater than
* `ge()`: Greater than or equal to
* `lt()`: Less than
* `le()`: Less than or equal to
* `And()`:: Operador AND lógico
* `Or()`:: Operador lógico OR

Las siguientes celdas filtran un conjunto de datos de ExperienceEvent a datos que existen exclusivamente entre el 1 de enero de 2019 y el 31 de diciembre de 2019.

```python
# Python

client_context = PLATFORM_SDK_CLIENT_CONTEXT
from platform_sdk.dataset_reader import DatasetReader

dataset_reader = DatasetReader(client_context, "{DATASET_ID}")
df = dataset_reader.\
    where(dataset_reader["timestamp"].gt("2019-01-01 00:00:00").\
    And(dataset_reader["timestamp"].lt("2019-12-31 23:59:59"))\
).read()
```

```R
# R

library(reticulate)
use_python("/usr/local/bin/ipython")
psdk <- import("platform_sdk")
py_run_file("../.ipython/profile_default/startup/platform_sdk_context.py")
client_context <- py$PLATFORM_SDK_CLIENT_CONTEXT

DatasetReader <- psdk$dataset_reader$DatasetReader
dataset_reader <- DatasetReader(client_context, "{DATASET_ID}") 
df <- dataset_reader$
    where(dataset_reader["timestamp"]$gt("2019-01-01 00:00:00")$
    And(dataset_reader["timestamp"]$lt("2019-12-31 23:59:59"))
)$read()
```

### Filtrar datos de ExperienceEvent en PySpark/[!DNL Spark]

El acceso y filtrado de un conjunto de datos de ExperienceEvent en un bloc de notas de PySpark o Scala requiere que proporcione la identidad del conjunto de datos (`{DATASET_ID}`), la identidad IMS de su organización y las reglas de filtro que definen un intervalo de tiempo específico. Un intervalo de tiempo de filtrado se define mediante la función `spark.sql()`, donde el parámetro de función es una cadena de consulta SQL.

Las siguientes celdas filtran un conjunto de datos de ExperienceEvent a datos que existen exclusivamente entre el 1 de enero de 2019 y el 31 de diciembre de 2019.

#### PySpark 3 ([!DNL Spark] 2.4) {#pyspark3-spark2.4}

```python
# PySpark 3 (Spark 2.4)

from pyspark.sql import SparkSession
spark = SparkSession.builder.getOrCreate()

%dataset read --datasetId {DATASET_ID} --dataFrame df

df.createOrReplaceTempView("event")
timepd = spark.sql("""
    SELECT *
    FROM event
    WHERE timestamp > CAST('2019-01-01 00:00:00.0' AS TIMESTAMP)
    AND timestamp < CAST('2019-12-31 23:59:59.9' AS TIMESTAMP)
""")
timepd.show()
```

#### Scala ([!DNL Spark] 2.4) {#scala-spark}

```scala
// Spark (Spark 2.4)

// Turn off extra logging
import org.apache.log4j.{Level, Logger}
Logger.getLogger("org").setLevel(Level.OFF)
Logger.getLogger("com").setLevel(Level.OFF)

import org.apache.spark.sql.{Dataset, SparkSession}
val spark = org.apache.spark.sql.SparkSession.builder().appName("Notebook")
  .master("local")
  .getOrCreate()

// Stage Exploratory
val dataSetId: String = "{DATASET_ID}"
val orgId: String = sys.env("IMS_ORG_ID")
val clientId: String = sys.env("PYDASDK_IMS_CLIENT_ID")
val userToken: String = sys.env("PYDASDK_IMS_USER_TOKEN")
val serviceToken: String = sys.env("PYDASDK_IMS_SERVICE_TOKEN")
val mode: String = "batch"

var df = spark.read.format("com.adobe.platform.query")
  .option("user-token", userToken)
  .option("ims-org", orgId)
  .option("api-key", clientId)
  .option("mode", mode)
  .option("dataset-id", dataSetId)
  .option("service-token", serviceToken)
  .load()
df.createOrReplaceTempView("event")
val timedf = spark.sql("""
    SELECT * 
    FROM event 
    WHERE timestamp > CAST('2019-01-01 00:00:00.0' AS TIMESTAMP)
    AND timestamp < CAST('2019-12-31 23:59:59.9' AS TIMESTAMP)
""")
timedf.show()
```

>[!TIP]
>En Scala, puede utilizar `sys.env()` para declarar y devolver un valor desde dentro `option`. Esto elimina la necesidad de definir variables si sabe que sólo se van a usar una sola vez. El siguiente ejemplo toma `val userToken` del ejemplo anterior y lo declara en línea dentro de `option` como alternativa:
> 
```scala
> .option("user-token", sys.env("PYDASDK_IMS_USER_TOKEN"))
> ```

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
| jq | 1.6 |
| keras | 2.2.4 |
| nltk | 3.2.5 |
| pandas | 0.22.0 |
| pandasql | 0.7.3 |
| almohada | 6.0.0 |
| scikit-image | 0.15.0 |
| scikit-learn | 0.21.3 |
| scipy | 1.3.0 |
| scrapy | 1.3.0 |
| seaborn | 0.9.0 |
| modelos de estado | 0.10.1 |
| elástico | 5.1.0.17 |
| gráfico | 0.11.5 |
| py-xgboox | 0.90 |
| opencv | 3.4.1 |
| pyspark | 2.4.3 |
| pytorch | 1.0.1 |
| wxpython | 4.0.6 |
| colorlover | 0.3.0 |
| geopandas | 0.5.1 |
| pyshp | 2.1.0 |
| de forma | 1.6.4 |
| rpy2 | 2.9.4 |
| r-essentials | 3.6 |
| r-arules | 1.6_3 |
| r-fpc | 2.2_3 |
| r-e1071 | 1.7_2 |
| r-gam | 1.16.1 |
| r-gbm | 2.1.5 |
| r-temas | 4.2.0 |
| r-ggvis | 0.4.4 |
| r-igraph | 1.2.4.1 |
| r-saltos | 3.0 |
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
| r-rjson | 0.2.20 |
| r-previsión | 8.7 |
| r-resolnp | 1.16 |
| r-reticulate | 1.12 |
| r-mlr | 2.14.0 |
| r-viridis | 0.5.1 |
| r-corplot | 0.84 |
| r-fnn | 1.1.3 |
| r-lubridate | 1.7.4 |
| r-randomforest | 4.6_14 |
| r-tidyverse | 1.2.1 |
| r-tree | 1.0_39 |
| pymongo | 3.8.0 |
| pyarrow | 0.14.1 |
| boto3 | 1.9.199 |
| ipyvolumen | 0.5.2 |
| fastparquet | 0.3.2 |
| python-sndish | 0.5.4 |
| ipywebrtc | 0.5.0 |
| jupyter_client | 5.3.1 |
| wordcloud | 1.5.0 |
| grafviz | 2.40.1 |
| python-graphviz | 0.11.1 |
| azure-almacenamiento | 0.36.0 |
| [!DNL jupyterlab] | 1.0.4 |
| pandas_ml | 0.6.1 |
| tensorflow-gpu | 1.14.0 |
| nodejs | 12.3.0 |
| mock | 3.0.5 |
| ipympl | 0.3.3 |
| fonts-anacond | 1.0 |
| psycopg2 | 2.8.3 |
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
| pandasql | 0.7.3 |
| almohada | 5.3.0 |
| scikit-image | 0.13.0 |
| scikit-learn | 0.19.0 |
| scipy | 0.19.1 |
| scrapy | 1.3.3 |
| modelos de estado | 0.8.0 |
| elástico | 4.0.30.44 |
| py-xgboox | 0.60 |
| opencv | 3.1.0 |
| pyarrow | 0.8.0 |
| boto3 | 1.5.18 |
| azure-almacenamiento-blob | 1.4.0 |
| [!DNL python] | 3.6.7 |
| mkl-rt | 11.1 |

## Indicadores SQL opcionales para [!DNL Query Service] {#optional-sql-flags-for-query-service}

Esta tabla describe los indicadores SQL opcionales para los que se puede utilizar [!DNL Query Service].

| **Indicador** | **Descripción** |
| --- | --- |
| `-h`, `--help` | Muestre el mensaje de ayuda y salga. |
| `-n`, `--notify` | Alternar la opción para notificar los resultados de la consulta. |
| `-a`, `--async` | El uso de este indicador ejecuta la consulta asincrónicamente y puede liberar el núcleo mientras la consulta se está ejecutando. Tenga cuidado al asignar resultados de consulta a variables, ya que podría no estar definida si la consulta no se ha completado. |
| `-d`, `--display` | El uso de este indicador evita que se muestren los resultados. |

