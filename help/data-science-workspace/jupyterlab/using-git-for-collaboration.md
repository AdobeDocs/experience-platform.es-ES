---
keywords: Experience Platform;JupyterLab;blocs de notas;Data Science Workspace;temas populares;Git;Github
solution: Experience Platform
title: Colaborar en JupyterLab mediante Git
type: Tutorial
description: Git es un sistema distribuido de control de versiones para rastrear cambios en el código fuente durante el desarrollo del software. Git está preinstalado en el entorno JupyterLab de Data Science Workspace.
exl-id: d7b766f7-b97d-4007-bc53-b83742425047
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '284'
ht-degree: 1%

---

# Colaborar en [!DNL JupyterLab] using [!DNL Git]

[!DNL Git] es un sistema distribuido de control de versiones para rastrear cambios en el código fuente durante el desarrollo del software. Git está preinstalado dentro de [!DNL Data Science Workspace JupyterLab] entorno.

## Requisitos previos

>[!NOTE]
>
> El servidor Git que pretenda utilizar debe ser accesible a través de Internet.

La variable [!DNL Data Science Workspace JupyterLab] es un entorno alojado y no se implementa dentro del cortafuegos corporativo, por lo que el servidor Git al que se conecta debe ser accesible desde la Internet pública. Podría ser un repositorio público o privado en [GitHub](https://github.com/) u otra instancia de un [!DNL Git] servidor que ha decidido alojar usted mismo.

## Connect [!DNL Git] a [!DNL Data Science Workspace JupyterLab Notebooks] entorno

Comience iniciando [!DNL Adobe Experience Platform] y vaya a la [[!DNL JupyterLabs Notebooks]](https://platform.adobe.com/notebooks/jupyterLab) entorno.

Within [!DNL JupyterLab], seleccione **[!UICONTROL Archivo]** pase el ratón por encima **[!UICONTROL Nuevo]**. En el menú desplegable que aparece, seleccione **[!UICONTROL Terminal]**.

![Navegación de JupyterLab](../images/jupyterlab/tutorials/open-terminal.png)

A continuación, en *Terminal* vaya al espacio de trabajo mediante el siguiente comando: `cd my-workspace`.

![espacio de trabajo del cd](../images/jupyterlab/tutorials/find-workspace.png)

>[!TIP]
>
> Para ver una lista de comandos git disponibles, ejecute el comando: `git -help` en su terminal.

A continuación, clone el repositorio que desee utilizar con el `git clone` comando. Clonar el proyecto mediante una `https://` URL en lugar de `ssh://`.

**Ejemplo**:

`git clone https://github.com/adobe/experience-platform-dsw-reference.git`

![clone](../images/jupyterlab/tutorials/git-collaboration.png)

>[!NOTE]
>
> Para realizar cualquier operación de escritura (`git push` por ejemplo) los siguientes comandos de configuración deben ejecutarse para cada nueva sesión. Tenga en cuenta también que cualquier comando push solicita un nombre de usuario y una contraseña.
>
>`git config --global user.email "you@example.com"`
>
>`git config --global user.name "Your Name"`

## Pasos siguientes

Una vez que haya terminado de clonar su repositorio, puede utilizar Git como lo haría normalmente en su equipo local para colaborar con otros en portátiles. Para obtener más información sobre lo que puede hacer en [!DNL JupyterLab], consulte la [[!DNL JupyterLab user guide]](./overview.md).
