---
keywords: 'publicidad; criteo; '
title: Conexión con Criteo
description: Criteo impulsa la publicidad confiable e impactante para traer experiencias más ricas a todos los consumidores a través del internet abierto. Con el mayor conjunto de datos comerciales del mundo y la mejor IA de su clase, Criteo garantiza que cada punto de contacto a través del recorrido de compras esté personalizado para llegar a los clientes con el anuncio correcto, en el momento adecuado.
source-git-commit: a3263a322012a48f37cee6137054c7fcf3cdb8a2
workflow-type: tm+mt
source-wordcount: '749'
ht-degree: 3%

---


# (Beta) Conexión con Criteo

## Información general {#overview}

>[!IMPORTANT]
>
>Esta página de documentación fue creada por Criteo. Actualmente es un producto beta. Para cualquier consulta o actualización de solicitudes, contacte directamente con Criteo [here](mailto:criteoTechnicalPartnerships@criteo.com).

Criteo impulsa la publicidad confiable e impactante para traer experiencias más ricas a todos los consumidores a través del internet abierto. Con el mayor conjunto de datos comerciales del mundo y la mejor IA de su clase, Criteo garantiza que cada punto de contacto a través del recorrido de compras esté personalizado para llegar a los clientes con el anuncio correcto, en el momento adecuado.

## Requisitos previos {#prerequisites}

* Debe tener una cuenta de usuario administrador en [Centro de gestión de Criteo](https://marketing.criteo.com).
* Necesitarás tu ID de Anunciante de Criteo (pregunta a tu contacto de Criteo si no tienes este ID).
* Criteo solo acepta correos SHA-256 y de texto sin formato (para ser transformados en SHA-256 antes de enviarlos). No envíe ningún PII (información personal de identificación, como los nombres o números de teléfono de las personas).

![Requisitos previos](../../assets/catalog/advertising/criteo/prerequisites.png)

## Identidades compatibles {#supported-identities}

Criteo apoya la activación de las identidades descritas en la siguiente tabla. Más información sobre [identidades](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=en#getting-started).

| Identidad de Target | Descripción | Consideraciones |
| --- | --- | --- |
| `email_sha256` | Direcciones de correo electrónico con hash con el algoritmo SHA-256 | Adobe Experience Platform admite las direcciones de correo electrónico tanto de texto sin formato como con hash SHA-256. Si el campo de origen contiene atributos sin hash, marque la casilla de verificación [!UICONTROL Aplicar transformación] , para que Platform haga hash automáticamente en los datos al activarlos. |

## Tipo de exportación y frecuencia {#export-type-frequency}

Consulte la tabla siguiente para obtener información sobre el tipo y la frecuencia de exportación de destino.

| Elemento | Tipo | Notas |
| --- | --- | --- |
| Tipo de exportación | Exportación de segmentos | Está exportando todos los miembros de un segmento (audiencia) con los identificadores (nombre, número de teléfono u otros) utilizados en la variable [!DNL Criteo] destino. |
| Frecuencia de exportación | Transmisión | Los destinos de flujo continuo son conexiones basadas en API &quot;siempre activadas&quot;. Tan pronto como un perfil se actualiza en el Experience Platform en función de la evaluación de segmentos, el conector envía la actualización descendente a la plataforma de destino. Más información sobre [destinos de flujo continuo](../../destination-types.md#streaming-destinations). |

## Casos de uso {#use-cases}

Para ayudarle a comprender mejor cómo usar la variable [!DNL Criteo] destino: estos son algunos de los objetivos que los clientes de Adobe Experience Platform pueden lograr [!DNL Criteo]:

### Caso de uso 1 : Obtener tráfico

Mostrará su negocio con ofertas de productos relevantes y creativos flexibles. Con las recomendaciones inteligentes de productos, sus publicidades incluirán automáticamente los productos con mayor probabilidad de déclencheur de visitas y participación. La orientación flexible le permite crear audiencias a partir del conjunto de datos comerciales de Criteo o de sus propias listas de posibles clientes y segmentos CDP de Adobe.

### Caso de uso 2 : Aumento de las conversiones de sitios web

Cuando los visitantes abandonen el sitio web, recuerde lo que faltan con los anuncios de redireccionamiento que aumentan las conversiones al mostrar ofertas especiales e hiper-relevantes, dondequiera que vayan a continuación. Conecte su segmento CDP de Adobe para volver a atraer a los clientes existentes o dirigirse a consumidores similares a los más fieles compradores.

## Conectarse a Criteo {#connect}

Para conectarse a este destino, siga los pasos descritos en la sección [tutorial de configuración de destino](../../ui/connect-destination.md).

### Autenticarse con Criteo

Los pasos para conectar son los siguientes:

1. Inicie sesión en Adobe Experience Platform y conéctese al destino de Criteo.

   ![Iniciar sesión](../../assets/catalog/advertising/criteo/connect-destination.png)

1. Se le redirigirá a Criteo para que autorice la conexión. Es posible que primero deba iniciar sesión con sus credenciales de Criteo:

   ![Inicio de sesión de Criteo](../../assets/catalog/advertising/criteo/log-in-1.png)

   ![Inicio de sesión de Criteo](../../assets/catalog/advertising/criteo/log-in-2.png)

   ![Inicio de sesión de Criteo](../../assets/catalog/advertising/criteo/log-in-3.png)


### Parámetros de conexión {#connection-parameters}

Después de autenticarse en el destino, rellene los siguientes parámetros de conexión.

![Parámetros de conexión](../../assets/catalog/advertising/criteo/connection-parameters.png)

| Campo | Descripción | Requerido |
| --- | --- | --- |
| Nombre | Un nombre que le ayudará a reconocer este destino en el futuro. El nombre que elija aquí será el [!DNL Audience] nombre en el Centro de Gestión de Criteo y no se puede modificar en una etapa posterior. | Sí |
| Descripción | Una descripción para ayudarle a identificar este destino en el futuro. | No |
| Versión de API | Versión de la API de Criteo. Seleccione Vista previa. | Sí |
| ID del anunciante | Criteo Advertiser ID de su organización. Póngase en contacto con su gestor de cuentas de Criteo para obtener esta información. | Sí |

## Activar segmentos en este destino {#activate-segments}

Lectura [Activar perfiles y segmentos en destinos de exportación de segmentos de flujo continuo](../../ui/activate-segment-streaming-destinations.md) para obtener instrucciones sobre la activación de segmentos de audiencia en este destino.

## Datos exportados {#exported-data}

Puede ver los segmentos exportados en la [Centro de gestión de Criteo](https://marketing.criteo.com/audience-manager/dashboard).

El organismo de solicitud recibido por el [!DNL Criteo] La conexión tiene un aspecto similar al siguiente:

```json
{ 
  "data": { 
    "type": "ContactlistWithUserAttributesAmendment", 
    "attributes": { 
      "operation": "add", 
      "identifierType": "sha256email", 
      "identifiers": [ 
        { 
          "identifier": "1c8494bbc4968277345133cca6ba257b9b3431b8a84833a99613cf075a62a16d", 
          "attributes": [{ "key": "customValue", "value": "1" }] 
        } 
      ] 
    } 
  } 
} 
```

## Uso y gobernanza de los datos {#data-usage}

Todos los destinos de Adobe Experience Platform cumplen las políticas de uso de datos al administrar los datos. Para obtener información detallada sobre cómo Adobe Experience Platform aplica la administración de datos, lea la [Información general sobre la administración de datos](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html?lang=en).

## Recursos adicionales

* [Centro de ayuda de Criteo](https://help.criteo.com/kb/en)
* [Portal para desarrolladores de Criteo](https://developers.criteo.com/marketing-solutions/v2022.04/reference/modifyaudienceuserswithattributes)
