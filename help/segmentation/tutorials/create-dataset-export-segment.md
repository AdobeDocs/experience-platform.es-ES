---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Crear un conjunto de datos para exportar un segmento de audiencia
topic: tutorial
translation-type: tm+mt
source-git-commit: 6d24637dc6cc282f98288b6416e4a3b7cebe42ea

---


# Crear un conjunto de datos para exportar un segmento de audiencia

Adobe Experience Platform le permite segmentar fácilmente perfiles de clientes en audiencias basadas en atributos específicos. Una vez creados los segmentos, puede exportar esa audiencia a un conjunto de datos donde se pueda acceder a ella y actuar en consecuencia. Para que la exportación se realice correctamente, el conjunto de datos debe configurarse correctamente.

En este tutorial se explican los pasos necesarios para crear un conjunto de datos que pueda utilizarse para exportar un segmento de audiencia mediante la interfaz de usuario de la plataforma de experiencia.

Este tutorial está directamente relacionado con los pasos descritos en el tutorial para [evaluar y acceder a los resultados](./evaluate-a-segment.md)del segmento. El tutorial de evaluación de un segmento proporciona pasos para crear un conjunto de datos mediante la API de catálogo, mientras que este tutorial describe los pasos para crear un conjunto de datos mediante la interfaz de usuario de la plataforma de experiencia.

## Primeros pasos

Para exportar un segmento, el conjunto de datos debe basarse en el Esquema de Unión de Perfil individual XDM. Un esquema de unión es un esquema de sólo lectura generado por el sistema que agrega los campos de todos los esquemas que comparten la misma clase, en este caso la clase de Perfil individual XDM. Para obtener más información sobre los esquemas de vista de uniones, consulte la sección Perfil de clientes en tiempo [real de la guía](../../xdm/schema/composition.md#union)para desarrolladores de Esquema Registry.

Para vista de esquemas de unión en la interfaz de usuario, haga clic en **Perfiles** en el panel de navegación izquierdo y, a continuación, haga clic en la ficha esquema *de* Unión como se muestra a continuación.

![Ficha esquema de Unión en la interfaz de usuario de la plataforma de experiencia](../images/tutorials/segment-export-dataset/union-schema-ui.png)


## Espacio de trabajo de conjuntos de datos

El espacio de trabajo de conjuntos de datos de la interfaz de usuario de la plataforma de experiencia le permite realizar vistas y administrar todos los conjuntos de datos que ha realizado su organización de IMS, así como crear otros nuevos.

Para vista del espacio de trabajo de conjuntos de datos, haga clic en **Conjuntos** de datos en el panel de navegación izquierdo y, a continuación, haga clic en la ficha *Examinar* . El espacio de trabajo de conjuntos de datos contiene una lista de conjuntos de datos, que incluye columnas con *Nombre*, *Creado* (fecha y hora), *Origen*, *Esquema* y Estado **** del último lote, así como la fecha y hora en que el conjunto de datos fue la Última actualización. Según el ancho de cada columna, puede que sea necesario desplazarse hacia la izquierda o la derecha para ver todas las columnas.

>[!NOTE] Haga clic en el icono de filtro situado junto a la barra de búsqueda para utilizar las funciones de filtrado con el fin de vista únicamente de los conjuntos de datos habilitados para el Perfil del cliente en tiempo real.

![Vista de todos los conjuntos de datos](../images/tutorials/segment-export-dataset/datasets-workspace.png)

## Crear un conjunto de datos

Para crear un conjunto de datos, haga clic en **Crear conjunto** de datos en la esquina superior derecha del espacio de trabajo Conjunto de datos.

![Haga clic en Crear conjunto de datos](../images/tutorials/segment-export-dataset/dataset-click-create.png)

En la pantalla *Crear conjunto de datos* , haga clic en **Crear conjunto de datos desde Esquema** para continuar.

![Seleccionar fuente de datos](../images/tutorials/segment-export-dataset/create-dataset.png)

## Seleccionar Esquema de Unión de Perfil individual XDM

Para seleccionar el Esquema de Unión de Perfil individual XDM para utilizarlo en el conjunto de datos, busque el esquema &quot;Perfil individual XDM&quot; con un tipo de &quot;Unión&quot; en la pantalla *Seleccionar Esquema* .

Seleccione el botón de radio junto a Perfil **individual** XDM y, a continuación, haga clic en **Siguiente** en la esquina superior derecha.

![Seleccionar esquema](../images/tutorials/segment-export-dataset/select-schema.png)

## Configurar conjunto de datos

En la pantalla **Configurar conjunto de datos** , se le pedirá que asigne un *nombre* al conjunto de datos y también puede proporcionar una *descripción* del conjunto de datos.

**Notas sobre los nombres de conjuntos de datos:**
- Los nombres de los conjuntos de datos deben ser cortos y descriptivos para que el conjunto de datos pueda encontrarse fácilmente en la biblioteca más adelante.
- Los nombres de los conjuntos de datos deben ser únicos, lo que significa que también deben ser lo suficientemente específicos como para que no se vuelvan a utilizar en el futuro.
- Se recomienda proporcionar información adicional sobre el conjunto de datos mediante el campo de descripción, ya que puede ayudar a otros usuarios a diferenciar entre conjuntos de datos en el futuro.

Una vez que el conjunto de datos tenga un nombre y una descripción, haga clic en **Finalizar**.

![Configurar conjunto de datos](../images/tutorials/segment-export-dataset/configure-dataset.png)

## actividad de conjunto de datos

Ahora se ha creado un conjunto de datos vacío y se le ha devuelto a la ficha Actividad *del* conjunto de datos en el espacio de trabajo Conjunto de datos. Debe ver el nombre del conjunto de datos en la esquina superior izquierda del espacio de trabajo, junto con una notificación de que &quot;No se han agregado lotes&quot;. Esto es de esperar, ya que todavía no ha agregado ningún lote a este conjunto de datos.

En la parte derecha del espacio de trabajo Conjunto de datos, verá la ficha **Información** que contiene información relacionada con el nuevo conjunto de datos, como ID *de* conjunto de datos, *Nombre*, *Descripción*, Nombre *de******* tabla,de datos, Streaming, OrigenDeDatos y OrigenFuente. La ficha Información también incluye información sobre cuándo se *creó* el conjunto de datos y su fecha de *última modificación* .

Tenga en cuenta el ID **del** conjunto de datos, ya que este valor es necesario para completar el flujo de trabajo de exportación del segmento de audiencia.

![actividad de conjunto de datos](../images/tutorials/segment-export-dataset/dataset-activity.png)

## Pasos siguientes

Ahora que ha creado un conjunto de datos basado en el Esquema de Unión de Perfil individual XDM, puede utilizar el ID **de** conjunto de datos para continuar con el tutorial de [evaluación y acceso a los resultados](./evaluate-a-segment.md) de segmentos.

En este momento, vuelva al tutorial de resultados de segmentos de evaluación y seleccione el paso [Generar Perfiles individuales XDM para miembros](./evaluate-a-segment.md#generate-profiles-for-audience-members) de audiencia de la [exportación de un flujo de trabajo de segmentos](./evaluate-a-segment.md#export-a-segment) .
