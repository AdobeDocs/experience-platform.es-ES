---
keywords: etiquetas de aerolíneas;destino de aerolíneas
title: Conexión de etiquetas de la aeronave
description: Transfiera sin problemas los datos de audiencia de Adobe a la nave aérea como etiquetas de audiencia para segmentar dentro de la nave aérea.
exl-id: 84cf5504-f0b5-48d8-8da1-ff91ee1dc171
source-git-commit: c5d2427635d90f3a9551e2a395d01d664005e8bc
workflow-type: tm+mt
source-wordcount: '770'
ht-degree: 1%

---

# [!DNL Airship Tags] connection {#airship-tags-destination}

## Información general

[!DNL Airship] es la plataforma de participación del cliente líder, que le ayuda a proporcionar mensajes omnicanal significativos y personalizados a sus usuarios en cada etapa del ciclo de vida del cliente.

Esta integración transfiere los datos de segmentos de Adobe Experience Platform a [!DNL Airship] como [Etiquetas](https://docs.airship.com/guides/audience/tags/) para objetivos o activaciones.

Para obtener más información sobre [!DNL Airship], consulte la [Documentos de Airship](https://docs.airship.com).


>[!TIP]
>
>Esta página de documentación la creó el [!DNL Airship] equipo. Para cualquier consulta o solicitud de actualización, póngase en contacto con ellos directamente en [support.airship.com](https://support.airship.com/).

## Requisitos previos

Antes de poder enviar los segmentos de Adobe Experience Platform a [!DNL Airship], debe:

* Cree un grupo de etiquetas en su [!DNL Airship] proyecto.
* Genere un token al portador para la autenticación.

>[!TIP]
> 
>Cree un [!DNL Airship] cuenta mediante [este vínculo de suscripción](https://go.airship.eu/accounts/register/plan/starter/) si aún no lo ha hecho.

## Tipo de exportación y frecuencia {#export-type-frequency}

Consulte la tabla siguiente para obtener información sobre el tipo y la frecuencia de exportación de destino.

| Elemento | Tipo | Notas |
---------|----------|---------|
| Tipo de exportación | **[!UICONTROL Exportación de segmentos]** | Está exportando todos los miembros de un segmento (audiencia) con los identificadores utilizados en el destino de Etiquetas de envío aéreo. |
| Frecuencia de exportación | **[!UICONTROL Transmisión]** | Los destinos de flujo continuo son conexiones basadas en API &quot;siempre activadas&quot;. Tan pronto como un perfil se actualiza en el Experience Platform en función de la evaluación de segmentos, el conector envía la actualización descendente a la plataforma de destino. Más información sobre [destinos de flujo continuo](/help/destinations/destination-types.md#streaming-destinations). |

{style=&quot;table-layout:auto&quot;}

## Grupos de etiquetas

El concepto de segmentos en Adobe Experience Platform es similar a [Etiquetas](https://docs.airship.com/guides/audience/tags/) en Airship, con ligeras diferencias en la implementación. Esta integración asigna el estado de la [pertenencia a un segmento de Experience Platform](../../../xdm/field-groups/profile/segmentation.md) a la presencia o no presencia de un [!DNL Airship] etiqueta. Por ejemplo, en un segmento de Platform en el que la variable `xdm:status` cambia a `realized`, la etiqueta se agrega al [!DNL Airship] canal o usuario con nombre al que se asigna este perfil. Si la variable `xdm:status` cambia a `exited`, se elimina la etiqueta .

Para habilitar esta integración, cree un *grupo de etiquetas* en [!DNL Airship] named `adobe-segments`.

>[!IMPORTANT]
>
>Al crear el nuevo grupo de etiquetas **No comprobar** el botón de opción que dice &quot;[!DNL Allow these tags to be set only from your server]&quot;. Si lo hace, la integración de las etiquetas de Adobe fallará.

Consulte [Administrar grupos de etiquetas](https://docs.airship.com/tutorials/manage-project/messaging/tag-groups) para obtener instrucciones sobre la creación del grupo de etiquetas.

## Generar token al portador

Vaya a **[!UICONTROL Configuración]** &quot; **[!UICONTROL API e integraciones]** en el [Panel de la aeronave](https://go.airship.com) y seleccione **[!UICONTROL Tokens]** en el menú de la izquierda.

Haga clic en **[!UICONTROL Crear token]**.

Proporcione un nombre descriptivo para el token, por ejemplo, &quot;Destino de etiquetas de Adobe&quot; y seleccione &quot;Acceso completo&quot; para la función.

Haga clic en **[!UICONTROL Crear token]** y guarde los detalles como confidenciales.

## Casos de uso

Para ayudarle a comprender mejor cómo y cuándo debe usar la variable [!DNL Airship Tags] destino, aquí hay ejemplos de casos de uso que los clientes de Adobe Experience Platform pueden resolver utilizando este destino.

### Caso de uso número 1

Los minoristas o las plataformas de entretenimiento pueden crear perfiles de usuario en sus clientes fieles y pasar esos segmentos a [!DNL Airship] para la segmentación de mensajes en campañas móviles.

### Caso de uso n.º 2

Déclencheur mensajes uno a uno en tiempo real cuando los usuarios entran o salen de segmentos específicos dentro de Adobe Experience Platform.

Por ejemplo, un minorista configura un segmento específico de jeans en Platform. Ese minorista ahora puede enviar un déclencheur a un mensaje móvil en cuanto alguien establezca su preferencia de jeans en una marca específica.

## Conectarse al destino {#connect}

Para conectarse a este destino, siga los pasos descritos en la sección [tutorial de configuración de destino](../../ui/connect-destination.md).

### Parámetros de conexión {#parameters}

While [configuración](../../ui/connect-destination.md) Para este destino, debe proporcionar la siguiente información:

* **[!UICONTROL Token portador]**: el token de portador que generó a partir de la variable [!DNL Airship] tablero.
* **[!UICONTROL Nombre]**: introduzca un nombre que le ayudará a identificar este destino.
* **[!UICONTROL Descripción]**: introduzca una descripción para este destino.
* **[!UICONTROL Dominio]**: seleccione un centro de datos de EE. UU. o de la UE, en función de cuál [!DNL Airship] el centro de datos se aplica a este destino.


## Activar segmentos en este destino {#activate}

Consulte [Activar datos de audiencia en destinos de exportación de segmentos de flujo continuo](../../ui/activate-segment-streaming-destinations.md) para obtener instrucciones sobre la activación de segmentos de audiencia en este destino.

## Consideraciones de asignación {#mapping-considerations}

[!DNL Airship] las etiquetas se pueden configurar en un canal, que representa la instancia del dispositivo, por ejemplo, iPhone, o un usuario con nombre, que asigna todos los dispositivos de un usuario a un identificador común, como un ID de cliente. Si tiene direcciones de correo electrónico de texto sin formato (sin hash) como identidad principal en el esquema, seleccione el campo de correo electrónico en el **[!UICONTROL Atributos de origen]** y asigne al [!DNL Airship] usuario con nombre en la columna derecha debajo de **[!UICONTROL Identidades de Target]**, como se muestra a continuación.

![Asignación de usuarios con nombre](../../assets/catalog/mobile-engagement/airship-tags/mapping-option-2.png)

Para identificadores que deben asignarse a un canal, es decir, un dispositivo, se debe asignar al canal adecuado en función del origen. Las siguientes imágenes muestran cómo asignar un ID de publicidad de Google a un [!DNL Airship] Canal de Android.

![Conectarse a las etiquetas de Airship](../../assets/catalog/mobile-engagement/airship-tags/select-source-identity.png)
![Conectarse a las etiquetas de Airship](../../assets/catalog/mobile-engagement/airship-tags/select-target-identity.png)
![Asignación de canales](../../assets/catalog/mobile-engagement/airship-tags/mapping-option.png)

## Uso y gobernanza de los datos {#data-usage-governance}

Todo [!DNL Adobe Experience Platform] Los destinos de cumplen las políticas de uso de datos al administrar los datos. Para obtener información detallada sobre cómo [!DNL Adobe Experience Platform] exige el control de datos, consulte [Información general sobre la administración de datos](../../../data-governance/home.md).
