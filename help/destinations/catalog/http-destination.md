---
keywords: flujo continuo;
title: Conexión HTTP
description: El destino HTTP en Adobe Experience Platform le permite enviar datos de perfil a extremos HTTP de terceros.
exl-id: 165a8085-c8e6-4c9f-8033-f203522bb288
source-git-commit: 802b1844bec1e577e978da5d5a69de87278c04b9
workflow-type: tm+mt
source-wordcount: '361'
ht-degree: 3%

---

# (Alpha) Conexión [!DNL HTTP]

>[!IMPORTANT]
>
>El destino [!DNL HTTP] en Platform está actualmente en alfa. La documentación y las funciones están sujetas a cambios.

## Información general {#overview}

El destino [!DNL HTTP] es un destino de flujo continuo [!DNL Adobe Experience Platform] que le ayuda a enviar datos de perfil a [!DNL HTTP] extremos de terceros.

Para enviar datos de perfil a [!DNL HTTP] extremos, primero debe conectarse al destino en [[!DNL Adobe Experience Platform]](#connect-destination).

## Casos de uso {#use-cases}

El destino [!DNL HTTP] está dirigido a clientes que necesitan exportar datos de perfil XDM y segmentos de audiencia a [!DNL HTTP] extremos genéricos.

[!DNL HTTP] los endpoints pueden ser sistemas propios de los clientes o soluciones de terceros.

## Conectarse al destino {#connect}

Para conectarse a este destino, siga los pasos descritos en el [tutorial de configuración de destino](../ui/connect-destination.md).

### Parámetros de conexión {#parameters}

Mientras [configura](../ui/connect-destination.md) este destino, debe proporcionar la siguiente información:

* **[!UICONTROL httpEndpoint]**: el  [!DNL URL] del extremo HTTP al que desea enviar los datos de perfil.
   * De forma opcional, puede agregar parámetros de consulta a [!UICONTROL httpEndpoint] [!DNL URL].
* **[!UICONTROL authEndpoint]**: el  [!DNL URL] del extremo HTTP utilizado para la  [!DNL OAuth2] autenticación.
* **[!UICONTROL ID]** de cliente: el  [!DNL clientID] parámetro utilizado en las credenciales del  [!DNL OAuth2] cliente.
* **[!UICONTROL Secreto]** del cliente: el  [!DNL clientSecret] parámetro utilizado en las credenciales del  [!DNL OAuth2] cliente.

   >[!NOTE]
   >
   >Actualmente solo se admiten [!DNL OAuth2] credenciales de cliente.

* **[!UICONTROL Nombre]**: introduzca un nombre por el que reconozca este destino en el futuro.
* **[!UICONTROL Descripción]**: escriba una descripción que le ayudará a identificar este destino en el futuro.
* **[!UICONTROL Encabezados]** personalizados: introduzca los encabezados personalizados que desee incluir en las llamadas de destino, siguiendo este formato:  `header1:value1,header2:value2,...headerN:valueN`.

   >[!IMPORTANT]
   >
   >La implementación actual requiere al menos un encabezado personalizado. Esta limitación se resolverá en una actualización futura.

## Activar segmentos en este destino {#activate}

Consulte [Activar perfiles y segmentos en un destino](../ui/activate-destinations.md#select-attributes) para obtener instrucciones sobre cómo activar segmentos de audiencia en destinos.

## Atributos de destino {#attributes}

En el paso [[!UICONTROL Select attributes]](../ui/activate-destinations.md#select-attributes), al [activar segmentos](../ui/activate-destinations.md) en un destino [!DNL HTTP], el Adobe recomienda que seleccione un identificador único de su [esquema de unión](../../profile/home.md#profile-fragments-and-union-schemas). Seleccione el identificador único y cualquier otro campo XDM que desee exportar al destino.

## Datos exportados {#exported-data}

Los datos [!DNL Experience Platform] exportados llegan al destino [!DNL HTTP] en formato JSON. Por ejemplo, el evento siguiente contiene el atributo de perfil de dirección de correo electrónico de una audiencia que se ha clasificado para un segmento determinado y ha salido de otro segmento. Las identidades de este posible cliente son [!DNL ECID] y correo electrónico.

```json
{
  "person": {
    "email": "yourstruly@adobe.con"
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
