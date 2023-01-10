---
keywords: Experience Platform;inicio;temas populares;exclusión;segmentación;servicio de segmentación;servicio de segmentación;honores de exclusión;exclusión;exclusión;exclusión;exclusión;consentimiento;compartir;recopilar;
solution: Experience Platform
title: Respeto del consentimiento en los segmentos
description: Obtenga información sobre cómo cumplir las preferencias de consentimiento del cliente para la recopilación y el uso compartido de datos personales en operaciones de segmentos.
exl-id: fe851ce3-60db-4984-a73c-f9c5964bfbad
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '675'
ht-degree: 0%

---

# Respeto del consentimiento en los segmentos

Las regulaciones legales de privacidad, como la [!DNL California Consumer Privacy Act] (CCPA) otorga a los consumidores el derecho a no participar en la recopilación o el intercambio de sus datos personales con terceros. Adobe Experience Platform proporciona componentes estándar del Modelo de datos de experiencia (XDM) destinados a capturar estas preferencias de consentimiento del cliente en datos del Perfil del cliente en tiempo real.

Si un cliente ha retirado o retenido el consentimiento para compartir sus datos personales, es importante que su organización respete esa preferencia al generar audiencias para actividades de marketing. Este documento describe cómo integrar los valores de consentimiento del cliente en las definiciones de segmentos mediante la interfaz de usuario del Experience Platform.

## Primeros pasos

El respeto de los valores de consentimiento del cliente requiere una comprensión de las distintas [!DNL Adobe Experience Platform] servicios implicados. Antes de iniciar este tutorial, asegúrese de que está familiarizado con los siguientes servicios:

* [[!DNL Experience Data Model (XDM)]](../xdm/home.md): El marco estandarizado mediante el cual Platform organiza los datos de experiencia del cliente.
* [[!DNL Real-Time Customer Profile]](../profile/home.md): Proporciona un perfil de cliente unificado en tiempo real basado en datos agregados de varias fuentes.
* [[!DNL Adobe Experience Platform Segmentation Service]](./home.md): Permite crear segmentos de audiencia a partir de [!DNL Real-Time Customer Profile] datos.

## Campos de esquema de consentimiento

Para cumplir con los consentimientos y las preferencias del cliente, uno de los esquemas que forma parte de su [!UICONTROL Perfil individual XDM] el esquema de unión debe contener el grupo de campos estándar **[!UICONTROL Consentimientos y preferencias]**.

Para obtener más información sobre la estructura y el caso de uso previsto de cada uno de los atributos proporcionados por el grupo de campos, consulte [guía de referencia de consentimientos y preferencias](../xdm/field-groups/profile/consents.md). Para obtener instrucciones paso a paso sobre cómo añadir un grupo de campos a un esquema, consulte la [Guía de interfaz de usuario de XDM](../xdm/ui/resources/schemas.md#add-field-groups).

Una vez agregado el grupo de campos a una [Esquema habilitado para perfiles](../xdm/ui/resources/schemas.md#profile) y sus campos se han utilizado para introducir datos de consentimiento de la aplicación de experiencia, puede utilizar los atributos de consentimiento recopilados en las reglas de segmentos.

## Gestión del consentimiento en la segmentación

Para garantizar que los perfiles no seleccionados no se incluyan en los segmentos, se deben agregar campos especiales a los segmentos existentes e incluirlos al crear cualquier segmento nuevo.

Los pasos siguientes muestran cómo añadir los campos adecuados para dos tipos de indicadores de exclusión:

1. [!UICONTROL Recopilación de datos]
1. [!UICONTROL Compartir datos]

>[!NOTE]
>
>Aunque esta guía se centra en los dos indicadores de exclusión anteriores, puede configurar sus segmentos para incorporar también señales de consentimiento adicionales. La variable [guía de referencia de consentimientos y preferencias](../xdm/field-groups/profile/consents.md) proporciona más información sobre cada una de estas opciones y sus casos de uso deseados.

Al crear un segmento en la interfaz de usuario, en **[!UICONTROL Atributos]**, vaya a **[!UICONTROL Perfil individual XDM]** y, a continuación, seleccione **[!UICONTROL Consentimientos y preferencias]**. Desde aquí puede ver las opciones de **[!UICONTROL Recopilación de datos]** y **[!UICONTROL Compartir datos]**.

![](./images/opt-outs/consents.png)

Comience por seleccionar la **[!UICONTROL Recopilación de datos]** categoría y, a continuación, arrastre **[!UICONTROL Valor de opción]** en el generador de segmentos. Al agregar el atributo al segmento, puede especificar la variable [valores de consentimiento](../xdm/field-groups/profile/consents.md#choice-values) que deben incluirse o excluirse.

![](./images/opt-outs/consent-values.png)

Un enfoque es excluir a los clientes que hayan optado por no tener que recopilar sus datos. Para ello, establezca el operador en **[!UICONTROL no es igual a]** y elija los siguientes valores:

* **[!UICONTROL No (exclusión)]**
* **[!UICONTROL Valor predeterminado de no (exclusión)]**
* **[!UICONTROL Unknown]** (si se supone que se retiene el consentimiento si no se conoce)

![](./images/opt-outs/collect.png)

En **[!UICONTROL Atributos]** en el carril izquierdo, vuelva al **[!UICONTROL Consentimientos y preferencias]** y, a continuación, seleccione **[!UICONTROL Compartir datos]**. Arrastre su correspondiente **[!UICONTROL Valor de opción]** en el lienzo y seleccione los mismos valores que para la variable [!UICONTROL Recopilación de datos] valor de opción. Asegúrese de que **[!UICONTROL O]** se establece entre los dos atributos.

![](./images/opt-outs/share.png)

Con ambas **[!UICONTROL Recopilación de datos]** y **[!UICONTROL Compartir datos]** valores de consentimiento agregados al segmento, cualquier cliente que haya excluido la utilización de sus datos se excluirá de la audiencia resultante. Desde aquí, puede seguir personalizando la definición del segmento antes de seleccionar **[!UICONTROL Guardar]** para finalizar el proceso.

## Pasos siguientes

Al seguir este tutorial, ahora debe comprender mejor cómo cumplir con los consentimientos y las preferencias del cliente al crear segmentos en Experience Platform.

Para obtener más información sobre la administración del consentimiento en Platform, consulte la siguiente documentación:

* [Procesamiento de consentimiento con el estándar de Adobe](../landing/governance-privacy-security/consent/adobe/overview.md)
* [Procesamiento de consentimiento con el estándar IAB TCF 2.0](../landing/governance-privacy-security/consent/iab/overview.md)