---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Activar datos de origen de entrada para rellenar perfiles de cliente
topic: overview
translation-type: tm+mt
source-git-commit: d6d2faf3d5eabcd8e948d3717fd8f8df4b9cb85a

---


# Activar datos de origen de entrada para rellenar perfiles de cliente

Los datos entrantes del conector de origen se pueden utilizar para enriquecer y rellenar los datos de Perfil del cliente en tiempo real.

## Primeros pasos

Este tutorial requiere un conocimiento práctico de los siguientes componentes de Adobe Experience Platform:

- [Sistema](../../../xdm/home.md)de modelo de datos de experiencia (XDM): Marco normalizado mediante el cual la plataforma de experiencias organiza los datos de experiencia del cliente.
   - [Conceptos básicos de la composición](../../../xdm/schema/composition.md)de esquemas: Obtenga información sobre los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   - [Tutorial](../../../xdm/tutorials/create-schema-ui.md)del Editor de Esquemas: Obtenga información sobre cómo crear esquemas personalizados mediante la interfaz de usuario del Editor de Esquemas.
- [Perfil](../../../profile/home.md)del cliente en tiempo real: Proporciona un perfil de consumo unificado y en tiempo real basado en datos agregados de varias fuentes.

Además, este tutorial requiere que ya haya creado y configurado un conector de origen.  Puede encontrar una lista de tutoriales para crear diferentes conectores en la interfaz de usuario en la descripción general [de los conectores](../../home.md)de origen.

## Rellene sus datos de Perfil de clientes en tiempo real

Para enriquecer los perfiles de los clientes, el esquema de origen del conjunto de datos de destinatario debe ser compatible para su uso en el Perfil del cliente en tiempo real. Un esquema compatible cumple los siguientes requisitos:

- El esquema tiene al menos un atributo especificado como propiedad de identidad.
- El esquema tiene una propiedad de identidad definida como la identidad principal.
- Existe una asignación dentro del flujo de datos donde la identidad principal es un atributo de destinatario.

En el espacio de trabajo Fuentes, haga clic en la ficha **Examinar** para realizar la lista de las conexiones base. En la lista mostrada, busque la conexión que contiene el flujo de datos con el que desea rellenar los perfiles. Haga clic en el nombre de la conexión para acceder a sus detalles.

![](../../images/tutorials/dataflow/cloud-storage/browse.png)

Se abre la pantalla actividad *de* origen de la conexión, que muestra los conjuntos de datos en los que la conexión está invirtiendo datos de origen. Haga clic en el nombre del conjunto de datos que desee habilitar para el Perfil.

![](../../images/tutorials/dataflow/cloud-storage/dataset-dataflow.png)

Aparece la pantalla *actividad* del conjunto de datos. La columna *Propiedades* del lado derecho de la pantalla muestra los detalles del conjunto de datos e incluye un conmutador de **Perfil** y un vínculo al esquema al que se adhiere el conjunto de datos. Haga clic en el nombre del esquema para vista de su composición.

![](../../images/tutorials/dataflow/cloud-storage/select-dataset-schema.png)

Aparece el Editor *de* Esquemas, que muestra la estructura del esquema en el lienzo central. Dentro del lienzo, seleccione el campo que se va a establecer como identidad principal. En la ficha Propiedades *del* campo que aparece, seleccione la casilla **Identidad** y, a continuación, la identidad **** principal. Finalmente, seleccione una Área de nombres **** de identidad adecuada y haga clic en **Aplicar**.

![](../../images/tutorials/dataflow/cloud-storage/set-schema-identity.png)

Haga clic en el objeto de nivel superior de la estructura del esquema y aparecerá la columna de propiedades *del* Esquema. Active el esquema para el Perfil alternando el conmutador de **Perfil** . Haga clic en **Guardar** para finalizar los cambios.

![](../../images/tutorials/dataflow/cloud-storage/enable-profile.png)

Ahora que el esquema está habilitado para el Perfil, vuelva a la pantalla de actividad *del* conjunto de datos y habilite el conjunto de datos para el Perfil haciendo clic en el botón de alternancia del **Perfil** en la columna *Propiedades* .

![](../../images/tutorials/dataflow/cloud-storage/enable-dataset-profile.png)

Con el esquema y el conjunto de datos habilitados para el Perfil, los datos ingestados en ese conjunto de datos ahora también rellenarán los perfiles de los clientes.

>[!NOTE] Perfil no consume los datos existentes dentro de un conjunto de datos recientemente habilitado

## Pasos siguientes

Siguiendo este tutorial, ha activado correctamente los datos de entrada para la población de Perfiles. Para obtener más información, consulte la descripción general [del Perfil del cliente en tiempo](../../../profile/home.md)real.