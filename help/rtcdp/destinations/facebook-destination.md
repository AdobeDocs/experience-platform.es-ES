---
title: Destino de Facebook
seo-title: Destino de Facebook
description: Active perfiles para sus campañas de Facebook para objetivos de audiencia, personalización y supresión basados en correos electrónicos con hash.
seo-description: Active perfiles para sus campañas de Facebook para objetivos de audiencia, personalización y supresión basados en correos electrónicos con hash.
translation-type: tm+mt
source-git-commit: bfcbc56f05fa1c3b5fafd57b1166e50130b6007d

---


# (Beta) Destino de Facebook

>[!IMPORTANT]
>
>El destino de Facebook en Adobe Real-time CDP está actualmente en fase beta y no está disponible para todos los usuarios. La documentación y las funciones están sujetas a cambios.

## Información general

Active perfiles para sus campañas de Facebook para objetivos de audiencia, personalización y supresión basados en correos electrónicos con hash.

## Especificaciones de destino

### Tipo de Activación

Exportación de segmentos: está exportando todos los miembros de un segmento (audiencia) con sus identificadores (nombre, número de teléfono, etc.) utilizado en el destino de Facebook

## Requisitos previos

Antes de enviar los segmentos de audiencia a [!DNL Facebook], asegúrese de cumplir los siguientes requisitos:

1. Su cuenta [!DNL Facebook] de usuario debe tener el permiso **Administrar campañas** habilitado para la cuenta de publicidad que planea usar.
2. Añada la cuenta comercial de **Adobe Experience Cloud** como socio publicitario en su [!DNL Facebook Ad Account]. En su lugar, utilice `business ID=206617933627973`. Consulte [Añadir socios a su administrador](https://www.facebook.com/business/help/1717412048538897) comercial para obtener más información.
   >[!IMPORTANT]
   > Al configurar los permisos para Adobe Experience Cloud, debe habilitar el permiso **Administrar campañas** . Esto es necesario para la [!DNL Adobe Real-time CDP] integración.
3. Lea y firme las [!DNL Facebook Custom Audiences] Condiciones de servicio. Para hacerlo, vaya a `https://business.facebook.com/ads/manage/customaudiences/tos/?act=[accountID]`, donde `accountID` está su [!DNL Facebook Ad Account ID].


## Destino de Connect

Para conectar el destino de Facebook, consulte Flujo de trabajo [de autenticación de destinos de red](/help/rtcdp/destinations/social-network-destinations-workflow.md)social.


## Activar segmentos en Facebook

Para obtener instrucciones sobre cómo activar segmentos en Facebook, consulte [Activar datos en destinos](/help/rtcdp/destinations/activate-destinations.md).