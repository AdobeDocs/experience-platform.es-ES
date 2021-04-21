---
keywords: Experience Platform;JupyterLab;blocs de notas;Data Science Workspace;temas populares;Git;Github
solution: Experience Platform
title: Colaborar en JupyterLab mediante Git
topic-legacy: tutorial
type: Tutorial
description: Git es un sistema distribuido de control de versiones para rastrear cambios en el código fuente durante el desarrollo del software. Git está preinstalado en el entorno JupyterLab de Data Science Workspace.
exl-id: d7b766f7-b97d-4007-bc53-b83742425047
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '281'
ht-degree: 1%

---

# Colaborar en [!DNL JupyterLab] mediante [!DNL Git]

[!DNL Git] es un sistema distribuido de control de versiones para rastrear cambios en el código fuente durante el desarrollo del software. Git está preinstalado dentro del entorno [!DNL Data Science Workspace JupyterLab] .

## Requisitos previos

>[!NOTE]
>
> El servidor Git que pretenda utilizar debe ser accesible a través de Internet.

El entorno [!DNL Data Science Workspace JupyterLab] es un entorno alojado y no se implementa dentro del firewall corporativo, por lo que el servidor Git al que se conecta debe ser accesible desde la Internet pública. Podría ser un repositorio público o privado en [GitHub](https://github.com/) u otra instancia de un servidor [!DNL Git] que haya decidido alojar usted mismo.

## Conecte [!DNL Git] al entorno [!DNL Data Science Workspace JupyterLab Notebooks]

Comience iniciando [!DNL Adobe Experience Platform] y navegando al entorno [[!DNL JupyterLabs Notebooks]](https://platform.adobe.com/notebooks/jupyterLab).

Dentro de [!DNL JupyterLab], seleccione **[!UICONTROL File]** y pase el ratón por encima de **[!UICONTROL New]**. En el menú desplegable que aparece, seleccione **[!UICONTROL Terminal]**.

![Navegación de JupyterLab](../images/jupyterlab/tutorials/open-terminal.png)

A continuación, en *Terminal* vaya al espacio de trabajo mediante el siguiente comando: `cd my-workspace`.

![espacio de trabajo del cd](../images/jupyterlab/tutorials/find-workspace.png)

>[!TIP]
>
> Para ver una lista de comandos git disponibles, ejecute el comando: `git -help` dentro de su terminal.

A continuación, clone el repositorio que desea utilizar utilizando el comando `git clone`. Clona el proyecto con una dirección URL `https://` en lugar de `ssh://`.

**Ejemplo**:

`git clone https://github.com/adobe/experience-platform-dsw-reference.git`

![clone](../images/jupyterlab/tutorials/git-collaboration.png)

>[!NOTE]
>
> Para realizar cualquier operación de escritura (`git push` por ejemplo) es necesario ejecutar los siguientes comandos de configuración para cada nueva sesión. Tenga en cuenta también que cualquier comando push solicita un nombre de usuario y una contraseña.
>
>`git config --global user.email "you@example.com"`
>
>`git config --global user.name "Your Name"`

## Pasos siguientes

Una vez que haya terminado de clonar su repositorio, puede utilizar Git como lo haría normalmente en su equipo local para colaborar con otros en portátiles. Para obtener más información sobre lo que puede hacer en [!DNL JupyterLab], consulte [[!DNL JupyterLab user guide]](./overview.md).
