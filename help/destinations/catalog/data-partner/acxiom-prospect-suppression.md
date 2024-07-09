---
title: Supresión de prospección de Acxiom
description: Exporte sus audiencias de origen al destino de Acxiom para permitir que Acxiom elimine clientes conocidos o convertidos. A continuación, utilice el conector de origen de Acxiom para introducir y activar listas de clientes potenciales de Acxiom, con sus clientes conocidos o convertidos eliminados.
last-substantial-update: 2024-03-14T00:00:00Z
badge: Beta
exl-id: d82e8cd3-970c-44af-99b0-ea154eb3655e
source-git-commit: c35b43654d31f0f112258e577a1bb95e72f0a971
workflow-type: tm+mt
source-wordcount: '1466'
ht-degree: 3%

---

# [!DNL Acxiom Prospect-Suppression] conexión de destino

>[!NOTE]
>
>El [!DNL Acxiom Prospect-Suppression] el destino está en versión beta. El equipo de Acxiom crea y mantiene este conector de destino y esta página de documentación. Para cualquier consulta o solicitud de actualización, póngase en contacto con ellos directamente en acxiom-adobe-help@acxiom.com.

## Información general {#overview}

Uso [!DNL Acxiom Prospect-Suppression] para ofrecer las audiencias de clientes potenciales más productivas posibles. Este conector exporta de forma segura datos de origen de Real-time Customer Data Platform y los ejecuta a través de una galardonada resolución de higiene e identidad que produce un archivo de datos para utilizarlo como lista de supresión. Esto se comparará con el [!DNL Acxiom Global] base de datos que permite adaptar las listas de clientes potenciales para su importación. A continuación, utilice el [[!DNL Acxiom Prospecting Data Import]](/help/sources/connectors/data-partners/acxiom-prospecting-data-import.md) conector de origen a listas de clientes potenciales de Acxiom de nuevo en Real-Time CDP, con sus clientes conocidos o convertidos eliminados.

![Diagrama de marketing para exportar datos de origen a Acxiom y, a continuación, importar datos de clientes potenciales de nuevo en Real-Time CDP](/help/destinations/assets/catalog/data-partner/acxiom/marketing-workflow.png)

Acxiom ofrece las audiencias de mejor rendimiento del sector con el mayor catálogo de más de 12.000 atributos de datos globales centrados específicamente en proporcionar experiencias personalizadas. Aproveche las combinaciones ilimitadas de datos de alta calidad para crear y distribuir audiencias para satisfacer necesidades específicas de la campaña.

Este tutorial proporciona los pasos para crear una [!DNL Acxiom Prospect-Suppression] conexión de destino y flujo de datos mediante la interfaz de usuario de Adobe Experience Platform. Este conector se utiliza para entregar datos al servicio de clientes potenciales de Acxiom mediante Amazon S3 como punto de caída. Póngase en contacto con el representante de cuentas de Acxiom cuando empiece a exportar archivos al punto de colocación de Amazon S3.

![El catálogo de destino con el destino Acxiom seleccionado.](../../assets/catalog/data-partner/acxiom/image-destination-catalog.png)

## Casos de uso {#use-cases}

Para ayudarle a comprender mejor cómo y cuándo debe utilizar el [!DNL Acxiom Prospect-Suppression] Destino. Estos son ejemplos de casos de uso que los clientes de Adobe Experience Platform pueden solucionar mediante este destino.

### Crear una lista de supresión para conjuntos de datos de prospección {#create-suppression-list}

Los profesionales de marketing que buscan mejorar la eficacia de sus estrategias de divulgación a menudo emplean la creación de una lista de supresión. Esta lista incluye los clientes existentes y segmentos específicos, lo que garantiza su exclusión de las actividades de prospección durante las campañas de objetivos. Este enfoque estratégico ayuda a refinar la audiencia, evita la comunicación redundante y contribuye a un esfuerzo de marketing más centrado y eficiente.

Por ejemplo, como experto en marketing, es posible que desee ampliar el alcance de su campaña añadiendo perfiles de clientes potenciales objetivo a sus campañas en función de los criterios de segmentación y supresión que ha proporcionado.

El caso de uso se ejecuta mediante una combinación de conectores de origen y destino.

Inicialmente, exportaría los perfiles de cliente existentes utilizando este conector de destino para utilizarlo como archivo de supresión. Esto garantiza que no se incluyan registros de clientes existentes.

El servicio de Acxiom buscaría el archivo, lo recuperaría y lo utilizaría junto con criterios de selección adicionales y generaría un archivo de cliente potencial. A continuación, utilice el correspondiente [[!DNL Acxiom Prospecting Data Import]](/help/sources/connectors/data-partners/acxiom-prospecting-data-import.md) conector de origen para introducir los perfiles del cliente potencial en Adobe Real-Time CDP.

## Requisitos previos {#prerequisites}

>[!IMPORTANT]
>
>* Para conectarse al destino, necesita el **[!UICONTROL Ver destinos]** y **[!UICONTROL Administrar destinos]**, **[!UICONTROL Activar destinos]**, **[!UICONTROL Ver perfiles]**, y **[!UICONTROL Ver segmentos]** [permisos de control de acceso](/help/access-control/home.md#permissions). Lea el [información general de control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.
>* Para exportar *identidades*, necesita el **[!UICONTROL Ver gráfico de identidad]** [permiso de control de acceso](/help/access-control/home.md#permissions). <br> ![Seleccione el área de nombres de identidad resaltada en el flujo de trabajo para activar audiencias en los destinos.](/help/destinations/assets/overview/export-identities-to-destination.png "Seleccione el área de nombres de identidad resaltada en el flujo de trabajo para activar audiencias en los destinos."){width="100" zoomable="yes"}

## Audiencias compatibles {#supported-audiences}

Esta sección describe qué tipo de audiencias puede exportar a este destino.

| Origen de audiencia | Admitido | Descripción |
|-----------------------------|-----------|---------------------------------------------------------------------------------------------------------------------|
| [!DNL Segmentation Service] | ✓ | Audiencias generadas mediante el Experience Platform [Servicio de segmentación](../../../segmentation/home.md). |
| Cargas personalizadas | x | Audiencias [importado](../../../segmentation/ui/audience-portal.md#import-audience) en el Experience Platform desde archivos CSV. |

{style="table-layout:auto"}


## Tipo y frecuencia de exportación {#export-type-frequency}

Consulte la tabla siguiente para obtener información sobre el tipo y la frecuencia de exportación de destino.

| Elemento | Tipo | Notas |
|------------------|--------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Tipo de exportación | **[!UICONTROL Basado en perfiles]** | Va a exportar todos los miembros de un segmento, junto con los campos de esquema deseados (por ejemplo: dirección de correo electrónico, número de teléfono, apellidos), tal como se elige en la pantalla seleccionar atributos de perfil del [flujo de trabajo de activación de destino](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes). |
| Frecuencia de exportación | **[!UICONTROL Lote]** | Los destinos por lotes exportan archivos a plataformas descendentes en incrementos de tres, seis, ocho, doce o veinticuatro horas. Más información sobre [destinos basados en archivos por lotes](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## Conexión al destino {#connect}

>[!IMPORTANT]
> 
>Para conectarse al destino, necesita el **[!UICONTROL Ver destinos]** y **[!UICONTROL Administrar destinos]** [permisos de control de acceso](/help/access-control/home.md#permissions). Lea el [información general de control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Para conectarse a este destino, siga los pasos descritos en la sección [tutorial de configuración de destino](../../ui/connect-destination.md). En el flujo de trabajo de configuración de destino, rellene los campos enumerados en las dos secciones siguientes.

### Autenticarse en el destino {#authenticate}

Para autenticarse en el destino, rellene los campos obligatorios y seleccione **[!UICONTROL Conectar con destino]**.

Para acceder al bloque en Experience Platform, debe proporcionar valores válidos para las siguientes credenciales:

| Credencial | Descripción |
|---------------|----------------------------------------------------------------------------------------------------------|
| Clave de acceso de S3 | ID de clave de acceso para el bloque. Puede recuperar este valor desde la variable [!DNL Acxiom] equipo. |
| Clave secreta de S3 | El ID de clave secreta de su cubo. Puede recuperar este valor desde la variable [!DNL Acxiom] equipo. |
| Nombre del segmento | Este es el espacio en el que se compartirán los archivos. Puede recuperar este valor desde la variable [!DNL Acxiom] equipo. |

### Nueva cuenta

Para definir una nueva ubicación de Acxiom Managed S3:

![Nueva cuenta](../../assets/catalog/data-partner/acxiom/image-destination-new-account.png)

### Cuenta existente

Cuentas ya definidas con el [!DNL Acxiom Prospect Suppression] Los destinos de aparecerán en una lista emergente. Cuando se selecciona, puede ver los detalles de la cuenta en el carril derecho. Vea el ejemplo desde la interfaz de usuario de, cuando navega a **[!UICONTROL Destinos]** > **[!UICONTROL Cuentas]**:

![Cuenta existente](../../assets/catalog/data-partner/acxiom/image-destination-account.png)

### Rellenar detalles de destino {#destination-details}

Para configurar los detalles del destino, rellene los campos obligatorios y opcionales a continuación. Un asterisco junto a un campo en la interfaz de usuario indica que el campo es obligatorio.

![Detalles del destino](../../assets/catalog/data-partner/acxiom/image-destination-details.png)

* **Nombre (obligatorio)** - El nombre en el que se guardará el destino
* **Descripción** - Breve explicación del propósito del destino
* **Nombre del contenedor (obligatorio)** - Nombre del contenedor de Amazon S3 configurado en S3
* **Ruta de carpeta (obligatorio)** - Si se utilizan subdirectorios en un bloque, se debe definir una ruta o &#39;/&#39; para hacer referencia a la ruta raíz.
* **Tipo de archivo** : seleccione el Experience Platform de formato que debe utilizar para los archivos exportados. En este momento, el único tipo de archivo que esperará el procesamiento de Acxiom es CSV

>[!IMPORTANT]
>
>Al seleccionar la opción CSV, *Delimitador*, *Carácter comillas*, *Carácter de escape*, *Valor vacío*, *Valor nulo*, *Formato de compresión*, y *Incluir archivo de manifiesto* se presentarán las opciones, el siguiente documento explica esta configuración con más detalle [configurar las opciones de formato](../../ui/batch-destinations-file-formatting-options.md).

![Opciones de CSV](../../assets/catalog/data-partner/acxiom/image-destination-csv-options.png)

### Habilitar alertas {#enable-alerts}

Puede activar alertas para recibir notificaciones sobre el estado del flujo de datos a su destino. Seleccione una alerta de la lista a la que suscribirse para recibir notificaciones sobre el estado del flujo de datos. Para obtener más información sobre las alertas, consulte la guía de [suscripción a alertas de destinos mediante la IU](../../ui/alerts.md).

Cuando haya terminado de proporcionar detalles para la conexión de destino, seleccione **[!UICONTROL Siguiente]**.

## Activar públicos en este destino {#activate}

>[!IMPORTANT]
>
>* Para activar los datos, necesita el **[!UICONTROL Ver destinos]**, **[!UICONTROL Activar destinos]**, **[!UICONTROL Ver perfiles]**, y **[!UICONTROL Ver segmentos]** [permisos de control de acceso](/help/access-control/home.md#permissions). Lea el [información general de control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.
>* Para exportar *identidades*, necesita el **[!UICONTROL Ver gráfico de identidad]** [permiso de control de acceso](/help/access-control/home.md#permissions). <br> ![Seleccione el área de nombres de identidad resaltada en el flujo de trabajo para activar audiencias en los destinos.](/help/destinations/assets/overview/export-identities-to-destination.png "Seleccione el área de nombres de identidad resaltada en el flujo de trabajo para activar audiencias en los destinos."){width="100" zoomable="yes"}

Leer [Activar datos de audiencia en destinos de exportación de perfiles por lotes](/help/destinations/ui/activate-batch-profile-destinations.md) para obtener instrucciones sobre cómo activar audiencias en este destino.

### Sugerencias de asignación

El procesamiento requiere elementos de nombre y dirección, mientras que no todos los elementos son necesarios. Proporcionar lo más posible ayudará a una coincidencia exitosa.  En la tabla siguiente se proporcionan sugerencias de asignación. Se enumeran los atributos del lado del destino que utiliza el procesamiento Acxiom y a los que los clientes pueden asignar atributos de perfil.  Esto debe tratarse como sugerencias, ya que no todos los elementos son necesarios y los valores de origen dependerán de las necesidades de la cuenta.

| Campo de destino | Descripción de Source |
|--------------|-------------------------------------------------------------|
| name | El `person.name.fullName` valor en Experience Platform. |
| firstName | El `person.name.firstName` valor en Experience Platform. |
| lastName | El `person.name.lastName` valor en Experience Platform. |
| dirección1 | El `mailingAddress.street1` valor en Experience Platform. |
| dirección2 | El `mailingAddress.street2` valor en Experience Platform. |
| ciudad | El `mailingAddress.city` valor en Experience Platform. |
| estado | El `mailingAddress.state` valor en Experience Platform. |
| zip | El `mailingAddress.postalCode` valor en Experience Platform. |

{style="table-layout:auto"}

>[!NOTE]
>
>Los campos adicionales no enumerados anteriormente se incluirán en la exportación, pero el procesamiento Acxiom los ignorará.

## Revisión del flujo de datos

Utilice la página de revisión para obtener un resumen del flujo de datos antes del envío

![Revisar](../../assets/catalog/data-partner/acxiom/image-destination-review.png)

## Validar exportación de datos {#exported-data}

Para comprobar si los datos se han exportado correctamente, compruebe su [!DNL Amazon S3 Storage] y asegúrese de que los archivos exportados contienen las poblaciones de perfiles esperadas.

## Pasos siguientes

Al seguir este tutorial, ha creado correctamente un flujo de datos para exportar datos por lotes de Experience Platform a su [!DNL Acxiom] ubicación de S3 administrada. Debe ponerse en contacto con su representante de Acxiom con el nombre de la cuenta, el nombre de archivo y la ruta del bloque para que se pueda configurar el procesamiento.

## Uso de datos y gobernanza {#data-usage-governance}

Todo [!DNL Adobe Experience Platform] Los destinos de cumplen con las políticas de uso de datos al gestionar los datos. Para obtener información detallada sobre cómo [!DNL Adobe Experience Platform] aplica la gobernanza de datos, lea la [Resumen de gobernanza de datos](/help/data-governance/home.md).

## Recursos adicionales {#additional-resources}

*Datos y distribución de audiencias de Acxiom:* https://www.acxiom.com/customer-data/audience-data-distribution/
