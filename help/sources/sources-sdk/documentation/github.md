---
keywords: Experience Platform;inicio;temas populares;fuentes;conectores;conectores de origen;sdk de fuentes;sdk;SDK
solution: Experience Platform
title: Uso de la interfaz web de GitHub para crear una página de documentación de orígenes
description: Este documento proporciona pasos sobre cómo utilizar la interfaz web de GitHub para crear documentación y enviar una solicitud de extracción (PR).
exl-id: 84b4219c-b3b2-4d0a-9a65-f2d5cd989f95
source-git-commit: e300e57df998836a8c388511b446e90499185705
workflow-type: tm+mt
source-wordcount: '564'
ht-degree: 0%

---

# Utilice la interfaz web de GitHub para crear una página de documentación de origen

Este documento proporciona pasos sobre cómo utilizar la interfaz web de GitHub para crear documentación y enviar una solicitud de extracción (PR).

>[!TIP]
>
>Los siguientes documentos de la guía de contribución de Adobe se pueden utilizar para respaldar aún más su proceso de documentación: <ul><li>[Instalar las herramientas de creación de Git y Markdown](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/install-tools.html)</li><li>[Configurar el repositorio Git localmente para la documentación](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html)</li><li>[Flujo de trabajo de contribución en GitHub para cambios importantes](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/full-workflow.html)</li></ul>

## Configuración del entorno de GitHub

El primer paso para configurar el entorno de GitHub es ir al [repositorio de GitHub de Adobe Experience Platform](https://github.com/AdobeDocs/experience-platform.es).

![platform-repo](../assets/platform-repo.png)

A continuación, seleccione **Bifurcación**.

![bifurcación](../assets/fork.png)

Una vez completada la bifurcación, seleccione **maestro** e introduzca un nombre para la nueva rama en el menú desplegable que aparece. Asegúrese de proporcionar un nombre descriptivo para la rama, ya que se utilizará para contener su trabajo y, a continuación, seleccione **crear rama**.

![create-branch](../assets/create-branch.png)

En la estructura de carpetas de GitHub del repositorio ramificado, vaya a [`experience-platform.en/help/sources/tutorials/api/create/`](https://github.com/AdobeDocs/experience-platform.en/tree/main/help/sources/tutorials/api/create) y, a continuación, seleccione la categoría adecuada para el origen en la lista. Por ejemplo, si está creando documentación para un nuevo origen de CRM, seleccione **crm**.

>[!TIP]
>
>Si está creando documentación para la interfaz de usuario, vaya a [`experience-platform.en/help/sources/tutorials/ui/create/`](https://github.com/AdobeDocs/experience-platform.en/tree/main/help/sources/tutorials/ui/create) y seleccione la categoría adecuada para el origen. Para agregar tus imágenes, ve a [`experience-platform.en/help/sources/images/tutorials/create/sdk`](https://github.com/AdobeDocs/experience-platform.en/tree/main/help/sources/images/tutorials/create) y luego agrega tus capturas de pantalla a la carpeta `sdk`.

![crm](../assets/crm.png)

Aparece una carpeta de orígenes de CRM existentes. Para agregar documentación para un nuevo origen, selecciona **Agregar archivo** y, a continuación, selecciona **Crear nuevo archivo** en el menú desplegable que aparece.

![create-new-file](../assets/create-new-file.png)

Asigne un nombre al archivo de origen `YOURSOURCE.md`, donde YOURSOURCE es el nombre del origen en Platform. Por ejemplo, si su empresa es ACME CRM, su nombre de archivo debe ser `acme-crm.md`.

![interfaz de Git](../assets/git-interface.png)

## Crear la página de documentación para el origen

Para empezar a documentar la nueva fuente, pegue el contenido de la [plantilla de documentación de fuentes](./template.md) en el editor web de GitHub. También puede descargar la plantilla [aquí](../assets/api-template.zip).

Con la plantilla copiada en la interfaz del editor web de GitHub, siga las instrucciones descritas en la plantilla y edite los valores que contengan información relevante para la fuente.

![pegar-plantilla](../assets/paste-template.png)

Cuando se complete, confirme el archivo en la rama.

![confirmar](../assets/commit.png)

## Envíe su documentación para su revisión

Una vez confirmado el archivo, puede abrir una solicitud de extracción (PR) para fusionar la rama de trabajo en la rama maestra del repositorio de documentación de Adobe. Asegúrese de que la rama en la que ha estado trabajando esté seleccionada y, a continuación, seleccione **Comparar y extraer solicitud**.

![comparar-pr](../assets/compare-pr.png)

Asegúrese de que las ramas base y de comparación son correctas. Agregue una nota al PR, describiendo su actualización, y luego seleccione **Crear solicitud de extracción**. Se abrirá una PR para fusionar la rama de trabajo del trabajo en la rama maestra del repositorio de Adobe.

>[!TIP]
>
>Deje seleccionada la casilla de verificación **Permitir ediciones por responsables** para garantizar que el equipo de documentación de Adobe pueda realizar ediciones en la PR.

![crear-pr](../assets/create-pr.png)

En este punto, aparece una notificación que le solicita que firme el Acuerdo de licencia para colaboradores de Adobe (CLA). Este es un paso obligatorio. Después de firmar el CLA, actualice la página PR y envíe la solicitud de extracción.

Puede confirmar que la solicitud de extracción se ha enviado inspeccionando la pestaña solicitudes de extracción en https://github.com/AdobeDocs/experience-platform.en.

![confirmar-pr](../assets/confirm-pr.png)
