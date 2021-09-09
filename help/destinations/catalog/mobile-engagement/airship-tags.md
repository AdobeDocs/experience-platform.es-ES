---
keywords: etiquetas de aerolíneas;destino de aerolíneas
title: Conexión de etiquetas de la aeronave
description: Transfiera sin problemas los datos de audiencia de Adobe a la nave aérea como etiquetas de audiencia para segmentar dentro de la nave aérea.
exl-id: 84cf5504-f0b5-48d8-8da1-ff91ee1dc171
source-git-commit: a765f6829f08f36010e0e12a7186bf5552dfe843
workflow-type: tm+mt
source-wordcount: '685'
ht-degree: 0%

---

# [!DNL Airship Tags] connection {#airship-tags-destination}

## Información general

[!DNL Airship] es la plataforma de participación del cliente líder, que le ayuda a proporcionar mensajes omnicanal significativos y personalizados a sus usuarios en cada etapa del ciclo de vida del cliente.

Esta integración pasa los datos de segmentos de Adobe Experience Platform a [!DNL Airship] como [Etiquetas](https://docs.airship.com/guides/audience/tags/) para el objetivo o la activación.

Para obtener más información sobre [!DNL Airship], consulte los [Documentos de Airship](https://docs.airship.com).


>[!TIP]
>
>Esta página de documentación la creó el equipo de [!DNL Airship]. Para cualquier solicitud de consulta o actualización, póngase en contacto con ellos directamente en [support.airship.com](https://support.airship.com/).

## Requisitos previos

Antes de poder enviar los segmentos de Adobe Experience Platform a [!DNL Airship], debe:

* Cree un grupo de etiquetas en su proyecto [!DNL Airship].
* Genere un token al portador para la autenticación.

>[!TIP]
> 
>Cree una cuenta [!DNL Airship] a través de [este vínculo de suscripción](https://go.airship.eu/accounts/register/plan/starter/) si aún no lo ha hecho.

## Grupos de etiquetas

El concepto de segmentos en Adobe Experience Platform es similar a [Etiquetas](https://docs.airship.com/guides/audience/tags/) en Envío aéreo, con ligeras diferencias en la implementación. Esta integración asigna el estado de la pertenencia de un usuario [en un segmento de Experience Platform](../../../xdm/field-groups/profile/segmentation.md) a la presencia o no presencia de una etiqueta [!DNL Airship]. Por ejemplo, en un segmento de Platform en el que `xdm:status` cambia a `realized`, la etiqueta se agrega al canal [!DNL Airship] o al usuario asignado a este perfil. Si el `xdm:status` cambia a `exited`, la etiqueta se elimina.

Para habilitar esta integración, cree un *grupo de etiquetas* en [!DNL Airship] con el nombre `adobe-segments`.

>[!IMPORTANT]
>
>Al crear su nuevo grupo de etiquetas **No marque** el botón de opción que dice &quot;[!DNL Allow these tags to be set only from your server]&quot;. Si lo hace, la integración de las etiquetas de Adobe fallará.

Consulte [Administrar grupos de etiquetas](https://docs.airship.com/tutorials/manage-project/messaging/tag-groups) para obtener instrucciones sobre la creación del grupo de etiquetas.

## Generar token al portador

Vaya a **[!UICONTROL Settings]**&quot; **[!UICONTROL APIs &amp; Integrations]** en el [Airship dashboard](https://go.airship.com) y seleccione **[!UICONTROL Tokens]** en el menú de la izquierda.

Haga clic en **[!UICONTROL Crear token]**.

Proporcione un nombre descriptivo para el token, por ejemplo, &quot;Destino de etiquetas de Adobe&quot; y seleccione &quot;Acceso completo&quot; para la función.

Haga clic en **[!UICONTROL Crear token]** y guarde los detalles como confidenciales.

## Casos de uso

Para ayudarle a comprender mejor cómo y cuándo debe utilizar el destino [!DNL Airship Tags], estos son ejemplos de casos de uso que los clientes de Adobe Experience Platform pueden resolver utilizando este destino.

### Caso de uso número 1

Los minoristas o las plataformas de entretenimiento pueden crear perfiles de usuario en sus clientes fieles y pasar esos segmentos a [!DNL Airship] para la segmentación de mensajes en campañas móviles.

### Caso de uso n.º 2

Déclencheur mensajes uno a uno en tiempo real cuando los usuarios entran o salen de segmentos específicos dentro de Adobe Experience Platform.

Por ejemplo, un minorista configura un segmento específico de jeans en Platform. Ese minorista ahora puede enviar un déclencheur a un mensaje móvil en cuanto alguien establezca su preferencia de jeans en una marca específica.

## Conectarse al destino {#connect}

Para conectarse a este destino, siga los pasos descritos en el [tutorial de configuración de destino](../../ui/connect-destination.md).

### Parámetros de conexión {#parameters}

Mientras [configura](../../ui/connect-destination.md) este destino, debe proporcionar la siguiente información:

* **[!UICONTROL Token de portador]**: el token al portador que ha generado desde el  [!DNL Airship] panel.
* **[!UICONTROL Nombre]**: introduzca un nombre que le ayudará a identificar este destino.
* **[!UICONTROL Descripción]**: introduzca una descripción para este destino.
* **[!UICONTROL Dominio]**: seleccione un centro de datos de EE. UU. o de la UE, según el centro de  [!DNL Airship] datos que se aplique a este destino.


## Activar segmentos en este destino {#activate}

Consulte [Activar datos de audiencia en destinos de exportación de segmentos de flujo continuo](../../ui/activate-segment-streaming-destinations.md) para obtener instrucciones sobre cómo activar segmentos de audiencia en este destino.

## Consideraciones de asignación {#mapping-considerations}

[!DNL Airship] las etiquetas se pueden configurar en un canal, que representa la instancia del dispositivo, por ejemplo, iPhone, o un usuario con nombre, que asigna todos los dispositivos de un usuario a un identificador común, como un ID de cliente. Si tiene direcciones de correo electrónico de texto sin formato (sin hash) como identidad principal en el esquema, seleccione el campo de correo electrónico en **[!UICONTROL Atributos de origen]** y asigne al usuario con nombre [!DNL Airship] en la columna derecha de **[!UICONTROL Identidades de destino]**, como se muestra a continuación.

![Asignación de usuarios con nombre](../../assets/catalog/mobile-engagement/airship-tags/mapping-option-2.png)

Para identificadores que deben asignarse a un canal, es decir, un dispositivo, se debe asignar al canal adecuado en función del origen. Las siguientes imágenes muestran cómo asignar un ID de publicidad de Google a un canal [!DNL Airship] de Android.

![Conectarse a ](../../assets/catalog/mobile-engagement/airship-tags/select-source-identity.png)
![Etiquetas de Envío AéreoConectarse a ](../../assets/catalog/mobile-engagement/airship-tags/select-target-identity.png)
![Etiquetas de Envío AéreoAsignación de Canal](../../assets/catalog/mobile-engagement/airship-tags/mapping-option.png)

## Uso y gobernanza de los datos {#data-usage-governance}

Todos los destinos [!DNL Adobe Experience Platform] cumplen las políticas de uso de datos al administrar los datos. Para obtener información detallada sobre cómo [!DNL Adobe Experience Platform] aplica el control de datos, consulte [Información general sobre el control de datos](../../../data-governance/home.md).
