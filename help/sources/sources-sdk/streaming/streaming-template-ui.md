---
title: Plantilla de autoservicio de documentación para la interfaz de usuario del SDK de transmisión
description: Aprenda a llevar datos de flujo continuo de un origen a Adobe Experience Platform mediante la interfaz de usuario.
hide: true
hidefromtoc: true
source-git-commit: eba86ab8aa7d4deac967f5dfb13b2a691bc7c773
workflow-type: tm+mt
source-wordcount: '1193'
ht-degree: 1%

---

# Crear una conexión de origen y un flujo de datos para flujo *YOURSOURCE* datos mediante la interfaz de usuario

*A medida que recorre esta plantilla, reemplace o elimine todos los párrafos en cursiva (a partir de este).*

*Comience por actualizar los metadatos (título y descripción) en la parte superior de la página. Ignore todas las instancias de UICONTROL en esta página. Esta es una etiqueta que ayuda a nuestros procesos de traducción automática a traducir correctamente la página a los múltiples idiomas compatibles. Añadiremos etiquetas a su documentación después de enviarla.*

Este tutorial proporciona los pasos para crear un *YOURSOURCE* conector de origen mediante la interfaz de usuario de Platform.

## Información general

*Proporcione una breve descripción general de su empresa, incluido el valor que proporciona a los clientes. Incluya un vínculo a la página de inicio de la documentación del producto para obtener más información.*

>[!IMPORTANT]
>
>Esta página de documentación la creó el *YOURSOURCE* equipo. Para cualquier consulta o solicitud de actualización, póngase en contacto con ellos directamente en *Inserte un vínculo o una dirección de correo electrónico donde pueda acceder a las actualizaciones*.

## Requisitos previos

*Agregue información en esta sección sobre cualquier cosa que los clientes deban tener en cuenta antes de comenzar a configurar el origen en la interfaz de usuario de Adobe Experience Platform. Esto puede tratarse de:*

* *necesidad de añadirlo a una lista de permitidos*
* *requisitos para el hash de correo electrónico*
* *cualquier información específica de la cuenta de su parte*
* *cómo obtener las credenciales de autenticación para conectarse a la plataforma*

### Recopilar las credenciales necesarias

Para conectarse *YOURSOURCE* en Platform, debe proporcionar valores para las siguientes propiedades de conexión:

| Credencial | Descripción | Ejemplo |
| --- | --- | --- |
| *credencial uno* | *Añada una breve descripción a la credencial de autenticación de la fuente aquí* | *Añada aquí un ejemplo de la credencial de autenticación de la fuente* |
| *credencial dos* | *Añada una breve descripción a la credencial de autenticación de la fuente aquí* | *Añada aquí un ejemplo de la credencial de autenticación de la fuente* |
| *credencial tres* | *Añada una breve descripción a la credencial de autenticación de la fuente aquí* | *Añada aquí un ejemplo de la credencial de autenticación de la fuente* |

Para obtener más información sobre estas credenciales, consulte la *YOURSOURCE* documentación de autenticación. *Añada el enlace a la documentación de autenticación de su plataforma aquí*.

### Integrar *YOURSOURCE* con su weblock

*El SDK de transmisión requiere que el origen sea compatible con los enlaces web para comunicarse con el Experience Platform. En esta sección, debe proporcionar los pasos que los usuarios deberán seguir para integrar YOURSOURCE con un enlace web.*

## Conecte su *YOURSOURCE* account

En la interfaz de usuario de Platform, seleccione **[!UICONTROL Fuentes]** en la barra de navegación izquierda para acceder a la [!UICONTROL Fuentes] espacio de trabajo. La variable [!UICONTROL Catálogo] muestra una variedad de fuentes con las que puede crear una cuenta.

Puede seleccionar la categoría adecuada del catálogo en la parte izquierda de la pantalla. Alternativamente, puede encontrar la fuente específica con la que desea trabajar usando la opción de búsqueda.

En el **Transmisión** categoría, seleccione *YOURSOURCE* y, a continuación, seleccione **[!UICONTROL Añadir datos]**.

>[!TIP]
>
>Las capturas de pantalla utilizadas a continuación son ejemplos. Al crear la documentación, reemplace las imágenes con capturas de pantalla de su fuente real. Puede utilizar el mismo patrón y color de marca, así como los mismos nombres de archivo. Asegúrese de que la captura de pantalla captura toda la pantalla de la interfaz de usuario de Platform. Para obtener información sobre cómo cargar las capturas de pantalla, consulte la guía de [enviar su documentación para su revisión](../documentation/github.md).

![El catálogo de fuentes del Experience Platform](../assets/streaming/catalog.png)

## Selección de datos

La variable **[!UICONTROL Seleccionar datos]** , proporcionando una interfaz para que seleccione los datos que aporta a Platform.

* La parte izquierda de la interfaz es un navegador que le permite ver los flujos de datos disponibles en su cuenta;
* La parte derecha de la interfaz le permite previsualizar hasta 100 filas de datos de un archivo JSON.

Select **[!UICONTROL Cargar archivos]** para cargar un archivo JSON desde su sistema local. Como alternativa, puede arrastrar y soltar el archivo JSON que desea cargar en el [!UICONTROL Arrastrar y soltar archivos] panel.

![El paso añadir datos del flujo de trabajo de fuentes.](../assets/streaming/add-data.png)

Una vez cargado el archivo, la interfaz de vista previa se actualiza para mostrar una vista previa del esquema que ha cargado. La interfaz de vista previa permite inspeccionar el contenido y la estructura de un archivo. También puede usar la variable [!UICONTROL Campo de búsqueda] para acceder a elementos específicos desde el esquema.

Cuando termine, seleccione **[!UICONTROL Siguiente]**.

![El paso de vista previa del flujo de trabajo de fuentes.](../assets/streaming/preview.png)

## Detalles de flujo de datos

La variable **Detalles de flujo de datos** aparece, proporcionando opciones para utilizar un conjunto de datos existente o establecer un nuevo conjunto de datos para su flujo de datos, así como una oportunidad para proporcionar un nombre y una descripción para su flujo de datos. Durante este paso, también puede configurar las opciones de ingesta de perfiles, diagnóstico de errores, ingesta parcial y alertas.

Cuando termine, seleccione **[!UICONTROL Siguiente]**.

![Paso de flujo de datos detallado del flujo de trabajo de origen.](../assets/streaming/dataflow-detail.png)

## Asignación

La variable [!UICONTROL Asignación] aparece, proporcionando una interfaz para asignar los campos de origen del esquema de origen a los campos XDM de destino adecuados en el esquema de destino.

Platform proporciona recomendaciones inteligentes para campos asignados automáticamente en función del esquema o conjunto de datos de destino que haya seleccionado. Puede ajustar manualmente las reglas de asignación para adaptarlas a sus casos de uso. En función de sus necesidades, puede elegir asignar campos directamente o utilizar funciones de preparación de datos para transformar los datos de origen a fin de derivar valores calculados o calculados. Para ver los pasos completos sobre el uso de la interfaz del asignador y los campos calculados, consulte la [Guía de la interfaz de usuario de preparación de datos](https://experienceleague.adobe.com/docs/experience-platform/data-prep/ui/mapping.html).

Una vez asignados correctamente los datos de origen, seleccione **[!UICONTROL Siguiente]**.

![El paso de asignación del flujo de trabajo de fuentes.](../assets/streaming/mapping.png)

## Revisión

La variable **[!UICONTROL Consulte]** , lo que le permite revisar el nuevo flujo de datos antes de crearlo. Los detalles se agrupan en las siguientes categorías:

* **[!UICONTROL Conexión]**: Muestra el tipo de origen, la ruta correspondiente del archivo de origen elegido y la cantidad de columnas dentro de ese archivo de origen.
* **[!UICONTROL Asignación de campos de conjunto de datos y asignación]**: Muestra en qué conjunto de datos se están incorporando los datos de origen, incluido el esquema al que se adhiere el conjunto de datos.

Una vez que haya revisado el flujo de datos, haga clic en **[!UICONTROL Finalizar]** y permitir que se cree un flujo de datos.

![El paso de revisión del flujo de trabajo de fuentes.](../assets/streaming/review.png)

## Obtener la URL del extremo de flujo continuo

Con el flujo de datos de flujo continuo creado, ahora puede recuperar la URL del extremo de flujo continuo. Este punto final se utilizará para suscribirse a su enlace web, permitiendo que su fuente de transmisión se comunique con el Experience Platform.

Para recuperar el extremo de flujo continuo, vaya a la [!UICONTROL Actividad de flujo de datos] del flujo de datos que acaba de crear y copie el extremo desde la parte inferior del [!UICONTROL Propiedades] panel.

![El extremo de flujo continuo en la actividad de flujo de datos.](../assets/testing/endpoint-test.png)

## Pasos siguientes

*Los flujos de trabajo para los pasos restantes de creación de un flujo de datos se modularizan. Si desea realizar alguna llamada específica con respecto a su origen, consulte la sección de recursos adicionales a continuación.*

Al seguir este tutorial, ha establecido una conexión con su *YOURSOURCE* cuenta. Ahora puede continuar con el siguiente tutorial y [configurar un flujo de datos para introducir datos en Platform](https://experienceleague.adobe.com/docs/experience-platform/sources/ui-tutorials/dataflow/crm.html).

## Recursos adicionales

*Esta es una sección opcional en la que puede proporcionar más vínculos a la documentación del producto o a cualquier otro paso, capturas de pantalla o matices que considere importantes para que el cliente tenga éxito. Puede utilizar esta sección para agregar información o sugerencias sobre todo el flujo de trabajo de su fuente, especialmente si hay problemas particulares que un usuario final podría encontrar.*
