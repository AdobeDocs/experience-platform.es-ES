---
title: Utilice un editor de texto en el entorno local para crear una página de documentación de destino
description: Las instrucciones de esta página muestran cómo utilizar un editor de texto para trabajar en su entorno local, crear una página de documentación para el destino del Experience Platform y enviarla para su revisión.
exl-id: 125f2d10-0190-4255-909c-5bd5bb59fcba
source-git-commit: e300e57df998836a8c388511b446e90499185705
workflow-type: tm+mt
source-wordcount: '795'
ht-degree: 0%

---

# Utilice un editor de texto en el entorno local para crear una página de documentación de destino {#local-authoring}

Las instrucciones de esta página muestran cómo utilizar un editor de texto para trabajar en el entorno local, crear documentación y enviar una solicitud de extracción (PR). Antes de seguir los pasos indicados aquí, asegúrate de leer [Documentar tu destino en Destinos de Adobe Experience Platform](./documentation-instructions.md).

>[!TIP]
>
>Consulte también la documentación de soporte en la Guía del colaborador de Adobe:
>* [Instalar las herramientas de creación de Git y Markdown](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/install-tools.html)
>* [Configurar el repositorio Git localmente para la documentación](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html)
>* [Flujo de trabajo de contribución en GitHub para cambios importantes](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/full-workflow.html).

## Conéctese a GitHub y configure su entorno de creación local {#set-up-environment}

1. En su explorador, vaya a `https://github.com/AdobeDocs/experience-platform.en`
2. Para [ramificar](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html#fork-the-repository) el repositorio, haga clic en **Ramificar** como se muestra a continuación. Esto crea una copia del repositorio de Experience Platform en su propia cuenta de GitHub.

   ![Repositorio de documentación de Fork Adobe](../assets/docs-framework/ssd-fork-repository.gif)

3. Clone el repositorio en el equipo local. Seleccione **Código > HTTPS > Abrir con GitHub Desktop**, como se muestra a continuación. Asegúrese de tener [GitHub Desktop](https://desktop.github.com/) instalado. Para obtener más información, lea [Crear un clon local del repositorio](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html#create-a-local-clone-of-the-repository) en la guía del colaborador de Adobe.

   ![Clonar repositorio de documentación de Adobe al entorno local](../assets/docs-framework/clone-local.png)

4. En la estructura de archivos local, vaya a `experience-platform.en/help/destinations/catalog/[...]`, donde `[...]` es la categoría deseada para el destino. Por ejemplo, si está agregando un destino de personalización al Experience Platform, seleccione la carpeta `personalization`.

## Crear la página de documentación de su destino {#author-documentation}

1. Su página de documentación se basa en la [plantilla de destino de autoservicio](../docs-framework/self-service-template.md). Descargar la [plantilla de destino](../assets/docs-framework/yourdestination-template.zip). Descomprímalo y extraiga el archivo `yourdestination-template.md` en el directorio mencionado en el paso 4 anterior.  Cambie el nombre del archivo `YOURDESTINATION.md`, donde YOURDESTINATION es el nombre del destino en Adobe Experience Platform. Por ejemplo, si su compañía se llama Moviestar, debe asignar un nombre al archivo `moviestar.md`.
2. Abra el nuevo archivo en el [editor de texto que elija](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/install-tools.html#understand-markdown-editors). Adobe recomienda usar [Visual Studio Code](https://code.visualstudio.com/) e instalar la extensión de Adobe Markdown Authoring. Para instalar la extensión, abra Visual Studio Code, seleccione la ficha **[!DNL Extensions]** a la izquierda de la pantalla y busque `adobe markdown authoring`. Seleccione la extensión y haga clic en **[!DNL Install]**.
   ![Instalar extensión de creación de Adobe Markdown](../assets/docs-framework/install-adobe-markdown-extension.gif)
3. Edite la plantilla con la información relevante para su destino. Siga las instrucciones de la plantilla.
4. Para cualquier captura de pantalla o imagen que planee agregar a su documentación, vaya a `GitHub/experience-platform.en/help/destinations/assets/catalog/[...]`, donde `[...]` es la categoría deseada para su destino. Por ejemplo, si está agregando un destino de personalización al Experience Platform, seleccione la carpeta `personalization`. Cree una nueva carpeta para el destino y guarde las imágenes aquí. Debe establecer un vínculo a ellos desde la página que está creando. Vea [instrucciones sobre cómo vincular a imágenes](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/linking.html#link-to-images).
5. Cuando esté listo, guarde el archivo en el que esté trabajando.

## Envíe su documentación para su revisión {#submit-review}

>[!TIP]
>
>Tenga en cuenta que no hay nada que pueda romper aquí. Al seguir las instrucciones de esta sección, simplemente sugiere una actualización de la documentación. El equipo de documentación de Adobe Experience Platform aprobará o editará la actualización sugerida.

1. En GitHub Desktop, cree una rama de trabajo para sus actualizaciones y seleccione **Publish branch** para publicar la rama en GitHub.

![Nueva sucursal local](../assets/docs-framework/new-branch-local.gif)

1. En GitHub Desktop, [confirme](https://docs.github.com/en/free-pro-team@latest/github/getting-started-with-github/github-glossary#commit) su trabajo, como se muestra a continuación.

   ![Confirmar local](../assets/docs-framework/commit-local.png)

1. En GitHub Desktop, [inserta](https://docs.github.com/en/free-pro-team@latest/github/getting-started-with-github/github-glossary#push) tu trabajo en la rama [remota](https://docs.github.com/en/free-pro-team@latest/github/getting-started-with-github/github-glossary#remote), como se muestra a continuación.

   ![Insertar su compromiso](../assets/docs-framework/push-local-to-remote.png)

1. En la interfaz web de GitHub, abra una solicitud de extracción (PR) para fusionar la rama de trabajo en la rama maestra del repositorio de documentación de Adobe. Asegúrese de que la rama en la que trabajó esté seleccionada y seleccione **Contribute > Abrir solicitud de extracción**.

   ![Crear solicitud de extracción](../assets/docs-framework/ssd-create-pull-request-1.gif)

1. Asegúrese de que las ramas base y de comparación son correctas. Agregue una nota al PR, describiendo su actualización, y seleccione **Crear solicitud de extracción**. Esto abre una PR para fusionar la rama de trabajo de la ramificación en la rama maestra del repositorio de Adobe.
   >[!TIP]
   >
   >Deje seleccionada la casilla de verificación **Permitir ediciones por responsables** para que el equipo de documentación de Adobe pueda realizar ediciones en la PR.

   ![Crear solicitud de extracción en el repositorio de documentación de Adobe](../assets/docs-framework/ssd-create-pull-request-2.png)

1. En este punto, aparece una notificación que le solicita que firme el Acuerdo de licencia para colaboradores de Adobe (CLA). Este es un paso obligatorio. Después de firmar el CLA, actualice la página PR y envíe la solicitud de extracción.

1. Puede confirmar que la solicitud de extracción se ha enviado inspeccionando la ficha **Solicitudes de extracción** en `https://github.com/AdobeDocs/experience-platform.en`.

![PR correcta](../assets/docs-framework/ssd-pr-successful.png)

1. ¡Gracias! El equipo de documentación del Adobe se pondrá en contacto con en caso de que sea necesario realizar alguna edición y le informará de cuándo se publicará la documentación.

>[!TIP]
>
>Para agregar imágenes y vínculos a tu documentación y para cualquier otra pregunta sobre Markdown, lee [Using Markdown](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html) en la guía de escritura colaborativa de Adobe.
