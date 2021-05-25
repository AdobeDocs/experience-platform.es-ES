---
keywords: destinos; preguntas; preguntas más frecuentes; faq; preguntas más frecuentes sobre destinos
title: Preguntas frecuentes
seo-title: Preguntas frecuentes
description: Respuestas a las preguntas más frecuentes sobre los destinos de Adobe Experience Platform
seo-description: Respuestas a las preguntas más frecuentes sobre los destinos de Adobe Experience Platform
source-git-commit: 47b3ef28281e3480e8b194486845f4fb4326b7d4
workflow-type: tm+mt
source-wordcount: '636'
ht-degree: 6%

---


# Preguntas frecuentes {#faq}

## Información general {#overview}

Este documento proporciona respuestas a las preguntas más frecuentes sobre los destinos de Adobe Experience Platform. Para preguntas y solución de problemas relacionados con otros [!DNL Platform] servicios, incluidos los que se encuentran en todas las API [!DNL Platform], consulte la [guía de solución de problemas del Experience Platform](../landing/troubleshooting.md).

## [!DNL Facebook Custom Audiences] {#facebook-faq}

**¿Qué debo hacer antes de poder activar audiencias en  [!DNL Facebook Custom Audiences]?**

Antes de enviar los segmentos de audiencia a [!DNL Facebook], asegúrese de cumplir los siguientes requisitos:

* Su cuenta de usuario [!DNL Facebook] debe tener el permiso **[!DNL Manage campaigns]** habilitado para la cuenta de anuncio que planea usar.
* La cuenta empresarial de **Adobe Experience Cloud** debe agregarse como socio publicitario en su [!DNL Facebook Ad Account]. En su lugar, utilice `business ID=206617933627973`. Consulte [Añadir socios a su administrador empresarial](https://www.facebook.com/business/help/1717412048538897) en la documentación de Facebook para obtener más información.
   >[!IMPORTANT]
   >
   > Al configurar los permisos para Adobe Experience Cloud, debe habilitar el permiso **Administrar campañas**. Es necesario para la integración de [!DNL Adobe Experience Platform].
* Lea y firme las [!DNL Facebook Custom Audiences] Condiciones de servicio. Para ello, vaya a `https://business.facebook.com/ads/manage/customaudiences/tos/?act=[accountID]`, donde `accountID` es su [!DNL Facebook Ad Account ID].

**¿Debo añadir aplicaciones o píxeles a mi cuenta de  [!DNL Facebook] anunciante?**

No. Como no se trata de una integración basada en píxeles, no es necesario añadir ningún píxel a la cuenta del anunciante.

**¿Cuánto tiempo tarda Facebook en procesar la información de Adobe Experience Platform?**

A partir de marzo de 2021, [!DNL Facebook Custom Audiences] necesita hasta una hora para procesar la información recibida de [!DNL Platform].

**¿Puedo usar  [!DNL Facebook Custom Audiences] para segmentación de audiencia en otras  [!DNL Facebook] aplicaciones, como  [!DNL Instagram]?**

Puede utilizar el destino [!DNL Facebook Custom Audiences] para la segmentación de audiencia en toda la familia de aplicaciones de Facebook compatibles con [!DNL Facebook Custom Audiences], incluidos [!DNL Facebook], [!DNL Instagram], [!DNL Audience Network] y [!DNL Messenger]. La selección de la aplicación en la que los anunciantes desean ejecutar campañas se indica en el nivel de ubicación en [!DNL Facebook Ads Manager].

**¿Cuál es la diferencia entre la  [!DNL Facebook Custom Audiences] conexión y la  [!DNL Facebook Pixel] extensión?**

La conexión [!DNL Facebook Custom Audiences] utiliza identidades [!DNL Platform] al enviar audiencias a [!DNL Facebook], mientras que la [[!DNL Facebook Pixel] conexión](../destinations/catalog/advertising/facebook-pixel.md) utiliza el píxel [!DNL Facebook] integrado en un sitio web.

Estas dos integraciones son complementarias; pueden utilizarse las dos para garantizar una mejor cobertura de audiencia. Por ejemplo, puede utilizar la extensión [!DNL Facebook Pixel] para la prospección de visitantes de sitios web que no hayan creado una cuenta, mientras que [!DNL Facebook Custom Audiences] puede ayudarle a dirigirse a los clientes existentes, según las identidades [!DNL Platform] .

**¿La integración de Adobe Experience Platform con  [!DNL Facebook Custom Audiences] permite descalificar a los usuarios de una audiencia cuando ya no cumplen los requisitos para ella?**

Sí, la integración admite la eliminación de usuarios de [!DNL Facebook Custom Audiences] cuando ya no cumplen los requisitos.

**¿Cómo debo hash los datos de audiencia antes de enviarlos a  [!DNL Facebook]?**

[!DNL Facebook] exige que no se envíe con claridad ninguna información de identificación personal (PII). Por lo tanto, las audiencias activadas en [!DNL Facebook] pueden desactivarse mediante identificadores *hash*, como direcciones de correo electrónico o números de teléfono.

Para obtener explicaciones detalladas sobre los requisitos de coincidencia de ID, consulte [Requisitos de coincidencia de ID](catalog/social/facebook.md#id-matching-requirements).

**¿Qué tipo de identidades puedo activar en  [!DNL Facebook Custom Audiences]?**

[!DNL Facebook Custom Audiences] admite la activación de las siguientes identidades: correos electrónicos con hash, números de teléfono con hash,  [!DNL GAID],  [!DNL IDFA] e ID externos personalizados.

## Audiencias coincidentes de linkedIn {#linkedin}

**¿Debo añadir aplicaciones o píxeles a mi cuenta de  [!DNL LinkedIn] anunciante?**

No. Como no se trata de una integración basada en píxeles, no es necesario añadir ningún píxel a la cuenta del anunciante.

**¿Qué debo hacer antes de poder activar audiencias en  [!DNL LinkedIn Matched Audiences]?**

Antes de usar el destino [!UICONTROL Audiencia coincidente con LinkedIn] , asegúrese de que su cuenta [!DNL LinkedIn Campaign Manager] tenga el nivel de permiso [!DNL Creative Manager] o superior.

Para obtener información sobre cómo editar los permisos de usuario de [!DNL LinkedIn Campaign Manager], consulte [Agregar, editar y eliminar permisos de usuario en cuentas publicitarias](https://www.linkedin.com/help/lms/answer/5753) en la documentación de LinkedIn.

**¿Cómo debo hash los datos de audiencia antes de enviarlos a  [!DNL LinkedIn]?**

[!DNL LinkedIn] exige que no se envíe con claridad ninguna información de identificación personal (PII). Por lo tanto, las audiencias activadas en [!DNL LinkedIn] pueden desactivarse mediante identificadores *hash*, como direcciones de correo electrónico o números de teléfono.

Para obtener explicaciones detalladas sobre los requisitos de coincidencia de ID, consulte [Requisitos de coincidencia de ID](catalog/social/linkedin.md#id-matching-requirements).

**¿Qué tipo de identidades puedo activar en  [!DNL LinkedIn]?**

[!DNL LinkedIn Matched Audiences] admite la activación de las siguientes identidades: correos electrónicos con hash,  [!DNL GAID] y  [!DNL IDFA].
