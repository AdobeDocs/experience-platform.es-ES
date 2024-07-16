---
keywords: Experience Platform;inicio;temas populares;esquema;XDM;esquemas;esquemas;Detalles de página web;tipo de datos;tipo de datos;tipo de datos;página web
solution: Experience Platform
title: Tipo de datos de información web
description: Obtenga información sobre el tipo de datos del modelo de datos de experiencia (XDM) de información web.
exl-id: bfb00835-5908-4baf-af2a-6d845710e340
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '166'
ht-degree: 2%

---

# [!UICONTROL Tipo de datos de información web]

[!UICONTROL Información web] es un tipo de datos estándar del Modelo de datos de experiencia (XDM) que describe la información registrada mediante un Evento de experiencia específico para el canal World Wide Web, incluidos la página web, el referente y/o el vínculo relacionado con la interacción en la página.

![](../images/data-types/web-information.png)

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `webInteraction` | [[!UICONTROL Interacción web]](./web-interaction.md) | Describe los detalles acerca del vínculo web o URL que corresponde a la interacción. |
| `webPageDetails` | [[!UICONTROL Detalles de la página web]](./webpage-details.md) | Describe los detalles de la página web donde se produjo la interacción web. |
| `webReferrer` | [!UICONTROL Objeto] | Describe el referente de una interacción web, que es la URL de la que viene un visitante inmediatamente antes de que se registre la interacción web actual. Contiene las siguientes subpropiedades: <ul><li>`URL`: la dirección URL del referente.</li><li>`type`: el tipo de referente.</li></ul> |

{style="table-layout:auto"}

Para obtener más información sobre el tipo de datos, consulte el repositorio XDM público:

* [Ejemplo completado](https://github.com/adobe/xdm/blob/master/components/datatypes/webinfo.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/webinfo.schema.json)
