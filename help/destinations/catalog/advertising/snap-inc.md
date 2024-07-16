---
title: Conexión de Snap Inc
description: Aprenda a conectarse a la plataforma de anuncios de Snapchat y a exportar las audiencias desde Experience Platform.
exl-id: 1f0f2dc0-5f3d-424b-9b22-b1a14ac30039
source-git-commit: ba39f62cd77acedb7bfc0081dbb5f59906c9b287
workflow-type: tm+mt
source-wordcount: '1012'
ht-degree: 2%

---

# Conexión de Snap Inc

## Información general {#overview}

[Los anuncios de Snapchat](https://forbusiness.snapchat.com/) se hacen para cada negocio, sin importar el tamaño o la industria. Forma parte de las conversaciones cotidianas de los Snapchatters con anuncios digitales en pantalla completa que inspiran la acción de las personas que más importan a tu negocio.

>[!IMPORTANT]
>
>El equipo *Snap Inc* crea y mantiene este conector de destino y esta página de documentación. Para cualquier consulta o solicitud de actualización, comuníquese directamente con ellos en *dev-support@snap.com*

## Casos de uso {#use-cases}

Este destino permite a los especialistas en marketing importar audiencias de usuarios creadas en Experience Platform a anuncios de Snapchat y utilizarlas para segmentar sus anuncios.

## Requisitos previos {#prerequisites}

Para usar este destino, debes tener una cuenta de Snapchat Ads. Consulte esta documentación para obtener información sobre cómo crear una:

[Introducción a Snapchat Advertising](https://businesshelp.snapchat.com/s/article/overview?language=en_US)

## Limitaciones {#limitations}

* Snap Inc no admite varias identidades para un segmento de audiencia determinado. Asigne solo una identidad al activar un segmento.
* Snap Inc no admite el cambio de nombre de segmentos. Para cambiar el nombre de un segmento, debe desactivarlo, cambiarle el nombre y, a continuación, activarlo.
* No es posible definir un período de retención para los miembros de un segmento de audiencia. Todos los miembros tienen retención de duración y estarán en la audiencia hasta que se eliminen.

## Identidades admitidas {#supported-identities}

El destino *Snap Inc* admite la activación de identidades descritas en la tabla siguiente. Más información sobre [identidades](/help/identity-service/features/namespaces.md).

Todos los identificadores enviados al destino *Snap Inc* deben tener un cifrado hash en formato SHA-256. Para hacer un hash de los identificadores de texto sin formato antes de enviarlos al destino, marque la opción **[!UICONTROL Aplicar transformación]** al asignar identificadores de destino para el destino.

>[!WARNING]
> 
> El destino Snap Inc no aceptará identificadores no hash y su envío podría provocar errores.


>[!IMPORTANT]
> 
> El destino Snap Inc no admite varias identidades. Seleccione solo una identidad.

| Identidad de destino | Descripción | Consideraciones |
|---|---|---|
| Correo electrónico | Dirección de correo electrónico con hash SHA-256 | Asigne direcciones de correo electrónico al campo de identidad de destino *emailAddress*. |
| Número de teléfono | Número de teléfono con hash SHA-256 | Asigne direcciones de correo electrónico al campo de identidad de destino *phoneNumber*. |
| GAID | ID de Advertising de Google con hash SHA-256 | Asigne ID de Advertising de Google al campo de identidad de destino *gaid*. |
| IDFA | ID de Advertising de Apple con hash SHA-256 | Asigne ID de Advertising de Apple al campo de identidad de destino *idfa*. |

{style="table-layout:auto"}

## Tipo y frecuencia de exportación {#export-type-frequency}

Consulte la tabla siguiente para obtener información sobre el tipo y la frecuencia de exportación de destino.

| Elemento | Tipo | Notas |
---------|----------|---------|
| Tipo de exportación | **[!UICONTROL Exportación de audiencia]** | Va a exportar todos los miembros de una audiencia con los identificadores (nombre, número de teléfono u otros) utilizados en el destino *YOURDESTINATION*. |
| Frecuencia de exportación | **[!UICONTROL Transmisión]** | Los destinos de streaming son conexiones basadas en API &quot;siempre activadas&quot;. Tan pronto como se actualiza un perfil en Experience Platform según la evaluación de audiencias, el conector envía la actualización de forma descendente a la plataforma de destino. Más información sobre [destinos de streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Conectando con Snap Inc {#connect}

>[!IMPORTANT]
> 
>Para conectarse al destino, necesita los **[!UICONTROL permisos de control de acceso](/help/access-control/home.md#permissions) de Ver destinos]** y **[!UICONTROL Administrar destinos]**[5}. Lea la [descripción general del control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

### Autenticarse en el destino {#authenticate}

Para autenticarse en el destino, siga estos pasos:

1. Busque el destino *Snap Inc* en el catálogo de destino de Adobe Experience Platform y seleccione **Configurar**.
2. Seleccione **[!UICONTROL Conectar con destino]**. Se le redirigirá a la siguiente pantalla:
   ![Pantalla de autenticación 1](/help/destinations/assets/catalog/advertising/snapchat-ads/auth1.png)
3. Escribe tus credenciales de Snapchat y selecciona **Iniciar sesión**.
4. Se te mostrarán los datos de Snapchat a los que Adobe Experience Platform podrá acceder. Seleccione **Continuar** para continuar con el proceso de conexión.

![Pantalla de autenticación 2](/help/destinations/assets/catalog/advertising/snapchat-ads/auth2.png)

Después de seleccionar continuar, espere hasta que se le redirija de nuevo a Adobe Experience Platform.

### Rellenar detalles de destino {#destination-details}

![Detalles del destino](/help/destinations/assets/catalog/advertising/snapchat-ads/destinationdetails.png)

Para configurar los detalles del destino, rellena los campos obligatorios y selecciona **[!UICONTROL Siguiente]**.

* **[!UICONTROL Nombre]**: Un nombre por el cual reconocerá este destino en el futuro.
* **[!UICONTROL Descripción]**: Una descripción que le ayudará a identificar este destino en el futuro.
* **[!UICONTROL ID de cuenta]**: el ID de cuenta de publicidad asociado con la cuenta de publicidad a la que desea importar las audiencias. Para obtener más información sobre cómo encontrar esto, consulte [esta documentación en el Centro de ayuda para empresas de Snapchat](https://businesshelp.snapchat.com/s/article/biz-acct-id?language=en_US).

>[!IMPORTANT]
> 
>Si se introduce un ID de cuenta de publicidad de Snapchat incorrecto o no válido, la activación de la audiencia fallará. Compruebe que ha introducido el ID de cuenta de publicidad correcto.

### Habilitar alertas {#enable-alerts}

Puede activar alertas para recibir notificaciones sobre el estado del flujo de datos a su destino. Seleccione una alerta de la lista a la que suscribirse para recibir notificaciones sobre el estado del flujo de datos. Para obtener más información sobre las alertas, consulte la guía sobre [suscripción a alertas de destinos mediante la interfaz de usuario](../../ui/alerts.md).

Cuando termine de proporcionar detalles para la conexión de destino, seleccione **[!UICONTROL Siguiente]**.

## Activar públicos en este destino {#activate}

>[!IMPORTANT]
> 
>* Para activar los datos, necesita los **[!UICONTROL permisos de control de acceso]**, **[!UICONTROL Activar destinos]**, **[!UICONTROL Ver perfiles]** y **[!UICONTROL Ver segmentos]**[para ](/help/access-control/home.md#permissions). Lea la [descripción general del control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.
>* Para exportar *identidades*, necesita el **[!UICONTROL permiso de control de acceso](/help/access-control/home.md#permissions) de]** Ver gráfico de identidad[. <br> ![Seleccione el área de nombres de identidad resaltada en el flujo de trabajo para activar audiencias en los destinos.](/help/destinations/assets/overview/export-identities-to-destination.png "Seleccione el área de nombres de identidad resaltada en el flujo de trabajo para activar audiencias en los destinos."){width="100" zoomable="yes"}

Lea [Activar perfiles y audiencias en destinos de exportación de audiencias de streaming](/help/destinations/ui/activate-segment-streaming-destinations.md) para obtener instrucciones sobre cómo activar audiencias en este destino.

## Validar exportación de datos {#exported-data}

Después de activar audiencias en el destino *Snap Inc*, podrás ver las audiencias en la sección [**Audiencias** del Administrador de anuncios de Snap](https://businesshelp.snapchat.com/s/article/audience-sharing). Para desplazarse a esta sección, siga estos pasos:

1. Iniciar sesión en [Administrador de anuncios de Snap](https://ads.snapchat.com/)
2. Seleccione **Audiencias** en el menú desplegable de la esquina superior izquierda de la pantalla. Verá las audiencias que activó en Adobe Experience Platform en la Biblioteca de audiencias:

![Públicos](/help/destinations/assets/catalog/advertising/snapchat-ads/audiences.png)

Tenga en cuenta que cuando se activa por primera vez una audiencia de Adobe en Snap Inc, inicialmente la verá como una audiencia vacía. Esto se debe a que Adobe Experience Platform no exporta datos de miembros a Snap Inc hasta que evalúa la audiencia. Para obtener más información sobre cómo se evalúan las audiencias en Experience Platform, consulte la [descripción general del servicio de segmentación](https://experienceleague.adobe.com/docs/experience-platform/segmentation/home.html#evaluate-segments).

## Uso de datos y gobernanza {#data-usage-governance}

Todos los destinos de [!DNL Adobe Experience Platform] cumplen con las políticas de uso de datos al administrar los datos. Para obtener información detallada sobre cómo [!DNL Adobe Experience Platform] aplica el control de datos, consulte la [Información general sobre el control de datos](/help/data-governance/home.md).
