---
keywords: publicidad; criteo;
title: Conexión con Criteo
description: Criteo impulsa la publicidad confiable e impactante para traer experiencias más ricas a todos los consumidores a través del internet abierto. Con el mayor conjunto de datos comerciales del mundo y la mejor IA de su clase, Criteo garantiza que cada punto de contacto a través del recorrido de compras esté personalizado para llegar a los clientes con el anuncio correcto, en el momento adecuado.
exl-id: e6f394b2-ab82-47bb-8521-1cf9d01a203b
source-git-commit: 8211ca28462548e1c17675e504e6de6f5cc55e73
workflow-type: tm+mt
source-wordcount: '1007'
ht-degree: 2%

---

# (Beta) Conexión con Criteo

## Información general {#overview}

>[!IMPORTANT]
>
>Esta página de documentación fue creada por Criteo. Actualmente es un producto beta y la funcionalidad está sujeta a cambios. Para cualquier consulta o actualización de solicitudes, contacte directamente con Criteo [here](mailto:criteoTechnicalPartnerships@criteo.com).

Criteo impulsa la publicidad confiable e impactante para traer experiencias más ricas a todos los consumidores a través del internet abierto. Con el mayor conjunto de datos comerciales del mundo y la mejor IA de su clase, Criteo garantiza que cada punto de contacto a través del recorrido de compras esté personalizado para llegar a los clientes con el anuncio correcto, en el momento adecuado.

## Requisitos previos {#prerequisites}

* Debe tener una cuenta de usuario administrador en [Centro de gestión de Criteo](https://marketing.criteo.com).
* Necesitarás tu ID de Anunciante de Criteo (pregunta a tu contacto de Criteo si no tienes este ID).
* Debe proporcionar [!DNL GUM caller ID], en caso de que desee utilizar [!DNL GUM ID] como identificador.

## Limitaciones {#limitations}

* Criteo solo acepta [!DNL SHA-256]Correos electrónicos con hash y texto sin formato (para transformarlos en [!DNL SHA-256] antes de enviar). No envíe ningún PII (información de identificación personal, como nombres de personas o números de teléfono).
* Criteo necesita que el cliente proporcione al menos un identificador. Prioriza [!DNL GUM ID] como identificador sobre correo electrónico con hash, ya que contribuye a mejorar la tasa de coincidencia.

![Requisitos previos](../../assets/catalog/advertising/criteo/prerequisites.png)

## Identidades compatibles {#supported-identities}

Criteo apoya la activación de las identidades descritas en la siguiente tabla. Más información sobre [identidades](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=en#getting-started).

| Identidad de Target | Descripción | Consideraciones |
| --- | --- | --- |
| `email_sha256` | Direcciones de correo electrónico con hash con el algoritmo SHA-256 | Adobe Experience Platform admite las direcciones de correo electrónico tanto de texto sin formato como con hash SHA-256. Si el campo de origen contiene atributos sin hash, marque la casilla de verificación [!UICONTROL Aplicar transformación] , para que Platform haga hash automáticamente en los datos al activarlos. |
| `gum_id` | Criteo [!DNL GUM] identificador de cookie | [!DNL GUM IDs] permitir a los clientes mantener una correspondencia entre su sistema de identificación de usuario y la identificación de usuario de Criteo ([!DNL UID]). Si el tipo de identificador es `gum_id`, un parámetro adicional, la variable [!DNL GUM Caller ID], también debe incluirse. Póngase en contacto con el equipo de su cuenta de Criteo para obtener información apropiada [!DNL GUM Caller ID] o para obtener más información sobre esto [!DNL GUM ID] sincronizar, si es necesario. |

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

>[!IMPORTANT]
> 
>Para conectarse al destino, necesita la variable **[!UICONTROL Administrar destinos]** [permiso de control de acceso](/help/access-control/home.md#permissions). Lea el [información general sobre el control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

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
| ID del anunciante | Criteo Advertiser ID de su organización. Póngase en contacto con su gestor de cuentas de Criteo para obtener esta información. | Sí |
| Criteo [!DNL GUM caller ID] | [!DNL GUM Caller ID] de su organización. Póngase en contacto con el equipo de su cuenta de Criteo para obtener información apropiada [!DNL GUM Caller ID] o para obtener más información sobre esto [!DNL GUM] sincronizar, si es necesario. | Sí, siempre [!DNL GUM ID] se proporciona como identificador |

### Habilitar alertas {#enable-alerts}

Puede activar las alertas para recibir notificaciones sobre el estado del flujo de datos a su destino. Seleccione una alerta de la lista para suscribirse y recibir notificaciones sobre el estado de su flujo de datos. Para obtener más información sobre las alertas, consulte la guía de [suscripción a alertas de destinos mediante la interfaz de usuario](../../ui/alerts.md).

Cuando haya terminado de proporcionar detalles para la conexión de destino, seleccione **[!UICONTROL Siguiente]**.

## Activar segmentos en este destino {#activate-segments}

>[!IMPORTANT]
> 
>Para activar los datos, necesita la variable **[!UICONTROL Administrar destinos]**, **[!UICONTROL Activar destinos]**, **[!UICONTROL Ver perfiles]** y **[!UICONTROL Ver segmentos]** [permisos de control de acceso](/help/access-control/home.md#permissions). Lea el [información general sobre el control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Lectura [Activar perfiles y segmentos en destinos de exportación de segmentos de flujo continuo](../../ui/activate-segment-streaming-destinations.md) para obtener instrucciones sobre la activación de segmentos de audiencia en este destino.

## Datos exportados {#exported-data}

Puede ver los segmentos exportados en la [Centro de gestión de Criteo](https://marketing.criteo.com/audience-manager/dashboard).

El cuerpo de la solicitud de adición de un perfil de usuario recibido por el [!DNL Criteo] La conexión tiene un aspecto similar al siguiente:

```json
{
  "data": {
    "type": "ContactlistWithUserAttributesAmendment",
    "attributes": {
      "operation": "add",
      "identifierType": "gum",
      "gumCallerId": "123",
      "identifiers": [
        {
          "identifier": "456",
          "attributes": [
            { "key": "ctoid_GumCaller", "value": "123" },
            { "key": "ctoid_Gum", "value": "456" },
            {
              "key": "ctoid_HashedEmail",
              "value": "98833030dc03751f2b2c1a0017078975fdae951aa6908668b3ec422040f2d4be"
            }
          ]
        }
      ]
    }
  }
}
```

El cuerpo de la solicitud de eliminación del perfil de usuario recibido por el [!DNL Criteo] La conexión tiene un aspecto similar al siguiente:

```json
{
  "data": {
    "type": "ContactlistWithUserAttributesAmendment",
    "attributes": {
      "operation": "remove",
      "identifierType": "gum",
      "gumCallerId": "123",
      "identifiers": [
        {
          "identifier": "456",
          "attributes": [
            { "key": "ctoid_GumCaller", "value": "123" },
            { "key": "ctoid_Gum", "value": "456" },
            {
              "key": "ctoid_HashedEmail",
              "value": "98833030dc03751f2b2c1a0017078975fdae951aa6908668b3ec422040f2d4be"
            }
          ]
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
* [Portal para desarrolladores de Criteo](https://developers.criteo.com)
