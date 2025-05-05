---
title: Mejora de datos de Acxiom
description: Utilice este conector para activar perfiles de Adobe de origen en Real-Time CDP a Acxiom para el enriquecimiento de datos y su uso en todos los canales de marketing. A continuación, puede utilizar la fuente Acxiom para importar los perfiles con datos mejorados y trabajar con ellos en Real-Time CDP.
last-substantial-update: 2024-03-14T00:00:00Z
badge: Beta
exl-id: 59edc43d-ae8e-4c3d-820c-b5be1c4483f9
source-git-commit: c35b43654d31f0f112258e577a1bb95e72f0a971
workflow-type: tm+mt
source-wordcount: '1346'
ht-degree: 3%

---

# [!DNL Acxiom Data Enhancement] conexión de destino

>[!NOTE]
>
>El destino [!DNL Acxiom Data Enhancement] se encuentra en la versión beta.  El equipo de Acxiom crea y mantiene este conector de destino y esta página de documentación. Para cualquier consulta o solicitud de actualización, póngase en contacto con ellos directamente en acxiom-adobe-help@acxiom.com.

## Información general {#overview}

Utilice el conector [!DNL Acxiom Data Enhancement] para proporcionar datos descriptivos adicionales a los perfiles de sus clientes para su uso en aplicaciones de análisis, segmentación y segmentación. Con cientos de elementos disponibles, esto le permite segmentar y modelar mejor los datos, lo que da como resultado un direccionamiento y un modelado predictivo más precisos.

![Diagrama de marketing para exportar datos de origen a Acxiom y, a continuación, volver a importar datos enriquecidos en Real-Time CDP](/help/destinations/assets/catalog/data-partner/acxiom/marketing-workflow-data-enhancement.png)

Este tutorial proporciona los pasos para crear una conexión de destino y un flujo de datos de [!DNL Acxiom Data Enhancement] mediante la interfaz de usuario de Adobe Experience Platform. Este conector se utiliza para entregar datos al servicio de mejora Acxiom mediante Amazon S3 como punto de caída.

![El catálogo de destino con el destino Acxiom seleccionado.](../../assets/catalog/data-partner/acxiom/image-destination-enhancement-catalog.png)

## Casos de uso {#use-cases}

Para ayudarle a comprender mejor cómo y cuándo debe utilizar el destino [!DNL Acxiom Data Enhancement], aquí hay casos de uso de ejemplo que los clientes de Adobe Experience Platform pueden solucionar mediante este destino.

### Mejore los datos de clientes {#enhance-customer-data}

Los profesionales de marketing deben utilizar este conector para mejorar la eficacia de sus estrategias de divulgación añadiendo elementos descriptivos seleccionados a sus perfiles de cliente y utilizándolos para dirigir mejor las campañas.

Por ejemplo, como experto en marketing, es posible que desee profundizar en el conocimiento de las audiencias existentes enriqueciendo sus perfiles con datos adicionales. Al hacerlo, mejorará las estrategias de segmentación y segmentación, lo que dará lugar a un aumento en la personalización y conversión de campañas.

El caso de uso se ejecuta mediante una combinación de conectores de origen y destino.

Para empezar, debe exportar los registros de cliente existentes para enriquecerlos con este conector de destino. El servicio de Acxiom buscaría el archivo, lo recuperaría, lo enriquecería con los datos de Acxiom y generaría un archivo.

El cliente usaría la tarjeta de origen [Acxiom Data Ingestion](/help/sources/connectors/data-partners/acxiom-data-ingestion.md) correspondiente para volver a ingerir los perfiles de clientes hidratados en Adobe Real-Time CDP.

## Requisitos previos {#prerequisites}

>[!IMPORTANT]
>
>* Para conectarte al destino, necesitas los **[[!UICONTROL permisos de &#x200B;]](/help/access-control/home.md#permissions)Ver destinos&rbrack;** y **[!UICONTROL Administrar destinos]**, **[!UICONTROL Activar destinos]**, **[!UICONTROL Ver perfiles]** y **[!UICONTROL Ver segmentos]** &lbrack;permisos de control de acceso. Lea la [descripción general del control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.
>* Para exportar *identidades*, necesita el **[[!UICONTROL permiso de control de acceso]](/help/access-control/home.md#permissions) de&rbrack;** Ver gráfico de identidad&lbrack;. <br> ![Seleccione el área de nombres de identidad resaltada en el flujo de trabajo para activar audiencias en los destinos.](/help/destinations/assets/overview/export-identities-to-destination.png "Seleccione el área de nombres de identidad resaltada en el flujo de trabajo para activar audiencias en los destinos."){width="100" zoomable="yes"}

## Audiencias compatibles {#supported-audiences}

Esta sección describe qué tipo de audiencias puede exportar a este destino.

| Origen de audiencia | Admitido | Descripción |
|-----------------------------|-----------|---------------------------------------------------------------------------------------------------------------------|
| [!DNL Segmentation Service] | ✓ | Audiencias generadas a través del Experience Platform [Servicio de segmentación](../../../segmentation/home.md). |
| Cargas personalizadas | x | Las audiencias [importadas](../../../segmentation/ui/audience-portal.md#import-audience) en el Experience Platform desde archivos CSV. |

{style="table-layout:auto"}


## Tipo y frecuencia de exportación {#export-type-frequency}

Consulte la tabla siguiente para obtener información sobre el tipo y la frecuencia de exportación de destino.

| Elemento | Tipo | Notas |
|------------------|--------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Tipo de exportación | **[!UICONTROL Basado en perfil]** | Va a exportar todos los miembros de un segmento, junto con los campos de esquema deseados (por ejemplo: dirección de correo electrónico, número de teléfono, apellidos), tal como se eligió en la pantalla Seleccionar atributos de perfil del [flujo de trabajo de activación de destino](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes). |
| Frecuencia de exportación | **[!UICONTROL Lote]** | Los destinos por lotes exportan archivos a plataformas descendentes en incrementos de tres, seis, ocho, doce o veinticuatro horas. Obtenga más información sobre [destinos basados en archivos por lotes](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## Conexión al destino {#connect}

>[!IMPORTANT]
>
>Para conectarse al destino, necesita los **[[!UICONTROL permisos de control de acceso]](/help/access-control/home.md#permissions) de Ver destinos&rbrack;** y **[!UICONTROL Administrar y activar destinos de conjuntos de datos]**&lbrack;5&rbrace;. Lea la [descripción general del control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Para conectarse a este destino, siga los pasos descritos en el [tutorial de configuración de destino](../../ui/connect-destination.md). En el flujo de trabajo de configuración de destino, rellene los campos enumerados en las dos secciones siguientes.

### Autenticarse en el destino {#authenticate}

Para autenticarse en el destino, rellene los campos obligatorios y seleccione **[!UICONTROL Conectar con destino]**.

Para acceder al bloque en Experience Platform, debe proporcionar valores válidos para las siguientes credenciales:

| Credencial | Descripción |
|---------------|----------------------------------------------------------------------------------------------------------|
| Clave de acceso de S3 | ID de clave de acceso para el bloque. Puede recuperar este valor del equipo [!DNL Acxiom]. |
| Clave secreta de S3 | El ID de clave secreta de su cubo. Puede recuperar este valor del equipo [!DNL Acxiom]. |
| Nombre del segmento | Este es el espacio en el que se compartirán los archivos. Puede recuperar este valor del equipo [!DNL Acxiom]. |

### Nueva cuenta

Para definir una nueva ubicación de Acxiom Managed S3:

![Nueva cuenta](../../assets/catalog/data-partner/acxiom/image-destination-new-account.png)

### Cuenta existente

Las cuentas ya definidas con el destino [!DNL Acxiom Data Enhancement] aparecen en una lista emergente. Cuando se selecciona, puede ver los detalles de la cuenta en el carril derecho. Vea el ejemplo desde la interfaz de usuario cuando vaya a **[!UICONTROL Destinos]** > **[!UICONTROL Cuentas]**;

![Cuenta existente](../../assets/catalog/data-partner/acxiom/image-destination-enhancement-account.png)

### Rellenar detalles de destino {#destination-details}

Para configurar los detalles del destino, rellene los campos obligatorios y opcionales a continuación. Un asterisco junto a un campo en la interfaz de usuario indica que el campo es obligatorio.

![Detalle del destino](../../assets/catalog/data-partner/acxiom/image-destination-details.png)

* **Nombre (obligatorio)** - El nombre en el que se guardará el destino
* **Descripción** - Breve explicación del propósito del destino
* **Nombre del contenedor (obligatorio)** - Nombre del contenedor de Amazon S3 configurado en S3
* **Ruta de acceso a la carpeta (obligatoria)**: si se usan subdirectorios en un bloque, se debe definir una ruta de acceso o &#39;/&#39; para hacer referencia a la ruta de acceso raíz.
* **Tipo de archivo**: seleccione el formato que el Experience Platform debe usar para los archivos exportados. En este momento, el único tipo de archivo que esperará el procesamiento de Acxiom es CSV

>[!IMPORTANT]
>
>Al seleccionar la opción CSV, se presentarán las opciones *Delimitador*, *Carácter de cita*, *Carácter de escape*, *Valor vacío*, *Valor nulo*, *Formato de compresión* y *Incluir archivo de manifiesto*. El siguiente documento explica esta configuración con más detalle [configurar las opciones de formato](../../ui/batch-destinations-file-formatting-options.md).

![Opciones de CSV](../../assets/catalog/data-partner/acxiom/image-destination-csv-options.png)

### Habilitar alertas {#enable-alerts}

Puede activar alertas para recibir notificaciones sobre el estado del flujo de datos a su destino. Seleccione una alerta de la lista a la que suscribirse para recibir notificaciones sobre el estado del flujo de datos. Para obtener más información sobre las alertas, consulte la guía sobre [suscripción a alertas de destinos mediante la interfaz de usuario](../../ui/alerts.md).

Cuando termine de proporcionar detalles para la conexión de destino, seleccione **[!UICONTROL Siguiente]**.

## Activar públicos en este destino {#activate}

>[!IMPORTANT]
>
>* Para activar los datos, necesita los **[!UICONTROL permisos de control de acceso]**, **[!UICONTROL Activar destinos]**, **[!UICONTROL Ver perfiles]** y **[!UICONTROL Ver segmentos]**&#x200B;[para ](/help/access-control/home.md#permissions). Lea la [descripción general del control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.
>* Para exportar *identidades*, necesita el **[[!UICONTROL permiso de control de acceso]](/help/access-control/home.md#permissions) de&rbrack;** Ver gráfico de identidad&lbrack;. <br> ![Seleccione el área de nombres de identidad resaltada en el flujo de trabajo para activar audiencias en los destinos.](/help/destinations/assets/overview/export-identities-to-destination.png "Seleccione el área de nombres de identidad resaltada en el flujo de trabajo para activar audiencias en los destinos."){width="100" zoomable="yes"}

Lea [Activar datos de audiencia en destinos de exportación de perfiles por lotes](/help/destinations/ui/activate-batch-profile-destinations.md) para obtener instrucciones sobre cómo activar audiencias en este destino.

### Sugerencias de asignación

El procesamiento correcto de archivos en el lado Acxiom requiere elementos de nombre y dirección. Aunque no todos los elementos son necesarios, proporcionar todo lo posible ayudará a que la coincidencia tenga éxito.

En la tabla siguiente se proporcionan sugerencias de asignación. Se enumeran los atributos del lado del destino que utiliza el procesamiento Acxiom y a los que los clientes pueden asignar atributos de perfil. Trate estos elementos como sugerencias, ya que no todos los elementos son necesarios y los valores de origen dependerán de las necesidades de la cuenta.

| Campo de destino | Descripción de Source |
|--------------|-------------------------------------------------------------|
| name | El valor `person.name.fullName` en el Experience Platform. |
| firstName | El valor `person.name.firstName` en el Experience Platform. |
| lastName | El valor `person.name.lastName` en el Experience Platform. |
| dirección1 | El valor `mailingAddress.street1` en el Experience Platform. |
| dirección2 | El valor `mailingAddress.street2` en el Experience Platform. |
| ciudad | El valor `mailingAddress.city` en el Experience Platform. |
| estado | El valor `mailingAddress.state` en el Experience Platform. |
| zip | El valor `mailingAddress.postalCode` en el Experience Platform. |

>[!NOTE]
>
>Si asigna campos adicionales no enumerados anteriormente en el flujo de datos, estos se incluirán en la exportación de datos, pero el procesamiento Acxiom los ignorará.

## Validar exportación de datos {#exported-data}

Para comprobar si los datos se han exportado correctamente, compruebe el bloque [!DNL Amazon S3 Storage] y asegúrese de que los archivos exportados contienen las poblaciones de perfiles esperadas.

## Pasos siguientes

Al seguir este tutorial, ha creado correctamente un flujo de datos para exportar datos de perfil del Experience Platform a su ubicación de S3 administrada de [!DNL Acxiom]. A continuación, debe ponerse en contacto con su representante de Acxiom con el nombre de la cuenta, los nombres de archivo y la ruta del bloque para que se pueda configurar el procesamiento.

## Uso de datos y gobernanza {#data-usage-governance}

Todos los destinos de [!DNL Adobe Experience Platform] cumplen con las políticas de uso de datos al administrar los datos. Para obtener información detallada sobre cómo [!DNL Adobe Experience Platform] aplica el control de datos, lea la [Información general sobre el control de datos](/help/data-governance/home.md).

## Recursos adicionales {#additional-resources}

*Base de datos de Acxiom:* https://www.acxiom.com/wp-content/uploads/2022/02/fs-acxiom-infobase_AC-0268-22.pdf
