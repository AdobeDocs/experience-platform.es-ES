---
title: Perfiles de los asistentes de RainFocus
description: Aprenda a utilizar el conector de destino Perfiles de asistente de RainFocus para sincronizar perfiles de audiencia con el Perfil de asistente global de RainFocus.
last-substantial-update: 2024-12-17T00:00:00Z
exl-id: 27c3848c-411a-4305-a5d5-00b145b95287
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '1000'
ht-degree: 5%

---

# Perfiles de los asistentes de RainFocus {#rainfocus-destination}

## Información general {#overview}

Utilice el destino de [!DNL RainFocus Attendee Profiles] para transmitir perfiles de clientes de Adobe Experience Platform a la plataforma [!DNL RainFocus] con el fin de crear y actualizar perfiles de asistentes.

>[!IMPORTANT]
>
>El conector de destino y la página de documentación los crea y mantiene el equipo [!DNL RainFocus]. Para cualquier consulta o solicitud de actualización, comuníquese directamente con ellos en `clientcare@rainfocus.com` o visite el [Centro de ayuda](https://help.rainfocus.com/hc/en-us) de RainFocus.

## Casos de uso {#use-cases}

Para ayudarle a comprender mejor cómo y cuándo debe utilizar el destino de RainFocus, aquí hay casos de uso de muestra que los clientes de Adobe Experience Platform pueden solucionar mediante este destino.

### Caso de uso #1 {#use-case-1}

Una gran compañía tecnológica empresarial tiene previsto abrir el registro para su próxima exposición global y le gustaría insertar los perfiles de clientes en [!DNL RainFocus] para optimizar el proceso de registro.

### Caso de uso #2 {#use-case-2}

Una marca de servicios financieros tiene previsto organizar una serie de giras dirigidas a clientes nuevos y existentes. Tienen una serie de segmentos de audiencia con clientes objetivo en Adobe Experience Platform. Mediante el conector de destino [!DNL RainFocus], pueden enviar fácilmente esos perfiles a [!DNL RainFocus] para su activación.

## Requisitos previos {#prerequisites}

Antes de usar el destino [!DNL RainFocus], asegúrese de cumplir los siguientes requisitos previos:

* Crear un perfil de API [!DNL RainFocus] con OAuth (global).
   * El extremo **Attendee Store** debe estar habilitado.
   * Será necesario generar **ID de cliente** y **Secreto de cliente**.

También debe tener un identificador de **código de evento** de RainFocus al que desee enviar los perfiles.

## Identidades admitidas {#supported-identities}

[!DNL RainFocus] admite la activación de las identidades descritas en la tabla siguiente. Más información sobre [identidades](/help/identity-service/features/namespaces.md).

| Identidad de destino | Descripción | Consideraciones |
|---|---|---|
| email_lc_sha256 | Direcciones de correo electrónico con el algoritmo SHA256 | Adobe Experience Platform admite direcciones de correo electrónico con hash SHA256 y de texto sin formato. Si el campo de origen contiene atributos sin hash, marque la opción **[!UICONTROL Aplicar transformación]** para que [!DNL Experience Platform] aplique automáticamente el hash a los datos durante la activación. |

{style="table-layout:auto"}

## Audiencias compatibles {#supported-audiences}

Esta sección describe qué tipo de audiencias puede exportar a este destino.

| Origen de audiencia | Admitido | Descripción |
---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Audiencias generadas a través del [servicio de segmentación](../../../segmentation/home.md) de Experience Platform. |
| Cargas personalizadas | ✓ | Las audiencias [importadas](../../../segmentation/ui/overview.md#import-audience) en Experience Platform desde archivos CSV. |

{style="table-layout:auto"}

## Tipo y frecuencia de exportación {#export-type-frequency}

Consulte la tabla siguiente para obtener información sobre el tipo y la frecuencia de exportación de destino.

| Elemento | Tipo | Notas |
---------|----------|---------|
| Tipo de exportación | **[!UICONTROL Basado en perfil]** | Va a exportar todos los miembros de un segmento, junto con los campos de esquema deseados (por ejemplo: dirección de correo electrónico, número de teléfono, apellidos), tal como se eligió en la pantalla Seleccionar atributos de perfil del [flujo de trabajo de activación de destino](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes). |
| Frecuencia de exportación | **[!UICONTROL Transmisión]** | Los destinos de streaming son conexiones basadas en API &quot;siempre activadas&quot;. Tan pronto como se actualiza un perfil en Experience Platform basado en la evaluación de segmentos, el conector envía la actualización de forma descendente a la plataforma de destino. Más información sobre [destinos de streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Conexión al destino {#connect}

>[!IMPORTANT]
> 
>Para conectarse al destino, necesita el **[[!UICONTROL permiso de control de acceso]](/help/access-control/home.md#permissions) de Ver destinos&rbrack;** y **[!UICONTROL Administrar destinos]**&lbrack;para obtener acceso. Lea la [descripción general del control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Para conectarse a este destino, siga los pasos descritos en el [tutorial de configuración de destino](../../ui/connect-destination.md). En el flujo de trabajo de configuración de destino, rellene los campos enumerados en las dos secciones siguientes.

### Autenticarse en el destino {#authenticate}

Para autenticarse en el destino, rellene los campos obligatorios y seleccione **[!UICONTROL Conectar con destino]**.

![Proporcione detalles de autenticación para el conector de destino RainFocus](/help/destinations/assets/catalog/marketing-automation/rainfocus/rainfocus-destination-authentication.png)

* **[!UICONTROL ID de cliente]**: complete [!DNL Client ID] proporcionado por el perfil de API de RainFocus.
* **[!UICONTROL Secreto de cliente]**: complete [!DNL Client Secret] proporcionado por el perfil de API de RainFocus.
* **[!UICONTROL Entorno]**: especifique a qué entorno de RainFocus se está conectando, por ejemplo `dev`, `prod`.
* **[!UICONTROL ID de organización]**: proporcione el `orgid` único para su instancia de RainFocus.

### Rellenar detalles de destino {#destination-details}

Para configurar los detalles del destino, rellene los campos obligatorios y opcionales a continuación. Un asterisco junto a un campo en la interfaz de usuario indica que el campo es obligatorio.

![Proporcione detalles de conexión para el conector de destino RainFocus](/help/destinations/assets/catalog/marketing-automation/rainfocus/rainfocus-configure-destination-details.png)

* **[!UICONTROL Nombre]**: Un nombre por el cual reconocerá este destino en el futuro.
* **[!UICONTROL Descripción]**: Una descripción que le ayudará a identificar este destino en el futuro.
* **[!UICONTROL ID de evento]**: el identificador de código de evento [!DNL RainFocus] al que desea que se envíen los perfiles.

### Habilitar alertas {#enable-alerts}

Puede activar alertas para recibir notificaciones sobre el estado del flujo de datos a su destino. Seleccione una alerta de la lista a la que suscribirse para recibir notificaciones sobre el estado del flujo de datos. Para obtener más información sobre las alertas, consulte la guía sobre [suscripción a alertas de destinos mediante la interfaz de usuario](../../ui/alerts.md).

Cuando termine de proporcionar detalles para la conexión de destino, seleccione **[!UICONTROL Siguiente]**.

## Activar segmentos en este destino {#activate}

>[!IMPORTANT]
> 
>* Para activar los datos, necesita los **[!UICONTROL permisos de control de acceso]**, **[!UICONTROL Activar destinos]**, **[!UICONTROL Ver perfiles]** y **[!UICONTROL Ver segmentos]**&#x200B;[para ](/help/access-control/home.md#permissions). Lea la [descripción general del control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Lea [Activar perfiles y segmentos en destinos de exportación de segmentos de flujo continuo](/help/destinations/ui/activate-segment-streaming-destinations.md) para obtener instrucciones sobre cómo activar segmentos de audiencia en este destino.

### Asignar atributos e identidades {#map}

Las siguientes áreas de nombres de identidad de destino deben asignarse según el caso de uso:

* **Correo electrónico** debe asignarse como campo de destino mediante **Campo de destino > Seleccionar área de nombres de identidad > correo electrónico**

![Cómo asignar campos de perfil e identidad](/help/destinations/assets/catalog/marketing-automation/rainfocus/rainfocus-destination-mapping.png)

Se recomienda asignar campos de perfil adicionales, ya que esto garantizará que el perfil del asistente en [!DNL RainFocus] esté completamente rellenado. Los siguientes campos de destino están disponibles en [!DNL RainFocus]:

| Campo de destino | Descripción |
|------------|-------------|
| `address1` | La primera línea de la dirección de la calle |
| `address2` | La segunda línea de la dirección de la calle (si corresponde) |
| `city` | El nombre de la ciudad |
| `companyname` | El nombre de la empresa |
| `countryid` | Un identificador de código de país ISO 3166-1 alpha-2 para el país |
| `email` | La dirección de correo electrónico |
| `firstname` | El nombre de la persona |
| `lastname` | El apellido de la persona |
| `jobtitle` | El puesto que ocupa la persona |
| `phone` | El número de teléfono |
| `state` | El código alfa de estado FIPS para el estado o la provincia |
| `zip` | El código postal |

{style="table-layout:auto"}

## Datos exportados / Validar exportación de datos {#exported-data}

Una vez enviado un conjunto de perfiles a [!DNL RainFocus], use el registro de perfil de API en [!DNL RainFocus] para validar que los perfiles se hayan ingerido correctamente.

![Ver registros en el perfil de API en RainFocus](/help/destinations/assets/catalog/marketing-automation/rainfocus/rainfocus-destination-api-profile.png)

![Validar que los perfiles se hayan ingerido correctamente](/help/destinations/assets/catalog/marketing-automation/rainfocus/rainfocus-destination-api-logging.png)

## Uso de datos y gobernanza {#data-usage-governance}

Todos los destinos de [!DNL Adobe Experience Platform] cumplen con las políticas de uso de datos al administrar los datos. Para obtener información detallada sobre cómo [!DNL Adobe Experience Platform] aplica el control de datos, lea la [Información general sobre el control de datos](/help/data-governance/home.md).

## Recursos adicionales {#additional-resources}

* [Conector de Source de flujo RainFocus](https://experienceleague.adobe.com/es/docs/experience-platform/sources/connectors/analytics/rainfocus)
