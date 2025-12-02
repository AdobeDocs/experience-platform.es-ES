---
title: Información general sobre la instalación de Web SDK
description: Obtenga información sobre cómo instalar Experience Platform Web SDK.
keywords: instalación del sdk web;instalar el sdk web;internet explorer;promise;npm package
exl-id: b1de7ca1-d0d2-4661-a273-a1acf29afcd5
source-git-commit: a490c429047f5e5997d69f30a51e6b78debe2d5d
workflow-type: tm+mt
source-wordcount: '229'
ht-degree: 0%

---

# Información general sobre la instalación de Web SDK

Existen tres formas compatibles de utilizar Adobe Experience Platform Web SDK:

1. **[Extensión de etiquetas Web SDK](/help/tags/extensions/client/web-sdk/overview.md)**: Adobe recomienda utilizar este método. Instale un cargador de etiquetas en el sitio y, a continuación, utilice la IU de recopilación de datos de Adobe Experience Platform para configurar la implementación.
1. **[Biblioteca Web SDK JavaScript](library.md)**: Haga referencia a un archivo de biblioteca alojado en CDN o aloje el archivo de biblioteca utilizando su propia infraestructura. Realice llamadas a la biblioteca dentro del código del sitio.
1. **[NPM](npm.md)**: instale Web SDK en su sitio mediante el administrador de paquetes NPM.

## Requisitos previos

Antes de utilizar o instalar Web SDK, debe cumplir los siguientes requisitos:

* La arquitectura de Adobe Experience Platform debe configurarse primero. Esta configuración incluye cualquier esquema, identidad y flujo de datos necesarios.
* Debe tener configurados los permisos adecuados para acceder a las herramientas adecuadas. Por ejemplo, si su organización decide utilizar la extensión de etiqueta, debe tener los permisos correctos para acceder a la IU de recopilación de datos. Consulte [Permisos de recopilación de datos](../../permissions.md) para obtener más información.
* Se recomienda tener un dominio de origen (CNAME). Si ya tiene un CNAME para Adobe Analytics, puede utilizarlo. Las pruebas en desarrollo funcionan sin un CNAME, pero Adobe recomienda tenerlas antes de publicarlas en producción. Consulte [ID de dispositivos de origen](../../use-cases/identity/first-party-device-ids.md) para obtener más información.
