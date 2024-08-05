---
keywords: Experience Platform; JupyterLab; Cuadernos; Data Science Espacio de trabajo; temas populares; Git; Concentrador de Github
solution: Experience Platform
title: Colabore en JupyterLab usando Git
type: Tutorial
description: Git es un sistema de control de versiones distribuido para rastrear cambios en el código fuente durante el desarrollo de software. Git está preinstalado en el entorno de Ciencia de datos Espacio de trabajo JupyterLab.
exl-id: d7b766f7-b97d-4007-bc53-b83742425047
source-git-commit: 5d98dc0cbfaf3d17c909464311a33a03ea77f237
workflow-type: tm+mt
source-wordcount: '303'
ht-degree: 1%

---

# Colabore en el [!DNL JupyterLab] uso de [!DNL Git]

>[!NOTE]
>
>La Espacio de trabajo de ciencia de datos ya no está disponible para su compra.
>
>Esta documentación está destinada a clientes existentes con derechos previos a Data Science Espacio de trabajo.

[!DNL Git] es un sistema distribuido de control de versiones para seguimiento cambios en el código fuente durante el desarrollo de software. Git está preinstalado dentro del [!DNL Data Science Workspace JupyterLab] entorno.

## Requisitos previos

>[!NOTE]
>
> El servidor Git que desee utilizar debe ser accesible a través de Internet.

El [!DNL Data Science Workspace JupyterLab] entorno es un entorno alojado y no está implementado dentro de su firewall corporativo y, por lo tanto, el servidor Git al que se conecta debe ser accesible desde la Internet pública. Podría ser un repositorio público o privado en [GitHub](https://github.com/) u otro instancia de un [!DNL Git] servidor que haya decidido host usted mismo.

## Conéctese [!DNL Git] al [!DNL Data Science Workspace JupyterLab Notebooks] entorno

Comience por iniciar [!DNL Adobe Experience Platform] y navegar al entorno [[!DNL JupyterLabs Notebooks]](https://platform.adobe.com/notebooks/jupyterLab).

En [!DNL JupyterLab], seleccione **[!UICONTROL Archivo]** y pase el ratón sobre **[!UICONTROL Nuevo]**. En el menú desplegable que aparece, selecciona **[!UICONTROL Terminal]**.

![JupyterLab Nav](../images/jupyterlab/tutorials/open-terminal.png)

Siguiente, dentro de *Terminal* , vaya a su espacio de trabajo mediante el siguiente comando: `cd my-workspace`.

![espacio de trabajo de CD](../images/jupyterlab/tutorials/find-workspace.png)

>[!TIP]
>
> Para ver una lista de comandos git disponibles, ejecute el comando: `git -help` dentro de su Terminal.

Siguiente, clona el repositorio que deseas usar usando el `git clone` comando. Clonar el proyecto usando un `https://` URL en lugar de `ssh://`.

**Ejemplo**:

`git clone https://github.com/adobe/experience-platform-dsw-reference.git`

![clon](../images/jupyterlab/tutorials/git-collaboration.png)

>[!NOTE]
>
> Para realizar cualquier operación de escritura (`git push` por ejemplo), es necesario ejecutar los siguientes comandos de configuración para cada nueva sesión. Tenga en cuenta también que cualquier comando push solicita un nombre de usuario y un contraseña.
>
>`git config --global user.email "you@example.com"`
>
>`git config --global user.name "Your Name"`

## Pasos siguientes

Cuando haya terminado de clonar su repositorio, puede usar Git como lo haría normalmente en su máquina local para colaborar con otros usuarios en blocs de notas. Para obtener más información sobre lo que puede hacer dentro de [!DNL JupyterLab], consulte .[[!DNL JupyterLab user guide]](./overview.md)
