---
keywords: Experience Platform;introducción;inteligencia artificial aplicada al cliente;temas populares;entrada de inteligencia artificial aplicada al cliente;salida de inteligencia artificial aplicada al cliente;solución de problemas de inteligencia artificial aplicada al cliente;errores de inteligencia artificial aplicada al cliente
solution: Experience Platform, Real-time Customer Data Platform
feature: Customer AI
title: Solución de errores de Customer AI
description: Encuentre respuestas a errores comunes en Customer AI.
type: Documentation
exl-id: 37ff4e85-da92-41ca-afd4-b7f3555ebd43
source-git-commit: 3bc750b5e1cf47cbca6b037d099936c80c926cf8
workflow-type: tm+mt
source-wordcount: '529'
ht-degree: 0%

---

# Solución de errores de Customer AI

La inteligencia artificial aplicada al cliente muestra errores cuando falla la formación, la puntuación y la configuración del modelo. En el **[!UICONTROL Instancias de servicio]** , una columna para **[!UICONTROL ÚLTIMO ESTADO DE EJECUCIÓN]** muestra uno de los siguientes mensajes: **[!UICONTROL Correcto]**, **[!UICONTROL Problema de formación]**, y **[!UICONTROL Error]**.

![último estado de ejecución](./images/errors/last-run-status.png)

En el caso de que **[!UICONTROL Error]** o **[!UICONTROL Problema de formación]** , puede seleccionar el estado de ejecución para abrir un panel lateral. El panel lateral contiene su **[!UICONTROL Último estado de ejecución]** y **[!UICONTROL Detalles de la última ejecución]**. **[!UICONTROL Detalles de la última ejecución]** contiene información sobre el motivo del error de ejecución. En caso de que la inteligencia artificial aplicada al cliente no pueda proporcionar detalles sobre el error, póngase en contacto con el servicio de asistencia técnica e incluya el código de error proporcionado.

<img src="./images/errors/last-run-details.png" width="300" /><br />

## No se puede acceder a la inteligencia artificial aplicada al cliente en Chrome de incógnito

Hay errores de carga en el modo incógnito de Google Chrome debido a las actualizaciones en la configuración de seguridad del modo incógnito de Google Chrome. El problema se está trabajando activamente con Chrome para convertir a experience.adobe.com en un dominio de confianza.

<img src="./images/errors/error.PNG" width="500" /><br />

### Corrección recomendada

Para solucionar este problema, debe agregar experience.adobe.com como sitio que siempre puede usar cookies. Comience por navegar hasta **chrome://settings/cookies**. A continuación, desplácese hacia abajo hasta la **Comportamientos personalizados** seguido de la selección de la **Añadir** junto a &quot;sitios que siempre pueden usar cookies&quot;. En la ventana emergente que aparece, copie y pegue `[*.]experience.adobe.com` a continuación, seleccione **Inclusión de cookies de terceros** casilla de verificación en este sitio. Una vez finalizado, seleccione **Añadir** y vuelva a cargar Customer AI en incógnito.

![corrección recomendada](./images/errors/cookies2.gif)

## La calidad del modelo es mala

Si recibe el error &quot;[!UICONTROL La calidad del modelo es mala. Se recomienda crear una aplicación nueva con la configuración modificada]&quot;. Siga los pasos recomendados a continuación para solucionar los problemas.

<img src="./images/errors/model-quality.png" width="300" /><br />

### Corrección recomendada

&quot;La calidad del modelo es mala&quot; significa que la precisión del modelo no está dentro de un rango aceptable. La inteligencia artificial aplicada al cliente no pudo crear un modelo fiable y el AUC (área bajo la curva ROC) &lt; 0,65 después del entrenamiento. Para corregir el error, se recomienda cambiar uno de los parámetros de configuración y volver a ejecutar la formación.

Comience por comprobar la precisión de los datos. Es importante que los datos contengan los campos necesarios para el resultado predictivo.

- Compruebe si el conjunto de datos tiene las fechas más recientes. La inteligencia artificial aplicada al cliente siempre supone que los datos están actualizados cuando se activa el modelo.
- Compruebe si faltan datos en la ventana de predicción e idoneidad definida. Los datos deben estar completos sin interrupciones. Asegúrese también de que el conjunto de datos cumpla los [Requisitos de datos históricos de Customer AI](./data-requirements.md#data-requirements).
- Compruebe si faltan datos en las propiedades de comercio, aplicación, web y búsqueda del campo de esquema.

Si los datos no parecen ser el problema, intente cambiar la condición de población de elegibilidad para restringir el modelo a ciertos perfiles (por ejemplo, `_experience.analytics.customDimensions.eVars.eVar142` existe en los últimos 56 días). Esto restringe la población y el tamaño de los datos utilizados en la ventana de formación.

Si la restricción de la población elegible no ha funcionado o no es posible, cambie la ventana de predicción.

- Pruebe a cambiar la ventana de predicción a 7 días y vea si el error persiste. Si el error ya no se produce, esto indica que es posible que no tenga suficientes datos para la ventana de predicción definida.
