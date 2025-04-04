---
title: Probar Y Enviar Su Source
description: El siguiente documento proporciona pasos sobre cómo probar y comprobar una nueva fuente mediante la API de Flow Service e integrar una nueva fuente mediante fuentes de autoservicio (Streaming SDK).
exl-id: 2ae0c3ad-1501-42ab-aaaa-319acea94ec2
badge: Beta
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1273'
ht-degree: 0%

---

# Probar y enviar el origen

>[!NOTE]
>
>Fuentes de autoservicio Streaming SDK está en versión beta. Lea [información general de orígenes](../../home.md#terms-and-conditions) para obtener más información sobre el uso de orígenes etiquetados como beta.

Los pasos finales para integrar su nueva fuente en Adobe Experience Platform mediante fuentes de autoservicio (Streaming de SDK) son probar y enviar la nueva fuente. Una vez que haya completado la especificación de conexión y haya actualizado la especificación de flujo de flujo de flujo, puede comenzar a probar la funcionalidad del origen a través de la API o la IU. Si lo consigue, puede enviar su nuevo origen poniéndose en contacto con su representante de Adobe.

El siguiente documento proporciona pasos sobre cómo probar y depurar el origen mediante la [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Introducción

* Para obtener información sobre cómo realizar llamadas correctamente a las API de Experience Platform, consulte la guía sobre [introducción a las API de Experience Platform](../../../landing/api-guide.md).
* Para obtener información sobre cómo generar tus credenciales para las API de Experience Platform, consulta el tutorial sobre [autenticación y acceso a las API de Experience Platform](../../../landing/api-authentication.md).
* Para obtener información sobre cómo configurar [!DNL Postman] para las API de Experience Platform, consulte el tutorial sobre [configuración de la consola para desarrolladores y [!DNL Postman]](../../../landing/postman.md).
* Para facilitar el proceso de prueba y depuración, descargue la colección de verificación de [fuentes de autoservicio y el entorno aquí](../assets/sdk-verification.zip) y siga los pasos descritos a continuación.

## Prueba de la fuente mediante la API

Para probar el origen mediante la API, debe ejecutar la [colección de comprobación de fuentes de autoservicio y el entorno](../assets/sdk-verification.zip) en [!DNL Postman], al tiempo que proporciona las variables de entorno apropiadas que pertenecen al origen.

Para iniciar la prueba, primero debe configurar la colección y el entorno en [!DNL Postman]. A continuación, especifique el Id. de especificación de conexión que desea probar.

>[!NOTE]
>
>Todas las variables de ejemplo siguientes son valores de marcador de posición que debe actualizar, excepto `flowSpecificationId` y `targetConnectionSpecId`, que son valores fijos.

| Parámetro | Descripción | Ejemplo |
| --- | --- | --- |
| `x-api-key` | Identificador único utilizado para autenticar llamadas a las API de Experience Platform. Consulte el tutorial sobre [autenticación y acceso a las API de Experience Platform](../../../landing/api-authentication.md) para obtener información sobre cómo recuperar su `x-api-key`. | `c8d9a2f5c1e03789bd22e8efdd1bdc1b` |
| `x-gw-ims-org-id` | Una entidad corporativa que puede poseer o licenciar productos y servicios y permitir el acceso a sus miembros. Consulte el tutorial sobre [configuración de la consola para desarrolladores y [!DNL Postman]](../../../landing/postman.md) para obtener instrucciones sobre cómo recuperar la información de `x-gw-ims-org-id`. | `ABCEH0D9KX6A7WA7ATQE0TE@adobeOrg` |
| `authorizationToken` | El token de autorización necesario para completar las llamadas a las API de Experience Platform. Consulte el tutorial sobre [autenticación y acceso a las API de Experience Platform](../../../landing/api-authentication.md) para obtener información sobre cómo recuperar su `authorizationToken`. | `Bearer authorizationToken` |
| `schemaId` | Para que los datos de origen se utilicen en Experience Platform, se debe crear un esquema de destino para estructurar los datos de origen según sus necesidades. Para ver los pasos detallados sobre cómo crear un esquema XDM de destino, consulte el tutorial de [creación de un esquema mediante la API](../../../xdm/api/schemas.md). | `https://ns.adobe.com/{TENANT_ID}.schemas.0ef4ce0d390f0809fad490802f53d30b` |
| `schemaVersion` | La versión única que se corresponde con el esquema. | `application/vnd.adobe.xed-full-notext+json; version=1` |
| `schemaAltId` | `meta:altId` que se devuelve junto con `schemaId` al crear un nuevo esquema. | `_{TENANT_ID}.schemas.0ef4ce0d390f0809fad490802f53d30b` |
| `dataSetId` | Para ver los pasos detallados sobre cómo crear un conjunto de datos de destino, consulte el tutorial de [creación de un conjunto de datos mediante la API](../../../catalog/api/create-dataset.md). | `5f3c3cedb2805c194ff0b69a` |
| `mappings` | Los conjuntos de asignaciones se pueden utilizar para definir cómo se asignan los datos de un esquema de origen al de un esquema de destino. Para ver los pasos detallados sobre cómo crear una asignación, consulte el tutorial sobre [creación de un conjunto de asignaciones mediante la API](../../../data-prep/api/mapping-set.md). | `[{"destinationXdmPath":"person.name.firstName","sourceAttribute":"email.email_id","identity":false,"version":0},{"destinationXdmPath":"person.name.lastName","sourceAttribute":"email.activity.action","identity":false,"version":0}]` |
| `mappingId` | ID único que corresponde al conjunto de asignaciones. | `bf5286a9c1ad4266baca76ba3adc9366` |
| `connectionSpecId` | El ID de especificación de conexión que corresponde con su origen. Este es el identificador que generó después de [crear una nueva especificación de conexión](./create.md). | `2e8580db-6489-4726-96de-e33f5f60295f` |
| `flowSpecificationId` | Identificador de especificación de flujo de `GenericStreamingAEP`. **Este es un valor fijo**. | `e77fde5a-22a8-11ed-861d-0242ac120002` |
| `targetConnectionSpecId` | El ID de conexión de destino del lago de datos donde aterrizan los datos ingeridos. **Este es un valor fijo**. | `c604ff05-7f1a-43c0-8e18-33bf874cb11c` |
| `verifyWatTimeInSecond` | Intervalo de tiempo designado que se debe seguir al comprobar la finalización de una ejecución de flujo. | `40` |
| `startTime` | La hora de inicio designada para el flujo de datos. La hora de inicio debe tener el formato unix time. | `1597784298` |

Una vez que haya proporcionado todas las variables de entorno, puede comenzar a ejecutar la colección usando la interfaz [!DNL Postman]. En la interfaz [!DNL Postman], seleccione los puntos suspensivos (**...**) junto a [!DNL Sources SSSs Verification Collection] y, a continuación, seleccione **Ejecutar colección**.

![ejecutor](../assets/runner.png)

Aparecerá la interfaz [!DNL Runner], lo que le permitirá configurar el orden de ejecución del flujo de datos. Seleccione **Ejecutar colección de verificación de SMS** para ejecutar la colección.

>[!NOTE]
>
>Puede deshabilitar **Eliminar flujo** de la lista de comprobación del orden de ejecución si prefiere usar el panel de supervisión de orígenes en la interfaz de usuario de Experience Platform. Sin embargo, una vez que haya terminado con la prueba, debe asegurarse de que los flujos de prueba se eliminen.

![run-collection](../assets/run-collection.png)

## Prueba del origen mediante la interfaz de usuario

Para probar la fuente en la interfaz de usuario de, vaya al catálogo de fuentes de la zona protegida de su organización en la interfaz de usuario de Experience Platform. Aquí debería ver su nuevo origen en la categoría *Transmisión*.

Ahora que la nueva fuente está disponible en la zona protegida, debe seguir el flujo de trabajo de fuentes para probar las funcionalidades. Para empezar, seleccione **[!UICONTROL Configurar]**.

![Catálogo de orígenes que muestra el nuevo origen de flujo continuo.](../assets/testing/catalog-test.png)

Aparecerá el paso [!UICONTROL Agregar datos]. Para probar que su fuente puede transmitir datos, use el lado izquierdo de la interfaz para cargar [un ejemplo de datos JSON](../assets/testing/raw.json.zip). Una vez cargados los datos, el lado derecho de la interfaz se actualiza a una vista previa de la jerarquía de archivos de los datos. Seleccione **[!UICONTROL Siguiente]** para continuar.

![Paso para agregar datos en el flujo de trabajo de orígenes donde puede cargar y obtener una vista previa de los datos antes de la ingesta.](../assets/testing/add-data-test.png)

La página [!UICONTROL Detalles del flujo de datos] le permite seleccionar si desea utilizar un conjunto de datos existente o uno nuevo. Durante este proceso, también puede configurar los datos para que se incorporen al perfil y habilitar opciones como [!UICONTROL Diagnósticos de error] e [!UICONTROL Ingesta parcial].

Para hacer pruebas, seleccione **[!UICONTROL Nuevo conjunto de datos]** y proporcione un nombre para el conjunto de datos de salida. Durante este paso, también puede proporcionar una descripción opcional para agregar más información al conjunto de datos. A continuación, seleccione un esquema al que asignar con la opción [!UICONTROL Búsqueda avanzada] o desplazándose por la lista de esquemas existentes en el menú desplegable. Una vez seleccionado un esquema, proporcione un nombre y una descripción para el flujo de datos.

Cuando termine, seleccione **[!UICONTROL Siguiente]**.

![Paso de detalle del flujo de datos en el flujo de trabajo de origen.](../assets/testing/dataflow-details-test.png)

Aparecerá el paso [!UICONTROL Mapping], que le proporcionará una interfaz para asignar los campos de origen del esquema de origen a sus campos XDM de destino adecuados en el esquema de destino.

Experience Platform proporciona recomendaciones inteligentes para campos asignados automáticamente en función del esquema o conjunto de datos de destino seleccionado. Puede ajustar manualmente las reglas de asignación para adaptarlas a sus casos de uso. En función de sus necesidades, puede elegir asignar campos directamente o utilizar funciones de preparación de datos para transformar los datos de origen y derivar valores calculados o calculados. Para ver los pasos detallados sobre el uso de la interfaz de asignador y los campos calculados, consulte la [guía de la interfaz de usuario de la preparación de datos](../../../data-prep/ui/mapping.md)

Una vez que los datos de origen estén asignados correctamente, seleccione **[!UICONTROL Siguiente]**.

![Paso de asignación del flujo de trabajo de orígenes.](../assets/testing/mapping-test.png)

Aparece el paso **[!UICONTROL Revisar]**, que le permite revisar el nuevo flujo de datos antes de crearlo. Los detalles se agrupan en las siguientes categorías:

* **[!UICONTROL Conexión]**: muestra el nombre de cuenta, el tipo de origen y otra información específica de la fuente de almacenamiento de nube de streaming que está usando.
* **[!UICONTROL Asignar campos de conjunto de datos y asignación]**: Muestra el conjunto de datos y esquema de destino que está utilizando para el flujo de datos.

Una vez que haya revisado el flujo de datos, seleccione **[!UICONTROL Finalizar]** y espere un poco para que se cree el flujo de datos.

![Paso de revisión del flujo de trabajo de orígenes.](../assets/testing/review-test.png)

Finalmente, debe recuperar el punto final de flujo de datos. Este punto de conexión se utilizará para suscribirse al webhook, lo que permitirá que el origen de flujo se comunique con Experience Platform. Para recuperar el extremo de flujo continuo, vaya a la página [!UICONTROL Actividad de flujo de datos] del flujo de datos que acaba de crear y copie el extremo desde la parte inferior del panel [!UICONTROL Propiedades].

![Punto final de flujo continuo en la actividad del flujo de datos.](../assets/testing/endpoint-test.png)

## Enviar el origen

Una vez que el origen pueda completar todo el flujo de trabajo, puede ponerse en contacto con el representante de Adobe y enviar el origen para que se integre en otras organizaciones de Experience Platform.
