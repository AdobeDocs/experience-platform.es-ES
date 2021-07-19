---
keywords: Experience Platform;inicio;temas populares;esquema;esquema;XDM;campos;esquemas;esquemas;detalles de página web;tipo de datos;tipo de datos;tipo de datos;página web
solution: Experience Platform
title: Tipo de datos de información web
topic-legacy: overview
description: Este documento proporciona información general sobre el tipo de datos del Modelo de datos de experiencias (XDM).
source-git-commit: 12c3f440319046491054b3ef3ec404798bb61f06
workflow-type: tm+mt
source-wordcount: '190'
ht-degree: 2%

---

# [!UICONTROL Tipo de datos de ] información web

[!UICONTROL La ] información web es un tipo de datos estándar del Modelo de datos de experiencia (XDM) que describe la información registrada mediante un Evento de experiencia específico del canal World Wide Web, incluida la página web, el referente o el vínculo relacionado con la interacción en la página.

![](../images/data-types/web-information.png)

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `webInteraction` | [[!UICONTROL Interacción web]](./web-interaction.md) | Describe los detalles sobre el vínculo web o la dirección URL que corresponde a la interacción. |
| `webPageDetails` | [[!UICONTROL Detalles de la página web]](./webpage-details.md) | Describe los detalles sobre la página web en la que se produjo la interacción web. |
| `webReferrer` | [!UICONTROL Objeto] | Describe el referente de una interacción web, que es la dirección URL de la que procedía un visitante inmediatamente antes de registrar la interacción web actual. Contiene las siguientes subpropiedades: <ul><li>`URL`: La dirección URL del referente.</li><li>`type`: El tipo de referente.</li></ul> |

{style=&quot;table-layout:auto&quot;}

Para obtener más información sobre el tipo de datos, consulte el repositorio XDM público:

* [Ejemplo rellenado](https://github.com/adobe/xdm/blob/master/components/datatypes/webinfo.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/webinfo.schema.json)
