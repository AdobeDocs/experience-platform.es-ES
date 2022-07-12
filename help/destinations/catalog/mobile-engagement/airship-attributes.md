---
keywords: atributos de la aeronave;destino de la aeronave
title: Conexión de atributos de aeronave
description: Transfiera sin problemas los datos de audiencia de Adobe a la nave aérea como atributos de audiencia para la segmentación dentro de la nave aérea.
exl-id: bfc1b52f-2d68-40d6-9052-c2ee1e877961
source-git-commit: fd2019feb25b540612a278cbea5bf5efafe284dc
workflow-type: tm+mt
source-wordcount: '975'
ht-degree: 1%

---

# [!DNL Airship Attributes] connection {#airship-attributes-destination}

## Información general {#overview}

[!DNL Airship] es la plataforma de participación del cliente líder, que le ayuda a proporcionar mensajes omnicanal significativos y personalizados a sus usuarios en cada etapa del ciclo de vida del cliente.

Esta integración transfiere los datos de perfil de Adobe a [!DNL Airship] como [Atributos](https://docs.airship.com/guides/audience/attributes/) para objetivos o activaciones.

Para obtener más información sobre [!DNL Airship], consulte la [Documentos de Airship](https://docs.airship.com).

>[!TIP]
>
>Esta página de documentación la creó el [!DNL Airship] equipo. Para cualquier consulta o solicitud de actualización, póngase en contacto con ellos directamente en [support.airship.com](https://support.airship.com/).

## Requisitos previos {#prerequisites}

Antes de poder enviar los segmentos de audiencia a [!DNL Airship], debe:

* Habilite los atributos en su [!DNL Airship] proyecto.
* Genere un token al portador para la autenticación.

>[!TIP]
>
>Cree un [!DNL Airship] cuenta mediante [este vínculo de suscripción](https://go.airship.eu/accounts/register/plan/starter/) si aún no lo ha hecho.

## Tipo de exportación y frecuencia {#export-type-frequency}

Consulte la tabla siguiente para obtener información sobre el tipo y la frecuencia de exportación de destino.

| Elemento | Tipo | Notas |
---------|----------|---------|
| Tipo de exportación | **[!UICONTROL Basado en perfiles]** | Está exportando todos los miembros de un segmento, junto con los campos de esquema deseados (por ejemplo: dirección de correo electrónico, número de teléfono, apellidos) o identidades, según la asignación de campos. |
| Frecuencia de exportación | **[!UICONTROL Transmisión]** | Los destinos de flujo continuo son conexiones basadas en API &quot;siempre activadas&quot;. Tan pronto como un perfil se actualiza en el Experience Platform en función de la evaluación de segmentos, el conector envía la actualización descendente a la plataforma de destino. Más información sobre [destinos de flujo continuo](/help/destinations/destination-types.md#streaming-destinations). |

{style=&quot;table-layout:auto&quot;}

## Habilitar atributos {#enable-attributes}

Los atributos de perfil de Adobe Experience Platform son similares a [!DNL Airship] y se pueden asignar fácilmente entre sí en Platform mediante la herramienta de asignación que se muestra más abajo en esta página.

[!DNL Airship] los proyectos tienen varios atributos predefinidos y predeterminados. Si tiene un atributo personalizado, debe definirlo en [!DNL Airship] primero. Consulte [Configuración y administración de atributos](https://docs.airship.com/tutorials/audience/attributes/) para obtener más información.

## Generar token al portador {#bearer-token}

Vaya a **[!UICONTROL Configuración]** &quot; **[!UICONTROL API e integraciones]** en el [Panel de la aeronave](https://go.airship.com) y seleccione **[!UICONTROL Tokens]** en el menú de la izquierda.

Haga clic en **[!UICONTROL Crear token]**.

Proporcione un nombre descriptivo para el token, por ejemplo, &quot;Destino de atributos de Adobe&quot; y seleccione &quot;Acceso completo&quot; para la función.

Haga clic en **[!UICONTROL Crear token]** y guarde los detalles como confidenciales.

## Casos de uso {#use-cases}

Para ayudarle a comprender mejor cómo y cuándo debe usar la variable [!DNL Airship Attributes] destino, aquí hay ejemplos de casos de uso que los clientes de Adobe Experience Platform pueden resolver utilizando este destino.

### Caso de uso número 1

Aproveche los datos de perfil recopilados en Adobe Experience Platform para personalizar el mensaje y el contenido enriquecido en cualquiera de los [!DNL Airship]los canales de . Por ejemplo, aproveche [!DNL Experience Platform] datos de perfil para establecer atributos de ubicación en [!DNL Airship]. Esto permitirá que una marca de hotel muestre una imagen para la ubicación del hotel más cercana para cada usuario.

### Caso de uso n.º 2

Aproveche los atributos de Adobe Experience Platform para enriquecer aún más [!DNL Airship] perfiles y combinarlos con SDK o [!DNL Airship] datos predictivos. Por ejemplo, un minorista puede crear un segmento con datos de estado de lealtad y ubicación (atributos de Platform) y [!DNL Airship] se predice que produzca datos para enviar mensajes altamente dirigidos a usuarios con estatus de fidelidad de oro que viven en Las Vegas, Nevada, y que tienen una alta probabilidad de producir.

## Conectarse al destino {#connect}

>[!IMPORTANT]
> 
>Para conectarse al destino, necesita la variable **[!UICONTROL Administrar destinos]** [permiso de control de acceso](/help/access-control/home.md#permissions). Lea el [información general sobre el control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Para conectarse a este destino, siga los pasos descritos en la sección [tutorial de configuración de destino](../../ui/connect-destination.md). En el flujo de trabajo de configuración de destino, rellene los campos que aparecen en las dos secciones siguientes.

### Autenticar en destino {#authenticate}

Para autenticarse en el destino, rellene los campos obligatorios y seleccione **[!UICONTROL Conectarse al destino]**.

* **[!UICONTROL Token portador]**: el token de portador que generó a partir de la variable [!DNL Airship] tablero.

### Rellenar detalles de destino {#destination-details}

Para configurar los detalles del destino, rellene los campos opcionales y requeridos a continuación. Un asterisco junto a un campo en la interfaz de usuario indica que el campo es obligatorio.

* **[!UICONTROL Nombre]**: introduzca un nombre que le ayudará a identificar este destino.
* **[!UICONTROL Descripción]**: introduzca una descripción para este destino.
* **[!UICONTROL Dominio]**: seleccione un centro de datos de EE. UU. o de la UE, en función de cuál [!DNL Airship] el centro de datos se aplica a este destino.

### Habilitar alertas {#enable-alerts}

Puede activar las alertas para recibir notificaciones sobre el estado del flujo de datos a su destino. Seleccione una alerta de la lista para suscribirse y recibir notificaciones sobre el estado de su flujo de datos. Para obtener más información sobre las alertas, consulte la guía de [suscripción a alertas de destinos mediante la interfaz de usuario](../../ui/alerts.md).

Cuando haya terminado de proporcionar detalles para la conexión de destino, seleccione **[!UICONTROL Siguiente]**.

## Activar segmentos en este destino {#activate}

>[!IMPORTANT]
> 
>Para activar los datos, necesita la variable **[!UICONTROL Administrar destinos]**, **[!UICONTROL Activar destinos]**, **[!UICONTROL Ver perfiles]** y **[!UICONTROL Ver segmentos]** [permisos de control de acceso](/help/access-control/home.md#permissions). Lea el [información general sobre el control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Consulte [Activar datos de audiencia en destinos de exportación de segmentos de flujo continuo](../../ui/activate-segment-streaming-destinations.md) para obtener instrucciones sobre la activación de segmentos de audiencia en este destino.

## Consideraciones de asignación {#mapping-considerations}

[!DNL Airship] los atributos se pueden configurar en un canal, que representa la instancia del dispositivo, por ejemplo, iPhone, o un usuario con nombre, que asigna todos los dispositivos de un usuario a un identificador común, como un ID de cliente. Si tiene direcciones de correo electrónico de texto sin formato (sin hash) como identidad principal en el esquema, seleccione el campo de correo electrónico en el **[!UICONTROL Atributos de origen]** y asigne al [!DNL Airship] usuario con nombre en la columna derecha debajo de **[!UICONTROL Identidades de Target]**, como se muestra a continuación.

![Asignación de usuarios con nombre](../../assets/catalog/mobile-engagement/airship/mapping.png)

Para identificadores que deben asignarse a un canal, es decir, un dispositivo, se debe asignar al canal adecuado en función del origen. Las siguientes imágenes muestran cómo se crean dos asignaciones:

* IDFA iOS Advertising ID to an [!DNL Airship] Canal de iOS
* Adobe `fullName` atributo a [!DNL Airship] Atributo &quot;Nombre completo&quot;

>[!NOTE]
>
>Utilice el nombre descriptivo que aparece en la variable [!DNL Airship] tablero al seleccionar el campo de destino para la asignación de atributos.

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

Todo [!DNL Adobe Experience Platform] Los destinos de cumplen las políticas de uso de datos al administrar los datos. Para obtener información detallada sobre cómo [!DNL Adobe Experience Platform] exige el control de datos; consulte [Información general sobre la administración de datos](../../../data-governance/home.md).
