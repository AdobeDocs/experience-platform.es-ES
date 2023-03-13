---
title: Utilice un editor de texto en el entorno local para crear una página de documentación de destino
description: Las instrucciones de esta página muestran cómo utilizar un editor de texto para trabajar en su entorno local, crear una página de documentación para el destino del Experience Platform y enviarla para su revisión.
exl-id: 125f2d10-0190-4255-909c-5bd5bb59fcba
source-git-commit: 1bbff0fa54f1b7ef1ee70efd2a85cd43b34b2f5a
workflow-type: tm+mt
source-wordcount: '885'
ht-degree: 2%

---

# Utilice un editor de texto en el entorno local para crear una página de documentación de destino {#local-authoring}

Las instrucciones de esta página muestran cómo utilizar un editor de texto para trabajar en el entorno local, crear documentación y enviar una solicitud de extracción (PR). Antes de seguir los pasos indicados aquí, asegúrese de leer [Documente su destino en Destinos de Adobe Experience Platform](./documentation-instructions.md).

>[!TIP]
>
>Consulte también la documentación de soporte en la Guía del colaborador de Adobe:
>* [Instalación de las herramientas de creación de Git y Markdown](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/install-tools.html?lang=en)
>* [Configure el repositorio de Git localmente para la documentación](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html?lang=en)
>* [Flujo de trabajo de contribución en GitHub para cambios importantes](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/full-workflow.html?lang=en).


## Conéctese a GitHub y configure su entorno de creación local {#set-up-environment}

1. En el explorador, vaya a `https://github.com/AdobeDocs/experience-platform.en`
2. Hasta [bifurcar](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html?lang=en#fork-the-repository) En el repositorio, haga clic en **Tenedor** como se muestra a continuación. Esto crea una copia del repositorio de Experience Platform en su propia cuenta de GitHub.

   ![Repositorio de documentación de Fork Adobe](./assets/ssd-fork-repository.gif)

3. Clone el repositorio en el equipo local. Seleccionar **Código > HTTPS > Abrir con GitHub Desktop**, como se muestra a continuación. Asegúrese de que tiene [GitHub Desktop](https://desktop.github.com/) instalado. Para más información, lea [Crear un clon local del repositorio](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html?lang=en#create-a-local-clone-of-the-repository) en la guía del colaborador de Adobe.

   ![Clonar repositorio de documentación de Adobe al entorno local](./assets/clone-local.png)

4. En la estructura de archivos local, vaya a `experience-platform.en/help/destinations/catalog/[...]`, donde `[...]` es la categoría deseada para el destino. Por ejemplo, si va a añadir un destino de personalización al Experience Platform, seleccione la opción `personalization` carpeta.

## Crear la página de documentación de su destino {#author-documentation}

1. La página de documentación se basa en [plantilla de destino de autoservicio](./self-service-template.md). Descargue la [plantilla de destino](assets/yourdestination-template.zip). Descomprima y extraiga el archivo `yourdestination-template.md` al directorio mencionado en el paso 4 anterior.  Cambie el nombre del archivo `YOURDESTINATION.md`, donde YOURDESTINATION es el nombre del destino en Adobe Experience Platform. Por ejemplo, si su empresa se llama Moviestar, debe asignar un nombre al archivo `moviestar.md`.
2. Abra el nuevo archivo en su [editor de texto elegido](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/install-tools.html?lang=en#understand-markdown-editors). El Adobe recomienda que utilice [Código de Visual Studio](https://code.visualstudio.com/) e instale la extensión de Adobe Markdown Authoring. Para instalar la extensión, abra Código de Visual Studio y seleccione **[!DNL Extensions]** en la parte izquierda de la pantalla y busque `adobe markdown authoring`. Seleccione la extensión y haga clic en **[!DNL Install]**.
   ![Instalar la extensión de creación de Adobe Markdown](./assets/install-adobe-markdown-extension.gif)
3. Edite la plantilla con la información relevante para su destino. Siga las instrucciones de la plantilla.
4. Para obtener capturas de pantalla o imágenes que planee agregar a la documentación, vaya a `GitHub/experience-platform.en/help/destinations/assets/catalog/[...]`, donde `[...]` es la categoría deseada para el destino. Por ejemplo, si va a añadir un destino de personalización al Experience Platform, seleccione la opción `personalization` carpeta. Cree una nueva carpeta para el destino y guarde las imágenes aquí. Debe establecer un vínculo a ellos desde la página que está creando. Consulte [instrucciones cómo vincular a imágenes](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/linking.html?lang=en#link-to-images).
5. Cuando esté listo, guarde el archivo en el que esté trabajando.

## Envíe su documentación para su revisión {#submit-review}

>[!TIP]
>
>Tenga en cuenta que no hay nada que pueda romper aquí. Al seguir las instrucciones de esta sección, simplemente sugiere una actualización de la documentación. El equipo de documentación de Adobe Experience Platform aprobará o editará la actualización sugerida.

1. En GitHub Desktop, cree una rama de trabajo para las actualizaciones y seleccione **Publicar rama** para publicar la rama en GitHub.

![Nueva sucursal local](./assets/new-branch-local.gif)

1. En GitHub Desktop, [comprometer](https://docs.github.com/en/free-pro-team@latest/github/getting-started-with-github/github-glossary#commit) su trabajo, como se muestra a continuación.

   ![Compromiso local](./assets/commit-local.png)

1. En GitHub Desktop, [push](https://docs.github.com/en/free-pro-team@latest/github/getting-started-with-github/github-glossary#push) su trabajo a la [remoto](https://docs.github.com/en/free-pro-team@latest/github/getting-started-with-github/github-glossary#remote) , como se muestra a continuación.

   ![Insertar el compromiso](./assets/push-local-to-remote.png)

1. En la interfaz web de GitHub, abra una solicitud de extracción (PR) para fusionar la rama de trabajo en la rama maestra del repositorio de documentación de Adobe. Asegúrese de que la rama en la que ha trabajado esté seleccionada y seleccione **Contribute > Abrir solicitud de extracción**.

   ![Crear solicitud de extracción](./assets/ssd-create-pull-request-1.gif)

1. Asegúrese de que las ramas base y de comparación son correctas. Añada una nota al PR, describa la actualización y seleccione **Crear solicitud de extracción**. Esto abre una PR para fusionar la rama de trabajo de la ramificación en la rama maestra del repositorio de Adobe.
   >[!TIP]
   >
   >Deje el **Permitir ediciones por responsables** casilla de verificación seleccionada para que el equipo de documentación de Adobe pueda realizar ediciones en el PR.

   ![Crear solicitud de extracción en el repositorio de documentación de Adobe](./assets/ssd-create-pull-request-2.png)

1. En este punto, aparece una notificación que le solicita que firme el Acuerdo de licencia para colaboradores de Adobe (CLA). Este es un paso obligatorio. Después de firmar el CLA, actualice la página PR y envíe la solicitud de extracción.

1. Puede confirmar que la solicitud de extracción se ha enviado inspeccionando el **Solicitudes de extracción** pestaña en `https://github.com/AdobeDocs/experience-platform.en`.

![PR correcta](./assets/ssd-pr-successful.png)

1. ¡Gracias! El equipo de documentación del Adobe se pondrá en contacto con en caso de que sea necesario realizar alguna edición y le informará de cuándo se publicará la documentación.

>[!TIP]
>
>Para añadir imágenes y vínculos a su documentación y para cualquier otra pregunta sobre Markdown, lea [Uso de Markdown](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html?lang=en) en la guía de escritura colaborativa de Adobe.
