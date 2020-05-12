---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Configurar un flujo de datos para un conector de base de datos en la interfaz de usuario
topic: overview
translation-type: tm+mt
source-git-commit: 415b59fc3fa20c09372549e92571c1b41006e540
workflow-type: tm+mt
source-wordcount: '1049'
ht-degree: 0%

---


# Configurar un flujo de datos para un conector de base de datos en la interfaz de usuario

Un flujo de datos es una tarea programada que recupera e ingiere datos de un origen a un conjunto de datos de la Plataforma. Este tutorial proporciona pasos para configurar un nuevo flujo de datos mediante el conector base de la base de datos.

## Primeros pasos

Este tutorial requiere un conocimiento práctico de los siguientes componentes de Adobe Experience Platform:

- [Sistema](../../../../xdm/home.md)de modelo de datos de experiencia (XDM): Marco normalizado mediante el cual la plataforma de experiencias organiza los datos de experiencia del cliente.
   - [Conceptos básicos de la composición](../../../../xdm/schema/composition.md)de esquemas: Obtenga información sobre los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   - [Tutorial](../../../../xdm/tutorials/create-schema-ui.md)del Editor de Esquemas: Obtenga información sobre cómo crear esquemas personalizados mediante la interfaz de usuario del Editor de Esquemas.
- [Perfil](../../../../profile/home.md)del cliente en tiempo real: Proporciona un perfil de consumo unificado y en tiempo real basado en datos agregados de varias fuentes.

Además, este tutorial requiere que ya haya creado un conector de base de datos. Puede encontrar una lista de tutoriales para crear diferentes conectores de base de datos en la interfaz de usuario en la descripción general [de los conectores](../../../home.md)de origen.

## Seleccionar datos

Después de crear el conector de la base de datos, aparece el paso *[!UICONTROL Seleccionar datos]* , que proporciona una interfaz interactiva para explorar la jerarquía de la base de datos.

- La mitad izquierda de la interfaz es un explorador que muestra la lista de las bases de datos de su cuenta.
- La mitad derecha de la interfaz permite la previsualización de hasta 100 filas de datos.

Seleccione la base de datos que desee utilizar y haga clic en **[!UICONTROL Siguiente]**.

![](../../../images/tutorials/dataflow/databases/add-data.png)

## Asignación de campos de datos a un esquema XDM

Aparece el paso *Asignación* , que proporciona una interfaz interactiva para asignar los datos de origen a un conjunto de datos de la plataforma.

Elija un conjunto de datos para los datos de entrada en los que se van a ingerir. Puede utilizar un conjunto de datos existente o crear un nuevo conjunto de datos.

### Usar un conjunto de datos existente

Para ingerir datos en un conjunto de datos existente, seleccione Conjunto de datos **[!UICONTROL existente]** y, a continuación, haga clic en el icono de conjunto de datos.

![](../../../images/tutorials/dataflow/databases/existing-dataset.png)

Aparece el cuadro de diálogo *[!UICONTROL Seleccionar conjunto de datos]* . Busque el conjunto de datos que desee utilizar, selecciónelo y haga clic en **[!UICONTROL Continuar]**.

![](../../../images/tutorials/dataflow/databases/select-existing-dataset.png)

### Usar un nuevo conjunto de datos

Para ingestar datos en un nuevo conjunto de datos, seleccione **[!UICONTROL Nuevo conjunto]** de datos e introduzca un nombre y una descripción para el conjunto de datos en los campos proporcionados.

Puede adjuntar un campo de esquema escribiendo un nombre de esquema en la barra de búsqueda **[!UICONTROL Seleccionar esquema]** . También puede seleccionar el icono desplegable para ver una lista de esquemas existentes. También puede seleccionar la búsqueda **** avanzada en una pantalla de esquemas existentes, incluidos sus respectivos detalles.

![](../../../images/tutorials/dataflow/databases/new-dataset.png)

Aparece el cuadro de diálogo *[!UICONTROL Seleccionar esquema] . Seleccione el esquema que desee aplicar al nuevo conjunto de datos y haga clic en **[!UICONTROL Finalizado]**.

![](../../../images/tutorials/dataflow/databases/select-existing-schema.png)

En función de sus necesidades, puede elegir asignar los campos directamente o utilizar funciones de asignador para transformar los datos de origen para derivar valores calculados o calculados. Para obtener más información sobre la asignación de datos y las funciones del asignador, consulte el tutorial sobre la [asignación de datos CSV a campos](../../../../ingestion/tutorials/map-a-csv-file.md)de esquema XDM.

Una vez asignados los datos de origen, haga clic en **[!UICONTROL Siguiente]**.

![](../../../images/tutorials/dataflow/databases/mapping.png)

## Programar ejecuciones de ingestión

Aparece el paso *[!UICONTROL Programación]* , que le permite configurar una programación de ingestión para ingestar automáticamente los datos de origen seleccionados mediante las asignaciones configuradas. La siguiente tabla describe los diferentes campos configurables para la programación:

| Campo | Descripción |
| --- | --- |
| Frecuencia | Las frecuencias seleccionables incluyen Minuto, Hora, Día y Semana. |
| Intervalo | Un entero que establece el intervalo para la frecuencia seleccionada. |
| Tiempo de Inicio | Marca de hora UTC para la que se producirá la primera ingestión. |
| Rellenar | Un valor booleano que determina qué datos se ingieren inicialmente. Si *Rellenar* está activado, todos los archivos actuales de la ruta especificada se ingerirán durante la primera ingestión programada. Si *Rellenar* está desactivado, solo se ingerirán los archivos que se carguen entre la primera ejecución de la ingesta y el tiempo *de* Inicio. Los archivos cargados antes de la hora *de* Inicio no se ingieren. |
| Columna delta | Una opción con un conjunto filtrado de campos de esquema de origen de tipo, fecha u hora. Este campo se utiliza para diferenciar entre datos nuevos y existentes. Los datos incrementales se ingieren según la marca de tiempo de la columna seleccionada. |

Los flujos de datos están diseñados para transferir datos automáticamente en forma programada. Si solo desea realizar una ingesta una vez a través de este flujo de trabajo, puede hacerlo configurando la **[!UICONTROL Frecuencia]** en &quot;Día&quot; y aplicando un número muy grande para el **[!UICONTROL intervalo]**, como 10000 o similar.

Proporcione valores para la programación y seleccione **[!UICONTROL Siguiente]**.

![](../../../images/tutorials/dataflow/databases/schedule.png)

## Asigne un nombre al flujo de datos

Aparece el paso de detalle *[!UICONTROL de flujo de]* datos, donde debe proporcionar un nombre y una descripción opcional para el flujo de datos. Seleccione **[!UICONTROL Siguiente]** cuando termine.

![](../../../images/tutorials/dataflow/databases/dataflow-detail.png)

## Revise el flujo de datos

Aparece el paso *[!UICONTROL Revisar]* , que le permite revisar el nuevo flujo de datos antes de crearlo. Los detalles se agrupan en las siguientes categorías:

- *Conexión*: Muestra el tipo de origen, la ruta de acceso relevante del archivo de origen seleccionado y la cantidad de columnas dentro de ese archivo de origen.
- *Asignar campos* de conjunto de datos y mapa: Muestra en qué conjunto de datos se están ingeriendo los datos de origen, incluido el esquema al que se adhiere el conjunto de datos.
- *Programación*: Muestra el período activo, la frecuencia y el intervalo del programa de ingestión.

Una vez que haya revisado el flujo de datos, haga clic en **[!UICONTROL Finalizar]** y permita que se cree el flujo de datos.

![](../../../images/tutorials/dataflow/databases/review.png)

## Monitorear el flujo de datos

Una vez creado el flujo de datos, puede monitorear los datos que se están ingeriendo a través de él. Para obtener más información sobre cómo supervisar los flujos de datos, consulte el tutorial sobre [cuentas y flujos de datos](../monitor.md).

## Pasos siguientes

Siguiendo este tutorial, se ha creado correctamente un flujo de datos para incorporar datos de una base de datos externa y obtener información sobre la supervisión de conjuntos de datos. Los datos entrantes ahora se pueden utilizar en los servicios de plataforma descendente, como Perfil del cliente en tiempo real y Área de trabajo de ciencias de datos. Consulte los siguientes documentos para obtener más información:

- [Información general sobre el Perfil del cliente en tiempo real](../../../../profile/home.md)
- [Información general sobre el área de trabajo de ciencias de datos](../../../../data-science-workspace/home.md)

## Apéndice

Las secciones siguientes proporcionan información adicional para trabajar con conectores de origen.

### Deshabilitar un flujo de datos

Cuando se crea un flujo de datos, se activa inmediatamente y se ingieren datos según la programación que se le haya dado. Puede desactivar un flujo de datos activo en cualquier momento siguiendo las instrucciones que se indican a continuación.

En el espacio de trabajo *[!UICONTROL Fuentes]* , seleccione la ficha **[!UICONTROL Flujos]** de datos. A continuación, seleccione el flujo de datos que desea deshabilitar.

![](../../../images/tutorials/dataflow/databases/list-of-dataflows.png)

La columna *Propiedades* aparece en la parte derecha de la pantalla, incluido un botón de alternancia **[!UICONTROL Habilitado]** . Seleccione la opción para desactivar el flujo de datos. Se puede utilizar la misma opción para volver a habilitar un flujo de datos después de desactivarlo.

![](../../../images/tutorials/dataflow/databases/disable.png)

### Activar datos de entrada para población de Perfiles

Los datos entrantes del conector de origen se pueden utilizar para enriquecer y rellenar los datos de Perfil del cliente en tiempo real. Para obtener más información sobre cómo rellenar los datos de Perfil de clientes reales, consulte el tutorial sobre población [de](../profile.md)Perfiles.