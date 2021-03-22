---
keywords: conexión linkedin;conexión linkedin;destinos linkedin;linkedin;
title: Conexión de audiencias coincidentes de Linkedin
description: Active perfiles para sus campañas de LinkedIn para segmentación, personalización y supresión de audiencias, en función de correos electrónicos con hash.
translation-type: tm+mt
source-git-commit: 7d579d85d427c45f39d000288ed883c7ffd003bf
workflow-type: tm+mt
source-wordcount: '654'
ht-degree: 0%

---


# [!DNL LinkedIn Matched Audiences] connection

Active perfiles para sus campañas [!DNL LinkedIn] para segmentación, personalización y supresión de audiencias, en función de correos electrónicos con hash e ID móviles.

![Destino de LinkedIn en la interfaz de usuario de Adobe Experience Platform](../../assets/catalog/social/linkedin/catalog.png)

## Casos de uso

Para ayudarle a comprender mejor cómo y cuándo utilizar el destino [!DNL LinkedIn Matched Audiences], este es un caso de uso que los clientes de Adobe Experience Platform pueden resolver utilizando esta función.

Una empresa de software organiza una conferencia y quiere mantenerse en contacto con los participantes, y mostrarles ofertas personalizadas basadas en su estado de asistencia a la conferencia. La empresa puede ingerir direcciones de correo electrónico o ID de dispositivos móviles desde su propio [!DNL CRM] en Adobe Experience Platform. A continuación, pueden generar segmentos a partir de sus propios datos sin conexión y enviarlos a la plataforma social [!DNL LinkedIn], lo que optimiza su gasto en publicidad.

## Identidades admitidas {#supported-identities}

[!DNL LinkedIn Matched Audiences] admite la activación de identidades descritas en la tabla siguiente. Obtenga más información sobre [identities](/help/identity-service/namespaces.md).

| Identidad de Target | Descripción | Consideraciones |
|---|---|---|
| GAID | Google Advertising ID | Seleccione esta identidad de destino cuando la identidad de origen sea un área de nombres GAID. |
| IDFA | Apple ID para anunciantes | Seleccione esta identidad de destino cuando la identidad de origen sea un área de nombres IDFA. |
| email_lc_sha256 | Direcciones de correo electrónico con hash con el algoritmo SHA256 | Adobe Experience Platform admite las direcciones de correo electrónico con texto sin formato y con hash SHA 256. Siga las instrucciones de la sección [Requisitos de coincidencia de ID](#id-matching-requirements-id-matching-requirements) y utilice los espacios de nombres adecuados para los correos electrónicos de texto sin formato y con hash, respectivamente. Cuando el campo de origen contenga atributos sin hash, marque la opción **[!UICONTROL Apply transformation]** para que [!DNL Platform] hash automáticamente los datos al activarlos. |


## Tipo de exportación {#export-type}

**Exportación de segmentos** : está exportando todos los miembros de un segmento (audiencia) con los identificadores (nombre, número de teléfono y otros) utilizados en el  [!DNL LinkedIn Matched Audiences] destino.

## Requisitos previos de cuenta de LinkedIn {#LinkedIn-account-prerequisites}

Antes de usar el destino [!UICONTROL LinkedIn Matched Audience] , asegúrese de que su cuenta [!DNL LinkedIn Campaign Manager] tenga el nivel de permiso [!DNL Creative Manager] o superior.

Para obtener información sobre cómo editar los permisos de usuario de [!DNL LinkedIn Campaign Manager], consulte [Agregar, editar y eliminar permisos de usuario en cuentas publicitarias](https://www.linkedin.com/help/lms/answer/5753) en la documentación de LinkedIn.

## Requisitos de coincidencia de ID {#id-matching-requirements}

[!DNL LinkedIn Matched Audiences] exige que no se envíe con claridad ninguna información de identificación personal (PII). Por lo tanto, las audiencias activadas en [!DNL LinkedIn Matched Audiences] pueden desactivarse mediante identificadores *hash*, como direcciones de correo electrónico o ID de dispositivos móviles.

En función del tipo de ID que ingrese en Adobe Experience Platform, debe cumplir sus requisitos correspondientes.

## Requisitos de hash de correo electrónico {#email-hashing-requirements}

Puede hash sobre las direcciones de correo electrónico antes de ingerirlas en Adobe Experience Platform, o usar las direcciones de correo electrónico claramente en el Experience Platform, y tener [!DNL Platform] hash sobre ellas cuando se activen.

Para obtener más información sobre la ingesta de direcciones de correo electrónico en Experience Platform, consulte la [información general sobre la ingesta por lotes](/help/ingestion/batch-ingestion/overview.md) y la [información general sobre la ingesta de flujo](/help/ingestion/streaming-ingestion/overview.md).

Si selecciona hash para las direcciones de correo electrónico usted mismo, asegúrese de cumplir con los siguientes requisitos:

- Recorte todos los espacios al principio y al final de la cadena de correo electrónico. Por ejemplo: `johndoe@example.com`, no `<space>johndoe@example.com<space>`;
- Al hash de las cadenas de correo electrónico, asegúrese de usar un hash para la cadena en minúsculas;
   - Ejemplo: `example@email.com`, no `EXAMPLE@EMAIL.COM`;
- Asegúrese de que la cadena con hash esté en minúscula
   - Ejemplo: `55e79200c1635b37ad31a378c39feb12f120f116625093a19bc32fff15041149`, no `55E79200C1635B37AD31A378C39FEB12F120F116625093A19bC32FFF15041149`;
- No sal la cadena.

>[!NOTE]
>
>Los datos de espacios de nombres sin hash se colocan automáticamente en hash mediante [!DNL Platform] al activarlos.
> Los datos de origen de atributos no se colocan automáticamente en hash.
> 
> Durante el paso [Asignación de identidad](../../ui/activate-destinations.md#identity-mapping), cuando el campo de origen contiene atributos sin hash, marque la opción **[!UICONTROL Apply transformation]** para que [!DNL Platform] hash automáticamente los datos al activarlos.
> 
> La opción **[!UICONTROL Apply transformation]** solo se muestra al seleccionar atributos como campos de origen. No se muestra al elegir espacios de nombres.

![Transformación de asignación de identidad](../../assets/ui/activate-destinations/identity-mapping-transformation.png)

## Conectarse al destino {#connect-destination}

Para conectarse al destino [!DNL LinkedIn Matched Audiences], consulte [Flujo de trabajo de autenticación de destinos de red social](./workflow.md).

## Activar segmentos en [!DNL LinkedIn Matched Audiences] {#activate-segments}

Para obtener instrucciones sobre cómo activar segmentos en [!DNL LinkedIn Matched Audiences], consulte [Activar datos en destinos](../../ui/activate-destinations.md).

## Datos exportados {#exported-data}

Una activación correcta significa que se crearía una audiencia [!DNL LinkedIn] personalizada mediante programación en [[!DNL LinkedIn Campaign Manager]](https://www.linkedin.com/campaignmanager/login). La pertenencia a segmentos en la audiencia se agregaría y eliminaría ya que los usuarios están cualificados o no cumplen los requisitos para los segmentos activados.

>[!TIP]
>
>La integración entre Adobe Experience Platform y [!DNL LinkedIn Matched Audiences] admite los rellenos históricos de audiencias. Todas las cualificaciones históricas de segmentos se envían a [!DNL LinkedIn] al activar los segmentos en el destino.