---
title: Información general sobre la extensión AWS
description: Obtenga información acerca de la extensión de AWS para reenvío de eventos en Adobe Experience Platform.
exl-id: 826a96aa-2d64-4a8b-88cf-34a0b6c26df5
last-substantial-update: 2022-11-23T00:00:00Z
source-git-commit: c2832821ea6f9f630e480c6412ca07af788efd66
workflow-type: tm+mt
source-wordcount: '810'
ht-degree: 4%

---

# Información general sobre la extensión [!DNL AWS]

>[!NOTE]
>
>Adobe Experience Platform Launch se ha convertido en un conjunto de tecnologías de recopilación de datos en Adobe Experience Platform. Como resultado, se han implementado varios cambios terminológicos en la documentación del producto. Consulte el siguiente [documento](../../../term-updates.md) para obtener una referencia consolidada de los cambios terminológicos.

[[!DNL Amazon Web Services] ([!DNL AWS])](https://aws.amazon.com/) es una plataforma de computación en la nube que ofrece una amplia variedad de servicios, como computación distribuida, almacenamiento de bases de datos, entrega de contenido y servicios de integración de software como servicio (SaaS) para la administración de la relación con los clientes (CRM) y la planificación de recursos empresariales (ERP).

La extensión [!DNL AWS] [reenvío de eventos](../../../ui/event-forwarding/overview.md) aprovecha [[!DNL Amazon Kinesis Data Streams]](https://docs.aws.amazon.com/streams/latest/dev/introduction.html) para enviar eventos del Edge Network de Adobe Experience Platform a [!DNL AWS] para un procesamiento posterior. Esta guía explica cómo instalar la extensión y utilizar sus funcionalidades en una regla de reenvío de eventos.

## Requisitos previos

Debe tener una cuenta de [!DNL AWS] con un flujo de datos de [!DNL Kinesis] existente para poder usar esta extensión. Si no tiene un flujo de datos preexistente, consulte la documentación de [!DNL AWS] sobre [creación de un nuevo flujo de datos con la [!DNL AWS] consola de administración](https://docs.aws.amazon.com/streams/latest/dev/how-do-i-create-a-stream.html).

## Instalación de la extensión {#install}

Para instalar la extensión [!DNL AWS], vaya a la IU de recopilación de datos o a la IU del Experience Platform y seleccione **[!UICONTROL Reenvío de eventos]** en el panel de navegación izquierdo. Aquí, seleccione una propiedad a la que añadir la extensión o cree una nueva propiedad.

Una vez que haya seleccionado o creado la propiedad deseada, seleccione **[!UICONTROL Extensiones]** en el panel de navegación izquierdo y, a continuación, seleccione la pestaña **[!UICONTROL Catálogo]**. Busque la tarjeta [!UICONTROL AWS] y, a continuación, seleccione **[!UICONTROL Instalar]**.

![Se está seleccionando el botón [!UICONTROL Instalar] para la extensión [!UICONTROL AWS] en la IU de recopilación de datos.](../../../images/extensions/server/aws/install.png)

En la pantalla siguiente, debe proporcionar las credenciales de conexión de la cuenta de [!DNL AWS]. Específicamente, debe proporcionar su clave de acceso [!DNL AWS] y su clave de acceso secreta. Si no conoce estos valores, consulte la documentación de [!DNL AWS] sobre [cómo obtener el identificador de clave de acceso y la clave de acceso secreta](https://docs.aws.amazon.com/powershell/latest/userguide/pstools-appendix-sign-up.html).

![El identificador de clave de acceso y la clave de acceso secreta se agregaron en la vista de configuración de la extensión.](../../../images/extensions/server/aws/credentials.png)

>[!IMPORTANT]
>
>Se debe adjuntar una directiva de acceso a la cuenta de [!DNL AWS] utilizada para generar las credenciales de acceso. Esta directiva debe configurarse para conceder derechos de acceso para enviar datos al flujo de datos de [!DNL Kinesis]. Consulte **Ejemplo 2** en el documento [!DNL AWS] sobre [directivas de ejemplo para [!DNL Kinesis Data Streams]](https://docs.aws.amazon.com/streams/latest/dev/controlling-access.html#kinesis-using-iam-examples) para ver cómo se debe definir la directiva.

Cuando termine, seleccione **[!UICONTROL Guardar]** y la extensión estará instalada.

## Configuración de una regla de reenvío de eventos {#rule}

Después de instalar la extensión, cree una nueva regla de reenvío de eventos [rule](../../../ui/managing-resources/rules.md) y configure sus condiciones como desee. Al configurar las acciones de la regla, seleccione la extensión **[!UICONTROL AWS]** y, a continuación, seleccione **[!UICONTROL Enviar datos al flujo de datos de Kinesis]** para el tipo de acción.

![Se está seleccionando el tipo de acción [!UICONTROL Enviar datos a la secuencia de datos de Kinesis] para una regla en la IU de recopilación de datos.](../../../images/extensions/server/aws/select-action-type.png)

El panel derecho se actualiza para mostrar las opciones de configuración de cómo se deben enviar los datos. En concreto, debe asignar [elementos de datos](../../../ui/managing-resources/data-elements.md) a las distintas propiedades que representan su configuración de [!DNL Event Hub].

![Las opciones de configuración para el tipo de acción [!UICONTROL Enviar datos a la secuencia de datos de Kinesis] que se muestra en la interfaz de usuario.](../../../images/extensions/server/aws/data-stream-details.png)

**[!UICONTROL Detalles del flujo de datos de Kinesis]**

| Entrada | Descripción |
| --- | --- |
| [!UICONTROL Nombre de secuencia] | Nombre del flujo al que esta regla de reenvío de eventos enviará registros de datos. |
| [!UICONTROL AWS Region] | Región [!DNL AWS] donde se crea el flujo de datos [!DNL Kinesis]. |
| [!UICONTROL Clave de partición] | La [clave de partición](https://docs.aws.amazon.com/streams/latest/dev/key-concepts.html#partition-key) que la extensión usará al enviar datos al flujo de datos.<br><br>[!DNL Kinesis Data Streams] separa los registros de datos que pertenecen a una secuencia en varios fragmentos. Utiliza la clave de partición que se envía con cada registro de datos para determinar a qué recurso compartido pertenece un registro de datos determinado.<br><br>Una buena clave de partición para distribuir clientes puede ser el número de cliente, ya que es diferente para cada cliente. Una clave de partición deficiente puede afectar a su código postal porque todos pueden vivir en la misma zona cercana. En general, debe elegir una clave de partición que tenga el rango más alto de diferentes valores potenciales. Consulte el artículo de [!DNL AWS] sobre [escalar los flujos de datos [!DNL Kinesis] 3} para conocer las prácticas recomendadas sobre la administración de claves de partición.](https://aws.amazon.com/blogs/big-data/under-the-hood-scaling-your-kinesis-data-streams/) |

{style="table-layout:auto"}

**[!UICONTROL Datos]**

| Entrada | Descripción |
| --- | --- |
| [!UICONTROL Carga] | Este campo contiene los datos que se reenviarán al flujo de datos [!DNL Kinesis], en formato JSON.<br><br>En la opción **[!UICONTROL Sin procesar]**, puede pegar el objeto JSON directamente en el campo de texto proporcionado o puede seleccionar el icono del elemento de datos (![Icono del conjunto de datos](/help/images/icons/database.png)) para seleccionarlo de una lista de elementos de datos existentes para representar la carga útil.<br><br>También puede usar la opción **[!UICONTROL Editor de pares clave-valor de JSON]** para agregar manualmente cada par clave-valor a través de un editor de interfaz de usuario. Cada valor se puede representar mediante una entrada sin procesar o se puede seleccionar un elemento de datos en su lugar. |

{style="table-layout:auto"}

Cuando termine, seleccione **[!UICONTROL Conservar cambios]** para agregar la acción a la configuración de regla. Cuando esté satisfecho con la regla, seleccione **[!UICONTROL Guardar en biblioteca]**.

Por último, publique un nuevo reenvío de eventos [build](../../../ui/publishing/builds.md) para habilitar los cambios en la biblioteca.

## Pasos siguientes

Esta guía explica cómo enviar datos a [!DNL Kinesis Data Streams] mediante la extensión de reenvío de eventos [!DNL AWS]. Para obtener más información sobre las funcionalidades de reenvío de eventos en Experience Platform, consulte la [descripción general del reenvío de eventos](../../../ui/event-forwarding/overview.md).
