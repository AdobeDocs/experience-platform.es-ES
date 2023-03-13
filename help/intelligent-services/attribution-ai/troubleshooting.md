---
keywords: Experience Platform;introducción;inteligencia artificial aplicada a la atribución;temas populares;entrada de ia de atribución;salida de ia de atribución;solución de problemas de ia de atribución;errores de ia de atribución
solution: Experience Platform, Real-time Customer Data Platform
feature: Attribution AI
title: solución de problemas de Attribution AI
description: Encuentre respuestas a errores comunes en Attribution AI.
type: Documentation
exl-id: c2ff700a-1e36-4ba2-876c-9f8b56344241
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '167'
ht-degree: 0%

---

# solución de problemas de Attribution AI

Este documento proporciona respuestas a las preguntas frecuentes acerca de Attribution AI.

## No se puede acceder a la Attribution AI de incógnito de Chrome

Hay errores de carga en el modo incógnito de Google Chrome debido a las actualizaciones en la configuración de seguridad del modo incógnito de Google Chrome. El problema se está trabajando activamente con Chrome para convertir a experience.adobe.com en un dominio de confianza.

<img src="./images/faq/error.PNG" width="500" /><br />

### Corrección recomendada

Para solucionar este problema, debe agregar experience.adobe.com como sitio que siempre puede usar cookies. Comience por navegar hasta **chrome://settings/cookies**. A continuación, desplácese hacia abajo hasta la **Comportamientos personalizados** seguido de la selección de la **Añadir** junto a &quot;sitios que siempre pueden usar cookies&quot;. En la ventana emergente que aparece, copie y pegue `[*.]experience.adobe.com` a continuación, seleccione **Inclusión de cookies de terceros** casilla de verificación en este sitio. Una vez finalizado, seleccione **Añadir** y vuelva a cargar el Attribution AI de incógnito.

![corrección recomendada](./images/faq/cookies2.gif)
