---
title: Lanzamiento de una extensión
description: Obtenga información sobre cómo publicar de forma privada o pública una extensión de etiqueta en Adobe Experience Platform.
source-git-commit: 39d9468e5d512c75c9d540fa5d2bcba4967e2881
workflow-type: tm+mt
source-wordcount: '320'
ht-degree: 58%

---

# Lanzamiento de una extensión

>[!NOTE]
>
>Adobe Experience Platform Launch se está convirtiendo en un conjunto de tecnologías de recopilación de datos en Experience Platform. Como resultado, se han implementado varios cambios terminológicos en la documentación del producto. Consulte el siguiente [documento](../../term-updates.md) para obtener una referencia consolidada de los cambios terminológicos.

Una vez finalizadas las pruebas y la documentación, la extensión está lista para su lanzamiento. Actualmente, puede realizar dos tipos de lanzamientos:

- **Lanzamiento privado**: la extensión completada está disponible para todas las propiedades de la compañía, pero no lo está para otras compañías de Adobe Experience Platform.
- **Versión** pública: La extensión completada está disponible en el mercado público para todos los usuarios de Adobe Experience Platform.

>[!NOTE]
>
>Una vez publicada la extensión, ya no puede realizar cambios y no puede cancelarla.  Una vez realizado el lanzamiento, las correcciones de errores y la incorporación de funciones se realizan utilizando el comando `POST`, que permite publicar una nueva versión del paquete de extensión, y siguiendo los pasos de prueba y lanzamiento descritos anteriormente con dicha nueva versión.

Debe realizar el lanzamiento de su extensión como extensión privada para poder lanzarla públicamente.

## Lanzamiento privado

La forma más sencilla de publicar la extensión con disponibilidad privada es utilizar el [lanzador de extensiones de etiqueta](https://www.npmjs.com/package/@adobe/reactor-releaser). Encontrará más instrucciones en su documentación.

Si desea publicar la extensión con disponibilidad privada utilizando la API directamente, consulte la llamada de ejemplo para [publicar de forma privada un paquete de extensión](https://developer.adobelaunch.com/api/reference/1.0/extension_packages/release_private/) en los documentos de API para obtener más información.

## Lanzamiento público

Una vez completado el lanzamiento privado, puede solicitar a Adobe el lanzamiento público. Esto hará que su extensión esté disponible en el catálogo público. Cualquier usuario de recopilación de datos puede instalar la extensión en cualquier propiedad.

Complete el [formulario de solicitud de lanzamiento público](https://adobe.allegiancetech.com/cgi-bin/qwebcorporate.dll?idx=7DRB5U) para comenzar el proceso de lanzamiento.
