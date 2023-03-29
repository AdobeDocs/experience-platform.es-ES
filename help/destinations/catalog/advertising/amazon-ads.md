---
title: Publicidades de Amazon
description: Amazon Ads ofrece una amplia gama de opciones para ayudarle a lograr sus objetivos publicitarios para vendedores registrados, proveedores, vendedores de libros, autores de Kindle Direct Publishing (KDP), desarrolladores de aplicaciones y/o agencias. La integración de Amazon Ads con Adobe Experience Platform proporciona integración llave en mano para los productos de Amazon Ads, incluido el Amazon DSP (ADSP). Con el destino Amazon Ads en Adobe Experience Platform, los usuarios pueden definir audiencias de anunciante para el direccionamiento y la activación en el DSP de Amazon.
last-substantial-update: 2023-03-29T00:00:00Z
source-git-commit: 732e6d3d53d983f3390941f4694d2c542d882004
workflow-type: tm+mt
source-wordcount: '1277'
ht-degree: 1%

---


# (Beta) Conexión de Amazon Ads {#amazon-ads}

## Información general {#overview}

Amazon Ads ofrece una amplia gama de opciones para ayudarle a lograr sus objetivos publicitarios para vendedores registrados, proveedores, vendedores de libros, autores de Kindle Direct Publishing (KDP), desarrolladores de aplicaciones y/o agencias.

La integración de Amazon Ads con Adobe Experience Platform proporciona integración llave en mano para los productos de Amazon Ads, incluido el Amazon DSP (ADSP). Con el destino Amazon Ads en Adobe Experience Platform, los usuarios pueden definir audiencias de anunciante para el direccionamiento y la activación en el DSP de Amazon.

Esta conexión admite la creación de audiencias en los siguientes Amazon Marketplaces: `US`, `CA`, `MX`, `BR`.

>[!IMPORTANT]
>
>Esta página de documentación la creó el *Publicidades de Amazon* equipo. Actualmente es un producto beta y la funcionalidad está sujeta a cambios. Para cualquier consulta o solicitud de actualización, póngase en contacto con ellos directamente en *`amc-support@amazon.com`.*

## Casos de uso {#use-cases}

Para ayudarle a comprender mejor cómo y cuándo debe usar la variable *Publicidades de Amazon* destino, aquí hay ejemplos de casos de uso que los clientes de Adobe Experience Platform pueden resolver utilizando este destino.

### Activación y segmentación {#activation-and-targeting}

Esta integración con Amazon DSP permite que los anunciantes de Amazon Ads pasen segmentos CDP del anunciante de Adobe Experience Platform a los DSP de Amazon para crear audiencias de anunciante para la segmentación de anuncios. Las audiencias se pueden seleccionar dentro de la DSP de Amazon para la segmentación positiva, así como para la segmentación negativa (supresión). Además, mediante las señales generadas a través del Marketing Cloud de Amazon, los anunciantes pueden optimizar sus audiencias de anunciantes, lo que sincroniza los cambios de audiencia con los DSP de Amazon.

## Requisitos previos {#prerequisites}

Para utilizar la conexión de Amazon Ads con Adobe Experience Platform, los usuarios deben tener acceso primero a una cuenta de Anunciante de Amazon DSP.  Para aprovisionar estas instancias, visite la siguiente página en el sitio web de Amazon Ads:

* [Introducción a Amazon DSP](https://advertising.amazon.com/solutions/products/amazon-dsp?ref_=a20m_us_hnav_p_dsp_adtech)

## Identidades compatibles {#supported-identities}

La variable *Publicidades de Amazon* connection admite la activación de identidades descritas en la siguiente tabla. Más información sobre [identidades](/help/identity-service/namespaces.md). Para obtener más información sobre las identidades admitidas por Amazon Ads, visite la [Centro de asistencia de Amazon DSP](https://advertising.amazon.com/dsp/help/ss/en/audiences#GA6BC9BW52YFXBNE).

| Identidad de Target | Descripción | Consideraciones |
|---|---|---|
| phone_sha256 | Números de teléfono con hash con el algoritmo SHA256 | Adobe Experience Platform admite los números de teléfono con texto sin formato y con hash SHA256. Si el campo de origen contiene atributos sin hash, marque la casilla de verificación **[!UICONTROL Aplicar transformación]** para [!DNL Platform] hash automático de los datos al activarlos. |
| email_lc_sha256 | Direcciones de correo electrónico con hash con el algoritmo SHA256 | Adobe Experience Platform admite las direcciones de correo electrónico con texto sin formato y con hash SHA 256. Si el campo de origen contiene atributos sin hash, marque la casilla de verificación **[!UICONTROL Aplicar transformación]** para [!DNL Platform] hash automático de los datos al activarlos. |

{style="table-layout:auto"}

## Tipo de exportación y frecuencia {#export-type-frequency}

Consulte la tabla siguiente para obtener información sobre el tipo y la frecuencia de exportación de destino.

| Elemento | Tipo | Notas |
---------|----------|---------|
| Tipo de exportación | **[!UICONTROL Exportación de segmentos]** | Está exportando todos los miembros de un segmento (audiencia) con los identificadores (nombre, número de teléfono u otros) utilizados en la variable *Publicidades de Amazon* destino. |
| Frecuencia de exportación | **[!UICONTROL Transmisión]** | Los destinos de flujo continuo son conexiones basadas en API &quot;siempre activadas&quot;. Tan pronto como un perfil se actualiza en el Experience Platform en función de la evaluación de segmentos, el conector envía la actualización descendente a la plataforma de destino. Más información sobre [destinos de flujo continuo](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Conectarse al destino {#connect}

>[!IMPORTANT]
> 
>Para conectarse al destino, necesita la variable **[!UICONTROL Administrar destinos]** [permiso de control de acceso](/help/access-control/home.md#permissions). Lea el [información general sobre el control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Para conectarse a este destino, siga los pasos descritos en la sección [tutorial de configuración de destino](../../ui/connect-destination.md). En el flujo de trabajo de configuración de destino, rellene los campos que aparecen en las dos secciones siguientes.

### Autenticar en destino {#authenticate}

Para autenticarse en el destino, rellene los campos obligatorios y seleccione **[!UICONTROL Conectarse al destino]**.

Se le dirigirá a la interfaz de conexión de Amazon Ads, donde primero seleccionará las cuentas de anunciante a las que desee conectarse.  Al conectarse, se le redirigirá de nuevo a Adobe Experience Platform con una nueva conexión, provista del ID de la cuenta del anunciante que haya seleccionado. Seleccione la cuenta del anunciante adecuada en la pantalla de configuración de destino para continuar.

* **[!UICONTROL Token portador]**: Rellene el token al portador para autenticarse en el destino.

### Rellenar detalles de destino {#destination-details}

Para configurar los detalles del destino, rellene los campos opcionales y requeridos a continuación. Un asterisco junto a un campo en la interfaz de usuario indica que el campo es obligatorio.

* **[!UICONTROL Nombre]**: Un nombre por el cual reconocerá este destino en el futuro.
* **[!UICONTROL Descripción]**: Descripción que le ayudará a identificar este destino en el futuro.
* **[!UICONTROL ID del anunciante de Amazon Ads]**: Seleccione el ID de la cuenta de Amazon Ads de destino que se utiliza para el destino.

Nota: una vez que seleccione este ID de anunciante de Amazon Ads, deberá crear un nuevo destino para cambiar esto. Si vuelve a autenticar las credenciales de OAuth y selecciona un nuevo ID de anunciante, no se aplicarán los cambios.

![Configurar nuevo destino](../../assets/catalog/advertising/amazon_ads_image_1.png)

### Habilitar alertas {#enable-alerts}

Puede activar las alertas para recibir notificaciones sobre el estado del flujo de datos a su destino. Seleccione una alerta de la lista para suscribirse y recibir notificaciones sobre el estado de su flujo de datos. Para obtener más información sobre las alertas, consulte la guía de [suscripción a alertas de destinos mediante la interfaz de usuario](../../ui/alerts.md).

Cuando haya terminado de proporcionar detalles para la conexión de destino, seleccione **[!UICONTROL Siguiente]**.

## Activar segmentos en este destino {#activate}

>[!IMPORTANT]
> 
>Para activar los datos, necesita la variable **[!UICONTROL Administrar destinos]**, **[!UICONTROL Activar destinos]**, **[!UICONTROL Ver perfiles]** y **[!UICONTROL Ver segmentos]** [permisos de control de acceso](/help/access-control/home.md#permissions). Lea el [información general sobre el control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Lectura [Activar perfiles y segmentos en destinos de exportación de segmentos de flujo continuo](/help/destinations/ui/activate-segment-streaming-destinations.md) para obtener instrucciones sobre la activación de segmentos de audiencia en este destino.

### Asignación de atributos e identidades {#map}

La conexión Amazon Ads admite direcciones de correo electrónico con hash y números de teléfono con hash para la coincidencia de identidades.  La captura de pantalla siguiente proporciona un ejemplo de coincidencia compatible con la conexión Amazon Ads:

![Asignación de Adobes a Amazon Ads](../../assets/catalog/advertising/amazon_ads_image_2.png)

* Para asignar direcciones de correo electrónico con hash, seleccione la opción `Email_LC_SHA256` área de nombres de identidad como campo de origen.
* Para asignar números de teléfono con hash, seleccione la opción `Phone_SHA256` área de nombres de identidad como campo de origen.
* Para asignar direcciones de correo electrónico o números de teléfono sin hash, seleccione los espacios de nombres de identidad correspondientes como campos de origen y marque la casilla de verificación `Apply Transformation` para que Platform hash las identidades en la activación.

Se recomienda encarecidamente asignar tantos campos como haya disponibles. Si solo hay un atributo de origen disponible, puede asignar un solo campo.  El destino de Amazon Ads utilizará todos los campos asignados con fines de asignación, lo que dará como resultado tasas de coincidencia más altas si se proporcionan más campos. Para obtener más información sobre los identificadores aceptados, visite la [Página de ayuda de audiencia con hash de Amazon Ads](https://advertising.amazon.com/dsp/help/ss/en/audiences#GA6BC9BW52YFXBNE).

## Datos exportados / Validar exportación de datos {#exported-data}

Una vez cargada la audiencia, puede validar que la audiencia se haya creado y cargado correctamente siguiendo los pasos siguientes:

**Para Amazon DSP**

Vaya a su ID del anunciante → Audiencias → Audiencias del anunciante. Si la audiencia se creó correctamente y cumple el número mínimo de miembros de la audiencia, verá el estado de `Active`.  Puede encontrar más información sobre el tamaño y el alcance de la audiencia en el panel Alcance previsto situado a la derecha de la interfaz de usuario de Amazon DSP.

![Validación de la creación de audiencias de Amazon DSP](../../assets/catalog/advertising/amazon_ads_image_3.png)

## Uso y gobernanza de los datos {#data-usage-governance}

Todo [!DNL Adobe Experience Platform] Los destinos de cumplen las políticas de uso de datos al administrar los datos. Para obtener información detallada sobre cómo [!DNL Adobe Experience Platform] exige la administración de datos, lea la [Información general sobre la administración de datos](/help/data-governance/home.md).

## Recursos adicionales {#additional-resources}

Para obtener documentación de ayuda adicional, visite los siguientes recursos de ayuda de Amazon Ads:

* [Centro de ayuda de Amazon DSP](https://advertising.amazon.com/dsp/help/ss/en/audiences#/)
