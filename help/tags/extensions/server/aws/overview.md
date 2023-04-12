---
title: Información general sobre la extensión de AWS
description: Obtenga información sobre la extensión de AWS para el reenvío de eventos en Adobe Experience Platform.
exl-id: 826a96aa-2d64-4a8b-88cf-34a0b6c26df5
last-substantial-update: 2022-11-23T00:00:00Z
source-git-commit: 1c417744518a7ac7cfb9c65d6af8219dcbc70d46
workflow-type: tm+mt
source-wordcount: '841'
ht-degree: 4%

---

# [!DNL AWS] información general de la extensión

>[!NOTE]
>
>Adobe Experience Platform Launch se ha convertido en un conjunto de tecnologías de recopilación de datos en Adobe Experience Platform. Como resultado, se han implementado varios cambios terminológicos en la documentación del producto. Consulte el siguiente [documento](../../../term-updates.md) para obtener una referencia consolidada de los cambios terminológicos.

[[!DNL Amazon Web Services] ([!DNL AWS])](https://aws.amazon.com/) es una plataforma de computación en la nube que ofrece una amplia variedad de servicios, como computación distribuida, almacenamiento de bases de datos, entrega de contenido y servicios de integración de software como a-service (SaaS) para administración de la relación con los clientes (CRM) y planificación de recursos empresariales (ERP).

La variable [!DNL AWS] [reenvío de eventos](../../../ui/event-forwarding/overview.md) aprovechamientos de extensión [[!DNL Amazon Kinesis Data Streams]](https://docs.aws.amazon.com/streams/latest/dev/introduction.html) para enviar eventos desde la red perimetral de Adobe Experience Platform a [!DNL AWS] para un procesamiento posterior. Esta guía explica cómo instalar la extensión y utilizar sus capacidades en una regla de reenvío de eventos.

## Requisitos previos

Debe tener un [!DNL AWS] cuenta con una [!DNL Kinesis] flujo de datos para utilizar esta extensión. Si no tiene un flujo de datos preexistente, consulte la [!DNL AWS] documentación sobre [creación de un nuevo flujo de datos mediante el [!DNL AWS] Consola de administración](https://docs.aws.amazon.com/streams/latest/dev/how-do-i-create-a-stream.html).

## Instalación de la extensión {#install}

Para instalar el [!DNL AWS] , vaya a la IU de recopilación de datos o a la IU del Experience Platform y seleccione **[!UICONTROL Reenvío de eventos]** desde el panel de navegación izquierdo. Desde aquí, seleccione una propiedad a la que añadir la extensión o cree una nueva propiedad.

Una vez seleccionada o creada la propiedad deseada, seleccione **[!UICONTROL Extensiones]** en el panel de navegación izquierdo, seleccione **[!UICONTROL Catálogo]** pestaña . Busque la variable [!UICONTROL AWS] tarjeta y, a continuación, seleccione **[!UICONTROL Instalar]**.

![La variable [!UICONTROL Instalar] botón seleccionado para la variable [!UICONTROL AWS] en la interfaz de usuario de la recopilación de datos.](../../../images/extensions/server/aws/install.png)

En la siguiente pantalla, debe proporcionar las credenciales de conexión para su [!DNL AWS] cuenta. Específicamente, debe proporcionar su [!DNL AWS] acceda al ID de clave y a la clave de acceso secreta. Si no conoce estos valores, consulte la [!DNL AWS] documentación sobre [cómo obtener su ID de clave de acceso y clave de acceso secreta](https://docs.aws.amazon.com/powershell/latest/userguide/pstools-appendix-sign-up.html).

![El ID de clave de acceso y la clave de acceso secreta añadidos en la vista de configuración de la extensión.](../../../images/extensions/server/aws/credentials.png)

>[!IMPORTANT]
>
>Se debe adjuntar una directiva de acceso al [!DNL AWS] cuenta utilizada para generar las credenciales de acceso. Esta directiva debe configurarse para conceder derechos de acceso para enviar datos al [!DNL Kinesis] flujo de datos. Consulte **Ejemplo 2** en el [!DNL AWS] documento en [directivas de ejemplo para [!DNL Kinesis Data Streams]](https://docs.aws.amazon.com/streams/latest/dev/controlling-access.html#kinesis-using-iam-examples) para ver cómo se debe definir la directiva.

Cuando termine, seleccione **[!UICONTROL Guardar]** y la extensión está instalada.

## Configuración de una regla de reenvío de eventos {#rule}

Después de instalar la extensión, cree un nuevo reenvío de eventos [regla](../../../ui/managing-resources/rules.md) y configure sus condiciones como desee. Al configurar las acciones para la regla, seleccione la **[!UICONTROL AWS]** extensión y, a continuación, seleccione **[!UICONTROL Envío de datos al flujo de datos de Kinesis]** para el tipo de acción.

![La variable [!UICONTROL Envío de datos al flujo de datos de Kinesis] tipo de acción que se está seleccionando para una regla en la interfaz de usuario de la recopilación de datos.](../../../images/extensions/server/aws/select-action-type.png)

El panel de la derecha se actualiza para mostrar las opciones de configuración de cómo se deben enviar los datos. Específicamente, debe asignar [elementos de datos](../../../ui/managing-resources/data-elements.md) a las distintas propiedades que representan su [!DNL Event Hub] configuración.

![Las opciones de configuración para la variable [!UICONTROL Envío de datos al flujo de datos de Kinesis] tipo de acción que se muestra en la interfaz de usuario.](../../../images/extensions/server/aws/data-stream-details.png)

**[!UICONTROL Detalles del flujo de datos de Kinesis]**

| Entrada | Descripción |
| --- | --- |
| [!UICONTROL Nombre de la emisión] | Nombre de la emisión a la que esta regla de reenvío de eventos enviará registros de datos. |
| [!UICONTROL AWS Region] | La variable [!DNL AWS] región en la que [!DNL Kinesis] se crea el flujo de datos. |
| [!UICONTROL Clave de partición] | La variable [clave de partición](https://docs.aws.amazon.com/streams/latest/dev/key-concepts.html#partition-key) que la extensión utilizará al enviar datos al flujo de datos.<br><br>[!DNL Kinesis Data Streams] divide los registros de datos que pertenecen a una emisión en varios fragmentos. Utiliza la clave de partición que se envía con cada registro de datos para determinar a qué compartido pertenece un registro de datos determinado.<br><br>Una buena clave de partición para distribuir clientes puede ser el número de cliente, ya que es diferente para cada cliente. Una clave de partición deficiente podría ser su código postal porque todos podrían vivir en el mismo área cercana. En general, debe elegir una clave de partición que tenga el rango más alto de valores potenciales diferentes. Consulte la [!DNL AWS] artículo sobre [escalar [!DNL Kinesis] flujos de datos](https://aws.amazon.com/blogs/big-data/under-the-hood-scaling-your-kinesis-data-streams/) para prácticas recomendadas sobre la administración de claves de partición. |

{style="table-layout:auto"}

**[!UICONTROL Datos]**

| Entrada | Descripción |
| --- | --- |
| [!UICONTROL Carga útil] | Este campo contiene los datos que se reenviarán al [!DNL Kinesis] flujo de datos, en formato JSON.<br><br>En el **[!UICONTROL Sin procesar]** , puede pegar el objeto JSON directamente en el campo de texto proporcionado o seleccionar el icono del elemento de datos (![Icono de conjunto de datos](../../../images/extensions/server/aws/data-element-icon.png)) para seleccionar de una lista de elementos de datos existentes para representar la carga útil.<br><br>También puede usar la variable **[!UICONTROL Editor de pares de clave-valor JSON]** para añadir manualmente cada par clave-valor a través de un editor de IU. Cada valor se puede representar mediante una entrada sin procesar, o se puede seleccionar un elemento de datos en su lugar. |

{style="table-layout:auto"}

Cuando termine, seleccione **[!UICONTROL Conservar cambios]** para agregar la acción a la configuración de regla. Cuando esté satisfecho con la regla, seleccione **[!UICONTROL Guardar en biblioteca]**.

Finalmente, publicar un nuevo reenvío de eventos [versión](../../../ui/publishing/builds.md) para activar los cambios en la biblioteca.

## Pasos siguientes

Esta guía trata sobre cómo enviar datos a [!DNL Kinesis Data Streams] usando la variable [!DNL AWS] extensión de reenvío de eventos. Para obtener más información sobre las funcionalidades de reenvío de eventos en Experience Platform, consulte la [información general sobre el reenvío de eventos](../../../ui/event-forwarding/overview.md).
