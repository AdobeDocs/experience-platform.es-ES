---
keywords: destinos; preguntas; preguntas más frecuentes; faq; preguntas más frecuentes sobre destinos
title: Preguntas frecuentes
seo-title: Frequently asked questions
description: Respuestas a las preguntas más frecuentes sobre los destinos de Adobe Experience Platform
seo-description: Answers to the most frequently asked questions about Adobe Experience Platform destinations
exl-id: 2c34ecd0-a6d0-48dd-86b0-a144a6acf61a
source-git-commit: 8f9a601a833149c83d465f68d16ca362ed730b8a
workflow-type: tm+mt
source-wordcount: '781'
ht-degree: 4%

---

# Preguntas frecuentes {#faq}

## Información general {#overview}

Este documento proporciona respuestas a las preguntas más frecuentes sobre los destinos de Adobe Experience Platform. Para preguntas y solución de problemas relacionados con otras [!DNL Platform] servicios, incluidos los que se encuentran en todos los [!DNL Platform] API, consulte la [Guía de solución de problemas del Experience Platform](../landing/troubleshooting.md).

## Preguntas generales sobre destinos {#general}

**¿Por qué veo diferentes recuentos de perfiles en la interfaz de usuario del Experience Platform y en los archivos CSV exportados?**

Se trata de un comportamiento normal debido a la forma en que el Experience Platform realiza la segmentación.

La segmentación por transmisión actualiza el recuento de perfiles de los segmentos de flujo continuo a lo largo del día, mientras que la segmentación por lotes actualiza el recuento de perfiles de los segmentos por lotes una vez cada 24 horas.

Cuando la programación de exportación de segmentos difiere de la programación de segmentación, el perfil se cuenta entre la interfaz de usuario y la exportada [!DNL CSV] será diferente, especialmente cuando se trata de segmentos de flujo continuo.

Consulte la [Documentación del servicio de segmentación](../segmentation/home.md) para obtener más información.

## [!DNL Facebook Custom Audiences] {#facebook-faq}

**¿Qué debo hacer antes de poder activar audiencias en [!DNL Facebook Custom Audiences]?**

Antes de poder enviar los segmentos de audiencia a [!DNL Facebook], asegúrese de cumplir los siguientes requisitos:

* Su [!DNL Facebook] la cuenta de usuario debe tener la variable **[!DNL Manage campaigns]** permiso habilitado para la cuenta de anuncio que planea usar.
* La variable **Adobe Experience Cloud** la cuenta comercial debe agregarse como socio de publicidad en su [!DNL Facebook Ad Account]. En su lugar, utilice `business ID=206617933627973`. Consulte [Añadir socios a su administrador empresarial](https://www.facebook.com/business/help/1717412048538897) en la documentación de Facebook para obtener más información.
   >[!IMPORTANT]
   >
   > Al configurar los permisos para Adobe Experience Cloud, debe habilitar la variable **Administración de campañas** permiso. Es necesario para la integración de [!DNL Adobe Experience Platform].
* Lea y firme el [!DNL Facebook Custom Audiences] Condiciones de servicio. Para ello, vaya a `https://business.facebook.com/ads/manage/customaudiences/tos/?act=[accountID]`, donde `accountID` es su [!DNL Facebook Ad Account ID].

**¿Debo añadir aplicaciones o píxeles a mis [!DNL Facebook] cuenta del anunciante?**

No. Como no se trata de una integración basada en píxeles, no es necesario añadir ningún píxel a la cuenta del anunciante.

**¿Cuánto tiempo tarda Facebook en procesar la información de Adobe Experience Platform?**

A partir de marzo de 2021, [!DNL Facebook Custom Audiences] necesita hasta una hora para procesar la información recibida de [!DNL Platform].

**¿Puedo usar [!DNL Facebook Custom Audiences] para segmentación de audiencia en otros [!DNL Facebook] aplicaciones, como [!DNL Instagram]?**

Puede usar la variable [!DNL Facebook Custom Audiences] destino para la segmentación de audiencia en toda la familia de aplicaciones de Facebook compatibles con [!DNL Facebook Custom Audiences], incluyendo [!DNL Facebook], [!DNL Instagram], [!DNL Audience Network]y [!DNL Messenger]. La selección de la aplicación en la que los anunciantes desean ejecutar las campañas se indica en el nivel de ubicación de [!DNL Facebook Ads Manager].

**¿Cuál es la diferencia entre las variables [!DNL Facebook Custom Audiences] conexión y [!DNL Facebook Pixel] extensión?**

La variable [!DNL Facebook Custom Audiences] usos de conexión [!DNL Platform] identidades al enviar audiencias a [!DNL Facebook], mientras que la variable [[!DNL Facebook Pixel] connection](../destinations/catalog/advertising/facebook-pixel.md) utiliza la variable [!DNL Facebook] píxeles integrados en un sitio web.

Estas dos integraciones son complementarias; pueden utilizarse las dos para garantizar una mejor cobertura de audiencia. Como ejemplo, puede usar la variable [!DNL Facebook Pixel] extensión para los visitantes del sitio web de prospección que no hayan creado una cuenta, mientras que [!DNL Facebook Custom Audiences] puede ayudarle a segmentar clientes existentes, en función de [!DNL Platform] identidades.

**¿La integración de Adobe Experience Platform con [!DNL Facebook Custom Audiences] admiten la descalificación de usuarios de una audiencia cuando ya no cumplen los requisitos para ella?**

Sí, la integración permite eliminar usuarios de [!DNL Facebook Custom Audiences] cuando ya no cumplen los requisitos.

**¿Cómo debo hash los datos de audiencia antes de enviarlos a [!DNL Facebook]?**

[!DNL Facebook] exige que no se envíe con claridad ninguna información de identificación personal (PII). Por lo tanto, las audiencias activadas en [!DNL Facebook] se puede desactivar *hash* identificadores, como direcciones de correo electrónico o números de teléfono.

Para obtener explicaciones detalladas sobre los requisitos de coincidencia de ID, consulte [Requisitos de coincidencia de ID](catalog/social/facebook.md#id-matching-requirements).

**Qué tipo de identidades puedo activar en [!DNL Facebook Custom Audiences]?**

[!DNL Facebook Custom Audiences] admite la activación de las siguientes identidades: correos electrónicos con hash, números de teléfono con hash, [!DNL GAID], [!DNL IDFA]e ID externos personalizados.

**¿Puedo crear varios destinos de Facebook en la interfaz de usuario de Platform para cuentas de Facebook independientes?**

Un destino de Facebook en Experience Platform es 1:1 para una cuenta publicitaria en Facebook. Puede crear un destino de Facebook independiente para cada cuenta de publicidad de Facebook en su empresa. Siga las [tutorial de conexión de destino](/help/destinations/ui/connect-destination.md) y conéctese a una cuenta de Facebook independiente para cada nuevo destino de Facebook en la interfaz de usuario de Platform.

## Audiencias coincidentes de linkedIn {#linkedin}

**¿Debo añadir aplicaciones o píxeles a mis [!DNL LinkedIn] cuenta del anunciante?**

No. Como no se trata de una integración basada en píxeles, no es necesario añadir ningún píxel a la cuenta del anunciante.

**¿Qué debo hacer antes de poder activar audiencias en [!DNL LinkedIn Matched Audiences]?**

Antes de usar la variable [!UICONTROL Audiencia coincidente de linkedIn] destino, asegúrese de que su [!DNL LinkedIn Campaign Manager] La cuenta tiene el [!DNL Creative Manager] nivel de permiso o superior.

Para aprender a editar su [!DNL LinkedIn Campaign Manager] permisos de usuario, consulte [Agregar, editar y eliminar permisos de usuario en cuentas publicitarias](https://www.linkedin.com/help/lms/answer/5753) en la documentación de LinkedIn.

**¿Cómo debo hash los datos de audiencia antes de enviarlos a [!DNL LinkedIn]?**

[!DNL LinkedIn] exige que no se envíe con claridad ninguna información de identificación personal (PII). Por lo tanto, las audiencias activadas en [!DNL LinkedIn] se puede desactivar *hash* identificadores, como direcciones de correo electrónico o números de teléfono.

Para obtener explicaciones detalladas sobre los requisitos de coincidencia de ID, consulte [Requisitos de coincidencia de ID](catalog/social/linkedin.md#id-matching-requirements).

**Qué tipo de identidades puedo activar en [!DNL LinkedIn]?**

[!DNL LinkedIn Matched Audiences] admite la activación de las siguientes identidades: correos electrónicos con hash, [!DNL GAID]y [!DNL IDFA].
