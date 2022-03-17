---
keywords: móvil; brasil; mensajería;
title: Conexión con el Brazo
description: Braze es una completa plataforma de participación del cliente que ofrece experiencias relevantes e inolvidables entre los clientes y las marcas que les encantan.
exl-id: 508e79ee-7364-4553-b153-c2c00cc85a73
source-git-commit: c5d2427635d90f3a9551e2a395d01d664005e8bc
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# [!DNL Braze] connection

## Información general {#overview}

La variable [!DNL Braze] destination le ayuda a enviar datos de perfil a [!DNL Braze].

[!DNL Braze] es una completa plataforma de participación del cliente que ofrece experiencias relevantes y memorables entre los clientes y las marcas que aman.

Para enviar datos de perfil a [!DNL Braze], primero debe conectarse al destino.

## Detalles de destino {#specifics}

Tenga en cuenta los siguientes detalles que son específicos de la variable [!DNL Braze] destino:

* [!DNL Adobe Experience Platform] los segmentos se exportan a [!DNL Braze] en el `AdobeExperiencePlatformSegments` atributo.

>[!NOTE]
>
>Tenga en cuenta que el envío de atributos personalizados adicionales a [!DNL Braze] puede causar un aumento en su [!DNL Braze] consumo de puntos de datos. Consulte con su [!DNL Braze] administrador de cuentas antes de enviar atributos personalizados adicionales.

## Casos de uso {#use-cases}

Como especialista en marketing, quiero segmentar usuarios en un destino de participación móvil, con segmentos integrados [!DNL Adobe Experience Platform]. Además, quiero ofrecerles experiencias personalizadas en función de los atributos de sus [!DNL Adobe Experience Platform] perfiles, en cuanto los segmentos y perfiles se actualicen en [!DNL Adobe Experience Platform].

## Identidades compatibles {#supported-identities}

[!DNL Braze] admite la activación de identidades descritas en la tabla siguiente.

| Identidad de Target | Descripción | Consideraciones |
|---|---|---|
| external_id | Personalizado [!DNL Braze] identificador que admite la asignación de cualquier identidad. | Puede enviar cualquier [identidad](../../../identity-service/namespaces.md) a [!DNL Braze] destino, siempre que lo asigne a la variable [!DNL Braze] [`external_id`](https://www.braze.com/docs/api/basics/#external-user-id-explanation). |

{style=&quot;table-layout:auto&quot;}

## Tipo de exportación y frecuencia {#export-type-frequency}

Consulte la tabla siguiente para obtener información sobre el tipo y la frecuencia de exportación de destino.

| Elemento | Tipo | Notas |
---------|----------|---------|
| Tipo de exportación | **[!UICONTROL Basado en perfiles]** | Está exportando todos los miembros de un segmento, junto con los campos de esquema deseados (por ejemplo: dirección de correo electrónico, número de teléfono, apellidos) o identidades, según la asignación de campos.[!DNL Adobe Experience Platform] los segmentos se exportan a [!DNL Braze] en el `AdobeExperiencePlatformSegments` atributo. |
| Frecuencia de exportación | **[!UICONTROL Transmisión]** | Los destinos de flujo continuo son conexiones basadas en API &quot;siempre activadas&quot;. Tan pronto como un perfil se actualiza en el Experience Platform en función de la evaluación de segmentos, el conector envía la actualización descendente a la plataforma de destino. Más información sobre [destinos de flujo continuo](/help/destinations/destination-types.md#streaming-destinations). |

{style=&quot;table-layout:auto&quot;}

## Conectarse al destino {#connect}

Para conectarse a este destino, siga los pasos descritos en la sección [tutorial de configuración de destino](../../ui/connect-destination.md).

### Parámetros de conexión {#parameters}

While [configuración](../../ui/connect-destination.md) Para este destino, debe proporcionar la siguiente información:

* **[!UICONTROL Token de cuenta de Brazo]**: Esta es su [!DNL Braze] [!DNL API] clave. Puede encontrar instrucciones detalladas sobre cómo obtener su [!DNL API] clave aquí: [Información general sobre la clave de API de REST](https://www.braze.com/docs/api/api_key/).
* **[!UICONTROL Nombre]**: introduzca un nombre por el que reconozca este destino en el futuro.
* **[!UICONTROL Descripción]**: escriba una descripción que le ayudará a identificar este destino en el futuro.
* **[!UICONTROL Instancia de extremo]**: pregunte a su [!DNL Braze] representa qué instancia de extremo debe utilizar.

## Activar segmentos en este destino {#activate}

Consulte [Activar datos de audiencia en destinos de exportación de segmentos de flujo continuo](../../ui/activate-segment-streaming-destinations.md) para obtener instrucciones sobre la activación de segmentos de audiencia en este destino.

## Consideraciones de asignación {#mapping-considerations}

Para enviar correctamente los datos de audiencia desde [!DNL Adobe Experience Platform] a [!DNL Braze] destino, debe pasar por el paso de asignación de campos.

La asignación consiste en crear un vínculo entre las [!DNL Experience Data Model] Campos de esquema (XDM) en el [!DNL Platform] y sus equivalentes correspondientes del destino de destino.

Para asignar correctamente los campos XDM a la variable [!DNL Braze] campos de destino, siga estos pasos:

En el [!UICONTROL Asignación] paso, haga clic en **[!UICONTROL Añadir nueva asignación]**.

![Asignación de agregación de destino de Brazo](../../assets/catalog/mobile-engagement/braze/mapping.png)

En el [!UICONTROL Campo de origen] , haga clic en el botón de flecha situado junto al campo vacío.

![Asignación de origen de destino de Brazo](../../assets/catalog/mobile-engagement/braze/mapping-source.png)

En el [!UICONTROL Seleccionar campo de origen] , puede elegir entre dos categorías de campos XDM:
* [!UICONTROL Seleccionar atributos]: utilice esta opción para asignar un campo específico del esquema XDM a un [!DNL Braze] atributo.

![Atributo de origen de asignación de destino de Brazo](../../assets/catalog/mobile-engagement/braze/mapping-attributes.png)

* [!UICONTROL Seleccionar área de nombres de identidad]: Utilice esta opción para asignar un [!DNL Platform] área de nombres de identidad a [!DNL Braze] espacio de nombres.

![Espacio de nombres de origen de asignación de destino de Brazo](../../assets/catalog/mobile-engagement/braze/mapping-namespaces.png)

Elija el campo de origen y haga clic en **[!UICONTROL Select]**.

En el [!UICONTROL Campo de destino] , haga clic en el icono mapping a la derecha del campo .

![Asignación de destino de Brazo](../../assets/catalog/mobile-engagement/braze/mapping-target.png)

En el [!UICONTROL Seleccionar campo de destino] , puede elegir entre dos categorías de campos de objetivo:
* [!UICONTROL Seleccionar área de nombres de identidad]: Usar esta opción para asignar [!DNL Platform] áreas de nombres de identidad a [!DNL Braze] áreas de nombres de identidad.
* [!UICONTROL Seleccionar atributos personalizados]: Utilice esta opción para asignar atributos XDM a [!DNL Braze] atributos que definió en su [!DNL Braze] cuenta. <br> También puede utilizar esta opción para cambiar el nombre de los atributos XDM existentes a [!DNL Braze]. Por ejemplo, la asignación de un `lastName` Atributo XDM a un `Last_Name` atributo en [!DNL Braze], creará la variable `Last_Name` atributo en [!DNL Braze], si aún no existe, y asigne la variable `lastName` Atributo XDM a él.

![Campos de asignación de destino de Brazo](../../assets/catalog/mobile-engagement/braze/mapping-target-fields.png)

Elija el campo de objetivo y haga clic en **[!UICONTROL Select]**.

Ahora debería ver la asignación de campos en la lista .

![Finalización de asignación de destino de Brazo](../../assets/catalog/mobile-engagement/braze/mapping-complete.png)

Para agregar más asignaciones, repita los pasos anteriores.

## Ejemplo de asignación {#mapping-example}

Digamos que su esquema de perfil XDM y su [!DNL Braze] contiene los siguientes atributos e identidades:

|  | Esquema de perfil XDM | [!DNL Braze] Instancia |
|---|---|---|
| Atributos | <ul><li>person.name.firstName</code></li><li>person.name.lastName</code></li><li>mobilePhone.number</code></li></ul> | <ul><li>Nombre</code></li><li>Apellido</code></li><li>PhoneNumber</code></li></ul> |
| Identidades | <ul><li>Correo electrónico</code></li><li>Google Ad ID (GAID)</code></li><li>Apple ID para anunciantes (IDFA)</code></li></ul> | <ul><li>external_id</code></li></ul> |

La asignación correcta tendría este aspecto:

![Ejemplo de asignación de destino de Brazo](../../assets/catalog/mobile-engagement/braze/mapping-example.png)

## Datos exportados {#exported-data}

Para verificar si los datos se han exportado correctamente a la variable [!DNL Braze] destino, compruebe su [!DNL Braze] cuenta. [!DNL Adobe Experience Platform] los segmentos se exportan a [!DNL Braze] en el `AdobeExperiencePlatformSegments` atributo.

## Uso y gobernanza de los datos {#data-usage-governance}

Todo [!DNL Adobe Experience Platform] Los destinos de cumplen las políticas de uso de datos al administrar los datos. Para obtener información detallada sobre cómo [!DNL Adobe Experience Platform] exige el control de datos, consulte [Información general sobre la administración de datos](../../../data-governance/home.md).
