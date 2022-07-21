---
title: (Beta) Conexión de asistencia al cliente - CRM
description: Active perfiles en su cuenta de Trade Desk para la segmentación y supresión de audiencias en función de los datos CRM.
source-git-commit: b186a1a4b7417503ffa08a66136411ccff495510
workflow-type: tm+mt
source-wordcount: '1041'
ht-degree: 2%

---


# (Beta) El [!DNL Trade Desk] - Conexión CRM

>[!IMPORTANT]
>
> [!DNL The Trade Desk - CRM] el destino en Platform está actualmente en fase beta. La documentación y la funcionalidad están sujetas a cambios.

## Información general {#overview}

>[!IMPORTANT]
>
> Esta página de documentación la creó el *[!DNL Trade Desk]* equipo. Para cualquier consulta o solicitud de actualización, póngase en contacto con su [!DNL Trade Desk] representante.

Este documento está diseñado para ayudarle a activar perfiles en sus [!DNL Trade Desk] cuenta para la segmentación y supresión de audiencias en función de los datos CRM.

>[!TIP]
>
>Uso [!DNL The Trade Desk] Destino de CRM para asignación de datos CRM, como correo electrónico o dirección de correo electrónico con hash. Utilice la variable [otro destino de mesa de comercio](/help/destinations/catalog/advertising/tradedesk.md) en el catálogo de Adobe Experience Platform para cookies y asignaciones de ID de dispositivo.

[!DNL The Trade Desk] (TTD) no gestiona directamente el archivo de carga de direcciones de correo electrónico en ningún momento ni [!DNL The Trade Desk] almacene los correos electrónicos sin procesar (sin hash).

## Requisitos previos {#prerequisites}

Antes de poder activar segmentos en [!DNL The Trade Desk], debe ponerse en contacto con su [!DNL The Trade Desk] administrador de cuentas para firmar el contrato de incorporación de CRM. [!DNL The Trade Desk] entonces dará permiso y compartirá su ID de anunciante para configurar su destino.

## Requisitos de coincidencia de ID {#id-matching-requirements}

En función del tipo de ID que ingrese en Adobe Experience Platform, debe cumplir sus requisitos correspondientes. Lea el [Información general sobre el área de nombres de identidad](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=es) para obtener más información.

## Identidades compatibles {#supported-identities}

[!DNL The Trade Desk] admite la activación de identidades descritas en la tabla siguiente. Más información sobre [identidades](/help/identity-service/namespaces.md).

Adobe Experience Platform admite las direcciones de correo electrónico con texto sin formato y con hash SHA 256. Siga las instrucciones de la sección de requisitos de coincidencia de ID y utilice las áreas de nombres adecuadas para el texto sin formato y las direcciones de correo electrónico con hash, respectivamente.

| Identidad de Target | Descripción | Consideraciones |
|---|---|---|
| Correo electrónico | Direcciones de correo electrónico (texto sin formato) | Seleccione el `Email` identidad de destino cuando la identidad de origen es un espacio de nombres o atributo de correo electrónico. |
| Email_LC_SHA256 | Las direcciones de correo electrónico deben tener un cifrado hash con SHA256 y minúsculas. Asegúrese de seguir cualquier [normalización de correo electrónico](https://github.com/UnifiedID2/uid2docs/tree/main/api#email-address-normalization) reglas requeridas. No podrá cambiar esta configuración más adelante. | Seleccione el `Email_LC_SHA256` identidad de destino cuando la identidad de origen es un espacio de nombres o atributo Email_LC_SHA256. |

{style=&quot;table-layout:auto&quot;}

## Requisitos de hash de correo electrónico {#hashing-requirements}

Puede hash las direcciones de correo electrónico antes de ingerirlas en Adobe Experience Platform o utilizar direcciones de correo electrónico sin procesar.

Para obtener más información sobre la ingesta de direcciones de correo electrónico en Experience Platform, consulte la [información general sobre la ingesta de lotes](https://experienceleague.adobe.com/docs/experience-platform/ingestion/batch/overview.html?lang=en).

Si selecciona hash para las direcciones de correo electrónico usted mismo, asegúrese de cumplir con los siguientes requisitos:

* Elimine los espacios al inicio y al final.
* Convertir todos los caracteres ASCII a minúsculas.
* En `gmail.com` direcciones de correo electrónico, elimine los siguientes caracteres de la parte del nombre de usuario de la dirección de correo electrónico:
   * El periodo (. (Código ASCII 46). Por ejemplo, normalizar `jane.doe@gmail.com` a `janedoe@gmail.com`.
   * El signo más (+ (código ASCII 43)) y todos los caracteres subsiguientes. Por ejemplo, normalizar `janedoe+home@gmail.com` a `janedoe@gmail.com`.

## Tipo de exportación y frecuencia {#export-type-frequency}

Consulte la tabla siguiente para obtener información sobre el tipo y la frecuencia de exportación de destino.

| Elemento | Tipo | Notas |
---------|----------|---------|
| Tipo de exportación | **[!UICONTROL Exportación de segmentos]** | Está exportando todos los miembros de un segmento (audiencia) con los identificadores (correo electrónico o correo electrónico con hash) utilizados en el destino del mostrador de comercio. |
| Frecuencia de exportación | **[!UICONTROL Lote diario]** | Como un perfil se actualiza en el Experience Platform en función de la evaluación de segmentos, el perfil (identidades) se actualiza una vez al día para llegar a la plataforma de destino. Más información sobre [cargas por lotes](https://experienceleague.adobe.com/docs/experience-platform/destinations/destination-types.html?lang=en#file-based). |

{style=&quot;table-layout:auto&quot;}

## Conectarse al destino {#connect}

### Autenticar en destino {#authenticate}

[!DNL The Trade Desk] El destino CRM es una carga diaria de archivos por lotes y no requiere autenticación del usuario.

### Rellenar detalles de destino {#fill-in-details}

Para poder enviar o activar datos de audiencia en un destino, debe configurar una conexión con su propia plataforma de destino. While [configuración](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/connect-destination.html?lang=en) Para este destino, debe proporcionar la siguiente información:

* **[!UICONTROL Tipo de cuenta]**: Elija el **[!UICONTROL Cuenta existente]** .
* **[!UICONTROL Nombre]**: Un nombre por el cual reconocerá este destino en el futuro.
* **[!UICONTROL Descripción]**: Descripción que le ayudará a identificar este destino en el futuro.
* **[!UICONTROL ID del anunciante]**: your [!DNL Trade Desk Advertiser ID], que puede compartir su [!DNL Trade Desk] Administrador de cuentas o en [!DNL Advertiser Preferences] en el [!DNL Trade Desk] IU.

Al conectarse al destino, la configuración de una directiva de control de datos es completamente opcional. Consulte al Experience Platform [información general sobre la administración de datos](https://experienceleague.adobe.com/docs/experience-platform/data-governance/policies/overview.html?lang=en) para obtener más información.

## Activar segmentos en este destino {#activate}

Consulte [activar datos de audiencia en destinos de exportación de perfiles por lotes](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-batch-profile-destinations.html?lang=en) para obtener instrucciones sobre cómo activar segmentos de audiencia en un destino.

En el **[!UICONTROL Programación]** , puede configurar la programación y los nombres de archivo para cada segmento que exporte. La configuración de la programación es obligatoria, pero la configuración del nombre del archivo es opcional.

>[!NOTE]
>
>Todos los segmentos activados en [!DNL The Trade Desk] El destino CRM se establece automáticamente en una frecuencia diaria y en una exportación completa de archivos.

En el **[!UICONTROL Asignación]** , debe seleccionar atributos o áreas de nombres de identidad de la columna de origen y asignarlos a la columna de destino.

A continuación se muestra un ejemplo de asignación de identidad correcta al activar segmentos en [!DNL The Trade Desk] Destino de CRM.

>[!IMPORTANT]
>
> [!DNL The Trade Desk] El destino CRM no acepta direcciones de correo electrónico sin procesar y con hash como identidades en el mismo flujo de activación. Cree flujos de activación independientes para las direcciones de correo electrónico sin procesar y con hash.

Selección de campos de origen:

* Seleccione el `Email` área de nombres o atributo como identidad de origen si se utiliza la dirección de correo electrónico sin procesar en la ingesta de datos.
* Seleccione el `Email_LC_SHA256` espacio de nombres o atributo como identidad de origen si ha pasado por hash las direcciones de correo electrónico de los clientes en la ingesta de datos en Platform.

Selección de campos de destino:

* Seleccione el `Email` área de nombres como identidad de destino cuando su espacio de nombres o atributo de origen es `Email`.
* Seleccione el `Email_LC_SHA256` área de nombres como identidad de destino cuando su espacio de nombres o atributo de origen es `Email_LC_SHA256`.

## Validar exportación de datos {#validate}

Para validar que los datos se exportan correctamente fuera del Experience Platform y en [!DNL The Trade Desk], busque los segmentos en el mosaico de datos de Adobe 1PD dentro de [!DNL The Trade Desk] Plataforma de gestión de datos (DMP). Estos son los pasos para encontrar el ID correspondiente dentro de la variable [!DNL Trade Desk] IU:

1. En primer lugar, haga clic en el **[!UICONTROL Datos]** Tabulación y revisión **[!UICONTROL Datos de origen]**.
2. Desplácese hacia abajo por la página, debajo de **[!UICONTROL Datos importados]**, encontrará la variable **[!UICONTROL Mosaico 1PD Adobe]**.
3. Haga clic en el[!UICONTROL Adobe 1PD]** y en él se enumerarán todos los segmentos activados en la variable [!DNL Trade Desk] destino del anunciante. También puede utilizar la función de búsqueda.
4. El número de ID de segmento del Experience Platform aparecerá como Nombre del segmento en la variable [!DNL Trade Desk] IU.

## Uso y gobernanza de los datos {#data-usage-governance}

Todo [!DNL Adobe Experience Platform] Los destinos de cumplen las políticas de uso de datos al administrar los datos. Para obtener información detallada sobre cómo [!DNL Adobe Experience Platform] exige el control de datos; consulte [Información general sobre la administración de datos](/help/data-governance/home.md).
