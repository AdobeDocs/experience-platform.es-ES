---
title: Acxiom Real ID&trade; Audience Connection
description: Use el destino  [!DNL Acxiom Real ID&trade; Audience Connection] para mejorar y activar audiencias en plataformas como [!DNL Altice], [!DNL Ampersand] y [!DNL Comcast].
source-git-commit: 3aefb36bbf525a5eebe3a9330e25587501167a64
workflow-type: tm+mt
source-wordcount: '1186'
ht-degree: 5%

---


# Destino [!DNL Acxiom Real ID™ Audience Connection]

Use el destino [!DNL Acxiom Real ID Audience Connection] para mejorar las audiencias con la tecnología [Real ID™](https://www.acxiom.com/real-id/real-id/) de [!DNL Acxiom]. A continuación, active esas audiencias en plataformas como [!DNL Altice], [!DNL Ampersand], [!DNL Comcast] y más.

>[!NOTE]
>
>El equipo [!DNL Acxiom] crea y mantiene este conector de destino y esta página de documentación. Para cualquier consulta o solicitud de actualización, comuníquese con [!DNL Acxiom] directamente al [acxiom-adobe-help@acxiom.com](mailto:acxiom-adobe-help@acxiom.com).

Siga estos pasos para crear un conector de destino [!DNL Acxiom Real ID Audience Connection] mediante la interfaz de usuario [!DNL Adobe Experience Platform]. Utilice este conector para crear y distribuir audiencias a destinos seleccionados.

## Casos de uso {#use-cases}

Use este destino si tiene [!DNL Real ID] de [!DNL Acxiom] cargado en [!DNL Real-Time CDP] como identificador. Los siguientes casos de uso muestran cómo se puede usar el destino [!DNL Acxiom Real ID Audience Connection].

### Enviar audiencias de [!DNL Experience Platform] a su cuenta de [!DNL Acxiom] {#send-audiences}

Utilice este conector de destino para enviar audiencias de [!DNL Experience Platform] a su cuenta de [!DNL Acxiom] para la adquisición entre canales.

Por ejemplo, el departamento Operaciones de marketing de una marca de servicios financieros globales está interesado en la adquisición de clientes en canales múltiples a través de varias plataformas publicitarias. Pueden usar el conector de destino [!DNL Acxiom Real ID Audience Connection] para enviar audiencias de [!DNL Experience Platform] a [!DNL Acxiom], mejorar las audiencias con la tecnología [!DNL Real ID] de [!DNL Acxiom] y activar las audiencias en varias plataformas, como [!DNL Altice], [!DNL Ampersand], [!DNL Comcast], etc.

## Requisitos previos {#prerequisites}

Antes de configurar el destino [!DNL Acxiom Real ID Audience Connection], complete los siguientes requisitos previos.

* **Confirmar términos de uso:** Lea y firme el Contrato de términos de uso de [!DNL Acxiom]. Recibirá el vínculo al acuerdo una vez que se haya completado el pedido de ventas ejecutado. Hasta que firme el acuerdo, la tarjeta de destino [!DNL Acxiom Real ID Audience Connection] no aparecerá en el catálogo de destino [!DNL Experience Platform]. Después de aceptar y firmar el acuerdo, [!DNL Adobe] completa la instalación y la tarjeta de destino [!DNL Acxiom Real ID Audience Connection] se vuelve visible.
* **Conozca su ID de organización [!DNL Adobe]:** Se necesita su ID de organización [!DNL Adobe] para completar el contrato de términos de uso. Vea el tema *Organizaciones en Experience Cloud* de [!DNL Adobe] para obtener detalles sobre cómo [ver su ID de organización](https://experienceleague.adobe.com/es/docs/core-services/interface/administration/organizations#concept_EA8AEE5B02CF46ACBDAD6A8508646255).
* **Obtener una licencia para el producto [!DNL Real ID] de [!DNL Acxiom]:** Una vez que obtenga una licencia, haga que [!DNL Real ID] de [!DNL Acxiom] esté disponible en [!DNL Real-Time CDP]. Consulte [Mejora de datos de Acxiom](/help/destinations/catalog/data-partner/acxiom-data-enhancement.md) para obtener más información.

## Identidades admitidas {#supported-identities}

El destino de conexión de audiencia [!DNL Real ID] de [!DNL Acxiom] admite las siguientes activaciones de identidad. Más información sobre [identidades](/help/identity-service/features/namespaces.md).

| Identidad de destino | Descripción | Consideraciones |
| --------------- | ----------- | -------------- |
| [!DNL Real ID] | [!DNL Real ID] | Asigne un campo de origen a esta identidad de destino. Su campo de origen puede ser un [!DNL Acxiom] [!DNL Real ID] o un identificador personalizado. |

{style="table-layout:auto"}

## Audiencias compatibles {#supported-audiences}

Esta sección describe qué tipos de audiencias puede exportar a este destino.

| Origen de audiencia | Admitido | Descripción |
| --------------- | --------- | ----------- |
| [!DNL Segmentation Service] | Sí | Audiencias generadas a través del [!DNL Experience Platform] [servicio de segmentación](/help/segmentation/home.md). |
| Todos los demás orígenes de audiencia | Sí | Esta categoría incluye todos los orígenes de audiencia fuera de las audiencias generadas a través de [!DNL Segmentation Service]. Obtenga información acerca de [varios orígenes de audiencia](/help/segmentation/ui/audience-portal.md#customize). Algunos ejemplos son: <ul><li>audiencias de carga personalizadas [importadas](/help/segmentation/ui/audience-portal.md#import-audience) en [!DNL Experience Platform] desde archivos CSV,</li><li>audiencias de similitud,</li><li>audiencias federadas,</li><li>audiencias generadas en otras [!DNL Experience Platform] aplicaciones como [!DNL Adobe Journey Optimizer],</li><li>y más.</li></ul> |

{style="table-layout:auto"}

### Audiencias compatibles por tipo de datos {#supported-audiences-data-type}

En la tabla siguiente se describen los tipos de datos de audiencia que se pueden exportar a este destino.

| Tipo de datos de audiencia | Admitido | Descripción | Casos de uso |
| -------------------- | --------- | ----------- | --------- |
| [Audiencias de personas](/help/segmentation/types/people-audiences.md) | Sí | Basado en perfiles de clientes. Utilícelos para dirigirse a grupos específicos de personas para campañas de marketing. | Compradores frecuentes, abandonadores del carro de compras |
| [Audiencias de la cuenta](/help/segmentation/types/account-audiences.md) | No | Segmente a individuos dentro de organizaciones específicas para estrategias de marketing basadas en cuentas. | Marketing B2B |
| [Audiencias potenciales](/help/segmentation/types/prospect-audiences.md) | No | Dirija la actividad a personas que aún no sean clientes, pero que compartan características con la audiencia a la que va dirigida. | Prospección con datos de terceros |
| [Exportaciones de conjuntos de datos](/help/catalog/datasets/overview.md) | No | Colecciones de datos estructurados almacenados en el lago de datos [!DNL Adobe Experience Platform]. | Informes, flujos de trabajo de ciencia de datos |

{style="table-layout:auto"}

## Tipo y frecuencia de exportación {#export-type-frequency}

En la tabla siguiente se describe el tipo y la frecuencia de exportación de destino.

| Elemento | Tipo | Notas |
| ---- | ---- | ----- |
| Tipo de exportación | **[!UICONTROL Audience export]** | Exporta todos los miembros de una audiencia con los identificadores utilizados en el destino [!DNL Acxiom Real ID Audience Connection]. |
| Frecuencia de exportación | **[!UICONTROL Batch]** | Los destinos por lotes exportan archivos a plataformas descendentes en incrementos de tres, seis, ocho, doce o veinticuatro horas. Obtenga más información sobre [destinos basados en archivos por lotes](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## Destinos admitidos {#supported-destinations}

Activar audiencias en las siguientes plataformas a través del destino [!DNL Acxiom Real ID Audience Connection].

* [!DNL Altice]
* [[!DNL Amazon]](#amazon)
* [!DNL Ampersand]
* [!DNL Comcast]
* [!DNL Cox]
* [[!DNL Facebook]](#facebook)
* [[!DNL LG Ads]](#lg-ads)
* [[!DNL Pinterest]](#pinterest)
* [!DNL Spectrum]
* [!DNL Viant]
* [[!DNL Vizio]](#vizio)

## Conectar con el destino {#connect}

[!DNL Experience Platform] administra automáticamente la autenticación de su destino [!DNL Acxiom Real ID Audience Connection].

>[!IMPORTANT]
>
>Para conectarse al destino, necesita los **[!UICONTROL View Destinations]** y **[!UICONTROL Manage Destinations]** [permisos de control de acceso](/help/access-control/home.md#permissions). Lea la [descripción general del control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

## Configuración específica del destino {#destination-settings}

Algunos [!DNL Acxiom Real ID Audience Connection] destinos requieren información adicional. Las secciones siguientes proporcionan instrucciones detalladas sobre cómo configurar estas opciones.

### [!DNL Amazon] {#amazon}

Para configurar los detalles del destino, complete los siguientes campos.

* **[!UICONTROL Publisher Account ID]**: escriba el id. de cuenta de editor asociado a este destino.

  ![Captura de pantalla del panel de detalles de destino [!DNL Amazon] que muestra el campo Identificador de cuenta de publicador.](../../assets/catalog/advertising/acxiom-real-id-audience-connection/real_id_amazon_destination_details.png){zoomable="yes"}

### [!DNL Facebook] {#facebook}

Para configurar los detalles del destino, complete los siguientes campos.

* **[!UICONTROL Destination Account ID]**: escriba el identificador de la cuenta de destino para este destino.

  ![Captura de pantalla del panel de detalles de destino [!DNL Facebook] que muestra el campo ID de cuenta de destino.](../../assets/catalog/advertising/acxiom-real-id-audience-connection/real_id_facebook_destination_details.png){zoomable="yes"}

### [!DNL LG Ads] {#lg-ads}

Para configurar los detalles del destino, complete los siguientes campos.

* **[!UICONTROL Segment Category]**: categoría o vertical de destino en la que se encuentra el segmento. Ejemplo: servicios financieros, automoción o salud.

  ![Captura de pantalla del panel de detalles de destino [!DNL LG Ads] que muestra el campo Categoría del segmento.](../../assets/catalog/advertising/acxiom-real-id-audience-connection/real_id_lg_ads_destination_details.png){zoomable="yes"}

### [!DNL Pinterest] {#pinterest}

Para configurar los detalles del destino, complete los siguientes campos.

* **[!UICONTROL Destination Account ID]**: escriba el identificador de la cuenta de destino para este destino.

  ![Captura de pantalla del panel de detalles de destino [!DNL Pinterest] que muestra el campo ID de cuenta de destino.](../../assets/catalog/advertising/acxiom-real-id-audience-connection/real_id_pinterest_destination_details.png){zoomable="yes"}

### [!DNL Vizio] {#vizio}

Para configurar los detalles del destino, complete los siguientes campos.

* **[!UICONTROL Advertiser Name]**: escriba el nombre del anunciante para este destino.

  ![Captura de pantalla del panel de detalles de destino [!DNL Vizio] que muestra el campo Nombre del anunciante.](../../assets/catalog/advertising/acxiom-real-id-audience-connection/real_id_vizio_destination_details.png){zoomable="yes"}

## Activar públicos en este destino {#activate}

Lea [Activar datos de audiencia en destinos de exportación de perfiles por lotes](/help/destinations/ui/activate-batch-profile-destinations.md) para obtener instrucciones sobre cómo activar audiencias en este destino.

>[!IMPORTANT]
>
>* Para activar los datos, necesita los permisos de control de acceso **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** y **[!UICONTROL View Segments]** [5}. ](/help/access-control/home.md#permissions)Lea la [descripción general del control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.
>* Para exportar *identidades*, necesita el **[!UICONTROL View Identity Graph]** [permiso de control de acceso](/help/access-control/home.md#permissions). <br> ![Seleccione el área de nombres de identidad resaltada en el flujo de trabajo para activar audiencias en los destinos.](/help/destinations/assets/overview/export-identities-to-destination.png){width="100" zoomable="yes"}

>[!NOTE]
>
>El destino [!DNL Acxiom Real ID Audience Connection] solo admite exportaciones de archivos completas.

### Asignar atributos e identidades {#map}

Para que el destino [!DNL Acxiom Real ID Audience Connection] reciba correctamente los datos de audiencia, asigne el campo de origen de [!DNL Experience Platform] al campo de destino [!DNL Acxiom Real ID Audience Connection] correcto.

El campo de destino **[!UICONTROL Real ID]** se rellena automáticamente en el paso de asignación. Asigne su campo de origen a él: un área de nombres de identificador personalizado o un [!DNL Acxiom] [!DNL Real ID] real almacenado en el esquema de perfil.

| Nombre del campo | Descripción | Requerido |
| ---------- | ----------- | -------- |
| [!DNL Real ID] | Un(a) [!DNL Real ID] es un identificador alfanumérico único de 36 bytes del gráfico de resolución de identidad propiedad de [!DNL Acxiom]. Es un identificador que representa a una persona, un hogar o una dirección. | Sí |

{style="table-layout:auto"}

En la columna **[!UICONTROL Source Field]**, escriba el nombre del atributo de origen que desea asignar al campo de destino **[!UICONTROL Real ID]**. O seleccione **[!UICONTROL Select source field]** para examinar los campos de origen disponibles. Luego seleccione **[!UICONTROL Next]**.

![Captura de pantalla de la pantalla de asignación que muestra la columna [!UICONTROL Source Field] y el panel [!UICONTROL Select source field].](../../assets/catalog/advertising/acxiom-real-id-audience-connection/real_id_mapping_screen.png){zoomable="yes"}

Si no usa el esquema estándar de [!DNL Adobe], consulte la [guía de la interfaz de usuario del servicio de consultas](/help/query-service/ui/overview.md) para rellenar el esquema estándar de [!DNL Adobe] con sus nombres de campo.

### Revisar el destino {#review}

Después de completar todos los pasos, revise el estado de la conexión de destino y los detalles de la audiencia antes de activarla. Las audiencias seleccionadas aparecen en una lista. Cada audiencia es una llamada independiente a la API [!DNL Acxiom Real ID Audience Connection].

Cuando los resultados parezcan correctos, seleccione **[!UICONTROL Finish]** para activar el destino.

![Captura de pantalla de la pantalla de revisión que muestra el estado de conexión de destino y las audiencias seleccionadas antes de la activación.](../../assets/catalog/advertising/acxiom-real-id-audience-connection/real_id_review_audience.png){zoomable="yes"}

## Solución de problemas {#troubleshooting}

Si el representante de destino no puede encontrar la audiencia, póngase en contacto con el representante de [!DNL Adobe] para obtener ayuda.

Proporcione la siguiente información a su representante de [!DNL Adobe]:

* Nombre del público
* Nombre del destino
* Fecha de activación de audiencia
* Nombre de archivo exportado

## Próximos pasos {#next-steps}

Se ha activado correctamente una audiencia en la plataforma de destino seleccionada. A continuación, póngase en contacto con el representante de la plataforma de destino para comenzar a configurar la campaña.

## Uso de datos y gobernanza {#data-usage-governance}

Todos los destinos de [!DNL Adobe Experience Platform] cumplen con las políticas de uso de datos al administrar los datos. Para obtener información detallada sobre cómo [!DNL Adobe Experience Platform] aplica el control de datos, lea la [Información general sobre el control de datos](/help/data-governance/home.md).
