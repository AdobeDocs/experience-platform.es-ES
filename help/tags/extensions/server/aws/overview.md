---
title: Información general sobre la extensión AWS
description: Obtenga información acerca de la extensión de AWS para reenvío de eventos en Adobe Experience Platform.
exl-id: 826a96aa-2d64-4a8b-88cf-34a0b6c26df5
source-git-commit: b4ff3dbc9c62dceefdf2b842cafa65132dde41fc
workflow-type: tm+mt
source-wordcount: '841'
ht-degree: 4%

---

# [!DNL AWS] información general sobre extensiones

>[!NOTE]
>
>Adobe Experience Platform Launch se ha convertido en un conjunto de tecnologías de recopilación de datos en Adobe Experience Platform. Como resultado, se han implementado varios cambios terminológicos en la documentación del producto. Consulte el siguiente [documento](../../../term-updates.md) para obtener una referencia consolidada de los cambios terminológicos.

[[!DNL Amazon Web Services] ([!DNL AWS])](https://aws.amazon.com/) es una plataforma de computación en la nube que ofrece una amplia variedad de servicios, como computación distribuida, almacenamiento de bases de datos, entrega de contenido y servicios de integración de software como servicio (SaaS) para la administración de la relación con los clientes (CRM) y la planificación de recursos empresariales (ERP).

El [!DNL AWS] [reenvío de eventos](../../../ui/event-forwarding/overview.md) la extensión aprovecha [[!DNL Amazon Kinesis Data Streams]](https://docs.aws.amazon.com/streams/latest/dev/introduction.html) para enviar eventos de Adobe Experience Platform Edge Network a [!DNL AWS] para un procesamiento posterior. Esta guía explica cómo instalar la extensión y utilizar sus funcionalidades en una regla de reenvío de eventos.

## Requisitos previos

Debe tener un [!DNL AWS] cuenta con un existente [!DNL Kinesis] flujo de datos para utilizar esta extensión. Si no tiene un flujo de datos preexistente, consulte la [!DNL AWS] documentación sobre [crear un nuevo flujo de datos utilizando [!DNL AWS] Consola de administración](https://docs.aws.amazon.com/streams/latest/dev/how-do-i-create-a-stream.html).

## Instalación de la extensión {#install}

Para instalar el [!DNL AWS] extensión, vaya a la IU de recopilación de datos o a la IU del Experience Platform y seleccione **[!UICONTROL Reenvío de eventos]** en el panel de navegación izquierdo. Aquí, seleccione una propiedad a la que añadir la extensión o cree una nueva propiedad.

Una vez seleccionada o creada la propiedad deseada, seleccione **[!UICONTROL Extensiones]** en el panel de navegación izquierdo, seleccione la opción **[!UICONTROL Catálogo]** pestaña. Busque la variable [!UICONTROL AWS] y, a continuación, seleccione **[!UICONTROL Instalar]**.

![El [!UICONTROL Instalar] botón seleccionado para la [!UICONTROL AWS] en la IU de recopilación de datos.](../../../images/extensions/server/aws/install.png)

En la pantalla siguiente, debe proporcionar las credenciales de conexión para su [!DNL AWS] cuenta. Específicamente, debe proporcionar su [!DNL AWS] ID de clave de acceso y clave de acceso secreta. Si no conoce estos valores, consulte la [!DNL AWS] documentación sobre [cómo obtener el ID de la clave de acceso y la clave de acceso secreta](https://docs.aws.amazon.com/powershell/latest/userguide/pstools-appendix-sign-up.html).

![El ID de clave de acceso y la clave de acceso secreta añadidas en la vista de configuración de la extensión.](../../../images/extensions/server/aws/credentials.png)

>[!IMPORTANT]
>
>Debe adjuntarse una política de acceso a la [!DNL AWS] cuenta utilizada para generar las credenciales de acceso. Esta directiva debe configurarse para conceder derechos de acceso para enviar datos a [!DNL Kinesis] flujo de datos. Consulte **Ejemplo 2** en el [!DNL AWS] documento en [políticas de ejemplo para [!DNL Kinesis Data Streams]](https://docs.aws.amazon.com/streams/latest/dev/controlling-access.html#kinesis-using-iam-examples) para ver cómo se debe definir la directiva.

Cuando termine, seleccione **[!UICONTROL Guardar]** y se instala la extensión de.

## Configuración de una regla de reenvío de eventos {#rule}

Después de instalar la extensión, cree un nuevo reenvío de eventos [regla](../../../ui/managing-resources/rules.md) y configure sus condiciones como desee. Al configurar las acciones de la regla, seleccione **[!UICONTROL AWS]** extensión y seleccione **[!UICONTROL Enviar datos al flujo de datos de Kinesis]** para el tipo de acción.

![El [!UICONTROL Enviar datos al flujo de datos de Kinesis] Tipo de acción seleccionado para una regla de la IU de recopilación de datos.](../../../images/extensions/server/aws/select-action-type.png)

El panel derecho se actualiza para mostrar las opciones de configuración de cómo se deben enviar los datos. Específicamente, debe asignar [elementos de datos](../../../ui/managing-resources/data-elements.md) a las distintas propiedades que representan su [!DNL Event Hub] configuración.

![Las opciones de configuración de [!UICONTROL Enviar datos al flujo de datos de Kinesis] tipo de acción que se muestra en la IU.](../../../images/extensions/server/aws/data-stream-details.png)

**[!UICONTROL Detalles del flujo de datos de Kinesis]**

| Entrada | Descripción |
| --- | --- |
| [!UICONTROL Nombre del flujo] | Nombre del flujo al que esta regla de reenvío de eventos enviará registros de datos. |
| [!UICONTROL AWS Region] | El [!DNL AWS] región donde el [!DNL Kinesis] se crea el flujo de datos. |
| [!UICONTROL Clave de partición] | El [clave de partición](https://docs.aws.amazon.com/streams/latest/dev/key-concepts.html#partition-key) que la extensión utilizará al enviar datos al flujo de datos.<br><br>[!DNL Kinesis Data Streams] separa los registros de datos que pertenecen a una secuencia en varios fragmentos. Utiliza la clave de partición que se envía con cada registro de datos para determinar a qué recurso compartido pertenece un registro de datos determinado.<br><br>Una buena clave de partición para distribuir clientes puede ser el número de cliente, ya que es diferente para cada cliente. Una clave de partición deficiente puede afectar a su código postal porque todos pueden vivir en la misma zona cercana. En general, debe elegir una clave de partición que tenga el rango más alto de diferentes valores potenciales. Consulte la [!DNL AWS] artículo sobre [escalar su [!DNL Kinesis] flujos de datos](https://aws.amazon.com/blogs/big-data/under-the-hood-scaling-your-kinesis-data-streams/) para conocer las prácticas recomendadas sobre la administración de claves de partición. |

{style="table-layout:auto"}

**[!UICONTROL Datos]**

| Entrada | Descripción |
| --- | --- |
| [!UICONTROL Carga útil] | Este campo contiene los datos que se reenviarán al [!DNL Kinesis] flujo de datos, en formato JSON.<br><br>En el **[!UICONTROL Raw]** , puede pegar el objeto JSON directamente en el campo de texto proporcionado o puede seleccionar el icono de elemento de datos (![Icono de conjunto de datos](../../../images/extensions/server/aws/data-element-icon.png)) para seleccionar de una lista de elementos de datos existentes para representar la carga útil.<br><br>También puede utilizar la variable **[!UICONTROL Editor de pares de clave-valor JSON]** para agregar manualmente cada par clave-valor a través de un editor de interfaz de usuario. Cada valor se puede representar mediante una entrada sin procesar o se puede seleccionar un elemento de datos en su lugar. |

{style="table-layout:auto"}

Cuando termine, seleccione **[!UICONTROL Conservar cambios]** para añadir la acción a la configuración de regla. Cuando esté satisfecho con la regla, seleccione **[!UICONTROL Guardar en biblioteca]**.

Por último, publique un nuevo reenvío de eventos [generar](../../../ui/publishing/builds.md) para habilitar los cambios en la biblioteca.

## Pasos siguientes

En esta guía se explica cómo enviar datos a [!DNL Kinesis Data Streams] uso del [!DNL AWS] extensión de reenvío de eventos. Para obtener más información sobre las funcionalidades de reenvío de eventos en Experience Platform, consulte la [resumen del reenvío de eventos](../../../ui/event-forwarding/overview.md).
