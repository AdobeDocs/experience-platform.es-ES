---
title: Utilice un editor de texto en el entorno local para crear una página de documentación de destino
description: Las instrucciones de esta página muestran cómo utilizar un editor de texto para trabajar en el entorno local con el fin de crear una página de documentación para el destino del Experience Platform y enviarla para su revisión.
exl-id: 125f2d10-0190-4255-909c-5bd5bb59fcba
source-git-commit: e239de97a26ea2ff36bb74390e249851a13d2e13
workflow-type: tm+mt
source-wordcount: '885'
ht-degree: 2%

---

# Utilice un editor de texto en el entorno local para crear una página de documentación de destino {#local-authoring}

Las instrucciones de esta página le muestran cómo utilizar un editor de texto para trabajar en su entorno local con el fin de crear documentación y enviar una solicitud de extracción (PR). Antes de seguir los pasos indicados aquí, asegúrese de leer [Documentar el destino en destinos de Adobe Experience Platform](./documentation-instructions.md).

>[!TIP]
>
>Consulte también la documentación de apoyo en la guía para colaboradores de Adobe:
>* [Instalación de las herramientas de creación de Git y Markdown](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/install-tools.html?lang=en)
>* [Configure el repositorio de Git localmente para la documentación](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html?lang=en)
>* [Flujo de trabajo de contribución en GitHub para cambios importantes](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/full-workflow.html?lang=en).


## Conéctese a GitHub y configure su entorno de creación local {#set-up-environment}

1. En el navegador, vaya a `https://github.com/AdobeDocs/experience-platform.en`
2. Hasta [ramificación](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html?lang=en#fork-the-repository) el repositorio, haga clic en **Bifurcación (Fork)** como se muestra a continuación. Esto crea una copia del repositorio del Experience Platform en su propia cuenta de GitHub.

   ![Repositorio de documentación de Adobe de ramificación](../assets/docs-framework/ssd-fork-repository.gif)

3. Clone el repositorio en el equipo local. Select **Código > HTTPS > Abrir con GitHub Desktop**, como se muestra a continuación. Asegúrese de que [Escritorio de GitHub](https://desktop.github.com/) instalado. Para más información, léase [Creación de un clon local del repositorio](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html?lang=en#create-a-local-clone-of-the-repository) en la guía del colaborador de Adobe.

   ![Clonar el repositorio de documentación de Adobe en el entorno local](../assets/docs-framework/clone-local.png)

4. En la estructura de archivos local, vaya a `experience-platform.en/help/destinations/catalog/[...]`, donde `[...]` es la categoría deseada para el destino. Por ejemplo, si va a añadir un destino de personalización al Experience Platform, seleccione la opción `personalization` carpeta.

## Cree la página de documentación para su destino {#author-documentation}

1. La página de documentación se basa en la variable [plantilla de destino de autoservicio](../docs-framework/self-service-template.md). Descargue el [plantilla de destino](../assets/docs-framework/yourdestination-template.zip). Descomprimirlo y extraer el archivo `yourdestination-template.md` al directorio mencionado en el paso 4 anterior.  Cambiar el nombre del archivo `YOURDESTINATION.md`, donde YOURDESTINATION es el nombre de su destino en Adobe Experience Platform. Por ejemplo, si su empresa se llama Moviestar, debe asignar un nombre al archivo `moviestar.md`.
2. Abra el nuevo archivo en su [editor de texto que elija](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/install-tools.html?lang=en#understand-markdown-editors). Adobe recomienda usar [Código de Visual Studio](https://code.visualstudio.com/) e instale la extensión de creación de Adobe Markdown. Para instalar la extensión, abra el código de Visual Studio y seleccione la opción **[!DNL Extensions]** a la izquierda de la pantalla y busque `adobe markdown authoring`. Seleccione la extensión y haga clic en **[!DNL Install]**.
   ![Instalación de la extensión de creación de Adobe Markdown](../assets/docs-framework/install-adobe-markdown-extension.gif)
3. Edite la plantilla con la información relevante para el destino. Siga las instrucciones de la plantilla.
4. Para cualquier captura de pantalla o imagen que planee añadir a su documentación, vaya a `GitHub/experience-platform.en/help/destinations/assets/catalog/[...]`, donde `[...]` es la categoría deseada para el destino. Por ejemplo, si va a añadir un destino de personalización al Experience Platform, seleccione la opción `personalization` carpeta. Cree una nueva carpeta para el destino y guarde las imágenes aquí. Debe vincularlos desde la página que esté creando. Consulte [instrucciones sobre cómo vincular a imágenes](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/linking.html?lang=en#link-to-images).
5. Cuando esté listo, guarde el archivo en el que está trabajando.

## Envíe su documentación para su revisión {#submit-review}

>[!TIP]
>
>Tenga en cuenta que no hay nada que pueda romper aquí. Al seguir las instrucciones de esta sección, simplemente está sugiriendo una actualización de la documentación. El equipo de documentación de Adobe Experience Platform aprobará o editará la actualización sugerida.

1. En GitHub Desktop, cree una rama de trabajo para sus actualizaciones y seleccione **Rama de publicación** para publicar la rama en GitHub.

![Nueva rama local](../assets/docs-framework/new-branch-local.gif)

1. En GitHub Desktop, [commit](https://docs.github.com/en/free-pro-team@latest/github/getting-started-with-github/github-glossary#commit) su trabajo, como se muestra a continuación.

   ![Confirmar local](../assets/docs-framework/commit-local.png)

1. En GitHub Desktop, [push](https://docs.github.com/en/free-pro-team@latest/github/getting-started-with-github/github-glossary#push) su trabajo con [remote](https://docs.github.com/en/free-pro-team@latest/github/getting-started-with-github/github-glossary#remote) como se muestra a continuación.

   ![Impulse su compromiso](../assets/docs-framework/push-local-to-remote.png)

1. En la interfaz web de GitHub, abra una solicitud de extracción (PR) para fusionar la rama de trabajo en la rama maestra del repositorio de documentación de Adobe. Asegúrese de que la rama en la que trabajó esté seleccionada y seleccione **Contribute > Abrir solicitud de extracción**.

   ![Crear solicitud de extracción](../assets/docs-framework/ssd-create-pull-request-1.gif)

1. Asegúrese de que la base y las ramas comparadas sean correctas. Agregue una nota a la PR, describa su actualización y seleccione **Crear solicitud de extracción**. Esto abre una PR para fusionar la rama de trabajo de la ramificación en la rama maestra del repositorio de Adobe.
   >[!TIP]
   >
   >Deje el **Permitir ediciones por parte de los administradores** casilla de verificación seleccionada para que el equipo de documentación de Adobe pueda realizar modificaciones en PR.

   ![Creación de solicitudes de extracción en el repositorio de documentación de Adobe](../assets/docs-framework/ssd-create-pull-request-2.png)

1. En este punto, aparece una notificación que le solicita que firme el Acuerdo de licencia para colaboradores de Adobe (CLA). Este es un paso obligatorio. Después de firmar el Acuerdo de colaboración, actualice la página de relaciones públicas y envíe la solicitud de extracción.

1. Puede confirmar que la solicitud de extracción se ha enviado inspeccionando la variable **Solicitudes de extracción** en `https://github.com/AdobeDocs/experience-platform.en`.

![PR con éxito](../assets/docs-framework/ssd-pr-successful.png)

1. ¡Gracias! El equipo de documentación de Adobe contactará con PR en caso de que se requieran modificaciones y le informará cuando se publicará la documentación.

>[!TIP]
>
>Para añadir imágenes y vínculos a la documentación y para cualquier otra pregunta sobre Markdown, lea [Uso de Markdown](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html?lang=en) en la guía de escritura colaborativa de Adobe.
