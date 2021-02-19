---
keywords: mobile; brasil; mensajería;
title: Conexión de Brazo
description: Braze es una amplia plataforma de compromiso con el cliente que ofrece experiencias relevantes e inolvidables entre los clientes y las marcas que les gustan.
translation-type: tm+mt
source-git-commit: 6e7ecfdc0b2cbf6f07e6b2220ec163289511375e
workflow-type: tm+mt
source-wordcount: '925'
ht-degree: 1%

---


# Conexión (Beta) [!DNL Braze]

>[!IMPORTANT]
>
>El destino Braze de Adobe Experience Platform está actualmente en fase beta. La documentación y las funciones están sujetas a cambios.

El destino [!DNL Braze] le ayuda a enviar datos de perfil a [!DNL Braze].

[!DNL Braze] es una completa plataforma de compromiso con el cliente que ofrece experiencias relevantes e inolvidables entre los clientes y las marcas que les gustan.

Para enviar datos de perfil a [!DNL Braze], primero debe conectarse al destino.

## Especificaciones de destino {#destination-specs}

Tenga en cuenta los siguientes detalles específicos del destino [!DNL Braze]:

* Puede enviar cualquier [identidad](../../../identity-service/namespaces.md) al destino [!DNL Braze], siempre y cuando lo asigne al [!DNL Braze] [`external_id`](https://www.braze.com/docs/api/basics/#external-user-id-explanation).
* [!DNL Adobe Experience Platform] los segmentos se exportan  [!DNL Braze] bajo el  `AdobeExperiencePlatformSegments` atributo .

>[!NOTE]
>
>Tenga en cuenta que el envío de atributos personalizados adicionales a [!DNL Braze] puede causar aumentos en el consumo de puntos de datos [!DNL Braze]. Consulte con su [!DNL Braze] administrador de cuentas antes de enviar atributos personalizados adicionales.

## Casos de uso {#use-cases}

Como especialista en mercadotecnia, quiero destinatario de usuarios en un destino de compromiso móvil, con segmentos integrados en [!DNL Adobe Experience Platform]. Además, quiero ofrecerles experiencias personalizadas, basadas en atributos de sus [!DNL Adobe Experience Platform] perfiles, tan pronto como los segmentos y perfiles se actualicen en [!DNL Adobe Experience Platform].

## Tipo de exportación {#export-type}

**[!DNL Profile-based]** - está exportando todos los miembros de un segmento, junto con los campos de esquema deseados (por ejemplo: dirección de correo electrónico, número de teléfono, apellido) y/o identidades, según la asignación de campos.
[!DNL Adobe Experience Platform] los segmentos se exportan  [!DNL Braze] bajo el  `AdobeExperiencePlatformSegments` atributo .


## Conectar al destino {#connect-destination}

En **[!UICONTROL Conexiones]** > **[!UICONTROL Destinos]**, seleccione [!DNL Braze] y seleccione **[!UICONTROL Configurar]**.

![Configurar destino de espacio](../../assets/catalog/mobile-engagement/braze/configure.png)

>[!NOTE]
>
>Si ya existe una conexión con este destino, puede ver un botón **[!UICONTROL Activar]** en la tarjeta de destino. Para obtener más información sobre la diferencia entre **[!UICONTROL Activar]** y **[!UICONTROL Configurar]**, consulte la sección [Catálogo](../../ui/destinations-workspace.md#catalog) de la documentación del espacio de trabajo de destino.
>
>![Activar destino de carro](../../assets/catalog/mobile-engagement/braze/activate.png)

En el paso [!UICONTROL Cuenta], debe proporcionar el token de cuenta [!DNL Braze]. Ésta es su clave [!DNL Braze] [!DNL API]. Puede encontrar instrucciones detalladas sobre cómo obtener su clave [!DNL API] aquí: [Información general de la clave de API de REST](https://www.braze.com/docs/api/api_key/). Introduzca el token y haga clic en **[!UICONTROL Conectar al destino]**.

![Paso de cuenta de destino de Brazo](../../assets/catalog/mobile-engagement/braze/account.png)

Haga clic en **[!UICONTROL Siguiente]**. En el paso [!UICONTROL Autenticación], debe introducir los detalles de conexión [!DNL Braze]:
* **[!UICONTROL Nombre]**: escriba un nombre por el cual reconocerá este destino en el futuro.
* **[!UICONTROL Descripción]**: escriba una descripción que le ayudará a identificar este destino en el futuro.
* **[!UICONTROL Instancia]** de extremo: pregunte a su  [!DNL Braze] representante qué instancia de extremo debe utilizar.
* **[!UICONTROL Acción]** de mercadotecnia: las acciones de mercadotecnia indican la intención de exportar los datos al destino. Puede seleccionar entre las acciones de marketing definidas por el Adobe o puede crear su propia acción de marketing. Para obtener más información sobre las acciones de mercadotecnia, consulte la página [Administración de datos en Adobe Experience Platform](../../../data-governance/policies/overview.md). Para obtener información sobre las acciones de mercadotecnia definidas por el Adobe, consulte la [información general de las directivas de uso de datos](../../../data-governance/policies/overview.md).

![Paso de autenticación de Brazo](../../assets/catalog/mobile-engagement/braze/authentication.png)

Haga clic en **[!UICONTROL Crear destino]**. Se ha creado el destino. Puede hacer clic en **[!UICONTROL Guardar y salir]** si desea activar segmentos más adelante, o bien puede seleccionar **[!UICONTROL Siguiente]** para continuar el flujo de trabajo y seleccionar los segmentos que desea activar. En cualquier caso, consulte la siguiente sección, [Activar segmentos](#activate-segments), para el resto del flujo de trabajo.

## Activar segmentos {#activate-segments}

Consulte [Activar perfiles y segmentos en un destino](../../ui/activate-destinations.md#select-attributes) para obtener información sobre el flujo de trabajo de activación de segmentos.

## Asignación de campos {#field-mapping}

Para enviar correctamente los datos de audiencia desde [!DNL Adobe Experience Platform] al destino [!DNL Braze], debe pasar por el paso de asignación de campos.

La asignación consiste en crear un vínculo entre los campos de esquema [!DNL Experience Data Model] (XDM) de su cuenta [!DNL Platform] y sus equivalentes correspondientes desde el destino de destinatario.

Para asignar correctamente los campos XDM a los campos de destino [!DNL Braze], siga estos pasos:

En el paso [!UICONTROL Mapping], haga clic en **[!UICONTROL Añadir nueva asignación]**.

![Asignación de Añado de destino de Brazo](../../assets/catalog/mobile-engagement/braze/mapping.png)

En la sección [!UICONTROL Campo de origen], haga clic en el botón de flecha situado junto al campo vacío.

![Asignación de origen de destino de Brazo](../../assets/catalog/mobile-engagement/braze/mapping-source.png)

En la ventana [!UICONTROL Seleccionar campo de origen], puede elegir entre dos categorías de campos XDM:
* [!UICONTROL Seleccionar atributos]: utilice esta opción para asignar un campo específico del esquema XDM a un  [!DNL Braze] atributo.

![Atributo de origen de asignación de destino de Brazo](../../assets/catalog/mobile-engagement/braze/mapping-attributes.png)

* [!UICONTROL Seleccionar Área de nombres] de identidad: Utilice esta opción para asignar una Área de nombres  [!DNL Platform] de identidad a una  [!DNL Braze] Área de nombres.

![Área de nombres de origen de asignación de destino de Brazo](../../assets/catalog/mobile-engagement/braze/mapping-namespaces.png)

Elija el campo de origen y haga clic en **[!UICONTROL Seleccionar]**.

En la sección [!UICONTROL Campo de Destinatario], haga clic en el icono de asignación a la derecha del campo.

![Asignación de destino de destino de Brazo](../../assets/catalog/mobile-engagement/braze/mapping-target.png)

En la ventana [!UICONTROL Seleccionar campo de destinatario], puede elegir entre tres categorías de campos de destinatario:
* [!UICONTROL Seleccionar atributos]: Utilice esta opción para asignar los atributos XDM a  [!DNL Braze] atributos estándar.
* [!UICONTROL Seleccionar Área de nombres] de identidad: Utilice esta opción para asignar Áreas de nombres  [!DNL Platform] de identidad a Áreas de nombres  [!DNL Braze] de identidad.
* [!UICONTROL Seleccionar atributos] personalizados: Utilice esta opción para asignar atributos XDM a  [!DNL Braze] atributos personalizados que haya definido en su  [!DNL Braze] cuenta.
* También puede utilizar esta opción para cambiar el nombre de los atributos XDM existentes a [!DNL Braze]. Por ejemplo, si se asigna un atributo `lastName` XDM a un atributo `Last_Name` personalizado en [!DNL Braze], se creará el atributo `Last_Name` en [!DNL Braze], si no existe, y se le asignará el atributo `lastName` XDM.

![Campos de Asignación de destino de destino de Brazo](../../assets/catalog/mobile-engagement/braze/mapping-target-fields.png)

Elija el campo de destinatario y haga clic en **[!UICONTROL Seleccionar]**.

Ahora debería ver la asignación de campos en la lista.

![Asignación de destino de Brazo finalizada](../../assets/catalog/mobile-engagement/braze/mapping-complete.png)

Para agregar más asignaciones, repita los pasos anteriores.

### Ejemplo {#mapping-example}

Supongamos que el esquema de perfil XDM y la instancia [!DNL Braze] contienen los atributos e identidades siguientes:

|  | Esquema de Perfil XDM | [!DNL Braze] Instancia |
|---|---|---|
| Atributos | <ul><li>person.name.firstName</code></li><li>person.name.lastName</code></li><li>mobilePhone.number</code></li></ul> | <ul><li>Nombre</code></li><li>Apellidos</code></li><li>PhoneNumber</code></li></ul> |
| Identidades | <ul><li>Correo electrónico</code></li><li>ID de publicidad de Google (GAID)</code></li><li>ID de Apple para anunciantes (IDFA)</code></li></ul> | <ul><li>external_id</code></li></ul> |

La asignación correcta tendría este aspecto:

![Ejemplo de Asignación de Destino de Brazo](../../assets/catalog/mobile-engagement/braze/mapping-example.png)

## Datos exportados {#exported-data}

Para verificar si los datos se han exportado correctamente al destino [!DNL Braze], compruebe su cuenta [!DNL Braze]. [!DNL Adobe Experience Platform] los segmentos se exportan  [!DNL Braze] bajo el  `AdobeExperiencePlatformSegments` atributo .

## Administración y uso de datos {#data-usage-governance}

Todos los destinos [!DNL Adobe Experience Platform] son compatibles con las políticas de uso de datos al administrar los datos. Para obtener información detallada sobre cómo [!DNL Adobe Experience Platform] aplica la administración de datos, consulte [Información general sobre la administración de datos](../../../data-governance/home.md).

