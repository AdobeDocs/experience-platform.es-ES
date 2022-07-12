---
title: Plantilla de autoservicio // Reemplazar por el nombre del destino
description: Utilice esta plantilla para crear documentación pública para el destino en el catálogo de Adobe Experience Platform. // Reemplazar por el párrafo de la sección Información general
source-git-commit: fd2019feb25b540612a278cbea5bf5efafe284dc
workflow-type: tm+mt
source-wordcount: '1341'
ht-degree: 1%

---


# Conexión YourDestination {#your-destination}

*A medida que recorre esta plantilla, reemplace o elimine todos los párrafos en cursiva (a partir de este).*

*Comience por actualizar los metadatos (título y descripción) en la parte superior de la página. Ignore todas las instancias de UICONTROL en esta página. Esta es una etiqueta que ayuda a nuestros procesos de traducción automática a traducir correctamente la página a los múltiples idiomas compatibles. Añadiremos etiquetas a su documentación después de enviarla.*

## Información general {#overview}

*Proporcione una breve descripción general de su empresa, incluido el valor que proporciona a los clientes. Incluya un vínculo a la página de inicio de la documentación del producto para obtener más información.*

>[!IMPORTANT]
>
>Esta página de documentación la creó el *YourDestination* equipo. Para cualquier consulta o solicitud de actualización, póngase en contacto con ellos directamente en *Inserte un vínculo o una dirección de correo electrónico donde se pueda acceder a las actualizaciones, por ejemplo `support@YourDestination.com`.*

## Casos de uso {#use-cases}

Para ayudarle a comprender mejor cómo y cuándo debe usar la variable *YourDestination* destino, aquí hay ejemplos de casos de uso que los clientes de Adobe Experience Platform pueden resolver utilizando este destino.

### Caso de uso número 1

*Para plataformas de mensajería móvil:*

*Una plataforma de ventas y alquiler de casas quiere enviar notificaciones móviles a los dispositivos Android y iOS de los clientes para informarles de que hay 100 anuncios actualizados en el área donde previamente buscaron un alquiler.*

### Caso de uso n.º 2

*Para plataformas de redes sociales:*

*Una marca de ropa deportiva quiere llegar a los clientes existentes a través de sus cuentas de medios sociales. La marca de ropa puede introducir direcciones de correo electrónico de su propio CRM a Adobe Experience Platform, generar segmentos a partir de sus propios datos sin conexión y enviar estos segmentos a YourDestination para mostrar anuncios en las fuentes de medios sociales de sus clientes.*

## Requisitos previos {#prerequisites}

*Agregue información en esta sección sobre cualquier cosa que los clientes deban tener en cuenta antes de comenzar a configurar el destino en la interfaz de usuario de Adobe Experience Platform. Esto puede tratarse de:*

* *necesidad de añadirlo a una lista de permitidos*
* *requisitos para el hash de correo electrónico*
* *cualquier información específica de la cuenta de su parte*
* *cómo obtener una clave de API para conectarse a la plataforma*

*Puede vincular a su documentación relevante si esto resulta útil para los clientes.*

## Identidades compatibles {#supported-identities}

*Agregue información en esta sección sobre las identidades admitidas por el destino. Hemos rellenado previamente la tabla con algunos valores estándar. Elimine los valores que no se apliquen al destino y los que no estén precompletados.*

*YourDestination* admite la activación de identidades descritas en la tabla siguiente. Más información sobre [identidades](/help/identity-service/namespaces.md).

| Identidad de Target | Descripción | Consideraciones |
|---|---|---|
| GAID | Google Advertising ID | Seleccione la identidad objetivo GAID cuando su identidad de origen sea un área de nombres GAID. |
| IDFA | Apple ID para anunciantes | Seleccione la identidad de destino IDFA cuando la identidad de origen sea un área de nombres IDFA. |
| ECID | Experience Cloud ID | Un espacio de nombres que representa ECID. Este espacio de nombres también puede ser referenciado por los siguientes alias: &quot;Adobe Marketing Cloud ID&quot;, &quot;Adobe Experience Cloud ID&quot;, &quot;Adobe Experience Platform ID&quot;. Consulte el siguiente documento sobre [ECID](/help/identity-service/ecid.md) para obtener más información. |
| phone_sha256 | Números de teléfono con hash con el algoritmo SHA256 | Adobe Experience Platform admite los números de teléfono con texto sin formato y con hash SHA256. Si el campo de origen contiene atributos sin hash, marque la casilla de verificación **[!UICONTROL Aplicar transformación]** para [!DNL Platform] hash automático de los datos al activarlos. |
| email_lc_sha256 | Direcciones de correo electrónico con hash con el algoritmo SHA256 | Adobe Experience Platform admite las direcciones de correo electrónico con texto sin formato y con hash SHA 256. Si el campo de origen contiene atributos sin hash, marque la casilla de verificación **[!UICONTROL Aplicar transformación]** para [!DNL Platform] hash automático de los datos al activarlos. |
| extern_id | ID de usuario personalizados | Seleccione esta identidad de destino cuando la identidad de origen sea un área de nombres personalizada. |

{style=&quot;table-layout:auto&quot;}

## Tipo de exportación y frecuencia {#export-type-frequency}

*En la tabla, mantenga solo las líneas que correspondan a su destino. Debe tener una línea para Export type y otra para Export frequency. Elimine los valores que no se apliquen al destino.*

Consulte la tabla siguiente para obtener información sobre el tipo y la frecuencia de exportación de destino.

| Elemento | Tipo | Notas |
---------|----------|---------|
| Tipo de exportación | **[!UICONTROL Exportación de segmentos]** | Está exportando todos los miembros de un segmento (audiencia) con los identificadores (nombre, número de teléfono u otros) utilizados en la variable *YourDestination* destino. |
| Tipo de exportación | **[!UICONTROL Basado en perfiles]** | Está exportando todos los miembros de un segmento, junto con los campos de esquema deseados (por ejemplo: dirección de correo electrónico, número de teléfono, apellidos), tal como se elige en la pantalla seleccionar atributos de perfil del [flujo de trabajo de activación de destino](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes). |
| Frecuencia de exportación | **[!UICONTROL Transmisión]** | Los destinos de flujo continuo son conexiones basadas en API &quot;siempre activadas&quot;. Tan pronto como un perfil se actualiza en el Experience Platform en función de la evaluación de segmentos, el conector envía la actualización descendente a la plataforma de destino. Más información sobre [destinos de flujo continuo](/help/destinations/destination-types.md#streaming-destinations). |
| Frecuencia de exportación | **[!UICONTROL Lote]** | Los destinos de lote exportan archivos a plataformas descendentes en incrementos de tres, seis, ocho, doce o veinticuatro horas. Más información sobre [destinos basados en archivos por lotes](/help/destinations/destination-types.md#file-based). |

{style=&quot;table-layout:auto&quot;}

## Conectarse al destino {#connect}

>[!IMPORTANT]
> 
>Para conectarse al destino, necesita la variable **[!UICONTROL Administrar destinos]** [permiso de control de acceso](/help/access-control/home.md#permissions). Lea el [información general sobre el control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Para conectarse a este destino, siga los pasos descritos en la sección [tutorial de configuración de destino](../../ui/connect-destination.md). En el flujo de trabajo de configuración de destino, rellene los campos que aparecen en las dos secciones siguientes.

### Autenticar en destino {#authenticate}

*Agregue los campos que los clientes deben rellenar al autenticarse en el destino. Estos campos son específicos de destino y dependen de la configuración en Destination SDK. Es posible que los campos del destino no sean los mismos que los que se enumeran a continuación. Por favor, incluya también una captura de pantalla similar a la captura de pantalla de muestra que se muestra a continuación.*

Para autenticarse en el destino, rellene los campos obligatorios y seleccione **[!UICONTROL Conectarse al destino]**.

![Añada un vínculo aquí a una o más capturas de pantalla de muestra que muestran a los usuarios cómo autenticarse en el destino](/help/destinations/destination-sdk/docs-framework/assets/authenticate-destination.png)

* **[!UICONTROL Token portador]**: Rellene el token al portador para autenticarse en el destino.

### Rellenar detalles de destino {#destination-details}

*Agregue los campos que los clientes deben rellenar al configurar un nuevo destino. Estos campos son específicos de destino y dependen de la configuración en Destination SDK. Es posible que los campos del destino no sean los mismos que los que se enumeran a continuación. Por favor, incluya también una captura de pantalla similar a la captura de pantalla de muestra que se muestra a continuación.*

Para configurar los detalles del destino, rellene los campos opcionales y requeridos a continuación. Un asterisco junto a un campo en la interfaz de usuario indica que el campo es obligatorio.

![Añada un vínculo aquí a una o más capturas de pantalla de muestra que muestran a los usuarios cómo rellenar los detalles para su destino](/help/destinations/destination-sdk/docs-framework/assets/configure-destination-details.png)

* **[!UICONTROL Nombre]**: Un nombre por el cual reconocerá este destino en el futuro.
* **[!UICONTROL Descripción]**: Descripción que le ayudará a identificar este destino en el futuro.
* **[!UICONTROL ID de cuenta]**: Su *YourDestination* ID de cuenta.

### Habilitar alertas {#enable-alerts}

Puede activar las alertas para recibir notificaciones sobre el estado del flujo de datos a su destino. Seleccione una alerta de la lista para suscribirse y recibir notificaciones sobre el estado de su flujo de datos. Para obtener más información sobre las alertas, consulte la guía de [suscripción a alertas de destinos mediante la interfaz de usuario](../../ui/alerts.md).

Cuando haya terminado de proporcionar detalles para la conexión de destino, seleccione **[!UICONTROL Siguiente]**.

## Activar segmentos en este destino {#activate}

>[!IMPORTANT]
> 
>Para activar los datos, necesita la variable **[!UICONTROL Administrar destinos]**, **[!UICONTROL Activar destinos]**, **[!UICONTROL Ver perfiles]** y **[!UICONTROL Ver segmentos]** [permisos de control de acceso](/help/access-control/home.md#permissions). Lea el [información general sobre el control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Lectura [Activar perfiles y segmentos en destinos de exportación de segmentos de flujo continuo](../../ui/activate/activate-segment-streaming-destinations.md) para obtener instrucciones sobre la activación de segmentos de audiencia en este destino.

## Datos exportados / Validar exportación de datos {#exported-data}

*Agregue un párrafo sobre cómo se exportan los datos al destino. Esto ayudaría al cliente a asegurarse de que se ha integrado correctamente con su destino. Por ejemplo, puede proporcionar un JSON de muestra como el que se muestra a continuación. O bien, podría proporcionar capturas de pantalla e información de la interfaz de su destino que muestre cómo los clientes deberían esperar que los segmentos se rellenen en la plataforma de destino.*

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
        "status": "existing"
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

## Uso y gobernanza de los datos {#data-usage-governance}

Todo [!DNL Adobe Experience Platform] Los destinos de cumplen las políticas de uso de datos al administrar los datos. Para obtener información detallada sobre cómo [!DNL Adobe Experience Platform] exige el control de datos; consulte [Información general sobre la administración de datos](/help/data-governance/home.md).

## Recursos adicionales {#additional-resources}

*Puede proporcionar más vínculos a la documentación del producto o a cualquier otro recurso que considere importante para que el cliente tenga éxito.*