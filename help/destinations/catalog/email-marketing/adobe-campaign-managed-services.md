---
title: Conexión de Adobe Campaign Managed Cloud Services
description: Adobe Campaign Managed Cloud Services ofrece una plataforma para diseñar experiencias multicanal para clientes, y proporciona un entorno para la organización visual de la campaña, la administración de interacciones en tiempo real y la ejecución multicanal.
exl-id: fe151ad3-c431-4b5a-b453-9d1d9aedf775
source-git-commit: d946d3dbb09c1fe0163fba3a892b4c0f1b331f87
workflow-type: tm+mt
source-wordcount: '1721'
ht-degree: 2%

---

# [!DNL Adobe Campaign Managed Cloud Services] conexión {#adobe-campaign-managed-services}

>[!IMPORTANT]
>
>Esta integración funciona con [[!DNL Adobe Campaign] versión 8.4 o superior](https://experienceleague.adobe.com/docs/campaign/campaign-v8/new/release-notes.html#release-8-4-1).

## Información general {#overview}

[!DNL Adobe Campaign Managed Cloud Services] proporciona una plataforma para diseñar experiencias multicanal para clientes, y proporciona un entorno para la orquestación visual de la campaña, la administración de interacciones en tiempo real y la ejecución multicanal. [Introducción a Campaign](https://experienceleague.adobe.com/docs/campaign/campaign-v8/start/get-started.html)

Utilice Campaign para lo siguiente:

* Impulso de la personalización y la participación mediante una única vista accesible del cliente,
* Integración de canales de correo electrónico, móviles, en línea y sin conexión en el recorrido del cliente.
* Automatice la entrega de mensajes y ofertas significativos y oportunos.

## Mecanismos de protección {#guardrails}

Tenga en cuenta las siguientes protecciones al utilizar la conexión [!DNL Adobe Campaign Managed Cloud Services]:

* Puede [activar](#activate) un máximo de 25 audiencias en este destino.

  Puede cambiar este límite actualizando el valor de la opción **NmsCdp_Aep_Audience_List_Limit** en la carpeta **[!UICONTROL Administration]** > **[!UICONTROL Platform]** > **[!UICONTROL Options]** del explorador de Campaign. Esta protección limita la cantidad total de audiencias de Experience Platform que se pueden exportar a una sola instancia de Campaign en todos los destinos configurados.

* Para cada audiencia, puede agregar hasta 20 campos a [map](#map) a [!DNL Adobe Campaign].

  Puede cambiar este límite actualizando el valor de la opción **NmsCdp_Aep_Destinations_Max_Columns** en la carpeta **[!UICONTROL Administration]** > **[!UICONTROL Platform]** > **[!UICONTROL Options]** del explorador de Campaign.

* Retención de datos en la zona de aterrizaje de datos (DLZ) del almacenamiento del blob de Azure: 7 días.
* La frecuencia de activación es de 3 horas como mínimo.
* La longitud máxima del nombre de archivo que admite esta conexión es de 255 caracteres. Cuando [configure el nombre de archivo exportado](../../ui/activate-batch-profile-destinations.md#configure-file-names), asegúrese de que el nombre de archivo no supere los 255 caracteres. Si se supera la longitud máxima del nombre de archivo, se producen errores de activación.
* Los segmentos o audiencias que contienen caracteres especiales (por ejemplo: `&`) no se admiten al exportar audiencias a [!DNL Adobe Campaign].

## Casos de uso {#use-cases}

Para ayudarle a comprender mejor cómo y cuándo debe usar el destino de administración de servicios de [!DNL Adobe Campaign], aquí tiene un ejemplo de caso de uso que los clientes de [!DNL Adobe Experience Platform] pueden resolver usando este destino.

* [!DNL Adobe Experience Platform] crea un perfil de cliente que incorpora información como el gráfico de identidad, datos de comportamiento de analytics, combina datos sin conexión y en línea, etc. Con esta integración, puede aumentar las capacidades de segmentación que ya existen dentro de [!DNL Adobe Campaign] con esas [!DNL Adobe Experience Platform] audiencias que se sirven de y, por lo tanto, puede activar esos datos en Campaign.

  Por ejemplo, una empresa de ropa deportiva quiere aprovechar las audiencias con tecnología de [!DNL Adobe Experience Platform] y activarlas con [!DNL Adobe Campaign] para llegar a su base de clientes en los diferentes canales admitidos por [!DNL Adobe Campaign]. Una vez enviados los mensajes, desean mejorar el perfil del cliente en [!DNL Adobe Experience Platform] con datos de experiencia de [!DNL Adobe Campaign], como envíos, aperturas y clics.

  El resultado son campañas en canales múltiples que son más coherentes en todo el ecosistema de Adobe Experience Cloud y un perfil de cliente enriquecido que se adapta y aprende rápidamente.


* Además de la activación de audiencias en Campaign, puede aprovechar el destino [!DNL Adobe Campaign Managed Services] para incorporar atributos de perfil adicionales vinculados a un perfil en [!DNL Adobe Experience Platform] y que tengan un proceso de sincronización configurado para que se actualicen en la base de datos [!DNL Adobe Campaign].

  Por ejemplo, supongamos que está capturando valores de inclusión y exclusión en [!DNL Adobe Experience Platform]. Con esta conexión, puede incluir estos valores en [!DNL Adobe Campaign] y establecer un proceso de sincronización para que se actualicen de manera regular.

  >[!NOTE]
  >
  >La sincronización de atributos de perfil está disponible para perfiles que ya están presentes en la base de datos [!DNL Adobe Campaign].

[Más información sobre [!DNL Adobe Campaign] la integración con [!DNL Adobe Experience Platform]](https://experienceleague.adobe.com/docs/campaign/campaign-v8/connect/ac-aep.html?lang=es)

## Identidades admitidas {#supported-identities}

*[!DNL Adobe Campaign Managed Cloud Services]* admite la activación de las identidades descritas en la tabla siguiente. Más información sobre [identidades](/help/identity-service/features/namespaces.md).

| Identidad de destino | Descripción | Consideraciones |
|---|---|---|
| external_id | ID de usuario personalizados | Seleccione esta identidad de destino cuando la identidad de origen sea un área de nombres personalizada. Se recomienda utilizar esta identidad y asignarla al ID en la instancia de Campaign que representa al cliente (loyalty_ID, account_ID, customer_ID...) |
| ECID | Experience Cloud ID | Un área de nombres que representa ECID. También se puede hacer referencia a este área de nombres mediante los siguientes alias: &quot;Adobe Marketing Cloud ID&quot;, &quot;[!DNL Adobe Experience Cloud] ID&quot;, &quot;[!DNL Adobe Experience Platform] ID&quot;. Consulte el siguiente documento sobre [ECID](/help/identity-service/features/ecid.md) para obtener más información. |
| email_lc_sha256 | Direcciones de correo electrónico con el algoritmo SHA256 | [!DNL Adobe Experience Platform] admite direcciones de correo electrónico con hash SHA256 y texto sin formato. Si el campo de origen contiene atributos sin hash, marque la opción **[!UICONTROL Apply transformation]** para que [!DNL Experience Platform] ponga en hash automáticamente los datos durante la activación. |
| phone_sha256 | Números de teléfono con hash con el algoritmo SHA256 | Los números de teléfono con hash SHA256 y texto sin formato son compatibles con [!DNL Adobe Experience Platform]. Si el campo de origen contiene atributos sin hash, marque la opción **[!UICONTROL Apply transformation]** para que [!DNL Experience Platform] ponga en hash automáticamente los datos durante la activación. |
| GAID | GOOGLE ADVERTISING ID | Seleccione la identidad de destino GAID cuando su identidad de origen sea un área de nombres GAID. |
| IDFA | Apple ID para anunciantes | Seleccione la identidad de destino IDFA cuando la identidad de origen sea un área de nombres IDFA. |

{style="table-layout:auto"}

## Audiencias compatibles {#supported-audiences}

Esta sección describe qué tipos de audiencias puede exportar a este destino.

| Origen de audiencia | Admitido | Descripción |
|---------|----------|----------|
| [!DNL Segmentation Service] | Sí | Audiencias generadas a través del [servicio de segmentación](../../../segmentation/home.md) de Experience Platform. |
| Todos los demás orígenes de audiencia | No | Esta categoría incluye todos los orígenes de audiencia fuera de las audiencias generadas a través de [!DNL Segmentation Service]. Obtenga información acerca de [varios orígenes de audiencia](/help/segmentation/ui/audience-portal.md#customize). Algunos ejemplos son: <ul><li> audiencias de carga personalizadas [importadas](../../../segmentation/ui/audience-portal.md#import-audience) a Experience Platform desde archivos CSV,</li><li> audiencias de similitud, </li><li> audiencias federadas, </li><li> audiencias generadas en otras aplicaciones de Experience Platform, como [!DNL Adobe Journey Optimizer], </li><li> y más. </li></ul> |

{style="table-layout:auto"}



Audiencias compatibles por tipo de datos de audiencia:

| Tipo de datos de audiencia | Admitido | Descripción | Casos de uso |
|--------------------|-----------|-------------|-----------|
| [Audiencias de personas](/help/segmentation/types/people-audiences.md) | Sí | Basado en perfiles de clientes, lo que le permite dirigirse a grupos específicos de personas para campañas de marketing. | Compradores frecuentes, abandonadores del carro de compras |
| [Audiencias de la cuenta](/help/segmentation/types/account-audiences.md) | No | Segmente a individuos dentro de organizaciones específicas para estrategias de marketing basadas en cuentas. | Marketing B2B |
| [Audiencias potenciales](/help/segmentation/types/prospect-audiences.md) | No | Dirija la actividad a personas que aún no sean clientes, pero que compartan características con la audiencia a la que va dirigida. | Prospección con datos de terceros |
| [Exportaciones de conjuntos de datos](/help/catalog/datasets/overview.md) | No | Colecciones de datos estructurados almacenados en el lago de datos [!DNL Adobe Experience Platform]. | Informes, flujos de trabajo de ciencia de datos |

{style="table-layout:auto"}


## Tipo y frecuencia de exportación {#export-type-frequency}

Consulte la tabla siguiente para obtener información sobre el tipo y la frecuencia de exportación de destino.

| Elemento | Tipo | Notas |
|---------|----------|---------|
| Tipo de exportación | **[!UICONTROL Profile-based]** | Va a exportar todos los miembros de una audiencia, junto con los campos de esquema deseados (por ejemplo: dirección de correo electrónico, número de teléfono, apellidos), tal como se eligió en la pantalla Seleccionar atributos de perfil del [flujo de trabajo de activación de destino](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes). |
| Frecuencia de exportación | **[!UICONTROL Batch]** | Los destinos por lotes exportan archivos a plataformas descendentes en incrementos de tres, seis, ocho, doce o veinticuatro horas. Obtenga más información sobre [destinos basados en archivos por lotes](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## Conectar con el destino {#connect}

>[!IMPORTANT]
>
>Para conectarse al destino, necesita los **[!UICONTROL View Destinations]** y **[!UICONTROL Manage Destinations]** [permisos de control de acceso](/help/access-control/home.md#permissions). Lea la [descripción general del control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Para conectarse a este destino, siga los pasos descritos en el [tutorial de configuración de destino](../../ui/connect-destination.md). En el flujo de trabajo de configuración de destino, rellene los campos enumerados en las dos secciones siguientes.

### Rellenar detalles de destino {#destination-details}

Para configurar los detalles del destino, rellene los campos obligatorios y opcionales a continuación. Un asterisco junto a un campo en la interfaz de usuario indica que el campo es obligatorio.

![[!DNL Adobe Campaign Managed Cloud Services] formulario de detalles de destino que muestra campos de nombre, descripción, selección de instancias, asignación de destino y tipo de sincronización.](../../assets/catalog/email-marketing/adobe-campaign-managed-services/destination-details.png)

* **[!UICONTROL Name]**: un nombre con el cual reconocerá este destino en el futuro.
* **[!UICONTROL Description]**: una descripción que le ayudará a identificar este destino en el futuro.
* **[!UICONTROL Select instance]**: su instancia de marketing **[!DNL Campaign]**.
* **[!UICONTROL Target mapping]**: seleccione la asignación de destino que está utilizando en **[!DNL Adobe Campaign]** para realizar envíos. [Más información](https://experienceleague.adobe.com/docs/campaign/campaign-v8/profiles-and-audiences/add-profiles/target-mappings.html).
* **[!UICONTROL Select sync type]**:

   * **[!UICONTROL Audience sync]**: use esta opción para enviar audiencias de [!DNL Adobe Experience Platform] a [!DNL Adobe Campaign].
   * **[!UICONTROL Profile sync (Update only)]**: use esta opción para llevar los atributos de perfil [!DNL Adobe Experience Platform] a [!DNL Adobe Campaign] y establecer un proceso de sincronización para que se puedan actualizar de forma regular.

### Habilitar alertas {#enable-alerts}

Puede activar alertas para recibir notificaciones sobre el estado del flujo de datos a su destino. Seleccione una alerta de la lista a la que suscribirse para recibir notificaciones sobre el estado del flujo de datos. Para obtener más información sobre las alertas, consulte la guía sobre [suscripción a alertas de destinos mediante la interfaz de usuario](../../ui/alerts.md).

Cuando termine de proporcionar detalles para la conexión de destino, seleccione **[!UICONTROL Next]**.

### Política de gobernanza y medidas coercitivas {#governance}

Seleccione las acciones de marketing aplicables a los datos que desea exportar al destino. Para [!DNL Adobe Campaign], le recomendamos que seleccione la acción de marketing **[!UICONTROL Email Targeting]**.

Para obtener más información acerca de las acciones de marketing, consulte la página [descripción general de las políticas de uso de datos](/help/data-governance/policies/overview.md).

## Activar públicos en este destino {#activate}

>[!IMPORTANT]
>
>* Para activar los datos, necesita los permisos de control de acceso **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** y **[!UICONTROL View Segments]** [5}. ](/help/access-control/home.md#permissions) Lea la [descripción general del control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.
>* Para exportar *identidades*, necesita el **[!UICONTROL View Identity Graph]** [permiso de control de acceso](/help/access-control/home.md#permissions). <br> ![Seleccione el área de nombres de identidad resaltada en el flujo de trabajo para activar audiencias en los destinos.](/help/destinations/assets/overview/export-identities-to-destination.png "Seleccione el área de nombres de identidad resaltada en el flujo de trabajo para activar audiencias en los destinos."){width="100" zoomable="yes"}

Lea [Activar datos de audiencia en destinos de exportación de perfiles por lotes](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-batch-profile-destinations.html) para obtener instrucciones sobre cómo activar datos de audiencia en este destino.

### Asignar atributos e identidades {#map}

Seleccione los campos XDM que desea exportar con los perfiles y asígnelos a los campos [!DNL Adobe Campaign] correspondientes.[Más información sobre la selección de atributos e identidad para los destinos de marketing por correo electrónico](overview.md)

1. Seleccionar campos de origen:

   * Seleccione un **identificador** (por ejemplo: el campo de correo electrónico) como identidad de origen que identifique de forma exclusiva un perfil en [!DNL Adobe Experience Platform] y [!DNL Adobe Campaign].

   * Seleccione todos los demás **atributos de perfil de origen XDM** que necesiten ser exportados a [!DNL Adobe Campaign].

   >[!NOTE]
   >
   >El campo &quot;segmentMembershipStatus&quot; es una asignación necesaria para reflejar el estado segmentMembership. Este campo se añade de forma predeterminada y no se puede modificar ni eliminar.

1. Asigne cada campo con su campo de destino en [!DNL Adobe Campaign]. Los campos de destino disponibles están determinados por la asignación de destino seleccionada al [crear el destino](#destination-details).

1. Identifique atributos obligatorios y claves de deduplicación. Tenga en cuenta que los valores de los atributos marcados como &quot;Obligatorio&quot; o &quot;Clave de anulación de duplicación&quot; no pueden ser nulos.

   * [Atributos obligatorios](../../ui/activate-batch-profile-destinations.md#mandatory-attributes): asegúrese de que todos los registros de perfil contengan los atributos seleccionados. Por ejemplo: todos los perfiles exportados contienen una dirección de correo electrónico. Se recomienda establecer como obligatorio tanto el campo de identidad como el campo utilizado como clave de anulación de duplicación.
   * [Una clave de anulación de duplicación](../../ui/activate-batch-profile-destinations.md#mandatory-attributes) es una clave principal que determina la identidad por la cual los usuarios desean que se dedupliquen sus perfiles.

     >[!IMPORTANT]
     >
     >Asegúrese de que el nombre del atributo de clave de anulación de duplicación coincida con un nombre de columna de la asignación de destino seleccionada.

   ![Pantalla de asignación de atributos que muestra campos de origen XDM asignados a [!DNL Adobe Campaign] campos de destino, con indicadores clave obligatorios y de deduplicación.](../../assets/catalog/email-marketing/adobe-campaign-managed-services/mapping.png)

1. Una vez realizada la asignación, puede revisar y completar la configuración de destino para empezar a enviar datos a **[!DNL Campaign]**.
   [Obtenga información sobre cómo revisar y completar la configuración de destino](/help/destinations/destination-types.md#destination-types-and-categories).

## Datos exportados / Validar exportación de datos {#exported-data}

Una vez activado un destino, puede acceder al trabajo correspondiente y a los datos exportados en Campaign.

### Monitorización de trabajos de exportación de datos {#jobs}

Vaya al menú **[!UICONTROL Administration]** > **[!UICONTROL Audit]** > **[!UICONTROL Audience load jobs]** para supervisar todos los trabajos de exportación activados desde [!DNL Adobe Experience Platform].

![[!DNL Adobe Campaign]: pantalla de trabajos de carga de audiencia que muestra los trabajos de exportación activados desde [!DNL Adobe Experience Platform].](../../assets/catalog/email-marketing/adobe-campaign-managed-services/campaign-jobs.png)

### Acceso a datos exportados {#data}

Para **[!UICONTROL Audience sync]**, puede comprobar la audiencia exportada si navega hasta el menú **[!UICONTROL Profile and target]** > **[!UICONTROL List]** > **[!UICONTROL AEP audiences]**.

![[!DNL Adobe Campaign] vista de lista de audiencias de AEP que muestra las audiencias exportadas de Experience Platform disponibles en Perfil y destino.](../../assets/catalog/email-marketing/adobe-campaign-managed-services/campaign-audiences.png)

Para **[!UICONTROL Profile sync (Update only)]**, los datos se actualizan automáticamente en la base de datos de Campaign para cada perfil dirigido por la audiencia activada en el destino.

## Uso de datos y gobernanza {#data-usage-governance}

Todos los destinos de [!DNL Adobe Experience Platform] cumplen con las políticas de uso de datos al administrar los datos. Para obtener información detallada sobre cómo [!DNL Adobe Experience Platform] aplica el control de datos, lea la [Información general sobre el control de datos](/help/data-governance/home.md).
