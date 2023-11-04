---
title: (Beta) La conexión de Trade Desk con CRM
description: Active los perfiles en su cuenta de Trade Desk para la segmentación y supresión de audiencias en función de los datos de CRM.
last-substantial-update: 2023-01-25T00:00:00Z
exl-id: e09eaede-5525-4a51-a0e6-00ed5fdc662b
source-git-commit: e300e57df998836a8c388511b446e90499185705
workflow-type: tm+mt
source-wordcount: '1148'
ht-degree: 5%

---

# (Beta) El [!DNL Trade Desk] - Conexión CRM

>[!IMPORTANT]
>
>[!DNL The Trade Desk - CRM] El destino en Platform se encuentra actualmente en la versión beta. La documentación y la funcionalidad están sujetas a cambios.
>
>Con el lanzamiento de EUID (European Unified ID), ahora ve dos destinos [!DNL The Trade Desk - CRM] en el [catálogo de destinos](/help/destinations/catalog/overview.md).
>* Si obtiene datos en la UE, utilice el destino **[!DNL The Trade Desk - CRM (EU)]**.
>* Si obtiene datos en las regiones APAC o NAMER, utilice el destino **[!DNL The Trade Desk - CRM (NAMER & APAC)]**.
>
>Ambos destinos en Experience Platform están actualmente en fase beta. Este conector de destino y la página de documentación los crea y mantiene el *[!DNL Trade Desk]* equipo. Para cualquier consulta o solicitud de actualización, póngase en contacto con su [!DNL Trade Desk] , la documentación y las funciones están sujetas a cambios.

## Información general {#overview}

Este documento se ha diseñado para ayudarle a activar perfiles en su [!DNL Trade Desk] cuenta para la segmentación y supresión de audiencias en función de los datos de CRM.

[!DNL The Trade Desk(TTD)] no gestiona directamente el archivo de carga de direcciones de correo electrónico en ningún momento ni [!DNL The Trade Desk] almacene sus correos electrónicos sin procesar (sin hash).

>[!TIP]
>
>Uso [!DNL The Trade Desk] Destinos de CRM para la asignación de datos de CRM, como correo electrónico o dirección de correo electrónico con hash. Utilice el [otro destino de Trade Desk](/help/destinations/catalog/advertising/tradedesk.md) en el catálogo de Adobe Experience Platform para cookies y asignaciones de ID de dispositivo.

## Requisitos previos {#prerequisites}

Antes de activar audiencias en [!DNL The Trade Desk], debe ponerse en contacto con su [!DNL The Trade Desk] administrador de cuentas para firmar el contrato de incorporación a CRM. [!DNL The Trade Desk] concederá permiso y compartirá su ID de anunciante para configurar su destino.

## Requisitos de coincidencia de ID {#id-matching-requirements}

Según el tipo de ID que introduzca en Adobe Experience Platform, debe cumplir con sus requisitos correspondientes. Lea el [Resumen de área de nombres de identidad](/help/identity-service/namespaces.md) para obtener más información.

## Identidades admitidas {#supported-identities}

[!DNL The Trade Desk] admite la activación de identidades descritas en la tabla siguiente. Más información sobre [identidades](/help/identity-service/namespaces.md).

Adobe Experience Platform admite direcciones de correo electrónico con hash SHA256 y de texto sin formato. Siga las instrucciones de la sección Requisitos de coincidencia de ID y utilice los espacios de nombres adecuados para las direcciones de correo electrónico de texto sin formato y con hash, respectivamente.

| Identidad de destino | Descripción | Consideraciones |
|---|---|---|
| Correo electrónico | Direcciones de correo electrónico (texto no cifrado) | Entrada `email` como identidad de destino cuando la identidad de origen es un área de nombres o atributo de correo electrónico. |
| Email_LC_SHA256 | Las direcciones de correo electrónico deben tener un cifrado hash con SHA256 y estar en minúsculas. Asegúrese de seguir cualquiera [normalización de correo electrónico](https://github.com/UnifiedID2/uid2docs/tree/main/api#email-address-normalization) reglas necesarias. No podrá cambiar esta configuración más adelante. | Entrada `hashed_email` como identidad de destino cuando la identidad de origen es un área de nombres o atributo Email_LC_SHA256. |

{style="table-layout:auto"}

## Requisitos de hash de correo electrónico {#hashing-requirements}

Puede hash las direcciones de correo electrónico antes de introducirlas en Adobe Experience Platform o utilizar direcciones de correo electrónico sin procesar.

Para obtener más información sobre la ingesta de direcciones de correo electrónico en Experience Platform, lea la [introducción a la ingesta por lotes](/help/ingestion/batch-ingestion/overview.md).

Si selecciona hash las direcciones de correo electrónico usted mismo, asegúrese de cumplir con los siguientes requisitos:

* Elimine los espacios iniciales y finales.
* Convierta todos los caracteres ASCII a minúsculas.
* Entrada `gmail.com` Las direcciones de correo electrónico de, elimine los siguientes caracteres de la parte de nombre de usuario de la dirección de correo electrónico:
   * El punto (. (Código ASCII 46). Por ejemplo, normalizar `jane.doe@gmail.com` hasta `janedoe@gmail.com`.
   * El signo más (+ (código ASCII 43)) y todos los caracteres posteriores. Por ejemplo, normalizar `janedoe+home@gmail.com` hasta `janedoe@gmail.com`.

## Tipo y frecuencia de exportación {#export-type-frequency}

Consulte la tabla siguiente para obtener información sobre el tipo y la frecuencia de exportación de destino.

| Elemento | Tipo | Notas |
---------|----------|---------|
| Tipo de exportación | **[!UICONTROL Exportación de audiencia]** | Va a exportar todos los miembros de una audiencia con los identificadores (correo electrónico o correo electrónico con hash) utilizados en el destino de la oficina de comercio. |
| Frecuencia de exportación | **[!UICONTROL Lote diario]** | Como el perfil se actualiza en Experience Platform en función de la evaluación de audiencias, el perfil (las identidades) se actualiza una vez al día de forma descendente a la plataforma de destino. Más información sobre [exportaciones por lotes](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## Conexión al destino {#connect}

### Autenticar en Destino {#authenticate}

[!DNL The Trade Desk] El destino de CRM es una carga diaria de archivos por lotes y no requiere autenticación por parte del usuario.

### Rellene los detalles del destino {#fill-in-details}

Para poder enviar o activar datos de audiencia a un destino, debe configurar una conexión con su propia plataforma de destino. While [configuración](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/connect-destination.html) Para este destino, debe proporcionar la siguiente información:

* **[!UICONTROL Tipo de cuenta]**: Elija la **[!UICONTROL Cuenta existente]** opción.
* **[!UICONTROL Nombre]**: Un nombre con el que reconocerá este destino en el futuro.
* **[!UICONTROL Descripción]**: Una descripción que le ayudará a identificar este destino en el futuro.
* **[!UICONTROL ID del anunciante]**: su [!DNL Trade Desk Advertiser ID], que puede compartir su [!DNL Trade Desk] Administrador de cuentas o se encuentra en [!DNL Advertiser Preferences] en el [!DNL Trade Desk] IU.

![Captura de pantalla de la IU de Platform que muestra cómo rellenar los detalles de destino.](/help/destinations/assets/catalog/advertising/tradedesk/configuredestination2.png)

Al conectarse al destino, la configuración de una directiva de control de datos es completamente opcional. Consulte al Experience Platform [información general sobre gobernanza de datos](/help/data-governance/policies/overview.md) para obtener más información.

## Activar públicos en este destino {#activate}

>[!IMPORTANT]
> 
>* Para activar los datos, necesita el **[!UICONTROL Administrar destinos]**, **[!UICONTROL Activar destinos]**, **[!UICONTROL Ver perfiles]**, y **[!UICONTROL Ver segmentos]** [permisos de control de acceso](/help/access-control/home.md#permissions). Lea el [información general de control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.
>* Para exportar *identidades*, necesita el **[!UICONTROL Ver gráfico de identidad]** [permiso de control de acceso](/help/access-control/home.md#permissions). <br> ![Seleccione el área de nombres de identidad resaltada en el flujo de trabajo para activar audiencias en los destinos.](/help/destinations/assets/overview/export-identities-to-destination.png "Seleccione el área de nombres de identidad resaltada en el flujo de trabajo para activar audiencias en los destinos."){width="100" zoomable="yes"}

Leer [activar datos de audiencia en destinos de exportación de perfiles por lotes](/help/destinations/ui/activate-batch-profile-destinations.md) para obtener instrucciones sobre cómo activar audiencias en un destino.

En el **[!UICONTROL Programación]** , puede configurar la programación y los nombres de archivo para cada audiencia que esté exportando. La configuración de la programación es obligatoria, pero la configuración del nombre del archivo es opcional.

![Captura de pantalla de la IU de Platform para programar la activación de audiencias.](/help/destinations/assets/catalog/advertising/tradedesk/schedulesegment1.png)

>[!NOTE]
>
>Todas las audiencias activadas a [!DNL The Trade Desk] Los destinos CRM se establecen automáticamente en una frecuencia diaria y exportación de archivos completa.

![Captura de pantalla de la IU de Platform para programar la activación de audiencias.](/help/destinations/assets/catalog/advertising/tradedesk/schedulesegment2.png)

En el **[!UICONTROL Asignación]** , debe seleccionar atributos o áreas de nombres de identidad de la columna de origen y asignarlos a la columna de destino.

![Captura de pantalla de la IU de Platform para asignar la activación de audiencia.](/help/destinations/assets/catalog/advertising/tradedesk/mappingsegment1.png)

A continuación se muestra un ejemplo de asignación de identidad correcta al activar audiencias en [!DNL The Trade Desk] Destino CRM.

>[!IMPORTANT]
>
> [!DNL The Trade Desk] El destino de CRM no acepta direcciones de correo electrónico sin procesar y con hash como identidades en el mismo flujo de activación. Cree flujos de activación independientes para las direcciones de correo electrónico sin procesar y con hash.

Selección de campos de origen:

* Seleccione el `Email` área de nombres o atributo como identidad de origen si se utiliza la dirección de correo electrónico sin procesar en la ingesta de datos.
* Seleccione el `Email_LC_SHA256` área de nombres o atributo como identidad de origen si ha creado un hash de las direcciones de correo electrónico de los clientes al ingerir datos en Platform.

Selección de campos de destino:

* Entrada  `email` como identidad de destino cuando el área de nombres o atributo de origen es `Email`.
* Entrada  `hashed_email` como identidad de destino cuando el área de nombres o atributo de origen es `Email_LC_SHA256`.

## Validar exportación de datos {#validate}

Para validar que los datos se exportan correctamente desde Experience Platform a [!DNL The Trade Desk], busque las audiencias en el mosaico de datos Adobe 1PD en [!DNL The Trade Desk] Plataforma de administración de datos (DMP). Estos son los pasos para encontrar el ID correspondiente dentro de la variable [!DNL Trade Desk] IU:

1. Primero, haga clic en **[!UICONTROL Datos]** Tabulación y revisión **[!UICONTROL De Origen]**.
2. Desplácese hacia abajo por la página, debajo de **[!UICONTROL Datos importados]**, encontrará la variable **[!UICONTROL Mosaico 1PD de Adobe]**.
3. Haga clic en**[!UICONTROL Adobe 1PD]** mosaico y se enumerarán todas las audiencias activadas en el [!DNL Trade Desk] destino del anunciante. También puede utilizar la función de búsqueda.
4. El ID de segmento # del Experience Platform aparecerá como el Nombre del segmento en la [!DNL Trade Desk] IU.

## Uso de datos y gobernanza {#data-usage-governance}

Todo [!DNL Adobe Experience Platform] Los destinos de cumplen con las políticas de uso de datos al gestionar los datos. Para obtener información detallada sobre cómo [!DNL Adobe Experience Platform] aplica la gobernanza de datos. Consulte la [Resumen de gobernanza de datos](/help/data-governance/home.md).
