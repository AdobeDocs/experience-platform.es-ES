---
title: Plantilla de autoservicio de documentación // Reemplazar por el nombre de su destino
description: Utilice esta plantilla para crear documentación pública para su destino en el catálogo de Adobe Experience Platform. // Reemplace con el párrafo en la sección Información general
exl-id: 99700474-8bf6-4176-acc1-38814e17c995
source-git-commit: 1773edff56059cf5bc57ebaaa133216423fcfe10
workflow-type: tm+mt
source-wordcount: '1528'
ht-degree: 1%

---

# Su conexión de destino {#your-destination}

*A medida que avanza por esta plantilla, reemplace o elimine todos los párrafos en cursiva (empezando por esta).*

*Comience por actualizar los metadatos (título y descripción) en la parte superior de la página. Ignore todas las instancias de UICONTROL en esta página. Esta es una etiqueta que ayuda a nuestros procesos de traducción automática a traducir correctamente la página a los múltiples idiomas que admitimos. Agregaremos etiquetas a su documentación después de que la envíe.*

>[!IMPORTANT]
>
>* Rellene todas las secciones de esta plantilla, en el orden en que se destacan en la plantilla.
>* Esta plantilla se actualiza con poca frecuencia, según los comentarios del socio. Antes de empezar a crear documentación para el destino, asegúrese de haber descargado el [última versión de la plantilla](../assets/docs-framework/yourdestination-template.zip).


## Información general {#overview}

*Proporcione una breve descripción general de su empresa, incluido el valor que proporciona a los clientes. Incluya un vínculo a la página de inicio de la documentación del producto para obtener más información.*

>[!IMPORTANT]
>
>Esta página de documentación fue creada por el *Su destino* equipo. Para cualquier consulta o solicitud de actualización, póngase en contacto directamente con ellos en *Inserte un vínculo o una dirección de correo electrónico donde pueda ponerse en contacto con usted para obtener actualizaciones, por ejemplo `support@YourDestination.com`.*

## Casos de uso {#use-cases}

Para ayudarle a comprender mejor cómo y cuándo debe utilizar el *Su destino* Destino. Estos son ejemplos de casos de uso que los clientes de Adobe Experience Platform pueden solucionar mediante este destino.

### Caso de uso #1 {#use-case-1}

*Para plataformas de mensajería móvil:*

*Una plataforma de venta y alquiler de viviendas quiere enviar notificaciones móviles a los dispositivos Android y iOS de los clientes para informarles de que hay 100 listados actualizados en la zona en la que anteriormente buscaron un alquiler.*

### Caso de uso #2 {#use-case-2}

*Para plataformas de redes sociales:*

*Una marca de ropa deportiva quiere llegar a los clientes existentes a través de sus cuentas en las redes sociales. La marca de ropa puede ingerir direcciones de correo electrónico de su propio CRM a Adobe Experience Platform, crear segmentos a partir de sus propios datos sin conexión y enviar estos segmentos a su destino para mostrar anuncios en las fuentes de medios sociales de sus clientes.*

## Requisitos previos {#prerequisites}

*Agregue información en esta sección sobre todo lo que los clientes deben tener en cuenta antes de comenzar a configurar el destino en la interfaz de usuario de Adobe Experience Platform. Puede tratarse de lo siguiente:*

* *necesidad de añadirse a una lista de permitidos*
* *requisitos para el hash de correo electrónico*
* *cualquier detalle de la cuenta de su parte*
* *Cómo obtener una clave API para conectarse a la plataforma*

*Puede vincular a la documentación relevante si esto resulta útil para los clientes.*

## Identidades admitidas {#supported-identities}

*Añada información en esta sección acerca de las identidades admitidas en el destino. Hemos rellenado previamente la tabla con algunos valores estándar. Elimine los valores que no se apliquen al destino y los valores que no estén rellenados previamente.*

*Su destino* admite la activación de identidades descritas en la tabla siguiente. Más información sobre [identidades](/help/identity-service/namespaces.md).

| Identidad de destino | Descripción | Consideraciones |
|---|---|---|
| GAID | ID de publicidad de Google | Seleccione la identidad de destino GAID cuando su identidad de origen sea un área de nombres GAID. |
| IDFA | Apple ID para anunciantes | Seleccione la identidad de destino IDFA cuando la identidad de origen sea un área de nombres IDFA. |
| ECID | Experience Cloud ID | Un área de nombres que representa ECID. Este área de nombres también se puede mencionar mediante los siguientes alias: &quot;Adobe Marketing Cloud ID&quot;, &quot;Adobe Experience Cloud ID&quot;, &quot;Adobe Experience Platform ID&quot;. Lea el siguiente documento el [ECID](/help/identity-service/ecid.md) para obtener más información. |
| phone_sha256 | Números de teléfono con hash con el algoritmo SHA256 | Los números de teléfono con hash SHA256 y texto sin formato son compatibles con Adobe Experience Platform. Si el campo de origen contiene atributos sin hash, marque la **[!UICONTROL Aplicar transformación]** opción, para tener [!DNL Platform] hash automático de los datos en la activación. |
| email_lc_sha256 | Direcciones de correo electrónico con el algoritmo SHA256 | Adobe Experience Platform admite direcciones de correo electrónico con hash SHA256 y de texto sin formato. Si el campo de origen contiene atributos sin hash, marque la **[!UICONTROL Aplicar transformación]** opción, para tener [!DNL Platform] hash automático de los datos en la activación. |
| extern_id | ID de usuario personalizados | Seleccione esta identidad de destino cuando la identidad de origen sea un área de nombres personalizada. |

{style="table-layout:auto"}

## Tipo y frecuencia de exportación {#export-type-frequency}

*En la tabla, conserve solo las líneas que correspondan a su destino. Debe tener una línea para el tipo de exportación y otra para la frecuencia de exportación. Elimine los valores que no se apliquen a su destino.*

Consulte la tabla siguiente para obtener información sobre el tipo y la frecuencia de exportación de destino.

| Elemento | Tipo | Notas |
---------|----------|---------|
| Tipo de exportación | **[!UICONTROL Exportación de segmentos]** | Va a exportar todos los miembros de un segmento (audiencia) con los identificadores (nombre, número de teléfono u otros) utilizados en *Su destino* destino. |
| Tipo de exportación | **[!UICONTROL Basado en perfiles]** | Va a exportar todos los miembros de un segmento, junto con los campos de esquema deseados (por ejemplo: dirección de correo electrónico, número de teléfono, apellidos), tal como se elige en la pantalla seleccionar atributos de perfil del [flujo de trabajo de activación de destino](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes). |
| Tipo de exportación | **[!UICONTROL Exportación de conjuntos de datos]** | Va a exportar conjuntos de datos sin procesar que no se agrupan ni estructuran por intereses o cualificaciones de audiencia. |
| Frecuencia de exportación | **[!UICONTROL Transmisión]** | Los destinos de streaming son conexiones basadas en API &quot;siempre activadas&quot;. Tan pronto como se actualiza un perfil en Experience Platform según la evaluación de segmentos, el conector envía la actualización de forma descendente a la plataforma de destino. Más información sobre [destinos de streaming](/help/destinations/destination-types.md#streaming-destinations). |
| Frecuencia de exportación | **[!UICONTROL Lote]** | Los destinos por lotes exportan archivos a plataformas descendentes en incrementos de tres, seis, ocho, doce o veinticuatro horas. Más información sobre [destinos basados en archivos por lotes](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## Conectar con el destino {#connect}

>[!IMPORTANT]
> 
>Para conectarse al destino, necesita el **[!UICONTROL Administrar destinos]** [permiso de control de acceso](/help/access-control/home.md#permissions). Lea el [información general de control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Para conectarse a este destino, siga los pasos descritos en la sección [tutorial de configuración de destino](../../ui/connect-destination.md). En el flujo de trabajo de configuración de destino, rellene los campos enumerados en las dos secciones siguientes.

### Autenticar en el destino {#authenticate}

*Añada los campos que los clientes deben rellenar al autenticarse en el destino. Estos campos son específicos del destino y dependen de la configuración de en Destination SDK. Es posible que los campos de su destino no sean los mismos que los que se enumeran a continuación. Por favor incluya también una captura de pantalla similar a la captura de pantalla de muestra que se muestra abajo.*

Para autenticarse en el destino, rellene los campos obligatorios y seleccione **[!UICONTROL Conectar con destino]**.

![Captura de pantalla de ejemplo que muestra cómo autenticarse en el destino](../assets/docs-framework/authenticate-destination.png)

* **[!UICONTROL Token de portador]**: complete el token de portador para autenticarse en el destino.

### Rellenar detalles de destino {#destination-details}

*Añada los campos que los clientes deben rellenar al configurar un nuevo destino. Estos campos son específicos del destino y dependen de la configuración de en Destination SDK. Es posible que los campos de su destino no sean los mismos que los que se enumeran a continuación. Por favor incluya también una captura de pantalla similar a la captura de pantalla de muestra que se muestra abajo.*

Para configurar los detalles del destino, rellene los campos obligatorios y opcionales a continuación. Un asterisco junto a un campo en la interfaz de usuario indica que el campo es obligatorio.

![Captura de pantalla de muestra que muestra cómo rellenar los detalles del destino.](../assets/docs-framework/configure-destination-details.png)

* **[!UICONTROL Nombre]**: Un nombre con el que reconocerá este destino en el futuro.
* **[!UICONTROL Descripción]**: Una descripción que le ayudará a identificar este destino en el futuro.
* **[!UICONTROL ID de cuenta]**: su *Su destino* ID de cuenta.

### Habilitar alertas {#enable-alerts}

Puede activar alertas para recibir notificaciones sobre el estado del flujo de datos a su destino. Seleccione una alerta de la lista a la que suscribirse para recibir notificaciones sobre el estado del flujo de datos. Para obtener más información sobre las alertas, lea la guía de [suscripción a alertas de destinos mediante la IU](../../ui/alerts.md).

Cuando haya terminado de proporcionar detalles para la conexión de destino, seleccione **[!UICONTROL Siguiente]**.

## Activar segmentos en este destino {#activate}

>[!IMPORTANT]
> 
>Para activar los datos, necesita el **[!UICONTROL Administrar destinos]**, **[!UICONTROL Activar destinos]**, **[!UICONTROL Ver perfiles]**, y **[!UICONTROL Ver segmentos]** [permisos de control de acceso](/help/access-control/home.md#permissions). Lea el [información general de control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

*Eliminar según corresponda: si está documentando un nuevo destino de flujo continuo, mantenga el primer párrafo a continuación. Si está documentando un nuevo destino basado en archivos, mantenga el segundo párrafo. Si está documentando un destino que exporta conjuntos de datos, conserve el tercer párrafo.*

Leer [Activación de perfiles y segmentos en destinos de exportación de segmentos de flujo continuo](/help/destinations/ui/activate-segment-streaming-destinations.md) para obtener instrucciones sobre cómo activar segmentos de audiencia en este destino.

Leer [Activar datos de audiencia en destinos de exportación de perfiles por lotes](/help/destinations/ui/activate-batch-profile-destinations.md) para obtener instrucciones sobre cómo activar segmentos de audiencia en este destino.

Leer [(Beta) Exportar conjuntos de datos](/help/destinations/ui/export-datasets.md) para obtener instrucciones detalladas sobre la exportación de conjuntos de datos a este destino.

### Asignar atributos e identidades {#map}

*Agregue información sobre las asignaciones compatibles entre los campos de origen y destino en el paso Asignación del flujo de trabajo de activación. El destino puede admitir la exportación de atributos de perfil, áreas de nombres de identidad o ambos. Algunos campos pueden ser obligatorios. Los atributos de destino pueden ser predefinidos o personalizados. Indique las advertencias importantes y use ejemplos, preferiblemente con capturas de pantalla. Dos ejemplos de páginas de destino que puede utilizar como referencia son:*

* *[Pega](/help/destinations/catalog/personalization/pega.md#mapping-example)*
* *[Medallia](/help/destinations/catalog/voice/medallia-connector.md#map)*

## Datos exportados / Validar exportación de datos {#exported-data}

*Agregue un párrafo sobre cómo se exportan los datos al destino. Esto ayudaría al cliente a asegurarse de que se ha integrado correctamente con su destino. Por ejemplo, puede proporcionar un JSON de muestra como el de abajo. O bien, puede proporcionar capturas de pantalla e información de la interfaz de su destino que muestren cómo los clientes deberían esperar que los segmentos se rellenen en la plataforma de destino.*

```
{
  "person": {
    "email": "yourstruly@adobe.com"
  },
  "segmentMembership": {
    "ups": {
      "7841ba61-23c1-4bb3-a495-00d3g5fe1e93": {
        "lastQualificationTime": "2020-05-25T21:24:39Z",
        "status": "exited"
      },
      "59bd2fkd-3c48-4b18-bf56-4f5c5e6967ae": {
        "lastQualificationTime": "2020-05-25T23:37:33Z",
        "status": "realized"
      }
    }
  },
  "identityMap": {
    "ecid": [
      {
        "id": "14575006536349286404619648085736425115"
      },
      {
        "id": "66478888669296734530114754794777368480"
      }
    ],
    "email_lc_sha256": [
      {
        "id": "655332b5fa2aea4498bf7a290cff017cb4"
      },
      {
        "id": "66baf76ef9de8b42df8903f00e0e3dc0b7"
      }
    ]
  }
}
```

## Uso de datos y gobernanza {#data-usage-governance}

Todo [!DNL Adobe Experience Platform] Los destinos de cumplen con las políticas de uso de datos al gestionar los datos. Para obtener información detallada sobre cómo [!DNL Adobe Experience Platform] aplica la gobernanza de datos, lea la [Resumen de gobernanza de datos](/help/data-governance/home.md).

## Recursos adicionales {#additional-resources}

*Puede proporcionar más vínculos a la documentación del producto o a cualquier otro recurso que considere importante para que el cliente tenga éxito.*