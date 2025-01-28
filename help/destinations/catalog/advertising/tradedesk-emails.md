---
title: La conexión de Trade Desk con CRM
description: Active los perfiles en su cuenta de Trade Desk para la segmentación y supresión de audiencias en función de los datos de CRM.
last-substantial-update: 2025-01-16T00:00:00Z
exl-id: e09eaede-5525-4a51-a0e6-00ed5fdc662b
source-git-commit: a189a86749996c0ee7b6146bcd030d8495745e12
workflow-type: tm+mt
source-wordcount: '1117'
ht-degree: 5%

---

# La conexión [!DNL Trade Desk] - CRM

>[!IMPORTANT]
>
>Con el lanzamiento de EUID (European Unified ID), ahora ve dos destinos [!DNL The Trade Desk - CRM] en el [catálogo de destinos](/help/destinations/catalog/overview.md).
>* Si obtiene datos en la UE, utilice el destino **[!DNL The Trade Desk - CRM (EU)]**.
>* Si obtiene datos en las regiones APAC o NAMER, utilice el destino **[!DNL The Trade Desk - CRM (NAMER & APAC)]**.
>
>El equipo *[!DNL Trade Desk]* crea y mantiene este conector de destino y esta página de documentación. Para cualquier consulta o solicitud de actualización, comuníquese con su representante de [!DNL Trade Desk].

## Información general {#overview}

Descubra cómo puede activar perfiles en su cuenta de [!DNL Trade Desk] para la segmentación y supresión de audiencias en función de los datos de CRM.

Este conector envía datos al extremo de origen [!DNL The Trade Desk]. La integración entre Adobe Experience Platform y [!DNL The Trade Desk] no permite exportar datos al extremo de terceros [!DNL The Trade Desk].

[!DNL The Trade Desk(TTD)] no gestiona directamente el archivo de carga de direcciones de correo electrónico en ningún momento, ni [!DNL The Trade Desk] almacena sus correos electrónicos sin procesar (sin hash).

>[!TIP]
>
>Usar [!DNL The Trade Desk] destinos CRM para la asignación de datos de CRM, como correo electrónico o dirección de correo electrónico con hash. Use [otro destino de Trade Desk](/help/destinations/catalog/advertising/tradedesk.md) en el catálogo de Adobe Experience Platform para las cookies y las asignaciones de ID de dispositivo.

## Requisitos previos {#prerequisites}

>[!IMPORTANT]
>
>Antes de activar audiencias en The Trade Desk, debe ponerse en contacto con su administrador de cuentas de [!DNL Trade Desk] para firmar el contrato de incorporación a CRM. [!DNL The Trade Desk] habilitará el uso de UID2/EUID y compartirá otros detalles para ayudarle a configurar su destino.

## Requisitos de coincidencia de ID {#id-matching-requirements}

Según el tipo de ID que introduzca en Adobe Experience Platform, debe cumplir con sus requisitos correspondientes. Lea la [descripción general del área de nombres de identidad](/help/identity-service/features/namespaces.md) para obtener más información.

## Identidades admitidas {#supported-identities}

[!DNL The Trade Desk] admite la activación de las identidades descritas en la tabla siguiente. Más información sobre [identidades](/help/identity-service/features/namespaces.md).

Adobe Experience Platform admite direcciones de correo electrónico con hash SHA256 y de texto sin formato. Siga las instrucciones de la sección Requisitos de coincidencia de ID y utilice los espacios de nombres adecuados para las direcciones de correo electrónico de texto sin formato y con hash, respectivamente.

| Identidad de destino | Descripción | Consideraciones |
|---|---|---|
| Correo electrónico | Direcciones de correo electrónico (texto no cifrado) | Escriba `email` como identidad de destino cuando la identidad de origen sea un área de nombres o atributo de correo electrónico. |
| Email_LC_SHA256 | Las direcciones de correo electrónico deben tener un cifrado hash con SHA256 y estar en minúsculas. No podrá cambiar esta configuración más adelante. | Escriba `hashed_email` como identidad de destino cuando la identidad de origen sea un espacio de nombres o atributo Email_LC_SHA256. |

{style="table-layout:auto"}

## Requisitos de hash de correo electrónico {#hashing-requirements}

Puede hash las direcciones de correo electrónico antes de introducirlas en Adobe Experience Platform o utilizar direcciones de correo electrónico sin procesar.

Para obtener más información sobre la ingesta de direcciones de correo electrónico en Experience Platform, lea la [descripción general de la ingesta por lotes](/help/ingestion/batch-ingestion/overview.md).

Si selecciona hash las direcciones de correo electrónico usted mismo, asegúrese de cumplir con los siguientes requisitos:

* Elimine los espacios iniciales y finales.
* Convierta todos los caracteres ASCII a minúsculas.
* En `gmail.com` direcciones de correo electrónico, elimine los siguientes caracteres de la parte de nombre de usuario de la dirección de correo electrónico:
   * El punto (. (Código ASCII 46). Por ejemplo, normalice `jane.doe@gmail.com` a `janedoe@gmail.com`.
   * El signo más (+ (código ASCII 43)) y todos los caracteres posteriores. Por ejemplo, normalice `janedoe+home@gmail.com` a `janedoe@gmail.com`.

## Tipo y frecuencia de exportación {#export-type-frequency}

Consulte la tabla siguiente para obtener información sobre el tipo y la frecuencia de exportación de destino.

| Elemento | Tipo | Notas |
---------|----------|---------|
| Tipo de exportación | **[!UICONTROL Exportación de audiencia]** | Va a exportar todos los miembros de una audiencia con los identificadores (correo electrónico o correo electrónico con hash) utilizados en el destino de la oficina de comercio. |
| Frecuencia de exportación | **[!UICONTROL Lote diario]** | Como el perfil se actualiza en Experience Platform en función de la evaluación de audiencias, el perfil (las identidades) se actualiza una vez al día de forma descendente a la plataforma de destino. Más información sobre [exportaciones por lotes](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## Conexión al destino {#connect}

### Autenticar en Destino {#authenticate}

[!DNL The Trade Desk] El destino de CRM es una carga de archivo por lotes diaria y no requiere autenticación por parte del usuario.

### Rellene los detalles del destino {#fill-in-details}

Para poder enviar o activar datos de audiencia a un destino, debe configurar una conexión con su propia plataforma de destino. Mientras [configura](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/connect-destination.html) este destino, debe proporcionar la siguiente información:

* **[!UICONTROL Tipo de cuenta]**: Elija la opción **[!UICONTROL Cuenta existente]**.
* **[!UICONTROL Nombre]**: Un nombre por el cual reconocerá este destino en el futuro.
* **[!UICONTROL Descripción]**: Una descripción que le ayudará a identificar este destino en el futuro.
* **[!UICONTROL ID del anunciante]**: tu [!DNL Trade Desk Advertiser ID], que puede compartir el administrador de cuentas de [!DNL Trade Desk] o que se encuentra en [!DNL Advertiser Preferences] en la interfaz de usuario de [!DNL Trade Desk].

![Captura de pantalla de la interfaz de usuario de Platform que muestra cómo rellenar los detalles de destino.](/help/destinations/assets/catalog/advertising/tradedesk/configuredestination2.png)

Al conectarse al destino, la configuración de una directiva de control de datos es completamente opcional. Consulte la [descripción general del control de datos](/help/data-governance/policies/overview.md) del Experience Platform para obtener más detalles.

## Activar públicos en este destino {#activate}

>[!IMPORTANT]
> 
>* Para activar los datos, necesita los **[!UICONTROL permisos de control de acceso]**, **[!UICONTROL Activar destinos]**, **[!UICONTROL Ver perfiles]** y **[!UICONTROL Ver segmentos]**[para ](/help/access-control/home.md#permissions). Lea la [descripción general del control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.
>* Para exportar *identidades*, necesita el **[!UICONTROL permiso de control de acceso](/help/access-control/home.md#permissions) de]** Ver gráfico de identidad[. <br> ![Seleccione el área de nombres de identidad resaltada en el flujo de trabajo para activar audiencias en los destinos.](/help/destinations/assets/overview/export-identities-to-destination.png "Seleccione el área de nombres de identidad resaltada en el flujo de trabajo para activar audiencias en los destinos."){width="100" zoomable="yes"}

Lea [activar datos de audiencia en destinos de exportación de perfiles por lotes](/help/destinations/ui/activate-batch-profile-destinations.md) para obtener instrucciones sobre cómo activar audiencias en un destino.

En la página **[!UICONTROL Programación]**, puede configurar la programación y los nombres de archivo para cada audiencia que esté exportando. La configuración de la programación es obligatoria, pero la configuración del nombre del archivo es opcional.

![Captura de pantalla de la IU de Platform para programar la activación de audiencias.](/help/destinations/assets/catalog/advertising/tradedesk/schedulesegment1.png)

>[!NOTE]
>
>Todas las audiencias activadas en [!DNL The Trade Desk] destino de CRM se establecen automáticamente en una frecuencia diaria y exportación de archivos completa.

![Captura de pantalla de la IU de Platform para programar la activación de audiencias.](/help/destinations/assets/catalog/advertising/tradedesk/schedulesegment2.png)

En la página **[!UICONTROL Mapping]**, debe seleccionar atributos o áreas de nombres de identidad de la columna de origen y asignarlos a la columna de destino.

![Captura de pantalla de la IU de Platform para asignar la activación de audiencia.](/help/destinations/assets/catalog/advertising/tradedesk/mappingsegment1.png)

A continuación se muestra un ejemplo de asignación de identidad correcta al activar audiencias en [!DNL The Trade Desk] destino de CRM.

>[!IMPORTANT]
>
> [!DNL The Trade Desk] El destino de CRM no acepta direcciones de correo electrónico sin procesar y con hash como identidades en el mismo flujo de activación. Cree flujos de activación independientes para las direcciones de correo electrónico sin procesar y con hash.

Selección de campos de origen:

* Seleccione el área de nombres o atributo `Email` como identidad de origen si utiliza la dirección de correo electrónico sin procesar al ingerir datos.
* Seleccione el área de nombres o el atributo `Email_LC_SHA256` como identidad de origen si ha creado un hash de las direcciones de correo electrónico de los clientes al ingerir datos en Platform.

Selección de campos de destino:

* Escriba `email` como identidad de destino cuando el área de nombres o atributo de origen sea `Email`.
* Escriba `hashed_email` como identidad de destino cuando el área de nombres o atributo de origen sea `Email_LC_SHA256`.

## Validar exportación de datos {#validate}

Para validar que los datos se exportan correctamente fuera del Experience Platform y en [!DNL The Trade Desk], busque las audiencias en el mosaico de datos de Adobe 1PD en [!DNL The Trade Desk] Data Management Platform (DMP). Estos son los pasos para encontrar el ID correspondiente en la interfaz de usuario de [!DNL Trade Desk]:

1. En primer lugar, seleccione la ficha **[!UICONTROL Datos]** y revise la sección **[!UICONTROL Datos de origen]**.
2. Desplácese hacia abajo en la página, en **[!UICONTROL Datos importados]**, encontrará el **[!UICONTROL Mosaico 1PD de Adobe]**.
3. Haga clic en el mosaico**[!UICONTROL Adobe 1PD]** y se enumerarán todas las audiencias activadas en el destino [!DNL Trade Desk] para su anunciante. También puede utilizar la función de búsqueda.
4. El ID de segmento # del Experience Platform aparecerá como el Nombre del segmento en la interfaz de usuario de [!DNL Trade Desk].

## Uso de datos y gobernanza {#data-usage-governance}

Todos los destinos de [!DNL Adobe Experience Platform] cumplen con las políticas de uso de datos al administrar los datos. Para obtener información detallada sobre cómo [!DNL Adobe Experience Platform] aplica el control de datos, consulte la [Información general sobre el control de datos](/help/data-governance/home.md).
