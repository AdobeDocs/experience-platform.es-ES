---
keywords: Experience Platform;inicio;temas populares;activar datos de entrada;rellenar perfil;rellenar rtcp;perfil unificado rellenado
solution: Experience Platform
title: Activar datos de origen de entrada para rellenar Perfiles del cliente en la interfaz de usuario
topic: overview
type: Tutorial
description: Los datos de entrada del conector de origen se pueden utilizar para enriquecer y completar los datos de Perfil del cliente en tiempo real.
translation-type: tm+mt
source-git-commit: c7fb0d50761fa53c1fdf4dd70a63c62f2dcf6c85
workflow-type: tm+mt
source-wordcount: '507'
ht-degree: 0%

---


# Activar datos de origen de entrada para rellenar perfiles de cliente

Los datos entrantes del conector de origen se pueden utilizar para enriquecer y rellenar los datos [!DNL Real-time Customer Profile].

## Primeros pasos

Este tutorial requiere un conocimiento práctico de los siguientes componentes de Adobe Experience Platform:

- [[!DNL Experience Data Model (XDM)] Sistema](../../../xdm/home.md): Marco normalizado por el cual se  [!DNL Experience Platform] organizan los datos de experiencia del cliente.
   - [Conceptos básicos de la composición](../../../xdm/schema/composition.md) de esquemas: Obtenga información sobre los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   - [Tutorial](../../../xdm/tutorials/create-schema-ui.md) del Editor de esquemas: Obtenga información sobre cómo crear esquemas personalizados mediante la interfaz de usuario del Editor de Esquemas.
- [[!DNL Real-time Customer Profile]](../../../profile/home.md):: Proporciona un perfil de consumo unificado y en tiempo real basado en datos agregados de varias fuentes.

Además, este tutorial requiere que ya haya creado y configurado un conector de origen.  Encontrará una lista de tutoriales para crear diferentes conectores en la interfaz de usuario en la [información general de los conectores de origen](../../home.md).

## Rellene los datos [!DNL Real-time Customer Profile]

Para enriquecer los perfiles del cliente, el esquema de origen del conjunto de datos de destinatario debe ser compatible para su uso en [!DNL Real-time Customer Profile]. Un esquema compatible cumple los siguientes requisitos:

- El esquema tiene al menos un atributo especificado como propiedad de identidad.
- El esquema tiene una propiedad de identidad definida como la identidad principal.
- Existe una asignación dentro del flujo de datos donde la identidad principal es un atributo de destinatario.

Dentro del espacio de trabajo Fuentes, haga clic en la ficha **[!UICONTROL Examinar]** para lista de las conexiones base. En la lista mostrada, busque la conexión que contiene el flujo de datos con el que desea rellenar los perfiles. Haga clic en el nombre de la conexión para acceder a sus detalles.

![](../../images/tutorials/dataflow/cloud-storage/batch/browse.png)

Se abre la pantalla **[!UICONTROL actividad de origen]** de la conexión, que muestra los conjuntos de datos en los que la conexión está invirtiendo datos de origen. Haga clic en el nombre del conjunto de datos que desee habilitar para [!DNL Profile].

![](../../images/tutorials/dataflow/cloud-storage/batch/dataset-dataflow.png)

Se abre la pantalla **[!UICONTROL actividad del conjunto de datos]**. La columna **[!UICONTROL Propiedades]** del lado derecho de la pantalla muestra los detalles del conjunto de datos e incluye un conmutador **[!UICONTROL Perfil]** y un vínculo al esquema al que se adhiere el conjunto de datos. Haga clic en el nombre del esquema para vista de su composición.

![](../../images/tutorials/dataflow/cloud-storage/batch/select-dataset-schema.png)

Aparece el **[!UICONTROL Editor de Esquemas]**, que muestra la estructura del esquema en el lienzo central. Dentro del lienzo, seleccione el campo que se va a establecer como identidad principal. En la ficha **[!UICONTROL Propiedades del campo]** que aparece, seleccione la casilla **[!UICONTROL Identidad]** y, a continuación, **[!UICONTROL Identidad principal]**. Finalmente, seleccione una **[!UICONTROL Área de nombres de identidad]** apropiada y haga clic en **[!UICONTROL Aplicar]**.

![](../../images/tutorials/dataflow/cloud-storage/batch/set-schema-identity.png)

Haga clic en el objeto de nivel superior de la estructura del esquema y aparecerá la columna **[!UICONTROL propiedades del Esquema]**. Habilite el esquema para [!DNL Profile] alternando el conmutador **[!UICONTROL Perfil]**. Haga clic en **[!UICONTROL Guardar]** para finalizar los cambios.

![](../../images/tutorials/dataflow/cloud-storage/batch/enable-profile.png)

Ahora que el esquema está habilitado para [!DNL Profile], vuelva a la pantalla **[!UICONTROL actividad del conjunto de datos]** y habilite el conjunto de datos para [!DNL Profile] haciendo clic en la opción **[!UICONTROL Perfil]** de la columna **[!UICONTROL Propiedades]**.

![](../../images/tutorials/dataflow/cloud-storage/batch/enable-dataset-profile.png)

Con el esquema y el conjunto de datos habilitados para [!DNL Profile], los datos ingestados en ese conjunto de datos ahora también rellenarán los perfiles de los clientes.

>[!NOTE]
>
>[!DNL Profile] no consume los datos existentes dentro de un conjunto de datos recientemente habilitado.

## Pasos siguientes

Siguiendo este tutorial, ha activado correctamente los datos de entrada para la población [!DNL Profile]. Para obtener más información, consulte la [[!DNL Real-time Customer Profile] información general](../../../profile/home.md).