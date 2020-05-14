---
title: Recuperando información de biblioteca
seo-title: Recuperación de información de biblioteca con el SDK web de Adobe Experience Platform
description: Obtenga información sobre cómo recuperar la biblioteca cargada en el sitio web
seo-description: Descubra cómo recuperar información sobre la biblioteca cargada en el sitio web por El SDK de Adobe Experience Cloud recopila automáticamente
translation-type: tm+mt
source-git-commit: e9fb726ddb84d7a08afb8c0f083a643025b0f903
workflow-type: tm+mt
source-wordcount: '104'
ht-degree: 0%

---


# Recuperando información de biblioteca

A menudo resulta útil acceder a algunos de los detalles de la biblioteca que ha cargado en su sitio web. Para ello, ejecute el `getLibraryInfo` comando de la siguiente manera:

```js
alloy("getLibraryInfo").then(function(libraryInfo) {
  console.log(libraryInfo.version);
});
```

Actualmente, el objeto proporcionado `libraryInfo` contiene las siguientes propiedades:

* `version` Esta es la versión de la biblioteca cargada. Por ejemplo, si la versión de la biblioteca que se carga fuera 1.0.0, el valor sería `1.0.0`.