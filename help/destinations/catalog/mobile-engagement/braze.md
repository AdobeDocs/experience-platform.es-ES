---
keywords: móvil; brasil; mensajería;
title: Conexión con el Brazo
description: Braze es una completa plataforma de participación del cliente que ofrece experiencias relevantes e inolvidables entre los clientes y las marcas que les encantan.
exl-id: 508e79ee-7364-4553-b153-c2c00cc85a73
source-git-commit: 3d7151645bc90a2dcbd6b31251ed459029ab77c9
workflow-type: tm+mt
source-wordcount: '757'
ht-degree: 1%

---

# [!DNL Braze] connection

## Información general {#overview}

El destino [!DNL Braze] le ayuda a enviar datos de perfil a [!DNL Braze].

[!DNL Braze] es una completa plataforma de participación del cliente que ofrece experiencias relevantes y memorables entre los clientes y las marcas que aman.

Para enviar datos de perfil a [!DNL Braze], primero debe conectarse al destino.

## Detalles de destino {#specifics}

Tenga en cuenta los siguientes detalles que son específicos del destino [!DNL Braze]:

* [!DNL Adobe Experience Platform] los segmentos se exportan a  [!DNL Braze] en el  `AdobeExperiencePlatformSegments` atributo .

>[!NOTE]
>
>Tenga en cuenta que el envío de atributos personalizados adicionales a [!DNL Braze] puede causar un aumento en el consumo de puntos de datos [!DNL Braze]. Consulte con su administrador de cuentas [!DNL Braze] antes de enviar atributos personalizados adicionales.

## Casos de uso {#use-cases}

Como especialista en marketing, quiero segmentar usuarios en un destino de participación móvil, con segmentos incorporados en [!DNL Adobe Experience Platform]. Además, quiero ofrecerles experiencias personalizadas basadas en atributos de sus perfiles [!DNL Adobe Experience Platform] en cuanto los segmentos y perfiles se actualicen en [!DNL Adobe Experience Platform].

## Identidades compatibles {#supported-identities}

[!DNL Braze] admite la activación de identidades descritas en la tabla siguiente.

| Identidad de Target | Descripción | Consideraciones |
|---|---|---|
| external_id | Identificador personalizado [!DNL Braze] que admite la asignación de cualquier identidad. | Puede enviar cualquier [identidad](../../../identity-service/namespaces.md) al destino [!DNL Braze], siempre y cuando lo asigne al [!DNL Braze] [`external_id`](https://www.braze.com/docs/api/basics/#external-user-id-explanation). |

## Tipo de exportación {#export-type}

**[!DNL Profile-based]** - está exportando todos los miembros de un segmento, junto con los campos de esquema deseados (por ejemplo: dirección de correo electrónico, número de teléfono, apellidos) o identidades, según la asignación de campos.
[!DNL Adobe Experience Platform] los segmentos se exportan a  [!DNL Braze] en el  `AdobeExperiencePlatformSegments` atributo .

## Conectarse al destino {#connect}

Para conectarse a este destino, siga los pasos descritos en el [tutorial de configuración de destino](../../ui/connect-destination.md).

### Parámetros de conexión {#parameters}

Mientras [configura](../../ui/connect-destination.md) este destino, debe proporcionar la siguiente información:

* **[!UICONTROL Token]** de cuenta en el espacio: Esta es tu  [!DNL Braze] [!DNL API] llave. Puede encontrar instrucciones detalladas sobre cómo obtener su clave [!DNL API] aquí: [Información general sobre la clave de API de REST](https://www.braze.com/docs/api/api_key/).
* **[!UICONTROL Nombre]**: introduzca un nombre por el que reconozca este destino en el futuro.
* **[!UICONTROL Descripción]**: escriba una descripción que le ayudará a identificar este destino en el futuro.
* **[!UICONTROL Instancia de extremo]**: pregunte a su  [!DNL Braze] representante qué instancia de extremo debe utilizar.

## Activar segmentos en este destino {#activate}

Consulte [Activar datos de audiencia en destinos de exportación de segmentos de flujo continuo](../../ui/activate-segment-streaming-destinations.md) para obtener instrucciones sobre cómo activar segmentos de audiencia en este destino.

## Consideraciones de asignación {#mapping-considerations}

Para enviar correctamente los datos de audiencia de [!DNL Adobe Experience Platform] al destino [!DNL Braze] , debe pasar por el paso de asignación de campos.

La asignación consiste en crear un vínculo entre los campos de esquema [!DNL Experience Data Model] (XDM) de la cuenta [!DNL Platform] y sus equivalentes correspondientes del destino de destino.

Para asignar correctamente los campos XDM a los campos de destino [!DNL Braze] , siga estos pasos:

En el paso [!UICONTROL Mapping], haga clic en **[!UICONTROL Add new mapping]**.

![Asignación de agregación de destino de Brazo](../../assets/catalog/mobile-engagement/braze/mapping.png)

En la sección [!UICONTROL Source Field] , haga clic en el botón de flecha situado junto al campo vacío.

![Asignación de origen de destino de Brazo](../../assets/catalog/mobile-engagement/braze/mapping-source.png)

En la ventana [!UICONTROL Select source field], puede elegir entre dos categorías de campos XDM:
* [!UICONTROL Seleccionar atributos]: utilice esta opción para asignar un campo específico del esquema XDM a un  [!DNL Braze] atributo.

![Atributo de origen de asignación de destino de Brazo](../../assets/catalog/mobile-engagement/braze/mapping-attributes.png)

* [!UICONTROL Seleccionar área de nombres de identidad]: Utilice esta opción para asignar un área de nombres de  [!DNL Platform] identidad a un área de  [!DNL Braze] nombres.

![Espacio de nombres de origen de asignación de destino de Brazo](../../assets/catalog/mobile-engagement/braze/mapping-namespaces.png)

Elija el campo de origen y haga clic en **[!UICONTROL Seleccionar]**.

En la sección [!UICONTROL Target Field] , haga clic en el icono de asignación a la derecha del campo.

![Asignación de destino de Brazo](../../assets/catalog/mobile-engagement/braze/mapping-target.png)

En la ventana [!UICONTROL Select target field] , puede elegir entre dos categorías de campos de destino:
* [!UICONTROL Seleccionar área de nombres de identidad]: Utilice esta opción para asignar áreas de nombres de  [!DNL Platform] identidad a espacios de nombres de  [!DNL Braze] identidad.
* [!UICONTROL Seleccione atributos] personalizados: Utilice esta opción para asignar atributos XDM a  [!DNL Braze] atributos personalizados que haya definido en la  [!DNL Braze] cuenta. <br> También puede utilizar esta opción para cambiar el nombre de los atributos XDM existentes a  [!DNL Braze]. Por ejemplo, si se asigna un atributo `lastName` XDM a un atributo `Last_Name` personalizado en [!DNL Braze], se creará el atributo `Last_Name` en [!DNL Braze], si no existe, y se le asignará el atributo `lastName` XDM.

![Campos de asignación de destino de Brazo](../../assets/catalog/mobile-engagement/braze/mapping-target-fields.png)

Elija el campo de destino y haga clic en **[!UICONTROL Seleccionar]**.

Ahora debería ver la asignación de campos en la lista .

![Finalización de asignación de destino de Brazo](../../assets/catalog/mobile-engagement/braze/mapping-complete.png)

Para agregar más asignaciones, repita los pasos anteriores.

## Ejemplo de asignación {#mapping-example}

Supongamos que el esquema de perfil XDM y la instancia [!DNL Braze] contienen los siguientes atributos e identidades:

|  | Esquema de perfil XDM | [!DNL Braze] Instancia |
|---|---|---|
| Atributos | <ul><li>person.name.firstName</code></li><li>person.name.lastName</code></li><li>mobilePhone.number</code></li></ul> | <ul><li>Nombre</code></li><li>Apellido</code></li><li>PhoneNumber</code></li></ul> |
| Identidades | <ul><li>Correo electrónico</code></li><li>Google Ad ID (GAID)</code></li><li>ID de Apple para anunciantes (IDFA)</code></li></ul> | <ul><li>external_id</code></li></ul> |

La asignación correcta tendría este aspecto:

![Ejemplo de asignación de destino de Brazo](../../assets/catalog/mobile-engagement/braze/mapping-example.png)

## Datos exportados {#exported-data}

Para verificar si los datos se han exportado correctamente al destino [!DNL Braze] , compruebe su cuenta [!DNL Braze]. [!DNL Adobe Experience Platform] los segmentos se exportan a  [!DNL Braze] en el  `AdobeExperiencePlatformSegments` atributo .

## Uso y gobernanza de los datos {#data-usage-governance}

Todos los destinos [!DNL Adobe Experience Platform] cumplen las políticas de uso de datos al administrar los datos. Para obtener información detallada sobre cómo [!DNL Adobe Experience Platform] aplica el control de datos, consulte [Información general sobre el control de datos](../../../data-governance/home.md).
