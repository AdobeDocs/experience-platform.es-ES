---
keywords: Experience Platform;inicio;temas populares;fuentes;conectores;conectores de origen;sdk de fuentes;sdk;SDK
solution: Experience Platform
title: Uso de un editor de texto en el entorno local para crear una página de documentación de orígenes
description: Este documento proporciona pasos sobre cómo utilizar el entorno local para crear documentación para el origen y enviar una solicitud de extracción (PR).
exl-id: 4cc89d1d-bc42-473d-ba54-ab3d1a2cd0d6
source-git-commit: e300e57df998836a8c388511b446e90499185705
workflow-type: tm+mt
source-wordcount: '640'
ht-degree: 3%

---

# Utilice un editor de texto en el entorno local para crear una página de documentación de fuentes

Este documento proporciona pasos sobre cómo utilizar el entorno local para crear documentación para el origen y enviar una solicitud de extracción (PR).

>[!TIP]
>
>Los siguientes documentos de la guía de contribución de Adobe se pueden utilizar para respaldar aún más su proceso de documentación: <ul><li>[Instalación de las herramientas de creación de Git y Markdown](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/install-tools.html)</li><li>[Configure el repositorio de Git localmente para la documentación](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html)</li><li>[Flujo de trabajo de contribución en GitHub para cambios importantes](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/full-workflow.html)</li></ul>

## Requisitos previos

El siguiente tutorial requiere que tenga GitHub Desktop instalado en el equipo local. Si no tiene GitHub Desktop, puede descargar la aplicación [aquí](https://desktop.github.com/).

## Conéctese a GitHub y configure su entorno de creación local

El primer paso para configurar el entorno de creación local es ir a [Repositorio de GitHub de Adobe Experience Platform](https://github.com/AdobeDocs/experience-platform.es).

![platform-repo](../assets/platform-repo.png)

En la página principal del repositorio de Platform GitHub, seleccione **Tenedor**.

![Fork (Ramificación)](../assets/fork.png)

Para clonar el repositorio en el equipo local, seleccione **Código**. En el menú desplegable que aparece, seleccione **HTTPS** y, a continuación, seleccione **Abrir con GitHub Desktop**.

>[!TIP]
>
>Para obtener más información, consulte el tutorial sobre [configuración del repositorio de Git localmente para la documentación](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html#create-a-local-clone-of-the-repository).

![open-git-desktop](../assets/open-git-desktop.png)

A continuación, espere unos momentos para que GitHub Desktop clone el `experience-platform.en` repositorio.

![clonación](../assets/cloning.png)

Una vez completado el proceso de clonación, vaya a GitHub Desktop para crear una nueva rama. Seleccionar **Principal** en la barra de navegación superior y, a continuación, seleccione **Nueva rama**

![new-branch](../assets/new-branch.png)

En el panel emergente que aparece, escriba un nombre descriptivo para la rama y, a continuación, seleccione **Crear rama**.

![create-branch-vs](../assets/create-branch-vs.png)

A continuación, seleccione **Publicar rama**.

![publish-branch](../assets/publish-branch.png)

## Crear la página de documentación para el origen

Con el repositorio clonado en el equipo local y una nueva rama creada, ahora puede empezar a crear la página de documentación para el nuevo origen a través de la [editor de texto de su elección](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/install-tools.html#understand-markdown-editors).

El Adobe recomienda que utilice [Código de Visual Studio](https://code.visualstudio.com/) y que instale la extensión de creación de Adobe Markdown. Para instalar la extensión, inicie Visual Studio Code y, a continuación, seleccione **Extensiones** de la barra de navegación izquierda.

![ Extensión](../assets/extension.png)

A continuación, introduzca `Adobe Markdown Authoring` en la barra de búsqueda y seleccione **Instalar** de la página que aparece.

![instalar](../assets/install.png)

Con el equipo local listo, descargue el [plantilla de documentación de orígenes](../assets/api-template.zip) y extraiga el archivo en `experience-platform.en/help/sources/tutorials/api/create/...` con [`...`] que representa la categoría que elija. Por ejemplo, si está creando un origen de base de datos, seleccione la carpeta de base de datos.

Finalmente, siga las instrucciones descritas en la plantilla y edite la plantilla con la información relevante perteneciente a su fuente.

![edit-template](../assets/edit-template.png)

## Envíe su documentación para su revisión

Para crear una solicitud de extracción (PR) y enviar la documentación para su revisión, guarde primero su trabajo en [!DNL Visual Studio Code] (o el editor de texto que haya elegido). A continuación, con GitHub Desktop, introduzca un mensaje de confirmación y seleccione **Compromiso con create-source-documentation**.

![commit-vs](../assets/commit-vs.png)

A continuación, seleccione **Origen push** para cargar su trabajo en la rama remota.

![de origen push](../assets/push-origin.png)

Para crear una solicitud de extracción, seleccione **Crear solicitud de extracción**.

![create-pr-vs](../assets/create-pr-vs.png)

Asegúrese de que las ramas base y de comparación son correctas. Añada una nota al PR, describiendo la actualización y, a continuación, seleccione **Crear solicitud de extracción**. Se abrirá una PR para fusionar la rama de trabajo del trabajo en la rama maestra del repositorio de Adobe.

>[!TIP]
>
>Deje el **Permitir ediciones por responsables** casilla de verificación seleccionada para garantizar que el equipo de documentación de Adobe pueda realizar ediciones en el PR.

![create-pr](../assets/create-pr.png)

Puede confirmar que la solicitud de extracción se ha enviado inspeccionando la pestaña solicitudes de extracción en https://github.com/AdobeDocs/experience-platform.en.

![confirm-pr](../assets/confirm-pr.png)
