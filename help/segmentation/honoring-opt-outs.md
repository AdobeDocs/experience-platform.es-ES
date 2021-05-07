---
keywords: Experience Platform;inicio;temas populares;exclusión;segmentación;servicio de segmentación;servicio de segmentación;exclusiones por honor;exclusión;exclusión;exclusión;exclusión;exclusión
solution: Experience Platform
title: Respeto de las solicitudes de exclusión en los segmentos
topic-legacy: overview
description: Adobe Experience Platform permite a sus clientes enviar solicitudes de exclusión con respecto al uso y almacenamiento de sus datos dentro del perfil del cliente en tiempo real]. Estas solicitudes de exclusión forman parte de la Ley de Privacidad del Consumidor de California (CCPA), que otorga a los residentes de California el derecho de acceder y eliminar sus datos personales y de saber si sus datos personales se venden o revelan (y a quién).
exl-id: fe851ce3-60db-4984-a73c-f9c5964bfbad
translation-type: tm+mt
source-git-commit: ab0798851e5f2b174d9f4241ad64ac8afa20a938
workflow-type: tm+mt
source-wordcount: '1030'
ht-degree: 0%

---

# Respeto de las solicitudes de exclusión en los segmentos

Adobe Experience Platform permite a sus clientes enviar solicitudes de exclusión relativas al uso y almacenamiento de sus datos en [!DNL Real-time Customer Profile]. Estas solicitudes de exclusión forman parte de la [!DNL California Consumer Privacy Act] (CCPA), que otorga a los residentes de California el derecho de acceder y eliminar sus datos personales y de saber si sus datos personales se venden o revelan (y a quién).

Una vez que un cliente ha optado por la exclusión, es importante que su organización respete estas exclusiones al generar audiencias para actividades de marketing. En este documento se describen detalles importantes sobre la aceptación de solicitudes de exclusión.

## Primeros pasos

El cumplimiento de las solicitudes de exclusión requiere comprender los distintos servicios [!DNL Adobe Experience Platform] implicados. Antes de trabajar con solicitudes de exclusión, revise la documentación de los siguientes servicios:

- [[!DNL Real-time Customer Profile]](../profile/home.md): Proporciona un perfil de cliente unificado en tiempo real basado en datos agregados de varias fuentes.
- [[!DNL Adobe Experience Platform Segmentation Service]](./home.md): Permite generar segmentos de audiencia a partir de  [!DNL Real-time Customer Profile] datos.
- [[!DNL Experience Data Model (XDM)]](../xdm/home.md): El marco estandarizado mediante el cual Platform organiza los datos de experiencia del cliente.
- [[!DNL Adobe Experience Platform Privacy Service]](../privacy-service/home.md): Ayuda a las organizaciones a automatizar el cumplimiento de las normas de privacidad de datos que implican datos de clientes dentro de  [!DNL Platform].

## Grupos de campos de esquema de exclusión

Para cumplir las solicitudes de exclusión de CCPA, uno de los esquemas que forma parte del esquema de unión debe contener los campos de exclusión necesarios [!DNL Experience Data Model] (XDM). Hay dos grupos de campos de esquema que se pueden utilizar para agregar campos de exclusión a un esquema. Cada uno de ellos se explica con más detalle en las secciones siguientes:

- [Privacidad](#profile-privacy) del perfil: Se utiliza para capturar distintos tipos de exclusión (general o venta/uso compartido).
- [Detalles](#profile-preferences-details) de preferencias de perfil: Se utiliza para capturar solicitudes de exclusión para canales XDM específicos.

Para obtener instrucciones paso a paso sobre cómo añadir un grupo de campos a un esquema, consulte la sección &quot;Añadir un grupo de campos&quot; en la siguiente documentación de XDM:
- [Tutorial de la API del Registro de esquemas](../xdm/api/getting-started.md).: Creación de un esquema mediante la API del Registro de esquemas.
- [Tutorial del Editor de esquemas](../xdm/tutorials/create-schema-ui.md): Creación de un esquema mediante la interfaz de usuario de Platform.

A continuación, se muestra un ejemplo de imagen que muestra los grupos de campos de exclusión agregados a un esquema en la interfaz de usuario:

![](images/opt-outs/opt-out-field-groups-user-interface.png)

La estructura de cada grupo de campos, así como una descripción de los campos que contribuyen al esquema, se describen con más detalle en las siguientes secciones.

### [!DNL Profile Privacy] {#profile-privacy}

El grupo de campos [!DNL Profile Privacy] permite capturar dos tipos de solicitudes de exclusión de CCPA de los clientes:

1. Exclusión general
2. Exclusión de ventas/uso compartido

![](images/opt-outs/profile-privacy.png)

El grupo de campos [!DNL Profile Privacy] contiene los siguientes campos:

- Exclusiones en la privacidad (`privacyOptOuts`): Matriz que contiene una lista de objetos de exclusión.
- Tipo de exclusión (`optOutType`): Tipo de exclusión. Este campo es una enumeración con dos valores posibles:
   - Exclusión general (`general_opt_out`)
   - Opción de exclusión de distribución de ventas (`sales_sharing_opt_out`)
- Valor de exclusión (`optOutValue`): El estado activo de la exclusión, también conocido como el valor de la señal de exclusión, según el tipo de exclusión especificado. Este campo es una enumeración con cuatro valores posibles:
   - No proporcionado (`not_provided`): No se ha proporcionado una solicitud de exclusión.
   - Verificación pendiente (`pending`): La solicitud de exclusión está pendiente de verificación.
   - Exclusión (`out`): El cliente se ha excluido.
   - Inclusión (`in`): El cliente ha elegido la opción de inclusión.
- Marca de tiempo de exclusión (`timestamp`): Marca de tiempo de la señal de exclusión recibida.

Para ver la estructura completa del grupo de campos [!DNL Profile Privacy], consulte el [repositorio público GitHub XDM](https://github.com/adobe/xdm/blob/master/schemas/context/profile-privacy.schema.json) o previsualice el grupo de campos mediante la interfaz de usuario de Platform.

### [!DNL Profile Preferences Details] {#profile-preferences-details}

El grupo de campos [!DNL Profile Preferences Details] proporciona varios campos que representan preferencias para perfiles de clientes (como formato de correo electrónico, idioma preferido y zona horaria). Uno de los campos incluidos en este grupo de campos, OptInOut (`optInOut`), permite establecer valores de exclusión para canales individuales.

![](images/opt-outs/profile-preferences-details.png)

El grupo de campos [!DNL Profile Preferences Details] contiene los siguientes campos relacionados con las exclusiones:

- OptInOut (`optInOut`): Objeto donde cada clave representa un URI válido y conocido para un canal de comunicación y el estado activo de la exclusión para cada canal. Cada canal puede tener uno de los cuatro valores posibles:
   - No proporcionado (`not_provided`): No se ha proporcionado una solicitud de exclusión para este canal.
   - Verificación pendiente (`pending`): La solicitud de exclusión de este canal está pendiente de verificación.
   - Exclusión (`out`): El cliente ha excluido este canal.
   - Inclusión (`in`): El cliente ha elegido este canal.
- Exclusión global (`globalOptout`): Un valor booleano que, cuando se establece en true, establece una anulación de exclusión global para el perfil. El valor predeterminado de este campo es false.

El ejemplo JSON siguiente destaca cómo el objeto OptInOut puede capturar varias señales de exclusión para diferentes canales de comunicación:

```json
{
  "xdm:optInOut": {
    "https://ns.adobe.com/xdm/channels/email": "pending",
    "https://ns.adobe.com/xdm/channels/phone": "out",
    "https://ns.adobe.com/xdm/channels/sms": "in",
    "https://ns.adobe.com/xdm/channels/fax": "not_provided",
    "https://ns.adobe.com/xdm/channels/direct-mail": "not_provided",
    "https://ns.adobe.com/xdm/channels/apns": "not_provided",
    "xdm:globalOptout": false
  }
}
```

Para ver la estructura completa del grupo de campos Detalles de preferencias de perfil , visite el [repositorio GitHub público XDM](https://github.com/adobe/xdm/blob/master/schemas/context/profile-preferences-details.schema.json) o previsualice el grupo de campos utilizando la interfaz de usuario [!DNL Platform] .

## Gestión de las exclusiones en la segmentación

Para garantizar que los perfiles marcados con indicadores de exclusión de CCPA no se incluyan en los segmentos, se deben añadir campos especiales a los segmentos existentes o incluir durante la creación del segmento.

Las secciones siguientes muestran cómo añadir los campos adecuados para los dos tipos de indicadores de exclusión:
1. Exclusión general
2. Exclusión de ventas/uso compartido

### Exclusión general

[!DNL Segmentation] respeta automáticamente todos los perfiles que contienen el indicador &quot;[!UICONTROL General Opt-Out]&quot;, lo que significa que esos perfiles no se incluirán en audiencias ni exportaciones de forma predeterminada. Sin embargo, se recomienda añadir los campos adecuados para garantizar que los perfiles no seleccionados no se incluyan en las audiencias y las actividades de marketing.

Esto se puede hacer mediante la interfaz de usuario añadiendo atributos **[!UICONTROL Privacy Opt-Outs]**. En este caso, el segmento se configura para incluir solo aquellos que han elegido (lo que significa que no tienen un indicador de exclusión general en su perfil). Esto se hace declarando que &quot;[!UICONTROL Opt-Out Type]&quot; es igual a &quot;[!UICONTROL General Opt-Out]&quot; y que &quot;[!UICONTROL Opt-Out Value]&quot; es igual a &quot;[!UICONTROL Opt-in]&quot;.

![](images/opt-outs/segment-general-opt-out.png)

### Exclusión de ventas/uso compartido

Si un usuario tiene un indicador de exclusión de venta/uso compartido establecido en su perfil, este perfil ya no debe utilizarse para ninguna creación de segmentos o actividad de marketing. Para garantizar que se cumpla este indicador, el &quot;[!UICONTROL Opt-Out Type]&quot; debe ser igual a &quot;[!UICONTROL Sales Sharing Opt-Out]&quot; y el &quot;[!UICONTROL Opt-Out Value]&quot; debe ser igual a &quot;[!UICONTROL Opt-in]&quot;.

![](images/opt-outs/segment-sales-sharing-opt-out.png)

<!-- ### Overriding default exclusions

In some instances, such as building a segment of people who have opted out, it may be necessary to override the default exclusion of opted-out profiles. This override can be done via the API or in the Segment Builder user interface. -->

## Pasos siguientes

Para obtener más información sobre segmentación, incluido el trabajo con definiciones de segmentos y audiencias a través de la API y la interfaz de usuario, comience por leer la [información general de segmentación](./home.md).

Para obtener más información sobre la privacidad de datos dentro de [!DNL Platform], incluido cómo [!DNL Privacy Service] ayuda a facilitar el cumplimiento automatizado de las normas de privacidad legales y organizativas, consulte la documentación de [[!DNL Privacy Service]](../privacy-service/home.md).
