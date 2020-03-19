---
title: Recuperando información de biblioteca
seo-title: Recuperación de información de biblioteca con el SDK web de Adobe Experience Platform
description: Obtenga información sobre cómo recuperar la biblioteca cargada en el sitio web
seo-description: Descubra cómo recuperar información sobre la biblioteca cargada en el sitio web por El SDK de Adobe Experience Cloud recopila automáticamente
translation-type: tm+mt
source-git-commit: 0cc6e233646134be073d20e2acd1702d345ff35f

---


# (Beta) Recuperación de información de biblioteca

>[!IMPORTANT]
>
>El SDK web de la plataforma de experiencia de Adobe se encuentra en fase beta y no está disponible para todos los usuarios. La documentación y la funcionalidad están sujetas a cambios.

A menudo resulta útil acceder a algunos de los detalles de la biblioteca que ha cargado en su sitio web. Para ello, ejecute el `getLibraryInfo` comando de la siguiente manera:

```js
alloy("getLibraryInfo").then(function(libraryInfo) {
  console.log(libraryInfo.version);
});
```

Actualmente, el objeto proporcionado `libraryInfo` contiene las siguientes propiedades:

* `version` Esta es la versión de la biblioteca cargada. Por ejemplo, si la versión de la biblioteca que se carga fuera 1.0.0, el valor sería `1.0.0`.