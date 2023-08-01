---
keywords: atributos del dirigible;destino del dirigible
title: Conexión de Atributos del dirigible
description: Transfiera sin problemas los datos de audiencias de Adobe al dirigible como atributos de audiencia para segmentar dentro del dirigible.
exl-id: bfc1b52f-2d68-40d6-9052-c2ee1e877961
source-git-commit: 1ed82798125f32fe392f2a06a12280ac61f225c6
workflow-type: tm+mt
source-wordcount: '1022'
ht-degree: 0%

---

# [!DNL Airship Attributes] conexión {#airship-attributes-destination}

## Información general {#overview}

[!DNL Airship] es la plataforma líder de participación del cliente, que le ayuda a proporcionar mensajes omnicanal significativos y personalizados a sus usuarios en cada fase del ciclo de vida del cliente.

Esta integración pasa los datos de perfil de Adobe a [!DNL Airship] as [Atributos](https://docs.airship.com/guides/audience/attributes/) para segmentar o activar.

Para obtener más información acerca de [!DNL Airship], consulte la [Documentos de dirigibles](https://docs.airship.com).

>[!TIP]
>
>Este conector de destino y la página de documentación los crea y mantiene el [!DNL Airship] equipo. Para cualquier consulta o solicitud de actualización, póngase en contacto directamente con ellos en [support.airship.com](https://support.airship.com/).

## Requisitos previos {#prerequisites}

Antes de enviar las audiencias a [!DNL Airship], debe:

* Habilite los atributos en su [!DNL Airship] proyecto.
* Genere un token de portador para la autenticación.

>[!TIP]
>
>Crear un [!DNL Airship] cuenta mediante [este vínculo de suscripción](https://go.airship.eu/accounts/register/plan/starter/) si aún no lo ha hecho.

## Compatibilidad con audiencias externas {#external-audiences-support}

Todos los destinos admiten la activación de audiencias generadas a través del Experience Platform [Servicio de segmentación](../../../segmentation/home.md).

Además, este destino también admite la activación de las audiencias externas que se describen en la tabla siguiente.

| Tipo de audiencia externa | Descripción |
---------|----------|
| Cargas personalizadas | Audiencias introducidas en Experience Platform desde archivos CSV. |

{style="table-layout:auto"}

## Tipo y frecuencia de exportación {#export-type-frequency}

Consulte la tabla siguiente para obtener información sobre el tipo y la frecuencia de exportación de destino.

| Elemento | Tipo | Notas |
---------|----------|---------|
| Tipo de exportación | **[!UICONTROL Basado en perfiles]** | Va a exportar todos los miembros de un segmento, junto con los campos de esquema deseados (por ejemplo: dirección de correo electrónico, número de teléfono, apellidos) o identidades, según la asignación de campos. |
| Frecuencia de exportación | **[!UICONTROL Transmisión]** | Los destinos de streaming son conexiones basadas en API &quot;siempre activadas&quot;. Tan pronto como se actualiza un perfil en Experience Platform según la evaluación de audiencias, el conector envía la actualización de forma descendente a la plataforma de destino. Más información sobre [destinos de streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Habilitar atributos {#enable-attributes}

Los atributos de perfil de Adobe Experience Platform son similares a [!DNL Airship] atributos y se pueden asignar fácilmente entre sí en Platform mediante la herramienta de asignación que se muestra más adelante en esta página.

[!DNL Airship] los proyectos tienen varios atributos predefinidos y predeterminados. Si tiene un atributo personalizado, debe definirlo en [!DNL Airship] primero. Consulte [Configurar y administrar atributos](https://docs.airship.com/tutorials/audience/attributes/) para obtener más información.

## Generar token de portador {#bearer-token}

Ir a **[!UICONTROL Configuración]** &quot; **[!UICONTROL API e integraciones]** en el [Tablero del dirigible](https://go.airship.com) y seleccione **[!UICONTROL Tokens]** en el menú de la izquierda.

Clic **[!UICONTROL Crear token]**.

Proporcione un nombre descriptivo para el token, por ejemplo, &quot;Atributos de Adobe Destino&quot;, y seleccione &quot;Todos los accesos&quot; para el rol.

Clic **[!UICONTROL Crear token]** y guarde los detalles como confidenciales.

## Casos de uso {#use-cases}

Para ayudarle a comprender mejor cómo y cuándo debe utilizar el [!DNL Airship Attributes] Destino. Estos son ejemplos de casos de uso que los clientes de Adobe Experience Platform pueden solucionar mediante este destino.

### Caso de uso #1

Aproveche los datos de perfil recopilados en Adobe Experience Platform para personalizar el mensaje y el contenido enriquecido en cualquiera de los siguientes elementos [!DNL Airship]Los canales de. Por ejemplo, aprovechar [!DNL Experience Platform] datos de perfil para establecer atributos de ubicación en [!DNL Airship]. Esto permitirá que la marca de un hotel muestre una imagen de la ubicación del hotel más cercana para cada usuario.

### Caso de uso #2

Aproveche los atributos de Adobe Experience Platform para enriquecer aún más [!DNL Airship] y combinarlo con SDK o [!DNL Airship] datos predictivos. Por ejemplo, un minorista puede crear una audiencia con datos de estado de fidelidad y ubicación (atributos de Platform) y [!DNL Airship] Se predice que perderá datos para enviar mensajes de alto nivel de segmentación a usuarios con el estado de fidelidad de oro que viven en Las Vegas, NV y que tienen una alta probabilidad de pérdida.

## Conectar con el destino {#connect}

>[!IMPORTANT]
> 
>Para conectarse al destino, necesita el **[!UICONTROL Administrar destinos]** [permiso de control de acceso](/help/access-control/home.md#permissions). Lea el [información general de control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Para conectarse a este destino, siga los pasos descritos en la sección [tutorial de configuración de destino](../../ui/connect-destination.md). En el flujo de trabajo de configuración de destino, rellene los campos enumerados en las dos secciones siguientes.

### Autenticar en el destino {#authenticate}

Para autenticarse en el destino, rellene los campos obligatorios y seleccione **[!UICONTROL Conectar con destino]**.

* **[!UICONTROL Token de portador]**: el token de portador que generó a partir del [!DNL Airship] panel.

### Rellenar detalles de destino {#destination-details}

Para configurar los detalles del destino, rellene los campos obligatorios y opcionales a continuación. Un asterisco junto a un campo en la interfaz de usuario indica que el campo es obligatorio.

* **[!UICONTROL Nombre]**: introduzca un nombre que le ayude a identificar este destino.
* **[!UICONTROL Descripción]**: introduzca una descripción para este destino.
* **[!UICONTROL Dominio]**: seleccione un centro de datos de EE. UU. o de la UE, según cuál [!DNL Airship] el centro de datos se aplica a este destino.

### Habilitar alertas {#enable-alerts}

Puede activar alertas para recibir notificaciones sobre el estado del flujo de datos a su destino. Seleccione una alerta de la lista a la que suscribirse para recibir notificaciones sobre el estado del flujo de datos. Para obtener más información sobre las alertas, consulte la guía de [suscripción a alertas de destinos mediante la IU](../../ui/alerts.md).

Cuando haya terminado de proporcionar detalles para la conexión de destino, seleccione **[!UICONTROL Siguiente]**.

## Activar audiencias en este destino {#activate}

>[!IMPORTANT]
> 
>Para activar los datos, necesita el **[!UICONTROL Administrar destinos]**, **[!UICONTROL Activar destinos]**, **[!UICONTROL Ver perfiles]**, y **[!UICONTROL Ver segmentos]** [permisos de control de acceso](/help/access-control/home.md#permissions). Lea el [información general de control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Consulte [Activar datos de audiencia en destinos de exportación de audiencia de flujo continuo](../../ui/activate-segment-streaming-destinations.md) para obtener instrucciones sobre cómo activar audiencias en este destino.

## Consideraciones de asignación {#mapping-considerations}

[!DNL Airship] Los atributos se pueden establecer en un canal que represente una instancia de dispositivo (por ejemplo, iPhone) o un usuario designado que asigne todos los dispositivos de un usuario a un identificador común (por ejemplo, un ID de cliente). Si tiene direcciones de correo electrónico de texto sin formato (sin hash) como identidad principal en el esquema, seleccione el campo de correo electrónico en su **[!UICONTROL Atributos de origen]** y asigne a [!DNL Airship] usuario designado en la columna derecha debajo de **[!UICONTROL Identidades de destino]**, como se muestra a continuación.

![Asignación de usuarios con nombre](../../assets/catalog/mobile-engagement/airship/mapping.png)

Para los identificadores que deben asignarse a un canal, es decir, a un dispositivo, asígnelos al canal adecuado en función del origen. Las siguientes imágenes muestran cómo se crean dos asignaciones:

* ID de publicidad de iOS de IDFA para una [!DNL Airship] Canal de iOS
* Adobe `fullName` atribuir a [!DNL Airship] Atributo &quot;Nombre completo&quot;

>[!NOTE]
>
>Utilice un nombre descriptivo que aparezca en el [!DNL Airship] al seleccionar el campo de destino de la asignación de atributos.

**Identidad del mapa**

Seleccionar campo de origen:

![Conectar con atributos de dirigible](../../assets/catalog/mobile-engagement/airship/select-source-identity.png)

Seleccionar campo de destino:

![Conectar con atributos de dirigible](../../assets/catalog/mobile-engagement/airship/select-target-identity.png)

**Asignar atributo**

Seleccionar atributo de origen:

![Seleccionar campo de origen](../../assets/catalog/mobile-engagement/airship/select-source-attributes.png)

Seleccionar atributo objetivo:

![Seleccionar campo de destino](../../assets/catalog/mobile-engagement/airship/select-target-attribute.png)

Verificar asignación:

![Asignación de canales](../../assets/catalog/mobile-engagement/airship/mapping.png)


## Uso de datos y gobernanza {#data-usage-governance}

Todo [!DNL Adobe Experience Platform] Los destinos de cumplen con las políticas de uso de datos al gestionar los datos. Para obtener información detallada sobre cómo [!DNL Adobe Experience Platform] aplica la gobernanza de datos. Consulte la [Resumen de gobernanza de datos](../../../data-governance/home.md).
