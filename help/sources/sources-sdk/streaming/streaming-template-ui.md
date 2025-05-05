---
title: Plantilla de autoservicio de documentación para la IU de SDK de streaming
description: Aprenda a llevar los datos de flujo continuo de una fuente a Adobe Experience Platform mediante la interfaz de usuario de.
exl-id: 82254be0-fa31-4114-a0ec-179a990e0904
badge: Beta
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1194'
ht-degree: 1%

---

# Cree una conexión de origen y un flujo de datos para transmitir *YOURSOURCE* datos mediante la interfaz de usuario

*A medida que revise esta plantilla, reemplace o elimine todos los párrafos en cursiva (comenzando por este párrafo).*

*Comience por actualizar los metadatos (título y descripción) en la parte superior de la página. Ignore todas las instancias de UICONTROL en esta página. Esta es una etiqueta que ayuda a nuestros procesos de traducción automática a traducir correctamente la página a los múltiples idiomas que admitimos. Agregaremos etiquetas a su documentación después de que la envíe.*

Este tutorial proporciona los pasos para crear un conector de origen *YOURSOURCE* mediante la interfaz de usuario de Experience Platform.

## Información general

*Proporcione una breve descripción general de su compañía, incluido el valor que proporciona a los clientes. Incluya un vínculo a la página principal de la documentación del producto para obtener más información.*

>[!IMPORTANT]
>
>El equipo *YOURSOURCE* crea y mantiene este conector de origen y esta página de documentación. Para cualquier consulta o solicitud de actualización, comuníquese directamente con ellos en *Inserte un enlace o una dirección de correo electrónico donde pueda obtener información sobre actualizaciones*.

## Requisitos previos

*Agregue información en esta sección acerca de todo lo que los clientes deban tener en cuenta antes de comenzar a configurar el origen en la interfaz de usuario de Adobe Experience Platform. Puede ser aproximadamente:*

* *es necesario agregarlo a una lista de permitidos*
* *requisitos para el hash de correo electrónico*
* *cualquier detalle de la cuenta a su lado*
* *cómo obtener las credenciales de autenticación para conectarse a su plataforma*

### Recopilar credenciales necesarias

Para conectar *YOURSOURCE* a Experience Platform, debe proporcionar valores para las siguientes propiedades de conexión:

| Credencial | Descripción | Ejemplo |
| --- | --- | --- |
| *credencial uno* | *Agregue una breve descripción a la credencial de autenticación de origen aquí* | *Agregue un ejemplo de la credencial de autenticación de origen aquí* |
| *credencial dos* | *Agregue una breve descripción a la credencial de autenticación de origen aquí* | *Agregue un ejemplo de la credencial de autenticación de origen aquí* |
| *credencial tres* | *Agregue una breve descripción a la credencial de autenticación de origen aquí* | *Agregue un ejemplo de la credencial de autenticación de origen aquí* |

Para obtener más información sobre estas credenciales, consulte la documentación de autenticación *YOURSOURCE*. *Agregue un vínculo a la documentación de autenticación de su plataforma aquí*.

### Integrar *YOURSOURCE* con tu webhook

*Streaming SDK requiere que tu fuente admita webhooks para poder comunicarse con Experience Platform. En esta sección, debe proporcionar los pasos que los usuarios deberán seguir para integrar YOURSOURCE con un webhook.*

## Conecta tu cuenta de *YOURSOURCE*

En la interfaz de usuario de Experience Platform, seleccione **[!UICONTROL Fuentes]** en la barra de navegación izquierda para acceder al área de trabajo de [!UICONTROL Fuentes]. La pantalla [!UICONTROL Catálogo] muestra una variedad de orígenes con los que puede crear una cuenta.

Puede seleccionar la categoría adecuada del catálogo en la parte izquierda de la pantalla. También puede encontrar la fuente específica con la que desea trabajar utilizando la opción de búsqueda.

En la categoría **Transmisión**, seleccione *SU FUENTE* y, a continuación, seleccione **[!UICONTROL Agregar datos]**.

>[!TIP]
>
>Las capturas de pantalla utilizadas a continuación son ejemplos. Al crear su documentación, reemplace las imágenes por capturas de pantalla de su origen real. Puede utilizar la misma trama de marcado y el mismo color, así como los mismos nombres de archivo. Asegúrese de que la captura de pantalla capture toda la pantalla de la interfaz de usuario de Experience Platform. Para obtener información sobre cómo cargar tus capturas de pantalla, consulta la guía sobre [enviar tu documentación para revisión](../documentation/github.md).

![El catálogo de orígenes de Experience Platform](../assets/streaming/catalog.png)

## Seleccionar datos

Aparecerá el paso **[!UICONTROL Seleccionar datos]**, que proporciona una interfaz para que pueda seleccionar los datos que trae a Experience Platform.

* La parte izquierda de la interfaz es un explorador que le permite ver los flujos de datos disponibles en su cuenta;
* La parte derecha de la interfaz de le permite previsualizar hasta 100 filas de datos de un archivo JSON.

Seleccione **[!UICONTROL Cargar archivos]** para cargar un archivo JSON desde su sistema local. También puede arrastrar y soltar el archivo JSON que desee cargar en el panel [!UICONTROL Arrastrar y soltar archivos].

![Paso para agregar datos del flujo de trabajo de orígenes.](../assets/streaming/add-data.png)

Una vez cargado el archivo, la interfaz de vista previa se actualiza para mostrar una vista previa del esquema cargado. La interfaz de vista previa permite inspeccionar el contenido y la estructura de un archivo. También puede usar la utilidad [!UICONTROL Campo de búsqueda] para acceder a elementos específicos desde el esquema.

Cuando termine, seleccione **[!UICONTROL Siguiente]**.

![Paso de vista previa del flujo de trabajo de orígenes.](../assets/streaming/preview.png)

## Detalles del flujo de datos

Aparecerá el paso **Detalle del flujo de datos**, que le proporcionará opciones para usar un conjunto de datos existente o establecer uno nuevo para su flujo de datos, así como la oportunidad de proporcionar un nombre y una descripción para su flujo de datos. Durante este paso, también puede configurar las opciones de Ingesta de perfiles, diagnósticos de error, ingesta parcial y alertas.

Cuando termine, seleccione **[!UICONTROL Siguiente]**.

![Paso de detalle del flujo de datos del flujo de trabajo de origen.](../assets/streaming/dataflow-detail.png)

## Asignación

Aparecerá el paso [!UICONTROL Mapping], que le proporcionará una interfaz para asignar los campos de origen del esquema de origen a sus campos XDM de destino adecuados en el esquema de destino.

Experience Platform proporciona recomendaciones inteligentes para campos asignados automáticamente en función del esquema o conjunto de datos de destino seleccionado. Puede ajustar manualmente las reglas de asignación para adaptarlas a sus casos de uso. En función de sus necesidades, puede elegir asignar campos directamente o utilizar funciones de preparación de datos para transformar los datos de origen y derivar valores calculados o calculados. Para ver los pasos detallados sobre el uso de la interfaz de asignador y los campos calculados, consulte la [guía de la interfaz de usuario de la preparación de datos](https://experienceleague.adobe.com/docs/experience-platform/data-prep/ui/mapping.html?lang=es).

Una vez que los datos de origen estén asignados correctamente, seleccione **[!UICONTROL Siguiente]**.

![Paso de asignación del flujo de trabajo de orígenes.](../assets/streaming/mapping.png)

## Revisar

Aparece el paso **[!UICONTROL Revisar]**, que le permite revisar el nuevo flujo de datos antes de crearlo. Los detalles se agrupan en las siguientes categorías:

* **[!UICONTROL Conexión]**: muestra el tipo de origen, la ruta de acceso relevante del archivo de origen elegido y la cantidad de columnas dentro de ese archivo de origen.
* **[!UICONTROL Asignar campos de conjunto de datos y asignación]**: muestra en qué conjunto de datos se están ingiriendo los datos de origen, incluido el esquema al que se adhiere el conjunto de datos.

Una vez que haya revisado el flujo de datos, haga clic en **[!UICONTROL Finalizar]** y espere un poco para que se cree el flujo de datos.

![Paso de revisión del flujo de trabajo de orígenes.](../assets/streaming/review.png)

## Obtener la URL del extremo de flujo continuo

Con el flujo de datos de flujo continuo creado, ahora puede recuperar la URL del extremo de flujo continuo. Este punto de conexión se utilizará para suscribirse al webhook, lo que permitirá que el origen de flujo se comunique con Experience Platform.

Para recuperar el extremo de flujo continuo, vaya a la página [!UICONTROL Actividad de flujo de datos] del flujo de datos que acaba de crear y copie el extremo desde la parte inferior del panel [!UICONTROL Propiedades].

![Punto final de flujo continuo en la actividad del flujo de datos.](../assets/testing/endpoint-test.png)

## Pasos siguientes

*Los flujos de trabajo para los pasos restantes de la creación de un flujo de datos están modularizados. Si desea realizar alguna llamada específica con respecto a su origen, consulte la sección de recursos adicionales a continuación.*

Siguiendo este tutorial, ha establecido una conexión con su cuenta de *YOURSOURCE*. Ahora puede continuar con el siguiente tutorial y [configurar un flujo de datos para introducir datos en Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/sources/ui-tutorials/dataflow/crm.html?lang=es).

## Recursos adicionales

*Esta es una sección opcional donde puede proporcionar más vínculos a la documentación del producto o a cualquier otro paso, captura de pantalla o matiz que considere importante para que el cliente tenga éxito. Puede utilizar esta sección para agregar información o sugerencias sobre todo el flujo de trabajo del origen, especialmente si hay problemas específicos que podría encontrar un usuario final.*
