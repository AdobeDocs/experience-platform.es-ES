---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Configuración de un flujo de datos para un conector de flujo de almacenamiento en la nube en la interfaz de usuario
topic: overview
translation-type: tm+mt
source-git-commit: dca1accc16395de72db6d0cc8eac78f07dd05e03
workflow-type: tm+mt
source-wordcount: '690'
ht-degree: 0%

---


# Configuración de un flujo de datos para un conector de flujo de almacenamiento en la nube en la interfaz de usuario

Un flujo de datos es una tarea programada que recupera e ingiere datos de un origen a un conjunto de datos de la Plataforma. Este tutorial proporciona pasos para configurar un nuevo flujo de datos mediante el conector base del almacenamiento de nube.

## Primeros pasos

Este tutorial requiere un conocimiento práctico de los siguientes componentes de Adobe Experience Platform:

- [Sistema](../../../../../xdm/home.md)de modelo de datos de experiencia (XDM): Marco normalizado mediante el cual la plataforma de experiencias organiza los datos de experiencia del cliente.
   - [Conceptos básicos de la composición](../../../../../xdm/schema/composition.md)de esquemas: Obtenga información sobre los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   - [Tutorial](../../../../../xdm/tutorials/create-schema-ui.md)del Editor de Esquemas: Obtenga información sobre cómo crear esquemas personalizados mediante la interfaz de usuario del Editor de Esquemas.
- [Perfil](../../../../../profile/home.md)del cliente en tiempo real: Proporciona un perfil de consumo unificado y en tiempo real basado en datos agregados de varias fuentes.

Además, este tutorial requiere que ya haya creado un conector de almacenamiento de nube. Encontrará una lista de tutoriales para crear diferentes conectores de almacenamiento en la interfaz de usuario en la descripción general [de los conectores](../../../../home.md)de origen.

## Seleccionar datos

Después de crear el conector de almacenamiento de nube, aparece el paso *Seleccionar datos* , que proporciona una interfaz para seleccionar el flujo desde el que se transmitirán los datos.

![](../../../../images/tutorials/dataflow/cloud-storage/streaming/select-data.png)

## Asignación de campos de datos a un esquema XDM

Aparece el paso *Asignación* , que proporciona una interfaz interactiva para asignar los datos de origen a un conjunto de datos de la plataforma.

Elija un conjunto de datos para los datos de entrada en los que se van a ingerir. Puede usar un conjunto de datos existente o crear uno nuevo.

**Usar un conjunto de datos existente**

Para ingerir datos en un conjunto de datos existente, seleccione **Utilizar conjunto** de datos existente y, a continuación, haga clic en el icono de conjunto de datos.

![](../../../../images/tutorials/dataflow/cloud-storage/streaming/use-existing-data.png)

Aparece el cuadro de diálogo _Seleccionar conjunto de datos_ . Busque el conjunto de datos que desee utilizar, selecciónelo y haga clic en **Continuar**.

![](../../../../images/tutorials/dataflow/cloud-storage/streaming/select-existing-data.png)

**Usar un nuevo conjunto de datos**

Para ingestar datos en un nuevo conjunto de datos, seleccione **Crear nuevo conjunto** de datos e introduzca un nombre y una descripción para el conjunto de datos en los campos proporcionados. A continuación, seleccione el esquema que desee utilizar en la lista desplegable.

![](../../../../images/tutorials/dataflow/cloud-storage/streaming/use-new-dataset.png)

## Asigne un nombre al flujo de datos

Aparece el paso de detalles ** de flujo de datos, que le permite asignar un nombre y una breve descripción del nuevo flujo de datos.

Proporcione valores para el flujo de datos y haga clic en **Siguiente**.

![](../../../../images/tutorials/dataflow/cloud-storage/streaming/name-your-dataflow.png)

### Revise el flujo de datos

Aparece el paso *Revisar* , que le permite revisar el nuevo flujo de datos antes de crearlo. Los detalles se agrupan en las siguientes categorías:

- *Detalles* de la fuente: Muestra el tipo de origen y otros detalles relevantes sobre el origen.
- *Detalles* del Destinatario: Muestra en qué conjunto de datos se están ingeriendo los datos de origen, incluido el esquema al que se adhiere el conjunto de datos.

Una vez que haya revisado el flujo de datos, haga clic en **Finalizar** y permita que se cree el flujo de datos.

![](../../../../images/tutorials/dataflow/cloud-storage/streaming/review.png)

## Monitorear el flujo de datos

Una vez creado el flujo de datos del almacenamiento de nube, puede supervisar los datos que se están ingeriendo a través de él. Para obtener más información sobre la supervisión de conjuntos de datos, consulte el tutorial sobre la [supervisión de flujos de datos](../../../../../ingestion/quality/monitor-data-flows.md)de flujo continuo.

## Pasos siguientes

Siguiendo este tutorial, ha creado correctamente un flujo de datos para traer datos de un almacenamiento de nube externo y ha adquirido una perspectiva sobre la supervisión de conjuntos de datos. Los datos entrantes ahora se pueden utilizar en los servicios de plataforma descendente, como Perfil del cliente en tiempo real y Área de trabajo de ciencias de datos. Consulte los siguientes documentos para obtener más información:

- [Información general sobre el Perfil del cliente en tiempo real](../../../../../profile/home.md)
- [Información general sobre el área de trabajo de ciencias de datos](../../../../../data-science-workspace/home.md)

## Apéndice

Las secciones siguientes proporcionan información adicional para trabajar con conectores de origen.

### Deshabilitar un flujo de datos

Cuando se crea un flujo de datos, se activa inmediatamente y se ingieren datos según la programación que se le haya dado. Puede desactivar un flujo de datos activo en cualquier momento siguiendo las instrucciones que se indican a continuación.

En el espacio de trabajo *Fuentes* , haga clic en la ficha **Examinar** . A continuación, haga clic en el nombre de la conexión base asociada al flujo de datos activo que desea deshabilitar.

![](../../../../images/tutorials/dataflow/cloud-storage/streaming/browse.png)

Aparece la página actividad ** de origen. Seleccione el flujo de datos activo de la lista para abrir su columna *Propiedades* en el lado derecho de la pantalla, que contiene un botón de alternancia **Habilitado** . Haga clic en el botón de alternancia para deshabilitar el flujo de datos. Se puede utilizar la misma opción para volver a habilitar un flujo de datos después de desactivarlo.

![](../../../../images/tutorials/dataflow/cloud-storage/streaming/disable-source.png)

### Activar datos de entrada para población de Perfiles

Los datos entrantes del conector de origen se pueden utilizar para enriquecer y rellenar los datos de Perfil del cliente en tiempo real. Para obtener más información sobre cómo rellenar los datos de Perfil de clientes reales, consulte el tutorial sobre población [de](../../profile.md)Perfiles.
