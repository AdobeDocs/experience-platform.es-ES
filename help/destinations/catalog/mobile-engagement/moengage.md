---
title: Conexión de Moengage
description: Moengage es una plataforma de participación del cliente que potencia las interacciones centradas en el cliente entre consumidores y marcas en tiempo real.
last-substantial-update: 2023-10-11T00:00:00Z
exl-id: 051f1a10-3c41-4c0a-b187-bf80de0565f0
source-git-commit: 308d07cf0c3b4096ca934a9008a13bf425dc30b6
workflow-type: tm+mt
source-wordcount: '1002'
ht-degree: 2%

---

# [!DNL Moengage] conexión

## Información general {#overview}

Utilice el [!DNL Moengage] para conectarse y asignar sus datos de Adobe (atributos de usuario, segmentos y eventos) a MoEngage en tiempo real. A continuación, los clientes pueden actuar sobre estos datos y ofrecer experiencias personalizadas y específicas.

Con Adobe, la integración es muy sencilla e intuitiva. Simplemente, tome cualquier perfil de usuario de Adobe y asígnelo a un atributo de usuario MoEngage.

>[!IMPORTANT]
>
>Este conector de destino y la página de documentación los crea y mantiene el *Moengage* equipo. Para cualquier consulta o solicitud de actualización, póngase en contacto directamente con ellos en *`https://help.moengage.com/hc/en-us`.*

## Casos de uso {#use-cases}

Un experto en marketing desea dirigirse a un segmento de usuario (integrado en Adobe Experience Platform) mediante [!DNL Moengage] campañas. Además, desean personalizar el contenido de la campaña en función de los atributos de los perfiles de Adobe Experience Platform. Con esta integración, los usuarios y atributos se actualizan en MoEngage en cuanto los segmentos y perfiles se actualizan en Adobe Experience Platform.

## Requisitos previos {#prerequisites}

Antes de poder enviar los datos de Adobe Experience Platform a [!DNL Moengage], tenga en cuenta los siguientes requisitos previos:

* Para utilizar el destino MoEngage con Adobe Experience Platform, los usuarios deben tener primero acceso a su [!DNL Moengage] Cuenta. Visite la siguiente página para registrarse o iniciar sesión en su cuenta de MoEngage: https://app.moengage.com


## Identidades admitidas {#supported-identities}

[!DNL Moengage] admite la activación de identidades descritas en la tabla siguiente.

| Identidad de destino | Descripción | Consideraciones |
|---|------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------|
| user_id | Identificador único que identifica de forma exclusiva un perfil de usuario en [!DNL Moengage] sistema. | Este identificador admite el tipo de cadena. Se requiere uno de user_id o anonymous_id |
| anonymous_id | Otro identificador para un perfil de usuario desconocido: es decir, un perfil que no existe en el sistema. | Este identificador admite el tipo de cadena. Se requiere uno de user_id o anonymous_id |

{style="table-layout:auto"}

## Tipo y frecuencia de exportación {#export-type-frequency}

Consulte la tabla siguiente para obtener información sobre el tipo y la frecuencia de exportación de destino.

| Elemento | Tipo | Notas |
---------|----------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Tipo de exportación | **[!UICONTROL Basado en perfiles]** | Va a exportar todos los miembros de un segmento (audiencia) con los identificadores (user_id, anonymous_id) junto con los atributos personalizados definidos por ha exportado a [!DNL Moengage]. |
| Frecuencia de exportación | **[!UICONTROL Transmisión]** | Los destinos de streaming son conexiones basadas en API &quot;siempre activadas&quot;. Tan pronto como se actualiza un perfil en Experience Platform según la evaluación de segmentos, el conector envía la actualización de forma descendente a la plataforma de destino. Más información sobre [destinos de streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Conexión al destino {#connect}

>[!IMPORTANT]
> 
>Para conectarse al destino, necesita el **[!UICONTROL Administrar destinos]** [permiso de control de acceso](/help/access-control/home.md#permissions). Lea el [información general de control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Para conectarse a este destino, siga los pasos descritos en la sección [tutorial de configuración de destino](../../ui/connect-destination.md). En el flujo de trabajo de configuración de destino, rellene los campos enumerados en las dos secciones siguientes.

### Autenticarse en el destino {#authenticate}

Para autenticarse en el destino, rellene los campos obligatorios y seleccione **[!UICONTROL Conectar con destino]**.

![Autenticación de destino de Moengage](../../assets/catalog/mobile-engagement/moengage/authentication.png)

### Rellenar detalles de destino {#destination-details}

Para configurar los detalles del destino, rellene los campos obligatorios y opcionales a continuación. Un asterisco junto a un campo en la interfaz de usuario indica que el campo es obligatorio.
![Autenticación de destino de Moengage](../../assets/catalog/mobile-engagement/moengage/settings.png)
* **[!UICONTROL USUARIO]**: ID de APLICACIÓN DE DATOS de la página de configuración de [!DNL Moengage] panel.
* **[!UICONTROL CONTRASEÑA]**: CLAVE DE APLICACIÓN DE DATOS de la página de configuración de [!DNL Moengage] panel.

![Autenticación de destino de Moengage](../../assets/catalog/mobile-engagement/moengage/destination_details.png)

* **[!UICONTROL Nombre]**: Un nombre con el que reconocerá este destino en el futuro.
* **[!UICONTROL Descripción]**: Una descripción que le ayudará a identificar este destino en el futuro.
* **[!UICONTROL Región]**: su aplicación *centro de datos*.

### Habilitar alertas {#enable-alerts}

Puede activar alertas para recibir notificaciones sobre el estado del flujo de datos a su destino. Seleccione una alerta de la lista a la que suscribirse para recibir notificaciones sobre el estado del flujo de datos. Para obtener más información sobre las alertas, consulte la guía de [suscripción a alertas de destinos mediante la IU](../../ui/alerts.md).

Cuando haya terminado de proporcionar detalles para la conexión de destino, seleccione **[!UICONTROL Siguiente]**.

## Activar segmentos en este destino {#activate}

>[!IMPORTANT]
> 
>Para activar los datos, necesita el **[!UICONTROL Administrar destinos]**, **[!UICONTROL Activar destinos]**, **[!UICONTROL Ver perfiles]**, y **[!UICONTROL Ver segmentos]** [permisos de control de acceso](/help/access-control/home.md#permissions). Lea el [información general de control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Consulte [Activar datos de audiencia en destinos de exportación de segmentos de flujo continuo](../../ui/activate-segment-streaming-destinations.md) para obtener instrucciones sobre cómo activar segmentos de audiencia en este destino.

### Asignar atributos e identidades {#map}

Para enviar correctamente los datos de audiencia desde [!DNL Adobe Experience Platform] a la [!DNL Moengage] destino, debe ir a través del paso de asignación de campos.

La asignación consiste en crear un vínculo entre las [!DNL Experience Data Model] Campos de esquema (XDM) en su [!DNL Platform] y sus equivalentes correspondientes desde el destino de destino.

Para asignar correctamente los campos XDM a [!DNL Moengage] campos de destino, siga estos pasos:

En el [!UICONTROL Asignación] paso, seleccione **[!UICONTROL Casilla]**.

![Asignación de adición de destino de Moengage](../../assets/catalog/mobile-engagement/moengage/segments.png)

En el [!UICONTROL Asignación] paso, seleccione **[!UICONTROL Añadir nueva asignación]**.

![Asignación de adición de destino de Moengage](../../assets/catalog/mobile-engagement/moengage/mapping.png)

En el [!UICONTROL Campo de origen] , seleccione el botón de flecha situado junto al campo vacío.

![Asignación de origen de destino de Moengage](../../assets/catalog/mobile-engagement/moengage/mapping-source.png)

En el [!UICONTROL Seleccionar campo de origen] , puede elegir entre dos categorías de campos XDM:
* [!UICONTROL Seleccionar atributos]: utilice esta opción para asignar un campo específico del esquema XDM a [!DNL Moengage] atributo.

![Atributo de origen de asignación de destino Moengage](../../assets/catalog/mobile-engagement/moengage/mapping-attributes.png)

Elija el campo de origen y, a continuación, seleccione **[!UICONTROL Seleccionar]**.

En el [!UICONTROL Campo de destino] , seleccione el icono de asignación a la derecha del campo.

![Asignación de destino de Moengage](../../assets/catalog/mobile-engagement/moengage/mapping-target.png)

En el [!UICONTROL Seleccionar campo de destino] , puede elegir entre dos categorías de campos de destino:
* [!UICONTROL Seleccionar área de nombres de identidad]: utilice esta opción para asignar [!DNL Platform] identifique áreas de nombres en [!DNL Moengage] áreas de nombres de identidad.
* [!UICONTROL Seleccionar atributos personalizados]: utilice esta opción para asignar atributos XDM a personalizados [!DNL Moengage] atributos que definió en su [!DNL Moengage] cuenta. <br> También puede utilizar esta opción para cambiar el nombre de los atributos XDM existentes a [!DNL Moengage]. Por ejemplo, la asignación de un `lastName` Atributo XDM a un personalizado `Last_Name` atributo en [!DNL Moengage], creará el `Last_Name` atributo en [!DNL Moengage], si aún no existe, y asigne el `lastName` Atributo XDM correspondiente.

![Campos de asignación de destino de Moengage](../../assets/catalog/mobile-engagement/moengage/mapping-target-fields.png)

Elija el campo de destino y, a continuación, seleccione **[!UICONTROL Seleccionar]**.

Ahora debería ver la asignación de campos en la lista.

![Asignación de destino de Moengagement completa](../../assets/catalog/mobile-engagement/moengage/mapping-complete.png)

Para agregar más asignaciones, repita los pasos anteriores.

## Datos exportados / Validar exportación de datos {#exported-data}

Para comprobar si los datos se han exportado correctamente a [!DNL Moengage] destino, vaya al perfil de usuario de [!DNL Moengage] cuenta. Verá un atributo de usuario denominado Segmento de AEP.

![Asignación de destino de Moengagement completa](../../assets/catalog/mobile-engagement/moengage/validation.png)

## Uso de datos y gobernanza {#data-usage-governance}

Todo [!DNL Adobe Experience Platform] Los destinos de cumplen con las políticas de uso de datos al gestionar los datos. Para obtener información detallada sobre cómo [!DNL Adobe Experience Platform] aplica la gobernanza de datos, lea la [Resumen de gobernanza de datos](/help/data-governance/home.md).
