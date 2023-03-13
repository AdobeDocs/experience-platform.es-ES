---
title: Administración de identidades en el flujo de trabajo de activación de destinos
description: Descubra cómo se gestiona la exportación de identidad en el flujo de trabajo de activación, según el tipo de destino
source-git-commit: 372231ab4fc1148c1c2c0c5fdbfd3cd5328b17cc
workflow-type: tm+mt
source-wordcount: '1186'
ht-degree: 2%

---

# Administración de identidades en el flujo de trabajo de activación de destinos

Esta página describe las particularidades de cómo se exportan las identidades a diferentes tipos de destino y enseña a encontrar qué identidades están disponibles para la exportación según el destino.

>[!TIP]
>
> Para obtener información detallada sobre identidades, áreas de nombres de identidad y definiciones de términos relacionados con la identidad, lea la [descripción general del servicio de identidad](/help/identity-service/home.md).

Cada destino de la [catalogar](/help/destinations/catalog/overview.md) es ligeramente diferente, por lo que no hay una configuración única para todos los destinos. Sin embargo, hay algunos patrones que guían la configuración de los destinos y sus requisitos de identidad, como se describe en las secciones siguientes.

## Destinos basados en archivos {#file-based}

Para [destinos basados en archivos](/help/destinations/destination-types.md#file-based) (por ejemplo, [!DNL Amazon S3], SFTP, la mayoría de los destinos de marketing por correo electrónico, como [!DNL Adobe Campaign], [!DNL Oracle Eloqua], [!DNL Salesforce Marketing Cloud]), la configuración de identidad de la mayoría de estos destinos está abierta, lo que significa que no es necesario seleccionar ninguna identidad en [Seleccionar atributos](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes) del flujo de trabajo de activación por lotes.

Si decide añadir identidades a las exportaciones de archivos, tenga en cuenta que solo una identidad de la variable [área de nombres de identidad](/help/identity-service/ui/identity-graph-viewer.md#access-identity-graph-viewer) se puede seleccionar en una exportación. Al seleccionar una identidad para exportar, se selecciona automáticamente como [atributo obligatorio](/help/destinations/ui/activate-batch-profile-destinations.md#mandatory-attributes) y [clave de deduplicación](/help/destinations/ui/activate-batch-profile-destinations.md#deduplication-keys).

![Una identidad seleccionada como atributo obligatorio y clave de anulación de duplicación.](/help/destinations/assets/how-destinations-work/selected-identity.png)

Como solución alternativa, puede agregar más identidades a la exportación si se han introducido en Experience Platform como atributos. Consulte a continuación un ejemplo en el que se seleccionó la dirección de correo electrónico del atributo XDM para la exportación, además del área de nombres de identidad `Phone_E.164`.

![Ejemplo de atributo de dirección de correo electrónico seleccionado para la exportación.](/help/destinations/assets/how-destinations-work/email-selected.png)

## Exportación de una identidad desde un mapa de identidad en comparación con la exportación de una identidad como atributo XDM: las diferencias {#identity-map-or-attribute}

El número de registros exportados puede diferir, en función de si selecciona para exportar identidades del mapa de identidad o identidades que se han introducido como atributos en Experience Platform. [Políticas de combinación](/help/profile/merge-policies/overview.md) también desempeña un papel importante en el número de registros que se exportan al seleccionar identidades del mapa de identidad.

Por ejemplo, considere que de dos conjuntos de datos diferentes, tiene los siguientes fragmentos de perfil que se combinarán en un único perfil de cliente:

**Fragmento de perfil uno**

| Mapa de identidad | Nombre | Apellidos | Atributo Email |
|---------|----------|---------|--------|
| correo electrónico1, ID de fidelización1 | John | Doe | correo electrónico 1 |


**Fragmento de perfil dos**

| Mapa de identidad | Nombre | Apellidos | Atributo Email |
|---------|----------|---------|--------|
| correo electrónico2, ID de fidelización1 | John | Doe | correo electrónico 2 |

El perfil combinado tendría el siguiente aspecto:

| Mapa de identidad | Nombre | Apellidos | Atributo Email |
|---------|----------|---------|--------|
| correo electrónico 1, correo electrónico 2, ID de fidelización 1 | John | Doe | correo electrónico 2 |

El comportamiento de exportación difiere según si selecciona `IdentityMap: Email` o `xdm: personalEmail.address` para la exportación.

Si un cliente activa `IdentityMap: Email`, habrá dos registros en el archivo exportado, uno para email1 y otro para email2.

Sin embargo, si un cliente activa `xdm: personalEmail.address`, solo email2 estará presente en el registro, ya que el campo de atributo de correo electrónico solo incluye email2. Estas situaciones pueden abordar diferentes casos de uso en los que es posible que desee activar a todas las direcciones de correo electrónico que tenga registradas para un cliente o solo a la dirección de correo electrónico más reciente que tenga registrada para el cliente.

La conclusión es que el número de registros exportados depende de las políticas de combinación seleccionadas y de si selecciona identidades o atributos en la exportación.

## Destinos de streaming basados en API {#streaming-destinations}

[Destinos de streaming basados en API](/help/destinations/destination-types.md#streaming-destination) compilado con [Destination SDK](/help/destinations/destination-sdk/overview.md) (por ejemplo, [!DNL Facebook], [!DNL Google Customer Match], [!DNL Pinterest], [!DNL Braze]y otros) solo admiten ID específicos para la exportación. Para obtener información detallada sobre las identidades específicas que se pueden exportar a cada destino, lea la *identidades admitidas* en cada página de documentación de destino (por ejemplo, consulte la sección [sección identidades admitidas](/help/destinations/catalog/advertising/pinterest.md) en el [!DNL Pinterest] página de destino).

Sin embargo, tenga en cuenta que tiene la flexibilidad de usar datos de [gráficos privados](/help/profile/merge-policies/overview.md#id-stitching) o de atributos como identidades. Esto significa que se pueden asignar atributos XDM al campo de identidad requerido por el destino. Consulte a continuación un ejemplo para la [!DNL Pinterest] destino, donde el atributo XDM `personalEmail.address` se asigna al requerido [!DNL Pinterest] identidad `pinterest_audience`.

>[!TIP]
>
>Si el campo de origen contiene atributos sin hash, marque la **[!UICONTROL Aplicar transformación]** opción para que el Experience Platform hash automáticamente los datos en la activación. Más información sobre la **[!UICONTROL Aplicar transformación]** en la opción [tutorial de activación de destinos de streaming](/help/destinations/ui/activate-segment-streaming-destinations.md#apply-transformation).

![Ejemplo de atributo de dirección de correo electrónico asignado al campo de identidad para el destino de Pinterest.](/help/destinations/assets/how-destinations-work/email-mapped-to-identity.png)

### Destinos publicitarios que dependen de integraciones de cookies de terceros {#third-party-cookie-destinations}

Destinos publicitarios que dependen de cookies de terceros (por ejemplo: [!DNL Google Ads], [!DNL Google Ad Manager], [!DNL Google DV360], [!DNL Bing], [!DNL The Trade Desk]) no requieren que los clientes seleccionen ID en el flujo de trabajo de activación. Para estos destinos, al configurar un flujo de trabajo de activación, Experience Platform busca automáticamente la tabla de coincidencia de identidades creada por [[!UICONTROL Servicio de ID de Experience Cloud]](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html?lang=es) y exporta todas las identidades disponibles para un perfil y admitidas por el destino.

Estos destinos requieren que se produzca una sincronización de ID a través de [!UICONTROL Servicio de ID de Experience Cloud] o mediante [!UICONTROL SDK web de Experience Platform].

Si está utilizando [!UICONTROL SDK web de Experience Platform] y el legado [!UICONTROL Servicio de ID de Experience Cloud] no está implementado en la página, por lo que debe asegurarse de que el conjunto de datos del sitio web en cuestión esté habilitado para permitir la sincronización de ID de terceros, como se describe en la [configuración de documentación de secuencia de datos](/help/edge/datastreams/configure.md#create).

Al configurar una secuencia de datos como se describe en la documentación vinculada anteriormente, debe asegurarse de que la variable **[!UICONTROL Sincronización de ID de terceros]** el control deslizante está activado. La mayoría de los clientes dejarían el `container_id` en blanco (el valor predeterminado es 0). Solo debe cambiar este valor si la implementación de Audience Manager heredada utiliza un ID de contenedor específico (tenga en cuenta, sin embargo, que esta sería la gran minoría de clientes).

>[!NOTE]
>
>La mayoría de estos destinos publicitarios son compatibles con Audience Manager (estos tipos de destinos se conocen en Audience Manager como destinos basados en dispositivos). Consulte un [lista de todos los destinos basados en dispositivos admitidos en Audience Manager](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/device-based/device-based-destinations-list.html?lang=en)). Solo unas pocas aparecen en Experience Platform. Para obtener información sobre cómo compartir datos entre el Experience Platform y el Audience Manager, lea la sección sobre [habilitar el uso compartido de datos de Experience Platform a Audience Manager](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html?lang=en#enable-aep-to-aam-data). Actualmente, no hay ningún plan para admitir más destinos de cookies de terceros.

## Destinos empresariales {#enterprise-destinations}

[Destinos empresariales](/help/destinations/destination-types.md#streaming-profile-export) ([!DNL Amazon Kinesis], [!DNL Azure Event Hubs], API HTTP) no requieren ID específicos en la exportación de datos, ya que están diseñados para casos de uso de integración empresarial. Sin embargo, puede exportar identidades como atributos XDM o desde el mapa de identidad, si lo desea. Ver un [ejemplo de datos exportados al destino HTTP](/help/destinations/catalog/streaming/http-destination.md#exported-data), que incluye tanto el `personalEmail.address` Atributo XDM y las identidades `ECID` y `email_lc_sha256` (dirección de correo electrónico con hash) del mapa de identidad.

## Destinos de personalización {#personalization-destinations}

[Destinos de personalización (o Edge)](/help/destinations/destination-types.md#edge-personalization-destinations) (por ejemplo: Adobe Target, [!DNL Custom Personalization]) no requieren ninguna selección de identidad en el flujo de trabajo de activación, ya que la integración es una búsqueda de perfil. El cliente ([!DNL Target], [!DNL Web SDK], u otros) consulta el [[!UICONTROL Edge]](/help/collection/home.md#edge) y extrae la información de perfil que necesita para la personalización en el sitio.

<!--
![Table with all supported identities](/help/destinations/assets/how-destinations-work/identities-table.png)

-->

## Pasos siguientes {#next-steps}

Después de leer este documento, ahora sabe cómo averiguar qué identidades son compatibles o necesarias para destinos individuales. Ahora también sabe cómo funciona la selección de identidad para cada tipo de destino.

A continuación, puede leer sobre cuál [exportar configuración](/help/destinations/how-destinations-work/destinations-configurations.md) para los destinos son comunes en todos los tipos de destino, que los desarrolladores pueden configurar en un nivel de destino individual y qué configuración pueden editar los usuarios en el flujo de trabajo de activación.

También puede consultar todos los destinos disponibles en la [catalogar](/help/destinations/catalog/overview.md).