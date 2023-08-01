---
title: Conexión de Snap Inc
description: Aprenda a conectarse a la plataforma de anuncios de Snapchat y a exportar las audiencias desde Experience Platform.
exl-id: 1f0f2dc0-5f3d-424b-9b22-b1a14ac30039
source-git-commit: 1ed82798125f32fe392f2a06a12280ac61f225c6
workflow-type: tm+mt
source-wordcount: '994'
ht-degree: 1%

---

# Conexión de Snap Inc

## Información general {#overview}

[Anuncios de Snapchat](https://forbusiness.snapchat.com/) están hechos para cada negocio, no importa el tamaño o la industria. Forma parte de las conversaciones cotidianas de los Snapchatters con anuncios digitales en pantalla completa que inspiran la acción de las personas que más importan a tu negocio.

>[!IMPORTANT]
>
>Este conector de destino y la página de documentación los crea y mantiene el *Snap Inc* equipo. Para cualquier consulta o solicitud de actualización, póngase en contacto directamente con ellos en *dev-support@snap.com*

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

El *Snap Inc* El destino de admite la activación de las identidades descritas en la siguiente tabla. Más información sobre [identidades](/help/identity-service/namespaces.md).

Todos los identificadores enviados a *Snap Inc* El destino debe tener un cifrado hash en formato SHA-256. Para hash los identificadores de texto sin formato antes de enviarlos al destino, marque la **[!UICONTROL Aplicar transformación]** opción al asignar identificadores de destino para el destino.

>[!WARNING]
> 
> El destino Snap Inc no aceptará identificadores no hash y su envío podría provocar errores.


>[!IMPORTANT]
> 
> El destino Snap Inc no admite varias identidades. Seleccione solo una identidad.

| Identidad de destino | Descripción | Consideraciones |
|---|---|---|
| Dirección de correo electrónico | Dirección de correo electrónico con hash SHA-256 | Asignación de direcciones de correo electrónico al campo de identidad de destinatario *emailAddress*. |
| N.º de teléfono | Número de teléfono con hash SHA-256 | Asignación de direcciones de correo electrónico al campo de identidad de destinatario *phoneNumber*. |
| GAID | ID de publicidad de Google con hash SHA-256 | Asignación de ID de publicidad de Google al campo de identidad de destinatario *gaid*. |
| IDFA | ID de publicidad de Apple con hash SHA-256 | Asignación de ID de publicidad de Apple al campo de identidad de destinatario *idfa*. |

{style="table-layout:auto"}

## Tipo y frecuencia de exportación {#export-type-frequency}

Consulte la tabla siguiente para obtener información sobre el tipo y la frecuencia de exportación de destino.

| Elemento | Tipo | Notas |
---------|----------|---------|
| Tipo de exportación | **[!UICONTROL Exportación de audiencia]** | Va a exportar todos los miembros de una audiencia con los identificadores (nombre, número de teléfono u otros) utilizados en *SU DESTINO* destino. |
| Frecuencia de exportación | **[!UICONTROL Transmisión]** | Los destinos de streaming son conexiones basadas en API &quot;siempre activadas&quot;. Tan pronto como se actualiza un perfil en Experience Platform según la evaluación de audiencias, el conector envía la actualización de forma descendente a la plataforma de destino. Más información sobre [destinos de streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Conectando con Snap Inc {#connect}

>[!IMPORTANT]
> 
>Para conectarse al destino, necesita el **[!UICONTROL Administrar destinos]** [permiso de control de acceso](/help/access-control/home.md#permissions). Lea el [información general de control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

### Autenticar en el destino {#authenticate}

Para autenticarse en el destino, siga estos pasos:

1. Busque el *Snap Inc* en el catálogo de destino de Adobe Experience Platform y seleccione **Configurar**.
2. Seleccionar **[!UICONTROL Conectar con destino]**. Se le redirigirá a la siguiente pantalla:
   ![Pantalla de autenticación 1](/help/destinations/assets/catalog/advertising/snapchat-ads/auth1.png)
3. Introduzca sus credenciales de Snapchat y seleccione **Iniciar sesión**.
4. Se te mostrarán los datos de Snapchat a los que Adobe Experience Platform podrá acceder. Seleccionar **Continuar** para continuar con el proceso de conexión.

![Pantalla de autenticación 2](/help/destinations/assets/catalog/advertising/snapchat-ads/auth2.png)

Después de seleccionar continuar, espere hasta que se le redirija de nuevo a Adobe Experience Platform.

### Rellenar detalles de destino {#destination-details}

![Detalles del destino](/help/destinations/assets/catalog/advertising/snapchat-ads/destinationdetails.png)

Para configurar los detalles del destino, rellene los campos obligatorios y seleccione **[!UICONTROL Siguiente]**.

* **[!UICONTROL Nombre]**: Un nombre con el que reconocerá este destino en el futuro.
* **[!UICONTROL Descripción]**: Una descripción que le ayudará a identificar este destino en el futuro.
* **[!UICONTROL ID de cuenta]**: ID de la cuenta de publicidad asociado con la cuenta de publicidad a la que desea importar las audiencias. Para obtener más información sobre cómo encontrar esto, consulte [esta documentación en el Centro de ayuda empresarial de Snapchat](https://businesshelp.snapchat.com/s/article/biz-acct-id?language=en_US).

>[!IMPORTANT]
> 
>Si se introduce un ID de cuenta de publicidad de Snapchat incorrecto o no válido, la activación de la audiencia fallará. Compruebe que ha introducido el ID de cuenta de publicidad correcto.

### Habilitar alertas {#enable-alerts}

Puede activar alertas para recibir notificaciones sobre el estado del flujo de datos a su destino. Seleccione una alerta de la lista a la que suscribirse para recibir notificaciones sobre el estado del flujo de datos. Para obtener más información sobre las alertas, consulte la guía de [suscripción a alertas de destinos mediante la IU](../../ui/alerts.md).

Cuando haya terminado de proporcionar detalles para la conexión de destino, seleccione **[!UICONTROL Siguiente]**.

## Activar audiencias en este destino {#activate}

>[!IMPORTANT]
> 
>Para activar los datos, necesita el **[!UICONTROL Administrar destinos]**, **[!UICONTROL Activar destinos]**, **[!UICONTROL Ver perfiles]**, y **[!UICONTROL Ver segmentos]** [permisos de control de acceso](/help/access-control/home.md#permissions). Lea el [información general de control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Leer [Activación de perfiles y audiencias en destinos de exportación de audiencia de streaming](/help/destinations/ui/activate-segment-streaming-destinations.md) para obtener instrucciones sobre cómo activar audiencias en este destino.

## Validar exportación de datos {#exported-data}

Después de activar las audiencias en *Snap Inc* destino, podrá ver las audiencias en el cuadro de diálogo [**Audiencias** sección](https://businesshelp.snapchat.com/s/article/audience-sharing). Para desplazarse a esta sección, siga estos pasos:

1. Inicie sesión en [Administrador de anuncios de Snap](https://ads.snapchat.com/)
2. Seleccionar **Audiencias** en el menú desplegable situado en la esquina superior izquierda de la pantalla. Verá las audiencias que activó en Adobe Experience Platform en la Biblioteca de audiencias:

![Audiences](/help/destinations/assets/catalog/advertising/snapchat-ads/audiences.png)

Tenga en cuenta que cuando se activa por primera vez una audiencia de Adobe en Snap Inc, inicialmente la verá como una audiencia vacía. Esto se debe a que Adobe Experience Platform no exporta datos de miembros a Snap Inc hasta que evalúa la audiencia. Para obtener más información sobre cómo se evalúan las audiencias en Experience Platform, consulte la [Resumen del servicio de segmentación](https://experienceleague.adobe.com/docs/experience-platform/segmentation/home.html?lang=en#evaluate-segments).

## Uso de datos y gobernanza {#data-usage-governance}

Todo [!DNL Adobe Experience Platform] Los destinos de cumplen con las políticas de uso de datos al gestionar los datos. Para obtener información detallada sobre cómo [!DNL Adobe Experience Platform] aplica la gobernanza de datos. Consulte la [Resumen de gobernanza de datos](/help/data-governance/home.md).
