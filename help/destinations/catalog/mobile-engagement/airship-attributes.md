---
keywords: atributos del dirigible;destino del dirigible
title: Conexión de Atributos del dirigible
description: Pase sin problemas los datos de audiencias de Adobe a la aeronave como atributos de audiencia para segmentar dentro de la aeronave.
exl-id: bfc1b52f-2d68-40d6-9052-c2ee1e877961
source-git-commit: 453884612e787439ea58f312d8080622ee0441f7
workflow-type: tm+mt
source-wordcount: '1150'
ht-degree: 2%

---

# [!DNL Airship Attributes] conexión {#airship-attributes-destination}

>[!IMPORTANT]
>
>* A partir del 25 de marzo de 2025, verá dos tarjetas de [!DNL Airship Attributes] en paralelo en el catálogo de destinos. Esto se debe a una actualización interna del servicio de destinos. Se ha cambiado el nombre del conector de destino [!DNL Airship Attributes] existente a **[!UICONTROL (obsoleto) Atributos del dirigible]** y ya tiene disponible una nueva tarjeta con el nombre **[!UICONTROL Atributos del dirigible]**.
>* Use la conexión **[!UICONTROL Airship Attributes]** en el catálogo para nuevos flujos de datos de activación. Si tiene flujos de datos activos en el destino **[!UICONTROL (obsoleto) Atributos de dirigible]**, se actualizarán automáticamente, por lo que no se requiere que realice ninguna acción por su parte.
>* Si está creando flujos de datos a través de la [API de Flow Service](https://developer.adobe.com/experience-platform-apis/references/destinations/), debe actualizar sus [!DNL flow spec ID] y [!DNL connection spec ID] a los siguientes valores:
>   * Id. de especificación de flujo: `a862e0be-966e-4e5a-80d3-1bb566461986`
>   * Id. de especificación de conexión: `594bc002-4a47-49b7-8a98-ac0d21045502`

## Información general {#overview}

[!DNL Airship] es la plataforma de participación del cliente líder, que le ayuda a entregar mensajes omnicanal significativos y personalizados a sus usuarios en cada etapa del ciclo de vida del cliente.

Esta integración pasa los datos de perfil de Adobe a [!DNL Airship] como [Atributos](https://docs.airship.com/guides/audience/attributes/) para el direccionamiento o el activador.

Para obtener más información sobre [!DNL Airship], consulte [Documentos de la aeronave](https://docs.airship.com).

>[!TIP]
>
>El equipo [!DNL Airship] crea y mantiene este conector de destino y esta página de documentación. Para cualquier consulta o solicitud de actualización, comuníquese directamente con ellos en [support.airship.com](https://support.airship.com/).

## Requisitos previos {#prerequisites}

Para poder enviar las audiencias a [!DNL Airship], debe:

* Habilite los atributos en su proyecto [!DNL Airship].
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
| Tipo de exportación | **[!UICONTROL Basado en perfil]** | Va a exportar todos los miembros de un segmento, junto con los campos de esquema deseados (por ejemplo: dirección de correo electrónico, número de teléfono, apellidos) o identidades, según la asignación de campos. |
| Frecuencia de exportación | **[!UICONTROL Transmisión]** | Los destinos de streaming son conexiones basadas en API &quot;siempre activadas&quot;. Tan pronto como se actualiza un perfil en Experience Platform basado en la evaluación de audiencias, el conector envía la actualización de forma descendente a la plataforma de destino. Más información sobre [destinos de streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Habilitar atributos {#enable-attributes}

Los atributos de perfil de Adobe Experience Platform son similares a los atributos de [!DNL Airship] y se pueden asignar fácilmente entre sí en Platform mediante la herramienta de asignación que se muestra más adelante en esta página.

[!DNL Airship] proyectos tienen varios atributos predefinidos y predeterminados. Si tiene un atributo personalizado, primero debe definirlo en [!DNL Airship]. Consulte [Configurar y administrar atributos](https://docs.airship.com/tutorials/audience/attributes/) para obtener más información.

## Generar token de portador {#bearer-token}

Vaya a **[!UICONTROL Configuración]**&quot; **[!UICONTROL API e integraciones]** en el [tablero del dirigible](https://go.airship.com) y seleccione **[!UICONTROL Tokens]** en el menú de la izquierda.

Haga clic en **[!UICONTROL Crear token]**.

Proporcione un nombre descriptivo para el token, por ejemplo, &quot;Atributos de Adobe Destino&quot;, y seleccione &quot;Todos los accesos&quot; para el rol.

Haga clic en **[!UICONTROL Crear token]** y guarde los detalles como confidenciales.

## Casos de uso {#use-cases}

Para ayudarle a comprender mejor cómo y cuándo debe utilizar el destino [!DNL Airship Attributes], aquí hay casos de uso de ejemplo que los clientes de Adobe Experience Platform pueden solucionar mediante este destino.

### Caso de uso #1

Aproveche los datos de perfil recopilados en Adobe Experience Platform para personalizar el mensaje y el contenido enriquecido en cualquiera de los canales de [!DNL Airship]. Por ejemplo, aproveche los datos de perfil de [!DNL Experience Platform] para establecer atributos de ubicación en [!DNL Airship]. Esto permitirá que la marca de un hotel muestre una imagen de la ubicación del hotel más cercana para cada usuario.

### Caso de uso #2

Aproveche los atributos de Adobe Experience Platform para enriquecer aún más los perfiles de [!DNL Airship] y combinarlos con datos predictivos de SDK o [!DNL Airship]. Por ejemplo, un minorista puede crear una audiencia con datos de estado de fidelidad y ubicación (atributos de Platform) y se predice que [!DNL Airship] perderá datos para enviar mensajes de alto nivel de segmentación a usuarios con estado de fidelidad de oro que viven en Las Vegas, NV y tienen una alta probabilidad de pérdida.

## Conexión al destino {#connect}

>[!IMPORTANT]
> 
>Para conectarse al destino, necesita los **[!UICONTROL permisos de control de acceso](/help/access-control/home.md#permissions) de Ver destinos]** y **[!UICONTROL Administrar destinos]**[5}. Lea la [descripción general del control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

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
>* Para activar los datos, necesita los **[!UICONTROL permisos de control de acceso]**, **[!UICONTROL Activar destinos]**, **[!UICONTROL Ver perfiles]** y **[!UICONTROL Ver segmentos]**[para ](/help/access-control/home.md#permissions). Lea la [descripción general del control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.
>* Para exportar *identidades*, necesita el **[!UICONTROL permiso de control de acceso](/help/access-control/home.md#permissions) de]** Ver gráfico de identidad[. <br> ![Seleccione el área de nombres de identidad resaltada en el flujo de trabajo para activar audiencias en los destinos.](/help/destinations/assets/overview/export-identities-to-destination.png "Seleccione el área de nombres de identidad resaltada en el flujo de trabajo para activar audiencias en los destinos."){width="100" zoomable="yes"}

Consulte [Activar datos de audiencia en destinos de exportación de audiencia de streaming](../../ui/activate-segment-streaming-destinations.md) para obtener instrucciones sobre cómo activar audiencias en este destino.

## Consideraciones de asignación {#mapping-considerations}

Los atributos de [!DNL Airship] se pueden establecer en un canal que represente una instancia de dispositivo (por ejemplo, iPhone) o un usuario designado que asigne todos los dispositivos de un usuario a un identificador común (por ejemplo, un ID de cliente). Si tiene direcciones de correo electrónico de texto sin formato (sin hash) como identidad principal en el esquema, seleccione el campo de correo electrónico en sus **[!UICONTROL Atributos de Source]** y asígnelo al usuario con nombre [!DNL Airship] en la columna derecha debajo de **[!UICONTROL Identidades de destino]**, como se muestra a continuación.

![Asignación de usuarios con nombre](../../assets/catalog/mobile-engagement/airship/mapping.png)

Para los identificadores que deben asignarse a un canal, es decir, a un dispositivo, asígnelos al canal adecuado en función del origen. Las siguientes imágenes muestran cómo se crean dos asignaciones:

* ID de iOS Advertising de IDFA para un canal de iOS [!DNL Airship]
* Atributo de Adobe `fullName` a [!DNL Airship] atributo &quot;Full Name&quot;

>[!NOTE]
>
>Utilice un nombre descriptivo que aparezca en el panel [!DNL Airship] al seleccionar el campo de destino para la asignación de atributos.

**Identidad de mapa**

Seleccionar campo de origen:

![Atributos de conexión a dirigible](../../assets/catalog/mobile-engagement/airship/select-source-identity.png)

Seleccionar campo de destino:

![Atributos de conexión a dirigible](../../assets/catalog/mobile-engagement/airship/select-target-identity.png)

**Atributo de mapa**

Seleccionar atributo de origen:

![Seleccionar campo de origen](../../assets/catalog/mobile-engagement/airship/select-source-attributes.png)

Seleccionar atributo objetivo:

![Seleccionar campo de destino](../../assets/catalog/mobile-engagement/airship/select-target-attribute.png)

Verificar asignación:

![Asignación de canales](../../assets/catalog/mobile-engagement/airship/mapping.png)


## Uso de datos y gobernanza {#data-usage-governance}

Todos los destinos de [!DNL Adobe Experience Platform] cumplen con las políticas de uso de datos al administrar los datos. Para obtener información detallada sobre cómo [!DNL Adobe Experience Platform] aplica el control de datos, consulte la [Información general sobre el control de datos](../../../data-governance/home.md).
