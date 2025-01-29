---
keywords: Experience Platform;introducción;inteligencia artificial aplicada a la atribución;temas populares;entrada de ia de atribución;salida de ia de atribución;solución de problemas de ia de atribución;errores de ia de atribución
solution: Experience Platform, Real-Time Customer Data Platform
feature: Attribution AI
title: solución de problemas de Attribution AI
description: Encuentre respuestas a errores comunes en Attribution AI.
type: Documentation
exl-id: c2ff700a-1e36-4ba2-876c-9f8b56344241
source-git-commit: e028fbb82b37b3940b308a860c26f8b5f9884d3a
workflow-type: tm+mt
source-wordcount: '171'
ht-degree: 0%

---

# solución de problemas de Attribution AI

Este documento proporciona respuestas a las preguntas frecuentes acerca de Attribution AI.

## No se puede acceder a la Attribution AI de incógnito de Chrome

Los errores de carga en el modo incógnito de Google Chrome están presentes debido a las actualizaciones en la configuración de seguridad del modo incógnito de Google Chrome. El problema se está trabajando activamente con Chrome para hacer de experience.adobe.com un dominio de confianza.

![Imagen de error](./images/faq/error.PNG){width=500}

### Corrección recomendada

Para solucionar este problema, debe agregar experience.adobe.com como sitio que siempre puede usar cookies. Comience por navegar hasta **chrome://settings/cookies**. A continuación, desplácese hacia abajo hasta la sección **Comportamientos personalizados** y, a continuación, seleccione el botón **Agregar** junto a &quot;Sitios que siempre pueden usar cookies&quot;. En la ventana emergente que aparece, copie y pegue `[*.]experience.adobe.com` y, a continuación, active la casilla de verificación **Incluyendo cookies de terceros** en este sitio. Una vez finalizado, selecciona **Agregar** y vuelve a cargar el Attribution AI de incógnito.

![corrección recomendada](./images/faq/cookies2.gif)
