---
keywords: etiquetas de dirigible;destino de dirigible
title: Conexión de etiquetas de dirigible
description: Transfiera sin problemas los datos de audiencias de Adobe al dirigible como etiquetas de audiencia para segmentar dentro del dirigible.
exl-id: 84cf5504-f0b5-48d8-8da1-ff91ee1dc171
source-git-commit: fd2019feb25b540612a278cbea5bf5efafe284dc
workflow-type: tm+mt
source-wordcount: '944'
ht-degree: 0%

---

# [!DNL Airship Tags] conexión {#airship-tags-destination}

## Información general

[!DNL Airship] es la plataforma líder de participación del cliente, que le ayuda a proporcionar mensajes omnicanal significativos y personalizados a sus usuarios en cada fase del ciclo de vida del cliente.

Esta integración pasa los datos de segmentos de Adobe Experience Platform a [!DNL Airship] as [Etiquetas](https://docs.airship.com/guides/audience/tags/) para segmentar o activar.

Para obtener más información acerca de [!DNL Airship], consulte la [Documentos de dirigibles](https://docs.airship.com).


>[!TIP]
>
>Esta página de documentación fue creada por el [!DNL Airship] equipo. Para cualquier consulta o solicitud de actualización, póngase en contacto directamente con ellos en [support.airship.com](https://support.airship.com/).

## Requisitos previos

Antes de poder enviar los segmentos de Adobe Experience Platform a [!DNL Airship], debe:

* Cree un grupo de etiquetas en su [!DNL Airship] proyecto.
* Genere un token de portador para la autenticación.

>[!TIP]
> 
>Crear un [!DNL Airship] cuenta mediante [este vínculo de suscripción](https://go.airship.eu/accounts/register/plan/starter/) si aún no lo ha hecho.

## Tipo y frecuencia de exportación {#export-type-frequency}

Consulte la tabla siguiente para obtener información sobre el tipo y la frecuencia de exportación de destino.

| Elemento | Tipo | Notas |
---------|----------|---------|
| Tipo de exportación | **[!UICONTROL Exportación de segmentos]** | Va a exportar todos los miembros de un segmento (audiencia) con los identificadores utilizados en el destino Etiquetas de dirigibles. |
| Frecuencia de exportación | **[!UICONTROL Transmisión]** | Los destinos de streaming son conexiones basadas en API &quot;siempre activadas&quot;. Tan pronto como se actualiza un perfil en Experience Platform según la evaluación de segmentos, el conector envía la actualización de forma descendente a la plataforma de destino. Más información sobre [destinos de streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Grupos de etiquetas

El concepto de segmentos en Adobe Experience Platform es similar al siguiente [Etiquetas](https://docs.airship.com/guides/audience/tags/) en Aeronave, con ligeras diferencias de implementación. Esta integración asigna el estado del de un usuario de [pertenencia a un segmento de Experience Platform](../../../xdm/field-groups/profile/segmentation.md) a la presencia o no presencia de un [!DNL Airship] etiqueta. Por ejemplo, en un segmento de Platform donde la variable `xdm:status` cambios en `realized`, la etiqueta se añade a [!DNL Airship] canal o usuario con nombre al que está asignado este perfil. Si la variable `xdm:status` cambios en `exited`, se eliminará la etiqueta.

Para habilitar esta integración, cree un *grupo de etiquetas* in [!DNL Airship] nombrado `adobe-segments`.

>[!IMPORTANT]
>
>Al crear el nuevo grupo de etiquetas **No comprobar** el botón de opción que dice &quot;[!DNL Allow these tags to be set only from your server]&quot;. Al hacerlo, la integración de etiquetas de Adobe falla.

Consulte [Administrar grupos de etiquetas](https://docs.airship.com/tutorials/manage-project/messaging/tag-groups) para obtener instrucciones sobre cómo crear el grupo de etiquetas.

## Generar token de portador

Ir a **[!UICONTROL Configuración]** &quot; **[!UICONTROL API e integraciones]** en el [Tablero del dirigible](https://go.airship.com) y seleccione **[!UICONTROL Tokens]** en el menú de la izquierda.

Clic **[!UICONTROL Crear token]**.

Proporcione un nombre descriptivo para el token, por ejemplo, &quot;Adobe Tags Destination&quot; y seleccione &quot;Todos los accesos&quot; para la función.

Clic **[!UICONTROL Crear token]** y guarde los detalles como confidenciales.

## Casos de uso

Para ayudarle a comprender mejor cómo y cuándo debe utilizar el [!DNL Airship Tags] Destino. Estos son ejemplos de casos de uso que los clientes de Adobe Experience Platform pueden solucionar mediante este destino.

### Caso de uso #1

Los minoristas o las plataformas de entretenimiento pueden crear perfiles de usuario en sus clientes fieles y pasar esos segmentos a [!DNL Airship] para la segmentación de mensajes en campañas móviles.

### Caso de uso #2

Almacene en déclencheur mensajes uno a uno en tiempo real cuando los usuarios entren o salgan de segmentos específicos dentro de Adobe Experience Platform.

Por ejemplo, un minorista configura un segmento específico de marca de jeans en Platform. Ese minorista ahora puede almacenar en déclencheur un mensaje móvil en cuanto alguien establece su preferencia de pantalones vaqueros para una marca específica.

## Conectar con el destino {#connect}

>[!IMPORTANT]
> 
>Para conectarse al destino, necesita el **[!UICONTROL Administrar destinos]** [permiso de control de acceso](/help/access-control/home.md#permissions). Lea el [información general de control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Para conectarse a este destino, siga los pasos descritos en la sección [tutorial de configuración de destino](../../ui/connect-destination.md). En el flujo de trabajo de configuración de destino, rellene los campos enumerados en las dos secciones siguientes.

### Autenticar en el destino {#authenticate}

Para autenticarse en el destino, rellene los campos obligatorios y seleccione **[!UICONTROL Conectar con destino]**.

* **[!UICONTROL Token de portador]**: el token de portador que generó a partir del [!DNL Airship] panel.

### Rellenar detalles de destino {#destination-details}

Para configurar los detalles del destino, rellene los campos obligatorios y opcionales a continuación. Un asterisco junto a un campo en la interfaz de usuario indica que el campo es obligatorio.

* **[!UICONTROL Nombre]**: introduzca un nombre que le ayude a identificar este destino.
* **[!UICONTROL Descripción]**: introduzca una descripción para este destino.
* **[!UICONTROL Dominio]**: seleccione un centro de datos de EE. UU. o de la UE, según cuál [!DNL Airship] el centro de datos se aplica a este destino.

### Habilitar alertas {#enable-alerts}

Puede activar alertas para recibir notificaciones sobre el estado del flujo de datos a su destino. Seleccione una alerta de la lista a la que suscribirse para recibir notificaciones sobre el estado del flujo de datos. Para obtener más información sobre las alertas, consulte la guía de [suscripción a alertas de destinos mediante la IU](../../ui/alerts.md).

Cuando haya terminado de proporcionar detalles para la conexión de destino, seleccione **[!UICONTROL Siguiente]**.

## Activar segmentos en este destino {#activate}

>[!IMPORTANT]
> 
>Para activar los datos, necesita el **[!UICONTROL Administrar destinos]**, **[!UICONTROL Activar destinos]**, **[!UICONTROL Ver perfiles]**, y **[!UICONTROL Ver segmentos]** [permisos de control de acceso](/help/access-control/home.md#permissions). Lea el [información general de control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Consulte [Activar datos de audiencia en destinos de exportación de segmentos de flujo continuo](../../ui/activate-segment-streaming-destinations.md) para obtener instrucciones sobre cómo activar segmentos de audiencia en este destino.

## Consideraciones de asignación {#mapping-considerations}

[!DNL Airship] las etiquetas se pueden establecer en un canal que represente una instancia de dispositivo (por ejemplo, iPhone) o un usuario designado que asigne todos los dispositivos de un usuario a un identificador común (por ejemplo, un ID de cliente). Si tiene direcciones de correo electrónico de texto sin formato (sin hash) como identidad principal en el esquema, seleccione el campo de correo electrónico en su **[!UICONTROL Atributos de origen]** y asigne a [!DNL Airship] usuario designado en la columna derecha debajo de **[!UICONTROL Identidades de destino]**, como se muestra a continuación.

![Asignación de usuarios con nombre](../../assets/catalog/mobile-engagement/airship-tags/mapping-option-2.png)

Para los identificadores que deben asignarse a un canal, es decir, a un dispositivo, asígnelos al canal adecuado en función del origen. Las siguientes imágenes muestran cómo se asigna un ID de publicidad de Google a un [!DNL Airship] Canal de Android.

![Conectar con etiquetas de dirigible](../../assets/catalog/mobile-engagement/airship-tags/select-source-identity.png)
![Conectar con etiquetas de dirigible](../../assets/catalog/mobile-engagement/airship-tags/select-target-identity.png)
![Asignación de canales](../../assets/catalog/mobile-engagement/airship-tags/mapping-option.png)

## Uso de datos y gobernanza {#data-usage-governance}

Todo [!DNL Adobe Experience Platform] Los destinos de cumplen con las políticas de uso de datos al gestionar los datos. Para obtener información detallada sobre cómo [!DNL Adobe Experience Platform] aplica la gobernanza de datos, consulte [Resumen de gobernanza de datos](../../../data-governance/home.md).
