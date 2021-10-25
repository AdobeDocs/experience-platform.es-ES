---
keywords: flujo continuo;
title: Conexión HTTP
description: El destino HTTP en Adobe Experience Platform le permite enviar datos de perfil a extremos HTTP de terceros.
exl-id: 165a8085-c8e6-4c9f-8033-f203522bb288
source-git-commit: 2b1cde9fc913be4d3bea71e7d56e0e5fe265a6be
workflow-type: tm+mt
source-wordcount: '357'
ht-degree: 3%

---

# (Alpha) [!DNL HTTP] connection

>[!IMPORTANT]
>
>La variable [!DNL HTTP] el destino en Platform está actualmente en alfa. La documentación y las funciones están sujetas a cambios.

## Información general {#overview}

La variable [!DNL HTTP] el destino es un [!DNL Adobe Experience Platform] destino de flujo continuo que le ayuda a enviar datos de perfil a terceros [!DNL HTTP] extremos.

Para enviar datos de perfil a [!DNL HTTP] extremos, primero debe conectarse al destino en [[!DNL Adobe Experience Platform]](#connect-destination).

## Casos de uso {#use-cases}

La variable [!DNL HTTP] El destino se dirige a los clientes que necesitan exportar datos de perfil XDM y segmentos de audiencia a genéricos [!DNL HTTP] extremos.

[!DNL HTTP] los endpoints pueden ser sistemas propios de los clientes o soluciones de terceros.

## Conectarse al destino {#connect}

Para conectarse a este destino, siga los pasos descritos en la sección [tutorial de configuración de destino](../ui/connect-destination.md).

### Parámetros de conexión {#parameters}

While [configuración](../ui/connect-destination.md) Para este destino, debe proporcionar la siguiente información:

* **[!UICONTROL httpEndpoint]**: el [!DNL URL] del extremo HTTP al que desea enviar los datos de perfil.
   * De forma opcional, puede agregar parámetros de consulta al [!UICONTROL httpEndpoint] [!DNL URL].
* **[!UICONTROL authEndpoint]**: el [!DNL URL] del extremo HTTP utilizado para [!DNL OAuth2] autenticación.
* **[!UICONTROL ID de cliente]**: el [!DNL clientID] parámetro utilizado en [!DNL OAuth2] credenciales del cliente.
* **[!UICONTROL Secreto del cliente]**: el [!DNL clientSecret] parámetro utilizado en [!DNL OAuth2] credenciales del cliente.

   >[!NOTE]
   >
   >Solo [!DNL OAuth2] actualmente se admiten credenciales de cliente.

* **[!UICONTROL Nombre]**: introduzca un nombre por el que reconozca este destino en el futuro.
* **[!UICONTROL Descripción]**: escriba una descripción que le ayudará a identificar este destino en el futuro.
* **[!UICONTROL Encabezados personalizados]**: introduzca los encabezados personalizados que desee incluir en las llamadas de destino, siguiendo este formato: `header1:value1,header2:value2,...headerN:valueN`.

   >[!IMPORTANT]
   >
   >La implementación actual requiere al menos un encabezado personalizado. Esta limitación se resolverá en una actualización futura.

## Activar segmentos en este destino {#activate}

Consulte [Activar datos de audiencia en destinos de exportación de perfil de flujo continuo](../ui/activate-streaming-profile-destinations.md) para obtener instrucciones sobre la activación de segmentos de audiencia en este destino.

### Atributos de destino {#attributes}

En el [[!UICONTROL Seleccionar atributos]](../ui/activate-streaming-profile-destinations.md#select-attributes) paso, Adobe recomienda seleccionar un identificador único de su [esquema de unión](../../profile/home.md#profile-fragments-and-union-schemas). Seleccione el identificador único y cualquier otro campo XDM que desee exportar al destino.

## Datos exportados {#exported-data}

Su exportación [!DNL Experience Platform] los datos llegan a su [!DNL HTTP] destino en formato JSON. Por ejemplo, el evento siguiente contiene el atributo de perfil de dirección de correo electrónico de una audiencia que se ha clasificado para un segmento determinado y ha salido de otro segmento. Las identidades de esta perspectiva son [!DNL ECID] y correo electrónico.

```json
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
