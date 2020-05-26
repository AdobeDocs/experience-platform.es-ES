---
keywords: Experience Platform;JupyterLab;notebooks;Data Science Workspace;popular topics;Git;Github
solution: Experience Platform
title: Colaborar en JupyterLab mediante Git
topic: Tutorial
translation-type: tm+mt
source-git-commit: 0134c21bc35c0cb1bde7f0201a33517a81addae3
workflow-type: tm+mt
source-wordcount: '276'
ht-degree: 1%

---


# Colaborar en JupyterLab mediante Git

Git es un sistema de control de versiones distribuido para rastrear los cambios en el código fuente durante el desarrollo de software. Git está preinstalado dentro del entorno de JupyterLab de Área de trabajo de ciencia de datos.

## Requisitos previos

>[!NOTE]
> El servidor Git que pretendas utilizar debe ser accesible a través de Internet.

El entorno de Data Science Workspace JupyterLab es un entorno alojado y no se implementa dentro del cortafuegos corporativo, por lo que el servidor Git al que se conecta debe ser accesible desde la Internet pública. Podría ser un repositorio público o privado en [GitHub](https://github.com/) u otra instancia de un servidor Git que usted haya decidido albergar.

## Conectar Git al entorno de portátiles JupyterLab de Data Science Workspace

Inicio iniciando Adobe Experience Platform y navegando hasta el entorno [JupyterLabs Notebooks](https://platform.adobe.com/notebooks/jupyterLab) .

En JupyterLab, seleccione **[!UICONTROL Archivo]** y, a continuación, pase el ratón sobre **[!UICONTROL Nuevo]**. En el menú desplegable que aparece, seleccione **[!UICONTROL Terminal]**.

![JupyterLab Nav](../images/jupyterlab/tutorials/open-terminal.png)

A continuación, en *Terminal* vaya al espacio de trabajo mediante el siguiente comando: `cd my-workspace`.

![espacio de trabajo de CD](../images/jupyterlab/tutorials/find-workspace.png)

>[!TIP]
> Para ver una lista de los comandos git disponibles, ejecute el comando: `git -help` en su terminal.

A continuación, clona el repositorio que desea utilizar con el `git clone` comando. Clona el proyecto con una `https://` dirección URL en lugar de `ssh://`.

**Ejemplo**:

`git clone https://github.com/adobe/experience-platform-dsw-reference.git`

![clone](../images/jupyterlab/tutorials/git-collaboration.png)

>[!NOTE]
> Para realizar cualquier operación de escritura (`git push` por ejemplo) es necesario ejecutar los siguientes comandos de configuración para cada nueva sesión. Tenga en cuenta también que cualquier comando push solicita un nombre de usuario y una contraseña.
>
>`git config --global user.email "you@example.com"`
>
>`git config --global user.name "Your Name"`

## Pasos siguientes

Una vez que haya terminado de clonar su repositorio, puede utilizar Git como lo haría normalmente en su equipo local para colaborar con otros usuarios en portátiles. Para obtener más información sobre lo que puede hacer en JupyterLab, consulte la guía del usuario de [JupyterLab](./overview.md).
