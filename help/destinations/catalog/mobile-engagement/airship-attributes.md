---
keywords: atributos de la aeronave;destino de la aeronave
title: Conexión de atributos de aeronave
description: Transfiera sin problemas los datos de audiencia de Adobe a la nave aérea como atributos de audiencia para la segmentación dentro de la nave aérea.
exl-id: bfc1b52f-2d68-40d6-9052-c2ee1e877961
source-git-commit: 3aac1e7c7fe838201368379da8504efc8e316e1c
workflow-type: tm+mt
source-wordcount: '726'
ht-degree: 1%

---

# (Beta) Conexión [!DNL Airship Attributes] {#airship-attributes-destination}

>[!IMPORTANT]
>
>El destino [!DNL Airship Attributes] en Adobe Experience Platform está actualmente en versión beta. La documentación y las funciones están sujetas a cambios.

## Información general {#overview}

[!DNL Airship] es la plataforma de participación del cliente líder, que le ayuda a proporcionar mensajes omnicanal significativos y personalizados a sus usuarios en cada etapa del ciclo de vida del cliente.

Esta integración pasa los datos de perfil de Adobe a [!DNL Airship] como [Atributos](https://docs.airship.com/guides/audience/attributes/) para el objetivo o la activación.

Para obtener más información sobre [!DNL Airship], consulte los [Documentos de Airship](https://docs.airship.com).

>[!TIP]
>
>Esta página de documentación la creó el equipo de [!DNL Airship]. Para cualquier solicitud de consulta o actualización, póngase en contacto con ellos directamente en [support.airship.com](https://support.airship.com/).

## Requisitos previos {#prerequisites}

Antes de poder enviar los segmentos de audiencia a [!DNL Airship], debe:

* Habilite los atributos en su proyecto [!DNL Airship].
* Genere un token al portador para la autenticación.

>[!TIP]
>
>Cree una cuenta [!DNL Airship] a través de [este vínculo de suscripción](https://go.airship.eu/accounts/register/plan/starter/) si aún no lo ha hecho.

## Habilitar atributos {#enable-attributes}

Los atributos de perfil de Adobe Experience Platform son similares a los atributos [!DNL Airship] y se pueden asignar fácilmente entre sí en Platform mediante la herramienta de asignación que se muestra más abajo en esta página.

[!DNL Airship] los proyectos tienen varios atributos predefinidos y predeterminados. Si tiene un atributo personalizado, primero debe definirlo en [!DNL Airship]. Consulte [Configuración y administración de atributos](https://docs.airship.com/tutorials/audience/attributes/) para obtener más información.

## Generar token al portador {#bearer-token}

Vaya a **[!UICONTROL Settings]**&quot; **[!UICONTROL APIs &amp; Integrations]** en el [Airship dashboard](https://go.airship.com) y seleccione **[!UICONTROL Tokens]** en el menú de la izquierda.

Haga clic en **[!UICONTROL Crear token]**.

Proporcione un nombre descriptivo para el token, por ejemplo, &quot;Destino de atributos de Adobe&quot; y seleccione &quot;Acceso completo&quot; para la función.

Haga clic en **[!UICONTROL Crear token]** y guarde los detalles como confidenciales.

## Casos de uso {#use-cases}

Para ayudarle a comprender mejor cómo y cuándo debe utilizar el destino [!DNL Airship Attributes], estos son ejemplos de casos de uso que los clientes de Adobe Experience Platform pueden resolver utilizando este destino.

### Caso de uso número 1

Aproveche los datos de perfil recopilados en Adobe Experience Platform para personalizar el mensaje y el contenido enriquecido en cualquiera de los canales de [!DNL Airship]. Por ejemplo, aproveche los datos de perfil [!DNL Experience Platform] para establecer los atributos de ubicación dentro de [!DNL Airship]. Esto permitirá que una marca de hotel muestre una imagen para la ubicación del hotel más cercana para cada usuario.

### Caso de uso n.º 2

Aproveche los atributos de Adobe Experience Platform para enriquecer aún más los perfiles [!DNL Airship] y combinarlos con datos predictivos del SDK o [!DNL Airship]. Por ejemplo, un minorista puede crear un segmento con datos de estado de fidelidad y ubicación (atributos de Platform) y [!DNL Airship] predicho que produzca datos para enviar mensajes altamente dirigidos a usuarios con el estado de fidelidad de oro que viven en Las Vegas, NV y que tienen una alta probabilidad de producir.

## Conectarse al destino {#connect}

Consulte [Activar datos de audiencia en destinos de exportación de segmentos de flujo continuo](../../ui/activate-segment-streaming-destinations.md) para obtener instrucciones sobre cómo activar segmentos de audiencia en este destino.

### Parámetros de conexión {#parameters}

Mientras [configura](../../ui/connect-destination.md) este destino, debe proporcionar la siguiente información:

* **[!UICONTROL Token de portador]**: el token al portador que ha generado desde el  [!DNL Airship] panel.
* **[!UICONTROL Nombre]**: introduzca un nombre que le ayudará a identificar este destino.
* **[!UICONTROL Descripción]**: introduzca una descripción para este destino.
* **[!UICONTROL Dominio]**: seleccione un centro de datos de EE. UU. o de la UE, según el centro de  [!DNL Airship] datos que se aplique a este destino.

## Activar segmentos en este destino {#activate}

Consulte [Activar datos de audiencia en destinos de exportación de segmentos de flujo continuo](../../ui/activate-segment-streaming-destinations.md) para obtener instrucciones sobre cómo activar segmentos de audiencia en este destino.

## Consideraciones de asignación {#mapping-considerations}

[!DNL Airship] los atributos se pueden configurar en un canal, que representa la instancia del dispositivo, por ejemplo, iPhone, o un usuario con nombre, que asigna todos los dispositivos de un usuario a un identificador común, como un ID de cliente. Si tiene direcciones de correo electrónico de texto sin formato (sin hash) como identidad principal en el esquema, seleccione el campo de correo electrónico en **[!UICONTROL Atributos de origen]** y asigne al usuario con nombre [!DNL Airship] en la columna derecha de **[!UICONTROL Identidades de destino]**, como se muestra a continuación.

![Asignación de usuarios con nombre](../../assets/catalog/mobile-engagement/airship/mapping.png)

Para identificadores que deben asignarse a un canal, es decir, un dispositivo, se debe asignar al canal adecuado en función del origen. Las siguientes imágenes muestran cómo se crean dos asignaciones:

* ID de publicidad de iOS IDFA a un [!DNL Airship] canal de iOS
* Atributo `fullName` de Adobe al atributo [!DNL Airship] &quot;Nombre completo&quot;

>[!NOTE]
>
>Utilice el nombre descriptivo que aparece en el panel [!DNL Airship] al seleccionar el campo de destino para la asignación de atributos.

**Identidad del mapa**

Seleccionar campo de origen:

![Conectar a Atributos de Envío Aéreo](../../assets/catalog/mobile-engagement/airship/select-source-identity.png)

Seleccionar campo de destino:

![Conectar a Atributos de Envío Aéreo](../../assets/catalog/mobile-engagement/airship/select-target-identity.png)

**Atributo de mapa**

Seleccionar atributo de origen:

![Seleccionar campo de origen](../../assets/catalog/mobile-engagement/airship/select-source-attributes.png)

Seleccione el atributo de destino:

![Seleccionar campo de destino](../../assets/catalog/mobile-engagement/airship/select-target-attribute.png)

Verificar asignación:

![Asignación de canales](../../assets/catalog/mobile-engagement/airship/mapping.png)


## Uso y gobernanza de los datos {#data-usage-governance}

Todos los destinos [!DNL Adobe Experience Platform] cumplen las políticas de uso de datos al administrar los datos. Para obtener información detallada sobre cómo [!DNL Adobe Experience Platform] aplica el control de datos, consulte la [Información general sobre el control de datos](../../../data-governance/home.md).
