---
keywords: destinos; preguntas; preguntas más frecuentes; faq; destinos faq
title: Preguntas frecuentes
description: Respuestas a las preguntas más frecuentes sobre destinos de Adobe Experience Platform
exl-id: 2c34ecd0-a6d0-48dd-86b0-a144a6acf61a
source-git-commit: a6fe0f5a0c4f87ac265bf13cb8bba98252f147e0
workflow-type: tm+mt
source-wordcount: '864'
ht-degree: 4%

---

# Preguntas frecuentes {#faq}

## Información general {#overview}

Este documento proporciona respuestas a las preguntas frecuentes acerca de los destinos de Adobe Experience Platform. Para preguntas y resolución de problemas relacionados con otros [!DNL Platform] servicios, incluidos los que se encuentran en todos los [!DNL Platform] API, consulte la [guía de solución de problemas del Experience Platform](../landing/troubleshooting.md).

## Preguntas sobre destinos generales {#general}

**¿Por qué veo diferentes recuentos de perfiles en la interfaz de usuario de Experience Platform y en los archivos CSV exportados?**

Se trata de un comportamiento normal debido a la forma en que el Experience Platform realiza la segmentación.

La segmentación por transmisión actualiza el recuento de perfiles de los segmentos de transmisión por secuencias a lo largo del día, mientras que la segmentación por lotes actualiza el recuento de perfiles de los segmentos por lotes una vez cada 24 horas.

Cuando la programación de exportación de segmentos difiere de la programación de segmentación, el perfil cuenta entre la interfaz de usuario y el segmento exportado [!DNL CSV] El archivo será diferente, especialmente cuando se trata de segmentos de flujo continuo.

Consulte la [Documentación del Servicio de segmentación](../segmentation/home.md) para obtener más información.

## [!DNL Facebook Custom Audiences] {#facebook-faq}

**¿Qué debo hacer antes de poder activar audiencias en? [!DNL Facebook Custom Audiences]?**

Antes de enviar los segmentos de audiencia a [!DNL Facebook], asegúrese de cumplir los siguientes requisitos:

* Su [!DNL Facebook] la cuenta de usuario debe tener el **[!DNL Manage campaigns]** permiso habilitado para la cuenta de Ad que planea usar.
* El **Adobe Experience Cloud** La cuenta comercial de debe añadirse como socio de publicidad en su [!DNL Facebook Ad Account]. En su lugar, utilice `business ID=206617933627973`. Consulte [Añadir socios a su administrador comercial](https://www.facebook.com/business/help/1717412048538897) en la documentación de Facebook para obtener más información.
   >[!IMPORTANT]
   >
   > Al configurar los permisos para Adobe Experience Cloud, debe habilitar la variable **Administración de campañas** permiso. Es necesario para la integración de [!DNL Adobe Experience Platform].
* Lea y firme el [!DNL Facebook Custom Audiences] Condiciones del servicio. Para ello, vaya a `https://business.facebook.com/ads/manage/customaudiences/tos/?act=[accountID]`, donde `accountID` es su [!DNL Facebook Ad Account ID].

**¿Debo agregar aplicaciones o píxeles a mi [!DNL Facebook] ¿cuenta del anunciante?**

No. Como no se trata de una integración basada en píxeles, no es necesario añadir píxeles a la cuenta del anunciante.

**¿Cuánto tiempo tarda Facebook en procesar la información de Adobe Experience Platform?**

En marzo de 2021, [!DNL Facebook Custom Audiences] necesita hasta una hora para procesar la información recibida de [!DNL Platform].

**¿Puedo usar [!DNL Facebook Custom Audiences] para la segmentación de audiencias en otros [!DNL Facebook] aplicaciones, como [!DNL Instagram]?**

Puede usar el complemento [!DNL Facebook Custom Audiences] destino para la segmentación de audiencias en toda la familia de aplicaciones de Facebook compatibles con [!DNL Facebook Custom Audiences], incluido [!DNL Facebook], [!DNL Instagram], [!DNL Audience Network], y [!DNL Messenger]. La selección de la aplicación en la que los anunciantes desean ejecutar campañas se indica en el nivel de ubicación en [!DNL Facebook Ads Manager].

**¿Cuál es la diferencia entre las [!DNL Facebook Custom Audiences] conexión y [!DNL Facebook Pixel] ¿Extensión?**

El [!DNL Facebook Custom Audiences] la conexión utiliza [!DNL Platform] identidades al enviar audiencias a [!DNL Facebook], mientras que el [[!DNL Facebook Pixel] conexión](../destinations/catalog/advertising/facebook-pixel.md) utiliza el [!DNL Facebook] píxel integrado en un sitio web.

Estas dos integraciones son complementarias; pueden utilizarse las dos para garantizar una mejor cobertura de audiencia. Por ejemplo, puede utilizar la variable [!DNL Facebook Pixel] extensión para la prospección de visitantes de sitios web que no hayan creado una cuenta, mientras que [!DNL Facebook Custom Audiences] puede ayudarle a segmentar clientes existentes según lo siguiente [!DNL Platform] identidades.

**¿La integración de Adobe Experience Platform con [!DNL Facebook Custom Audiences] ¿permitir que se descalifique a los usuarios de una audiencia cuando ya no cumplen los requisitos?**

Sí, la integración permite eliminar usuarios de [!DNL Facebook Custom Audiences] cuando ya no cumplan los requisitos.

**¿Cómo debo hash los datos de audiencia antes de enviarlos a? [!DNL Facebook]?**

[!DNL Facebook] requiere que no se envíe información de identificación personal (PII) de forma clara. Por lo tanto, las audiencias se activan para [!DNL Facebook] se puede cerrar con llave *con hash* identificadores, como direcciones de correo electrónico o números de teléfono.

Para obtener explicaciones detalladas sobre los requisitos de coincidencia de ID, consulte [Requisitos de coincidencia de ID](catalog/social/facebook.md#id-matching-requirements).

**Qué tipo de identidades puedo activar en [!DNL Facebook Custom Audiences]?**

[!DNL Facebook Custom Audiences] admite la activación de las siguientes identidades: correos electrónicos con hash, números de teléfono con hash, [!DNL GAID], [!DNL IDFA]y los ID externos personalizados.

**¿Puedo crear varios destinos de Facebook en la interfaz de usuario de Platform para cuentas de Facebook independientes?**

Sí. Un destino de Facebook en Experience Platform es 1:1 en una cuenta de publicidad en Facebook. Puede crear un destino de Facebook independiente para cada cuenta de publicidad de Facebook de su compañía. Siga las [tutorial de conexión de destino](/help/destinations/ui/connect-destination.md) y conectarse a una cuenta de Facebook independiente para cada nuevo destino de Facebook en la interfaz de usuario de Platform. No hay límite en el número de cuentas de publicidad de Facebook a las que puede conectarse.

## Coincidencia de clientes de Google {#google-customer-match}

**Al exportar segmentos a Google Customer Match, ¿por qué veo números adicionales anexados al final de los nombres de segmentos en la interfaz de Google?**

Google requiere que los nombres de los segmentos sean únicos. Los números que está viendo son [Marcas de tiempo UNIX](https://www.unixtimestamp.com/) y se anexan para mantener los nombres de segmento únicos, si ha asignado el mismo segmento a varios destinos de Google.

## Audiencias coincidentes de linkedIn {#linkedin}

**¿Debo agregar aplicaciones o píxeles a mi [!DNL LinkedIn] ¿cuenta del anunciante?**

No. Como no se trata de una integración basada en píxeles, no es necesario añadir píxeles a la cuenta del anunciante.

**¿Qué debo hacer antes de poder activar audiencias en? [!DNL LinkedIn Matched Audiences]?**

Antes de usar el [!UICONTROL Audiencia coincidente de linkedIn] destino, asegúrese de que su [!DNL LinkedIn Campaign Manager] La cuenta tiene el [!DNL Creative Manager] nivel de permiso o superior.

Para obtener información sobre cómo editar su [!DNL LinkedIn Campaign Manager] permisos de usuario, consulte [Agregar, editar y quitar permisos de usuario en cuentas publicitarias](https://www.linkedin.com/help/lms/answer/5753) en la documentación de LinkedIn.

**¿Cómo debo hash los datos de audiencia antes de enviarlos a? [!DNL LinkedIn]?**

[!DNL LinkedIn] requiere que no se envíe información de identificación personal (PII) de forma clara. Por lo tanto, las audiencias se activan para [!DNL LinkedIn] se puede cerrar con llave *con hash* identificadores, como direcciones de correo electrónico o números de teléfono.

Para obtener explicaciones detalladas sobre los requisitos de coincidencia de ID, consulte [Requisitos de coincidencia de ID](catalog/social/linkedin.md#id-matching-requirements).

**Qué tipo de identidades puedo activar en [!DNL LinkedIn]?**

[!DNL LinkedIn Matched Audiences] admite la activación de las siguientes identidades: correos electrónicos con hash, [!DNL GAID], y [!DNL IDFA].
