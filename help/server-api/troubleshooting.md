---
title: Resolución de problemas
description: Obtenga información sobre cómo solucionar errores al utilizar la API de Adobe Experience Platform Edge Network Server
seo-description: Learn how to troubleshoot errors when using the Adobe Experience Platform Edge Network Server API
keywords: red perimetral;puerta de enlace;api;solución de problemas;errores;griffon
exl-id: f0223fca-30ec-4229-93a5-3faa6cef5482
source-git-commit: 422f859bef8faf292fd7e5fd8b6a8d31967421c1
workflow-type: tm+mt
source-wordcount: '106'
ht-degree: 1%

---

# Resolución de problemas

La API de Adobe Experience Platform Edge Network Server permite capturar información de depuración de servicios, ya que los eventos se procesan mediante el canalizador de recopilación de datos de Edge Network.

El mismo mecanismo que utiliza el [Experience Platform Debugger](https://experienceleague.adobe.com/docs/debugger-learn/tutorials/experience-platform-debugger/introduction-to-the-experience-platform-debugger.html?lang=en) permite depurar implementaciones basadas en API.

Uso [Griffon del proyecto](https://aep-sdks.gitbook.io/docs/beta/project-griffon), puede crear un ID de sesión de depuración que se puede utilizar en las solicitudes de red perimetral para rastrear eventos.
