---
title: Registrar solicitudes de eliminación (flujo de trabajo de IU)
description: Obtenga información sobre cómo eliminar registros en la interfaz de usuario de Adobe Experience Platform.
exl-id: 5303905a-9005-483e-9980-f23b3b11b1d9
source-git-commit: 83aed6a79d47ee4043a8303ec8f8c8c20482e12a
workflow-type: tm+mt
source-wordcount: '2383'
ht-degree: 6%

---

# Registrar solicitudes de eliminación (flujo de trabajo de IU) {#record-delete}

Use [[!UICONTROL Data Lifecycle] espacio de trabajo](./overview.md) para eliminar registros en Adobe Experience Platform según sus identidades principales. Estos registros se pueden asociar a consumidores individuales o a cualquier otra entidad que se incluya en el gráfico de identidad.

>[!IMPORTANT]
>
>Las eliminaciones de registros están pensadas para utilizarse para limpiar, eliminar datos anónimos o minimizar datos. Son **no** para usar en solicitudes de derechos de titulares de datos (cumplimiento) relacionadas con normas de privacidad como el Reglamento General de Protección de Datos (RGPD). Para todos los casos de uso de cumplimiento, usa [Adobe Experience Platform Privacy Service](../../privacy-service/home.md) en su lugar.

## Requisitos previos {#prerequisites}

La eliminación de registros requiere una comprensión práctica del funcionamiento de los campos de identidad en Experience Platform. Específicamente, debe conocer los valores del área de nombres de identidad de las entidades cuyos registros desea eliminar, según el conjunto de datos (o conjuntos de datos) desde el que los elimine.

Consulte la siguiente documentación para obtener más información sobre las identidades en Experience Platform:

* [Servicio de identidad de Adobe Experience Platform](../../identity-service/home.md): vincula identidades entre dispositivos y sistemas y vincula conjuntos de datos en función de los campos de identidad definidos por los esquemas XDM a los que se ajustan.
* [Áreas de nombres de identidad](../../identity-service/features/namespaces.md): Las áreas de nombres de identidad definen los diferentes tipos de información de identidad que se pueden relacionar con una sola persona y son un componente necesario para cada campo de identidad.
* [Perfil del cliente en tiempo real](../../profile/home.md): Utiliza gráficos de identidad para proporcionar perfiles de consumidor unificados basados en datos agregados de varias fuentes, actualizados en tiempo casi real.
* [Modelo de datos de experiencia (XDM)](../../xdm/home.md): Proporciona definiciones y estructuras estándar para datos de Experience Platform mediante el uso de esquemas. Todos los conjuntos de datos de Experience Platform se ajustan a un esquema XDM específico y el esquema define qué campos son identidades.
* [Campos de identidad](../../xdm/ui/fields/identity.md): Descubra cómo se define un campo de identidad en un esquema XDM.

## Creación de una solicitud {#create-request}

Para iniciar el proceso, seleccione **[!UICONTROL Data Lifecycle]** en el panel de navegación izquierdo de la interfaz de usuario de Experience Platform. Aparece el área de trabajo [!UICONTROL Data lifecycle requests]. A continuación, seleccione **[!UICONTROL Create request]** de la página principal del área de trabajo.

![El área de trabajo [!UICONTROL Data lifecycle requests] con [!UICONTROL Create request] seleccionado.](../images/ui/record-delete/create-request-button.png)

Aparecerá el flujo de trabajo de creación de solicitudes. De manera predeterminada, la opción **[!UICONTROL Delete record]** está seleccionada en la sección **[!UICONTROL Requested Action]**. Deje seleccionada esta opción.

>[!IMPORTANT]
> 
>Para mejorar la eficacia y reducir el coste de las operaciones de los conjuntos de datos, las organizaciones que se han trasladado al formato Delta pueden eliminar datos del servicio de identidad, del perfil del cliente en tiempo real y del lago de datos. Este tipo de usuario se denomina migración delta. Los usuarios de organizaciones que se han migrado de forma delta pueden elegir eliminar registros de uno o de todos los conjuntos de datos. Los usuarios de organizaciones que no se han sometido a la migración delta no pueden eliminar selectivamente registros de un único conjunto de datos o de todos ellos, como se muestra en la siguiente imagen. En este caso, continúe a la sección [Proporcionar identidades](#provide-identities) de la guía.

![Flujo de trabajo de creación de solicitudes con la opción [!UICONTROL Delete record] seleccionada y resaltada.](../images/ui/record-delete/delete-record.png)

## Seleccionar conjuntos de datos {#select-dataset}

El siguiente paso es determinar si desea eliminar registros de un único conjunto de datos o de todos ellos. Según la configuración de su organización, es posible que la opción de selección de conjuntos de datos no esté disponible. Si no ve esta opción, continúe a la sección [Proporcionar identidades](#provide-identities) de la guía.

En la sección **[!UICONTROL Record Details]**, seleccione un botón de opción para elegir un conjunto de datos específico o todos.

Para eliminar de un conjunto de datos específico, seleccione **[!UICONTROL Select dataset]** y, a continuación, seleccione el icono de base de datos (![El icono de base de datos](/help/images/icons/database.png)). En el cuadro de diálogo que aparece, elija un conjunto de datos y seleccione **[!UICONTROL Done]** para confirmar.

![Cuadro de diálogo [!UICONTROL Select dataset] con un conjunto de datos seleccionado y [!UICONTROL Done] resaltado.](../images/ui/record-delete/select-dataset.png)

Para eliminar de todos los conjuntos de datos, seleccione **[!UICONTROL All datasets]**. Esta opción aumenta el ámbito de la operación y requiere que proporcione todos los tipos de identidad relevantes.

![Cuadro de diálogo [!UICONTROL Select dataset] con la opción [!UICONTROL All datasets] seleccionada.](../images/ui/record-delete/all-datasets.png)

>[!WARNING]
>
>Al seleccionar **[!UICONTROL All datasets]**, se expande la operación a todos los conjuntos de datos de su organización. Cada conjunto de datos puede utilizar un tipo de identidad principal diferente. Debe proporcionar **todos los tipos de identidad** necesarios para garantizar una coincidencia precisa.
>
>Si falta algún tipo de identidad, es posible que algunos registros se omitan durante la eliminación. Esto puede ralentizar el procesamiento y generar **resultados parciales**.

Cada conjunto de datos de Experience Platform solo admite un tipo de identidad principal.

* Al eliminar de **un solo conjunto de datos**, todas las identidades de su solicitud deben usar **el mismo tipo**.
* Al eliminar de **todos los conjuntos de datos**, puede incluir **varios tipos de identidad**, ya que distintos conjuntos de datos pueden depender de identidades principales diferentes&quot;.

## Proporcionar identidades {#provide-identities}

>[!CONTEXTUALHELP]
>id="platform_hygiene_primaryidentity"
>title="Espacio de nombres de identidad"
>abstract="Un espacio de nombres de identidad es un atributo que vincula un registro al perfil de un consumidor en Experience Platform. El campo de espacio de nombres de identidad de un conjunto de datos se define mediante el esquema en el que se basa el conjunto de datos. En esta columna, debe proporcionar el tipo (o espacio de nombres) para el espacio de nombres de identidad del registro, como `email` para direcciones de correo electrónico y `ecid` para los ID de Experience Cloud. Para obtener más información, consulte la guía de la interfaz de usuario sobre el ciclo de vida de datos."

>[!CONTEXTUALHELP]
>id="platform_hygiene_identityvalue"
>title="Valor de identidad principal"
>abstract="En esta columna, debe proporcionar el valor del espacio de nombres de identidad del registro, que debe corresponder con el tipo de identidad proporcionado en la columna izquierda. Si el tipo de espacio de nombres de identidad es `email`, el valor debe ser la dirección de correo electrónico del registro. Para obtener más información, consulte la guía de la interfaz de usuario sobre el ciclo de vida de datos."

Al eliminar registros, debe proporcionar información de identidad para que el sistema pueda determinar qué registros se eliminarán. Para cualquier conjunto de datos en Experience Platform, los registros se eliminan en función del campo **área de nombres de identidad** definido por el esquema del conjunto de datos.

Al igual que todos los campos de identidad de Experience Platform, un área de nombres de identidad consta de dos cosas: un **tipo** (a veces denominado área de nombres de identidad) y un **valor**. El tipo de identidad proporciona contexto sobre cómo el campo identifica un registro (como una dirección de correo electrónico). El valor representa la identidad específica de un registro para ese tipo (por ejemplo, `jdoe@example.com` para el tipo de identidad `email`). Los campos comunes utilizados como identidades incluyen información de la cuenta, ID de dispositivo e ID de cookie.

>[!TIP]
>
>Si no conoce el área de nombres de identidad de un conjunto de datos concreto, puede encontrarla en la interfaz de usuario de Experience Platform. En el área de trabajo **[!UICONTROL Datasets]**, seleccione el conjunto de datos en cuestión en la lista. En la página de detalles del conjunto de datos, pase el ratón sobre el nombre del esquema del conjunto de datos en el carril derecho. El área de nombres de identidad se muestra junto con el nombre y la descripción del esquema.
>
>![El panel Conjuntos de datos con un conjunto de datos seleccionado y un cuadro de diálogo de esquema abierto desde el panel de detalles del conjunto de datos. El identificador principal del conjunto de datos está resaltado.](../images/ui/record-delete/dataset-primary-identity.png)

Existen dos opciones para proporcionar identidades al eliminar registros:

* [Cargar un archivo JSON](#upload-json)
* [Introduzca manualmente los valores de identidad principales](#manual-identity)

### Cargar un archivo JSON {#upload-json}

Para cargar un archivo JSON, puede arrastrar y soltar el archivo en el área proporcionada o seleccionar **[!UICONTROL Choose files]** para examinar y seleccionar en el directorio local.

![Flujo de trabajo de creación de solicitudes con la interfaz de elegir archivos y arrastrar y soltar para cargar archivos JSON resaltados.](../images/ui/record-delete/upload-json.png)

El archivo JSON debe tener el formato de una matriz de objetos; cada objeto representa una identidad.

```json
[
  {
    "namespaceCode": "email",
    "value": "jdoe@example.com"
  },
  {
    "namespaceCode": "email",
    "value": "san.gray@example.com"
  }
]
```

| Propiedad | Descripción |
| --- | --- |
| `namespaceCode` | El tipo de identidad. |
| `value` | El valor de identidad principal indicado por el tipo. |

Una vez cargado el archivo, puede continuar [enviando la solicitud](#submit).

### Introducir identidades manualmente {#manual-identity}

Para introducir identidades manualmente, seleccione **[!UICONTROL Add identity]**.

![Flujo de trabajo de creación de solicitud con la opción [!UICONTROL Add identity] resaltada.](../images/ui/record-delete/add-identity.png)

Aparecen controles que permiten introducir las identidades de una en una. En **[!UICONTROL identity namespace]**, utilice el menú desplegable para seleccionar el tipo de identidad. En **[!UICONTROL Primary Identity Value]**, proporcione el valor del área de nombres de identidad para el registro.

![Flujo de trabajo de creación de solicitudes con un campo de identidad agregado manualmente.](../images/ui/record-delete/identity-added.png)

Para agregar más identidades, seleccione el icono más (![Un icono más.](/help/images/icons/tree-expand-all.png)) junto a una de las filas o seleccione **[!UICONTROL Add identity]**.

![Flujo de trabajo de creación de solicitud con el icono más y el icono de agregar identidad resaltados.](../images/ui/record-delete/more-identities.png)

## Cuotas y plazos de procesamiento {#quotas}

Las solicitudes de eliminación de registros están sujetas a límites diarios y mensuales de envío de identificadores, determinados por el derecho de licencia de su organización. Estos límites se aplican a solicitudes de eliminación basadas en la interfaz de usuario y la API.

>[!NOTE]
>
>Puede enviar hasta **1.000.000 de identificadores por día**, pero solo si la cuota mensual restante lo permite. Si su límite mensual es inferior a 1 millón, sus envíos diarios no pueden exceder ese límite.

### Derecho de envío mensual por producto {#quota-limits}

En la tabla siguiente se describen los límites de envío de identificadores por producto y nivel de asignación de derechos. Para cada producto, el límite mensual es el menor de dos valores: un límite de identificador fijo o un umbral basado en porcentajes y vinculado al volumen de datos con licencia.

| Producto | Descripción del derecho | Límite mensual (el que sea menor) |
|----------|-------------------------|---------------------------------|
| REAL-TIME CDP o ADOBE JOURNEY OPTIMIZER | Sin el complemento Escudo de privacidad y seguridad o Escudo de atención sanitaria | 2 000 000 de identificadores o el 5 % de la audiencia direccionable |
| REAL-TIME CDP o ADOBE JOURNEY OPTIMIZER | Con el complemento Escudo de privacidad y seguridad o Escudo de atención sanitaria | 15 000 000 de identificadores o el 10 % de la audiencia direccionable |
| Customer Journey Analytics | Sin el complemento Escudo de privacidad y seguridad o Escudo de atención sanitaria | 2 000 000 de identificadores o 100 identificadores por millón de filas de CJA de derechos |
| Customer Journey Analytics | Con el complemento Escudo de privacidad y seguridad o Escudo de atención sanitaria | 15 000 000 de identificadores o 200 identificadores por millón de filas de CJA de derechos |

>[!NOTE]
>
> La mayoría de las organizaciones tendrán límites mensuales más bajos en función de su audiencia direccionable real o de los derechos de fila de CJA.

Las cuotas se restablecen el primer día de cada mes calendario. La cuota no utilizada **no** se transfiere.

>[!NOTE]
>
>Las cuotas se basan en los derechos mensuales con licencia de su organización para **identificadores enviados**. Estas no se aplican mediante protecciones del sistema, pero se pueden supervisar y revisar.
>
>La eliminación de registros es un **servicio compartido**. Su límite mensual refleja el derecho más alto en Real-Time CDP, Adobe Journey Optimizer, Customer Journey Analytics y cualquier complemento de Shield aplicable.

### Tiempos de procesamiento para los envíos de identificadores {#sla-processing-timelines}

Después del envío, las solicitudes de eliminación de registros se ponen en cola y se procesan según su nivel de asignación de derechos.

| Descripción del producto y los derechos | Duración de cola | Tiempo máximo de procesamiento (SLA) |
|------------------------------------------------------------------------------------|---------------------|-------------------------------|
| Sin el complemento Escudo de privacidad y seguridad o Escudo de atención sanitaria | Hasta 15 días | 30 días |
| Con el complemento Escudo de privacidad y seguridad o Escudo de atención sanitaria | Normalmente 24 horas | 15 días |

Si su organización requiere límites más altos, póngase en contacto con su representante de Adobe para obtener una revisión de las autorizaciones.

>[!TIP]
>
>Para comprobar el uso actual de la cuota o el nivel de derechos, consulte la [Guía de referencia de cuotas](../api/quota.md).

## Enviar la solicitud {#submit}

Cuando haya terminado de agregar identidades a la solicitud, en **[!UICONTROL Request settings]**, proporcione un nombre y una descripción opcional para la solicitud antes de seleccionar **[!UICONTROL Submit]**.

>[!TIP]
>
>Puede enviar hasta 10 000 identidades por solicitud a través de la interfaz de usuario. Para enviar volúmenes más grandes (hasta 100 000 ID por solicitud), usa el [método API](../api/workorder.md#create).

![Los campos [!UICONTROL Name] y [!UICONTROL Description] de la configuración de la solicitud con [!UICONTROL Submit] resaltados.](../images/ui/record-delete/submit.png)

Aparecerá un cuadro de diálogo [!UICONTROL Confirm request] para indicar que las identidades no se pueden recuperar una vez eliminadas. Seleccione **[!UICONTROL Submit]** para confirmar la lista de identidades cuyos datos desea eliminar.

![Cuadro de diálogo [!UICONTROL Confirm request].](../images/ui/record-delete/confirm-request.png)

Una vez enviada la solicitud, se crea una orden de trabajo y aparece en la ficha [!UICONTROL Record] del área de trabajo [!UICONTROL Data Lifecycle]. Desde aquí puede supervisar el estado de la orden de trabajo a medida que procesa la solicitud.

>[!NOTE]
>
>Consulte la sección de información general sobre [cronologías y transparencia](../home.md#record-delete-transparency) para obtener detalles sobre cómo se procesan las eliminaciones de registros una vez que se ejecutan.

![La ficha [!UICONTROL Record] del área de trabajo [!UICONTROL Data Lifecycle] con la nueva solicitud resaltada.](../images/ui/record-delete/request-log.png)

## Eliminación de registros de conjuntos de datos basados en esquemas relacionales {#relational-record-delete}

Si el conjunto de datos que está eliminando se basa en un esquema relacional, revise las siguientes consideraciones para asegurarse de que los registros se quiten correctamente y no se vuelvan a ingerir debido a discrepancias entre Experience Platform y el sistema de origen.

>[!NOTE]
>
>Los esquemas relacionales se denominaban anteriormente esquemas basados en modelos en versiones anteriores de la documentación de Adobe Experience Platform. La funcionalidad y el comportamiento de eliminación siguen siendo los mismos.

### Comportamiento de eliminación de registros

En la tabla siguiente se describe cómo se comportan las eliminaciones de registros en Experience Platform y en los sistemas de origen, según el método de ingesta y el cambio de la configuración de captura de datos.

| Aspecto | Comportamiento |
|---------------------|--------------------------------------------------------------------------|
| Eliminación de plataforma | Los registros se eliminan del conjunto de datos de Experience Platform y del lago de datos. |
| Retención de Source | Los registros permanecen en el sistema de origen a menos que se eliminen explícitamente allí. |
| Impacto de actualización completa | Si se utiliza la actualización completa, los registros eliminados se pueden volver a ingerir a menos que se quiten o excluyan del origen. |
| Cambio del comportamiento de captura de datos | Los registros marcados con `_change_request_type = 'd'` se eliminan durante la ingesta. Los registros no marcados se pueden volver a ingerir. |

Para evitar la reingesta, aplique el mismo método de eliminación tanto en el sistema de origen como en Experience Platform, ya sea eliminando registros de ambos sistemas o incluyendo `_change_request_type = 'd'` para los registros que desea eliminar.

### Cambiar las columnas de captura y control de datos

Los esquemas relacionales que utilizan orígenes con captura de datos de cambio pueden utilizar la columna de control `_change_request_type` al distinguir eliminaciones de actualizaciones. Durante la ingesta, los registros marcados con `d` se eliminan del conjunto de datos, mientras que los marcados con `u` o sin la columna se tratan como actualizaciones. La columna `_change_request_type` se lee solo en el momento de la ingesta y no se almacena en el esquema de destino ni se asigna a campos XDM.

>[!NOTE]
>
>La eliminación de registros a través de la IU del ciclo vital de datos no afecta al sistema de origen. Para quitar datos de ambas ubicaciones, elimínelos tanto en Experience Platform como en el origen.

### Métodos de eliminación adicionales para esquemas relacionales

Más allá del flujo de trabajo de eliminación de registros estándar, los esquemas relacionales admiten métodos adicionales para casos de uso específicos:

* **Enfoque de conjunto de datos de copia segura**: duplique el conjunto de datos de producción y aplique eliminaciones a la copia para pruebas o reconciliación controladas antes de aplicar cambios a los datos de producción.
* **Carga por lotes de solo eliminación**: cargue un archivo que contenga únicamente operaciones de eliminación para el mantenimiento de destino cuando necesite eliminar registros específicos sin que ello afecte a otros datos.

### Compatibilidad del descriptor con operaciones de higiene {#descriptor-support}

Los descriptores de esquema relacionales proporcionan metadatos esenciales para operaciones de higiene precisas:

* **Descriptor de clave principal**: Identifica registros de forma exclusiva para actualizaciones o eliminaciones de destino, lo que garantiza que los registros correctos se vean afectados.
* **Descriptor de versión**: garantiza que las eliminaciones y actualizaciones se apliquen en el orden cronológico correcto, lo que evita operaciones fuera de secuencia.
* **Descriptor de marca de tiempo (esquemas de series de tiempo)**: alinea las operaciones de eliminación con los tiempos de ocurrencia de eventos en lugar de los tiempos de ingesta.

>[!NOTE]
>
>Los procesos de higiene operan en el nivel del conjunto de datos. Para conjuntos de datos con perfil habilitado, es posible que se requieran flujos de trabajo de perfil adicionales para mantener la coherencia en el perfil del cliente en tiempo real.

### Retención programada para esquemas relacionales

Para obtener una higiene automatizada basada en la edad de los datos y no en identidades específicas, consulte [Administrar la retención del conjunto de datos de evento de experiencia (TTL)](../../catalog/datasets/experience-event-dataset-retention-ttl-guide.md) para obtener información sobre la retención programada en el nivel de fila en el lago de datos.

>[!NOTE]
>
>La caducidad a nivel de fila solo se admite para conjuntos de datos que utilizan el comportamiento de series temporales.

### Prácticas recomendadas para la eliminación de registros relacionales

Para evitar una reingesta involuntaria y mantener la coherencia de los datos en todos los sistemas, siga estas prácticas recomendadas:

* **Coordinar eliminaciones**: alinee las eliminaciones de registros con la configuración de captura de datos de cambio y la estrategia de administración de datos de origen.
* **Monitorizar los flujos de captura de datos modificados**: después de eliminar los registros en Platform, supervise los flujos de datos y confirme que el sistema de origen quita los mismos registros o los incluye con `_change_request_type = 'd'`.
* **Limpiar el origen**: Para los orígenes que usan la ingesta de actualización completa o los que no admiten eliminaciones mediante la captura de datos de cambio, elimine registros directamente del sistema de origen para evitar la reingesta.

Para obtener más información sobre los requisitos de esquema, consulte [requisitos de descriptor de esquema relacional](../../xdm/schema/relational.md#relational-schemas).

Para saber cómo funciona la captura de datos modificados con las fuentes, consulte [Habilitar la captura de datos modificados en las fuentes](../../sources/tutorials/api/change-data-capture.md#using-change-data-capture-with-relational-schemas).

## Próximos pasos

En este documento se explica cómo eliminar registros en la interfaz de usuario de Experience Platform. Para obtener información sobre cómo realizar otras tareas de administración del ciclo de vida de datos en la interfaz de usuario, consulte [Información general sobre la IU del ciclo de vida de datos](./overview.md).

Para obtener información sobre cómo eliminar registros mediante la API de higiene de datos, consulte la [guía de extremo de orden de trabajo](../api/workorder.md).
