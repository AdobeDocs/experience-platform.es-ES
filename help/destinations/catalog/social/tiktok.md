---
title: Conexión de TikTok
description: Cree públicos personalizados en TikTok con sus datos para segmentar con sus campañas de anuncios. Estas audiencias pueden ser de personas que visitaron el sitio web o interactuaron con el contenido. Publique de forma rápida y segura la audiencia deseada de Adobe Experience Platform a TikTok mediante la integración en tiempo real de Adobe con el Administrador de TikTok Ads.
last-substantial-update: 2023-03-20T00:00:00Z
exl-id: 7b12d17f-7d9a-4615-9830-92bffe3f6927
source-git-commit: 05e996f9e33e0d8be3d15a9ab3baaaf6d8152b5a
workflow-type: tm+mt
source-wordcount: '1046'
ht-degree: 4%

---

# Conexión de TikTok

## Información general {#overview}

Cree públicos personalizados en TikTok con sus datos para segmentar con sus campañas de anuncios. Estas audiencias pueden ser de personas que visitaron el sitio web o interactuaron con el contenido. Publique de forma rápida y segura la audiencia deseada de Adobe Experience Platform a TikTok mediante la integración en tiempo real de Adobe con el Administrador de TikTok Ads. Visita [Centro de ayuda empresarial de TikTok](https://ads.tiktok.com/help/article/audiences?lang=en) para obtener más información.

>[!IMPORTANT]
>
>El equipo de TikTok crea y mantiene este conector de destino y esta página de documentación. Para cualquier consulta o solicitud de actualización, póngase en contacto directamente con ellos en [https://ads.tiktok.com/help/](https://ads.tiktok.com/help/).

## Casos de uso {#use-cases}

Para ayudarle a comprender mejor cómo y cuándo debe utilizar el destino de TikTok, aquí tiene un ejemplo de uso para clientes de Adobe Experience Platform.

### Caso de uso {#use-case-1}

Una marca de ropa deportiva quiere llegar a los clientes existentes a través de sus cuentas en las redes sociales. La marca de ropa puede introducir direcciones de correo electrónico de su propio CRM a Adobe Experience Platform, crear audiencias a partir de sus propios datos sin conexión y enviar estas audiencias a TikTok para mostrar anuncios en las fuentes de medios sociales de sus clientes.

## Requisitos previos {#prerequisites}

Tiene que tener [!DNL Admin] o [!DNL Operator] Acceda a la cuenta de TikTok Ads Manager a la que desee enviar audiencias. Encontrará más instrucciones en la [Centro de ayuda de TikTok](https://ads.tiktok.com/help/article/add-users-tiktok-business-center?lang=en).

Antes de enviar datos a su cuenta de TikTok Ads Manager, deberá conceder permiso a Adobe Experience Platform para acceder a su cuenta de publicidad de `Audience Management`. Este permiso lo puede proporcionar [introducción de su ID de Ads Manager](#authenticate) en la interfaz de usuario de Experience Platform y conceder el permiso después de ser redirigido a su cuenta de TikTok Ads Manager.

## Identidades admitidas {#supported-identities}

TikTok admite la activación de las identidades que se describen en la tabla siguiente. Más información sobre [identidades](/help/identity-service/namespaces.md).

| Identidad de destino | Descripción | Consideraciones |
|---|---|---|
| GAID | ID de publicidad de Google | Seleccione la identidad de destino GAID cuando su identidad de origen sea un área de nombres GAID. |
| IDFA | Apple ID para anunciantes | Seleccione la identidad de destino IDFA cuando la identidad de origen sea un área de nombres IDFA. |
| Número de teléfono | Números de teléfono con hash con el algoritmo SHA256 | Los números de teléfono con hash SHA256 y texto sin formato son compatibles con Adobe Experience Platform y deben estar en formato E.164. Si el campo de origen contiene atributos sin hash, marque la **[!UICONTROL Aplicar transformación]** opción, para tener [!DNL Platform] hash automático de los datos en la activación. |
| Correo electrónico | Direcciones de correo electrónico con el algoritmo SHA256 | Adobe Experience Platform admite direcciones de correo electrónico con hash SHA256 y de texto sin formato. Si el campo de origen contiene atributos sin hash, marque la **[!UICONTROL Aplicar transformación]** opción, para tener [!DNL Platform] hash automático de los datos en la activación. |

{style="table-layout:auto"}

## Tipo y frecuencia de exportación {#export-type-frequency}

Consulte la tabla siguiente para obtener información sobre el tipo y la frecuencia de exportación de destino.

| Elemento | Tipo | Notas |
---------|----------|---------|
| Tipo de exportación | **[!UICONTROL Exportación de audiencia]** | Va a exportar todos los miembros de una audiencia con los identificadores (nombre, número de teléfono u otros) utilizados en el destino de TikTok. |
| Frecuencia de exportación | **[!UICONTROL Transmisión]** | Los destinos de streaming son conexiones basadas en API &quot;siempre activadas&quot;. Tan pronto como se actualiza un perfil en Experience Platform según la evaluación de audiencias, el conector envía la actualización de forma descendente a la plataforma de destino. Más información sobre [destinos de streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Conectar con el destino {#connect}

>[!IMPORTANT]
> 
>Para conectarse al destino, necesita el **[!UICONTROL Administrar destinos]** [permiso de control de acceso](/help/access-control/home.md#permissions). Lea el [información general de control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Para conectarse a este destino, siga los pasos descritos en la sección [tutorial de configuración de destino](../../ui/connect-destination.md). En el flujo de trabajo de configuración de destino, rellene los campos enumerados en las dos secciones siguientes.

### Autenticar en el destino {#authenticate}

Para autenticarse en el destino, se le redirigirá para que inicie sesión en su [!DNL TikTok Ads Manager] y autorizar el Adobe para administrar audiencias en su nombre.

![Selección de permisos de TikTok](/help/destinations/assets/catalog/social/tiktok/tiktok-authenticate-destination.png "Imagen de la interfaz de usuario de TikTok para seleccionar permisos")

### Rellenar detalles de destino {#destination-details}

Para configurar los detalles del destino, rellene los campos obligatorios y opcionales a continuación. Un asterisco junto a un campo en la interfaz de usuario indica que el campo es obligatorio.

![Detalles de conexión de destino](/help/destinations/assets/catalog/social/tiktok/tiktok-configure-destination-details.png "Imagen de la interfaz de usuario de Platform que muestra los detalles de conexión de destino que se van a rellenar")

* **[!UICONTROL Nombre]**: Un nombre con el que reconocerá este destino en el futuro.
* **[!UICONTROL Descripción]**: Una descripción que le ayudará a identificar este destino en el futuro.
* **[!UICONTROL ID de TikTok Ads Manager]**: su [!DNL TikTok Ads Manager ID]. Puede encontrar esto en su [!DNL TikTok Ads manager] cuenta.

![ID de TikTok Ads Manager](/help/destinations/assets/catalog/social/tiktok/tiktok-ads-manager-ID.png "Imagen de la interfaz de usuario del administrador de TikTok Ads, que muestra cómo obtener el ID del administrador de TikTok Ads")

### Habilitar alertas {#enable-alerts}

Puede activar alertas para recibir notificaciones sobre el estado del flujo de datos a su destino. Seleccione una alerta de la lista a la que suscribirse para recibir notificaciones sobre el estado del flujo de datos. Para obtener más información sobre las alertas, consulte la guía de [suscripción a alertas de destinos mediante la IU](../../ui/alerts.md).

Cuando haya terminado de proporcionar detalles para la conexión de destino, seleccione **[!UICONTROL Siguiente]**.

## Activar audiencias en este destino {#activate}

>[!IMPORTANT]
> 
>* Para activar los datos, necesita el **[!UICONTROL Administrar destinos]**, **[!UICONTROL Activar destinos]**, **[!UICONTROL Ver perfiles]**, y **[!UICONTROL Ver segmentos]** [permisos de control de acceso](/help/access-control/home.md#permissions). Lea el [información general de control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.
>* Para exportar *identidades*, necesita el **[!UICONTROL Ver gráfico de identidad]** [permiso de control de acceso](/help/access-control/home.md#permissions). <br> ![Seleccione el área de nombres de identidad resaltada en el flujo de trabajo para activar audiencias en los destinos.](/help/destinations/assets/overview/export-identities-to-destination.png "Seleccione el área de nombres de identidad resaltada en el flujo de trabajo para activar audiencias en los destinos."){width="100" zoomable="yes"}

Leer [Activación de perfiles y audiencias en destinos de exportación de audiencia de streaming](/help/destinations/ui/activate-segment-streaming-destinations.md) para obtener instrucciones sobre cómo activar audiencias en este destino.

### Asignación de identidades {#map}

A continuación se muestra un ejemplo de asignación de identidad correcta al exportar audiencias al Administrador de TikTok Ads.

Selección de campos de origen:

* Seleccione un identificador (por ejemplo:` Email_LC_SHA256`) como identidad de origen que identifica de forma exclusiva un perfil en Adobe Experience Platform y [!DNL TikTok Ads Manager].

Selección de campos de destino:

* Seleccione el área de nombres de correo electrónico como identidad de destino.

![Asignación de identidad](/help/destinations/assets/catalog/social/tiktok/tiktok-map-identity.png "Imagen de la IU de Platform, asignación de identidades")

## Datos exportados {#exported-data}

Compruebe su [!DNL TikTok Ads Manager] cuenta (en **Recursos > Audiencias**) para comprobar si la audiencia de Experience Platform se ha exportado correctamente. La audiencia se rellenará como un tipo de audiencia: `Partner Audience`.

## Uso de datos y gobernanza {#data-usage-governance}

Todo [!DNL Adobe Experience Platform] Los destinos de cumplen con las políticas de uso de datos al gestionar los datos. Para obtener información detallada sobre cómo [!DNL Adobe Experience Platform] aplica la gobernanza de datos, lea la [Resumen de gobernanza de datos](/help/data-governance/home.md).

## Recursos adicionales {#additional-resources}

Consulte la [Página del Centro de ayuda de TikTok](https://ads.tiktok.com/help/article/audiences?lang=en) para obtener más información.
