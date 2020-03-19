---
title: Destino de Google
seo-title: Destino de Google
description: El CDP en tiempo real de Adobe se integra con Google para permitirle ejecutar y activar sus datos en DV360, Google Ad Manager, Google AdWords y Google AdX.
seo-description: El CDP en tiempo real de Adobe se integra con Google para permitirle ejecutar y activar sus datos en DV360, Google Ad Manager, Google AdWords y Google AdX.
translation-type: tm+mt
source-git-commit: 5396bee00044e5046bd768a863fceca0aec1d24e

---


# Destino de Google

## Información general

El CDP en tiempo real de Adobe se integra con Google para permitirle ejecutar y activar sus datos en DV360, Google Ad Manager, Google AdWords Display y Google AdX.

## Especificaciones de destino

Tenga en cuenta los siguientes detalles específicos de destinos de Google:

* Puede enviar las siguientes [identidades](https://www.adobe.io/apis/experienceplatform/home/profile-identity-segmentation/profile-identity-segmentation-services.html#!api-specification/markdown/narrative/technical_overview/identity_namespace_overview/identity_namespace_overview.md) a destinos de Google: ID de cookie de **Google, IDFA, GAID**.
* Las audiencias activadas se crean mediante programación en la plataforma Google.
* Actualmente, CDP en tiempo real de Adobe no incluye una métrica de medición para validar la activación correcta. Consulte los recuentos de audiencias en Google para validar la integración y comprender la lista desplegable de datos.

## Requisitos previos

### Lista blanca

Antes de conectar el destino de Google en Adobe Real-time CDP, debe ponerse en contacto con Google para solicitar que la cuenta se incluya en la lista de direcciones permitidas. Póngase en contacto con Google y proporcione la siguiente información:

* **ID** de cuenta: este es el ID de cuenta de Adobe con Google. Póngase en contacto con el servicio de asistencia técnica de Adobe para obtener este ID.
* **ID** del cliente: es el ID de cuenta de cliente de Adobe con Google. Póngase en contacto con el servicio de asistencia técnica de Adobe para obtener este ID.
* **ID** del socio: Este es su ID de socio de tres dígitos con Google;
* **ID** de red: esta es su cuenta con Google;
* **ID** del vínculo de audiencia: esta es su cuenta con Google;
* El tipo de cuenta. Podría ser **anunciante** de invitación, socio **de** invitación, **DFP**, **AdWords**, **AdX**.


## Destino de Connect

1. En **[!UICONTROL Conexiones > Destinos]**, seleccione Google y, a continuación, **[!UICONTROL Crear destino]**.
   ![Destino de Connect Google](/help/rtcdp/destinations/assets/google-destination.png)

2. En el asistente de destino de Connect, rellene la información básica del destino.
   ![Información básica Google](/help/rtcdp/destinations/assets/google-basic-information.png)
* **Nombre**: Rellene el nombre preferido para este destino.
* **Descripción**: Opcional. Por ejemplo, puede mencionar para qué campaña utiliza este destino.
* **Tipo** de cuenta: Seleccione una opción, en función de su cuenta con Google:
   * Uso `Invite advertiser` para Google DV360
   * Uso `Invite partner` para Google DV360
   * Usar `DFP by Google` para Google Ad Manager
   * Pantalla Usar `AdWords` para Google AdWords
   * Usar `AdX buyer` para Google AdX
* **ID** de cuenta: Rellene su ID de cuenta con Google.

>[!NOTE]
>
>Al configurar un destino de Google, trabaje con el administrador de cuentas de Google o con un representante de Adobe para comprender en qué tipo de producto se encuentra su cuenta. Para Google DV360, pregunte a su administrador de cuentas de Google en qué tipo de producto se encuentra su cuenta. 

## Activar segmentos en Google

Para obtener instrucciones sobre cómo activar segmentos en Google, consulte [Activar datos en destinos](/help/rtcdp/destinations/activate-destinations.md).