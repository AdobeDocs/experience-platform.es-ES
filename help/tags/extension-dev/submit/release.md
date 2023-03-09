---
title: Lanzamiento de una extensión
description: Obtenga información sobre cómo publicar de forma privada o pública una extensión de etiqueta en Adobe Experience Platform.
exl-id: a5eb6902-4b0f-4717-a431-a290c50fb5a6
source-git-commit: 3e349c5d78d964c8c2a5b635ef1866d4f41ef6bb
workflow-type: tm+mt
source-wordcount: '319'
ht-degree: 92%

---

# Lanzamiento de una extensión

>[!NOTE]
>
>Adobe Experience Platform Launch se ha convertido en un conjunto de tecnologías de recopilación de datos en Adobe Experience Platform. Como resultado, se han implementado varios cambios terminológicos en la documentación del producto. Consulte el siguiente [documento](../../term-updates.md) para obtener una referencia consolidada de los cambios terminológicos.

Una vez finalizadas las pruebas y la documentación, la extensión está lista para su lanzamiento. Actualmente, puede realizar dos tipos de lanzamientos:

- **Lanzamiento privado**: la extensión completada está disponible para todas las propiedades de la compañía, pero no lo está para otras compañías de Adobe Experience Platform.
- **Lanzamiento público**: La extensión completada está disponible en el mercado público para todos los usuarios de Adobe Experience Platform.

>[!NOTE]
>
>Una vez realizado el lanzamiento de la extensión, ya no podrá cambiarla y no podrá cancelar el lanzamiento.  Una vez realizado el lanzamiento, las correcciones de errores y la incorporación de funciones se realizan utilizando el comando `POST`, que permite publicar una nueva versión del paquete de extensión, y siguiendo los pasos de prueba y lanzamiento descritos anteriormente con dicha nueva versión.

Debe realizar el lanzamiento de su extensión como extensión privada para poder lanzarla públicamente.

## Lanzamiento privado

La manera más fácil de realizar el lanzamiento de la extensión con disponibilidad privada consiste en utilizar el [publicador de extensiones de etiqueta](https://www.npmjs.com/package/@adobe/reactor-releaser). Encontrará más instrucciones en su documentación.

Si desea realizar el lanzamiento de su extensión de manera privada directamente mediante la API, consulte la llamada de ejemplo de [lanzamiento privado de un paquete de extensión](https://developer.adobelaunch.com/api/reference/1.0/extension_packages/release_private/) en los documentos de la API para obtener más información.

## Lanzamiento público

Una vez completado el lanzamiento privado, puede solicitar a Adobe el lanzamiento público. Esto hará que su extensión esté disponible en el catálogo público. Cualquier usuario de recopilación de datos podrá instalar su extensión en cualquier propiedad.

Complete el [formulario de solicitud de lanzamiento público](https://www.feedbackprogram.adobe.com/c/r/DCExtensionReleaseRequest) para comenzar el proceso de lanzamiento.
