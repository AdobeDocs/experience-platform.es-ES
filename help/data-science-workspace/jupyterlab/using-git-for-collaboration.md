---
keywords: Experience Platform;JupyterLab;blocs de notas;Área de trabajo de ciencias de datos;temas populares;Git;Github
solution: Experience Platform
title: Colaborar en JupyterLab con Git
topic: tutorial
type: Tutorial
description: Git es un sistema de control de versiones distribuido para rastrear los cambios en el código fuente durante el desarrollo de software. Git está preinstalado dentro del entorno de JupyterLab de Área de trabajo de ciencia de datos.
translation-type: tm+mt
source-git-commit: f6cfd691ed772339c888ac34fcbd535360baa116
workflow-type: tm+mt
source-wordcount: '284'
ht-degree: 1%

---


# Colaborar en [!DNL JupyterLab] mediante [!DNL Git]

[!DNL Git] es un sistema de control de versiones distribuido para rastrear los cambios en el código fuente durante el desarrollo del software. Git está preinstalado dentro del entorno [!DNL Data Science Workspace JupyterLab].

## Requisitos previos

>[!NOTE]
>
> El servidor Git que pretendas utilizar debe ser accesible a través de Internet.

El entorno [!DNL Data Science Workspace JupyterLab] es un entorno alojado y no se implementa dentro del servidor de seguridad corporativo, por lo que el servidor Git al que se conecta debe ser accesible desde Internet público. Podría ser un repositorio público o privado en [GitHub](https://github.com/) u otra instancia de un servidor [!DNL Git] que haya decidido alojar usted mismo.

## Conectar [!DNL Git] al entorno [!DNL Data Science Workspace JupyterLab Notebooks]

Inicio iniciando [!DNL Adobe Experience Platform] y navegando al entorno [[!DNL JupyterLabs Notebooks]](https://platform.adobe.com/notebooks/jupyterLab).

Dentro de [!DNL JupyterLab], seleccione **[!UICONTROL Archivo]** y pase el ratón por encima de **[!UICONTROL Nuevo]**. En el menú desplegable que aparece, seleccione **[!UICONTROL Terminal]**.

![JupyterLab Nav](../images/jupyterlab/tutorials/open-terminal.png)

A continuación, en *Terminal* navegue hasta su área de trabajo mediante el siguiente comando: `cd my-workspace`.

![espacio de trabajo de CD](../images/jupyterlab/tutorials/find-workspace.png)

>[!TIP]
>
> Para ver una lista de los comandos git disponibles, ejecute el comando: `git -help` dentro de su terminal.

A continuación, clona el repositorio que desea utilizar con el comando `git clone`. Clona el proyecto con una dirección URL `https://` en lugar de `ssh://`.

**Ejemplo**:

`git clone https://github.com/adobe/experience-platform-dsw-reference.git`

![clone](../images/jupyterlab/tutorials/git-collaboration.png)

>[!NOTE]
>
> Para realizar cualquier operación de escritura (`git push`, por ejemplo) es necesario ejecutar los siguientes comandos de configuración para cada nueva sesión. Tenga en cuenta también que cualquier comando push solicita un nombre de usuario y una contraseña.
>
>`git config --global user.email "you@example.com"`
>
>`git config --global user.name "Your Name"`

## Pasos siguientes

Una vez que haya terminado de clonar su repositorio, puede utilizar Git como lo haría normalmente en su equipo local para colaborar con otros usuarios en portátiles. Para obtener más información sobre lo que puede hacer dentro de [!DNL JupyterLab], consulte [[!DNL JupyterLab user guide]](./overview.md).
