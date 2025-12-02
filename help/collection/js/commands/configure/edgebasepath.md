---
title: edgeBasePath
description: Ruta base del extremo que se utiliza para interactuar con los servicios de Adobe.
exl-id: 3542575d-ad02-415c-8e47-97c877dfdd9d
source-git-commit: 1fa7b48f99948a5252635dc1a8c5142fea5df57b
workflow-type: tm+mt
source-wordcount: '110'
ht-degree: 0%

---

# `edgeBasePath`

La propiedad `edgeBasePath` modifica la ruta de destino al interactuar con los servicios de Adobe. Adobe puede solicitar que cambie esta variable si participa en programas alfa o beta para la recopilación de datos. La mayoría de las organizaciones no necesitan establecer o modificar esta propiedad.

Establezca el campo de texto `edgeBasePath` al ejecutar el comando `configure`. Si omite esta propiedad, el valor predeterminado será `ee`. Adobe recomienda omitir esta propiedad en la mayoría de las configuraciones.

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  edgeBasePath: "ee"
});
```

## Ruta base de Edge con la extensión de etiquetas Web SDK

El equivalente de la extensión de etiquetas Web SDK de este campo se encuentra en [Opciones de configuración avanzadas](/help/tags/extensions/client/web-sdk/configure/advanced-settings.md) al configurar la extensión de etiquetas.
