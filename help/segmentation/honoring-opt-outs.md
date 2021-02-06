---
keywords: Experience Platform;inicio;temas populares;desactivación;Segmentación;Servicio de segmentación;servicio de segmentación;desactivación de honor;desactivación;exclusión;desactivación;
solution: Experience Platform
title: Cumplimiento de las solicitudes de exclusión en segmentos
topic: overview
description: 'Adobe Experience Platform permite a sus clientes enviar solicitudes de exclusión con respecto al uso y el almacenamiento de sus datos dentro del Perfil del cliente en tiempo real]. Estas solicitudes de exclusión forman parte de la Ley de privacidad del consumidor de California (CCPA), que otorga a los residentes de California el derecho de acceder y eliminar sus datos personales y de saber si sus datos personales se venden o revelan (y a quién). '
translation-type: tm+mt
source-git-commit: b3defc3e33a55855e307ab70b9797d985d5719e3
workflow-type: tm+mt
source-wordcount: '1031'
ht-degree: 0%

---


# Cumplimiento de las solicitudes de exclusión en segmentos

Adobe Experience Platform permite a sus clientes enviar solicitudes de exclusión con respecto al uso y el almacenamiento de sus datos dentro de [!DNL Real-time Customer Profile]. Estas solicitudes de exclusión forman parte del [!DNL California Consumer Privacy Act] (CCPA), que otorga a los residentes de California el derecho de acceder y eliminar sus datos personales y de saber si sus datos personales se venden o revelan (y a quién).

Una vez que un cliente ha optado por la exclusión, es importante que su organización respete dichas exclusiones al generar audiencias para actividades de marketing. Este documento describe detalles importantes sobre el cumplimiento de las solicitudes de exclusión.

## Primeros pasos

El cumplimiento de las solicitudes de exclusión requiere una comprensión de los distintos [!DNL Adobe Experience Platform] servicios involucrados. Antes de trabajar con solicitudes de exclusión, consulte la documentación de los siguientes servicios:

- [[!DNL Real-time Customer Profile]](../profile/home.md):: Proporciona un perfil de cliente unificado en tiempo real basado en datos agregados de varias fuentes.
- [[!DNL Adobe Experience Platform Segmentation Service]](./home.md):: Permite generar segmentos de audiencia a partir de  [!DNL Real-time Customer Profile] datos.
- [[!DNL Experience Data Model (XDM)]](../xdm/home.md):: El marco estandarizado por el cual Platform organiza los datos de experiencia del cliente.
- [[!DNL Adobe Experience Platform Privacy Service]](../privacy-service/home.md):: Ayuda a las organizaciones a automatizar el cumplimiento de las regulaciones de privacidad de datos que involucran datos de clientes dentro de  [!DNL Platform].

## Mezclas de exclusión

Para cumplir las solicitudes de exclusión de CCPA, uno de los esquemas que forma parte del esquema de unión debe contener los campos de exclusión necesarios [!DNL Experience Data Model] (XDM). Existen dos mezclas que se pueden utilizar para agregar campos de exclusión a un esquema; cada una de ellas se trata con más detalle en las secciones siguientes:

- [Privacidad](#profile-privacy) de perfil: Se utiliza para capturar diferentes tipos de exclusión (general o de ventas/uso compartido).
- [Detalles](#profile-preferences-details) de las preferencias de perfil: Se utiliza para capturar solicitudes de exclusión para canales XDM específicos.

Para obtener instrucciones detalladas sobre cómo añadir una mezcla a un esquema, consulte la sección &quot;Añadir una mezcla&quot; en la siguiente documentación de XDM:
- [Tutorial](../xdm/api/getting-started.md) de la API del Registro de esquemas.:: Creación de un esquema mediante la API del Registro de Esquema.
- [Tutorial](../xdm/tutorials/create-schema-ui.md) del Editor de esquemas: Creación de un esquema mediante la interfaz de usuario de la plataforma.

Esta es una imagen de ejemplo que muestra las mezclas de exclusión agregadas a un esquema en la interfaz de usuario:

![](images/opt-outs/opt-out-mixins-user-interface.png)

La estructura de cada mezcla, así como una descripción de los campos que contribuyen al esquema, se describen con más detalle en las siguientes secciones.

### [!DNL Profile Privacy] {#profile-privacy}

La combinación [!DNL Profile Privacy] le permite capturar dos tipos de solicitudes de exclusión de CCPA de los clientes:

1. Desactivación general
2. Opción de exclusión de ventas/uso compartido

![](images/opt-outs/profile-privacy.png)

La mezcla [!DNL Profile Privacy] contiene los siguientes campos:

- Opciones de exclusión de privacidad (`privacyOptOuts`): Matriz que contiene una lista de objetos de exclusión.
- Tipo de exclusión (`optOutType`): Tipo de exclusión. Este campo es una enumeración con dos valores posibles:
   - Desactivación general (`general_opt_out`)
   - Opción de exclusión para compartir ventas (`sales_sharing_opt_out`)
- Valor de exclusión (`optOutValue`): El estado activo de la exclusión, también conocido como el valor de la señal de exclusión, según el tipo de exclusión especificado. Este campo es una enumeración con cuatro valores posibles:
   - No proporcionado (`not_provided`): No se ha proporcionado una solicitud de exclusión.
   - Verificación pendiente (`pending`): La solicitud de exclusión está pendiente de verificación.
   - Opción de exclusión (`out`): El cliente ha optado por la exclusión.
   - Inclusión (`in`): El cliente ha elegido la opción de participar.
- Marca de tiempo de exclusión (`timestamp`): Marca de tiempo de la señal de exclusión recibida.

Para realizar la vista de la estructura completa de la mezcla [!DNL Profile Privacy], consulte el [repositorio público GitHub XDM](https://github.com/adobe/xdm/blob/master/schemas/context/profile-privacy.schema.json) o previsualización de la mezcla mediante la interfaz de usuario de la plataforma.

### [!DNL Profile Preferences Details] {#profile-preferences-details}

La combinación [!DNL Profile Preferences Details] proporciona varios campos que representan las preferencias de los perfiles del cliente (como formato del correo electrónico, idioma preferido y huso horario). Uno de los campos incluidos en esta mezcla, OptInOut (`optInOut`), permite establecer valores de exclusión para canales individuales.

![](images/opt-outs/profile-preferences-details.png)

La mezcla [!DNL Profile Preferences Details] contiene los siguientes campos relacionados con las exclusiones:

- OptInOut (`optInOut`): Objeto donde cada clave representa un URI válido y conocido para un canal de comunicaciones y el estado activo de la exclusión para cada canal. Cada canal puede tener uno de los cuatro valores posibles:
   - No proporcionado (`not_provided`): No se ha proporcionado una solicitud de exclusión para este canal.
   - Verificación pendiente (`pending`): La solicitud de exclusión para este canal está pendiente de verificación.
   - Opción de exclusión (`out`): El cliente ha excluido este canal.
   - Inclusión (`in`): El cliente ha elegido este canal.
- Opción de exclusión global (`globalOptout`): Un valor booleano que, cuando se define como true, establece una anulación de la exclusión global para el perfil. El valor predeterminado de este campo es false.

El ejemplo JSON siguiente resalta cómo el objeto OptInOut puede capturar varias señales de exclusión para diferentes canales de comunicación:

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

Para realizar la vista de la estructura completa de la combinación de Detalles de preferencias de Perfil, visite el [repositorio público de GitHub XDM](https://github.com/adobe/xdm/blob/master/schemas/context/profile-preferences-details.schema.json) o previsualización de la mezcla mediante la [!DNL Platform] IU.

## Gestión de las opciones de exclusión en la segmentación

Para garantizar que los perfiles marcados con indicadores de exclusión de CCPA no se incluyan en los segmentos, se deben agregar campos especiales a los segmentos existentes o incluir durante la creación de segmentos.

Las secciones siguientes muestran cómo agregar los campos correspondientes para los dos tipos de indicadores de exclusión:
1. Desactivación general
2. Opción de exclusión de ventas/uso compartido

### Desactivación general

[!DNL Segmentation] honra automáticamente todos los perfiles que contengan el indicador de &quot;exclusión [!UICONTROL general]&quot;, lo que significa que dichos perfiles no se incluirán en las audiencias o exportaciones de forma predeterminada. Sin embargo, se recomienda agregar los campos apropiados para asegurarse de que los perfiles de exclusión no se incluyen en las audiencias y actividades de marketing.

Esto se puede hacer mediante la interfaz de usuario agregando atributos **[!UICONTROL de exclusión de privacidad]**. En este caso, el segmento está configurado para incluir solamente a los que han adhesión (lo que significa que no tienen un indicador de exclusión general en su perfil). Esto se lleva a cabo declarando que el &quot;[!UICONTROL Tipo de exclusión]&quot; es igual a &quot;[!UICONTROL Exclusión general]&quot; y que el &quot;[!UICONTROL Valor de exclusión]&quot; es igual a &quot;[!UICONTROL Inclusión]&quot;.

![](images/opt-outs/segment-general-opt-out.png)

### Opción de exclusión de ventas/uso compartido

Si un usuario tiene un indicador de exclusión de venta/uso compartido establecido en su perfil, este perfil ya no debe usarse para ninguna actividad de marketing o creación de segmentos. Para asegurarse de que se cumple este indicador, el &quot;[!UICONTROL Tipo de exclusión]&quot; debe ser igual a &quot;[!UICONTROL Opción de exclusión de compartir ventas]&quot; y el &quot;[!UICONTROL Valor de exclusión]&quot; debe ser igual a &quot;[!UICONTROL Opción]&quot;.

![](images/opt-outs/segment-sales-sharing-opt-out.png)

<!-- ### Overriding default exclusions

In some instances, such as building a segment of people who have opted out, it may be necessary to override the default exclusion of opted-out profiles. This override can be done via the API or in the Segment Builder user interface. -->

## Pasos siguientes

Para obtener más información sobre la segmentación, incluido el trabajo con definiciones de segmentos y audiencias a través de la API y la interfaz de usuario, lea la [información general de segmentación](./home.md).

Para obtener más información sobre la privacidad de datos dentro de [!DNL Platform], incluso cómo [!DNL Privacy Service] ayuda a facilitar el cumplimiento automatizado de las regulaciones de privacidad legales y organizativas, consulte la documentación de [[!DNL Privacy Service]](../privacy-service/home.md).
