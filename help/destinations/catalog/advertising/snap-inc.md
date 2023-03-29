---
title: Conexión a Snap Inc
description: Obtenga información sobre cómo conectarse a la plataforma de anuncios de Snapchat y exportar los segmentos de audiencia desde el Experience Platform.
exl-id: 1f0f2dc0-5f3d-424b-9b22-b1a14ac30039
source-git-commit: 988ecbed3084ef162453c9f1124998c6e9ae2e45
workflow-type: tm+mt
source-wordcount: '993'
ht-degree: 1%

---

# Conexión a Snap Inc

## Información general {#overview}

[Publicidades de Snapchat](https://forbusiness.snapchat.com/) están hechos para cada empresa, sin importar el tamaño o la industria. Conviértase en parte de las conversaciones diarias de Snapchatters con anuncios digitales de pantalla completa que inspiran la acción de las personas que más importan para su negocio.

>[!IMPORTANT]
>
>Esta página de documentación la creó el *Snap Inc* equipo. Para cualquier consulta o solicitud de actualización, póngase en contacto con ellos directamente en *dev-support@snap.com*

## Casos de uso {#use-cases}

Este destino permite a los especialistas en marketing importar segmentos de usuario creados en Experience Platform en anuncios de Snapchat y utilizarlos para dirigir sus anuncios.

## Requisitos previos {#prerequisites}

Para utilizar este destino, debe tener una cuenta de Snapchat Ads. Consulte esta documentación para obtener información sobre cómo crear una:

[Introducción a la publicidad de Snapchat](https://businesshelp.snapchat.com/s/article/overview?language=en_US)

## Limitaciones {#limitations}

* Snap Inc no admite varias identidades para un segmento de audiencia determinado. Asigne solo una identidad al activar un segmento.
* Snap Inc no admite el cambio de nombre de segmentos. Para cambiar el nombre de un segmento, debe desactivarlo, cambiarle el nombre y, a continuación, activarlo.
* No es posible definir un periodo de retención para los miembros de un segmento de audiencia. Todos los miembros tienen retención de duración y permanecerán en el segmento hasta que se eliminen.

## Identidades compatibles {#supported-identities}

La variable *Snap Inc* destination admite la activación de identidades descritas en la tabla siguiente. Más información sobre [identidades](/help/identity-service/namespaces.md).

Todos los identificadores enviados al *Snap Inc* el destino debe tener un valor hash en formato SHA-256. Para hash de los identificadores de texto sin formato antes de enviarlos al destino, marque la casilla de verificación **[!UICONTROL Aplicar transformación]** al asignar identificadores de destino.

>[!WARNING]
> 
> Los identificadores sin hash no serán aceptados por el destino de Snap Inc y su envío podría causar errores.


>[!IMPORTANT]
> 
> El destino de Snap Inc no admite varias identidades. Seleccione solo una identidad.

| Identidad de Target | Descripción | Consideraciones |
|---|---|---|
| Dirección de correo electrónico | Dirección de correo electrónico con hash SHA-256 | Asignación de direcciones de correo electrónico al campo de identidad de destino *emailAddress*. |
| N.º de teléfono | Número de teléfono con hash SHA-256 | Asignación de direcciones de correo electrónico al campo de identidad de destino *phoneNumber*. |
| GAID | ID de publicidad de Google con hash SHA-256 | Asignación de ID de publicidad de Google al campo de identidad de destino *gaid*. |
| IDFA | ID de publicidad de Apple con hash SHA-256 | Asignación de ID de publicidad de Apple al campo de identidad de destino *idfa*. |

{style="table-layout:auto"}

## Tipo de exportación y frecuencia {#export-type-frequency}

Consulte la tabla siguiente para obtener información sobre el tipo y la frecuencia de exportación de destino.

| Elemento | Tipo | Notas |
---------|----------|---------|
| Tipo de exportación | **[!UICONTROL Exportación de segmentos]** | Está exportando todos los miembros de un segmento (audiencia) con los identificadores (nombre, número de teléfono u otros) utilizados en la variable *YOURDESTINATION* destino. |
| Frecuencia de exportación | **[!UICONTROL Transmisión]** | Los destinos de flujo continuo son conexiones basadas en API &quot;siempre activadas&quot;. Tan pronto como un perfil se actualiza en el Experience Platform en función de la evaluación de segmentos, el conector envía la actualización descendente a la plataforma de destino. Más información sobre [destinos de flujo continuo](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Conexión a Snap Inc {#connect}

>[!IMPORTANT]
> 
>Para conectarse al destino, necesita la variable **[!UICONTROL Administrar destinos]** [permiso de control de acceso](/help/access-control/home.md#permissions). Lea el [información general sobre el control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

### Autenticar en destino {#authenticate}

Para autenticarse en el destino, siga estos pasos:

1. Busque la *Snap Inc* destino del catálogo de destino de Adobe Experience Platform y seleccione **Configurar**.
2. Select **[!UICONTROL Conectarse al destino]**. Se le redirigirá a la siguiente pantalla:
   ![Pantalla de autenticación 1](/help/destinations/assets/catalog/advertising/snapchat-ads/auth1.png)
3. Introduzca sus credenciales de Snapchat y seleccione **Iniciar sesión**.
4. Se le mostrarán los datos de Snapchat a los que Adobe Experience Platform podrá acceder. Select **Continuar** para continuar con el proceso de conexión.

![Pantalla de autenticación 2](/help/destinations/assets/catalog/advertising/snapchat-ads/auth2.png)

Después de seleccionar continuar, espere hasta que se le redirija de nuevo a Adobe Experience Platform.

### Rellenar detalles de destino {#destination-details}

![Detalles de destino](/help/destinations/assets/catalog/advertising/snapchat-ads/destinationdetails.png)

Para configurar los detalles del destino, rellene los campos obligatorios y seleccione **[!UICONTROL Siguiente]**.

* **[!UICONTROL Nombre]**: Un nombre por el cual reconocerá este destino en el futuro.
* **[!UICONTROL Descripción]**: Descripción que le ayudará a identificar este destino en el futuro.
* **[!UICONTROL ID de cuenta]**: El ID de cuenta de anuncio asociado a la cuenta de anuncio a la que desea importar los segmentos. Para obtener más información sobre cómo encontrar esto, consulte [esta documentación en el centro de ayuda de Snapchat Business](https://businesshelp.snapchat.com/s/article/biz-acct-id?language=en_US).

>[!IMPORTANT]
> 
>Si se introduce un ID de cuenta de anuncio de Snapchat incorrecto o no válido, se producirá un error en la activación del segmento. Compruebe que ha introducido el ID de cuenta de anuncio adecuado.

### Habilitar alertas {#enable-alerts}

Puede activar las alertas para recibir notificaciones sobre el estado del flujo de datos a su destino. Seleccione una alerta de la lista para suscribirse y recibir notificaciones sobre el estado de su flujo de datos. Para obtener más información sobre las alertas, consulte la guía de [suscripción a alertas de destinos mediante la interfaz de usuario](../../ui/alerts.md).

Cuando haya terminado de proporcionar detalles para la conexión de destino, seleccione **[!UICONTROL Siguiente]**.

## Activar segmentos en este destino {#activate}

>[!IMPORTANT]
> 
>Para activar los datos, necesita la variable **[!UICONTROL Administrar destinos]**, **[!UICONTROL Activar destinos]**, **[!UICONTROL Ver perfiles]** y **[!UICONTROL Ver segmentos]** [permisos de control de acceso](/help/access-control/home.md#permissions). Lea el [información general sobre el control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Lectura [Activar perfiles y segmentos en destinos de exportación de segmentos de flujo continuo](/help/destinations/ui/activate-segment-streaming-destinations.md) para obtener instrucciones sobre la activación de segmentos de audiencia en este destino.

## Validación de la exportación de datos {#exported-data}

Después de activar segmentos en la variable *Snap Inc* destino, podrá ver los segmentos en el informe del Administrador de Snap Ads [**Audiencias** sección](https://businesshelp.snapchat.com/s/article/audience-sharing). Para acceder a esta sección, siga estos pasos:

1. Inicie sesión en el [Administrador de anuncios de instantáneas](https://ads.snapchat.com/)
2. Select **Audiencias** en el menú desplegable de la esquina superior izquierda de la pantalla. Verá los segmentos que activó en Adobe Experience Platform en la Biblioteca de audiencias:

![Audiencias](/help/destinations/assets/catalog/advertising/snapchat-ads/audiences.png)

Tenga en cuenta que cuando un segmento de Adobe se activa por primera vez en Snap Inc, inicialmente lo verá como una audiencia vacía. Esto se debe a que Adobe Experience Platform no exporta datos de miembros a Snap Inc hasta que evalúa el segmento. Para obtener más información sobre cómo se evalúan los segmentos en el Experience Platform, consulte la [Información general del servicio de segmentación](https://experienceleague.adobe.com/docs/experience-platform/segmentation/home.html?lang=en#evaluate-segments).

## Uso y gobernanza de los datos {#data-usage-governance}

Todo [!DNL Adobe Experience Platform] Los destinos de cumplen las políticas de uso de datos al administrar los datos. Para obtener información detallada sobre cómo [!DNL Adobe Experience Platform] exige el control de datos; consulte [Información general sobre la administración de datos](/help/data-governance/home.md).
