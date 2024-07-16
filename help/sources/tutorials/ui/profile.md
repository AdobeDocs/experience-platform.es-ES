---
keywords: Experience Platform;inicio;temas populares;activar datos de entrada;rellenar perfil;rellenar rtcp;perfil unificado rellenado
solution: Experience Platform
title: Activar datos de Source entrantes para rellenar perfiles de cliente en la interfaz de usuario
type: Tutorial
description: Los datos entrantes del conector de origen se pueden utilizar para enriquecer y rellenar los datos del perfil del cliente en tiempo real.
exl-id: ddd3766a-3f55-4bbc-8358-c578eae2c629
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '507'
ht-degree: 0%

---

# Activar datos de origen entrantes para rellenar perfiles de clientes

Los datos de entrada del conector de origen se pueden usar para enriquecer y rellenar los datos de [!DNL Real-Time Customer Profile].

## Introducción

Este tutorial requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

- [[!DNL Experience Data Model (XDM)] Sistema](../../../xdm/home.md): El marco de trabajo estandarizado mediante el cual [!DNL Experience Platform] organiza los datos de la experiencia del cliente.
   - [Aspectos básicos de la composición de esquemas](../../../xdm/schema/composition.md): obtenga información sobre los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   - [Tutorial del editor de esquemas](../../../xdm/tutorials/create-schema-ui.md): Aprenda a crear esquemas personalizados mediante la interfaz de usuario del editor de esquemas.
- [[!DNL Real-Time Customer Profile]](../../../profile/home.md): proporciona un perfil de consumidor unificado y en tiempo real basado en los datos agregados de varias fuentes.

Además, este tutorial requiere que ya haya creado y configurado un conector de origen.  Encontrará una lista de tutoriales para crear diferentes conectores en la interfaz de usuario en [descripción general de los conectores de origen](../../home.md).

## Rellene los datos de [!DNL Real-Time Customer Profile]

Para enriquecer los perfiles de los clientes, el esquema de origen del conjunto de datos de destino debe ser compatible para su uso en [!DNL Real-Time Customer Profile]. Un esquema compatible cumple los siguientes requisitos:

- El esquema tiene al menos un atributo especificado como propiedad de identidad.
- El esquema tiene una propiedad de identidad definida como la identidad principal.
- Existe una asignación dentro del flujo de datos en la que la identidad principal es un atributo de destino.

En el área de trabajo Fuentes, haga clic en la ficha **[!UICONTROL Examinar]** para ver una lista de las conexiones base. En la lista mostrada, busque la conexión que contiene el flujo de datos con el que desea rellenar los perfiles. Haga clic en el nombre de la conexión para acceder a sus detalles.

![](../../images/tutorials/dataflow/cloud-storage/batch/browse.png)

Aparece la pantalla **[!UICONTROL actividad Source]** de la conexión, que muestra los conjuntos de datos en los que la conexión está ingiriendo datos de origen. Haga clic en el nombre del conjunto de datos que desea habilitar para [!DNL Profile].

![](../../images/tutorials/dataflow/cloud-storage/batch/dataset-dataflow.png)

Aparece la pantalla **[!UICONTROL Actividad del conjunto de datos]**. La columna **[!UICONTROL Propiedades]** en el lado derecho de la pantalla muestra los detalles del conjunto de datos e incluye un modificador **[!UICONTROL Perfil]** y un vínculo al esquema al que se adhiere el conjunto de datos. Haga clic en el nombre del esquema para ver su composición.

![](../../images/tutorials/dataflow/cloud-storage/batch/select-dataset-schema.png)

Aparece **[!UICONTROL Editor de esquemas]**, que muestra la estructura del esquema en el lienzo central. Dentro del lienzo, seleccione el campo que se va a establecer como identidad principal. En la ficha **[!UICONTROL Propiedades del campo]** que aparece, active la casilla de verificación **[!UICONTROL Identidad]** y, a continuación, **[!UICONTROL Identidad principal]**. Finalmente, seleccione un **[!UICONTROL área de nombres de identidad]** apropiado y luego haga clic en **[!UICONTROL Aplicar]**.

![](../../images/tutorials/dataflow/cloud-storage/batch/set-schema-identity.png)

Haga clic en el objeto de nivel superior de la estructura del esquema y aparecerá la columna **[!UICONTROL Propiedades del esquema]**. Habilite el esquema para [!DNL Profile] alternando el modificador **[!UICONTROL Profile]**. Haga clic en **[!UICONTROL Guardar]** para finalizar los cambios.

![](../../images/tutorials/dataflow/cloud-storage/batch/enable-profile.png)

Ahora que el esquema está habilitado para [!DNL Profile], vuelva a la pantalla **[!UICONTROL Actividad del conjunto de datos]** y habilite el conjunto de datos para [!DNL Profile] haciendo clic en el botón de alternancia **[!UICONTROL Perfil]** dentro de la columna **[!UICONTROL Propiedades]**.

![](../../images/tutorials/dataflow/cloud-storage/batch/enable-dataset-profile.png)

Con el esquema y el conjunto de datos habilitados para [!DNL Profile], los datos ingeridos en ese conjunto de datos ahora también rellenarán perfiles de clientes.

>[!NOTE]
>
>[!DNL Profile] no consume los datos existentes dentro de un conjunto de datos habilitado recientemente.

## Pasos siguientes

Al seguir este tutorial, ha activado correctamente los datos de entrada para la población [!DNL Profile]. Para obtener más información, consulte [[!DNL Real-Time Customer Profile] descripción general](../../../profile/home.md).
