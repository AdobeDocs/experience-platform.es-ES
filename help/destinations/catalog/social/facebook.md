---
keywords: conexión de Facebook;conexión de Facebook;destinos de Facebook;facebook;instagram;mensajero;mensajero de facebook;mensajero de facebook
title: Conexión de Facebook
description: Active perfiles para sus campañas de Facebook para objetivos de audiencia, personalización y supresión basados en correos electrónicos con hash.
translation-type: tm+mt
source-git-commit: 8b7befd9775654a2d55d28a64b4b104e7f9576aa
workflow-type: tm+mt
source-wordcount: '1001'
ht-degree: 3%

---


# [!DNL Facebook] connection

>[!IMPORTANT]
>
>Actualmente estamos migrando clientes a la nueva versión de este destino, [!DNL Facebook Custom Audience].
>
> Las instrucciones de este artículo se aplican a ambas versiones, con la siguiente nota: mientras esta migración está en curso, solo verá la versión actual del destino [!DNL Facebook] en la interfaz de usuario, donde solo puede utilizar las identidades [!UICONTROL EMAIL] y [!UICONTROL EMAIL_LC_SHA_256] para la activación.

Active perfiles para sus [!DNL Facebook] campañas de objetivo de audiencia, personalización y supresión en base a correos electrónicos con hash.

Puede usar este destino para objetivos de audiencia en toda la familia [!DNL Facebook’s] de aplicaciones admitidas por [!DNL Custom Audiences], incluso [!DNL Facebook], [!DNL Instagram], [!DNL Audience Network] y [!DNL Messenger]. La selección de la aplicación con la que quiere ejecutar la campaña se indica en el nivel de colocación de [!DNL Facebook Ads Manager].

![Destino de Facebook en la interfaz de usuario de Adobe Experience Platform](../../assets/catalog/social/facebook/catalog.png)

## Casos de uso

Para ayudarle a comprender mejor cómo y cuándo debe utilizar el destino [!DNL Facebook], aquí hay dos casos de uso de muestra que los clientes de Adobe Experience Platform pueden resolver con esta función.

### Caso de uso n.º 1

Un minorista en línea quiere llegar a los clientes existentes a través de las plataformas sociales y mostrarles ofertas personalizadas basadas en sus pedidos anteriores. El minorista en línea puede ingerir direcciones de correo electrónico de su propia CRM a Adobe Experience Platform, generar segmentos a partir de sus propios datos sin conexión y enviar estos segmentos a la plataforma social [!DNL Facebook], optimizando así su inversión en publicidad.

### Caso de uso n.º 2

Una aerolínea tiene diferentes niveles de clientes (bronce, plata y oro), y quiere ofrecer a cada uno de los niveles ofertas personalizadas a través de las plataformas sociales. Sin embargo, no todos los clientes utilizan la aplicación móvil de la aerolínea y algunos de ellos no han iniciado sesión en el sitio web de la compañía. Los únicos identificadores que tiene la compañía sobre estos clientes son los ID de pertenencia y las direcciones de correo electrónico.

Para destinatario en los medios sociales, pueden incorporar los datos de cliente desde su CRM a Adobe Experience Platform, utilizando las direcciones de correo electrónico como identificadores.

A continuación, pueden utilizar sus datos sin conexión, incluidos los ID de pertenencia asociados y los niveles de cliente, para crear nuevos segmentos de audiencia que pueden generar destinatarios a través del [!DNL Facebook] destino.

## Detalles de destino {#destination-specs}

### Administración de datos para destinos [!DNL Facebook] {#data-governance}

>[!IMPORTANT]
>
>Los datos enviados a [!DNL Facebook] no deben incluir identidades vinculadas. Usted es responsable de cumplir esta obligación y puede hacerlo asegurándose de que los segmentos seleccionados para la activación no utilicen una opción de vinculación en su política de combinación. Obtenga más información sobre [políticas de combinación](/help/profile/ui/merge-policies.md).

### Tipo de exportación {#export-type}

**Exportación**  de segmentos: está exportando todos los miembros de un segmento (audiencia) con los identificadores (nombre, número de teléfono, etc.) se usa en el destino de Facebook.

### Requisitos previos de cuenta de Facebook {#facebook-account-prerequisites}

Antes de enviar los segmentos de audiencia a [!DNL Facebook], asegúrese de cumplir los siguientes requisitos:

- Su cuenta de [!DNL Facebook] usuario debe tener el permiso **[!DNL Manage campaigns]** habilitado para la cuenta de publicidad que planea utilizar.
- La cuenta de negocios **Adobe Experience Cloud** debe agregarse como socio publicitario en su [!DNL Facebook Ad Account]. En su lugar, utilice `business ID=206617933627973`. Consulte [Añadir socios a su administrador comercial](https://www.facebook.com/business/help/1717412048538897) en la documentación de Facebook para obtener más información.
   >[!IMPORTANT]
   >
   > Al configurar los permisos para Adobe Experience Cloud, debe habilitar el permiso **Administrar campañas**. Es necesario para la integración de [!DNL Adobe Experience Platform].
- Lea y firme las [!DNL Facebook Custom Audiences] Condiciones de servicio. Para ello, vaya a `https://business.facebook.com/ads/manage/customaudiences/tos/?act=[accountID]`, donde `accountID` es su [!DNL Facebook Ad Account ID].

### Requisitos de coincidencia de ID {#id-matching-requirements}

[!DNL Facebook] exige que no se envíe con claridad ninguna información de identificación personal. Por lo tanto, las audiencias activadas en [!DNL Facebook] se pueden desactivar *identificadores con hash*, como direcciones de correo electrónico o números de teléfono.

Según el tipo de ID que ingrese en Adobe Experience Platform, debe cumplir los requisitos correspondientes.

#### Requisitos de hash de número telefónico {#phone-number-hashing-requirements}

Existen dos métodos para activar los números de teléfono en [!DNL Facebook]:

- **Ingesta de números** de teléfono sin procesar: puede ingerir números de teléfono sin procesar en el  [!DNL E.164] formato  [!DNL Platform], que se etiquetarán automáticamente al efectuar la activación. Si elige esta opción, asegúrese de ingerir siempre los números de teléfono sin procesar en la Área de nombres `Phone_E.164`.
- **Ingesta de números** de teléfono con hash: puede prehash sus números de teléfono antes de ingerirlos a  [!DNL Platform]. Si elige esta opción, asegúrese de ingerir siempre los números de teléfono con hash en la Área de nombres `Phone_SHA256`.

>[!NOTE]
>
>Los números de teléfono ingestados en la Área de nombres `Phone` no se pueden activar en [!DNL Facebook].


#### Requisitos de hash de correo electrónico {#email-hashing-requirements}

Puede elegir hash las direcciones de correo electrónico antes de ingerirlas en Adobe Experience Platform, o puede elegir trabajar con las direcciones de correo electrónico de forma clara en Experience Platform y hacer que nuestro algoritmo las incluya en activación.

Para obtener más información sobre la ingesta de direcciones de correo electrónico en Experience Platform, consulte la [información general sobre la ingestión por lotes](/help/ingestion/batch-ingestion/overview.md) y la [información general sobre la ingestión por vapor](/help/ingestion/streaming-ingestion/overview.md).

Si selecciona hash para las direcciones de correo electrónico usted mismo, asegúrese de cumplir con los siguientes requisitos:

- Recorte todos los espacios al inicio y al final de la cadena de correo electrónico; ejemplo: `johndoe@example.com`, no `<space>johndoe@example.com<space>`;
- Al aplicar hash a las cadenas de correo electrónico, asegúrese de que la cadena está en minúsculas;
   - Ejemplo: `example@email.com`, no `EXAMPLE@EMAIL.COM`;
- Asegúrese de que la cadena con hash esté en minúsculas
   - Ejemplo: `55e79200c1635b37ad31a378c39feb12f120f116625093a19bc32fff15041149`, no `55E79200C1635B37AD31A378C39FEB12F120F116625093A19bC32FFF15041149`;
- No escriba la cadena.

>[!NOTE]
>
>Los datos de las Áreas de nombres sin hash se hash automáticamente mediante [!DNL Platform] en el momento de la activación.
> Los datos de origen de atributos no se hash automáticamente. Cuando el campo de origen contenga atributos sin hash, marque la opción **[!UICONTROL Aplicar transformación]** para que [!DNL Platform] hash automáticamente los datos en la activación.
> La opción **[!UICONTROL Aplicar transformación]** solo se muestra cuando se seleccionan atributos como campos de origen. No se muestra al elegir Áreas de nombres.

![Transformación de asignación de identidades](../../assets/ui/activate-destinations/identity-mapping-transformation.png)

#### Uso de Áreas de nombres personalizadas {#custom-namespaces}

Antes de poder utilizar la Área de nombres `Extern_ID` para enviar datos a [!DNL Facebook], asegúrese de sincronizar sus propios identificadores con [!DNL Facebook Pixel]. Consulte la [documentación oficial](https://developers.facebook.com/docs/marketing-api/audiences/guides/custom-audiences/#external_identifiers) para obtener información detallada.

## Conectar al destino {#connect-destination}

Para conectarse al destino [!DNL Facebook], consulte [Flujo de trabajo de autenticación de destinos de red social](./workflow.md).

## Activar segmentos a [!DNL Facebook] {#activate-segments}

Para obtener instrucciones sobre cómo activar segmentos en [!DNL Facebook], consulte [Activar datos en destinos](../../ui/activate-destinations.md).

En el paso **[!UICONTROL Programación de segmentos]**, debe proporcionar el [!UICONTROL Origen de audiencia] al enviar segmentos a [!DNL Facebook Custom Audiences].

![Origen de Audiencia de Facebook](../../assets/catalog/social/facebook/facebook-origin-audience.png)

## Datos exportados {#exported-data}

Para [!DNL Facebook], una activación exitosa significa que se creará una audiencia personalizada [!DNL Facebook] mediante programación en [[!DNL Facebook Ads Manager]](https://www.facebook.com/adsmanager/manage/). La pertenencia a segmentos en la audiencia se agregaría y eliminaría a medida que los usuarios estuvieran cualificados o descalificados para los segmentos activados.

>[!TIP]
>
>La integración entre Adobe Experience Platform y [!DNL Facebook] admite los rellenos de audiencia históricos. Todas las cualificaciones del segmento histórico se envían a [!DNL Facebook] al activar los segmentos en el destino.