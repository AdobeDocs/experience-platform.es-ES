---
keywords: Experience Platform;JupyterLab;notebooks;Data Science Workspace;popular topics;Git;Github
solution: Experience Platform
title: Colaborar en JupyterLab mediante Git
topic: Tutorial
translation-type: tm+mt
source-git-commit: 690ddbd92f0a2e4e06b988e761dabff399cd2367
workflow-type: tm+mt
source-wordcount: '248'
ht-degree: 1%

---


# Colaborar en el [!DNL JupyterLab] uso [!DNL Git]

[!DNL Git] es un sistema de control de versiones distribuido para rastrear los cambios en el código fuente durante el desarrollo del software. Git está preinstalado dentro del [!DNL Data Science Workspace JupyterLab] entorno.

## Requisitos previos

>[!NOTE]
>
> El servidor Git que pretendas utilizar debe ser accesible a través de Internet.

El [!DNL Data Science Workspace JupyterLab] entorno es un entorno alojado y no se implementa dentro del servidor de seguridad de su empresa, por lo que el servidor Git al que se conecta debe ser accesible desde la Internet pública. Podría ser un repositorio público o privado en [GitHub](https://github.com/) u otra instancia de un [!DNL Git] servidor que usted haya decidido albergar.

## Conectar [!DNL Git] al [!DNL Data Science Workspace JupyterLab Notebooks] entorno

Inicio iniciando [!DNL Adobe Experience Platform] y navegando al [!DNL JupyterLabs Notebooks](https://platform.adobe.com/notebooks/jupyterLab) entorno.

En [!DNL JupyterLab], seleccione **[!UICONTROL Archivo]** y, a continuación, pase el ratón sobre **[!UICONTROL Nuevo]**. En el menú desplegable que aparece, seleccione **[!UICONTROL Terminal]**.

![JupyterLab Nav](../images/jupyterlab/tutorials/open-terminal.png)

A continuación, en *Terminal* vaya al espacio de trabajo mediante el siguiente comando: `cd my-workspace`.

![espacio de trabajo de CD](../images/jupyterlab/tutorials/find-workspace.png)

>[!TIP]
>
> Para ver una lista de los comandos git disponibles, ejecute el comando: `git -help` en su terminal.

A continuación, clona el repositorio que desea utilizar con el `git clone` comando. Clona el proyecto con una `https://` dirección URL en lugar de `ssh://`.

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

Una vez que haya terminado de clonar su repositorio, puede utilizar Git como lo haría normalmente en su equipo local para colaborar con otros usuarios en portátiles. Para obtener más información sobre lo que puede hacer dentro de [!DNL JupyterLab], consulte la [!DNL JupyterLab user guide](./overview.md).
