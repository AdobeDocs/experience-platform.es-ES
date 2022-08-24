---
keywords: Experience Platform;inicio;temas populares;orígenes;conectores;conectores de origen;sdk de fuentes;sdk;SDK
solution: Experience Platform
title: Utilizar un editor de texto en el entorno local para crear una página de documentación de fuentes
topic-legacy: tutorial
description: Este documento proporciona pasos sobre cómo utilizar el entorno local para crear documentación para el origen y enviar una solicitud de extracción (PR).
exl-id: 4cc89d1d-bc42-473d-ba54-ab3d1a2cd0d6
source-git-commit: 4d7799b01c34f4b9e4a33c130583eadcfdc3af69
workflow-type: tm+mt
source-wordcount: '650'
ht-degree: 3%

---

# Utilice un editor de texto en el entorno local para crear una página de documentación de fuentes

Este documento proporciona pasos sobre cómo utilizar el entorno local para crear documentación para el origen y enviar una solicitud de extracción (PR).

>[!TIP]
>
>Los siguientes documentos de la guía de contribución de Adobe se pueden utilizar para respaldar aún más su proceso de documentación: <ul><li>[Instalación de las herramientas de creación de Git y Markdown](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/install-tools.html?lang=en)</li><li>[Configure el repositorio de Git localmente para la documentación](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html?lang=en)</li><li>[Flujo de trabajo de contribución en GitHub para cambios importantes](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/full-workflow.html?lang=en)</li></ul>

## Requisitos previos

El siguiente tutorial requiere que tenga GitHub Desktop instalado en el equipo local. Si no tiene GitHub Desktop, puede descargar la aplicación [here](https://desktop.github.com/).

## Conéctese a GitHub y configure su entorno de creación local

El primer paso para configurar el entorno de creación local es ir al [Repositorio de Adobe Experience Platform GitHub](https://github.com/AdobeDocs/experience-platform.en).

![platform-repo](../assets/platform-repo.png)

En la página principal del repositorio de Platform GitHub, seleccione **Bifurcación (Fork)**.

![Fork (Ramificación)](../assets/fork.png)

Para clonar el repositorio en el equipo local, seleccione **Código**. En el menú desplegable que aparece, seleccione **HTTPS** y, a continuación, seleccione **Abrir con GitHub Desktop**.

>[!TIP]
>
>Para obtener más información, consulte el tutorial sobre [configuración del repositorio de Git localmente para la documentación](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html?lang=en#create-a-local-clone-of-the-repository).

![open-git-desktop](../assets/open-git-desktop.png)

A continuación, espere unos momentos para que GitHub Desktop clone el `experience-platform.en` repositorio.

![clonación](../assets/cloning.png)

Una vez completado el proceso de clonación, vaya a GitHub Desktop para crear una rama nueva. Select **Maestro** en la barra de navegación superior y, a continuación, seleccione **Nueva rama**

![rama nueva](../assets/new-branch.png)

En el panel emergente que aparece, introduzca un nombre descriptivo para la rama y, a continuación, seleccione **Crear rama**.

![create-branch-vs](../assets/create-branch-vs.png)

A continuación, seleccione **Rama de publicación**.

![publish-branch](../assets/publish-branch.png)

## Cree la página de documentación para el origen

Con el repositorio clonado en el equipo local y una rama nueva creada, ahora puede empezar a crear la página de documentación para el nuevo origen a través del [editor de texto de su elección](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/install-tools.html?lang=en#understand-markdown-editors).

Adobe recomienda usar [Código de Visual Studio](https://code.visualstudio.com/) y que instale la extensión de creación de Adobe Markdown. Para instalar la extensión, inicie Visual Studio Code y, a continuación, seleccione la variable **Extensiones** de la barra de navegación izquierda.

![ Extensión](../assets/extension.png)

A continuación, introduzca `Adobe Markdown Authoring` en la barra de búsqueda y, a continuación, seleccione **Instalar** de la página que aparece.

![instalar](../assets/install.png)

Con el equipo local listo, descargue el [plantilla de documentación de fuentes](../assets/template.zip) y extraer el archivo a `experience-platform.en/help/sources/tutorials/api/create/...` con [`...`] que representan la categoría que elija. Por ejemplo, si está creando un origen de base de datos, seleccione la carpeta de la base de datos.

Finalmente, siga las instrucciones descritas en la plantilla y edite la plantilla con la información relevante relacionada con su fuente.

![edit-template](../assets/edit-template.png)

## Envíe su documentación para su revisión

Para crear una solicitud de extracción (PR) y enviar la documentación para su revisión, guarde primero su trabajo en [!DNL Visual Studio Code] (o el editor de texto elegido). A continuación, con GitHub Desktop, introduzca un mensaje de confirmación y seleccione **Confirmar para create-source-documentation**.

![commit-vs](../assets/commit-vs.png)

A continuación, seleccione **Origen push** para cargar el trabajo en la rama remota.

![push-origin](../assets/push-origin.png)

Para crear una solicitud de extracción, seleccione **Crear solicitud de extracción**.

![create-pr-vs](../assets/create-pr-vs.png)

Asegúrese de que la base y las ramas comparadas sean correctas. Agregue una nota a la PR, describa su actualización y, a continuación, seleccione **Crear solicitud de extracción**. Esto abre una PR para fusionar la rama de trabajo del trabajo en la rama maestra del repositorio de Adobe.

>[!TIP]
>
>Deje el **Permitir ediciones por parte de los administradores** casilla de verificación seleccionada para garantizar que el equipo de documentación de Adobe pueda realizar modificaciones en PR.

![create-pr](../assets/create-pr.png)

Puede confirmar que la solicitud de extracción se ha enviado inspeccionando la pestaña de solicitudes de extracción en https://github.com/AdobeDocs/experience-platform.en.

![confirm-pr](../assets/confirm-pr.png)
