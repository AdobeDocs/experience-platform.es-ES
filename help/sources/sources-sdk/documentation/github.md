---
keywords: Experience Platform;inicio;temas populares;orígenes;conectores;conectores de origen;sdk de fuentes;sdk;SDK
solution: Experience Platform
title: Uso de la interfaz web de GitHub para crear una página de documentación de fuentes
topic-legacy: tutorial
description: Este documento proporciona pasos sobre cómo utilizar la interfaz web de GitHub para crear documentación y enviar una solicitud de extracción (PR).
hide: true
hidefromtoc: true
source-git-commit: d4b5b54be9fa2b430a3b45eded94a523b6bd4ef8
workflow-type: tm+mt
source-wordcount: '561'
ht-degree: 2%

---

# Utilice la interfaz web de GitHub para crear una página de documentación de origen

Este documento proporciona pasos sobre cómo utilizar la interfaz web de GitHub para crear documentación y enviar una solicitud de extracción (PR).

>[!TIP]
>
>Los siguientes documentos de la guía de contribución de Adobe se pueden utilizar para respaldar aún más su proceso de documentación: <ul><li>[Instalación de las herramientas de creación de Git y Markdown](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/install-tools.html?lang=en)</li><li>[Configure el repositorio de Git localmente para la documentación](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html?lang=en)</li><li>[Flujo de trabajo de contribución en GitHub para cambios importantes](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/full-workflow.html?lang=en)</li></ul>

## Configuración del entorno de GitHub

El primer paso para configurar el entorno de GitHub es ir a la [Repositorio de Adobe Experience Platform GitHub](https://github.com/AdobeDocs/experience-platform.en).

![platform-repo](../assets/platform-repo.png)

A continuación, seleccione **Bifurcación (Fork)**.

![Fork (Ramificación)](../assets/fork.png)

Una vez finalizada la ramificación, seleccione **maestro** e introduzca un nombre para la nueva rama en el menú desplegable que aparece. Asegúrese de proporcionar un nombre descriptivo para la rama, ya que se utilizará para contener el trabajo, y luego seleccione **crear rama**.

![create-branch](../assets/create-branch.png)

En la estructura de carpetas de GitHub del repositorio ramificado, navegue hasta `experience-platform.en/help/sources/tutorials/api/create/` y, a continuación, seleccione la categoría adecuada para el origen en la lista. Por ejemplo, si está creando documentación para una nueva fuente de almacenamiento en la nube, seleccione **almacenamiento en la nube**.

![almacenamiento en la nube](../assets/cloud-storage.png)

Aparece una carpeta de orígenes de almacenamiento en la nube existentes. Para agregar documentación para una fuente nueva, seleccione **Agregar archivo** y, a continuación, seleccione **Crear nuevo archivo** del menú desplegable que aparece.

![create-new-file](../assets/create-new-file.png)

Asigne un nombre al archivo de origen `YOURSOURCE.md` donde YOURSOURCE es el nombre de su fuente en Platform. Por ejemplo, si su empresa es [!DNL Mailchimp], el nombre del archivo debe ser `mailchimp.md`.

![git-interface](../assets/git-interface.png)

## Cree la página de documentación para el origen

Para empezar a documentar el nuevo origen, pegue el contenido del [plantilla de documentación de fuentes](./template.md) en el editor web de GitHub. También puede descargar la plantilla [here](../assets/template.zip).

Con la plantilla copiada en la interfaz del editor web de GitHub, siga las instrucciones descritas en la plantilla y edite los valores que contengan información relevante para la fuente.

![pegar-plantilla](../assets/paste-template.png)

Cuando termine, confirme el archivo en su rama.

![commit](../assets/commit.png)

## Envíe su documentación para su revisión

Una vez confirmado el archivo, puede abrir una solicitud de extracción (PR) para fusionar la rama de trabajo en la rama maestra del repositorio de documentación de Adobe. Asegúrese de que la rama en la que ha estado trabajando está seleccionada y, a continuación, seleccione **Comparar y extraer solicitudes**.

![compare-pr](../assets/compare-pr.png)

Asegúrese de que la base y las ramas comparadas sean correctas. Agregue una nota a la PR, describa su actualización y, a continuación, seleccione **Crear solicitud de extracción**. Esto abre una PR para fusionar la rama de trabajo del trabajo en la rama maestra del repositorio de Adobe.

>[!TIP]
>
>Deje el **Permitir ediciones por parte de los administradores** casilla de verificación seleccionada para garantizar que el equipo de documentación de Adobe pueda realizar modificaciones en PR.

![create-pr](../assets/create-pr.png)

En este punto, aparece una notificación que le solicita que firme el Acuerdo de licencia para colaboradores de Adobe (CLA). Este es un paso obligatorio. Después de firmar el Acuerdo de colaboración, actualice la página de relaciones públicas y envíe la solicitud de extracción.

Puede confirmar que la solicitud de extracción se ha enviado inspeccionando la pestaña de solicitudes de extracción en https://github.com/AdobeDocs/experience-platform.en.

![confirm-pr](../assets/confirm-pr.png)
