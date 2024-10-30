---
title: Lanzamiento de una extensión
description: Obtenga información sobre cómo publicar de forma privada o pública una extensión de etiqueta en Adobe Experience Platform.
exl-id: a5eb6902-4b0f-4717-a431-a290c50fb5a6
source-git-commit: 2152cf98d9809654cca7abd7b8469a72e8387b2a
workflow-type: tm+mt
source-wordcount: '479'
ht-degree: 67%

---

# Lanzamiento de una extensión

>[!NOTE]
>
>Adobe Experience Platform Launch se ha convertido en un grupo de tecnologías de recopilación de datos en Adobe Experience Platform. Como resultado, se han implementado varios cambios terminológicos en la documentación del producto. Consulte el siguiente [documento](../../term-updates.md) para obtener una referencia consolidada de los cambios terminológicos.

Una vez finalizadas las pruebas y la documentación, la extensión está lista para su lanzamiento. Actualmente, puede realizar dos tipos de lanzamientos:

- **Lanzamiento privado**: la extensión completada está disponible para todas las propiedades de la compañía, pero no lo está para otras compañías de Adobe Experience Platform.
- **Lanzamiento público**: La extensión completada está disponible en el mercado público para todos los usuarios de Adobe Experience Platform.

>[!NOTE]
>
>Una vez realizado el lanzamiento de la extensión, ya no podrá cambiarla y no podrá cancelar el lanzamiento.  Una vez realizado el lanzamiento, las correcciones de errores y la incorporación de funciones se realizan utilizando el comando `POST`, que permite publicar una nueva versión del paquete de extensión, y siguiendo los pasos de prueba y lanzamiento descritos anteriormente con dicha nueva versión.

Primero debe realizar el lanzamiento de la extensión como extensión privada para poder lanzarla públicamente.

## Lanzamiento privado

La manera más fácil de realizar el lanzamiento de tu extensión con disponibilidad privada consiste en usar el [publicador de extensiones de etiqueta](https://www.npmjs.com/package/@adobe/reactor-releaser).

```bash
npx @adobe/reactor-releaser
```

`npx` le permite descargar y ejecutar un paquete npm sin instalarlo realmente en su equipo. Esta es la forma más sencilla de ejecutar el publicador.

>[!NOTE]
> De forma predeterminada, el publicador espera credenciales de Adobe I/O para un flujo de Oauth de servidor a servidor. Las credenciales heredadas de `jwt-auth`
> se puede usar ejecutando `npx @adobe/reactor-releaser@v3.1.3` hasta que quede obsoleto el 1 de enero de 2025. Los parámetros necesarios
> para ejecutar la versión `jwt-auth` se puede encontrar [aquí](https://github.com/adobe/reactor-releaser/tree/9ea66aa2c683fe7da0cca50ff5c9b9372f183bb5).

El publicador requiere que introduzca solo unos pocos datos. `clientId` y `clientSecret` se pueden recuperar de la consola de Adobe I/O. Vaya a la [página Integraciones](https://console.adobe.io/integrations) en la consola de I/O. Seleccione la organización correcta en el menú desplegable, busque la integración correcta y seleccione **[!UICONTROL Ver]**.

- ¿Cuál es su `clientId`? Copie y pegue esto desde la consola de I/O.
- ¿Cuál es su `clientSecret`? Copie y pegue esto desde la consola de I/O.

El publicador leerá los campos `name` y `platform` de su manifiesto de extensión y consultará la API para obtener un paquete de extensión coincidente en la disponibilidad de desarrollo.
El publicador le pedirá que confirme que ha encontrado el paquete de extensión correcto que desea publicar en disponibilidad privada.

Si desea realizar el lanzamiento de su extensión de manera privada directamente mediante la API, consulte la llamada de ejemplo de [lanzamiento privado de un paquete de extensión](../../api/endpoints/extension-packages.md/#private-release) en los documentos de la API para obtener más información.

## Lanzamiento público

Una vez completado el lanzamiento privado, puede solicitar a Adobe el lanzamiento público. Esto hará que su extensión esté disponible en el catálogo público. Cualquier usuario de recopilación de datos podrá instalar su extensión en cualquier propiedad.

Complete el [formulario de solicitud de lanzamiento público](https://www.feedbackprogram.adobe.com/c/r/DCExtensionReleaseRequest) para comenzar el proceso de lanzamiento.
