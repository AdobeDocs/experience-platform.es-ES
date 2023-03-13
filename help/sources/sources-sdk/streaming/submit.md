---
title: Prueba Y Envío Del Origen
description: El siguiente documento proporciona pasos sobre cómo probar y verificar una nueva fuente mediante la API de Flow Service e integrar una nueva fuente mediante fuentes de autoservicio (SDK de streaming).
hide: true
hidefromtoc: true
source-git-commit: 7744fef9751212a40f8f20df52812d38130c42fc
workflow-type: tm+mt
source-wordcount: '1249'
ht-degree: 0%

---

# Probar y enviar el origen

Los pasos finales para integrar su nueva fuente en Adobe Experience Platform mediante fuentes de autoservicio (SDK de streaming) son probar y enviar la nueva fuente. Una vez que haya completado la especificación de conexión y haya actualizado la especificación de flujo de flujo de flujo, puede comenzar a probar la funcionalidad del origen a través de la API o la IU. Si lo consigue, puede enviar la nueva fuente poniéndose en contacto con el representante de Adobe.

En el siguiente documento se proporcionan los pasos necesarios para probar y depurar el código fuente utilizando [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Primeros pasos

* Para obtener información sobre cómo realizar llamadas correctamente a las API de Platform, consulte la guía de [introducción a las API de Platform](../../../landing/api-guide.md).
* Para obtener información sobre cómo generar sus credenciales para las API de Platform, consulte el tutorial sobre [autenticación y acceso a las API de Experience Platform](../../../landing/api-authentication.md).
* Para obtener información sobre cómo configurar [!DNL Postman] para las API de Platform, consulte el tutorial sobre [configuración de la consola para desarrolladores y [!DNL Postman]](../../../landing/postman.md).
* Para ayudarle en el proceso de prueba y depuración, descargue el [Recopilación de verificación de fuentes de autoservicio y entorno aquí](../assets/sdk-verification.zip) y siga los pasos descritos a continuación.

## Prueba de la fuente mediante la API

Para probar el origen mediante la API, debe ejecutar el [Recopilación y entorno de verificación de fuentes de autoservicio](../assets/sdk-verification.zip) el [!DNL Postman] al tiempo que proporciona las variables de entorno adecuadas que pertenecen a su origen.

Para iniciar la prueba, primero debe configurar la colección y el entorno en [!DNL Postman]. A continuación, especifique el Id. de especificación de conexión que desea probar.

>[!NOTE]
>
>Todas las variables de ejemplo siguientes son valores de marcador de posición que debe actualizar, excepto para `flowSpecificationId` y `targetConnectionSpecId`, que son valores fijos.

| Parámetro | Descripción | Ejemplo |
| --- | --- | --- |
| `x-api-key` | Identificador único utilizado para autenticar llamadas a las API de Experience Platform. Consulte el tutorial sobre [autenticación y acceso a las API de Experience Platform](../../../landing/api-authentication.md) para obtener información sobre cómo recuperar su `x-api-key`. | `c8d9a2f5c1e03789bd22e8efdd1bdc1b` |
| `x-gw-ims-org-id` | Una entidad corporativa que puede poseer o licenciar productos y servicios y permitir el acceso a sus miembros. Consulte el tutorial sobre [configuración de la consola para desarrolladores y [!DNL Postman]](../../../landing/postman.md) para obtener instrucciones sobre cómo recuperar su `x-gw-ims-org-id` información. | `ABCEH0D9KX6A7WA7ATQE0TE@adobeOrg` |
| `authorizationToken` | El token de autorización necesario para completar las llamadas a las API de Experience Platform. Consulte el tutorial sobre [autenticación y acceso a las API de Experience Platform](../../../landing/api-authentication.md) para obtener información sobre cómo recuperar su `authorizationToken`. | `Bearer authorizationToken` |
| `schemaId` | Para que los datos de origen se utilicen en Platform, se debe crear un esquema de destino para estructurar los datos de origen según sus necesidades. Para ver los pasos detallados sobre cómo crear un esquema XDM de destino, consulte el tutorial sobre [creación de un esquema con la API](../../../xdm/api/schemas.md). | `https://ns.adobe.com/{TENANT_ID}.schemas.0ef4ce0d390f0809fad490802f53d30b` |
| `schemaVersion` | La versión única que se corresponde con el esquema. | `application/vnd.adobe.xed-full-notext+json; version=1` |
| `schemaAltId` | El `meta:altId` que se devuelve junto con el  `schemaId` al crear un nuevo esquema. | `_{TENANT_ID}.schemas.0ef4ce0d390f0809fad490802f53d30b` |
| `dataSetId` | Para ver los pasos detallados sobre cómo crear un conjunto de datos de destinatario, consulte el tutorial sobre [creación de un conjunto de datos mediante la API](../../../catalog/api/create-dataset.md). | `5f3c3cedb2805c194ff0b69a` |
| `mappings` | Los conjuntos de asignaciones se pueden utilizar para definir cómo se asignan los datos de un esquema de origen al de un esquema de destino. Para ver los pasos detallados sobre cómo crear una asignación, consulte el tutorial sobre [creación de un conjunto de asignaciones mediante la API](../../../data-prep/api/mapping-set.md). | `[{"destinationXdmPath":"person.name.firstName","sourceAttribute":"email.email_id","identity":false,"version":0},{"destinationXdmPath":"person.name.lastName","sourceAttribute":"email.activity.action","identity":false,"version":0}]` |
| `mappingId` | ID único que corresponde al conjunto de asignaciones. | `bf5286a9c1ad4266baca76ba3adc9366` |
| `connectionSpecId` | El ID de especificación de conexión que corresponde con su origen. Este es el ID que generó después de [creación de una nueva especificación de conexión](./create.md). | `2e8580db-6489-4726-96de-e33f5f60295f` |
| `flowSpecificationId` | El ID de especificación de flujo de `GenericStreamingAEP`. **Este es un valor fijo**. | `e77fde5a-22a8-11ed-861d-0242ac120002` |
| `targetConnectionSpecId` | El ID de conexión de destino del lago de datos donde aterrizan los datos ingeridos. **Este es un valor fijo**. | `c604ff05-7f1a-43c0-8e18-33bf874cb11c` |
| `verifyWatTimeInSecond` | Intervalo de tiempo designado que se debe seguir al comprobar la finalización de una ejecución de flujo. | `40` |
| `startTime` | La hora de inicio designada para el flujo de datos. La hora de inicio debe tener el formato unix time. | `1597784298` |

Una vez que haya proporcionado todas las variables de entorno, puede comenzar a ejecutar la colección usando [!DNL Postman] interfaz. En el [!DNL Postman] interfaz, seleccione los puntos suspensivos (**...**) al lado [!DNL Sources SSSs Verification Collection] y luego seleccione **Ejecutar colección**.

![corredor](../assets/runner.png)

El [!DNL Runner] , lo que le permite configurar el orden de ejecución del flujo de datos. Seleccionar **Ejecutar colección de verificación de SMS** para ejecutar la colección.

>[!NOTE]
>
>Puede deshabilitar **Eliminar flujo** en la lista de comprobación del orden de ejecución si prefiere utilizar el panel de monitorización de fuentes en la interfaz de usuario de Platform. Sin embargo, una vez que haya terminado con la prueba, debe asegurarse de que los flujos de prueba se eliminen.

![run-collection](../assets/run-collection.png)

## Prueba del origen mediante la interfaz de usuario

Para probar la fuente en la interfaz de usuario de, vaya al catálogo de fuentes de la zona protegida de su organización en la interfaz de usuario de Platform. Desde aquí, debería ver la nueva fuente debajo de *Transmisión* categoría.

Ahora que la nueva fuente está disponible en la zona protegida, debe seguir el flujo de trabajo de fuentes para probar las funcionalidades. Para empezar, seleccione **[!UICONTROL Configuración de]**.

![El catálogo de fuentes que muestra el nuevo origen de flujo continuo.](../assets/testing/catalog-test.png)

El [!UICONTROL Añadir datos] aparece el paso. Para probar que el origen puede transmitir datos, utilice la parte izquierda de la interfaz para cargar [una muestra de datos JSON](../assets/testing/raw.json.zip). Una vez cargados los datos, el lado derecho de la interfaz se actualiza a una vista previa de la jerarquía de archivos de los datos. Seleccionar **[!UICONTROL Siguiente]** para continuar.

![Paso para añadir datos en el flujo de trabajo de fuentes, donde puede cargar y previsualizar los datos antes de la ingesta.](../assets/testing/add-data-test.png)

El [!UICONTROL Detalles del flujo de datos] le permite seleccionar si desea utilizar un conjunto de datos existente o uno nuevo. Durante este proceso, también puede configurar los datos para que se introduzcan en el perfil y habilitar ajustes como [!UICONTROL Diagnósticos de error] y [!UICONTROL Ingesta parcial].

Para las pruebas, seleccione **[!UICONTROL Nuevo conjunto de datos]** y proporcione un nombre para el conjunto de datos de salida. Durante este paso, también puede proporcionar una descripción opcional para agregar más información al conjunto de datos. A continuación, seleccione un esquema al que asignar mediante la variable [!UICONTROL Búsqueda avanzada] o desplazándose por la lista de esquemas existentes en el menú desplegable. Una vez seleccionado un esquema, proporcione un nombre y una descripción para el flujo de datos.

Cuando termine, seleccione **[!UICONTROL Siguiente]**.

![Paso de detalle del flujo de datos en el flujo de trabajo de orígenes.](../assets/testing/dataflow-details-test.png)

El [!UICONTROL Asignación] Este paso aparece y le proporciona una interfaz para asignar los campos de origen del esquema de origen a sus campos XDM de destino adecuados en el esquema de destino.

Platform proporciona recomendaciones inteligentes para campos asignados automáticamente en función del esquema o el conjunto de datos de destino seleccionado. Puede ajustar manualmente las reglas de asignación para adaptarlas a sus casos de uso. En función de sus necesidades, puede elegir asignar campos directamente o utilizar funciones de preparación de datos para transformar los datos de origen y derivar valores calculados o calculados. Para ver los pasos detallados sobre el uso de la interfaz de asignación y los campos calculados, consulte la [Guía de IU de preparación de datos](../../../data-prep/ui/mapping.md)

Una vez que los datos de origen se hayan asignado correctamente, seleccione **[!UICONTROL Siguiente]**.

![Paso de asignación del flujo de trabajo de orígenes.](../assets/testing/mapping-test.png)

El **[!UICONTROL Revisar]** Este paso aparece, lo que le permite revisar el nuevo flujo de datos antes de crearlo. Los detalles se agrupan en las siguientes categorías:

* **[!UICONTROL Conexión]**: Muestra el nombre de la cuenta, el tipo de origen y otra información específica de la fuente de almacenamiento en la nube de flujo continuo que esté utilizando.
* **[!UICONTROL Asignar campos de conjunto de datos y asignación]**: Muestra el conjunto de datos y el esquema de destino que está utilizando para el flujo de datos.

Una vez revisado el flujo de datos, seleccione **[!UICONTROL Finalizar]** y deje pasar un tiempo para crear el flujo de datos.

![Paso de revisión del flujo de trabajo de orígenes.](../assets/testing/review-test.png)

Finalmente, debe recuperar el punto final de flujo de datos. Este punto de conexión se utilizará para suscribirse al webhook, lo que permitirá que el origen de la transmisión se comunique con el Experience Platform. Para recuperar el extremo de flujo continuo, vaya a [!UICONTROL Actividad de flujo de datos] página del flujo de datos que acaba de crear y copie el punto final de la parte inferior de la [!UICONTROL Propiedades] panel.

![El extremo de flujo continuo en la actividad de flujo de datos.](../assets/testing/endpoint-test.png)

## Enviar el origen

Una vez que el origen pueda completar todo el flujo de trabajo, puede ponerse en contacto con el Adobe y enviar el origen para que se integre en otras organizaciones de Experience Platform.
