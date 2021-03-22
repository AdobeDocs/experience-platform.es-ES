---
keywords: atributos de la aeronave;destino de la aeronave
title: Conexión de atributos de aeronave
description: Transfiera sin problemas los datos de audiencia de Adobe a la nave aérea como atributos de audiencia para la segmentación dentro de la nave aérea.
translation-type: tm+mt
source-git-commit: 7d579d85d427c45f39d000288ed883c7ffd003bf
workflow-type: tm+mt
source-wordcount: '1142'
ht-degree: 1%

---


# (Beta) Conexión [!DNL Airship Attributes] {#airship-attributes-destination}

>[!IMPORTANT]
>
>El destino [!DNL Airship Attributes] en Adobe Experience Platform está actualmente en versión beta. La documentación y las funciones están sujetas a cambios.

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

Vaya a **[!UICONTROL Settings]**&quot; **[!UICONTROL APIs & Integrations]** en el [Airship dashboard](https://go.airship.com) y seleccione **[!UICONTROL Tokens]** en el menú de la izquierda.

Haga clic en **[!UICONTROL Create Token]**.

Proporcione un nombre descriptivo para el token, por ejemplo, &quot;Destino de atributos de Adobe&quot; y seleccione &quot;Acceso completo&quot; para la función.

Haga clic en **[!UICONTROL Create Token]** y guarde los detalles como confidenciales.

## Casos de uso {#use-cases}

Para ayudarle a comprender mejor cómo y cuándo debe utilizar el destino [!DNL Airship Attributes], estos son ejemplos de casos de uso que los clientes de Adobe Experience Platform pueden resolver utilizando este destino.

### Caso de uso número 1

Aproveche los datos de perfil recopilados en Adobe Experience Platform para personalizar el mensaje y el contenido enriquecido en cualquiera de los canales de [!DNL Airship]. Por ejemplo, aproveche los datos de perfil [!DNL Experience Platform] para establecer los atributos de ubicación dentro de [!DNL Airship]. Esto permitirá que una marca de hotel muestre una imagen para la ubicación del hotel más cercana para cada usuario.

### Caso de uso n.º 2

Aproveche los atributos de Adobe Experience Platform para enriquecer aún más los perfiles [!DNL Airship] y combinarlos con datos predictivos del SDK o [!DNL Airship]. Por ejemplo, un minorista puede crear un segmento con datos de estado de fidelidad y ubicación (atributos de Platform) y [!DNL Airship] predicho que produzca datos para enviar mensajes altamente dirigidos a usuarios con el estado de fidelidad de oro que viven en Las Vegas, NV y que tienen una alta probabilidad de producir.

## Conectarse a [!DNL Airship Attributes] {#connect-airship-attributes}

En **[!UICONTROL Destinations]** > **[!UICONTROL Catalog]**, desplácese hasta la categoría **[!UICONTROL Mobile Engagement]**. Seleccione **[!DNL Airship Attributes]** y luego seleccione **[!UICONTROL Configure]**.

>[!NOTE]
>
>Si ya existe una conexión con este destino, puede ver un botón **[!UICONTROL Activate]** en la tarjeta de destino. Para obtener más información sobre la diferencia entre **[!UICONTROL Activate]** y **[!UICONTROL Configure]**, consulte la sección [Catalog](../../ui/destinations-workspace.md#catalog) de la documentación del espacio de trabajo de destino.

![Conectar a Atributos de Envío Aéreo](../../assets/catalog/mobile-engagement/airship/catalog.png)

En el paso **Account**, si anteriormente había configurado una conexión con su destino [!DNL Airship Attributes], seleccione **[!UICONTROL Existing Account]** y la conexión existente. O bien, puede seleccionar **[!UICONTROL New Account]** para configurar una nueva conexión a [!DNL Airship Attributes]. Seleccione **[!UICONTROL Connect to destination]** para conectar Adobe Experience Platform al proyecto [!DNL Airship] utilizando el token al portador que generó desde el panel [!DNL Airship].

>[!NOTE]
>
>Adobe Experience Platform admite la validación de credenciales en el proceso de autenticación y muestra un mensaje de error si introduce credenciales incorrectas en su cuenta [!DNL Airship]. Esto garantiza que no complete el flujo de trabajo con credenciales incorrectas.

![Conectar a Atributos de Envío Aéreo](../../assets/catalog/mobile-engagement/airship/connect.png)

Una vez confirmadas las credenciales y que Adobe Experience Platform esté conectado al proyecto [!DNL Airship], puede seleccionar **[!UICONTROL Next]** para continuar con el paso **[!UICONTROL Setup]**.

En el paso **[!UICONTROL Authentication]**, introduzca un **[!UICONTROL Name]** y un **[!UICONTROL Description]** para el flujo de activación.

Además, en este paso, puede seleccionar un centro de datos de EE. UU. o de la UE, según el [!DNL Airship] centro de datos que se aplique a este destino. Finalmente, seleccione uno o más **[!UICONTROL Marketing Actions]** para los que se exportarán datos al destino. Puede seleccionar entre las acciones de marketing definidas por el Adobe o puede crear las suyas. Para obtener más información sobre las acciones de marketing, consulte [Información general sobre las políticas de uso de datos](../../../data-governance/policies/overview.md).

Seleccione **[!UICONTROL Create Destination]** después de rellenar los campos anteriores.

![Conectar a Atributos de Envío Aéreo](../../assets/catalog/mobile-engagement/airship/select-domain.png)

Se ha creado el destino. Puede seleccionar **[!UICONTROL Save & Exit]** si desea activar segmentos más adelante o puede seleccionar **[!UICONTROL Next]** para continuar con el flujo de trabajo y seleccionar segmentos para activarlos. En cualquier caso, consulte la siguiente sección, [Activar segmentos](#activate-segments), para el resto del flujo de trabajo.

## Activar segmentos {#activate-segments}

Para activar segmentos en [!DNL Airship Attributes], siga los pasos a continuación:

En **[!UICONTROL Destinations > Browse]**, seleccione el destino [!DNL Airship Attributes] donde desea activar los segmentos.

![activate-flow](../../assets/catalog/mobile-engagement/airship/browse.png)

Haga clic en el nombre del destino. Esto le lleva al flujo de activación.

Tenga en cuenta que si ya existe un flujo de activación para un destino, puede ver los segmentos que se están enviando actualmente al destino. Seleccione **[!UICONTROL Edit activation]** en el carril derecho y siga los pasos a continuación para modificar los detalles de activación.

![activate-flow](../../assets/catalog/mobile-engagement/airship/activate.png)

Seleccione **[!UICONTROL Activate]**. En el flujo de trabajo **[!UICONTROL Activate destination]** , en la página **[!UICONTROL Select Segments]**, seleccione qué segmentos desea enviar a [!DNL Airship Attributes].

![segmentos a destino](../../assets/catalog/mobile-engagement/airship/select-segments.png)

En el paso **[!UICONTROL Mapping]**, seleccione qué atributos e identidades del esquema [XDM](../../../xdm/home.md) se asignarán al esquema de destino. Seleccione **[!UICONTROL Add new mapping]** para examinar el esquema y asignarlo a la identidad de destino correspondiente.

![pantalla inicial de asignación de identidad](../../assets/catalog/mobile-engagement/airship/identity-mapping.png)

[!DNL Airship] los atributos se pueden configurar en un canal, que representa la instancia del dispositivo, por ejemplo, iPhone, o un usuario con nombre, que asigna todos los dispositivos de un usuario a un identificador común, como un ID de cliente. Si tiene direcciones de correo electrónico de texto sin formato (sin hash) como identidad principal en el esquema, seleccione el campo de correo electrónico en **[!UICONTROL Source Attributes]** y asigne al usuario [!DNL Airship] con nombre en la columna derecha de **[!UICONTROL Target Identities]**, como se muestra a continuación.

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

En la página **[!UICONTROL Segment schedule]**, la programación está deshabilitada. Haga clic en **[!UICONTROL Next]** para continuar con el paso de revisión.

![Programación deshabilitada](../../assets/catalog/mobile-engagement/airship/scheduling.png)

En la página **[!UICONTROL Review]** puede ver un resumen de su selección. Seleccione **[!UICONTROL Cancel]** para desglosar el flujo, **[!UICONTROL Back]** para modificar la configuración o **[!UICONTROL Finish]** para confirmar la selección y empezar a enviar datos al destino.

>[!IMPORTANT]
>
>En este paso, Adobe Experience Platform comprueba las infracciones de la directiva de uso de datos. A continuación se muestra un ejemplo en el que se infringe una política. No puede completar el flujo de trabajo de activación de segmentos hasta que no haya resuelto la infracción. Para obtener información sobre cómo resolver infracciones de políticas, consulte [Aplicación de políticas](../../../data-governance/enforcement/auto-enforcement.md) en la sección de documentación de control de datos.

![confirm-selection](../../assets/common/data-policy-violation.png)

Si no se ha detectado ninguna infracción de directiva, seleccione **[!UICONTROL Finish]** para confirmar la selección y empezar a enviar datos al destino.

![review](../../assets/catalog/mobile-engagement/airship/review.png)

## Administración y uso de datos {#data-usage-governance}

Todos los destinos [!DNL Adobe Experience Platform] cumplen las políticas de uso de datos al administrar los datos. Para obtener información detallada sobre cómo [!DNL Adobe Experience Platform] aplica el control de datos, consulte la [Información general sobre el control de datos](../../../data-governance/home.md).
