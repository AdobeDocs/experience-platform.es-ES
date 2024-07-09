---
title: Destino del lote de flujo Magnite
description: Utilice este destino para enviar audiencias CDP de Adobe a la plataforma de streaming Magnite en lote.
badgeBeta: label="Beta" type="Informative"
hide: true
hidefromtoc: true
source-git-commit: c35b43654d31f0f112258e577a1bb95e72f0a971
workflow-type: tm+mt
source-wordcount: '1685'
ht-degree: 1%

---


# Magnite Streaming: conexión por lotes {#magnite-streaming-batch}

## Información general {#overview}

Este documento describe Magnite Streaming: destino por lotes y proporciona casos de uso de muestra para ayudarle a comprender mejor cómo activar y exportar audiencias a él.

Las audiencias de Adobe Real-Time CDP se pueden enviar a Magnite: Streaming platform de dos formas: se pueden enviar una vez al día o en tiempo real:

1. Si solo desea o necesita enviar audiencias una vez al día, puede utilizar el destino Magnite: Streaming Batch, que envía audiencias a Magnite: Streaming a través de una entrega diaria de archivos por lotes S3. Estas audiencias por lotes se almacenan indefinidamente en nuestra plataforma, a diferencia de las audiencias en tiempo real, que solo se almacenan durante un par de días.

2. Sin embargo, si desea o necesita enviar audiencias en tiempo real, debe utilizar el destino Magnite: Streaming Real-Time. Al utilizar el destino en tiempo real, Magnite: Streaming recibirá audiencias en tiempo real, pero solo podemos almacenar audiencias en tiempo real temporalmente en nuestra plataforma y se eliminarán de nuestro sistema en un par de días. Por este motivo, si desea utilizar el destino Magnite: Streaming Real-Time, TAMBIÉN debe utilizar el destino Magnite: Streaming Batch: cada audiencia que active al destino Real-Time, también debe activarlo al destino Batch.

Para recapitular: si solo desea enviar audiencias de Adobe Real-Time CDP una vez al día, solo utilizará Magnite: Streaming Batch destination, y las audiencias se enviarán una vez al día. Si desea enviar audiencias de Adobe Real-Time CDP en tiempo real, utilice los destinos Magnite: Streaming Batch y Magnite: Streaming Real-Time. Para obtener más información, consulte Magnite: Streaming.


Siga leyendo a continuación para obtener más información sobre Magnite: Streaming Batch destination, cómo conectarse a él y cómo activar audiencias de Adobe Real-Time CDP en él.
Para obtener más información sobre el destino en tiempo real, consulte [este documento](magnite-streaming.md) en su lugar.

>[!IMPORTANT]
>
>Este conector de destino está en versión beta y solo está disponible para clientes seleccionados. Para solicitar acceso, póngase en contacto con el representante del Adobe.
>
>El conector de destino y la página de documentación los crea y mantiene el [!DNL Magnite] equipo. Para cualquier consulta o solicitud de actualización, póngase en contacto directamente con ellos en `adobe-tech@magnite.com`.

## Casos de uso {#use-cases}

Para ayudarle a comprender mejor cómo y cuándo debe utilizar Magnite Streaming: Batch destination, estos son algunos casos de uso que los clientes de Adobe Experience Platform pueden resolver mediante este destino.

### Caso de uso #1 {#use-case-1}

Ha activado una audiencia en Magnite Streaming: destino en tiempo real.

Cualquier audiencia activada a través de Magnite Streaming: destino en tiempo real también debe utilizar Magnite Streaming: destino por lotes, ya que los datos de la entrega por lotes están pensados para reemplazar/mantener los datos de la entrega en tiempo real dentro de la plataforma Magnite Streaming.

### Caso de uso #2 {#use-case-2}

Desea activar una audiencia solo en una cadencia por lotes/diaria a la plataforma Magnite Streaming.

Cualquier audiencia activada a través de Magnite Streaming: destino del lote se enviará en una cadencia por lotes/diaria y, a continuación, se podrá segmentar en la plataforma Magnite Streaming.

## Requisitos previos {#prerequisites}

Para utilizar los destinos de Magnite en Adobe Experience Platform, primero debe tener una cuenta de Magnite Streaming. Si tiene un [!DNL Magnite Streaming] cuenta, póngase en contacto con su [!DNL Magnite] Administrador de cuentas al que se deben proporcionar credenciales para acceder [!DNL Magnite's] destinos. Si no tiene un [!DNL Magnite Streaming] cuenta de, póngase en contacto con adobe-tech@magnite.com

## Identidades admitidas {#supported-identities}

Magnite Streaming: el destino por lotes puede recibir *cualquiera* fuentes de identidad de la CDP de Adobe. Actualmente, este destino tiene tres campos de identidad de destino a los que puede asignar.

>[!NOTE]
>
>*Cualquiera* las fuentes de identidad pueden asignarse a cualquiera de las identidades de destino magnite_deviceId.

| Identidad de destino | Descripción | Consideraciones |
|:--------------------------- |:------------------------------------------------------------------------------------------------ |:------------------------------------------------------------------------------------- |
| magnite_deviceId_GAID | GOOGLE ADVERTISING ID | Seleccione esta identidad de destinatario cuando su identidad de origen sea un GAID |
| magnite_deviceId_IDFA | Apple ID para anunciantes | Seleccione esta identidad de destino cuando la identidad de origen sea un IDFA |
| magnite_deviceId_CUSTOM | ID personalizado/definido por el usuario | Seleccione esta identidad de destinatario cuando su identidad de origen no sea GAID o IDFA, o si sea un ID personalizado o definido por el usuario |

{style="table-layout:auto"}

## Audiencias compatibles {#supported-audiences}

| Origen de audiencia | Admitido | Descripción |
|-----------------------------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Audiencias generadas mediante el Experience Platform [Servicio de segmentación](../../../segmentation/home.md). |
| Cargas personalizadas | ✓ | Audiencias [importado](../../../segmentation/ui/audience-portal.md#import-audience) en el Experience Platform desde archivos CSV. |

{style="table-layout:auto"}

## Tipo y frecuencia de exportación {#export-type-frequency}

| Elemento | Tipo | Notas |
|-----------------------------|----------|----------|
| Tipo de exportación | Exportación de audiencia | Va a exportar todos los miembros de una audiencia con los identificadores (nombre, número de teléfono u otros) utilizados en Magnite Streaming: destino por lotes. |
| Frecuencia de exportación | Lote | Los destinos por lotes exportan archivos a plataformas descendentes en incrementos de tres, seis, ocho, doce o veinticuatro horas. Más información sobre el lote [destinos basados en archivos](/help/destinations/destination-types.md). |

{style="table-layout:auto"}

## Conexión al destino {#connect}

Una vez que se haya aprobado el uso de destino y Magnite Streaming haya compartido sus credenciales, siga los pasos a continuación para autenticar, asignar y compartir datos.

### Autenticarse en el destino {#authenticate}

Busque Magnite Streaming: Batch destination en el catálogo de experiencias de Adobe. Haga clic en el botón de opciones adicionales (\...) y, a continuación, configure la conexión o instancia de destino.

Si ya tiene una cuenta, puede localizarla cambiando la opción Account type a &quot;Existing account&quot;. De lo contrario, creará una cuenta a continuación:

Para crear una nueva cuenta y autenticarla en el destino por primera vez, rellene los campos obligatorios de &quot;clave de acceso S3&quot; y &quot;clave secreta S3&quot; (que se le han proporcionado mediante su administrador de cuentas) y seleccione **[!UICONTROL Conectar con destino]**

![campos de autenticación de configuración de destino sin rellenar](../../assets/catalog/advertising/magnite/destination-batch-config-auth-unfilled.png)

>[!NOTE]
>
>La política de seguridad de Magnite Streaming requiere una rotación regular de las claves S3. Debería esperar actualizar su cuenta en el futuro con nuevas claves secretas S3 access y S3. Solo necesita actualizar la cuenta en sí: los destinos que utilicen esa cuenta utilizarán automáticamente las claves actualizadas. Si no se cargan las claves nuevas, los datos no se enviarán a este destino.

### Rellenar detalles de destino {#destination-details}

Para configurar los detalles del destino, rellene los campos obligatorios y opcionales a continuación. Un asterisco junto a un campo en la interfaz de usuario indica que el campo es obligatorio.

* **[!UICONTROL Nombre]**: Nombre con el que reconocerá esta conexión/instancia de destino en el futuro.
* **[!UICONTROL Descripción]**: una descripción que le ayudará a identificar esta conexión o instancia de destino en el futuro.
* **[!UICONTROL Nombre de su socio de origen]**: El nombre que le gustaría usar como fuente en la plataforma de Magnite Streaming.

![campos de autenticación de configuración de destino rellenados](../../assets/catalog/advertising/magnite/destination-batch-config-auth-filled.png)

>[!NOTE]
>
>Si planea enviar varios tipos de ID (GAID, IDFA, etc.) con el destino Lote, se requiere una nueva conexión/instancia de destino para cada uno. Póngase en contacto con el representante de su cuenta de Magnite para obtener más información.

A continuación, puede continuar seleccionando **[!UICONTROL Siguiente]**

En la siguiente pantalla, titulada &quot;Política de gobernanza y acciones de aplicación (opcional)&quot;, puede seleccionar opcionalmente cualquier política de gobernanza de datos relevante. &quot;Exportación de datos&quot; se selecciona generalmente como destino del lote de flujo magnético.

![Política de gobernanza opcional y acciones coercitivas](../../assets/catalog/advertising/magnite/destination-batch-config-grouping-policy.png)

Una vez seleccionada, o si desea omitir esta pantalla opcional, seleccione **[!UICONTROL Crear]**

### Habilitar alertas {#enable-alerts}

Puede activar alertas para recibir notificaciones sobre el estado del flujo de datos a su destino. Seleccione una alerta de la lista a la que suscribirse para recibir notificaciones sobre el estado del flujo de datos. Para obtener más información sobre las alertas, consulte la guía de [suscripción a alertas de destinos mediante la IU](../../ui/alerts.md).

Cuando haya terminado de proporcionar detalles para la conexión de destino, seleccione **[!UICONTROL Siguiente]**.

### Activar segmentos en este destino {#activate}

>[!IMPORTANT]
> 
>* Para activar los datos, necesita el **[!UICONTROL Ver destinos]**, **[!UICONTROL Activar destinos]**, **[!UICONTROL Ver perfiles]**, y **[!UICONTROL Ver segmentos]** [permisos de control de acceso](/help/access-control/home.md#permissions). Lea el [información general de control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.
>* Para exportar *identidades*, necesita el **[!UICONTROL Ver gráfico de identidad]** [permiso de control de acceso](/help/access-control/home.md#permissions). <br> ![Seleccione el área de nombres de identidad resaltada en el flujo de trabajo para activar audiencias en los destinos.](/help/destinations/assets/overview/export-identities-to-destination.png "Seleccione el área de nombres de identidad resaltada en el flujo de trabajo para activar audiencias en los destinos."){width="100" zoomable="yes"}

Leer [Activar datos de audiencia en destinos de exportación de perfiles por lotes](/help/destinations/ui/activate-batch-profile-destinations.md) para obtener instrucciones sobre cómo activar segmentos de audiencia en este destino.

### Asignar atributos e identidades {#map}

En el **[!UICONTROL Campo de Source]**, puede seleccionar cualquier atributo o identidad para sus dispositivos. En este ejemplo, se ha seleccionado un mapa de identidad personalizado llamado &quot;DeviceId&quot;
![asigne los campos de datos deseados al campo device_id](../../assets/catalog/advertising/magnite/destination-batch-active-audience-field-mapping.png)

En el **[!UICONTROL Campo de destino]**:
![seleccione la identidad de destino del tipo de dispositivo correspondiente](../../assets/catalog/advertising/magnite/destination-batch-active-audience-select-device-type.png) Consulte [Identidades admitidas](#supported-identities) para obtener más información.
En este ejemplo, se ha seleccionado la variable **[!UICONTROL Campo de destino]**: magnite_deviceId_CUSTOM, porque nuestra **[!UICONTROL Campo de Source]** se definió como un IdentityMap personalizado: DeviceID.

>[!NOTE]
>
>Si planea enviar/asignar varios tipos de ID (GAID, IDFA, etc.) con el destino Lote, se requiere una nueva conexión/instancia de destino para cada uno. Póngase en contacto con el representante de su cuenta de Magnite para obtener más información.


En la pantalla &quot;Configure a filename and export schedule for each audience&quot; (Configurar un nombre de archivo y una programación de exportación para cada audiencia), ahora debe configurar una fecha de inicio (obligatoria), una fecha de finalización (opcional) y un ID de asignación (obligatorio) para cada audiencia.

>[!IMPORTANT]
>
> Se requiere un ID de asignación o &quot;NONE&quot; para este destino.
>
> Se debe proporcionar un ID de asignación cuando una audiencia tenga un ID de segmento preexistente conocido anteriormente para Magnite Streaming. De lo contrario, se debe utilizar &quot;NINGUNO&quot; como ID de asignación.
>
> Al configurar el nombre de archivo para cada audiencia, incluya el ID de asignación a través del campo &quot;Texto personalizado&quot; para agregar. El ID de asignación se anexará como: `{previous_filename}\_\[MAPPING_ID\].` Si esta audiencia es nueva en Magnite Streaming y no va a proporcionar un ID de asignación, se debe introducir &quot;NONE&quot; en el campo &quot;Texto personalizado&quot;. El nuevo nombre de archivo en este caso debe ser: `{previous_filename}\_\[NONE\]`.

## Datos exportados / Validar exportación de datos {#exported-data}

Una vez que las audiencias se hayan cargado, puede validar que se hayan creado y cargado correctamente.

* El destino Magnite Streaming Batch entrega archivos S3 a Magnite Streaming en una cadencia diaria. Después de la entrega y la ingesta, se espera que las audiencias y los segmentos aparezcan en Magnite Streaming y se puedan aplicar a una oferta. Puede confirmarlo consultando el ID de segmento o el nombre de segmento compartido durante los pasos de activación en Adobe Experience Platform.

>[!NOTE]
>
>Las audiencias activadas o entregadas al destino del lote de flujo Magnite *replace* las mismas audiencias que se activaron o entregaron a través del destino de flujo en tiempo real de Magnite. Si está buscando un segmento con el nombre, es posible que no encuentre el segmento en tiempo real, hasta que la plataforma Magnite Streaming haya ingerido y procesado el lote.

## Uso de datos y gobernanza {#data-usage-governance}

Todo [!DNL Adobe Experience Platform] Los destinos de cumplen con las políticas de uso de datos al gestionar los datos. Para obtener información detallada sobre cómo [!DNL Adobe Experience Platform] aplica la gobernanza de datos, lea la [Resumen de gobernanza de datos](/help/data-governance/home.md).

## Recursos adicionales {#additional-resources}

Para obtener documentación de ayuda adicional, visite la [Centro de ayuda de Magnite](https://help.magnite.com/help).
