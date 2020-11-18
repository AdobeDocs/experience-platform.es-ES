---
keywords: airship attributes;airship destination
title: Destino de atributos de aeronaves
seo-title: Destino de atributos de aeronaves
description: Pasar sin problemas los datos de Audiencia de Adobe a la aeronave como atributos de Audiencia para objetivos dentro de la aeronave.
seo-description: Pasar sin problemas los datos de Audiencia de Adobe a la aeronave como atributos de Audiencia para objetivos dentro de la aeronave.
translation-type: tm+mt
source-git-commit: 0e065bbc0917d5009738b4cae890ffd13c0ab154
workflow-type: tm+mt
source-wordcount: '1245'
ht-degree: 1%

---


# (Beta) [!DNL Airship Attributes] Destino {#airship-attributes-destination}

>[!IMPORTANT]
>
>El [!DNL Airship Attributes] destino de Adobe Experience Platform está actualmente en fase beta. La documentación y las funciones están sujetas a cambios.

## Información general {#overview}

[!DNL Airship] es la plataforma líder de compromiso con el cliente, que le ayuda a enviar mensajes de canal omnicho significativos y personalizados a sus usuarios en cada etapa del ciclo vital del cliente.

Esta integración pasa los datos de perfil de Adobe a [!DNL Airship] como [atributos](https://docs.airship.com/guides/audience/attributes/) para direccionamiento o activación.

Para obtener más información sobre [!DNL Airship], consulte los documentos [de Airship](https://docs.airship.com).


>[!TIP]
>
>Esta página de documentación fue creada por el [!DNL Airship] equipo. Para cualquier consulta o solicitud de actualización, póngase en contacto con ellos directamente en [support.airship.com](https://support.airship.com/).

## Requisitos previos  {#prerequisites}

Para poder enviar los segmentos de audiencia a [!DNL Airship], debe:

* Habilite atributos en el [!DNL Airship] proyecto.
* Genere un token portador para la autenticación.

>[!TIP]
>
>Cree una [!DNL Airship] cuenta a través de [este vínculo](https://go.airship.eu/accounts/register/plan/starter/) de registro si aún no lo ha hecho.

### Habilitar atributos {#enable-attributes}

Los atributos de perfil de Adobe Experience Platform son similares a [!DNL Airship] los atributos y se pueden asignar fácilmente entre sí en la plataforma mediante la herramienta de asignación que se muestra más abajo en esta página.

[!DNL Airship] los proyectos tienen varios atributos predeterminados y predefinidos. Si tiene un atributo personalizado, debe definirlo en [!DNL Airship] primer lugar. Consulte [Configurar y administrar atributos](https://docs.airship.com/tutorials/audience/attributes/) para obtener más información.

### Testigo del portador {#bearer-token}

1. Vaya a **[!UICONTROL Configuración]** &quot; **[!UICONTROL API e integraciones]** en el panel [de](https://go.airship.com) Airship y seleccione **[!UICONTROL Tokens]** en el menú de la izquierda.
1. Haga clic en **[!UICONTROL Crear token]**.
1. Proporcione un nombre descriptivo para el token, por ejemplo, &quot;Destino de atributos de Adobe&quot;, y seleccione &quot;Acceso total&quot; para el rol.
1. Haga clic en **[!UICONTROL Crear token]** y guarde los detalles como confidenciales.


## Casos de uso {#use-cases}

Para ayudarle a comprender mejor cómo y cuándo debe utilizar el [!DNL Airship Attributes] destino, a continuación se muestran ejemplos de casos de uso que los clientes de Adobe Experience Platform pueden resolver usando este destino.

### Caso de uso n.º 1

Aproveche los datos de perfil recopilados en Adobe Experience Platform para personalizar el mensaje y el contenido enriquecido dentro de cualquiera de los canales [!DNL Airship]de Adobe. Por ejemplo, aproveche los datos de [!DNL Experience Platform] perfil para establecer atributos de ubicación dentro de [!DNL Airship]. Esto permitirá que una marca de hotel muestre una imagen para la ubicación del hotel más cercana para cada usuario.

### Caso de uso n.º 2

Aproveche los atributos de Adobe Experience Platform para enriquecer aún más [!DNL Airship] perfiles y combinarlos con SDK o datos [!DNL Airship] predictivos. Por ejemplo, un minorista puede crear un segmento con datos de ubicación y estado de lealtad (atributos de Platform) y [!DNL Airship] predecir que genere datos para enviar mensajes con un objetivo muy preciso a los usuarios con un estado de lealtad al oro que viven en Las Vegas, NV y que tienen una alta probabilidad de reproducirse.

## Conectar con [!DNL Airship] atributos {#connect-airship-attributes}

1. En **[!UICONTROL Destinos]** > **[!UICONTROL Catálogo]**, desplácese hasta la categoría Participación **** móvil. Seleccione **[!DNL Airship Attributes]** y, a continuación, seleccione **[!UICONTROL Configurar]**.

   >[!NOTE]
   >
   >Si ya existe una conexión con este destino, puede ver un botón **[!UICONTROL Activar]** en la tarjeta de destino. Para obtener más información sobre la diferencia entre **[!UICONTROL Activar]** y **[!UICONTROL Configurar]**, consulte la sección [Catálogo](/help/rtcdp/destinations/destinations-workspace.md#catalog) de la documentación del espacio de trabajo de destino.

   ![Conectar a atributos de aerolíneas](/help/rtcdp/destinations/assets/airship-attributes-in-catalog.png)

2. En el paso **Cuenta** , si ha configurado anteriormente una conexión con su [!DNL Airship Attributes] destino, seleccione Cuenta **** existente y seleccione la conexión existente. O bien, puede seleccionar **[!UICONTROL Nueva cuenta]** para configurar una nueva conexión con [!DNL Airship Attributes]. Seleccione **[!UICONTROL Conectar a destino]** para conectar Adobe Experience Platform al [!DNL Airship] proyecto utilizando el distintivo de portador que generó desde el [!DNL Airship] panel.

   >[!NOTE]
   >
   >Adobe Experience Platform admite la validación de credenciales en el proceso de autenticación y muestra un mensaje de error si introduce credenciales incorrectas en la [!DNL Airship] cuenta. Esto garantiza que no se complete el flujo de trabajo con credenciales incorrectas.

   ![Conectar a atributos de aerolíneas](/help/rtcdp/destinations/assets/airship1-connect-to-airship.png)

3. Una vez que se hayan confirmado las credenciales y Adobe Experience Platform esté conectado al [!DNL Airship] proyecto, puede seleccionar **[!UICONTROL Siguiente]** para continuar con el paso de **[!UICONTROL configuración]** .

4. En el paso **[!UICONTROL Autenticación]** , escriba un **[!UICONTROL Nombre]** y una **[!UICONTROL Descripción]** para el flujo de activación. <br> También en este paso, puede seleccionar un centro de datos de EE. UU. o de la UE, según el centro de datos que se aplique a este destino [!DNL Airship] . Finalmente, seleccione uno o varios casos de uso de mercadotecnia para los que se exportarán datos al destino. Puede seleccionar entre los casos de uso de mercadotecnia definidos por el Adobe o puede crear los suyos propios. Para obtener más información sobre los casos de uso de mercadotecnia, consulte la página [Administración de datos en tiempo real de CDP](/help/rtcdp/privacy/data-governance-overview.md#destinations) . Para obtener información sobre los casos individuales de uso de mercadotecnia definidos por el Adobe, consulte la descripción general [de las políticas de uso de](/help/data-governance/policies/overview.md#core-actions)datos. <br> Seleccione **[!UICONTROL Crear destino]** después de haber rellenado los campos anteriores.

   ![Conectar a atributos de aerolíneas](/help/rtcdp/destinations/assets/airship2-select-airship-domain.png)

5. Se ha creado el destino. Puede seleccionar **[!UICONTROL Guardar y salir]** si desea activar segmentos más adelante o puede seleccionar **[!UICONTROL Siguiente]** para continuar el flujo de trabajo y seleccionar los segmentos que desea activar. En cualquier caso, consulte la siguiente sección, [Activar segmentos](#activate-segments), para el resto del flujo de trabajo.

## Activar segmentos {#activate-segments}

Para activar segmentos en [!DNL Airship Attributes], siga los pasos a continuación:

1. En **[!UICONTROL Destinos > Examinar]**, seleccione el [!DNL Airship Attributes] destino en el que desea activar los segmentos.
   ![activate-flow](/help/rtcdp/destinations/assets/airship-attributes-activate1.png)
1. Haga clic en el nombre del destino. Esto le lleva al flujo Activar.
Tenga en cuenta que si ya existe un flujo de activación para un destino, puede ver los segmentos que se están enviando al destino. Seleccione **[!UICONTROL Editar activación]** en el carril derecho y siga los pasos a continuación para modificar los detalles de la activación. ![activate-flow](/help/rtcdp/destinations/assets/airship-attributes-activate2.png)
1. Seleccione **[!UICONTROL Activar]**;
1. En el flujo de trabajo **[!UICONTROL Activar destino]** , en la página **[!UICONTROL Seleccionar segmentos]** , seleccione los segmentos a los que desea enviar [!DNL Airship Attributes].
   ![segmentos a destino](/help/rtcdp/destinations/assets/airship3-select-segments-to-export.png)
1. En el paso **[!UICONTROL Asignación]** , seleccione qué atributos e identidades del esquema [XDM](https://docs.adobe.com/content/help/es-ES/experience-platform/xdm/home.html) se asignarán al esquema de destino. Seleccione **[!UICONTROL Añadir nueva asignación]** para examinar el esquema y asignarlo a la identidad de destinatario correspondiente.
   ![pantalla inicial de asignación de identidad](/help/rtcdp/destinations/assets/gcm-identity-mapping.png)
   [!DNL Airship] los atributos pueden configurarse en un canal, que representa la instancia de dispositivo, por ejemplo, iPhone, o un usuario designado, que asigna todos los dispositivos de un usuario a un identificador común, como un ID de cliente. Si tiene direcciones de correo electrónico de texto sin formato (sin hash) como identidad principal en el esquema, seleccione el campo de correo electrónico en los atributos **** de origen y asigne al usuario con [!DNL Airship] nombre en la columna derecha en Identidades **[!UICONTROL de]**Destinatario, como se muestra a continuación.
   ![Asignación](/help/rtcdp/destinations/assets/airshiptags7-mappingoption2.png)de usuarios con nombrePara identificadores que deben asignarse a un canal, es decir, un dispositivo, se asigna al canal apropiado en función del origen. Las siguientes imágenes muestran cómo se crean dos asignaciones:

   * ID de publicidad de IDFA iOS en un canal [!DNL Airship] iOS
   * Atributo de Adobe `fullName` al atributo [!DNL Airship] &quot;Nombre completo&quot;

   >[!NOTE]
   >
   >Utilice el nombre descriptivo que aparece en el [!DNL Airship] panel al seleccionar el campo destinatario para la asignación de atributos.

   **Identidad**de mapaSeleccionar campo de origen:
   ![Conectar con atributos](/help/rtcdp/destinations/assets/airship5-select-source-identity.png)de aerolíneasCampo Seleccionar destinatario:
   ![Conectar a atributos de aerolíneas](/help/rtcdp/destinations/assets/airship6-select-target-identity.png)

   **Atributo de mapa**

   Seleccionar atributo de origen:
   ![Seleccionar campo](/help/rtcdp/destinations/assets/airship7-select-source-attributes.png)de origenSeleccionar atributo de destinatario:
   ![Seleccionar campo](/help/rtcdp/destinations/assets/airship8-select-target-attribute.png)destinatario Verificar asignación:
   ![Asignación de canales](/help/rtcdp/destinations/assets/airship9-mapping-final.png)

1. En la página de programación **[!UICONTROL de]** segmentos, la programación está deshabilitada. Haga clic en **[!UICONTROL Siguiente]** para continuar con el paso de revisión. ![Programación deshabilitada actualmente](/help/rtcdp/destinations/assets/airship10-scheduling-step-is-disabled-for-now.png)

1. En la página **[!UICONTROL Revisar]** , puede ver un resumen de su selección. Seleccione **[!UICONTROL Cancelar]** para desglosar el flujo, **[!UICONTROL Atrás]** para modificar la configuración o **[!UICONTROL Finalizar]** para confirmar la selección y el inicio de envío de datos al destino.

>[!IMPORTANT]
>
>En este paso, Adobe Experience Platform comprueba si hay infracciones de la directiva de uso de datos. A continuación se muestra un ejemplo de violación de una política. No puede completar el flujo de trabajo de activación de segmentos hasta que no haya resuelto la infracción. Para obtener información sobre cómo resolver las infracciones de políticas, consulte Aplicación de [políticas](/help/rtcdp/privacy/data-governance-overview.md#enforcement) en la sección de documentación de administración de datos.

![confirmación-selección](/help/rtcdp/destinations/assets/data-policy-violation.png)

Si no se ha detectado ninguna infracción de directiva, seleccione **[!UICONTROL Finalizar]** para confirmar la selección y el inicio al enviar datos al destino.

![revisión](/help/rtcdp/destinations/assets/airship11-review-step.png)

## Uso y gobernanza de los datos {#data-usage-governance}

Todos los [!DNL Adobe Experience Platform] destinos cumplen con las directivas de uso de datos al administrar los datos. Para obtener información detallada sobre cómo [!DNL Adobe Experience Platform] implementar la administración de datos, consulte Administración de [datos en CDP](/help/rtcdp/privacy/data-governance-overview.md)en tiempo real.
