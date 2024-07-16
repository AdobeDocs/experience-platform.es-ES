---
keywords: Experience Platform;JupyterLab;blocs de notas;Workspace de ciencia de datos;temas populares;Git;Github
solution: Experience Platform
title: Colaboración en JupyterLab mediante Git
type: Tutorial
description: Git es un sistema de control de versiones distribuido para rastrear cambios en el código fuente durante el desarrollo de software. Git está preinstalado en el entorno de Data Science Workspace JupyterLab.
exl-id: d7b766f7-b97d-4007-bc53-b83742425047
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '280'
ht-degree: 1%

---

# Colaborar en [!DNL JupyterLab] mediante [!DNL Git]

[!DNL Git] es un sistema de control de versiones distribuido para realizar el seguimiento de los cambios en el código fuente durante el desarrollo de software. Git está preinstalado en el entorno [!DNL Data Science Workspace JupyterLab].

## Requisitos previos

>[!NOTE]
>
> El servidor Git que pretenda utilizar debe ser accesible a través de Internet.

El entorno [!DNL Data Science Workspace JupyterLab] es un entorno alojado y no implementado dentro del firewall corporativo y, por lo tanto, el servidor Git al que se conecte debe ser accesible desde la red pública de Internet. Podría ser un repositorio público o privado en [GitHub](https://github.com/) u otra instancia de un servidor [!DNL Git] que usted mismo haya decidido hospedar.

## Conectar [!DNL Git] al entorno [!DNL Data Science Workspace JupyterLab Notebooks]

Comience por iniciar [!DNL Adobe Experience Platform] y navegar al entorno [[!DNL JupyterLabs Notebooks]](https://platform.adobe.com/notebooks/jupyterLab).

En [!DNL JupyterLab], seleccione **[!UICONTROL Archivo]** y luego pase el ratón sobre **[!UICONTROL Nuevo]**. En el menú desplegable que aparece, seleccione **[!UICONTROL Terminal]**.

![JupyterLab Nav](../images/jupyterlab/tutorials/open-terminal.png)

A continuación, en *Terminal*, desplácese hasta el área de trabajo mediante el siguiente comando: `cd my-workspace`.

![espacio de trabajo en cd](../images/jupyterlab/tutorials/find-workspace.png)

>[!TIP]
>
> Para ver una lista de los comandos de Git disponibles, emita el comando: `git -help` en el terminal.

A continuación, clone el repositorio que desea utilizar con el comando `git clone`. Clone su proyecto mediante una dirección URL `https://` en lugar de `ssh://`.

**Ejemplo**:

`git clone https://github.com/adobe/experience-platform-dsw-reference.git`

![clon](../images/jupyterlab/tutorials/git-collaboration.png)

>[!NOTE]
>
> Para realizar cualquier operación de escritura (`git push`, por ejemplo), se deben ejecutar los siguientes comandos de configuración en cada nueva sesión. Tenga en cuenta también que cualquier comando push solicita un nombre de usuario y una contraseña.
>
>`git config --global user.email "you@example.com"`
>
>`git config --global user.name "Your Name"`

## Pasos siguientes

Una vez que haya terminado de clonar el repositorio, puede utilizar Git como lo haría normalmente en su equipo local para colaborar con otros en portátiles. Para obtener más información sobre lo que puede hacer en [!DNL JupyterLab], consulte [[!DNL JupyterLab user guide]](./overview.md).
