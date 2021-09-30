---
title: 'Utilice la interfaz web de GitHub para crear una página de documentación de destino '
description: Las instrucciones de esta página muestran cómo usar la interfaz web de GitHub para crear una página de documentación para el destino del Experience Platform y enviarla para su revisión.
exl-id: 4780e05e-3d1d-4f1b-8441-df28d09c1a88
source-git-commit: 83539a9aa2fddcae0c9a44302d8bfa9d9f56de0c
workflow-type: tm+mt
source-wordcount: '768'
ht-degree: 1%

---

# Utilice la interfaz web de GitHub para crear una página de documentación de destino {#github-interface}

Las instrucciones siguientes muestran cómo utilizar la interfaz web de GitHub para crear documentación y enviar una solicitud de extracción (PR). Antes de seguir los pasos indicados aquí, asegúrese de leer [Document your destination in Adobe Experience Platform Destinations](./documentation-instructions.md).

>[!TIP]
>
>Consulte también la documentación de apoyo en la guía para colaboradores de Adobe:
>* [Instalación de las herramientas de creación de Git y Markdown](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/install-tools.html?lang=en)
>* [Configure el repositorio de Git localmente para la documentación](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html?lang=en)
>* [Flujo de trabajo de contribución en GitHub para cambios importantes](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/full-workflow.html?lang=en).


## Configuración del entorno de creación de GitHub {#set-up-environment}

1. En el explorador, vaya a `https://github.com/AdobeDocs/experience-platform.en`.
2. Para [ramificar](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html?lang=en#fork-the-repository) el repositorio, haga clic en **Fork** como se muestra en la imagen siguiente.

   ![Repositorio de documentación de Adobe de ramificación](./assets/ssd-fork-repository.gif)

3. En la ramificación del repositorio, cree una nueva rama para su proyecto, como se muestra a continuación. Utilice esta nueva rama para su trabajo.

   ![Crear nueva rama de GitHub](./assets/new-branch-github.gif)

4. En la estructura de carpetas de GitHub del repositorio ramificado, vaya a `experience-platform.en/help/destinations/catalog/[...]`, donde `[...]` es la categoría deseada para su destino. Por ejemplo, si está agregando un destino de personalización al Experience Platform, seleccione la categoría `personalization` . Seleccione **Agregar archivo > Crear nuevo archivo**.

   ![Añadir nuevo archivo](./assets/github-navigate-and-create-file.gif)

5. Asigne un nombre a su destino `YOURDESTINATION.md`, donde DESTINO es el nombre de su destino en Adobe Experience Platform. Por ejemplo, si su empresa se llama Moviestar, debe asignar un nombre al archivo `moviestar.md`.

## Cree la página de documentación para su destino {#author-documentation}

1. Creará el contenido de la página de destino en función de la plantilla de autoservicio [documentación](./self-service-template.md). **[](assets/yourdestination-template.zip)** Descargue la plantilla y descomprima para extraer la plantilla de  `.md` archivo.
2. Pegue y edite el contenido de la plantilla con información relevante para el destino en un editor de Markdown en línea, como [dillinger.io](https://dillinger.io/). Siga las instrucciones de la plantilla para obtener detalles sobre qué debe rellenar y qué párrafos se pueden eliminar.

   >[!TIP]
   >
   >Puede cerrar la ventana del explorador en cualquier momento y volver a abrirla más tarde. Su trabajo se guarda automáticamente y se le espera cuando vuelva a abrir el explorador.
3. Copie el contenido del editor de markdown en el nuevo archivo de GitHub.
4. Para las capturas de pantalla o imágenes que planee usar, utilice la interfaz de GitHub para cargar los archivos en `experience-platform.en/help/destinations/assets/catalog/[...]`, donde `[...]` es la categoría deseada para el destino. Por ejemplo, si está agregando un destino de personalización al Experience Platform, seleccione la categoría `personalization` . Debe vincular las imágenes de la página que esté creando. Consulte [instrucciones sobre cómo vincular a imágenes](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/linking.html?lang=en#link-to-images).

   ![Cargar imagen a GitHub](./assets/upload-image.gif)

5. Cuando esté listo, guarde el archivo en su rama.

![Confirmar la creación del archivo](./assets/ssd-confirm-file-creation.png)

## Envíe su documentación para su revisión {#submit-review}

>[!TIP]
>
>Tenga en cuenta que no hay nada que pueda romper aquí. Al seguir las instrucciones de esta sección, simplemente está sugiriendo una actualización de la documentación. El equipo de documentación de Adobe Experience Platform aprobará o editará la actualización sugerida.

1. Después de guardar el archivo y cargar las imágenes que desee, puede abrir una solicitud de extracción (PR) para fusionar la rama de trabajo en la rama maestra del repositorio de documentación de Adobe. Asegúrese de que la rama en la que ha trabajado esté seleccionada y seleccione **Contribute > Pull request**.

![Crear solicitud de extracción](./assets/ssd-create-pull-request-1.gif)

1. Asegúrese de que la base y las ramas comparadas sean correctas. Agregue una nota a la PR, describiendo su actualización, y seleccione **Crear solicitud de extracción**. Esto abre una PR para fusionar la rama de trabajo de la ramificación en la rama maestra del repositorio de Adobe.

   >[!TIP]
   >
   >Deje activada la casilla **Permitir ediciones por parte de los mantenedores** para que el equipo de documentación de Adobe pueda realizar ediciones en PR.

   ![Creación de solicitudes de extracción en el repositorio de documentación de Adobe](./assets/ssd-create-pull-request-2.png)

1. En este punto, aparece una notificación que le solicita que firme el Acuerdo de licencia para colaboradores de Adobe (CLA). Este es un paso obligatorio. Después de firmar el Acuerdo de colaboración, actualice la página de relaciones públicas y envíe la solicitud de extracción.

1. Puede confirmar que la solicitud de extracción se ha enviado inspeccionando la pestaña **Pull request** en `https://github.com/AdobeDocs/experience-platform.en`.

   ![PR con éxito](./assets/ssd-pr-successful.png)

1. ¡Gracias! El equipo de documentación de Adobe contactará con PR en caso de que se requieran modificaciones y le informará cuando se publicará la documentación.

>[!TIP]
>
>Para añadir imágenes y vínculos a la documentación y para cualquier otra pregunta relacionada con Markdown, lea [Using Markdown](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html?lang=en) en la guía de escritura colaborativa de Adobe.
