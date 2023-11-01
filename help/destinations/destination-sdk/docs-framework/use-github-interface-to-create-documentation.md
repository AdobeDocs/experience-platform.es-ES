---
title: Utilice la interfaz web de GitHub para crear una página de documentación de destino
description: Las instrucciones de esta página muestran cómo utilizar la interfaz web de GitHub para crear una página de documentación para el destino del Experience Platform y enviarla para su revisión.
exl-id: 4780e05e-3d1d-4f1b-8441-df28d09c1a88
source-git-commit: e300e57df998836a8c388511b446e90499185705
workflow-type: tm+mt
source-wordcount: '768'
ht-degree: 1%

---

# Utilice la interfaz web de GitHub para crear una página de documentación de destino {#github-interface}

Las instrucciones siguientes muestran cómo utilizar la interfaz web de GitHub para crear documentación y enviar una solicitud de extracción (PR). Antes de seguir los pasos indicados aquí, asegúrese de leer [Documente su destino en Destinos de Adobe Experience Platform](./documentation-instructions.md).

>[!TIP]
>
>Consulte también la documentación de soporte en la Guía del colaborador de Adobe:
>* [Instalación de las herramientas de creación de Git y Markdown](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/install-tools.html)
>* [Configure el repositorio de Git localmente para la documentación](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html)
>* [Flujo de trabajo de contribución en GitHub para cambios importantes](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/full-workflow.html).

## Configuración del entorno de creación de GitHub {#set-up-environment}

1. En el explorador, vaya a `https://github.com/AdobeDocs/experience-platform.en`.
2. Hasta [bifurcar](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html#fork-the-repository) En el repositorio, haga clic en **Tenedor** como se muestra a continuación. Esto crea una copia del repositorio de Experience Platform en su propia cuenta de GitHub.

   ![Repositorio de documentación de Fork Adobe](../assets/docs-framework/ssd-fork-repository.gif)

3. En la ramificación del repositorio, cree una nueva rama para el proyecto, como se muestra a continuación. Utilice esta nueva rama para su trabajo.

   ![Crear nueva rama de GitHub](../assets/docs-framework/new-branch-github.gif)

4. En la estructura de carpetas de GitHub del repositorio ramificado, navegue hasta `experience-platform.en/help/destinations/catalog/[...]`, donde `[...]` es la categoría deseada para el destino. Por ejemplo, si va a añadir un destino de personalización al Experience Platform, seleccione la opción `personalization` categoría. Seleccionar **Añadir archivo > Crear nuevo archivo**.

   ![Añadir nuevo archivo](../assets/docs-framework/github-navigate-and-create-file.gif)

5. Asigne un nombre al destino `YOURDESTINATION.md`, donde YOURDESTINATION es el nombre del destino en Adobe Experience Platform. Por ejemplo, si su empresa se llama Moviestar, debe asignar un nombre al archivo `moviestar.md`.

## Crear la página de documentación de su destino {#author-documentation}

1. Creará el contenido de la página de destino en función de la variable [plantilla de autoservicio de documentación](./self-service-template.md). **[Descargar](../assets/docs-framework/yourdestination-template.zip)** Abra la plantilla y descomprímala para extraer el `.md` plantilla de archivo.
2. Pegue y edite el contenido de la plantilla con información relevante para su destino en un editor de markdown en línea, como [dillinger.io](https://dillinger.io/). Siga las instrucciones de la plantilla para obtener más información sobre lo que debe rellenar y los párrafos que se pueden eliminar.

   >[!TIP]
   >
   >Puede cerrar la ventana del explorador en cualquier momento y volver a abrirla más tarde. Su trabajo se guarda automáticamente y le estará esperando cuando vuelva a abrir el explorador.
3. Copie el contenido del editor de markdown en el nuevo archivo en GitHub.
4. Para cualquier captura de pantalla o imagen que planee utilizar, utilice la interfaz de GitHub para cargar los archivos en `experience-platform.en/help/destinations/assets/catalog/[...]`, donde `[...]` es la categoría deseada para el destino. Por ejemplo, si va a añadir un destino de personalización al Experience Platform, seleccione la opción `personalization` categoría. Debe vincular a las imágenes de la página que está creando. Consulte [instrucciones cómo vincular a imágenes](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/linking.html#link-to-images).

   ![Cargar imagen en GitHub](../assets/docs-framework/upload-image.gif)

5. Cuando esté listo, guarde el archivo en la rama.

![Confirmar creación de archivo](../assets/docs-framework/ssd-confirm-file-creation.png)

## Envíe su documentación para su revisión {#submit-review}

>[!TIP]
>
>Tenga en cuenta que no hay nada que pueda romper aquí. Al seguir las instrucciones de esta sección, simplemente sugiere una actualización de la documentación. El equipo de documentación de Adobe Experience Platform aprobará o editará la actualización sugerida.

1. Después de guardar el archivo y cargar las imágenes deseadas, puede abrir una solicitud de extracción (PR) para fusionar la rama de trabajo en la rama maestra del repositorio de documentación de Adobe. Asegúrese de que la rama en la que ha trabajado esté seleccionada y seleccione **Contribute > Abrir solicitud de extracción**.

![Crear solicitud de extracción](../assets/docs-framework/ssd-create-pull-request-1.gif)

1. Asegúrese de que las ramas base y de comparación son correctas. Añada una nota al PR, describa la actualización y seleccione **Crear solicitud de extracción**. Esto abre una PR para fusionar la rama de trabajo de la ramificación en la rama maestra del repositorio de Adobe.

   >[!TIP]
   >
   >Deje el **Permitir ediciones por responsables** casilla de verificación seleccionada para que el equipo de documentación de Adobe pueda realizar ediciones en el PR.

   ![Crear solicitud de extracción en el repositorio de documentación de Adobe](../assets/docs-framework/ssd-create-pull-request-2.png)

1. En este punto, aparece una notificación que le solicita que firme el Acuerdo de licencia para colaboradores de Adobe (CLA). Este es un paso obligatorio. Después de firmar el CLA, actualice la página PR y envíe la solicitud de extracción.

1. Puede confirmar que la solicitud de extracción se ha enviado inspeccionando el **Solicitudes de extracción** pestaña en `https://github.com/AdobeDocs/experience-platform.en`.

   ![PR correcta](../assets/docs-framework/ssd-pr-successful.png)

1. ¡Gracias! El equipo de documentación del Adobe se pondrá en contacto con en caso de que sea necesario realizar alguna edición y le informará de cuándo se publicará la documentación.

>[!TIP]
>
>Para añadir imágenes y vínculos a su documentación y para cualquier otra pregunta sobre Markdown, lea [Uso de Markdown](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html) en la guía de escritura colaborativa de Adobe.
