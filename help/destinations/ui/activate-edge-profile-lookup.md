---
title: Búsqueda de atributos de perfil de Edge en tiempo real
description: Aprenda a buscar atributos de perfil de Edge en tiempo real, mediante la API de Edge Network y destino de Personalization personalizada
type: Tutorial
source-git-commit: 6414168c1deb047af30d8636ef8d61316f56aecf
workflow-type: tm+mt
source-wordcount: '1904'
ht-degree: 2%

---


# Búsqueda de atributos de perfil en Edge en tiempo real

Adobe Experience Platform usa el [perfil del cliente en tiempo real](../../profile/home.md) como única fuente fiable para todos los datos de perfil. Para recuperar datos de forma rápida y en tiempo real, utiliza [perfiles Edge](../../profile/edge-profiles.md), que son perfiles ligeros distribuidos por todo el [Edge Network](../../collection/home.md#edge). Esto permite casos de uso de personalización rápidos en tiempo real.

## Casos de uso {#use-cases}

A continuación se muestran dos casos de uso en los que la búsqueda de perfiles de Edge puede ayudar.

* **Real-Time Personalization**: Recupere rápidamente información de perfil del perfil de Edge para personalizar la experiencia de un usuario en su sitio web.
* **Atención al cliente**: recupera información de perfil en tiempo real cuando un cliente llama a un agente del centro de asistencia.

En esta página se describen los pasos que debe seguir para buscar datos de perfil de Edge en tiempo real, para ofrecer experiencias de personalización o informar a las reglas de toma de decisiones a través de aplicaciones de flujo descendente.

## Terminología y requisitos previos {#prerequisites}

Al configurar el caso de uso descrito en esta página, utilizará los siguientes componentes de Platform:

* [Datastreams](../../datastreams/overview.md): un conjunto de datos recibe datos de evento entrantes del SDK web y responde con datos de perfil Edge.
* [Políticas de combinación](../../segmentation/ui/segment-builder.md#merge-policies): Creará una política de combinación [!UICONTROL Activa en Edge] para garantizar que los perfiles de Edge utilicen correctamente los datos de perfil.
* [Conexión personalizada de Personalization](../catalog/personalization/custom-personalization.md): configurará una nueva conexión personalizada que enviará los atributos de perfil al Edge Network.
* [API de Edge Network](../../server-api/overview.md): usará la funcionalidad de la API de Edge Network [recopilación interactiva de datos](../../server-api/interactive-data-collection.md) para recuperar rápidamente atributos de perfil de los perfiles de Edge.

## Protecciones de rendimiento {#guardrails}

Los casos de uso de búsqueda de perfiles de Edge están sujetos a las protecciones de rendimiento específicas que se describen en la tabla siguiente. Para obtener más información acerca de las protecciones de la API de Edge Network, consulte la [página de documentación](https://developer.adobe.com/data-collection-apis/docs/getting-started/guardrails/) de las protecciones.

| Servicio de Edge Network | Segmentación de Edge | Solicitudes por segundo |
|---------|----------|---------|
| [Destino de personalización personalizado](../catalog/personalization/custom-personalization.md) mediante [API de Edge Network](https://developer.adobe.com/data-collection-apis/docs/api/) | Sí | 1500 |
| [Destino de personalización personalizado](../catalog/personalization/custom-personalization.md) mediante [API de Edge Network](https://developer.adobe.com/data-collection-apis/docs/api/) | No | 1500 |

## Paso 1: Crear y configurar una secuencia de datos {#create-datastream}

Siga los pasos de la documentación de [configuración de secuencia de datos](../../datastreams/configure.md#create-a-datastream) para crear una nueva secuencia de datos con la siguiente configuración de **[!UICONTROL Servicio]**:

* **[!UICONTROL Servicio]**: [!UICONTROL Adobe Experience Platform]
* **[!UICONTROL Destinos de Personalization]**: Habilitado
* **[!UICONTROL Segmentación de Edge]**: Si necesita segmentación de Edge, habilite esta opción. Si solo le interesa buscar atributos de perfil en el perímetro de, pero no desea realizar ninguna segmentación basada en los perfiles de Edge, deje esta opción desactivada.


  <!-- >[!IMPORTANT]
    >
    >Enabling edge segmentation limits the maximum number of lookup requests to 1500 request per second. If you need a higher request throughput, disable edge segmentation for your datastream. See the [guardrails documentation](../guardrails.md#edge-destinations-activation) for detailed information. -->

  ![Imagen de la interfaz de usuario de Platform que muestra la pantalla de configuración de secuencia de datos.](../assets/ui/activate-edge-profile-lookup/datastream-config.png)


## Paso 2: Configurar las audiencias para la evaluación de Edge {#audience-edge-evaluation}

La búsqueda de atributos de perfil en Edge requiere que las audiencias estén configuradas para la evaluación de Edge.

Asegúrese de que las audiencias que planea activar tengan [Active-on-Edge Merge Policy](../../segmentation/ui/segment-builder.md#merge-policies) establecida como predeterminada. La política de combinación [!DNL Active-On-Edge] garantiza que las audiencias se evalúen constantemente [en el perímetro](../../segmentation/ui/edge-segmentation.md) y que estén disponibles para casos de uso de personalización en tiempo real.

Siga las instrucciones de [creación de una política de combinación](../../profile/merge-policies/ui-guide.md#create-a-merge-policy) y asegúrese de habilitar la opción **[!UICONTROL Política de combinación activa en Edge]**.

>[!IMPORTANT]
>
>Si las audiencias utilizan una política de combinación diferente, no podrá recuperar atributos de perfil de Edge y no podrá realizar búsquedas de perfiles de Edge.

## Paso 3: Envío de datos de atributos de perfil al Edge Network{#configure-custom-personalization-connection}

Para buscar perfiles Edge, incluidos atributos y datos de pertenencia a audiencias, en tiempo real, los datos deben estar disponibles en el Edge Network. Para ello, debe crear una conexión con un destino de **[!UICONTROL Personalization personalizado con atributos]** y activar las audiencias, incluidos los atributos que desee buscar en los perfiles de Edge.

+++ Configuración de un Personalization personalizado con conexión de atributos

Siga el [tutorial de creación de conexión de destino](../ui/connect-destination.md) para obtener instrucciones detalladas sobre cómo crear una nueva conexión de destino.

Al configurar el nuevo destino, seleccione la secuencia de datos que creó en el [paso 1](#create-datastream) en el campo **[!UICONTROL ID de secuencia de datos]**. Para **[!UICONTROL alias de integración]**, puede usar cualquier valor que le ayude a identificar esta conexión de destino en el futuro, como el nombre del destino.

![Imagen de la interfaz de usuario del Experience Platform que muestra la pantalla de configuración Personalization personalizado con atributos.](../assets/ui/activate-edge-profile-lookup/destination-config.png)

+++

+++Active las audiencias en la conexión Personalization personalizado con atributos

Después de crear una conexión de **[!UICONTROL Personalization personalizado con atributos]**, ya puede enviar datos de perfil al Edge Network.

>[!IMPORTANT]
> 
> * Para activar los datos y habilitar el [paso de asignación](#mapping) del flujo de trabajo, necesita los **[!UICONTROL permisos de control de acceso]**, **[!UICONTROL Activar destinos]**, **[!UICONTROL Ver perfiles]** y **[!UICONTROL Ver segmentos]** [para ver los destinos](/help/access-control/home.md#permissions).
> 
> Lea la [descripción general del control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

1. Vaya a **[!UICONTROL Conexiones > Destinos]** y seleccione la pestaña **[!UICONTROL Catálogo]**.

   ![Ficha Catálogo de destino resaltada en la interfaz de usuario del Experience Platform.](../assets/ui/activate-edge-personalization-destinations/catalog-tab.png)

1. Busque la tarjeta de destino **[!UICONTROL Personalization personalizado con atributos]** y, a continuación, seleccione **[!UICONTROL Activar audiencias]**, como se muestra en la imagen siguiente.

   ![Activar el control de audiencia resaltado en una tarjeta de destino del catálogo.](../assets/ui/activate-edge-personalization-destinations/activate-audiences-button.png)

1. Seleccione la conexión de destino que configuró anteriormente, luego seleccione **[!UICONTROL Siguiente]**.

   ![Seleccionar paso de destino en el flujo de trabajo de activación.](../assets/ui/activate-edge-personalization-destinations/select-destination.png)

1. Seleccione las audiencias. Utilice las casillas de verificación de la izquierda de los nombres de audiencia para seleccionar las audiencias que desea activar en el destino y, a continuación, seleccione **[!UICONTROL Siguiente]**.

   Puede seleccionar entre varios tipos de audiencias, según su origen:

   * **[!UICONTROL Servicio de segmentación]**: Audiencias generadas en Experience Platform por el servicio de segmentación. Consulte la [documentación de segmentación](../../segmentation/ui/overview.md) para obtener más información.
   * **[!UICONTROL Carga personalizada]**: audiencias generadas fuera de Experience Platform y cargadas en Platform como archivos CSV. Para obtener más información sobre audiencias externas, consulte la documentación sobre [importación de una audiencia](../../segmentation/ui/overview.md#import-audience).
   * Otros tipos de audiencias, originadas en otras soluciones de Adobe, como [!DNL Audience Manager].

     ![Seleccione el paso de audiencias del flujo de trabajo de activación con varias audiencias resaltadas.](../assets/ui/activate-edge-personalization-destinations/select-audiences.png)

1. Seleccione los atributos de perfil que desea que estén disponibles para los perfiles de Edge.

   * **Seleccionar atributos de origen**. Para agregar atributos de origen, seleccione el control **[!UICONTROL Agregar nuevo campo]** en la columna **[!UICONTROL Campo de Source]** y busque o navegue hasta el campo de atributo XDM que desee, como se muestra a continuación.

     ![Grabación de pantalla que muestra cómo seleccionar un atributo de destino en el paso de asignación.](../assets/ui/activate-edge-personalization-destinations/mapping-step-select-attribute.gif)

   * **Seleccionar atributos de destino**. Para agregar atributos de destino, seleccione el control **[!UICONTROL Agregar nuevo campo]** en la columna **[!UICONTROL Campo de destino]** y escriba el nombre de atributo personalizado al que desea asignar el atributo de origen.

     ![Grabación de pantalla que muestra cómo seleccionar un atributo XDM en el paso de asignación](../assets/ui/activate-edge-personalization-destinations/mapping-step-select-target-attribute.gif)



Cuando termine de asignar atributos de perfil, seleccione **[!UICONTROL Siguiente]**.

En la página **[!UICONTROL Revisar]**, puedes ver un resumen de tu selección. Seleccione **[!UICONTROL Cancelar]** para dividir el flujo, **[!UICONTROL Atrás]** para modificar la configuración o **[!UICONTROL Finalizar]** para confirmar su selección y comenzar a enviar datos de perfil al Edge Network.

![Resumen de la selección en el paso de revisión.](../assets/ui/activate-edge-personalization-destinations/review.png)

+++

+++Evaluación de la política de consentimiento

Si su organización ha adquirido **Adobe Healthcare Shield** o **Adobe Privacy &amp; Security Shield**, seleccione **[!UICONTROL Ver directivas de consentimiento aplicables]** para ver qué directivas de consentimiento se aplican y cuántos perfiles se incluyen en la activación como resultado de ellas. Lea acerca de [evaluación de directivas de consentimiento](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation) para obtener más información.

**Comprobaciones de directivas de uso de datos**

En el paso **[!UICONTROL Revisar]**, el Experience Platform también comprueba si hay alguna infracción de la directiva de uso de datos. A continuación se muestra un ejemplo de infracción de una directiva. No puede completar el flujo de trabajo de activación de audiencia hasta que haya resuelto la infracción. Para obtener información sobre cómo resolver infracciones de directivas, lea acerca de [infracciones de directivas de uso de datos](/help/data-governance/enforcement/auto-enforcement.md#data-usage-violation) en la sección de documentación de control de datos.

![Ejemplo de infracción de directiva de datos.](../assets/common/data-policy-violation.png)

+++

+++Filtrar audiencias

En el paso **[!UICONTROL Revisar]** puede usar los filtros disponibles en la página para mostrar solo las audiencias cuya programación o asignación se haya actualizado como parte de este flujo de trabajo. También puede alternar qué columnas de tabla desea ver.

![Grabación de pantalla que muestra los filtros de audiencia disponibles en el paso de revisión.](../assets/ui/activate-edge-personalization-destinations/filter-audiences-review-step.gif)


Si está satisfecho con su selección y no se han detectado infracciones de directivas, seleccione **[!UICONTROL Finalizar]** para confirmar su selección.

+++

## Paso 4: Búsqueda de los atributos de perfil en el perímetro {#configure-edge-profile-lookup}

A estas alturas, ya debería haber [configurado su secuencia de datos](#create-datastream), ha [creado una nueva conexión de destino de Personalization personalizado con atributos](#configure-destination) y ha utilizado esta conexión para [enviar los atributos de perfil](#activate-audiences) que podrá consultar al Edge Network.

El siguiente paso es configurar la solución de personalización para recuperar atributos de perfil de los perfiles Edge.

>[!IMPORTANT]
>
>Los atributos de perfil pueden contener datos confidenciales. Para proteger estos datos, debe recuperar los atributos de perfil mediante la [API de Edge Network](../../server-api/overview.md). Además, debe recuperar los atributos de perfil a través de la API de Edge Network [extremo interactivo de recopilación de datos](../../server-api/interactive-data-collection.md), para que se autentiquen las llamadas de API.
><br>Si no sigue los requisitos anteriores, la personalización se basará únicamente en la pertenencia a audiencias y los atributos de perfil no estarán disponibles para usted.

La secuencia de datos que configuró en [paso 1](#create-datastream) ya está lista para aceptar datos de evento entrantes y responder con información de perfil de Edge.

Configure la integración para recuperar la información del perfil de Edge, como se muestra en los ejemplos siguientes.

### Solicitud {#request}

Para recuperar datos de perfil perimetral, envíe una llamada `POST` vacía al extremo `/interact`, con la identidad principal para la que busca atributos de perfil incluidos en el evento, como se muestra a continuación.

```shell
curl -X POST "https://server.adobedc.net/ee/v2/interact?dataStreamId={DATASTREAM_ID}" 
-H "Authorization: Bearer {TOKEN}" 
-H "x-gw-ims-org-id: {ORG_ID}" 
-H "x-api-key: {API_KEY}" 
-H "Content-Type: application/json" 
-d '{
    "event":
    {
        "xdm": {
            "identityMap": {
                "Email": [
                    {  
                        "id":"test123@adobetest.com",
                        "primary":true
                    }
                ]
            }
        }
    }
    
}'
```

| Parámetro | Tipo | Requerido | Descripción |
| --- | --- | --- | --- |
| `dataStreamId` | `String` | Sí. | ID de la secuencia de datos que creó en el [paso 1](#create-datastream). |

### Respuesta {#response}

Una respuesta correcta devuelve el estado HTTP `200 OK`, con un objeto `Handle` que incluye información similar a los ejemplos de las pestañas siguientes, en función de si el perfil se encuentra en el perímetro o no.

>[!NOTE]
>
>Las respuestas de API son modulares y el objeto `handle` puede incluir varios objetos `payload` de varios tipos. La información relacionada con la búsqueda del perfil de Edge se agrupa en el objeto `payload` con `"type": "activation:pull"`,

>[!BEGINTABS]

>[!TAB El perfil existe en el perímetro]

Si el perfil existe en el perímetro de, según los atributos de perfil y las audiencias activadas en el perímetro de, puede esperar una respuesta con atributos y pertenencias a audiencias similares a la de abajo.

```json
{
  "requestId": "3c600138-d785-42ca-a025-bb725f4b5da9",
  "handle": [
    {
      "payload": [
        {
          "type": "profileLookup",
          "destinationId": "9218b727-ec59-4a46-b8b9-05503f138c5d",
          "alias": "rk-demo-custom-personalization-XXXX",
          "attributes": {
            "zip": {
              "value": "19000"
            },
            "firstName": {
              "value": "Test"
            },
            "lastName": {
              "value": "User123"
            },
            "gender": {
              "value": "male"
            },
            "city": {
              "value": "Philadelphia"
            },
            "state": {
              "value": "PA"
            },
            "email": {
              "value": "test123@adobetest.com"
            }
          },
          "segments": [
            {
              "id": "85018bd8-7ad1-4e17-ae30-8389c04bd3c0",
              "namespace": "ups"
            },
            {
              "id": "d09a8159-8b30-4178-b2f2-7a8c5e3168d9",
              "namespace": "ups"
            }
          ]
        }
      ],
      "type": "activation:pull",
      "eventIndex": 0
    }
  ]
}
```

El objeto `handle` proporciona la información descrita en la tabla siguiente.

| Parámetro | Descripción |
|---------|----------|
| `payload` | El objeto `payload` que incluye la información de búsqueda perimetral. La respuesta puede contener varios objetos `payload` adicionales, que no están relacionados con la búsqueda de Edge. |
| `type` | Las cargas útiles se agrupan en la respuesta por tipo. El tipo de carga útil de la búsqueda de perfiles perimetrales siempre está establecido en `profileLookup`. |
| `destinationId` | El identificador de la instancia de conexión **[!UICONTROL Custom Personalization]** que creó en el [paso 3](#configure-custom-personalization-connection). |
| `alias` | Alias de la conexión de destino, configurado por el usuario cuando crea la conexión de destino [Personalization personalizado](../catalog/personalization/custom-personalization.md). |
| `attributes` | Esta matriz incluye los atributos de perfil de Edge de las audiencias que activó en el [paso 3](#configure-custom-personalization-connection). |
| `segments` | Esta matriz incluye las audiencias que activó en el [paso 3](#configure-custom-personalization-connection). |
| `type` | `handle` objetos están agrupados por tipo. En los casos de uso de búsqueda de perfiles perimetrales, el tipo del objeto `handle` siempre es `activation:pull`. |
| `eventIndex` | El Edge Network recibe eventos del cliente en forma de matrices. El orden de los eventos de la matriz se conserva durante su procesamiento y se refleja en este índice. La indexación de eventos comienza con `0`. |

>[!TAB El perfil no existe en el perímetro]

Si el perfil no existe en el perímetro de, recibirá una respuesta similar a la que se muestra a continuación.

```json
{
  "requestId": "531b541a-4541-419e-ac99-fd7e452f0c0f",
  "handle": [
    {
      "payload": [],
      "type": "activation:pull",
      "eventIndex": 0
    }
  ]
}
```

El objeto `handle` proporciona la información descrita en la tabla siguiente.

| Parámetro | Descripción |
|---------|----------|
| `payload` | Cuando el perfil no está presente en el perímetro, el objeto `payload` está vacío. |
| `type` | `payload` objetos están agrupados por tipo. En los casos de uso de búsqueda de perfiles perimetrales, el tipo del objeto `payload` siempre es `activation:pull`. |
| `eventIndex` | El Edge Network recibe eventos del cliente en forma de matrices. El orden de los eventos de la matriz se conserva durante su procesamiento y se refleja en este índice. La indexación de eventos comienza con `0`. |

>[!ENDTABS]

>[!SUCCESS]
>
>Si ha configurado la integración correctamente, ahora tiene acceso a los datos de perfil de Edge y puede utilizar los atributos y la pertenencia a audiencias de sus perfiles Edge para almacenar en déclencheur la personalización en tiempo real en el motor de personalización descendente.

## Conclusión {#conclusion}

Al seguir los pasos anteriores, puede buscar de forma eficaz atributos de perfil de Edge en tiempo real, lo que permite experiencias personalizadas y toma de decisiones informada a través de aplicaciones descendentes.
