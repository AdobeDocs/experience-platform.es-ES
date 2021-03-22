---
keywords: flujo continuo;
title: Conexión HTTP
description: El destino HTTP en Adobe Experience Platform le permite enviar datos de perfil a extremos HTTP de terceros.
translation-type: tm+mt
source-git-commit: 709908196bb5df665c7e7df10dc58ee9f3b0edbf
workflow-type: tm+mt
source-wordcount: '510'
ht-degree: 2%

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

## Conectarse al destino {#connect-destination}

En **[!UICONTROL Connections]** > **[!UICONTROL Destinations]**, seleccione [!DNL HTTP API] y seleccione **[!UICONTROL Configure]**.

![Activar destino HTTP](../assets/catalog/http/activate.png)

Si ya existe una conexión con este destino, puede ver un botón **[!UICONTROL Activate]** en la tarjeta de destino. Para obtener más información sobre la diferencia entre **[!UICONTROL Activate]** y **[!UICONTROL Configure]**, consulte la sección [Catalog](../ui/destinations-workspace.md#catalog) de la documentación del espacio de trabajo de destino.

![Activar destino HTTP](../assets/catalog/http/connect.png)

En el paso [!UICONTROL Account], debe definir los detalles de conexión del extremo HTTP. Seleccione **[!UICONTROL New account]** e introduzca los detalles de conexión del extremo HTTP al que desea conectarse.
- **[!UICONTROL httpEndpoint]**: la finalización  [!DNL URL] del extremo HTTP al que desea enviar los datos de perfil.
   - De forma opcional, puede agregar parámetros de consulta a [!UICONTROL httpEndpoint] [!DNL URL].
- **[!UICONTROL authEndpoint]**: la finalización  [!DNL URL] del extremo HTTP utilizado para la  [!DNL OAuth2] autenticación.
- **[!UICONTROL Client ID]**: el  [!DNL clientID] parámetro utilizado en las credenciales del  [!DNL OAuth2] cliente.
- **[!UICONTROL Client Secret]**: el  [!DNL clientSecret] parámetro utilizado en las credenciales del  [!DNL OAuth2] cliente.

>[!NOTE]
>
>Actualmente solo se admiten [!DNL OAuth2] credenciales de cliente.

![Conexión de extremo HTTP](../assets/catalog/http/connect.png)

Haga clic en **[!UICONTROL Connect to destination]**. Una vez que la conexión se haya realizado correctamente, haga clic en **[!UICONTROL Next]**.

En el paso [!UICONTROL Authentication], introduzca las credenciales de autenticación de la cuenta:
- **[!UICONTROL Name]**: introduzca un nombre por el que reconozca este destino en el futuro.
- **[!UICONTROL Description]**: escriba una descripción que le ayudará a identificar este destino en el futuro.
- **[!UICONTROL Custom Headers]**: introduzca los encabezados personalizados que desee incluir en las llamadas de destino, siguiendo este formato:  `header1:value1,header2:value2,...headerN:valueN`.
- **[!UICONTROL Marketing actions]**: Las acciones de marketing indican la intención para la que se exportarán los datos al destino. Puede seleccionar entre las acciones de marketing definidas por el Adobe o crear su propia acción de marketing. Para obtener más información sobre las acciones de marketing, consulte la página [Control de datos en Adobe Experience Platform](/help/data-governance/policies/overview.md). Para obtener información sobre las acciones de marketing definidas por el Adobe, consulte la [Información general sobre las políticas de uso de datos](/help/data-governance/policies/overview.md).

>[!IMPORTANT]
>
>La implementación actual requiere al menos un encabezado personalizado. Esta limitación se resolverá en una actualización futura.

![Autenticación HTTP](../assets/catalog/http/authenticate.png)

**[!UICONTROL Marketing action]**: Las acciones de marketing indican la intención para la que se exportarán los datos al destino. Puede seleccionar entre las acciones de marketing definidas por el Adobe o crear su propia acción de marketing. Para obtener más información sobre las acciones de marketing, consulte [Información general sobre las políticas de uso de datos](../../data-governance/policies/overview.md).

Haga clic en **[!UICONTROL Create destination]**.

## Activar segmentos

Consulte [Activar perfiles y segmentos en un destino](../ui/activate-destinations.md#select-attributes) para obtener información sobre el flujo de trabajo de activación de segmentos.

## Atributos de destino

Durante el paso [[!UICONTROL Select attributes]](../ui/activate-destinations.md#select-attributes), al [activar segmentos](../ui/activate-destinations.md) en un destino [!DNL HTTP], se recomienda seleccionar un identificador único de su [esquema de unión](../../profile/home.md#profile-fragments-and-union-schemas). Seleccione el identificador único y cualquier otro campo XDM que desee exportar al destino.

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
