---
title: Conexión de Adobe Campaign Managed Cloud Services
description: Adobe Campaign Managed Cloud Services ofrece una plataforma para diseñar experiencias multicanal para clientes, y proporciona un entorno para la organización visual de la campaña, la administración de interacciones en tiempo real y la ejecución multicanal.
exl-id: fe151ad3-c431-4b5a-b453-9d1d9aedf775
source-git-commit: c4ead035202828a09c8c170e0a380fa49d186473
workflow-type: tm+mt
source-wordcount: '1548'
ht-degree: 4%

---

# Conexión de Adobe Campaign Managed Cloud Services {#adobe-campaign-managed-services}

>[!IMPORTANT]
>
>Esta integración funciona con [Adobe Campaign versión 8.4 o superior](https://experienceleague.adobe.com/docs/campaign/campaign-v8/new/release-notes.html?lang=en#release-8-4-1).

## Información general {#overview}

Adobe Campaign Managed Cloud Services ofrece una plataforma para diseñar experiencias multicanal para clientes, y proporciona un entorno para la organización visual de la campaña, la administración de interacciones en tiempo real y la ejecución multicanal. [Introducción a Campaign](https://experienceleague.adobe.com/docs/campaign/campaign-v8/start/get-started.html)

Utilice Campaign para lo siguiente:
* Impulso de la personalización y la participación mediante una única vista accesible del cliente,
* Integración de canales de correo electrónico, móviles, en línea y sin conexión en el recorrido del cliente,
* Automatización de la entrega de mensajes y ofertas significativos y oportunos.

>[!IMPORTANT]
>
>Tenga en cuenta las siguientes protecciones al utilizar la conexión de Adobe Campaign Managed Cloud Services:
>
>* Se puede seleccionar un máximo de 50 segmentos [activado](#activate) para el destino,
>* Para cada segmento, puede añadir hasta 20 campos a [asignar](#map) a Adobe Campaign,
>* Retención de datos en la zona de aterrizaje de datos (DLZ) del almacenamiento del blob de Azure: 7 días,
>* La frecuencia de activación es de 3 horas como mínimo.

## Casos de uso {#use-cases}

Para ayudarle a comprender mejor cómo y cuándo debe utilizar el destino de Adobe Campaign Manage Service, aquí tiene un ejemplo de caso de uso que los clientes de Adobe Experience Platform pueden solucionar mediante este destino.

* Adobe Experience Platform crea un perfil de cliente que incorpora información como el gráfico de identidades, datos de comportamiento de analytics, combinaciones de datos sin conexión y en línea, etc. Con esta integración, puede aumentar las capacidades de segmentación que ya existen en Adobe Campaign con esas audiencias con tecnología de Adobe Experience Platform y, por lo tanto, activar esos datos en Campaign.

  Por ejemplo, una empresa de atuendos deportivos quiere aprovechar los segmentos inteligentes con tecnología de Adobe Experience Platform y activarlos con Adobe Campaign para llegar a su base de clientes en los diferentes canales admitidos por Adobe Campaign. Una vez enviados los mensajes, se desea mejorar el perfil del cliente en Adobe Experience Platform con datos de experiencia de Adobe Campaign, como envíos, aperturas y clics.

  El resultado son campañas en canales múltiples que son más coherentes en todo el ecosistema de Adobe Experience Cloud y un perfil de cliente enriquecido que se adapta y aprende rápidamente.


* Además de la activación de segmentos en Campaign, puede aprovechar el destino de Adobe Campaign Managed Services para incorporar atributos de perfil adicionales vinculados a un perfil en Adobe Experience Platform y que tienen un proceso de sincronización configurado para que se actualicen en la base de datos de Adobe Campaign.

  Por ejemplo, supongamos que captura los valores de inclusión y exclusión en Adobe Experience Platform. Con esta conexión, puede trasladar estos valores a Adobe Campaign y establecer un proceso de sincronización para que se actualicen de forma regular.

  >[!NOTE]
  >
  >La sincronización de atributos de perfil está disponible para perfiles que ya están presentes en la base de datos de Adobe Campaign.

[Obtenga más información sobre la integración de Adobe Campaign con Adobe Experience Platform](https://experienceleague.adobe.com/docs/campaign/campaign-v8/connect/ac-aep.html?lang=es)

## Identidades admitidas {#supported-identities}

*Adobe Campaign Managed Cloud Services* admite la activación de identidades descritas en la tabla siguiente. Más información sobre [identidades](/help/identity-service/namespaces.md).

| Identidad de destino | Descripción | Consideraciones |
|---|---|---|
| external_id | ID de usuario personalizados | Seleccione esta identidad de destino cuando la identidad de origen sea un área de nombres personalizada. Se recomienda utilizar esta identidad y asignarla al ID en la instancia de Campaign que representa al cliente (loyalty_ID, account_ID, customer_ID...) |
| ECID | Experience Cloud ID | Un área de nombres que representa ECID. Este área de nombres también se puede mencionar mediante los siguientes alias: &quot;Adobe Marketing Cloud ID&quot;, &quot;Adobe Experience Cloud ID&quot;, &quot;Adobe Experience Platform ID&quot;. Consulte el siguiente documento sobre [ECID](/help/identity-service/ecid.md) para obtener más información. |
| email_lc_sha256 | Direcciones de correo electrónico con el algoritmo SHA256 | Adobe Experience Platform admite direcciones de correo electrónico con hash SHA256 y de texto sin formato. Si el campo de origen contiene atributos sin hash, marque la **[!UICONTROL Aplicar transformación]** opción, para tener [!DNL Platform] hash automático de los datos en la activación. |
| phone_sha256 | Números de teléfono con hash con el algoritmo SHA256 | Los números de teléfono con hash SHA256 y texto sin formato son compatibles con Adobe Experience Platform. Si el campo de origen contiene atributos sin hash, marque la **[!UICONTROL Aplicar transformación]** opción, para tener [!DNL Platform] hash automático de los datos en la activación. |
| GAID | ID de publicidad de Google | Seleccione la identidad de destino GAID cuando su identidad de origen sea un área de nombres GAID. |
| IDFA | Apple ID para anunciantes | Seleccione la identidad de destino IDFA cuando la identidad de origen sea un área de nombres IDFA. |

{style="table-layout:auto"}

## Tipo y frecuencia de exportación {#export-type-frequency}

Consulte la tabla siguiente para obtener información sobre el tipo y la frecuencia de exportación de destino.

| Elemento | Tipo | Notas |
---------|----------|---------|
| Tipo de exportación | **[!UICONTROL Basado en perfiles]** | Va a exportar todos los miembros de un segmento, junto con los campos de esquema deseados (por ejemplo: dirección de correo electrónico, número de teléfono, apellidos), tal como se elige en la pantalla seleccionar atributos de perfil del [flujo de trabajo de activación de destino](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes). |
| Frecuencia de exportación | **[!UICONTROL Lote]** | Los destinos por lotes exportan archivos a plataformas descendentes en incrementos de tres, seis, ocho, doce o veinticuatro horas. Más información sobre [destinos basados en archivos por lotes](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## Conectar con el destino {#connect}

>[!IMPORTANT]
> 
>Para conectarse al destino, necesita el **[!UICONTROL Administrar destinos]** [permiso de control de acceso](/help/access-control/home.md#permissions). Lea el [información general de control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Para conectarse a este destino, siga los pasos descritos en la sección [tutorial de configuración de destino](../../ui/connect-destination.md). En el flujo de trabajo de configuración de destino, rellene los campos enumerados en las dos secciones siguientes.

### Rellenar detalles de destino {#destination-details}

Para configurar los detalles del destino, rellene los campos obligatorios y opcionales a continuación. Un asterisco junto a un campo en la interfaz de usuario indica que el campo es obligatorio.

![](../../assets/catalog/email-marketing/adobe-campaign-managed-services/destination-details.png)

* **[!UICONTROL Nombre]**: Un nombre con el que reconocerá este destino en el futuro.
* **[!UICONTROL Descripción]**: Una descripción que le ayudará a identificar este destino en el futuro.
* **[!UICONTROL Seleccionar instancia]**: su **[!DNL Campaign]** instancia de marketing.
* **[!UICONTROL Asignación de destino]**: seleccione la asignación de destino que está utilizando en **[!DNL Adobe Campaign]** para realizar envíos. [Más información](https://experienceleague.adobe.com/docs/campaign/campaign-v8/profiles-and-audiences/add-profiles/target-mappings.html).
* **[!UICONTROL Seleccionar tipo de sincronización]**:

   * **[!UICONTROL Sincronización de audiencia]**: utilice esta opción para enviar audiencias de Adobe Experience Platform a Adobe Campaign.
   * **[!UICONTROL Sincronización de perfiles (solo actualizar)]**: utilice esta opción para incorporar atributos de perfil de Adobe Experience Platform a Adobe Campaign y establecer un proceso de sincronización para que se puedan actualizar de forma regular.

### Habilitar alertas {#enable-alerts}

Puede activar alertas para recibir notificaciones sobre el estado del flujo de datos a su destino. Seleccione una alerta de la lista a la que suscribirse para recibir notificaciones sobre el estado del flujo de datos. Para obtener más información sobre las alertas, consulte la guía de [suscripción a alertas de destinos mediante la IU](../../ui/alerts.md).

Cuando haya terminado de proporcionar detalles para la conexión de destino, seleccione **[!UICONTROL Siguiente]**.

### Política de gobernanza y medidas coercitivas {#governance}

Seleccione las acciones de marketing aplicables a los datos que desea exportar al destino. Para Adobe Campaign, le recomendamos que seleccione la **[!UICONTROL Segmentación de correo electrónico]** acción de marketing.

Para obtener más información sobre las acciones de marketing, consulte la [información general sobre políticas de uso de datos](/help/data-governance/policies/overview.md) página.

## Activar segmentos en este destino {#activate}

>[!IMPORTANT]
> 
>Para activar los datos, necesita el **[!UICONTROL Administrar destinos]**, **[!UICONTROL Activar destinos]**, **[!UICONTROL Ver perfiles]**, y **[!UICONTROL Ver segmentos]** [permisos de control de acceso](/help/access-control/home.md#permissions). Lea el [información general de control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Leer [Activar datos de audiencia en destinos de exportación de perfiles por lotes](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-batch-profile-destinations.html?lang=es) para obtener instrucciones sobre cómo activar datos de audiencia en este destino.

### Asignar atributos e identidades {#map}

Seleccione los campos XDM que desea exportar con los perfiles y asígnelos a los campos de Adobe Campaign correspondientes.[Obtenga más información sobre la selección de identidad y atributos para destinos de marketing por correo electrónico](overview.md)

1. Seleccionar campos de origen:

   * Seleccione un **identificador** (Por ejemplo: el campo de correo electrónico) como identidad de origen que identifica de forma exclusiva un perfil en Adobe Experience Platform y Adobe Campaign.

   * Seleccionar todos los demás **Atributos de perfil de origen XDM** que deben exportarse a Adobe Campaign.

   >[!NOTE]
   >
   >El campo &quot;segmentMembershipStatus&quot; es una asignación necesaria para reflejar el estado segmentMembership. Este campo se añade de forma predeterminada y no se puede modificar ni eliminar.

1. Asigne cada campo con su campo de destino en Adobe Campaign. Los campos de destino disponibles están determinados por la asignación de destino seleccionada cuando [creación del destino](#destination-details).

1. Identifique atributos obligatorios y claves de deduplicación. Tenga en cuenta que los valores de los atributos marcados como &quot;Obligatorio&quot; o &quot;Clave de anulación de duplicación&quot; no pueden ser nulos.

   * [Atributos obligatorios](../../ui/activate-batch-profile-destinations.md#mandatory-attributes) asegúrese de que todos los registros de perfil contienen los atributos seleccionados. Por ejemplo: todos los perfiles exportados contienen una dirección de correo electrónico. Se recomienda establecer como obligatorio tanto el campo de identidad como el campo utilizado como clave de anulación de duplicación.
   * [Una clave de deduplicación](../../ui/activate-batch-profile-destinations.md#mandatory-attributes) es una clave principal que determina la identidad con la que los usuarios desean que se dedupliquen sus perfiles.

     >[!IMPORTANT]
     >
     >Asegúrese de que el nombre del atributo de clave de anulación de duplicación coincida con un nombre de columna de la asignación de destino seleccionada.

   ![](../../assets/catalog/email-marketing/adobe-campaign-managed-services/mapping.png)

1. Una vez realizada la asignación, puede revisar y completar la configuración de destino para comenzar a enviar datos a **[!DNL Campaign]**.
   [Obtenga información sobre cómo revisar y completar la configuración de destino](/help/destinations/destination-types.md#review).

## Datos exportados / Validar exportación de datos {#exported-data}

Una vez activado un destino, puede acceder al trabajo correspondiente y a los datos exportados en Campaign.

### Monitorización de trabajos de exportación de datos {#jobs}

Vaya a **[!UICONTROL Administration]** > **[!UICONTROL Auditoría]** > **[!UICONTROL Trabajos de carga de audiencia]** para controlar todos los trabajos de exportación activados desde Adobe Experience Platform.

![](../../assets/catalog/email-marketing/adobe-campaign-managed-services/campaign-jobs.png)

### Acceso a datos exportados {#data}

Para **[!UICONTROL Sincronización de audiencia]**, puede comprobar la audiencia exportada navegando hasta el **[!UICONTROL Perfil y destinatario]** > **[!UICONTROL Lista]** > **[!UICONTROL Audiencias de AEP]** menú.

![](../../assets/catalog/email-marketing/adobe-campaign-managed-services/campaign-audiences.png)

Para **[!UICONTROL Sincronización de perfiles (solo actualizar)]**, los datos se actualizan automáticamente en la base de datos de Campaign para cada perfil dirigido por el segmento activado en el destino.

## Uso de datos y gobernanza {#data-usage-governance}

Todo [!DNL Adobe Experience Platform] Los destinos de cumplen con las políticas de uso de datos al gestionar los datos. Para obtener información detallada sobre cómo [!DNL Adobe Experience Platform] aplica la gobernanza de datos, lea la [Resumen de gobernanza de datos](/help/data-governance/home.md).
