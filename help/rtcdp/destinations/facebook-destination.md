---
keywords: facebook extensions;facebook extension;facebook destinations;facebook;instagram;messenger;facebook messenger
title: Destino de Facebook
seo-title: Destino de Facebook
description: Active perfiles para sus campañas de Facebook para objetivos de audiencia, personalización y supresión basados en correos electrónicos con hash.
seo-description: Active perfiles para sus campañas de Facebook para objetivos de audiencia, personalización y supresión basados en correos electrónicos con hash.
translation-type: tm+mt
source-git-commit: c66fb4cf0a414e02ceb58becc9d9b59db3fe987b
workflow-type: tm+mt
source-wordcount: '758'
ht-degree: 4%

---


# [!DNL Facebook] Destino

## Información general {#overview}

Active perfiles para sus [!DNL Facebook] campañas para la segmentación, personalización y supresión de audiencias en base a correos electrónicos con hash.

Puede usar este destino para la segmentación de audiencias en [!DNL Facebook’s] varias familias de aplicaciones compatibles con [!DNL Custom Audiences], incluidas [!DNL Facebook], [!DNL Instagram][!DNL Audience Network] y [!DNL Messenger]. La selección de la aplicación con la que quiere ejecutar la campaña se indica en el nivel de colocación de [!DNL Facebook Ads Manager].

![Destino de Facebook en la interfaz de usuario de CDP en tiempo real](/help/rtcdp/destinations/assets/facebook-destination.png)


## Casos de uso

Para ayudarle a comprender mejor cómo y cuándo debe utilizar el destino, a continuación se presentan dos casos de uso de muestra que los clientes de la Plataforma de datos de clientes en tiempo real de Adobe pueden solucionar con esta función. [!DNL Facebook]


### Caso de uso n.º 1


Un minorista en línea quiere llegar a los clientes existentes a través de las plataformas sociales y mostrarles ofertas personalizadas basadas en sus pedidos anteriores. El minorista en línea puede ingerir direcciones de correo electrónico desde su propia CRM a Adobe de CDP en tiempo real, generar segmentos a partir de sus propios datos sin conexión y enviar estos segmentos a la plataforma [!DNL Facebook] social, optimizando así la inversión en publicidad.


### Caso de uso n.º 2


Una aerolínea tiene diferentes niveles de clientes (bronce, plata y oro), y quiere ofrecer a cada uno de los niveles ofertas personalizadas a través de las plataformas sociales. Sin embargo, no todos los clientes utilizan la aplicación móvil de la aerolínea y algunos de ellos no han iniciado sesión en el sitio web de la compañía. Los únicos identificadores que tiene la compañía sobre estos clientes son los ID de pertenencia y las direcciones de correo electrónico.

Para destinatario en los medios sociales, pueden incorporar los datos del cliente desde su CRM al CDP en tiempo real de Adobe, utilizando las direcciones de correo electrónico como identificadores.

A continuación, pueden utilizar sus datos sin conexión, incluidos los ID de pertenencia asociados y los niveles de cliente, para crear nuevos segmentos de audiencia que pueden realizar destinatarios a través del [!DNL Facebook] destino.

## Especificaciones del destino {#destination-specs}

### Administración de datos para [!DNL Facebook] destinos {#data-governance}

>[!IMPORTANT]
>
>Los datos enviados a no [!DNL Facebook] deben incluir identidades vinculadas. Usted es responsable de cumplir esta obligación y puede hacerlo asegurándose de que los segmentos seleccionados para la activación no utilicen una opción de vinculación en su política de combinación. Obtenga más información sobre las políticas [de](/help/profile/ui/merge-policies.md)combinación.

### Tipo de exportación {#export-type}

**Exportación** de segmentos: está exportando todos los miembros de un segmento (audiencia) con los identificadores (nombre, número de teléfono, etc.) se usa en el destino de Facebook.

### Requisitos previos de cuenta de Facebook {#facebook-account-prerequisites}

Antes de enviar los segmentos de audiencia a [!DNL Facebook], asegúrese de cumplir los siguientes requisitos:

1. Su cuenta [!DNL Facebook] de usuario debe tener el **[!DNL Manage campaigns]** permiso habilitado para la cuenta de publicidad que planea usar.
2. Add the **Adobe Experience Cloud** business account as an advertising partner in your [!DNL Facebook Ad Account]. En su lugar, utilice `business ID=206617933627973`. Consulte [Añadir socios a su administrador](https://www.facebook.com/business/help/1717412048538897) comercial en la documentación de Facebook para obtener más información.
   >[!IMPORTANT]
   >
   > When configuring the permissions for Adobe Experience Cloud, you must enable the **Manage campaigns** permission. Es necesario para la integración de [!DNL Adobe Real-time CDP].
3. Lea y firme las [!DNL Facebook Custom Audiences] Condiciones de servicio. Para ello, vaya a `https://business.facebook.com/ads/manage/customaudiences/tos/?act=[accountID]`, donde `accountID` es su [!DNL Facebook Ad Account ID].

### Requisitos de hash de correo electrónico {#email-hashing-requirements}

[!DNL Facebook] exige que no se envíe con claridad ninguna información de identificación personal. Por lo tanto, las audiencias activadas en [!DNL Facebook] deben bloquearse las direcciones de correo electrónico con *hash* . Puede elegir hash las direcciones de correo electrónico antes de ingerirlas en Adobe Experience Platform, o puede elegir trabajar con las direcciones de correo electrónico de forma clara en Experience Platform y hacer que nuestro algoritmo las incluya en activación.

Para obtener más información sobre la ingesta de direcciones de correo electrónico en Experience Platform, consulte la información general [sobre la ingestión de](/help/ingestion/batch-ingestion/overview.md) lotes y la información general [sobre la ingestión](/help/ingestion/streaming-ingestion/overview.md)por lotes.

Si selecciona hash para las direcciones de correo electrónico usted mismo, asegúrese de cumplir con los siguientes requisitos:

* Recorte todos los espacios al inicio y al final de la cadena de correo electrónico; ejemplo: `johndoe@example.com`, no `<space>johndoe@example.com<space>`;
* Al aplicar hash a las cadenas de correo electrónico, asegúrese de que la cadena está en minúsculas;
   * Ejemplo: `example@email.com`, no `EXAMPLE@EMAIL.COM`;
* Asegúrese de que la cadena con hash esté en minúsculas
   * Ejemplo: `55e79200c1635b37ad31a378c39feb12f120f116625093a19bc32fff15041149`, no `55E79200C1635B37AD31A378C39FEB12F120F116625093A19bC32FFF15041149`;
* No escriba la cadena.


>[!IMPORTANT]
>
>Si decide no usar hash en las direcciones de correo electrónico, Adobe Real-time CDP lo hará por usted cuando active segmentos en [!DNL Facebook]. En el flujo de trabajo [de](/help/rtcdp/destinations/activate-destinations.md#activate-data) activación (consulte el paso 5), seleccione la `Email` opción como se muestra a continuación para las direcciones *de correo electrónico* sin procesar y `Email_LC_SHA256` para las direcciones *de correo electrónico* con hash.


![Hashing en activación](/help/rtcdp/destinations/assets/identity-mapping.png)

## Conectar al destino {#connect-destination}

Para conectarse al [!DNL Facebook] destino, consulte Flujo de trabajo [de autenticación de destinos de red](/help/rtcdp/destinations/social-network-destinations-workflow.md)social.


## Activar segmentos para [!DNL Facebook] {#activate-segments}

Para obtener instrucciones sobre cómo activar segmentos en [!DNL Facebook], consulte [Activar datos en destinos](/help/rtcdp/destinations/activate-destinations.md).

## Datos exportados {#exported-data}

Por [!DNL Facebook], una activación exitosa significa que se crearía una audiencia [!DNL Facebook] personalizada mediante programación en [[!DNL Facebook Ads Manager]](https://www.facebook.com/adsmanager/manage/). La pertenencia a segmentos en la audiencia se agregaría y eliminaría a medida que los usuarios estuvieran cualificados o descalificados para los segmentos activados.

>[!TIP]
>
>La integración entre CDP en tiempo real de Adobe y [!DNL Facebook] admite los rellenos históricos de audiencias. Todas las cualificaciones del segmento histórico se envían [!DNL Facebook] cuando activa los segmentos en el destino.