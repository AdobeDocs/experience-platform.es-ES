---
keywords: Experience Platform;inicio;temas populares;exclusión;Segmentación;Servicio de segmentación;servicio de segmentación;servicio de segmentación;aceptar exclusiones;exclusiones;exclusión;exclusión;exclusiones;consentimiento;compartir;recopilar;
solution: Experience Platform
title: Respeto del consentimiento en los segmentos
description: Aprenda a cumplir las preferencias de consentimiento del cliente para la recopilación de datos personales y el uso compartido en operaciones de segmentos.
exl-id: fe851ce3-60db-4984-a73c-f9c5964bfbad
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '675'
ht-degree: 0%

---

# Respeto del consentimiento en los segmentos

Regulaciones legales de privacidad, como la [!DNL California Consumer Privacy Act] (CCPA) otorga a los consumidores el derecho de optar por no recopilar o compartir sus datos personales con terceros. Adobe Experience Platform proporciona componentes de modelo de datos de experiencia (XDM) estándar destinados a capturar estas preferencias de consentimiento del cliente en datos de perfil del cliente en tiempo real.

Si un cliente ha retirado o retenido el consentimiento para que se compartan sus datos personales, es importante que su organización respete esa preferencia al generar audiencias para actividades de marketing. En este documento se describe cómo integrar los valores de consentimiento del cliente en las definiciones de segmentos mediante la interfaz de usuario de Experience Platform.

## Primeros pasos

El cumplimiento de los valores de consentimiento del cliente requiere una comprensión de los distintos [!DNL Adobe Experience Platform] servicios implicados. Antes de iniciar este tutorial, asegúrese de estar familiarizado con los siguientes servicios:

* [[!DNL Experience Data Model (XDM)]](../xdm/home.md): el marco estandarizado mediante el cual Platform organiza los datos de experiencia del cliente.
* [[!DNL Real-Time Customer Profile]](../profile/home.md): Proporciona un perfil de cliente unificado en tiempo real en función de los datos agregados de varias fuentes.
* [[!DNL Adobe Experience Platform Segmentation Service]](./home.md): le permite generar segmentos de audiencia a partir de [!DNL Real-Time Customer Profile] datos.

## Campos del esquema de consentimiento

Para cumplir con los consentimientos y preferencias del cliente, uno de los esquemas que forma parte de su [!UICONTROL Perfil individual de XDM] el esquema de unión debe contener el grupo de campos estándar **[!UICONTROL Consentimientos y preferencias]**.

Para obtener más información sobre la estructura y el caso de uso previsto de cada uno de los atributos proporcionados por el grupo de campos, consulte el [guía de referencia de preferencias y consentimientos](../xdm/field-groups/profile/consents.md). Para obtener instrucciones paso a paso sobre cómo añadir un grupo de campos a un esquema, consulte la [Guía de IU de XDM](../xdm/ui/resources/schemas.md#add-field-groups).

Una vez agregado el grupo de campos a una [Esquema con perfil habilitado](../xdm/ui/resources/schemas.md#profile) y sus campos se han utilizado para introducir datos de consentimiento de su aplicación de experiencia, puede utilizar los atributos de consentimiento recopilados en las reglas de segmento.

## Gestión del consentimiento en la segmentación

Para garantizar que los perfiles de exclusión no se incluyan en los segmentos, se deben añadir campos especiales a los segmentos existentes e incluirlos al crear cualquier segmento nuevo.

Los pasos siguientes muestran cómo agregar los campos adecuados para dos tipos de indicadores de exclusión:

1. [!UICONTROL Recopilación de datos]
1. [!UICONTROL Compartir datos]

>[!NOTE]
>
>Aunque esta guía se centra en los dos indicadores de exclusión anteriores, también puede configurar sus segmentos para incorporar señales de consentimiento adicionales. El [guía de referencia de preferencias y consentimientos](../xdm/field-groups/profile/consents.md) proporciona más información sobre cada una de estas opciones y sus casos de uso previstos.

Al crear un segmento en la interfaz de usuario de, en **[!UICONTROL Atributos]**, vaya a **[!UICONTROL Perfil individual de XDM]**, luego seleccione **[!UICONTROL Consentimientos y preferencias]**. Desde aquí puede ver las opciones de **[!UICONTROL Recopilación de datos]** y **[!UICONTROL Compartir datos]**.

![](./images/opt-outs/consents.png)

Comience por seleccionar la **[!UICONTROL Recopilación de datos]** categoría y, a continuación, arrastre **[!UICONTROL Valor de opción]** en el generador de segmentos. Al agregar el atributo al segmento, puede especificar el [valores de consentimiento](../xdm/field-groups/profile/consents.md#choice-values) que deben incluirse o excluirse.

![](./images/opt-outs/consent-values.png)

Un método consiste en excluir a los clientes que hayan optado por no recopilar sus datos. Para ello, establezca el operador en **[!UICONTROL no es igual a]** y elija los siguientes valores:

* **[!UICONTROL No (exclusión)]**
* **[!UICONTROL Valor predeterminado de No (exclusión)]**
* **[!UICONTROL Desconocido]** (si se supone que el consentimiento se retiene si no se conoce)

![](./images/opt-outs/collect.png)

En **[!UICONTROL Atributos]** en el carril izquierdo, vuelva a la **[!UICONTROL Consentimientos y preferencias]** , luego seleccione **[!UICONTROL Compartir datos]**. Arrastre su correspondiente **[!UICONTROL Valor de opción]** en el lienzo y seleccione los mismos valores que para la variable [!UICONTROL Recopilación de datos] valor de opción. Asegúrese de que una **[!UICONTROL O]** Se establece una relación entre los dos atributos.

![](./images/opt-outs/share.png)

Con ambos **[!UICONTROL Recopilación de datos]** y **[!UICONTROL Compartir datos]** Si se añaden valores de consentimiento al segmento, los clientes que hayan optado por no utilizar sus datos se excluirán de la audiencia resultante. Desde aquí puede seguir personalizando la definición del segmento antes de seleccionar **[!UICONTROL Guardar]** para finalizar el proceso.

## Pasos siguientes

Al seguir este tutorial, debería comprender mejor cómo cumplir los consentimientos y preferencias de los clientes al crear segmentos en Experience Platform.

Para obtener más información sobre la administración del consentimiento en Platform, consulte la siguiente documentación:

* [Procesamiento de consentimiento mediante el estándar de Adobe](../landing/governance-privacy-security/consent/adobe/overview.md)
* [Procesamiento de consentimiento mediante el estándar IAB TCF 2.0](../landing/governance-privacy-security/consent/iab/overview.md)