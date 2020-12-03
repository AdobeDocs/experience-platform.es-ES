---
keywords: airship tags;airship destination
title: Destino de las etiquetas de la aeronave
seo-title: Destino de las etiquetas de la aeronave
description: Pasar sin problemas los datos de Audiencia de Adobe a la aeronave como etiquetas de Audiencia para objetivos dentro de la aeronave.
seo-description: Pasar sin problemas los datos de Audiencia de Adobe a la aeronave como etiquetas de Audiencia para objetivos dentro de la aeronave.
translation-type: tm+mt
source-git-commit: 0bb1622895b1e0f97fc47b5c61d456bc369746c8
workflow-type: tm+mt
source-wordcount: '1228'
ht-degree: 1%

---


# (Beta) [!DNL Airship Tags] destino {#airship-tags-destination}

>[!IMPORTANT]
>
>El [!DNL Airship Tags] destino de Adobe Experience Platform está actualmente en fase beta. La documentación y las funciones están sujetas a cambios.

## Información general

[!DNL Airship] es la plataforma líder de compromiso con el cliente, que le ayuda a enviar mensajes de canal omnicho significativos y personalizados a sus usuarios en cada etapa del ciclo vital del cliente.

Esta integración pasa los datos de segmentos de Adobe Experience Platform a [!DNL Airship] como [etiquetas](https://docs.airship.com/guides/audience/tags/) para direccionamiento o activación.

Para obtener más información sobre [!DNL Airship], consulte los documentos [de Airship](https://docs.airship.com).


>[!TIP]
>
>Esta página de documentación fue creada por el [!DNL Airship] equipo. Para cualquier consulta o solicitud de actualización, póngase en contacto con ellos directamente en [support.airship.com](https://support.airship.com/).

## Requisitos previos 

Para poder enviar los segmentos de Adobe Experience Platform a [!DNL Airship], debe:

* Cree un grupo de etiquetas en el [!DNL Airship] proyecto.
* Genere un token portador para la autenticación.

>[!TIP]
> 
>Cree una [!DNL Airship] cuenta a través de [este vínculo](https://go.airship.eu/accounts/register/plan/starter/) de registro si aún no lo ha hecho.

### Grupos de etiquetas

El concepto de segmentos en Adobe Experience Platorm es similar a [Etiquetas](https://docs.airship.com/guides/audience/tags/) en Airship, con ligeras diferencias en la implementación. Esta integración asigna el estado de la [pertenencia de un usuario a un segmento](https://experienceleague.adobe.com/docs/experience-platform/xdm/mixins/profile/segmentation.html?lang=en#mixins) Experience Platform a la presencia o no presencia de una [!DNL Airship] etiqueta. Por ejemplo, en un segmento Plataforma en el que `xdm:status` cambia a `realized`, la etiqueta se agrega al [!DNL Airship] canal o al usuario con nombre a este perfil. Si la etiqueta `xdm:status` cambia a `exited`, se elimina.

Para habilitar esta integración, cree un grupo *de* etiquetas con [!DNL Airship] nombre `adobe-segments`.

>[!IMPORTANT]
>
>Al crear el nuevo grupo de etiquetas **No marque** el botón de opción que dice &quot;[!DNL Allow these tags to be set only from your server]&quot;. Al hacerlo, se producirá un error en la integración de las etiquetas Adobe.

Consulte [Administrar grupos](https://docs.airship.com/tutorials/manage-project/messaging/tag-groups) de etiquetas para obtener instrucciones sobre cómo crear el grupo de etiquetas.

### Testigo del portador

Vaya a **[!UICONTROL Configuración]** &quot; **[!UICONTROL API e integraciones]** en el panel [de](https://go.airship.com) Airship y seleccione **[!UICONTROL Tokens]** en el menú de la izquierda.

Haga clic en **[!UICONTROL Crear token]**.

Proporcione un nombre descriptivo para el token, por ejemplo, &quot;Destino de etiquetas de Adobe&quot;, y seleccione &quot;Acceso total&quot; para el rol.

Haga clic en **[!UICONTROL Crear token]** y guarde los detalles como confidenciales.

## Casos de uso

Para ayudarle a comprender mejor cómo y cuándo debe utilizar el [!DNL Airship Tags] destino, a continuación se muestran ejemplos de casos de uso que los clientes de Adobe Experience Platform pueden resolver usando este destino.

### Caso de uso n.º 1

Los minoristas o las plataformas de entretenimiento pueden crear perfiles de usuarios en función de sus clientes fieles y pasar dichos segmentos a [!DNL Airship] para la segmentación de mensajes en campañas móviles.

### Caso de uso n.º 2

Activar mensajes uno a uno en tiempo real cuando los usuarios entran o salen de segmentos específicos dentro o fuera de Adobe Experience Platform.

Por ejemplo, un minorista configura un segmento específico de jeans en la plataforma. Ese minorista ahora puede activar un mensaje móvil tan pronto como alguien establece su preferencia de vaqueros en una marca específica.

## Conectar a [!DNL Airship Tags] {#connect-airship-tags}

En **[!UICONTROL Destinos]** > **[!UICONTROL Catálogo]**, desplácese hasta la categoría Participación **** móvil. Seleccione **[!DNL Airship Tags]** y, a continuación, seleccione **[!UICONTROL Configurar]**.

>[!NOTE]
>
>Si ya existe una conexión con este destino, puede ver un botón **[!UICONTROL Activar]** en la tarjeta de destino. Para obtener más información sobre la diferencia entre **[!UICONTROL Activar]** y **[!UICONTROL Configurar]**, consulte la sección [Catálogo](../../ui/destinations-workspace.md#catalog) de la documentación del espacio de trabajo de destino.

![Conectar a etiquetas de aerolíneas](../../assets/catalog/mobile-engagement/airship-tags/catalog.png)

En el paso **Cuenta** , si ha configurado anteriormente una conexión con su [!DNL Airship Tags] destino, seleccione Cuenta **** existente y seleccione la conexión existente. O bien, puede seleccionar **[!UICONTROL Nueva cuenta]** para configurar una nueva conexión con [!DNL Airship Tags]. Seleccione **[!UICONTROL Conectar a destino]** para conectar Adobe Experience Platform al [!DNL Airship] proyecto utilizando el distintivo de portador que generó desde el [!DNL Airship] panel.

>[!NOTE]
>
>Adobe Experience Platform admite la validación de credenciales en el proceso de autenticación y muestra un mensaje de error si introduce credenciales incorrectas en la [!DNL Airship] cuenta. Esto garantiza que no se complete el flujo de trabajo con credenciales incorrectas.

![Conectar a etiquetas de aerolíneas](../../assets/catalog/mobile-engagement/airship-tags/connect-account.png)

Una vez que se hayan confirmado las credenciales y Adobe Experience Platform esté conectado al [!DNL Airship] proyecto, puede seleccionar **[!UICONTROL Siguiente]** para continuar con el paso de **[!UICONTROL configuración]** .

En el paso **[!UICONTROL Autenticación]** , escriba un **[!UICONTROL Nombre]** y una **[!UICONTROL Descripción]** para el flujo de activación.

También en este paso, puede seleccionar un centro de datos de EE. UU. o de la UE, según el centro de datos que se aplique a este destino [!DNL Airship] . Finalmente, seleccione uno o varios casos de uso de mercadotecnia para los que se exportarán datos al destino. Puede seleccionar entre los casos de uso de mercadotecnia definidos por el Adobe o puede crear los suyos propios. Para obtener más información sobre los casos de uso de mercadotecnia, consulte la página [Administración de datos en tiempo real de CDP](../../../rtcdp/privacy/data-governance-overview.md#destinations) . Para obtener información sobre los casos individuales de uso de mercadotecnia definidos por el Adobe, consulte la descripción general [de las políticas de uso de](../../../data-governance/policies/overview.md#core-actions)datos.

Seleccione **[!UICONTROL Crear destino]** después de haber rellenado los campos anteriores.

![Conectar a etiquetas de aerolíneas](../../assets/catalog/mobile-engagement/airship-tags/select-domain.png)

Se ha creado el destino. Puede seleccionar **[!UICONTROL Guardar y salir]** si desea activar segmentos más adelante o puede seleccionar **[!UICONTROL Siguiente]** para continuar el flujo de trabajo y seleccionar los segmentos que desea activar. En cualquier caso, consulte la siguiente sección, [Activar segmentos](#activate-segments), para el resto del flujo de trabajo.

## Activar segmentos {#activate-segments}

Para activar segmentos en [!DNL Airship Tags], siga los pasos a continuación:

En **[!UICONTROL Destinos > Examinar]**, seleccione el [!DNL Airship Tags] destino en el que desea activar los segmentos.

![activate-flow](../../assets/catalog/mobile-engagement/airship-tags/browse.png)

Haga clic en el nombre del destino. Esto le lleva al flujo Activar.

Tenga en cuenta que si ya existe un flujo de activación para un destino, puede ver los segmentos que se están enviando al destino. Seleccione **[!UICONTROL Editar activación]** en el carril derecho y siga los pasos a continuación para modificar los detalles de la activación.

![activate-flow](../../assets/catalog/mobile-engagement/airship-tags/activate.png)

Seleccione **[!UICONTROL Activar]**. En el flujo de trabajo **[!UICONTROL Activar destino]** , en la página **[!UICONTROL Seleccionar segmentos]** , seleccione los segmentos a los que desea enviar [!DNL Airship Tags].

![segmentos a destino](../../assets/catalog/mobile-engagement/airship-tags/select-segments.png)

En el paso **[!UICONTROL Asignación]** , seleccione qué atributos e identidades del esquema [XDM](../../../xdm/home.md) se asignarán al esquema de destino. Seleccione **[!UICONTROL Añadir nueva asignación]** para examinar el esquema y asignarlo a la identidad de destinatario correspondiente.

![pantalla inicial de asignación de identidad](../../assets/catalog/mobile-engagement/airship-tags/identity-mapping.png)

[!DNL Airship] las etiquetas se pueden establecer en un canal, que representa la instancia de dispositivo, por ejemplo, iPhone, o en un usuario designado, que asigna todos los dispositivos de un usuario a un identificador común, como un ID de cliente. Si tiene direcciones de correo electrónico de texto sin formato (sin hash) como identidad principal en el esquema, seleccione el campo de correo electrónico en los atributos **** de origen y asigne al usuario con [!DNL Airship] nombre en la columna derecha en Identidades **[!UICONTROL de]** Destinatario, como se muestra a continuación.

![Asignación de usuarios con nombre](../../assets/catalog/mobile-engagement/airship-tags/mapping-option-2.png)

Para los identificadores que deben asignarse a un canal, es decir, un dispositivo, se asigna al canal apropiado en función del origen. Las siguientes imágenes muestran cómo asignar un ID de publicidad de Google a un canal de [!DNL Airship] Android.

![Conectar a etiquetas](../../assets/catalog/mobile-engagement/airship-tags/select-source-identity.png)de Airship![Conectar a asignación de etiquetas](../../assets/catalog/mobile-engagement/airship-tags/select-target-identity.png)de Airship![Canal](../../assets/catalog/mobile-engagement/airship-tags/mapping-option.png)

En la página de programación **[!UICONTROL de]** segmentos, la programación está deshabilitada. Haga clic en **[!UICONTROL Siguiente]** para continuar con el paso de revisión.

En la página **[!UICONTROL Revisar]** , puede ver un resumen de su selección. Seleccione **[!UICONTROL Cancelar]** para desglosar el flujo, **[!UICONTROL Atrás]** para modificar la configuración o **[!UICONTROL Finalizar]** para confirmar la selección y el inicio de envío de datos al destino.

>[!IMPORTANT]
>
>En este paso, Adobe Experience Platform comprueba si hay infracciones de la directiva de uso de datos. A continuación se muestra un ejemplo de violación de una política. No puede completar el flujo de trabajo de activación de segmentos hasta que no haya resuelto la infracción. Para obtener información sobre cómo resolver las infracciones de políticas, consulte Aplicación de [políticas](../../../rtcdp/privacy/data-governance-overview.md#enforcement) en la sección de documentación de administración de datos.

![confirmación-selección](../../assets/common/data-policy-violation.png)

Si no se ha detectado ninguna infracción de directiva, seleccione **[!UICONTROL Finalizar]** para confirmar la selección y el inicio al enviar datos al destino.

![confirmación-selección](../../assets/catalog/mobile-engagement/airship-tags/review.png)


## Uso y gobernanza de los datos {#data-usage-governance}

Todos los [!DNL Adobe Experience Platform] destinos cumplen con las directivas de uso de datos al administrar los datos. Para obtener información detallada sobre cómo [!DNL Adobe Experience Platform] implementar la administración de datos, consulte Administración de [datos en CDP](../../../rtcdp/privacy/data-governance-overview.md)en tiempo real.

