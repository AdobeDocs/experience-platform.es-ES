---
title: Activar audiencias en destinos depurados según identificadores de LiveRamp
type: Tutorial
description: Aprenda a activar audiencias de Adobe Experience Platform en destinos de audio y TV conectados, y otras integraciones mediante LiveRamp RampID.
source-git-commit: adc7e66fa17484ccb9527650f197acc29ef4d0f1
workflow-type: tm+mt
source-wordcount: '646'
ht-degree: 0%

---


# Activar audiencias en destinos depurados según identificadores de LiveRamp

Uso de la integración de Adobe Real-Time CDP con [!DNL LiveRamp] para activar audiencias en una lista revisada de destinos que utilizan [!DNL [LiveRamp RampID]](https://docs.liveramp.com/connect/en/interpreting-rampid,-liveramp-s-people-based-identifier.html) para la activación, incluidos los destinos de audio y TV conectados, como los que se enumeran a continuación.

>[!IMPORTANT]
>
>No es necesario ingerir ni trabajar de ninguna manera con LiveRamp RampIDs en la interfaz del Experience Platform.
>
> Puede exportar identidades desde Real-Time CDP, como identificadores basados en PII, identificadores conocidos e ID personalizados, tal como se describe en el [Documentación de LiveRamp](https://docs.liveramp.com/connect/en/identity-and-identifier-terms-and-concepts.html#known-identifiers). Estas identidades coinciden con [!DNL LiveRamp RampIDs] más adelante en el proceso de activación.


* [[!DNL 4C Insights]](#insights)
* [[!DNL Acast]](#acast)
* [[!DNL Ampersand.tv]](#ampersand-tv)
* [[!DNL Captify]](#captify)
* [[!DNL Cardlytics]](#cardlytics)
* [[!DNL Disney (Hulu/ESPN/ABC)]](#disney)
* [[!DNL iHeartMedia]](#iheartmedia)
* [[!DNL Index Exchange]](#index-exchange)
* [[!DNL Magnite CTV Platform]](#magnite)
* [[!DNL Magnite DV+ (Rubicon Project)]](#magnite-dv)
* [[!DNL Nexxen]](#nexxen)
* [[!DNL One Fox]](#fox)
* [[!DNL Pandora]](#pandora)
* [[!DNL Reddit]](#reddit)
* [[!DNL Roku]](#roku)
* [[!DNL Spotify]](#spotify)
* [[!DNL Taboola]](#taboola)
* [[!DNL TargetSpot]](#targetspot)
* [[!DNL Teads]](#teads)
* [[!DNL WB Discovery]](#wb-discovery)

En este artículo se explica el flujo de trabajo necesario para activar audiencias desde Real-Time CDP a los destinos enumerados anteriormente, directamente desde la interfaz de usuario de Real-Time CDP.

## Flujo de trabajo de activación {#workflow}

Las audiencias se activan en destinos de audio y TV conectados siguiendo un proceso de dos pasos y utilizando [LiveRamp: incorporación](../catalog/advertising/liveramp-onboarding.md) y el [LiveRamp - Distribución](../catalog/advertising/liveramp-distribution.md) destinos, como se muestra en la siguiente imagen.

![Diagrama que muestra el flujo de trabajo para activar audiencias desde Real-Time CDP a destinos depurados, a través de LiveRamp.](../assets/ui/activate-curated-destinations-liveramp/workflow-diagram.png)

Primero, exporte las audiencias de Real-Time CDP a [[!DNL LiveRamp - Onboarding]](../catalog/advertising/liveramp-onboarding.md) destino, como archivos CSV.

Después de exportar las audiencias, puede activarlas con el complemento [[!DNL LiveRamp - Distribution]](../catalog/advertising/liveramp-distribution.md) destino.

>[!TIP]
>
>Este proceso le permite activar audiencias en destinos como [[!DNL Roku]](../catalog/advertising/liveramp-distribution.md#roku), [[!DNL Disney]](../catalog/advertising/liveramp-distribution.md#disney), etc., directamente desde la interfaz de usuario de Real-Time CDP, sin necesidad de iniciar sesión en su [!DNL LiveRamp] cuenta para la activación.

### Paso 1: Envíe sus audiencias de Experience Platform a LiveRamp, a través del [!DNL LiveRamp - Onboarding] destino {#onboarding}

Lo primero que debe hacer para activar sus audiencias en destinos depurados basados en LiveRamp RampID es **exporte sus audiencias de Experience Platform a[!DNL LiveRamp]**.

Para ello, utilice el **[!DNL LiveRamp - Onboarding]** destino.

![Imagen de la IU del Experience Platform que muestra la tarjeta de destino LiveRamp - Onboarding](../assets/ui/activate-curated-destinations-liveramp/liveramp-onboarding-catalog.png)

Para obtener información sobre cómo configurar [!DNL LiveRamp - Onboarding] y exporte sus audiencias desde Experience Platform, lea la [[!DNL LiveRamp - Onboarding]](../catalog/advertising/liveramp-onboarding.md) documentación de destino.

>[!IMPORTANT]
>
>Al exportar archivos a [!DNL LiveRamp - Onboarding] destino, Platform genera un archivo CSV para cada [ID de política de combinación](../../profile/merge-policies/overview.md). Consulte la [[!DNL LiveRamp - Onboarding]](../catalog/advertising/liveramp-onboarding.md) documentación de destino para obtener información detallada sobre cómo validar la exportación de datos a LiveRamp.


Después de exportar correctamente las audiencias a LiveRamp, continúe a [paso 2](#distribution).

>[!TIP]
>
>Antes de pasar a [paso 2](#distribution), [validate](../catalog/advertising/liveramp-onboarding.md#exported-data) que sus audiencias se han exportado correctamente a LiveRamp. Consulte la documentación sobre [monitorización de flujos de datos de destino](../../dataflows/ui/monitor-destinations.md#dataflow-runs-for-batch-destinations) y leer los detalles específicos de monitorización para [[!DNL LiveRamp - Onboarding]](../catalog/advertising/liveramp-onboarding.md#exported-data).

### Paso 2: Activar las audiencias integradas en destinos de audio y TV conectados, a través del [!DNL LiveRamp - Distribution] destino {#distribution}

Después de que tenga [validado](../catalog/advertising/liveramp-onboarding.md#exported-data) Si las audiencias se han exportado correctamente a LiveRamp, es hora de activar las audiencias en sus destinos preferidos, como [[!DNL Roku]](../catalog/advertising/liveramp-distribution.md#roku), [[!DNL Disney]](../catalog/advertising/liveramp-distribution.md#disney), y más.

Las audiencias (exportadas en ) se activan [paso 1](#onboarding)) mediante el uso de **[!DNL LiveRamp - Distribution]** destino.

![Imagen de la IU del Experience Platform que muestra la tarjeta de destino LiveRamp - Distribution](../assets/ui/activate-curated-destinations-liveramp/liveramp-distribution-catalog.png)

Para obtener información sobre cómo configurar **[!DNL LiveRamp - Distribution]** y active las audiencias que exportó en. [paso 1](#onboarding), lea la [[!DNL LiveRamp - Distribution]](../catalog/advertising/liveramp-distribution.md) documentación de destino.

>[!IMPORTANT]
>
>En el **selección de audiencia** paso del **[!DNL LiveRamp - Distribution]** destino, debe seleccionar el *exactamente las mismas audiencias* que ha exportado a la [LiveRamp: incorporación](../catalog/advertising/liveramp-onboarding.md) destino en [paso 1](#onboarding).

Al configurar la variable **[!DNL LiveRamp - Distribution]** debe crear una conexión dedicada para cada destino descendente que desee utilizar (Roku, Disney, etc.).

>[!TIP]
>
>Al asignar un nombre al destino, Adobe recomienda seguir este formato: `LiveRamp - Downstream Destination Name`. Este patrón de nomenclatura le ayuda a identificar rápidamente sus destinos en la [Examinar](../ui/destinations-workspace.md#browse) de la pestaña destinos de workspace.
><br>
>Ejemplo: `LiveRamp - Roku`.

![Captura de pantalla de la IU de Platform que muestra varios destinos de LiveRamp.](../assets/ui/activate-curated-destinations-liveramp/liveramp-naming.png)

## Datos exportados / Validar exportación de datos {#exported-data}

Para validar la exportación correcta de las audiencias a [[!DNL LiveRamp - Onboarding]](../catalog/advertising/liveramp-onboarding.md) destino, consulte la documentación sobre [monitorización de flujos de datos de destino](../../dataflows/ui/monitor-destinations.md#dataflow-runs-for-batch-destinations) y leer los detalles específicos de monitorización para [[!DNL LiveRamp - Onboarding]](../catalog/advertising/liveramp-onboarding.md#exported-data).

Para validar la activación correcta de las audiencias en la plataforma de publicidad que elija (como Roku, Disney y otras), inicie sesión en la cuenta de la plataforma de destino y compruebe las métricas de activación.
