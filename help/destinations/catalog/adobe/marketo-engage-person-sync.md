---
title: Sincronización de personas de Marketo Engage
description: Utilice el conector de sincronización de personas de Marketo Engage para transmitir las actualizaciones de una audiencia de persona a los registros correspondientes de su Marketo Engage.
last-substantial-update: 2025-01-14T00:00:00Z
badgeBeta: label="Beta" type="Informative"
exl-id: 2c909633-b169-4ec8-9f58-276395cb8df2
source-git-commit: 2dd4ae4146f7c1c5228e22d24ff2ba31010adedb
workflow-type: tm+mt
source-wordcount: '1223'
ht-degree: 6%

---

# Conexión de sincronización de persona de Marketo Engage {#marketo-engage-person-sync}

>[!IMPORTANT]
>
>Este conector de destino está en versión beta y solo está disponible para clientes seleccionados. Para solicitar acceso, póngase en contacto con su representante de Adobe.

>[!IMPORTANT]
>
>La tarjeta de destino **[!UICONTROL Marketo Engage Person Sync]** quedará obsoleta en **octubre de 2025**.
>
>Para garantizar una transición sin problemas al nuevo destino **[[!UICONTROL Marketo Engage]](marketo-engage-connection.md)**, revise los siguientes puntos clave y las acciones necesarias:
>
>* Todos los usuarios deben **dejar de usar el destino de sincronización de personas de Marketo Engage** y migrar al nuevo destino **[[!UICONTROL Marketo Engage]](marketo-engage-connection.md)** para octubre de 2025.
>* **Los flujos de datos existentes no se migrarán automáticamente.** Debe [configurar una nueva conexión](marketo-engage-connection.md#connect-to-the-destination) al nuevo destino **[!UICONTROL Marketo Engage]** y activar sus audiencias allí.


## Información general {#overview}

Utilice el conector de sincronización de personas de Marketo Engage para transmitir las actualizaciones de las audiencias de persona a los registros correspondientes de la instancia de Marketo Engage.

>[!IMPORTANT]
>
>El [Conector de sincronización de audiencia de Marketo V2](/help/destinations/catalog/adobe/marketo-engage.md) no se debe usar en el modo de creación junto con el Conector de sincronización de actualización de perfil

## Identidades y atributos admitidos {#support-identities-and-attributes}

### Identidades admitidas {#supported-identities}

| Identidad de destino | Descripción |
| --------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Correo electrónico | Un área de nombres que representa una dirección de correo electrónico. Este tipo de área de nombres suele estar asociado a una sola persona y, por lo tanto, se puede utilizar para identificarla en diferentes canales. |

{style="table-layout:auto"}

### Atributos admitidos {#supported-attributes}

Puede asignar atributos de Experience Platform a cualquiera de los atributos a los que su organización tiene acceso en Marketo. En Marketo, puede usar la solicitud [Describir API](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Leads/operation/describeUsingGET_6) para recuperar los campos de atributos a los que su organización tiene acceso.

## Audiencias compatibles {#supported-audiences}

Esta sección describe qué tipos de audiencias puede exportar a este destino.

| Origen de audiencia | Admitido | Descripción |
| -------------------- | :-------: | ------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Servicio de segmentación | Sí | Audiencias generadas a través del [servicio de segmentación](https://experienceleague.adobe.com/es/docs/experience-platform/segmentation/home) de Experience Platform. |
| Todos los demás orígenes de audiencia | Sí | Esta categoría incluye todos los orígenes de audiencia fuera de las audiencias generadas a través de [!DNL Segmentation Service]. Obtenga información acerca de [varios orígenes de audiencia](/help/segmentation/ui/audience-portal.md#customize). Algunos ejemplos son: <ul><li> audiencias de carga personalizadas [importadas](../../../segmentation/ui/audience-portal.md#import-audience) a Experience Platform desde archivos CSV,</li><li> audiencias de similitud, </li><li> audiencias federadas, </li><li> audiencias generadas en otras aplicaciones de Experience Platform, como Adobe Journey Optimizer, </li><li> y más. </li></ul> |

{style="table-layout:auto"}

Audiencias compatibles por tipo de datos de audiencia:

| Tipo de datos de audiencia | Admitido | Descripción | Casos de uso |
|--------------------|-----------|-------------|-----------|
| [Audiencias de personas](/help/segmentation/types/people-audiences.md) | Sí | Basado en perfiles de clientes, lo que le permite dirigirse a grupos específicos de personas para campañas de marketing. | Compradores frecuentes, abandonadores del carro de compras |
| [Audiencias de la cuenta](/help/segmentation/types/account-audiences.md) | No | Segmente a individuos dentro de organizaciones específicas para estrategias de marketing basadas en cuentas. | Marketing B2B |
| [Audiencias potenciales](/help/segmentation/types/prospect-audiences.md) | No | Dirija la actividad a personas que aún no sean clientes, pero que compartan características con la audiencia a la que va dirigida. | Prospección con datos de terceros |
| [Exportaciones de conjuntos de datos](/help/catalog/datasets/overview.md) | No | Recopilaciones de datos estructurados almacenados en el lago de datos de Adobe Experience Platform. | Informes, flujos de trabajo de ciencia de datos |

{style="table-layout:auto"}

## Tipo y frecuencia de exportación {#export-type-and-frequency}

Consulte la tabla siguiente para obtener información sobre el tipo y la frecuencia de exportación de destino.

| Elemento | Tipo | Notas |
| ---------------- | --------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Frecuencia de exportación | Streaming | Los destinos de streaming son conexiones basadas en API &quot;siempre activadas&quot;. Tan pronto como se actualiza un perfil en Experience Platform basado en la evaluación de audiencias, el conector envía la actualización de forma descendente a la plataforma de destino. Más información sobre [destinos de streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Configurar destino {#set-up-destination}

>[!IMPORTANT]
>
>* Para conectarse al destino, necesita los **[!UICONTROL View Destinations]** y **[!UICONTROL Manage Destinations]** [permisos de control de acceso](/help/access-control/home.md#permissions).

Si su empresa tiene acceso a varias organizaciones, asegúrese de utilizar la misma organización tanto en Marketo Engage como en Real-Time CDP, donde está configurando el conector de destino en Marketo.  Si ya ha configurado un destino, puede seleccionar una cuenta existente de Marketo para usarla con la nueva configuración.  Si no es así, haga clic en el indicador Connector to Destination, que le permitirá establecer el nombre, la descripción y el ID de Marketo Munchkin del destino deseado.  El Munchkin ID de su instancia de Marketo se encuentra en el menú Administración->Munchkin.

>[!IMPORTANT]
>
>El usuario que configura el destino debe tener el permiso [Editar persona](https://experienceleague.adobe.com/es/docs/marketo/using/product-docs/administration/users-and-roles/descriptions-of-role-permissions#access-database) en la instancia y partición de Marketo.

![Conectar con destino](../../assets/catalog/adobe/marketo-engage-person-sync/connect-to-destination.png)

* **[!UICONTROL Name]**: un nombre con el cual reconocerá este destino en el futuro.
* **[!UICONTROL Description]**: una descripción que le ayudará a identificar este destino en el futuro.
* **[!UICONTROL Munchkin ID]**: el ID de Munchkin es el identificador único de una instancia de Marketo específica.
* **[!UICONTROL Partition]**: concepto de Marketo Engage que se usa para separar los registros de posibles clientes por motivo de negocio
* **[!UICONTROL First searchable field]**: campo en el que se deduplicará. El campo debe estar presente en cada registro de posibles clientes de la entrada. El valor predeterminado es correo electrónico
* **[!UICONTROL First searchable field]**: campo secundario en el que se va a deduplicar. El campo debe estar presente en cada registro de posibles clientes de la entrada. Opcional

Una vez seleccionada la instancia, también debe seleccionar la partición de posible cliente con la que desea integrar la configuración. Una [partición de posibles clientes](https://experienceleague.adobe.com/es/docs/marketo/using/product-docs/administration/workspaces-and-person-partitions/understanding-workspaces-and-person-partitions) es un concepto de Marketo Engage que se usa para separar los registros de posibles clientes por motivo de negocio, como una marca o una región de ventas. Si su suscripción a Marketo no tiene la función Espacios de trabajo y particiones, o si no se han creado particiones adicionales en su suscripción, solo estará disponible la partición predeterminada. Una sola configuración solo puede actualizar los registros de posibles clientes que existan en su partición configurada.

>[!IMPORTANT]
>
>Después de activar una audiencia en el destino de Marketo por primera vez, rellenar los perfiles que ya existían en la audiencia antes de la activación del destino de Marketo puede tardar *hasta 24 horas*. En adelante, cada vez que los perfiles se añadan a la audiencia, se añadirán a Marketo inmediatamente.

### Campos de deduplicación {#deduplication-fields}

Al enviar actualizaciones a Marketo Engage, los registros se seleccionan en función de la partición seleccionada y de uno o dos campos seleccionados por el usuario. Si el destino está configurado con la partición de Norteamérica y tiene los campos Dirección de correo electrónico y Nombre de la empresa configurados como campos de anulación de duplicación, los tres campos deben coincidir para aplicar los cambios a un registro existente. Por ejemplo:

* El destino se configura con la partición de Norteamérica
* La persona con correo electrónico <test@example.com> y nombre de compañía Example Inc. de Experience Platform coincide con la audiencia de destino
* A menos que ya exista un registro con esos valores en la partición de Norteamérica en Marketo, se creará un nuevo registro de posibles clientes

Si no se encuentra ningún registro de posible cliente coincidente, se creará un nuevo registro.

![Detalles del destino](../../assets/catalog/adobe/marketo-engage-person-sync/destination-details.png)

## Activar audiencias {#activate-audiences}

>[!IMPORTANT]
>
>* Para activar los datos, necesita los permisos de control de acceso **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** y **[!UICONTROL View Segments]** [5&rbrace;. &#x200B;](/help/access-control/home.md#permissions) Lea la [descripción general del control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Lea [Activar audiencias en destinos de flujo continuo](/help/destinations/ui/activate-segment-streaming-destinations.md) para obtener instrucciones sobre cómo activar audiencias en este destino.

En el paso Activar audiencias, podrá seleccionar entre las audiencias de persona que sean visibles para usted.

![Activar audiencias](../../assets/catalog/adobe/marketo-engage-person-sync/activate-audiences.png)

## Asignación de campos {#field-mapping}

Para que los cambios en un atributo de persona determinado se envíen a Marketo Engage, el campo debe asignarse de un campo de Real-Time CDP a un campo de Marketo.

![Asignación de campos](../../assets/catalog/adobe/marketo-engage-person-sync/field-mapping.png)

Los tipos de datos de Experience Platform y los tipos de datos de Marketo se pueden asignar de las siguientes maneras:

| Tipo de datos de Experience Platform | Tipo de datos de Marketo |
| ----------------------------- | ------------------------------------ |
| Cadena | Cadena, Área De Texto, Url, Teléfono, Correo Electrónico |
| Enumeración | Cadena |
| Fecha | Fecha |
| Fecha y hora | Datetime |
| Número entero | Número entero |
| Corto | Número entero |
| Largo | Flotante |
| Duplicada | Moneda, Flotante, Porcentaje |
| Booleano | Booleano |
| Matriz | No compatible |
| Objeto | No compatible |
| Mapa | No compatible |
| Byte | No compatible |

{style="table-layout:auto"}

En algunos casos, es deseable permitir integraciones para establecer el valor de un campo si no hay ninguno, al mismo tiempo que evita que las integraciones realicen actualizaciones en campos que ya tienen un valor.  Si necesita evitar que el conector de destino sobrescriba los valores existentes en la instancia de Marketo Engage, puede configurar los campos para bloquear las actualizaciones en la sección Administración->Administración de campos de la instancia de Marketo y alternar el tipo de origen de Adobe Experience Platform.

![Bloquear actualizaciones de campos](../../assets/catalog/adobe/marketo-engage-person-sync/block-field-updates.png)

![Bloquear actualizaciones de campos](../../assets/catalog/adobe/marketo-engage-person-sync/block-field-updates-2.png)

## Uso de datos y administración {#data-usage-and-governance}

Todos los destinos de Adobe Experience Platform cumplen con las políticas de uso de datos al administrar los datos. Para obtener información detallada sobre cómo Adobe Experience Platform aplica el control de datos, consulte la [descripción general del control de datos](/help/data-governance/home.md).
