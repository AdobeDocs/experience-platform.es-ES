---
keywords: etiquetas de dirigible;destino de dirigible
title: Conexión de etiquetas de dirigible
description: Pase sin problemas los datos de audiencia de Adobe al dirigible como etiquetas de audiencia para segmentar dentro del dirigible.
exl-id: 84cf5504-f0b5-48d8-8da1-ff91ee1dc171
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '972'
ht-degree: 2%

---

# [!DNL Airship Tags] conexión {#airship-tags-destination}

## Información general

[!DNL Airship] es la plataforma de participación del cliente líder, que le ayuda a entregar mensajes omnicanal significativos y personalizados a sus usuarios en cada etapa del ciclo de vida del cliente.

Esta integración pasa los datos de audiencia de Adobe Experience Platform a [!DNL Airship] como [Etiquetas](https://docs.airship.com/guides/audience/tags/) para direccionamiento o activación.

Para obtener más información sobre [!DNL Airship], consulte [Documentos de la aeronave](https://docs.airship.com).


>[!TIP]
>
>El equipo [!DNL Airship] crea y mantiene este conector de destino y esta página de documentación. Para cualquier consulta o solicitud de actualización, comuníquese directamente con ellos en [support.airship.com](https://support.airship.com/).

## Requisitos previos

Para poder enviar las audiencias de Adobe Experience Platform a [!DNL Airship], debe:

* Cree un grupo de etiquetas en su proyecto [!DNL Airship].
* Genere un token de portador para la autenticación.

>[!TIP]
> 
>Cree una cuenta de [!DNL Airship] a través de [este vínculo de suscripción](https://go.airship.eu/accounts/register/plan/starter/) si aún no lo ha hecho.

## Audiencias compatibles {#supported-audiences}

Esta sección describe qué tipos de audiencias puede exportar a este destino.

| Origen de audiencia | Admitido | Descripción |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Audiencias generadas a través del [servicio de segmentación](../../../segmentation/home.md) de Experience Platform. |
| Cargas personalizadas | ✓ | Las audiencias [importadas](../../../segmentation/ui/audience-portal.md#import-audience) en Experience Platform desde archivos CSV. |

{style="table-layout:auto"}

## Tipo y frecuencia de exportación {#export-type-frequency}

Consulte la tabla siguiente para obtener información sobre el tipo y la frecuencia de exportación de destino.

| Elemento | Tipo | Notas |
---------|----------|---------|
| Tipo de exportación | **[!UICONTROL Exportación de audiencia]** | Va a exportar todos los miembros de una audiencia con los identificadores utilizados en el destino de Etiquetas de dirigibles. |
| Frecuencia de exportación | **[!UICONTROL Transmisión]** | Los destinos de streaming son conexiones basadas en API &quot;siempre activadas&quot;. Tan pronto como se actualiza un perfil en Experience Platform basado en la evaluación de audiencias, el conector envía la actualización de forma descendente a la plataforma de destino. Más información sobre [destinos de streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Grupos de etiquetas

El concepto de audiencias en Adobe Experience Platform es similar a [Etiquetas](https://docs.airship.com/guides/audience/tags/) en Airship, con ligeras diferencias en la implementación. Esta integración asigna el estado de la [pertenencia de un usuario a un segmento de Experience Platform](../../../xdm/field-groups/profile/segmentation.md) a la presencia o no presencia de una etiqueta [!DNL Airship]. Por ejemplo, en una audiencia de Experience Platform donde `xdm:status` cambia a `realized`, la etiqueta se agrega al canal [!DNL Airship] o al usuario con nombre al que se asigna este perfil. Si `xdm:status` cambia a `exited`, se quita la etiqueta.

Para habilitar esta integración, cree un *grupo de etiquetas* en [!DNL Airship] denominado `adobe-segments`.

>[!IMPORTANT]
>
>Al crear su nuevo grupo de etiquetas **No verifique** el botón de opción que dice &quot;[!DNL Allow these tags to be set only from your server]&quot;. Al hacerlo, la integración de etiquetas de Adobe falla.

Consulte [Administrar grupos de etiquetas](https://docs.airship.com/tutorials/manage-project/messaging/tag-groups) para obtener instrucciones sobre cómo crear el grupo de etiquetas.

## Generar token de portador

Vaya a **[!UICONTROL Configuración]**&quot; **[!UICONTROL API e integraciones]** en el [tablero del dirigible](https://go.airship.com) y seleccione **[!UICONTROL Tokens]** en el menú de la izquierda.

Haga clic en **[!UICONTROL Crear token]**.

Proporcione un nombre descriptivo para el token, por ejemplo, &quot;Destino de etiquetas de Adobe&quot;, y seleccione &quot;Todo el acceso&quot; para el rol.

Haga clic en **[!UICONTROL Crear token]** y guarde los detalles como confidenciales.

## Casos de uso

Para ayudarle a comprender mejor cómo y cuándo debe utilizar el destino [!DNL Airship Tags], aquí hay casos de uso de ejemplo que los clientes de Adobe Experience Platform pueden solucionar mediante este destino.

### Caso de uso #1

Los minoristas o las plataformas de entretenimiento pueden crear perfiles de usuario en sus clientes fieles y pasar esas audiencias a [!DNL Airship] para la segmentación de mensajes en campañas móviles.

### Caso de uso #2

Almacene en déclencheur mensajes uno a uno en tiempo real cuando los usuarios entren o salgan de audiencias específicas dentro de Adobe Experience Platform.

Por ejemplo, un retailer configura una audiencia específica de marca de jeans en Experience Platform. Que retailer ahora puede almacenar en déclencheur un mensaje móvil en cuanto alguien establece su preferencia de vaqueros para una marca específica.

## Conexión al destino {#connect}

>[!IMPORTANT]
> 
>Para conectarse al destino, necesita los **[[!UICONTROL permisos de control de acceso]](/help/access-control/home.md#permissions) de Ver destinos&rbrack;** y **[!UICONTROL Administrar destinos]**&lbrack;5&rbrace;. Lea la [descripción general del control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Para conectarse a este destino, siga los pasos descritos en el [tutorial de configuración de destino](../../ui/connect-destination.md). En el flujo de trabajo de configuración de destino, rellene los campos enumerados en las dos secciones siguientes.

### Autenticarse en el destino {#authenticate}

Para autenticarse en el destino, rellene los campos obligatorios y seleccione **[!UICONTROL Conectar con destino]**.

* **[!UICONTROL Token de portador]**: el token de portador que generó desde el panel [!DNL Airship].

### Rellenar detalles de destino {#destination-details}

Para configurar los detalles del destino, rellene los campos obligatorios y opcionales a continuación. Un asterisco junto a un campo en la interfaz de usuario indica que el campo es obligatorio.

* **[!UICONTROL Nombre]**: escriba un nombre que le ayude a identificar este destino.
* **[!UICONTROL Descripción]**: escriba una descripción para este destino.
* **[!UICONTROL Dominio]**: seleccione un centro de datos de EE. UU. o de la UE, según el centro de datos [!DNL Airship] que se aplique a este destino.

### Habilitar alertas {#enable-alerts}

Puede activar alertas para recibir notificaciones sobre el estado del flujo de datos a su destino. Seleccione una alerta de la lista a la que suscribirse para recibir notificaciones sobre el estado del flujo de datos. Para obtener más información sobre las alertas, consulte la guía sobre [suscripción a alertas de destinos mediante la interfaz de usuario](../../ui/alerts.md).

Cuando termine de proporcionar detalles para la conexión de destino, seleccione **[!UICONTROL Siguiente]**.

## Activar públicos en este destino {#activate}

>[!IMPORTANT]
> 
>Para activar los datos, necesita los **[!UICONTROL permisos de control de acceso]**, **[!UICONTROL Activar destinos]**, **[!UICONTROL Ver perfiles]** y **[!UICONTROL Ver segmentos]**&#x200B;[para ](/help/access-control/home.md#permissions). Lea la [descripción general del control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Consulte [Activar datos de audiencia en destinos de exportación de audiencia de streaming](../../ui/activate-segment-streaming-destinations.md) para obtener instrucciones sobre cómo activar audiencias en este destino.

## Consideraciones de asignación {#mapping-considerations}

Las etiquetas [!DNL Airship] se pueden establecer en un canal que represente una instancia de dispositivo (por ejemplo, iPhone) o un usuario designado que asigne todos los dispositivos de un usuario a un identificador común (por ejemplo, un ID de cliente). Si tiene direcciones de correo electrónico de texto sin formato (sin hash) como identidad principal en el esquema, seleccione el campo de correo electrónico en sus **[!UICONTROL Atributos de Source]** y asígnelo al usuario con nombre [!DNL Airship] en la columna derecha debajo de **[!UICONTROL Identidades de destino]**, como se muestra a continuación.

![Asignación de usuarios con nombre](../../assets/catalog/mobile-engagement/airship-tags/mapping-option-2.png)

Para los identificadores que deben asignarse a un canal, es decir, a un dispositivo, asígnelos al canal adecuado en función del origen. Las siguientes imágenes muestran cómo asignar un ID de Advertising de Google a un canal de Android [!DNL Airship].

![Conectar con etiquetas de dirigible](../../assets/catalog/mobile-engagement/airship-tags/select-source-identity.png)
![Conectar con etiquetas de dirigible](../../assets/catalog/mobile-engagement/airship-tags/select-target-identity.png)
![Asignación de canales](../../assets/catalog/mobile-engagement/airship-tags/mapping-option.png)

## Uso de datos y gobernanza {#data-usage-governance}

Todos los destinos de [!DNL Adobe Experience Platform] cumplen con las políticas de uso de datos al administrar los datos. Para obtener información detallada sobre cómo [!DNL Adobe Experience Platform] aplica el control de datos, consulte [Resumen de control de datos](../../../data-governance/home.md).
