---
title: Información general sobre la instalación del SDK web
description: Obtenga información sobre cómo instalar el SDK web de Experience Platform.
keywords: instalación del sdk web;instalar el sdk web;internet explorer;promise;npm package
exl-id: b1de7ca1-d0d2-4661-a273-a1acf29afcd5
source-git-commit: f75dcfc945be2f45c1638bdd4d670288aef6e1e6
workflow-type: tm+mt
source-wordcount: '231'
ht-degree: 0%

---

# Información general sobre la instalación del SDK web

Hay tres formas de utilizar el SDK web de Adobe Experience Platform:

1. **[Extensión de etiquetas de SDK web](extension.md)**: el Adobe recomienda utilizar este método. Instale un cargador de etiquetas en el sitio y, a continuación, utilice la IU de recopilación de datos de Adobe Experience Platform para configurar la implementación.
1. **[Biblioteca JavaScript de SDK web](library.md)**: Haga referencia a un archivo de biblioteca alojado en CDN o aloje el archivo de biblioteca con su propia infraestructura. Realice llamadas a la biblioteca dentro del código del sitio.
1. **[NPM](npm.md)**: instale el SDK web en su sitio mediante el administrador de paquetes NPM

## Requisitos previos

Antes de utilizar o instalar el SDK web, debe cumplir los siguientes requisitos:

* La arquitectura de Adobe Experience Platform debe configurarse primero. Esta configuración incluye cualquier esquema, identidad y flujo de datos necesarios.
* Debe tener configurados los permisos adecuados para acceder a las herramientas adecuadas. Por ejemplo, si su organización decide utilizar la extensión de etiqueta, debe tener los permisos correctos para acceder a la IU de recopilación de datos. Consulte [administración de permisos de recopilación de datos](https://experienceleague.adobe.com/docs/experience-platform/collection/permissions.html?lang=es) para obtener más información.
* Se recomienda tener un dominio de origen (CNAME). Si ya tiene un CNAME para Adobe Analytics, puede utilizarlo. Las pruebas en desarrollo funcionan sin un CNAME, pero Adobe recomienda tenerlas antes de publicarlas en producción. Consulte [ID de dispositivos de origen](../identity/first-party-device-ids.md) para obtener más información.
