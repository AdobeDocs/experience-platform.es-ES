---
keywords: atributos de la aeronave;destino de la aeronave
title: Conexión de atributos de aeronaves
description: Pasar sin problemas los datos de Audiencia de Adobe a la aeronave como atributos de Audiencia para objetivos dentro de la aeronave.
translation-type: tm+mt
source-git-commit: e13a19640208697665b0a7e0106def33fd1e456d
workflow-type: tm+mt
source-wordcount: '1204'
ht-degree: 0%

---


# (Beta) [!DNL Airship Attributes] conexión {#airship-attributes-destination}

>[!IMPORTANT]
>
>El destino [!DNL Airship Attributes] de Adobe Experience Platform está actualmente en versión beta. La documentación y las funciones están sujetas a cambios.

[!DNL Airship] es la plataforma líder de compromiso con el cliente, que le ayuda a enviar mensajes de canal omnicho significativos y personalizados a sus usuarios en cada etapa del ciclo vital del cliente.

Esta integración pasa los datos de perfil de Adobe a [!DNL Airship] como [Atributos](https://docs.airship.com/guides/audience/attributes/) para la determinación de objetivos o la activación.

Para obtener más información sobre [!DNL Airship], consulte los [documentos de Airship](https://docs.airship.com).


>[!TIP]
>
>Esta página de documentación fue creada por el equipo [!DNL Airship]. Para cualquier consulta o solicitud de actualización, póngase en contacto con ellos directamente en [support.airship.com](https://support.airship.com/).

## Requisitos previos {#prerequisites}

Para poder enviar los segmentos de audiencia a [!DNL Airship], debe:

* Habilite atributos en el proyecto [!DNL Airship].
* Genere un token portador para la autenticación.

>[!TIP]
>
>Cree una cuenta [!DNL Airship] mediante [este vínculo de inicio de sesión](https://go.airship.eu/accounts/register/plan/starter/) si aún no lo ha hecho.

### Habilitar atributos {#enable-attributes}

Los atributos de perfil de Adobe Experience Platform son similares a los atributos [!DNL Airship] y se pueden asignar fácilmente entre sí en la plataforma mediante la herramienta de asignación que se muestra más abajo en esta página.

[!DNL Airship] los proyectos tienen varios atributos predeterminados y predefinidos. Si tiene un atributo personalizado, primero debe definirlo en [!DNL Airship]. Consulte [Configurar y administrar atributos](https://docs.airship.com/tutorials/audience/attributes/) para obtener más información.

### Distintivo del portador {#bearer-token}

Vaya a **[!UICONTROL Settings]**&quot; **[!UICONTROL APIs &amp; Integrations]** en el [panel de Airship](https://go.airship.com) y seleccione **[!UICONTROL Tokens]** en el menú de la izquierda.

Haga clic en **[!UICONTROL Crear token]**.

Proporcione un nombre descriptivo para el token, por ejemplo, &quot;Destino de atributos de Adobe&quot;, y seleccione &quot;Acceso total&quot; para el rol.

Haga clic en **[!UICONTROL Crear token]** y guarde los detalles como confidenciales.

## Casos de uso {#use-cases}

Para ayudarle a comprender mejor cómo y cuándo debe utilizar el destino [!DNL Airship Attributes], a continuación se muestran ejemplos de casos de uso que los clientes de Adobe Experience Platform pueden resolver usando este destino.

### Caso de uso n.º 1

Aproveche los datos de perfil recopilados en Adobe Experience Platform para personalizar el mensaje y el contenido enriquecido dentro de cualquiera de los canales de [!DNL Airship]. Por ejemplo: aproveche los datos de perfil [!DNL Experience Platform] para establecer atributos de ubicación dentro de [!DNL Airship]. Esto permitirá que una marca de hotel muestre una imagen para la ubicación del hotel más cercana para cada usuario.

### Caso de uso n.º 2

Aproveche los atributos de Adobe Experience Platform para enriquecer aún más los perfiles [!DNL Airship] y combinarlos con datos predictivos de SDK o [!DNL Airship]. Por ejemplo: un minorista puede crear un segmento con datos de ubicación y estado de lealtad (atributos de Platform) y [!DNL Airship] predichos para generar datos para enviar mensajes altamente dirigidos a los usuarios con el estado de lealtad de oro que viven en Las Vegas, NV y que tienen una alta probabilidad de producir.

## Conectar con [!DNL Airship Attributes] {#connect-airship-attributes}

En **[!UICONTROL Destinations]** > **[!UICONTROL Catalog]**, desplácese a la categoría **[!UICONTROL Mobile Engagement]**. Seleccione **[!DNL Airship Attributes]** y, a continuación, seleccione **[!UICONTROL Configurar]**.

>[!NOTE]
>
>Si ya existe una conexión con este destino, puede ver un botón **[!UICONTROL Activar]** en la tarjeta de destino. Para obtener más información sobre la diferencia entre **[!UICONTROL Activar]** y **[!UICONTROL Configurar]**, consulte la sección [Catálogo](../../ui/destinations-workspace.md#catalog) de la documentación del espacio de trabajo de destino.

![Conectar a atributos de aerolíneas](../../assets/catalog/mobile-engagement/airship/catalog.png)

En el paso **Cuenta**, si anteriormente había configurado una conexión con su destino [!DNL Airship Attributes], seleccione **[!UICONTROL Cuenta existente]** y seleccione la conexión existente. O bien, puede seleccionar **[!UICONTROL Nueva cuenta]** para configurar una nueva conexión a [!DNL Airship Attributes]. Seleccione **[!UICONTROL Conectar a destino]** para conectar Adobe Experience Platform al proyecto [!DNL Airship] utilizando el distintivo portador que generó a partir del panel [!DNL Airship].

>[!NOTE]
>
>Adobe Experience Platform admite la validación de credenciales en el proceso de autenticación y muestra un mensaje de error si introduce credenciales incorrectas en su cuenta [!DNL Airship]. Esto garantiza que no se complete el flujo de trabajo con credenciales incorrectas.

![Conectar a atributos de aerolíneas](../../assets/catalog/mobile-engagement/airship/connect.png)

Una vez confirmadas las credenciales y que Adobe Experience Platform esté conectado al proyecto [!DNL Airship], puede seleccionar **[!UICONTROL Siguiente]** para continuar con el paso **[!UICONTROL Configuración]**.

En el paso **[!UICONTROL Autenticación]**, escriba un **[!UICONTROL Nombre]** y una **[!UICONTROL Descripción]** para el flujo de activación.

También en este paso, puede seleccionar un centro de datos de EE. UU. o de la UE, según el [!DNL Airship] centro de datos que se aplique a este destino. Finalmente, seleccione uno o varios casos de uso de mercadotecnia para los que se exportarán datos al destino. Puede seleccionar entre los casos de uso de mercadotecnia definidos por el Adobe o puede crear los suyos propios. Para obtener más información acerca de los casos de uso de mercadotecnia, consulte la [información general de las directivas de uso de datos](../../../data-governance/policies/overview.md).

Seleccione **[!UICONTROL Crear destino]** después de completar los campos anteriores.

![Conectar a atributos de aerolíneas](../../assets/catalog/mobile-engagement/airship/select-domain.png)

Se ha creado el destino. Puede seleccionar **[!UICONTROL Guardar y salir]** si desea activar segmentos más adelante o puede seleccionar **[!UICONTROL Siguiente]** para continuar el flujo de trabajo y seleccionar los segmentos que desea activar. En cualquier caso, consulte la siguiente sección, [Activar segmentos](#activate-segments), para el resto del flujo de trabajo.

## Activar segmentos {#activate-segments}

Para activar segmentos en [!DNL Airship Attributes], siga los pasos a continuación:

En **[!UICONTROL Destinos > Examinar]**, seleccione el [!DNL Airship Attributes] destino en el que desea activar los segmentos.

![activate-flow](../../assets/catalog/mobile-engagement/airship/browse.png)

Haga clic en el nombre del destino. Esto le lleva al flujo Activar.

Tenga en cuenta que si ya existe un flujo de activación para un destino, puede ver los segmentos que se están enviando al destino. Seleccione **[!UICONTROL Editar activación]** en el carril derecho y siga los pasos a continuación para modificar los detalles de la activación.

![activate-flow](../../assets/catalog/mobile-engagement/airship/activate.png)

Seleccione **[!UICONTROL Activar]**. En el flujo de trabajo **[!UICONTROL Activar destino]**, en la página **[!UICONTROL Seleccionar segmentos]**, seleccione los segmentos que se enviarán a [!DNL Airship Attributes].

![segmentos a destino](../../assets/catalog/mobile-engagement/airship/select-segments.png)

En el paso **[!UICONTROL Mapping]**, seleccione qué atributos e identidades del esquema [XDM](../../../xdm/home.md) se asignarán al esquema de destino. Seleccione **[!UICONTROL Añadir nueva asignación]** para examinar el esquema y asignarlo a la identidad de destinatario correspondiente.

![pantalla inicial de asignación de identidad](../../assets/catalog/mobile-engagement/airship/identity-mapping.png)

[!DNL Airship] los atributos pueden configurarse en un canal, que representa la instancia de dispositivo, por ejemplo, iPhone, o un usuario designado, que asigna todos los dispositivos de un usuario a un identificador común, como un ID de cliente. Si tiene direcciones de correo electrónico de texto sin formato (sin hash) como identidad principal en el esquema, seleccione el campo de correo electrónico en los **[!UICONTROL Atributos de origen]** y asigne al [!DNL Airship] usuario con nombre en la columna derecha debajo de **[!UICONTROL Identidades de Destinatario]**, como se muestra a continuación.

![Asignación de usuarios con nombre](../../assets/catalog/mobile-engagement/airship/mapping.png)

Para los identificadores que deben asignarse a un canal, es decir, un dispositivo, se asigna al canal apropiado en función del origen. Las siguientes imágenes muestran cómo se crean dos asignaciones:

* ID de publicidad de iOS de IDFA en un canal de [!DNL Airship] iOS
* Atributo `fullName` de Adobe al atributo [!DNL Airship] &quot;Nombre completo&quot;

>[!NOTE]
>
>Utilice el nombre descriptivo que aparece en el panel [!DNL Airship] al seleccionar el campo destinatario para la asignación de atributos.

**Asignar identidad**

Seleccionar campo de origen:

![Conectar a atributos de aerolíneas](../../assets/catalog/mobile-engagement/airship/select-source-identity.png)

Seleccione el campo destinatario:

![Conectar a atributos de aerolíneas](../../assets/catalog/mobile-engagement/airship/select-target-identity.png)

**Atributo de mapa**

Seleccionar atributo de origen:

![Seleccionar campo de origen](../../assets/catalog/mobile-engagement/airship/select-source-attributes.png)

Seleccionar atributo de destinatario:

![Seleccionar campo destinatario](../../assets/catalog/mobile-engagement/airship/select-target-attribute.png)

Verificar asignación:

![Asignación de canales](../../assets/catalog/mobile-engagement/airship/mapping.png)

En la página **[!UICONTROL Programación de segmentos]**, la programación está deshabilitada. Haga clic en **[!UICONTROL Siguiente]** para continuar con el paso de revisión.

![Programación deshabilitada actualmente](../../assets/catalog/mobile-engagement/airship/scheduling.png)

En la página **[!UICONTROL Revisar]**, puede ver un resumen de su selección. Seleccione **[!UICONTROL Cancelar]** para desglosar el flujo, **[!UICONTROL Atrás]** para modificar la configuración o **[!UICONTROL Finalizar]** para confirmar la selección y el inicio al enviar datos al destino.

>[!IMPORTANT]
>
>En este paso, Adobe Experience Platform comprueba si hay infracciones de la directiva de uso de datos. A continuación se muestra un ejemplo de violación de una política. No puede completar el flujo de trabajo de activación de segmentos hasta que no haya resuelto la infracción. Para obtener información sobre cómo resolver las violaciones de políticas, consulte [Aplicación de políticas](../../../data-governance/enforcement/auto-enforcement.md) en la sección de documentación de administración de datos.

![confirmación-selección](../../assets/common/data-policy-violation.png)

Si no se ha detectado ninguna infracción de directiva, seleccione **[!UICONTROL Finalizar]** para confirmar la selección y el inicio al enviar datos al destino.

![revisión](../../assets/catalog/mobile-engagement/airship/review.png)

## Administración y uso de datos {#data-usage-governance}

Todos los destinos [!DNL Adobe Experience Platform] son compatibles con las políticas de uso de datos al administrar los datos. Para obtener información detallada sobre cómo [!DNL Adobe Experience Platform] impone la administración de datos, consulte la [información general sobre la administración de datos](../../../data-governance/home.md).
