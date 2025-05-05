---
title: Conexión de Adobe Campaign Managed Cloud Services
description: Adobe Campaign Managed Cloud Services ofrece una plataforma para diseñar experiencias multicanal para clientes, y proporciona un entorno para la organización visual de la campaña, la administración de interacciones en tiempo real y la ejecución multicanal.
exl-id: fe151ad3-c431-4b5a-b453-9d1d9aedf775
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '1633'
ht-degree: 2%

---

# Conexión de Adobe Campaign Managed Cloud Services {#adobe-campaign-managed-services}

>[!IMPORTANT]
>
>Esta integración funciona con [Adobe Campaign versión 8.4 o superior](https://experienceleague.adobe.com/docs/campaign/campaign-v8/new/release-notes.html#release-8-4-1).

## Información general {#overview}

Adobe Campaign Managed Cloud Services ofrece una plataforma para diseñar experiencias multicanal para clientes, y proporciona un entorno para la organización visual de la campaña, la administración de interacciones en tiempo real y la ejecución multicanal. [Introducción a Campaign](https://experienceleague.adobe.com/docs/campaign/campaign-v8/start/get-started.html)

Utilice Campaign para lo siguiente:

* Impulso de la personalización y la participación mediante una única vista accesible del cliente,
* Integración de canales de correo electrónico, móviles, en línea y sin conexión en el recorrido del cliente.
* Automatice la entrega de mensajes y ofertas significativos y oportunos.

## Mecanismos de protección {#guardrails}

Tenga en cuenta las siguientes protecciones al utilizar la conexión de Adobe Campaign Managed Cloud Services:

* Puede [activar](#activate) un máximo de 25 audiencias en este destino.

  Puede cambiar este límite actualizando el valor de la opción **NmsCdp_Aep_Audience_List_Limit** en la carpeta **[!UICONTROL Administración]** > **[!UICONTROL Plataforma]** > **[!UICONTROL Opciones]** del explorador de Campaign.

* Para cada audiencia, puede agregar hasta 20 campos a [map](#map) a Adobe Campaign.

  Puede cambiar este límite actualizando el valor de la opción **NmsCdp_Aep_Destinations_Max_Columns** en la carpeta **[!UICONTROL Administración]** > **[!UICONTROL Plataforma]** > **[!UICONTROL Opciones]** del explorador de Campaign.

* Retención de datos en la zona de aterrizaje de datos (DLZ) del almacenamiento del blob de Azure: 7 días.
* La frecuencia de activación es de 3 horas como mínimo.
* La longitud máxima del nombre de archivo que admite esta conexión es de 255 caracteres. Cuando [configure el nombre de archivo exportado](../../ui/activate-batch-profile-destinations.md#configure-file-names), asegúrese de que el nombre de archivo no supere los 255 caracteres. Si se supera la longitud máxima del nombre de archivo, se producen errores de activación.

## Casos de uso {#use-cases}

Para ayudarle a comprender mejor cómo y cuándo debe utilizar el destino de Adobe Campaign Manage Service, aquí tiene un ejemplo de caso de uso que los clientes de Adobe Experience Platform pueden solucionar mediante este destino.

* Adobe Experience Platform crea un perfil de cliente que incorpora información como el gráfico de identidades, datos de comportamiento de analytics, combinaciones de datos sin conexión y en línea, etc. Con esta integración, puede aumentar las capacidades de segmentación que ya existen en Adobe Campaign con esas audiencias con tecnología de Adobe Experience Platform y, por lo tanto, activar esos datos en Campaign.

  Por ejemplo, una empresa de atuendos deportivos quiere aprovechar las audiencias con tecnología Adobe Experience Platform y activarlas con Adobe Campaign para llegar a su base de clientes en los diferentes canales admitidos por Adobe Campaign. Una vez enviados los mensajes, se desea mejorar el perfil del cliente en Adobe Experience Platform con datos de experiencia de Adobe Campaign como envíos, aperturas y clics.

  El resultado son campañas en canales múltiples que son más coherentes en todo el ecosistema de Adobe Experience Cloud y un perfil de cliente enriquecido que se adapta y aprende rápidamente.


* Además de la activación de audiencias en Campaign, puede aprovechar el destino de Adobe Campaign Managed Services para incorporar atributos de perfil adicionales vinculados a un perfil en Adobe Experience Platform y que tienen un proceso de sincronización configurado para que se actualicen en la base de datos de Adobe Campaign.

  Por ejemplo, supongamos que captura los valores de inclusión y exclusión en Adobe Experience Platform. Con esta conexión, puede trasladar estos valores a Adobe Campaign y establecer un proceso de sincronización para que se actualicen de forma regular.

  >[!NOTE]
  >
  >La sincronización de atributos de perfil está disponible para perfiles que ya están presentes en la base de datos de Adobe Campaign.

[Más información sobre la integración de Adobe Campaign con Adobe Experience Platform](https://experienceleague.adobe.com/docs/campaign/campaign-v8/connect/ac-aep.html?lang=es)

## Identidades admitidas {#supported-identities}

*Adobe Campaign Managed Cloud Services* admite la activación de identidades que se describe en la tabla siguiente. Más información sobre [identidades](/help/identity-service/features/namespaces.md).

| Identidad de destino | Descripción | Consideraciones |
|---|---|---|
| external_id | ID de usuario personalizados | Seleccione esta identidad de destino cuando la identidad de origen sea un área de nombres personalizada. Se recomienda utilizar esta identidad y asignarla al ID en la instancia de Campaign que representa al cliente (loyalty_ID, account_ID, customer_ID...) |
| ECID | Experience Cloud ID | Un área de nombres que representa ECID. Este área de nombres también se puede mencionar mediante los siguientes alias: &quot;Adobe Marketing Cloud ID&quot;, &quot;Adobe Experience Cloud ID&quot;, &quot;Adobe Experience Platform ID&quot;. Consulte el siguiente documento sobre [ECID](/help/identity-service/features/ecid.md) para obtener más información. |
| email_lc_sha256 | Direcciones de correo electrónico con el algoritmo SHA256 | Adobe Experience Platform admite direcciones de correo electrónico con hash SHA256 y de texto sin formato. Si el campo de origen contiene atributos sin hash, marque la opción **[!UICONTROL Aplicar transformación]** para que [!DNL Experience Platform] aplique automáticamente el hash a los datos durante la activación. |
| phone_sha256 | Números de teléfono con hash con el algoritmo SHA256 | Los números de teléfono con hash SHA256 y texto sin formato son compatibles con Adobe Experience Platform. Si el campo de origen contiene atributos sin hash, marque la opción **[!UICONTROL Aplicar transformación]** para que [!DNL Experience Platform] aplique automáticamente el hash a los datos durante la activación. |
| GAID | GOOGLE ADVERTISING ID | Seleccione la identidad de destino GAID cuando su identidad de origen sea un área de nombres GAID. |
| IDFA | Apple ID para anunciantes | Seleccione la identidad de destino IDFA cuando la identidad de origen sea un área de nombres IDFA. |

{style="table-layout:auto"}

## Tipo y frecuencia de exportación {#export-type-frequency}

Consulte la tabla siguiente para obtener información sobre el tipo y la frecuencia de exportación de destino.

| Elemento | Tipo | Notas |
---------|----------|---------|
| Tipo de exportación | **[!UICONTROL Basado en perfil]** | Va a exportar todos los miembros de una audiencia, junto con los campos de esquema deseados (por ejemplo: dirección de correo electrónico, número de teléfono, apellidos), tal como se eligió en la pantalla Seleccionar atributos de perfil del [flujo de trabajo de activación de destino](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes). |
| Frecuencia de exportación | **[!UICONTROL Lote]** | Los destinos por lotes exportan archivos a plataformas descendentes en incrementos de tres, seis, ocho, doce o veinticuatro horas. Obtenga más información sobre [destinos basados en archivos por lotes](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## Conexión al destino {#connect}

>[!IMPORTANT]
> 
>Para conectarse al destino, necesita los **[[!UICONTROL permisos de control de acceso]](/help/access-control/home.md#permissions) de Ver destinos&rbrack;** y **[!UICONTROL Administrar destinos]**&lbrack;5&rbrace;. Lea la [descripción general del control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Para conectarse a este destino, siga los pasos descritos en el [tutorial de configuración de destino](../../ui/connect-destination.md). En el flujo de trabajo de configuración de destino, rellene los campos enumerados en las dos secciones siguientes.

### Rellenar detalles de destino {#destination-details}

Para configurar los detalles del destino, rellene los campos obligatorios y opcionales a continuación. Un asterisco junto a un campo en la interfaz de usuario indica que el campo es obligatorio.

![](../../assets/catalog/email-marketing/adobe-campaign-managed-services/destination-details.png)

* **[!UICONTROL Nombre]**: Un nombre por el cual reconocerá este destino en el futuro.
* **[!UICONTROL Descripción]**: Una descripción que le ayudará a identificar este destino en el futuro.
* **[!UICONTROL Seleccionar instancia]**: su instancia de marketing **[!DNL Campaign]**.
* **[!UICONTROL Asignación de destino]**: seleccione la asignación de destino que está utilizando en **[!DNL Adobe Campaign]** para realizar envíos. [Más información](https://experienceleague.adobe.com/docs/campaign/campaign-v8/profiles-and-audiences/add-profiles/target-mappings.html).
* **[!UICONTROL Seleccionar tipo de sincronización]**:

   * **[!UICONTROL Sincronización de audiencias]**: use esta opción para enviar audiencias de Adobe Experience Platform a Adobe Campaign.
   * **[!UICONTROL Sincronización de perfiles (solo actualización)]**: utilice esta opción para traer los atributos de perfil de Adobe Experience Platform a Adobe Campaign y establecer un proceso de sincronización para que se puedan actualizar de forma regular.

### Habilitar alertas {#enable-alerts}

Puede activar alertas para recibir notificaciones sobre el estado del flujo de datos a su destino. Seleccione una alerta de la lista a la que suscribirse para recibir notificaciones sobre el estado del flujo de datos. Para obtener más información sobre las alertas, consulte la guía sobre [suscripción a alertas de destinos mediante la interfaz de usuario](../../ui/alerts.md).

Cuando termine de proporcionar detalles para la conexión de destino, seleccione **[!UICONTROL Siguiente]**.

### Política de gobernanza y medidas coercitivas {#governance}

Seleccione las acciones de marketing aplicables a los datos que desea exportar al destino. Para Adobe Campaign, le recomendamos que seleccione la acción de marketing **[!UICONTROL Segmentación por correo electrónico]**.

Para obtener más información acerca de las acciones de marketing, consulte la página [descripción general de las políticas de uso de datos](/help/data-governance/policies/overview.md).

## Activar públicos en este destino {#activate}

>[!IMPORTANT]
> 
>* Para activar los datos, necesita los **[!UICONTROL permisos de control de acceso]**, **[!UICONTROL Activar destinos]**, **[!UICONTROL Ver perfiles]** y **[!UICONTROL Ver segmentos]**&#x200B;[para ](/help/access-control/home.md#permissions). Lea la [descripción general del control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.
>* Para exportar *identidades*, necesita el **[[!UICONTROL permiso de control de acceso]](/help/access-control/home.md#permissions) de&rbrack;** Ver gráfico de identidad&lbrack;. <br> ![Seleccione el área de nombres de identidad resaltada en el flujo de trabajo para activar audiencias en los destinos.](/help/destinations/assets/overview/export-identities-to-destination.png "Seleccione el área de nombres de identidad resaltada en el flujo de trabajo para activar audiencias en los destinos."){width="100" zoomable="yes"}

Lea [Activar datos de audiencia en destinos de exportación de perfiles por lotes](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-batch-profile-destinations.html) para obtener instrucciones sobre cómo activar datos de audiencia en este destino.

### Asignar atributos e identidades {#map}

Seleccione los campos XDM que desea exportar con los perfiles y asígnelos a los campos de Adobe Campaign correspondientes.[Más información sobre la selección de atributos e identidad para los destinos de marketing por correo electrónico](overview.md)

1. Seleccionar campos de origen:

   * Seleccione un **identificador** (por ejemplo: el campo de correo electrónico) como identidad de origen que identifica de forma exclusiva un perfil en Adobe Experience Platform y Adobe Campaign.

   * Seleccione todos los demás **atributos de perfil de origen XDM** que deban exportarse a Adobe Campaign.

   >[!NOTE]
   >
   >El campo &quot;segmentMembershipStatus&quot; es una asignación necesaria para reflejar el estado segmentMembership. Este campo se añade de forma predeterminada y no se puede modificar ni eliminar.

1. Asigne cada campo con su campo de destino en Adobe Campaign. Los campos de destino disponibles están determinados por la asignación de destino seleccionada al [crear el destino](#destination-details).

1. Identifique atributos obligatorios y claves de deduplicación. Tenga en cuenta que los valores de los atributos marcados como &quot;Obligatorio&quot; o &quot;Clave de anulación de duplicación&quot; no pueden ser nulos.

   * [Atributos obligatorios](../../ui/activate-batch-profile-destinations.md#mandatory-attributes): asegúrese de que todos los registros de perfil contengan los atributos seleccionados. Por ejemplo: todos los perfiles exportados contienen una dirección de correo electrónico. Se recomienda establecer como obligatorio tanto el campo de identidad como el campo utilizado como clave de anulación de duplicación.
   * [Una clave de anulación de duplicación](../../ui/activate-batch-profile-destinations.md#mandatory-attributes) es una clave principal que determina la identidad por la cual los usuarios desean que se dedupliquen sus perfiles.

     >[!IMPORTANT]
     >
     >Asegúrese de que el nombre del atributo de clave de anulación de duplicación coincida con un nombre de columna de la asignación de destino seleccionada.

   ![](../../assets/catalog/email-marketing/adobe-campaign-managed-services/mapping.png)

1. Una vez realizada la asignación, puede revisar y completar la configuración de destino para empezar a enviar datos a **[!DNL Campaign]**.
   [Obtenga información sobre cómo revisar y completar la configuración de destino](/help/destinations/destination-types.md#review).

## Datos exportados / Validar exportación de datos {#exported-data}

Una vez activado un destino, puede acceder al trabajo correspondiente y a los datos exportados en Campaign.

### Monitorización de trabajos de exportación de datos {#jobs}

Vaya al menú **[!UICONTROL Administración]** > **[!UICONTROL Auditoría]** > **[!UICONTROL Trabajos de carga de audiencia]** para supervisar todos los trabajos de exportación activados desde Adobe Experience Platform.

![](../../assets/catalog/email-marketing/adobe-campaign-managed-services/campaign-jobs.png)

### Acceso a datos exportados {#data}

Para la **[!UICONTROL sincronización de audiencias]**, puede comprobar la audiencia exportada si navega al menú **[!UICONTROL Perfil y destino]** > **[!UICONTROL Lista]** > **[!UICONTROL Audiencias de AEP]**.

![](../../assets/catalog/email-marketing/adobe-campaign-managed-services/campaign-audiences.png)

Para la **[!UICONTROL sincronización de perfiles (solo actualización)]**, los datos se actualizan automáticamente en la base de datos de Campaign para cada perfil dirigido por la audiencia activada en el destino.

## Uso de datos y gobernanza {#data-usage-governance}

Todos los destinos de [!DNL Adobe Experience Platform] cumplen con las políticas de uso de datos al administrar los datos. Para obtener información detallada sobre cómo [!DNL Adobe Experience Platform] aplica el control de datos, lea la [Información general sobre el control de datos](/help/data-governance/home.md).
