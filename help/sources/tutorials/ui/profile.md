---
keywords: Experience Platform;inicio;temas populares;activar datos entrantes;rellenar perfil;rellenar rtcp;perfil unificado rellenado
solution: Experience Platform
title: Activar datos de origen entrantes para rellenar perfiles de cliente en la interfaz de usuario
type: Tutorial
description: Los datos de entrada del conector de origen se pueden utilizar para enriquecer y rellenar los datos del perfil del cliente en tiempo real.
exl-id: ddd3766a-3f55-4bbc-8358-c578eae2c629
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '507'
ht-degree: 0%

---

# Activar datos de origen entrantes para rellenar perfiles de cliente

Los datos de entrada del conector de origen se pueden utilizar para enriquecer y rellenar el [!DNL Real-Time Customer Profile] datos.

## Primeros pasos

Este tutorial requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

- [[!DNL Experience Data Model (XDM)] Sistema](../../../xdm/home.md): El marco normalizado por el cual [!DNL Experience Platform] organiza los datos de experiencia del cliente.
   - [Aspectos básicos de la composición del esquema](../../../xdm/schema/composition.md): Obtenga información sobre los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   - [Tutorial del Editor de esquemas](../../../xdm/tutorials/create-schema-ui.md): Obtenga información sobre cómo crear esquemas personalizados mediante la interfaz de usuario del Editor de esquemas.
- [[!DNL Real-Time Customer Profile]](../../../profile/home.md): Proporciona un perfil de cliente unificado y en tiempo real basado en datos agregados de varias fuentes.

Además, este tutorial requiere que ya haya creado y configurado un conector de origen.  Puede encontrar una lista de tutoriales para crear diferentes conectores en la interfaz de usuario en la [información general sobre conectores de origen](../../home.md).

## Rellene su [!DNL Real-Time Customer Profile] data

Para enriquecer los perfiles de cliente, el esquema de origen del conjunto de datos de destino debe ser compatible para su uso en [!DNL Real-Time Customer Profile]. Un esquema compatible cumple los siguientes requisitos:

- El esquema tiene al menos un atributo especificado como propiedad de identidad.
- El esquema tiene una propiedad de identidad definida como la identidad principal.
- Existe una asignación dentro del flujo de datos donde la identidad principal es un atributo de destino.

En el espacio de trabajo Fuentes, haga clic en el botón **[!UICONTROL Examinar]** para enumerar las conexiones base. En la lista mostrada, busque la conexión que contiene el flujo de datos con el que desea rellenar los perfiles. Haga clic en el nombre de la conexión para acceder a sus detalles.

![](../../images/tutorials/dataflow/cloud-storage/batch/browse.png)

La conexión es **[!UICONTROL Actividad de origen]** , mostrando los conjuntos de datos en los que la conexión está incorporando datos de origen. Haga clic en el nombre del conjunto de datos para el que desea habilitar [!DNL Profile].

![](../../images/tutorials/dataflow/cloud-storage/batch/dataset-dataflow.png)

La variable **[!UICONTROL Actividad del conjunto de datos]** se abre. La variable **[!UICONTROL Propiedades]** a la derecha de la pantalla muestra los detalles del conjunto de datos e incluye una **[!UICONTROL Perfil]** y un vínculo al esquema al que se adhiere el conjunto de datos. Haga clic en el nombre del esquema para ver su composición.

![](../../images/tutorials/dataflow/cloud-storage/batch/select-dataset-schema.png)

La variable **[!UICONTROL Editor de esquemas]** , mostrando la estructura del esquema en el lienzo central. Dentro del lienzo, seleccione el campo que desea establecer como identidad principal. En el **[!UICONTROL Propiedades del campo]** que aparece, seleccione **[!UICONTROL Identidad]** casilla de verificación, luego **[!UICONTROL Identidad primaria]**. Finalmente, seleccione una **[!UICONTROL Área de nombres de identidad]** y haga clic en **[!UICONTROL Aplicar]**.

![](../../images/tutorials/dataflow/cloud-storage/batch/set-schema-identity.png)

Haga clic en el objeto de nivel superior de la estructura del esquema y en el **[!UICONTROL Propiedades del esquema]** aparece. Habilitar el esquema para [!DNL Profile] activando el temporizador **[!UICONTROL Perfil]** . Haga clic en **[!UICONTROL Guardar]** para finalizar los cambios.

![](../../images/tutorials/dataflow/cloud-storage/batch/enable-profile.png)

Ahora que el esquema está habilitado para [!DNL Profile], vuelva a la **[!UICONTROL Actividad del conjunto de datos]** y habilite el conjunto de datos para [!DNL Profile] haciendo clic en el botón **[!UICONTROL Perfil]** alternar dentro de **[!UICONTROL Propiedades]** para abrir el Navegador.

![](../../images/tutorials/dataflow/cloud-storage/batch/enable-dataset-profile.png)

Con el esquema y el conjunto de datos habilitados para [!DNL Profile], los datos introducidos en ese conjunto de datos ahora también rellenarán los perfiles de los clientes.

>[!NOTE]
>
>Los datos existentes en un conjunto de datos habilitado recientemente no se consumen en [!DNL Profile].

## Pasos siguientes

Siguiendo este tutorial, ha activado correctamente los datos de entrada para [!DNL Profile] población. Para obtener más información, consulte la [[!DNL Real-Time Customer Profile] información general](../../../profile/home.md).
