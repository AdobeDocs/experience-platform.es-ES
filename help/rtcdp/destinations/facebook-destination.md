---
title: Destino de Facebook
seo-title: Destino de Facebook
description: Active perfiles para sus campañas de Facebook para objetivos de audiencia, personalización y supresión basados en correos electrónicos con hash.
seo-description: Active perfiles para sus campañas de Facebook para objetivos de audiencia, personalización y supresión basados en correos electrónicos con hash.
translation-type: tm+mt
source-git-commit: 522014f8e5f3de0f553a69763d3a37482953b7c4
workflow-type: tm+mt
source-wordcount: '665'
ht-degree: 0%

---


# Destino de Facebook

## Información general {#overview}

Active perfiles para sus campañas de Facebook para objetivos de audiencia, personalización y supresión basados en correos electrónicos con hash.

![Destino de Facebook en la interfaz de usuario de CDP en tiempo real](/help/rtcdp/destinations/assets/facebook-destination.png)

## Casos de uso

Para ayudarle a comprender mejor cómo y cuándo debe usar el destino de Facebook, aquí hay dos casos de uso de muestra que los clientes de la Plataforma de datos del cliente en tiempo real de Adobe pueden resolver con esta función.


### Caso de uso n.º 1


Un minorista en línea quiere llegar a los clientes existentes a través de las plataformas sociales y mostrarles ofertas personalizadas basadas en sus pedidos anteriores. El minorista en línea puede ingerir direcciones de correo electrónico de su propio CRM al CDP en tiempo real de Adobe, generar segmentos a partir de sus propios datos sin conexión y enviar estos segmentos a la plataforma social de Facebook, optimizando así el gasto en publicidad.


### Caso de uso n.º 2


Una aerolínea tiene diferentes niveles de clientes (bronce, plata y oro), y quiere ofrecer a cada uno de los niveles ofertas personalizadas a través de las plataformas sociales. Sin embargo, no todos los clientes utilizan la aplicación móvil de la aerolínea y algunos de ellos no han iniciado sesión en el sitio web de la compañía. Los únicos identificadores que tiene la compañía sobre estos clientes son los ID de pertenencia y las direcciones de correo electrónico.
Para destinatario en los medios sociales, pueden incorporar los datos del cliente desde su CRM al CDP en tiempo real de Adobe, utilizando como identificadores las direcciones de correo electrónico con hash.
A continuación, pueden combinar sus datos sin conexión con los datos de actividad en línea existentes para crear nuevos segmentos de audiencia que pueden destinatario a través del destino de Facebook.

## Especificaciones del destino {#destination-specs}

### Administración de datos para destinos de Facebook {#data-governance}

>[!IMPORTANT]
>
>Los datos enviados a Facebook no deben incluir identidades vinculadas. Usted es responsable de cumplir esta obligación y puede hacerlo asegurándose de que los segmentos seleccionados para la activación no utilicen una opción de vinculación en su política de combinación. Obtenga más información sobre las políticas [de](/help/profile/ui/merge-policies.md)combinación.

### Tipo de Activación {#activation-type}

**Exportación** de segmentos: está exportando todos los miembros de un segmento (audiencia) con los identificadores (nombre, número de teléfono, etc.) se usa en el destino de Facebook.

### Requisitos previos de cuenta de Facebook {#facebook-account-prerequisites}

Antes de enviar los segmentos de audiencia a [!DNL Facebook], asegúrese de cumplir los siguientes requisitos:

1. Su cuenta [!DNL Facebook] de usuario debe tener el **[!DNL Manage campaigns]** permiso habilitado para la cuenta de publicidad que planea usar.
2. Añada la cuenta comercial de **Adobe Experience Cloud** como socio publicitario en su [!DNL Facebook Ad Account]. En su lugar, utilice `business ID=206617933627973`. Consulte [Añadir socios a su administrador](https://www.facebook.com/business/help/1717412048538897) comercial en la documentación de Facebook para obtener más información.
   >[!IMPORTANT]
   > Al configurar los permisos para Adobe Experience Cloud, debe habilitar el permiso **Administrar campañas** . Esto es necesario para la [!DNL Adobe Real-time CDP] integración.
3. Lea y firme las [!DNL Facebook Custom Audiences] Condiciones de servicio. Para hacerlo, vaya a `https://business.facebook.com/ads/manage/customaudiences/tos/?act=[accountID]`, donde `accountID` está su [!DNL Facebook Ad Account ID].

### Requisitos de hash de correo electrónico {#email-hashing-requirements}

Facebook exige que no se envíe información de identificación personal (PII) de manera clara. Por lo tanto, las audiencias activadas en Facebook deben bloquearse las direcciones de correo *hash* . Puede elegir entre hash de las direcciones de correo electrónico antes de ingerirlas en Adobe Experience Platform, o bien puede elegir trabajar con las direcciones de correo electrónico de forma clara en la plataforma de experiencia y hacer que nuestro algoritmo las hash en la activación.

Para obtener más información sobre la ingesta de direcciones de correo electrónico en la plataforma de experiencias, consulte la descripción general [de la ingestión por](/help/ingestion/batch-ingestion/overview.md) lotes y la descripción general [de la ingestión](/help/ingestion/streaming-ingestion/overview.md)por vapor.

Si selecciona hash para las direcciones de correo electrónico usted mismo, asegúrese de cumplir con los siguientes requisitos:

* Recorte todos los espacios al inicio y al final de la cadena de correo electrónico; ejemplo: `johndoe@example.com`, no `<space>johndoe@example.com<space>`;
* Al aplicar hash a las cadenas de correo electrónico, asegúrese de que la cadena está en minúsculas;
   * Ejemplo: `example@email.com`, no `EXAMPLE@EMAIL.COM`;
* Asegúrese de que la cadena con hash esté en minúsculas
   * Ejemplo: `55e79200c1635b37ad31a378c39feb12f120f116625093a19bc32fff15041149`, no `55E79200C1635B37AD31A378C39FEB12F120F116625093A19bC32FFF15041149`;
* No escriba la cadena.


>[!IMPORTANT]
>
>Si decide no usar hash en las direcciones de correo electrónico, Adobe Real-time CDP lo hará por usted cuando active segmentos en Facebook. En el flujo de trabajo [de](/help/rtcdp/destinations/activate-destinations.md#activate-data) activación (consulte el paso 5), seleccione la `Email` opción como se muestra a continuación para las direcciones *de correo electrónico* sin procesar y `Email_LC_SHA256` para las direcciones *de correo electrónico* con hash.


![Hashing en activación](/help/rtcdp/destinations/assets/identity-mapping.png)

## Conectar al destino {#connect-destination}

Para conectarse al destino de Facebook, consulte Flujo de trabajo [de autenticación de destinos de red](/help/rtcdp/destinations/social-network-destinations-workflow.md)social.


## Activar segmentos en Facebook {#activate-segments}

Para obtener instrucciones sobre cómo activar segmentos en Facebook, consulte [Activar datos en destinos](/help/rtcdp/destinations/activate-destinations.md).