---
keywords: Experience Platform;JupyterLab;blocs de notas;Data Science Workspace;temas populares;Git;Github
solution: Experience Platform
title: Colaboración en JupyterLab mediante Git
type: Tutorial
description: Git es un sistema de control de versiones distribuido para rastrear cambios en el código fuente durante el desarrollo de software. Git está preinstalado en el entorno de JupyterLab de Data Science Workspace.
exl-id: d7b766f7-b97d-4007-bc53-b83742425047
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '284'
ht-degree: 1%

---

# Colaboración en [!DNL JupyterLab] usando [!DNL Git]

[!DNL Git] es un sistema de control de versiones distribuido para realizar un seguimiento de los cambios en el código fuente durante el desarrollo de software. Git está preinstalado en el [!DNL Data Science Workspace JupyterLab] entorno.

## Requisitos previos

>[!NOTE]
>
> El servidor Git que pretenda utilizar debe ser accesible a través de Internet.

El [!DNL Data Science Workspace JupyterLab] El entorno de es un entorno alojado y no implementado dentro del cortafuegos corporativo. Por lo tanto, el servidor Git al que se conecte debe ser accesible desde la red pública de Internet. Podría ser un repositorio público o privado en [GitHub](https://github.com/) u otra instancia de un [!DNL Git] servidor que ha decidido alojar usted mismo.

## Connect [!DNL Git] a la [!DNL Data Science Workspace JupyterLab Notebooks] entorno

Comience por iniciar [!DNL Adobe Experience Platform] y navegación al [[!DNL JupyterLabs Notebooks]](https://platform.adobe.com/notebooks/jupyterLab) entorno.

En [!DNL JupyterLab], seleccione **[!UICONTROL Archivo]** luego, pase el ratón sobre **[!UICONTROL Nuevo]**. En la lista desplegable que aparece, seleccione **[!UICONTROL Terminal]**.

![JupyterLab Nav](../images/jupyterlab/tutorials/open-terminal.png)

Siguiente, en *Terminal* vaya al espacio de trabajo con el siguiente comando: `cd my-workspace`.

![cd workspace](../images/jupyterlab/tutorials/find-workspace.png)

>[!TIP]
>
> Para ver una lista de los comandos de Git disponibles, emita el comando: `git -help` en el terminal.

A continuación, clone el repositorio que desea utilizar con el `git clone` comando. Clone su proyecto mediante una `https://` URL en lugar de `ssh://`.

**Ejemplo**:

`git clone https://github.com/adobe/experience-platform-dsw-reference.git`

![clonar](../images/jupyterlab/tutorials/git-collaboration.png)

>[!NOTE]
>
> Para realizar cualquier operación de escritura (`git push` por ejemplo) los siguientes comandos de configuración deben ejecutarse para cada nueva sesión. Tenga en cuenta también que cualquier comando push solicita un nombre de usuario y una contraseña.
>
>`git config --global user.email "you@example.com"`
>
>`git config --global user.name "Your Name"`

## Pasos siguientes

Una vez que haya terminado de clonar el repositorio, puede utilizar Git como lo haría normalmente en su equipo local para colaborar con otros en portátiles. Para obtener más información sobre lo que puede hacer dentro de [!DNL JupyterLab], consulte la [[!DNL JupyterLab user guide]](./overview.md).
