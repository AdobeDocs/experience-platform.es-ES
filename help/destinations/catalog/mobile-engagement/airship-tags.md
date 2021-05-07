---
keywords: etiquetas de aerolíneas;destino de aerolíneas
title: Conexión de etiquetas de la aeronave
description: Transfiera sin problemas los datos de audiencia de Adobe a la nave aérea como etiquetas de audiencia para segmentar dentro de la nave aérea.
exl-id: 84cf5504-f0b5-48d8-8da1-ff91ee1dc171
translation-type: tm+mt
source-git-commit: ab0798851e5f2b174d9f4241ad64ac8afa20a938
workflow-type: tm+mt
source-wordcount: '1123'
ht-degree: 1%

---

# (Beta) Conexión [!DNL Airship Tags] {#airship-tags-destination}

>[!IMPORTANT]
>
>El destino [!DNL Airship Tags] en Adobe Experience Platform está actualmente en versión beta. La documentación y las funciones están sujetas a cambios.

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

Vaya a **[!UICONTROL Settings]**&quot; **[!UICONTROL APIs & Integrations]** en el [Airship dashboard](https://go.airship.com) y seleccione **[!UICONTROL Tokens]** en el menú de la izquierda.

Haga clic en **[!UICONTROL Create Token]**.

Proporcione un nombre descriptivo para el token, por ejemplo, &quot;Destino de etiquetas de Adobe&quot; y seleccione &quot;Acceso completo&quot; para la función.

Haga clic en **[!UICONTROL Create Token]** y guarde los detalles como confidenciales.

## Casos de uso

Para ayudarle a comprender mejor cómo y cuándo debe utilizar el destino [!DNL Airship Tags], estos son ejemplos de casos de uso que los clientes de Adobe Experience Platform pueden resolver utilizando este destino.

### Caso de uso número 1

Los minoristas o las plataformas de entretenimiento pueden crear perfiles de usuario en sus clientes fieles y pasar esos segmentos a [!DNL Airship] para la segmentación de mensajes en campañas móviles.

### Caso de uso n.º 2

Déclencheur mensajes uno a uno en tiempo real cuando los usuarios entran o salen de segmentos específicos dentro de Adobe Experience Platform.

Por ejemplo, un minorista configura un segmento específico de jeans en Platform. Ese minorista ahora puede enviar un déclencheur a un mensaje móvil en cuanto alguien establezca su preferencia de jeans en una marca específica.

## Conectarse a [!DNL Airship Tags] {#connect-airship-tags}

En **[!UICONTROL Destinations]** > **[!UICONTROL Catalog]**, desplácese hasta la categoría **[!UICONTROL Mobile Engagement]**. Seleccione **[!DNL Airship Tags]** y luego seleccione **[!UICONTROL Configure]**.

>[!NOTE]
>
>Si ya existe una conexión con este destino, puede ver un botón **[!UICONTROL Activate]** en la tarjeta de destino. Para obtener más información sobre la diferencia entre **[!UICONTROL Activate]** y **[!UICONTROL Configure]**, consulte la sección [Catalog](../../ui/destinations-workspace.md#catalog) de la documentación del espacio de trabajo de destino.

![Conectarse a las etiquetas de Airship](../../assets/catalog/mobile-engagement/airship-tags/catalog.png)

En el paso **Account**, si anteriormente había configurado una conexión con su destino [!DNL Airship Tags], seleccione **[!UICONTROL Existing Account]** y la conexión existente. O bien, puede seleccionar **[!UICONTROL New Account]** para configurar una nueva conexión a [!DNL Airship Tags]. Seleccione **[!UICONTROL Connect to destination]** para conectar Adobe Experience Platform al proyecto [!DNL Airship] utilizando el token al portador que generó desde el panel [!DNL Airship].

>[!NOTE]
>
>Adobe Experience Platform admite la validación de credenciales en el proceso de autenticación y muestra un mensaje de error si introduce credenciales incorrectas en su cuenta [!DNL Airship]. Esto garantiza que no complete el flujo de trabajo con credenciales incorrectas.

![Conectarse a las etiquetas de Airship](../../assets/catalog/mobile-engagement/airship-tags/connect-account.png)

Una vez confirmadas las credenciales y que Adobe Experience Platform esté conectado al proyecto [!DNL Airship], puede seleccionar **[!UICONTROL Next]** para continuar con el paso **[!UICONTROL Setup]**.

En el paso **[!UICONTROL Authentication]**, introduzca un **[!UICONTROL Name]** y un **[!UICONTROL Description]** para el flujo de activación.

Además, en este paso, puede seleccionar un centro de datos de EE. UU. o de la UE, según el [!DNL Airship] centro de datos que se aplique a este destino. Finalmente, seleccione uno o más **[!UICONTROL Marketing Actions]** para los que se exportarán datos al destino. Puede seleccionar entre las acciones de marketing definidas por el Adobe o puede crear las suyas. Para obtener más información sobre las acciones de marketing, consulte [Información general sobre las políticas de uso de datos](../../../data-governance/policies/overview.md).

Seleccione **[!UICONTROL Create Destination]** después de rellenar los campos anteriores.

![Conectarse a las etiquetas de Airship](../../assets/catalog/mobile-engagement/airship-tags/select-domain.png)

Se ha creado el destino. Puede seleccionar **[!UICONTROL Save & Exit]** si desea activar segmentos más adelante o puede seleccionar **[!UICONTROL Next]** para continuar con el flujo de trabajo y seleccionar segmentos para activarlos. En cualquier caso, consulte la siguiente sección, [Activar segmentos](#activate-segments), para el resto del flujo de trabajo.

## Activar segmentos {#activate-segments}

Para activar segmentos en [!DNL Airship Tags], siga los pasos a continuación:

En **[!UICONTROL Destinations > Browse]**, seleccione el destino [!DNL Airship Tags] donde desea activar los segmentos.

![activate-flow](../../assets/catalog/mobile-engagement/airship-tags/browse.png)

Haga clic en el nombre del destino. Esto le lleva al flujo de activación.

Tenga en cuenta que si ya existe un flujo de activación para un destino, puede ver los segmentos que se están enviando actualmente al destino. Seleccione **[!UICONTROL Edit activation]** en el carril derecho y siga los pasos a continuación para modificar los detalles de activación.

![activate-flow](../../assets/catalog/mobile-engagement/airship-tags/activate.png)

Seleccione **[!UICONTROL Activate]**. En el flujo de trabajo **[!UICONTROL Activate destination]** , en la página **[!UICONTROL Select Segments]**, seleccione qué segmentos desea enviar a [!DNL Airship Tags].

![segmentos a destino](../../assets/catalog/mobile-engagement/airship-tags/select-segments.png)

En el paso **[!UICONTROL Mapping]**, seleccione qué atributos e identidades del esquema [XDM](../../../xdm/home.md) se asignarán al esquema de destino. Seleccione **[!UICONTROL Add new mapping]** para examinar el esquema y asignarlo a la identidad de destino correspondiente.

![pantalla inicial de asignación de identidad](../../assets/catalog/mobile-engagement/airship-tags/identity-mapping.png)

[!DNL Airship] las etiquetas se pueden configurar en un canal, que representa la instancia del dispositivo, por ejemplo, iPhone, o un usuario con nombre, que asigna todos los dispositivos de un usuario a un identificador común, como un ID de cliente. Si tiene direcciones de correo electrónico de texto sin formato (sin hash) como identidad principal en el esquema, seleccione el campo de correo electrónico en **[!UICONTROL Source Attributes]** y asigne al usuario [!DNL Airship] con nombre en la columna derecha de **[!UICONTROL Target Identities]**, como se muestra a continuación.

![Asignación de usuarios con nombre](../../assets/catalog/mobile-engagement/airship-tags/mapping-option-2.png)

Para identificadores que deben asignarse a un canal, es decir, un dispositivo, se debe asignar al canal adecuado en función del origen. Las siguientes imágenes muestran cómo asignar un ID de publicidad de Google a un canal [!DNL Airship] de Android.

![Conectarse a ](../../assets/catalog/mobile-engagement/airship-tags/select-source-identity.png)
![Etiquetas de Envío AéreoConectarse a ](../../assets/catalog/mobile-engagement/airship-tags/select-target-identity.png)
![Etiquetas de Envío AéreoAsignación de Canal](../../assets/catalog/mobile-engagement/airship-tags/mapping-option.png)

En la página **[!UICONTROL Segment schedule]**, la programación está deshabilitada. Haga clic en **[!UICONTROL Next]** para continuar con el paso de revisión.

En la página **[!UICONTROL Review]** puede ver un resumen de su selección. Seleccione **[!UICONTROL Cancel]** para desglosar el flujo, **[!UICONTROL Back]** para modificar la configuración o **[!UICONTROL Finish]** para confirmar la selección y empezar a enviar datos al destino.

>[!IMPORTANT]
>
>En este paso, Adobe Experience Platform comprueba las infracciones de la directiva de uso de datos. A continuación se muestra un ejemplo en el que se infringe una política. No puede completar el flujo de trabajo de activación de segmentos hasta que no haya resuelto la infracción. Para obtener información sobre cómo resolver infracciones de políticas, consulte [Aplicación de políticas](../../../data-governance/enforcement/auto-enforcement.md) en la sección de documentación de control de datos.

![confirm-selection](../../assets/common/data-policy-violation.png)

Si no se ha detectado ninguna infracción de directiva, seleccione **[!UICONTROL Finish]** para confirmar la selección y empezar a enviar datos al destino.

![confirm-selection](../../assets/catalog/mobile-engagement/airship-tags/review.png)


## Administración y uso de datos {#data-usage-governance}

Todos los destinos [!DNL Adobe Experience Platform] cumplen las políticas de uso de datos al administrar los datos. Para obtener información detallada sobre cómo [!DNL Adobe Experience Platform] aplica el control de datos, consulte [Información general sobre el control de datos](../../../data-governance/home.md).
