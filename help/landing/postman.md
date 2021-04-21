---
keywords: Experience Platform;inicio;temas populares;Adobe Experience Platform;guía de la api;guía de la api de platform;introducción a platform;guía para desarrolladores
solution: Experience Platform
title: Postman en Adobe Experience Platform
topic-legacy: api guide
description: Este documento contiene pasos que describen cómo configurar un entorno Postman, importar colecciones Postman y una lista de colecciones disponibles para cada servicio de Platform.
exl-id: a09b3875-97f5-47f1-a562-52decbce67b1
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '550'
ht-degree: 0%

---

# Postman en Adobe Experience Platform

Postman es una plataforma de colaboración para el desarrollo de API que le permite configurar entornos con variables preestablecidas, compartir colecciones de API, optimizar solicitudes CRUD y mucho más. La mayoría de los servicios de API de plataforma tienen colecciones Postman que se pueden utilizar para ayudar a realizar llamadas de API.

## Configuración de un entorno Postman para Experience Platform

La siguiente guía de vídeo describe la creación y configuración del entorno Postman. Un entorno Postman contiene todos los encabezados necesarios para realizar llamadas de API a las distintas colecciones que se proporcionan a continuación. Una vez configurado, cada vez que un valor caduque (como `ACCESS_TOKEN`), podrá actualizar el valor actual en el entorno y este nuevo valor se utilizará en todas sus colecciones.

>[!VIDEO](https://video.tv.adobe.com/v/28832)

## Colecciones Postman {#collections}

Puede encontrar una carpeta que contenga todas las colecciones Postman disponibles en, visitando el [Experience Platform Postman muestra el repositorio de GitHub](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/experience-platform). Alternativamente, se puede encontrar un vínculo de recopilación de Postman en cada archivo de intercambio individual en la [documentación de referencia de la API](http://www.adobe.com/go/platform-api-reference-en) en el Adobe I/O.

Para descargar una colección de Postman, seleccione **[!DNL Raw]** en la página de GitHub para cargar el archivo JSON sin procesar en una nueva pestaña. A continuación, haga clic con el botón derecho y seleccione **[!DNL Save as]** para guardar el archivo en un destino local de su elección.

![JSON sin procesar](./images/api-guide/raw-collection.PNG)

## Importar una colección de Postman {#import}

Para utilizar una [colección Postman](#collections), debe tener configurado un entorno. Una vez completada la configuración del entorno, seleccione el selector **[!DNL Manage Environments]** en la esquina superior derecha.

![administrar selector de entorno](./images/api-guide/environment-selector.png)

Aparece una ventana emergente que muestra todos los entornos actuales. Para importar una colección, seleccione **[!DNL import]** .

![botón importar](./images/api-guide/import-collection.png)

Se le pedirá que elija un archivo para importar. Seleccione el archivo de colección Postman que desea importar. Una vez seleccionada, la colección se rellena en el carril izquierdo de la ficha Colecciones.

![colección rellenada](./images/api-guide/imported-collection.png)

Cada colección tiene diferentes pares de clave-valor que pueden ser necesarios para realizar una operación CRUD correcta. Revise la [guía para desarrolladores de API](api-guide.md#api-guides) del servicio para obtener más información sobre los valores, sugerencias y ver ejemplos necesarios.

Para obtener más información sobre la interfaz de usuario de Postman y sus funciones disponibles, visite la [documentación de Postman](https://learning.postman.com/docs/getting-started/navigating-postman/).

### Generar un token de acceso con Postman para uso que no sea de producción

>[!WARNING]
>
>Como se indica en la colección Postman de generación de token de acceso a Adobe I/O, los métodos de generación indicados son adecuados para **usos que no sean de producción**. La firma local carga una biblioteca JavaScript desde un host de terceros y la firma remota envía la clave privada a un servicio web que es propiedad de y está gestionado por el Adobe. Aunque Adobe no almacena esta clave privada, las claves de producción nunca deben compartirse con nadie.

El siguiente vídeo utiliza la [colección de generación de tokens de acceso al Adobe I/O](https://github.com/adobe/experience-platform-postman-samples/blob/master/apis/ims/Adobe%20IO%20Access%20Token%20Generation.postman_collection.json) que se puede descargar del repositorio público de GitHub.

>[!VIDEO](https://video.tv.adobe.com/v/29698/?quality=12&learn=on)

## Pasos siguientes

Este documento introdujo entornos Postman, colecciones y cómo importar colecciones. Ahora que tiene Postman listo, visite la [Guía de introducción a la plataforma](api-guide.md) para obtener información sobre los encabezados, ejemplos y una lista de [guías de API](api-guide.md#api-guides) disponibles para cada servicio de Platform.
