---
keywords: Experience Platform;introducción;ai del cliente;temas populares;entrada de la interfaz del cliente;salida de la interfaz del cliente;solución de problemas de la interfaz del cliente;errores de la interfaz del cliente
solution: Experience Platform, Intelligent Services, Real-time Customer Data Platform
title: Solución de errores de Customer AI
topic-legacy: Getting started
description: Encuentre respuestas a errores comunes en Customer AI.
type: Documentation
source-git-commit: ceb203899cda83aa79b994d45798d6147c3ff3b8
workflow-type: tm+mt
source-wordcount: '409'
ht-degree: 0%

---


# Solución de errores de Customer AI

Customer AI muestra errores cuando falla la formación, puntuación y configuración del modelo. En la sección **[!UICONTROL Service instances]** , una columna para **[!UICONTROL LAST RUN STATUS]** muestra uno de los siguientes mensajes: **[!UICONTROL Success]**, **[!UICONTROL Training issue]** y **[!UICONTROL Failed]**.

![estado de última ejecución](./images/errors/last-run-status.png)

En el caso de que se muestre **[!UICONTROL Failed]** o **[!UICONTROL Training issue]** , puede seleccionar el estado de ejecución para abrir un panel lateral. El panel lateral contiene su **[!UICONTROL Último estado de ejecución]** y **[!UICONTROL Detalles de la última ejecución]**. **[!UICONTROL Los]** detalles de la última ejecución contienen información sobre por qué la ejecución falló. En el caso de que Customer AI no pueda proporcionar detalles sobre su error, póngase en contacto con el servicio de asistencia técnica con el código de error proporcionado.

<img src="./images/errors/last-run-details.png" width="300" /><br />

## La calidad del modelo es deficiente

Si recibe el error &quot;[!UICONTROL Calidad del modelo es deficiente. Se recomienda crear una aplicación nueva con la configuración modificada]&quot;. Siga los pasos recomendados a continuación para solucionar problemas.

<img src="./images/errors/model-quality.png" width="300" /><br />

### Corrección recomendada

&quot;La calidad del modelo es deficiente&quot; significa que la precisión del modelo no se encuentra dentro de un rango aceptable. Customer AI no pudo construir un modelo y un AUC fiables (Área bajo la curva ROC) &lt; 0,65 después de la formación. Para solucionar el error, se recomienda cambiar uno de los parámetros de configuración y volver a ejecutar la formación.

Comience por comprobar la precisión de sus datos. Es importante que los datos contengan los campos necesarios para el resultado predictivo.

- Compruebe si el conjunto de datos tiene las fechas más recientes. Customer AI siempre supone que los datos están actualizados cuando se activa el modelo.
- Compruebe si faltan datos en la ventana de predicción y elegibilidad definida. Los datos deben completarse sin espacios. Asegúrese también de que su conjunto de datos cumpla los [requisitos de datos históricos de Customer AI](./input-output.md#data-requirements).
- Compruebe si faltan datos en comercio, aplicación, web y búsqueda, dentro de las propiedades del campo de esquema.

Si los datos no parecen ser el problema, intente cambiar la condición de población de elegibilidad para restringir el modelo a ciertos perfiles (por ejemplo, `_experience.analytics.customDimensions.eVars.eVar142` existe en los últimos 56 días). Esto restringe la población y el tamaño de los datos utilizados en la ventana de capacitación.

Si la restricción de la población elegible no funcionaba o no era posible, cambie la ventana de predicción.

- Intente cambiar la ventana de predicción a 7 días y vea si el error sigue ocurriendo. Si el error ya no se produce, esto indica que es posible que no tenga datos suficientes para la ventana de predicción definida.

