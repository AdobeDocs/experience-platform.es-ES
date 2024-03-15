---
title: Plantilla de autoservicio de documentación para la interfaz de usuario del SDK de streaming
description: Aprenda a llevar los datos de flujo continuo de una fuente a Adobe Experience Platform mediante la interfaz de usuario de.
exl-id: 82254be0-fa31-4114-a0ec-179a990e0904
source-git-commit: 36de441a68a7cb9248d058e12e6ca3ed60f899ef
workflow-type: tm+mt
source-wordcount: '1186'
ht-degree: 1%

---

# Crear una conexión de origen y un flujo de datos para transmitir *SU ORIGEN* datos mediante la interfaz de usuario

*A medida que avanza por esta plantilla, reemplace o elimine todos los párrafos en cursiva (empezando por esta).*

*Comience por actualizar los metadatos (título y descripción) en la parte superior de la página. Ignore todas las instancias de UICONTROL en esta página. Esta es una etiqueta que ayuda a nuestros procesos de traducción automática a traducir correctamente la página a los múltiples idiomas que admitimos. Agregaremos etiquetas a su documentación después de que la envíe.*

Este tutorial proporciona los pasos para crear una *SU ORIGEN* conector de origen mediante la interfaz de usuario de Platform.

## Información general

*Proporcione una breve descripción general de su empresa, incluido el valor que proporciona a los clientes. Incluya un vínculo a la página de inicio de la documentación del producto para obtener más información.*

>[!IMPORTANT]
>
>Este conector de origen y esta página de documentación los crea y mantiene el *SU ORIGEN* equipo. Para cualquier consulta o solicitud de actualización, póngase en contacto directamente con ellos en *Insertar vínculo o dirección de correo electrónico donde se pueda contactar para obtener actualizaciones*.

## Requisitos previos

*Agregue información en esta sección sobre todo lo que los clientes deben tener en cuenta antes de comenzar a configurar el origen en la interfaz de usuario de Adobe Experience Platform. Puede tratarse de lo siguiente:*

* *necesidad de añadirse a una lista de permitidos*
* *requisitos para el hash de correo electrónico*
* *cualquier detalle de la cuenta de su parte*
* *cómo obtener las credenciales de autenticación para conectarse a la plataforma*

### Recopilar credenciales necesarias

Para poder conectarse *SU ORIGEN* En Platform, debe proporcionar valores para las siguientes propiedades de conexión:

| Credencial | Descripción | Ejemplo |
| --- | --- | --- |
| *credencial uno* | *Agregue una breve descripción a la credencial de autenticación de su fuente aquí* | *Agregue un ejemplo de la credencial de autenticación de su origen aquí* |
| *credencial dos* | *Agregue una breve descripción a la credencial de autenticación de su fuente aquí* | *Agregue un ejemplo de la credencial de autenticación de su origen aquí* |
| *credencial tres* | *Agregue una breve descripción a la credencial de autenticación de su fuente aquí* | *Agregue un ejemplo de la credencial de autenticación de su origen aquí* |

Para obtener más información sobre estas credenciales, consulte la *SU ORIGEN* documentación de autenticación. *Agregue un vínculo a la documentación de autenticación de su plataforma aquí*.

### Integrar *SU ORIGEN* con su webhook

*El SDK de streaming requiere que su fuente admita los webhooks para poder comunicarse con el Experience Platform. En esta sección, debe proporcionar los pasos que los usuarios deberán seguir para integrar YOURSOURCE con un webhook.*

## Conecte su *SU ORIGEN* account

En la IU de Platform, seleccione **[!UICONTROL Fuentes]** desde la barra de navegación izquierda para acceder a [!UICONTROL Fuentes] workspace. El [!UICONTROL Catálogo] La pantalla muestra una variedad de fuentes con las que puede crear una cuenta.

Puede seleccionar la categoría adecuada del catálogo en la parte izquierda de la pantalla. También puede encontrar la fuente específica con la que desea trabajar utilizando la opción de búsqueda.

En el **Transmisión** categoría, seleccionar *SU ORIGEN*, y luego seleccione **[!UICONTROL Añadir datos]**.

>[!TIP]
>
>Las capturas de pantalla utilizadas a continuación son ejemplos. Al crear su documentación, reemplace las imágenes por capturas de pantalla de su origen real. Puede utilizar la misma trama de marcado y el mismo color, así como los mismos nombres de archivo. Asegúrese de que la captura de pantalla capture toda la pantalla de la interfaz de usuario de Platform. Para obtener información sobre cómo cargar las capturas de pantalla, consulte la guía de [enviar la documentación para su revisión](../documentation/github.md).

![El catálogo de fuentes del Experience Platform](../assets/streaming/catalog.png)

## Seleccionar datos

El **[!UICONTROL Seleccionar datos]** Este paso aparece y proporciona una interfaz para que seleccione los datos que lleva a Platform.

* La parte izquierda de la interfaz es un explorador que le permite ver los flujos de datos disponibles en su cuenta;
* La parte derecha de la interfaz de le permite previsualizar hasta 100 filas de datos de un archivo JSON.

Seleccionar **[!UICONTROL Cargar archivos]** para cargar un archivo JSON desde el sistema local. También puede arrastrar y soltar el archivo JSON que desee cargar en [!UICONTROL Arrastrar y soltar archivos] panel.

![Paso para añadir datos del flujo de trabajo de orígenes.](../assets/streaming/add-data.png)

Una vez cargado el archivo, la interfaz de vista previa se actualiza para mostrar una vista previa del esquema cargado. La interfaz de vista previa permite inspeccionar el contenido y la estructura de un archivo. También puede utilizar la variable [!UICONTROL Campo de búsqueda] para acceder a elementos específicos desde el esquema.

Cuando termine, seleccione **[!UICONTROL Siguiente]**.

![Paso de vista previa del flujo de trabajo de orígenes.](../assets/streaming/preview.png)

## Detalles del flujo de datos

El **Detalles del flujo de datos** Este paso se muestra y le proporciona opciones para utilizar un conjunto de datos existente o establecer un nuevo conjunto de datos para su flujo de datos, así como la oportunidad de proporcionar un nombre y una descripción para su flujo de datos. Durante este paso, también puede configurar las opciones de Ingesta de perfiles, diagnósticos de error, ingesta parcial y alertas.

Cuando termine, seleccione **[!UICONTROL Siguiente]**.

![Paso de detalle del flujo de datos del flujo de trabajo de orígenes.](../assets/streaming/dataflow-detail.png)

## Asignación

El [!UICONTROL Asignación] Este paso aparece y le proporciona una interfaz para asignar los campos de origen del esquema de origen a sus campos XDM de destino adecuados en el esquema de destino.

Platform proporciona recomendaciones inteligentes para campos asignados automáticamente en función del esquema o el conjunto de datos de destino seleccionado. Puede ajustar manualmente las reglas de asignación para adaptarlas a sus casos de uso. En función de sus necesidades, puede elegir asignar campos directamente o utilizar funciones de preparación de datos para transformar los datos de origen y derivar valores calculados o calculados. Para ver los pasos detallados sobre el uso de la interfaz de asignación y los campos calculados, consulte la [Guía de IU de preparación de datos](https://experienceleague.adobe.com/docs/experience-platform/data-prep/ui/mapping.html).

Una vez que los datos de origen se hayan asignado correctamente, seleccione **[!UICONTROL Siguiente]**.

![Paso de asignación del flujo de trabajo de orígenes.](../assets/streaming/mapping.png)

## Revisión

El **[!UICONTROL Revisar]** Este paso aparece, lo que le permite revisar el nuevo flujo de datos antes de crearlo. Los detalles se agrupan en las siguientes categorías:

* **[!UICONTROL Conexión]**: Muestra el tipo de origen, la ruta relevante del archivo de origen elegido y la cantidad de columnas dentro de ese archivo de origen.
* **[!UICONTROL Asignar campos de conjunto de datos y asignación]**: Muestra en qué conjunto de datos se están ingiriendo los datos de origen, incluido el esquema al que se adhiere el conjunto de datos.

Una vez revisado el flujo de datos, haga clic en **[!UICONTROL Finalizar]** y deje pasar un tiempo para crear el flujo de datos.

![Paso de revisión del flujo de trabajo de orígenes.](../assets/streaming/review.png)

## Obtener la URL del extremo de flujo continuo

Con el flujo de datos de flujo continuo creado, ahora puede recuperar la URL del extremo de flujo continuo. Este punto de conexión se utilizará para suscribirse al webhook, lo que permitirá que el origen de la transmisión se comunique con el Experience Platform.

Para recuperar el extremo de flujo continuo, vaya a [!UICONTROL Actividad de flujo de datos] página del flujo de datos que acaba de crear y copie el punto final de la parte inferior de la [!UICONTROL Propiedades] panel.

![El extremo de flujo continuo en la actividad de flujo de datos.](../assets/testing/endpoint-test.png)

## Pasos siguientes

*Los flujos de trabajo para los pasos restantes de la creación de un flujo de datos están modularizados. Si desea realizar alguna llamada específica con respecto a su fuente, consulte la sección de recursos adicionales a continuación.*

Al seguir este tutorial, ha establecido una conexión con su *SU ORIGEN* cuenta. Ahora puede continuar con el siguiente tutorial y [configuración de un flujo de datos para introducir datos en Platform](https://experienceleague.adobe.com/docs/experience-platform/sources/ui-tutorials/dataflow/crm.html).

## Recursos adicionales

*Esta es una sección opcional en la que puede proporcionar más vínculos a la documentación del producto o a cualquier otro paso, captura de pantalla o matiz que considere importante para que el cliente tenga éxito. Puede utilizar esta sección para agregar información o sugerencias sobre todo el flujo de trabajo del origen, especialmente si hay problemas concretos que un usuario final podría encontrar.*
