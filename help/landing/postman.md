---
keywords: Experience Platform;inicio;temas populares;Adobe Experience Platform;guía de api;guía de api de plataforma;introducción a platform;guía para desarrolladores
solution: Experience Platform
title: Postman en Adobe Experience Platform
description: Este documento contiene los pasos necesarios para configurar un entorno de Postman, importar colecciones de Postman y una lista de colecciones disponibles para cada servicio de Experience Platform.
role: Developer
feature: API
exl-id: a09b3875-97f5-47f1-a562-52decbce67b1
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '524'
ht-degree: 0%

---

# Postman en Adobe Experience Platform

Postman es una plataforma de colaboración para el desarrollo de API que le permite configurar entornos con variables preestablecidas, compartir colecciones de API, optimizar solicitudes de CRUD y mucho más. La mayoría de los servicios de API de Experience Platform tienen colecciones Postman que se pueden utilizar para ayudar a realizar llamadas de API.

## Configuración de un entorno de Postman para Experience Platform

La siguiente guía de vídeo describe la creación y configuración de su entorno de Postman. Un entorno de Postman contiene todos los encabezados necesarios para realizar llamadas de API a las distintas colecciones que se proporcionan a continuación. Una vez configurado, cada vez que caduca un valor (como un `ACCESS_TOKEN`), puede actualizar el valor actual en el entorno y este nuevo valor se utilizará en todas las colecciones.

>[!VIDEO](https://video.tv.adobe.com/v/31627?captions=spa)

## Colecciones de Postman {#collections}

Para encontrar una carpeta que contenga todas las colecciones de Postman disponibles, visite el [repositorio de GitHub de muestras de Experience Platform Postman](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/experience-platform). Como alternativa, se puede encontrar un vínculo de colección de Postman en cada archivo swagger individual en la [documentación de referencia de API](https://www.adobe.com/go/platform-api-reference-en) en Adobe I/O.

Para descargar una colección de Postman, seleccione **[!DNL Raw]** de la página de GitHub para cargar el archivo JSON sin procesar en una nueva pestaña. A continuación, haga clic con el botón derecho y seleccione **[!DNL Save as]** para guardar el archivo en un destino local de su elección.

![JSON sin procesar](./images/api-guide/raw-collection.PNG)

## Importar una colección de Postman {#import}

Para utilizar una [colección de Postman](#collections), necesita tener configurado un entorno. Una vez que haya completado la configuración de su entorno, seleccione el selector **[!DNL Manage Environments]** en la esquina superior derecha.

![administrar selector de entorno](./images/api-guide/environment-selector.png)

Aparece una ventana emergente que muestra todos los entornos actuales. Para importar una colección, seleccione **[!DNL import]**

![botón de importación](./images/api-guide/import-collection.png)

Se le pedirá que elija un archivo para importar. Seleccione el archivo de recopilación de Postman que desea importar. Una vez seleccionada, la colección se rellena en el carril izquierdo bajo la pestaña Colecciones.

![colección completada](./images/api-guide/imported-collection.png)

Cada colección tiene diferentes pares de clave-valor que pueden ser necesarios para realizar una operación CRUD correcta. Consulte la [Guía para desarrolladores de API](api-guide.md#api-guides) del servicio para obtener información sobre los valores y sugerencias necesarios, y vea ejemplos.

Para obtener más información acerca de la interfaz de usuario de Postman y sus características disponibles, visita la [documentación de Postman](https://learning.postman.com/docs/getting-started/navigating-postman/).

### Generación de un token de acceso con Postman para uso que no sea de producción

>[!WARNING]
>
>Como se indica en la colección Postman del servicio Identity Management (IMS), los métodos de generación indicados son adecuados para **uso que no sea de producción**. La firma local carga una biblioteca de JavaScript desde un host de terceros y la firma remota envía la clave privada a un servicio web que es propiedad de Adobe y que administra. Aunque Adobe no almacena esta clave privada, las claves de producción nunca deben compartirse con nadie.

El siguiente vídeo utiliza la [colección Postman del servicio Identity Management (IMS)](https://github.com/adobe/experience-platform-postman-samples/blob/master/apis/ims/Identity%20Management%20Service.postman_collection.json) que se puede descargar del repositorio público de GitHub.

>[!VIDEO](https://video.tv.adobe.com/v/32727/?quality=12&learn=on&captions=spa)

## Pasos siguientes

Este documento presentaba entornos, colecciones y cómo importar colecciones de Postman. Ahora que Postman está listo, visite la [Guía de introducción de Experience Platform](api-guide.md) para obtener información sobre los encabezados, ejemplos y una lista de [guías de API](api-guide.md#api-guides) disponibles para cada servicio de Experience Platform.
