---
keywords: Experience Platform;introducción;ai de atribución;temas populares;entrada de ai de atribución;salida de ai de atribución;solución de problemas de ai de atribución;errores de ai de atribución
solution: Experience Platform, Real-time Customer Data Platform
feature: Attribution AI
title: solución de errores de Attribution AI
description: Encuentre respuestas a errores comunes en Attribution AI.
type: Documentation
exl-id: c2ff700a-1e36-4ba2-876c-9f8b56344241
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '167'
ht-degree: 0%

---

# solución de errores de Attribution AI

Este documento proporciona respuestas a las preguntas más frecuentes sobre la Attribution AI.

## No se puede acceder al Attribution AI en Chrome incógnito

Los errores de carga en el modo incógnito de Google Chrome están presentes debido a las actualizaciones en la configuración de seguridad del modo incógnito de Google Chrome. El problema se está trabajando activamente con Chrome para que experience.adobe.com sea un dominio de confianza.

<img src="./images/faq/error.PNG" width="500" /><br />

### Corrección recomendada

Para solucionar este problema, debe agregar experience.adobe.com como sitio que siempre puede usar cookies. Para empezar, vaya a **chrome://settings/cookies**. A continuación, desplácese hacia abajo hasta el **Comportamientos personalizados** seguido de seleccionar la **Agregar** situado junto a &quot;sitios que siempre pueden utilizar cookies&quot;. En la ventana emergente que aparece, copie y pegue `[*.]experience.adobe.com` a continuación, seleccione la **Inclusión de cookies de terceros** en esta casilla de verificación del sitio. Una vez finalizada, seleccione **Agregar** y recargue la Attribution AI en incógnito.

![corrección recomendada](./images/faq/cookies2.gif)
