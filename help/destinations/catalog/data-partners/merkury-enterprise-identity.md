---
title: Destino de identidad empresarial de Merkury
description: Obtenga información sobre cómo crear una conexión de destino de Enterprise Identity de Mercury mediante la interfaz de usuario de Adobe Experience Platform.
source-git-commit: 01ce38d26cf61706de84ec143e3dd8af720d0591
workflow-type: tm+mt
source-wordcount: '1469'
ht-degree: 2%

---


# Destino de identidad empresarial de Merkury

>[!NOTE]
>
>El conector de destino y la página de documentación los crea y mantiene el equipo [!DNL Merkury]. Para cualquier consulta o solicitud de actualización, comuníquese con el representante de la cuenta de [!DNL Merkury].

## Información general

Utilice el destino [!DNL Merkury Enterprise Identity] para generar perfiles de consumidores más precisos, completos y perspicaces. Con los datos de perfil mejorados, los especialistas en marketing pueden obtener mejores perspectivas, segmentos y modelos, lo que da como resultado una segmentación y un modelado predictivo más precisos.

![Diagrama que muestra la interconexión entre Merkury y el Experience Platform, incluida la ingesta y la activación](../../assets/catalog/data-partners/merkury-identity/media/image1.png)

Siga los pasos de esta página de documentación para crear una conexión de destino [!DNL Merkury Identity] y activar audiencias para su identificación y enriquecimiento mediante la interfaz de usuario de Adobe Experience Platform.

>[!NOTE]
>
>Si desea activar audiencias en destinos multimedia con su cuenta de [!DNL Merkury Connect], use el destino [!DNL Merkury Connections] en su lugar.

![Tarjeta de destino de identidad de empresa de Merkury resaltada en el catálogo de destinos de Experience Platform.](../../assets/catalog/data-partners/merkury-identity/media/image2.png)

## Casos de uso

El destino [!DNL Merkury Enterprise Identity] proporciona la capacidad de transferir de forma segura la PII del consumidor para las siguientes capacidades de [!DNL Merkury]:

* **Calidad de los datos**: mejore la calidad de los datos del perfil del consumidor con la higiene y estandarización de los datos. [!DNL Merkury] incluye higiene postal de EE. UU. e identificación de movimiento para admitir los casos de uso de marketing por correo postal más avanzados.
* **Resolución de identidad**: cree una vista única precisa y completa del cliente, basada en [!DNL Merkury] ID individuales y domésticos. Los ID de Mercury ofrecen un nivel profundo de vinculación de perfiles con el gráfico de identidad de consumidor adulto estadounidense completo de [!DNL Merkury] de más de 268 millones de personas.
* **Enriquecimiento**: Mejore la información y la personalización con [!DNL Merkury Data]. [!DNL Merkury Data] incluye más de 10 000 atributos de datos disponibles, que van desde datos demográficos, de estilo de vida, financieros, eventos personales y datos de compras de [!DNL Merkury Data Suite].

>[!NOTE]
>
>Estos casos de uso se ejecutan mediante una combinación de conectores de origen y destino. El cliente empezaría exportando sus registros de cliente existentes para el enriquecimiento mediante este conector de destino. El servicio de [!DNL Merkury] buscaría el archivo, lo recuperaría, lo enriquecería con los datos de [!DNL Merkury] y generaría un archivo. El cliente usaría la tarjeta de origen del conector de Source [!DNL Merkury] correspondiente para volver a introducir los perfiles de cliente hidratados en Adobe Real-Time CDP.

## Requisitos previos

>[!IMPORTANT]
>
>* Para conectarse al destino, necesita **Ver destinos** y **Administrar destinos**, **Activar destinos**, **Ver perfiles** y **Ver segmentos** [[permisos de control de acceso]](https://experienceleague.adobe.com/en/docs/experience-platform/access-control/home#permissions). Lea [[descripción general del control de acceso]](https://experienceleague.adobe.com/en/docs/experience-platform/access-control/ui/overview) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.
>* Para exportar *identidades*, necesita el **Ver gráfico de identidad** [[permiso de control de acceso]](https://experienceleague.adobe.com/en/docs/experience-platform/access-control/home#permissions).\![Seleccione el área de nombres de identidad resaltada en el flujo de trabajo para activar audiencias en los destinos.](../../assets/catalog/data-partners/merkury-identity/media/image3.png)

## Identidades admitidas {#supported-identities}

| Identidad de destino | Descripción | Consideraciones |
|---|---|---|
| GAID | GOOGLE ADVERTISING ID | Seleccione la identidad de destino GAID cuando su identidad de origen sea un área de nombres GAID. |
| IDFA | Apple ID para anunciantes | Seleccione la identidad de destino IDFA cuando la identidad de origen sea un área de nombres IDFA. |
| ECID | Experience Cloud ID | Un área de nombres que representa ECID. Este área de nombres también se puede mencionar mediante los siguientes alias: &quot;Adobe Marketing Cloud ID&quot;, &quot;Adobe Experience Cloud ID&quot;, &quot;Adobe Experience Platform ID&quot;. Consulte el siguiente documento sobre [ECID](/help/identity-service/features/ecid.md) para obtener más información. |
| phone_sha256 | Números de teléfono con hash con el algoritmo SHA256 | Los números de teléfono con hash SHA256 y texto sin formato son compatibles con Adobe Experience Platform. Si el campo de origen contiene atributos sin hash, marque la opción **[!UICONTROL Aplicar transformación]** para que [!DNL Platform] aplique automáticamente el hash a los datos durante la activación. |
| email_lc_sha256 | Direcciones de correo electrónico con el algoritmo SHA256 | Adobe Experience Platform admite direcciones de correo electrónico con hash SHA256 y de texto sin formato. Si el campo de origen contiene atributos sin hash, marque la opción **[!UICONTROL Aplicar transformación]** para que [!DNL Platform] aplique automáticamente el hash a los datos durante la activación. |
| extern_id | ID de usuario personalizados | Seleccione esta identidad de destino cuando la identidad de origen sea un área de nombres personalizada. |

{style="table-layout:auto"}

## Audiencias compatibles

Esta sección describe qué tipo de audiencias puede exportar a este destino.

| **Audiencia** | **Compatible** | **Descripción** | **origen** |
|---|---|---|---|
| Servicio de segmentación | ✓ | Audiencias generadas a través del Experience Platform [[Servicio de segmentación]](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/home). |
| Cargas personalizadas | x | Audiencias [[importadas]](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/overview#import-audience) en el Experience Platform desde archivos CSV. |

{style="table-layout:auto"}

## Tipo y frecuencia de exportación

Consulte la tabla siguiente para obtener información sobre el tipo y la frecuencia de exportación de destino.
|**Audiencia**|**Admitida**|**Descripción del origen**|\
|—|—|—|\
✓ |Servicio de segmentación|Audiencias generadas a través del Experience Platform [[Servicio de segmentación]](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/home).|
Cargas personalizadas|X|Audiencias [[importadas]](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/overview#import-audience) en el Experience Platform a partir de archivos CSV.

{style="table-layout:auto"}

## Conexión al destino

>[!IMPORTANT]
>
>Para conectarse al destino, necesita **Ver destinos** y **Administrar y activar destinos de conjuntos de datos** [[permisos de control de acceso]](https://experienceleague.adobe.com/en/docs/experience-platform/access-control/home#permissions). Lea [[descripción general del control de acceso]](https://experienceleague.adobe.com/en/docs/experience-platform/access-control/ui/overview) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Para conectarse a este destino, siga los pasos descritos en [[tutorial de configuración de destino]](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/ui/connect-destination). En el flujo de trabajo de configuración de destino, rellene los campos enumerados en las dos secciones siguientes.

### Autenticarse en el destino

Para autenticarse en el destino, rellene los campos obligatorios y seleccione **Conectar con destino**.

Para acceder al bloque en Experience Platform, debe proporcionar valores válidos para las siguientes credenciales:

| **Credencial** | **Descripción** |
|---|---|
| Clave de acceso | ID de clave de acceso para el bloque. Puede recuperar este valor del equipo de Merkury. |
| Clave secreta | El ID de clave secreta de su cubo. Puede recuperar este valor del equipo de Merkury. |
| Nombre del segmento | Este es el espacio en el que se compartirán los archivos. Puede recuperar este valor del equipo de Merkury. |

{style="table-layout:auto"}

![nueva pantalla de creación de destino](../../assets/catalog/data-partners/merkury-identity/media/image4.png)

### Rellenar detalles de destino

Para configurar los detalles del destino, rellene los campos obligatorios y opcionales a continuación. Un asterisco junto a un campo en la interfaz de usuario indica que el campo es obligatorio.

![Captura de pantalla con detalles de destino](../../assets/catalog/data-partners/merkury-identity/media/image6.png)


* **Nombre (obligatorio)** - El nombre en el que se guardará el destino
* **Descripción** - Breve explicación del propósito del destino
* **Nombre del contenedor (obligatorio)** - Nombre del contenedor de Amazon S3 configurado en S3
* **Ruta de acceso a la carpeta (obligatoria)**: si se usan subdirectorios en un bloque, se debe definir una ruta de acceso o &#39;/&#39; para hacer referencia a la ruta de acceso raíz.
* **Tipo de archivo**: seleccione el formato que el Experience Platform debe usar para los archivos exportados. Consulte con su equipo de Mercury el tipo de archivo esperado para su cuenta.

>[!NOTE]
>
>Al seleccionar la opción CSV, se presentarán las opciones Delimitador, Comilla, Carácter de escape, Valor vacío, Valor nulo, Formato de compresión e Incluir archivo de manifiesto. Consulte con su equipo de Mercury la configuración adecuada para su cuenta.

![imagen de la opción csv](../../assets/catalog/data-partners/merkury-identity/media/image8.png)

### Cuenta existente

Las cuentas ya definidas con el destino de identidad de empresa de Merkury aparecen en una lista emergente. Cuando se selecciona, puede ver los detalles de la cuenta en el carril derecho. Vea el ejemplo desde la interfaz de usuario cuando vaya a **Destinos** > **Cuentas**;

![Captura de pantalla de la cuenta de destino en la página de cuentas de destino](../../assets/catalog/data-partners/merkury-identity/media/image5.png)


### Habilitar alertas

Puede activar alertas para recibir notificaciones sobre el estado del flujo de datos a su destino. Seleccione una alerta de la lista a la que suscribirse para recibir notificaciones sobre el estado del flujo de datos. Para obtener más información sobre las alertas, consulte la guía sobre [suscripción a alertas de destinos mediante la interfaz de usuario](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/ui/alerts).

Cuando termine de proporcionar detalles para la conexión de destino, seleccione **Siguiente**.

## Activar públicos en este destino

>[!IMPORTANT]
>
>* Para activar los datos, necesita los permisos de control de acceso de **Ver destinos**, **Activar destinos**, **Ver perfiles** y **Ver segmentos**. Lea la descripción general del control de acceso o póngase en contacto con el administrador del producto para obtener los permisos necesarios.
>* Para exportar identidades, necesita el permiso de control de acceso **Ver gráfico de identidad**.

Lea [Activar datos de audiencia en destinos de exportación de perfiles por lotes](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/ui/activate/activate-batch-profile-destinations) para obtener instrucciones sobre cómo activar audiencias en este destino.

## Sugerencias de asignación

El procesamiento correcto de archivos en el lado [!DNL Merkury] requiere elementos de nombre y dirección. Aunque no todos los elementos son necesarios, proporcionar todo lo posible ayudará a que la coincidencia tenga éxito.

Las sugerencias de asignación se proporcionan en la tabla siguiente, que enumera los atributos del lado de destino que usa el procesamiento [!DNL Merkury] al que los clientes pueden asignar atributos de perfil. Trate estos elementos como sugerencias, ya que no todos los elementos son necesarios y los valores de origen dependerán de las necesidades de la cuenta.

| Campo de destino | Descripción de Source |
|---|---|
| Identificación | Campo de identidad que se utilizará para asignar datos de [!DNL Merkury] al Experience Platform a través del conector de Source [!DNL Merkury Enterprise Identity] |
| Input_First_Name | El valor `person.name.firstName` en el Experience Platform. |
| Input_Last_Name | El valor `person.name.lastName` en el Experience Platform. |
| Input_Address_Line_1 | El valor `mailingAddress.street` en el Experience Platform. |
| Input_City | El valor `mailingAddress.city` en el Experience Platform. |
| Input_State_Province_Code | El valor `mailingAddress.state` en el Experience Platform. Utilícelo si el estado está en el formulario de código de dos caracteres. |
| Input_State_Province_Name | El valor `mailingAddress.state` en el Experience Platform. Utilícelo si el estado es el nombre completo del estado |
| Input_Postal_Code | El valor `mailingAddress.postalCode` en el Experience Platform. |
| Input_Email_Address | El valor que desea asignar como dirección de correo electrónico de perfiles. |
| Input_Phone | El valor que desea asignar como número de teléfono de los perfiles. |

{style="table-layout:auto"}

## Validar exportación de datos

Para comprobar si los datos se han exportado correctamente, compruebe el contenedor de almacenamiento de Amazon S3 y asegúrese de que los archivos exportados contienen las poblaciones de perfiles esperadas.

## Uso de datos y gobernanza

Todos los destinos de Adobe Experience Platform cumplen con las políticas de uso de datos al administrar los datos. Para obtener información detallada sobre cómo Adobe Experience Platform aplica el control de datos, lea la [Información general sobre el control de datos](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/home).

## Pasos siguientes

Al seguir este tutorial, ha creado correctamente un flujo de datos para exportar datos de perfil del Experience Platform a su ubicación de S3 administrada de [!DNL Merkury]. A continuación, debe ponerse en contacto con su representante de [!DNL Merkury] y proporcionarle el nombre de la cuenta, los nombres de archivo y la ruta de acceso del bloque para que se pueda configurar el procesamiento.