---
title: Conexión TikTok
description: Cree audiencias personalizadas en TikTok con sus datos para segmentar con sus campañas de publicidad. Estas audiencias pueden ser de personas que visitaron el sitio web o que interactuaron con el contenido. Inserte de forma rápida y segura el segmento deseado de Adobe Experience Platform a TikTok mediante la integración en tiempo real de Adobe con TikTok Ads Manager.
last-substantial-update: 2023-03-20T00:00:00Z
source-git-commit: 7bfcd0132380f0c847742ff05c1f334542adfba2
workflow-type: tm+mt
source-wordcount: '980'
ht-degree: 2%

---


# Conexión TikTok

## Información general {#overview}

Cree audiencias personalizadas en TikTok con sus datos para segmentar con sus campañas de publicidad. Estas audiencias pueden ser de personas que visitaron el sitio web o que interactuaron con el contenido. Inserte de forma rápida y segura el segmento deseado de Adobe Experience Platform a TikTok mediante la integración en tiempo real de Adobe con TikTok Ads Manager. Visita [Centro de ayuda empresarial de TikTok](https://ads.tiktok.com/help/article/audiences?lang=en) para obtener más información.

>[!IMPORTANT]
>
>El equipo de TikTok ha creado esta página de documentación. Para cualquier consulta o solicitud de actualización, póngase en contacto con ellos directamente en [https://ads.tiktok.com/help/](https://ads.tiktok.com/help/).

## Casos de uso {#use-cases}

Para ayudarle a comprender mejor cómo y cuándo debe utilizar el destino de TikTok, este es un ejemplo de caso de uso para clientes de Adobe Experience Platform.

### Caso de uso {#use-case-1}

Una marca de ropa deportiva quiere llegar a los clientes existentes a través de sus cuentas de medios sociales. La marca de ropa puede introducir direcciones de correo electrónico desde su propio CRM a Adobe Experience Platform, generar segmentos a partir de sus propios datos sin conexión y enviar estos segmentos a TikTok para mostrar anuncios en las fuentes de medios sociales de sus clientes.

## Requisitos previos {#prerequisites}

Antes de enviar datos a su [!DNL TikTok Ads Manager] , deberá dar permiso a Adobe Experience Platform para acceder a su cuenta de publicidad para `Audience Management`. Este permiso se puede proporcionar introduciendo su ID de anunciante en el Experience Platform y siguiendo la redirección para conceder el permiso. Puede encontrar más instrucciones en la sección [Documentación de la API de TikTok](https://ads.tiktok.com/marketing_api/docs?id=1738373141733378).

## Identidades compatibles {#supported-identities}

TikTok admite la activación de identidades descritas en la tabla siguiente. Más información sobre [identidades](/help/identity-service/namespaces.md).

| Identidad de Target | Descripción | Consideraciones |
|---|---|---|
| GAID | Google Advertising ID | Seleccione la identidad objetivo GAID cuando su identidad de origen sea un área de nombres GAID. |
| IDFA | Apple ID para anunciantes | Seleccione la identidad de destino IDFA cuando la identidad de origen sea un área de nombres IDFA. |
| Número de teléfono | Números de teléfono con hash con el algoritmo SHA256 | Adobe Experience Platform admite los números de teléfono tanto de texto sin formato como de hash SHA256, y deben tener el formato E.164. Si el campo de origen contiene atributos sin hash, marque la casilla de verificación **[!UICONTROL Aplicar transformación]** para [!DNL Platform] hash automático de los datos al activarlos. |
| Correo electrónico | Direcciones de correo electrónico con hash con el algoritmo SHA256 | Adobe Experience Platform admite las direcciones de correo electrónico con texto sin formato y con hash SHA 256. Si el campo de origen contiene atributos sin hash, marque la casilla de verificación **[!UICONTROL Aplicar transformación]** para [!DNL Platform] hash automático de los datos al activarlos. |

{style="table-layout:auto"}

## Tipo de exportación y frecuencia {#export-type-frequency}

Consulte la tabla siguiente para obtener información sobre el tipo y la frecuencia de exportación de destino.

| Elemento | Tipo | Notas |
---------|----------|---------|
| Tipo de exportación | **[!UICONTROL Exportación de segmentos]** | Está exportando todos los miembros de un segmento (audiencia) con los identificadores (nombre, número de teléfono u otros) utilizados en el destino de TikTok. |
| Frecuencia de exportación | **[!UICONTROL Transmisión]** | Los destinos de flujo continuo son conexiones basadas en API &quot;siempre activadas&quot;. Tan pronto como un perfil se actualiza en el Experience Platform en función de la evaluación de segmentos, el conector envía la actualización descendente a la plataforma de destino. Más información sobre [destinos de flujo continuo](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Conectarse al destino {#connect}

>[!IMPORTANT]
> 
>Para conectarse al destino, necesita la variable **[!UICONTROL Administrar destinos]** [permiso de control de acceso](/help/access-control/home.md#permissions). Lea el [información general sobre el control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Para conectarse a este destino, siga los pasos descritos en la sección [tutorial de configuración de destino](../../ui/connect-destination.md). En el flujo de trabajo de configuración de destino, rellene los campos que aparecen en las dos secciones siguientes.

### Autenticar en destino {#authenticate}

Para autenticarse en el destino, se le redirigirá para que inicie sesión en su [!DNL TikTok Ads Manager] y autorice el Adobe para administrar audiencias en su nombre.

![Selección de permisos de TikTok](/help/destinations/assets/catalog/social/tiktok/tiktok-authenticate-destination.png "Imagen de la interfaz de usuario de TikTok para seleccionar permisos")

### Rellenar detalles de destino {#destination-details}

Para configurar los detalles del destino, rellene los campos opcionales y requeridos a continuación. Un asterisco junto a un campo en la interfaz de usuario indica que el campo es obligatorio.

![Detalles de conexión de destino](/help/destinations/assets/catalog/social/tiktok/tiktok-configure-destination-details.png "Imagen de la interfaz de usuario de Platform que muestra los detalles de conexión de destino que se van a rellenar")

* **[!UICONTROL Nombre]**: Un nombre por el cual reconocerá este destino en el futuro.
* **[!UICONTROL Descripción]**: Descripción que le ayudará a identificar este destino en el futuro.
* **[!UICONTROL ID del administrador de TikTok Ads]**: Su [!DNL TikTok Ads Manager ID]. Puede encontrarlo en su [!DNL TikTok Ads manager] cuenta.

![ID del administrador de TikTok Ads](/help/destinations/assets/catalog/social/tiktok/tiktok-ads-manager-ID.png "Imagen de la interfaz de usuario del administrador de TikTok Ads, que muestra cómo obtener el ID del administrador de TikTok Ads")

### Habilitar alertas {#enable-alerts}

Puede activar las alertas para recibir notificaciones sobre el estado del flujo de datos a su destino. Seleccione una alerta de la lista para suscribirse y recibir notificaciones sobre el estado de su flujo de datos. Para obtener más información sobre las alertas, consulte la guía de [suscripción a alertas de destinos mediante la interfaz de usuario](../../ui/alerts.md).

Cuando haya terminado de proporcionar detalles para la conexión de destino, seleccione **[!UICONTROL Siguiente]**.

## Activar segmentos en este destino {#activate}

>[!IMPORTANT]
> 
>Para activar los datos, necesita la variable **[!UICONTROL Administrar destinos]**, **[!UICONTROL Activar destinos]**, **[!UICONTROL Ver perfiles]** y **[!UICONTROL Ver segmentos]** [permisos de control de acceso](/help/access-control/home.md#permissions). Lea el [información general sobre el control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Lectura [Activar perfiles y segmentos en destinos de exportación de segmentos de flujo continuo](/help/destinations/ui/activate-segment-streaming-destinations.md) para obtener instrucciones sobre la activación de segmentos de audiencia en este destino.

### Asignación de identidades {#map}

A continuación se muestra un ejemplo de asignación de identidad correcta al exportar segmentos a TikTok Ads Manager.

Selección de campos de origen:

* Seleccione un identificador (por ejemplo:` Email_LC_SHA256`) como identidad de origen que identifica de forma exclusiva un perfil en Adobe Experience Platform y [!DNL TikTok Ads Manager].

Selección de campos de destino:

* Seleccione el espacio de nombres del correo electrónico como identidad de destino.

![Asignación de identidad](/help/destinations/assets/catalog/social/tiktok/tiktok-map-identity.png "Imagen de la interfaz de usuario de Platform, asignación de identidades")

## Datos exportados {#exported-data}

Compruebe su [!DNL TikTok Ads Manager] cuenta (en **Assets > Audiencias**) para comprobar si el segmento del Experience Platform se ha exportado correctamente. La audiencia se rellenará como un tipo de audiencia: `Partner Audience`.

## Uso y gobernanza de los datos {#data-usage-governance}

Todo [!DNL Adobe Experience Platform] Los destinos de cumplen las políticas de uso de datos al administrar los datos. Para obtener información detallada sobre cómo [!DNL Adobe Experience Platform] exige la administración de datos, lea la [Información general sobre la administración de datos](/help/data-governance/home.md).

## Recursos adicionales {#additional-resources}

Consulte la [Página del Centro de ayuda de TikTok](https://ads.tiktok.com/help/article/audiences?lang=en) para obtener más información.
