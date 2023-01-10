---
keywords: Experience Platform;inicio;temas populares;esquema;esquema;XDM;campos;esquemas;esquemas;detalles de página web;tipo de datos;tipo de datos;tipo de datos;página web
solution: Experience Platform
title: Tipo de datos de información web
description: Este documento proporciona información general sobre el tipo de datos del Modelo de datos de experiencias (XDM).
exl-id: bfb00835-5908-4baf-af2a-6d845710e340
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '190'
ht-degree: 3%

---

# [!UICONTROL Información web] tipo de datos

[!UICONTROL Información web] es un tipo de datos estándar del Modelo de datos de experiencia (XDM) que describe información registrada mediante un Evento de experiencia que es específico del canal World Wide Web, incluida la página web, el referente o el vínculo relacionado con la interacción en la página.

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
