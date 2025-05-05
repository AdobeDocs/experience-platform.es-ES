---
keywords: Experience Platform;inicio;temas populares;fuentes;conectores;conectores de origen;fuentes sdk;sdk;SDK
solution: Experience Platform
title: Uso de un editor de texto en el entorno local para crear una página de documentación de orígenes
description: Este documento proporciona pasos sobre cómo utilizar el entorno local para crear documentación para el origen y enviar una solicitud de extracción (PR).
exl-id: 4cc89d1d-bc42-473d-ba54-ab3d1a2cd0d6
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '601'
ht-degree: 0%

---

# Utilice un editor de texto en el entorno local para crear una página de documentación de fuentes

Este documento proporciona pasos sobre cómo utilizar el entorno local para crear documentación para el origen y enviar una solicitud de extracción (PR).

>[!TIP]
>
>Los siguientes documentos de la guía de contribución de Adobe se pueden utilizar para respaldar aún más su proceso de documentación: <ul><li>[Instalar las herramientas de creación de Git y Markdown](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/install-tools.html?lang=es)</li><li>[Configurar el repositorio Git localmente para la documentación](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html?lang=es)</li><li>[Flujo de trabajo de contribución en GitHub para cambios importantes](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/full-workflow.html?lang=es)</li></ul>

## Requisitos previos

El siguiente tutorial requiere que tenga GitHub Desktop instalado en el equipo local. Si no tiene GitHub Desktop, puede descargar la aplicación [aquí](https://desktop.github.com/).

## Conéctese a GitHub y configure su entorno de creación local

El primer paso para configurar el entorno de creación local es ir al [repositorio de GitHub de Adobe Experience Platform](https://github.com/AdobeDocs/experience-platform.es).

![platform-repo](../assets/platform-repo.png)

En la página principal del repositorio de GitHub de Experience Platform, seleccione **Fork**.

![bifurcación](../assets/fork.png)

Para clonar el repositorio en el equipo local, seleccione **Código**. En el menú desplegable que aparece, seleccione **HTTPS** y, a continuación, seleccione **Abrir con GitHub Desktop**.

>[!TIP]
>
>Para obtener más información, consulte el tutorial sobre [configuración local del repositorio Git para la documentación](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html?lang=es#create-a-local-clone-of-the-repository).

![open-git-desktop](../assets/open-git-desktop.png)

A continuación, espere unos momentos para que GitHub Desktop clone el repositorio `experience-platform.en`.

![clonando](../assets/cloning.png)

Una vez completado el proceso de clonación, vaya a GitHub Desktop para crear una nueva rama. Seleccione **Principal** en la barra de navegación superior y luego seleccione **Nueva rama**

![rama nueva](../assets/new-branch.png)

En el panel emergente que aparece, escriba un nombre descriptivo para la rama y, a continuación, seleccione **Crear rama**.

![create-branch-vs](../assets/create-branch-vs.png)

A continuación, seleccione **Publicar rama**.

![rama de publicación](../assets/publish-branch.png)

## Crear la página de documentación para el origen

Con el repositorio clonado en el equipo local y una nueva rama creada, ahora puedes empezar a crear la página de documentación para tu nuevo origen a través del [editor de texto que elijas](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/install-tools.html?lang=es#understand-markdown-editors).

Adobe recomienda usar [Visual Studio Code](https://code.visualstudio.com/) e instalar la extensión de Adobe Markdown Authoring. Para instalar la extensión, inicie Visual Studio Code y, a continuación, seleccione la ficha **Extensiones** en el panel de navegación izquierdo.

![ Extensión](../assets/extension.png)

A continuación, escriba `Adobe Markdown Authoring` en la barra de búsqueda y seleccione **Instalar** en la página que aparece.

![instalar](../assets/install.png)

Con el equipo local listo, descargue la [plantilla de documentación de orígenes](../assets/api-template.zip) y extraiga el archivo en `experience-platform.en/help/sources/tutorials/api/create/...`, donde [`...`] representa la categoría que elija. Por ejemplo, si está creando un origen de base de datos, seleccione la carpeta de base de datos.

Finalmente, siga las instrucciones descritas en la plantilla y edite la plantilla con la información relevante perteneciente a su fuente.

![editar-plantilla](../assets/edit-template.png)

## Envíe su documentación para su revisión

Para crear una solicitud de extracción (PR) y enviar la documentación para su revisión, primero guarde el trabajo en [!DNL Visual Studio Code] (o en el editor de texto que haya elegido). A continuación, con GitHub Desktop, introduzca un mensaje de confirmación y seleccione **Confirmar para crear-documentación-origen**.

![compromiso frente a](../assets/commit-vs.png)

A continuación, seleccione **Origen push** para cargar el trabajo en la rama remota.

![push-origin](../assets/push-origin.png)

Para crear una solicitud de extracción, seleccione **Crear solicitud de extracción**.

![create-pr-vs](../assets/create-pr-vs.png)

Asegúrese de que las ramas base y de comparación son correctas. Agregue una nota al PR, describiendo su actualización, y luego seleccione **Crear solicitud de extracción**. Se abrirá una PR para fusionar la rama de trabajo del trabajo en la rama maestra del repositorio de Adobe.

>[!TIP]
>
>Deje seleccionada la casilla de verificación **Permitir ediciones por responsables** para garantizar que el equipo de documentación de Adobe pueda realizar ediciones en la PR.

![crear-pr](../assets/create-pr.png)

Puede confirmar que la solicitud de extracción se ha enviado inspeccionando la pestaña solicitudes de extracción en https://github.com/AdobeDocs/experience-platform.en.

![confirmar-pr](../assets/confirm-pr.png)
