---
title: Configuración de extensión
description: Obtenga información sobre cómo configurar una extensión de etiqueta para recopilar la configuración global de un usuario en la IU de Adobe Experience Platform o la IU de recopilación de datos.
exl-id: 2bf33617-1398-499f-8325-3849dbdb1f97
source-git-commit: 44e2b8241a8c348d155df3061d398c4fa43adcea
workflow-type: tm+mt
source-wordcount: '229'
ht-degree: 89%

---

# Configuración de extensión

La configuración de extensión es la forma en que una extensión recopila la configuración global de un usuario. Por ejemplo, considere una extensión que permita al usuario enviar una señalización mediante la acción Enviar señalización y la señalización siempre debe contener un ID de cuenta. No queremos molestar a los usuarios pidiéndoles el ID de cuenta cada vez que configuren una acción Enviar señalización. En su lugar, la extensión debe solicitar el ID de la cuenta una vez desde la vista de configuración de la extensión. De este modo, cada vez que se envíe una señalización, el módulo de biblioteca de acciones Enviar señalización podrá extraer el ID de cuenta de la configuración de la extensión y añadirlo a la señalización.

Cuando los usuarios instalan una extensión en una propiedad de etiqueta de Adobe Experience Platform, se les mostrará la vista de configuración de la extensión que proporcionará su extensión. No pueden completar la instalación de la extensión sin completar la configuración de esta. Consulte el documento acerca de las [vistas](./web/views.md) para obtener información sobre cómo crear una vista para la configuración de la extensión.

Una vez guardadas las opciones de configuración desde una vista de configuración de extensión, se emitirán en la biblioteca de tiempo de ejecución de etiquetas. A continuación, podrá acceder a esta configuración desde los módulos de biblioteca de extensiones llamando a [`turbine.getExtensionSettings()`](./turbine.md#get-extension-settings).

La configuración de la extensión es una función opcional que puede optar por no utilizar.
