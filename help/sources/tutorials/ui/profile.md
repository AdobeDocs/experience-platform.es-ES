---
keywords: Experience Platform;inicio;temas populares;activar datos entrantes;rellenar perfil;rellenar rtcp;perfil unificado rellenado
solution: Experience Platform
title: Activar datos de origen entrantes para rellenar perfiles de cliente en la interfaz de usuario
topic-legacy: overview
type: Tutorial
description: Los datos de entrada del conector de origen se pueden utilizar para enriquecer y rellenar los datos del perfil del cliente en tiempo real.
exl-id: ddd3766a-3f55-4bbc-8358-c578eae2c629
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '482'
ht-degree: 0%

---

# Activar datos de origen entrantes para rellenar perfiles de cliente

Los datos de entrada del conector de origen se pueden utilizar para enriquecer y rellenar los datos [!DNL Real-time Customer Profile].

## Primeros pasos

Este tutorial requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

- [[!DNL Experience Data Model (XDM)] Sistema](../../../xdm/home.md): El marco estandarizado mediante el cual se  [!DNL Experience Platform] organizan los datos de experiencia del cliente.
   - [Aspectos básicos de la composición](../../../xdm/schema/composition.md) del esquema: Obtenga información sobre los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   - [Tutorial del Editor de esquemas](../../../xdm/tutorials/create-schema-ui.md): Aprenda a crear esquemas personalizados mediante la interfaz de usuario del Editor de esquemas.
- [[!DNL Real-time Customer Profile]](../../../profile/home.md): Proporciona un perfil de cliente unificado y en tiempo real basado en datos agregados de varias fuentes.

Además, este tutorial requiere que ya haya creado y configurado un conector de origen.  Puede encontrar una lista de tutoriales para crear diferentes conectores en la interfaz de usuario en la [descripción general de los conectores de origen](../../home.md).

## Rellene los datos [!DNL Real-time Customer Profile]

Para enriquecer los perfiles del cliente, el esquema de origen del conjunto de datos de destino debe ser compatible para su uso en [!DNL Real-time Customer Profile]. Un esquema compatible cumple los siguientes requisitos:

- El esquema tiene al menos un atributo especificado como propiedad de identidad.
- El esquema tiene una propiedad de identidad definida como la identidad principal.
- Existe una asignación dentro del flujo de datos donde la identidad principal es un atributo de destino.

Dentro del espacio de trabajo de Fuentes, haga clic en la pestaña **[!UICONTROL Browse]** para enumerar las conexiones base. En la lista mostrada, busque la conexión que contiene el flujo de datos con el que desea rellenar los perfiles. Haga clic en el nombre de la conexión para acceder a sus detalles.

![](../../images/tutorials/dataflow/cloud-storage/batch/browse.png)

Aparece la pantalla **[!UICONTROL Source activity]** de la conexión, que muestra los conjuntos de datos en los que la conexión está incorporando datos de origen. Haga clic en el nombre del conjunto de datos que desea habilitar para [!DNL Profile].

![](../../images/tutorials/dataflow/cloud-storage/batch/dataset-dataflow.png)

Aparece la pantalla **[!UICONTROL Dataset activity]**. La columna **[!UICONTROL Properties]** en el lado derecho de la pantalla muestra los detalles del conjunto de datos e incluye un conmutador **[!UICONTROL Profile]** y un vínculo al esquema al que se adhiere el conjunto de datos. Haga clic en el nombre del esquema para ver su composición.

![](../../images/tutorials/dataflow/cloud-storage/batch/select-dataset-schema.png)

Aparece el **[!UICONTROL Schema Editor]**, que muestra la estructura del esquema en el lienzo central. Dentro del lienzo, seleccione el campo que desea establecer como identidad principal. En la pestaña **[!UICONTROL Field properties]** que aparece, seleccione la casilla **[!UICONTROL Identity]** y luego **[!UICONTROL Primary identity]**. Finalmente, seleccione un **[!UICONTROL Identity namespace]** apropiado y haga clic en **[!UICONTROL Apply]**.

![](../../images/tutorials/dataflow/cloud-storage/batch/set-schema-identity.png)

Haga clic en el objeto de nivel superior de la estructura del esquema y aparecerá la columna **[!UICONTROL Schema properties]**. Active el esquema para [!DNL Profile] alternando el conmutador **[!UICONTROL Profile]**. Haga clic en **[!UICONTROL Save]** para finalizar los cambios.

![](../../images/tutorials/dataflow/cloud-storage/batch/enable-profile.png)

Ahora que el esquema está habilitado para [!DNL Profile], vuelva a la pantalla **[!UICONTROL Dataset activity]** y habilite el conjunto de datos para [!DNL Profile] haciendo clic en el botón **[!UICONTROL Profile]** dentro de la columna **[!UICONTROL Properties]** .

![](../../images/tutorials/dataflow/cloud-storage/batch/enable-dataset-profile.png)

Con el esquema y el conjunto de datos habilitados para [!DNL Profile], los datos incorporados en ese conjunto de datos ahora también rellenarán los perfiles del cliente.

>[!NOTE]
>
>[!DNL Profile] no consume los datos existentes en un conjunto de datos habilitado recientemente.

## Pasos siguientes

Siguiendo este tutorial, ha activado correctamente los datos de entrada para la población [!DNL Profile] . Para obtener más información, consulte [[!DNL Real-time Customer Profile] descripción general](../../../profile/home.md).
