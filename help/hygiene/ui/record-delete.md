---
title: Registrar solicitudes de eliminación (flujo de trabajo de IU)
description: Obtenga información sobre cómo eliminar registros en la interfaz de usuario de Adobe Experience Platform.
exl-id: 5303905a-9005-483e-9980-f23b3b11b1d9
source-git-commit: 9ee5225c7494c28023c26181dfe626780133bb5d
workflow-type: tm+mt
source-wordcount: '1848'
ht-degree: 7%

---

# Registrar solicitudes de eliminación (flujo de trabajo de IU) {#record-delete}

Use el espacio de trabajo [[!UICONTROL Ciclo de vida de datos]](./overview.md) para eliminar registros en Adobe Experience Platform según sus identidades principales. Estos registros se pueden asociar a consumidores individuales o a cualquier otra entidad que se incluya en el gráfico de identidad.

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

Para iniciar el proceso, seleccione **[!UICONTROL Ciclo de vida de datos]** en la navegación izquierda de la interfaz de usuario de Experience Platform. Aparece el área de trabajo [!UICONTROL Solicitudes del ciclo de vida de datos]. A continuación, seleccione **[!UICONTROL Crear solicitud]** de la página principal del área de trabajo.

![El espacio de trabajo [!UICONTROL Solicitudes del ciclo de vida de datos] con [!UICONTROL Crear solicitud] seleccionada.](../images/ui/record-delete/create-request-button.png)

Aparecerá el flujo de trabajo de creación de solicitudes. De manera predeterminada, la opción **[!UICONTROL Eliminar registro]** está seleccionada en la sección **[!UICONTROL Acción solicitada]**. Deje seleccionada esta opción.

>[!IMPORTANT]
> 
>Para mejorar la eficacia y reducir el coste de las operaciones de los conjuntos de datos, las organizaciones que se han trasladado al formato Delta pueden eliminar datos del servicio de identidad, del perfil del cliente en tiempo real y del lago de datos. Este tipo de usuario se denomina migración delta. Los usuarios de organizaciones que se han migrado de forma delta pueden elegir eliminar registros de uno o de todos los conjuntos de datos. Los usuarios de organizaciones que no se han sometido a la migración delta no pueden eliminar selectivamente registros de un único conjunto de datos o de todos ellos, como se muestra en la siguiente imagen. En este caso, continúe a la sección [Proporcionar identidades](#provide-identities) de la guía.

![Flujo de trabajo de creación de solicitudes con la opción [!UICONTROL Eliminar registro] seleccionada y resaltada.](../images/ui/record-delete/delete-record.png)

## Seleccionar conjuntos de datos {#select-dataset}

El siguiente paso es determinar si desea eliminar registros de un único conjunto de datos o de todos ellos. Según la configuración de su organización, es posible que la opción de selección de conjuntos de datos no esté disponible. Si no ve esta opción, continúe a la sección [Proporcionar identidades](#provide-identities) de la guía.

En la sección **[!UICONTROL Detalles del registro]**, seleccione un botón de opción para elegir un conjunto de datos específico o todos los conjuntos de datos.

Para eliminar de un conjunto de datos específico, seleccione **[!UICONTROL Seleccionar conjunto de datos]** y, a continuación, seleccione el icono de base de datos (![El icono de base de datos](/help/images/icons/database.png)). En el cuadro de diálogo que aparece, elija un conjunto de datos y seleccione **[!UICONTROL Listo]** para confirmar.

![Cuadro de diálogo [!UICONTROL Seleccionar conjunto de datos] con un conjunto de datos seleccionado y [!UICONTROL Listo] resaltado.](../images/ui/record-delete/select-dataset.png)

Para eliminar de todos los conjuntos de datos, seleccione **[!UICONTROL Todos los conjuntos de datos]**. Esta opción aumenta el ámbito de la operación y requiere que proporcione todos los tipos de identidad relevantes.

![Cuadro de diálogo [!UICONTROL Seleccionar conjunto de datos] con la opción [!UICONTROL Todos los conjuntos de datos] seleccionada.](../images/ui/record-delete/all-datasets.png)

>[!WARNING]
>
>Al seleccionar **[!UICONTROL Todos los conjuntos de datos]**, se expande la operación a todos los conjuntos de datos de su organización. Cada conjunto de datos puede utilizar un tipo de identidad principal diferente. Debe proporcionar **todos los tipos de identidad** necesarios para garantizar una coincidencia precisa.
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
>Si no conoce el área de nombres de identidad de un conjunto de datos concreto, puede encontrarla en la interfaz de usuario de Experience Platform. En el área de trabajo **[!UICONTROL Conjuntos de datos]**, seleccione el conjunto de datos en cuestión en la lista. En la página de detalles del conjunto de datos, pase el ratón sobre el nombre del esquema del conjunto de datos en el carril derecho. El área de nombres de identidad se muestra junto con el nombre y la descripción del esquema.
>
>![El panel Conjuntos de datos con un conjunto de datos seleccionado y un cuadro de diálogo de esquema abierto desde el panel de detalles del conjunto de datos. El identificador principal del conjunto de datos está resaltado.](../images/ui/record-delete/dataset-primary-identity.png)

Existen dos opciones para proporcionar identidades al eliminar registros:

* [Cargar un archivo JSON](#upload-json)
* [Introduzca manualmente los valores de identidad principales](#manual-identity)

### Cargar un archivo JSON {#upload-json}

Para cargar un archivo JSON, puede arrastrar y soltar el archivo en el área proporcionada o seleccionar **[!UICONTROL Elegir archivos]** para examinar y seleccionar en el directorio local.

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

Para escribir identidades manualmente, seleccione **[!UICONTROL Agregar identidad]**.

![Flujo de trabajo de creación de solicitud con la opción [!UICONTROL Agregar identidad] resaltada.](../images/ui/record-delete/add-identity.png)

Aparecen controles que permiten introducir las identidades de una en una. En **[!UICONTROL área de nombres de identidad]**, utilice el menú desplegable para seleccionar el tipo de identidad. En **[!UICONTROL Valor de identidad principal]**, proporcione el valor del área de nombres de identidad para el registro.

![Flujo de trabajo de creación de solicitudes con un campo de identidad agregado manualmente.](../images/ui/record-delete/identity-added.png)

Para agregar más identidades, seleccione el icono más (![Un icono más.](/help/images/icons/tree-expand-all.png)) junto a una de las filas o seleccione **[!UICONTROL Agregar identidad]**.

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

Una vez que haya terminado de agregar identidades a la solicitud, en **[!UICONTROL Configuración de solicitud]**, proporcione un nombre y una descripción opcional para la solicitud antes de seleccionar **[!UICONTROL Enviar]**.

>[!TIP]
>
>Puede enviar hasta 10 000 identidades por solicitud a través de la interfaz de usuario. Para enviar volúmenes más grandes (hasta 100 000 ID por solicitud), usa el [método API](../api/workorder.md#create).

![Los campos [!UICONTROL Nombre] y [!UICONTROL Descripción] de la configuración de la solicitud con [!UICONTROL Enviar] resaltados.](../images/ui/record-delete/submit.png)

Aparece un cuadro de diálogo [!UICONTROL Confirmar solicitud] para indicar que las identidades no se pueden recuperar una vez eliminadas. Seleccione **[!UICONTROL Enviar]** para confirmar la lista de identidades cuyos datos desea eliminar.

![Cuadro de diálogo [!UICONTROL Confirmar solicitud].](../images/ui/record-delete/confirm-request.png)

Una vez enviada la solicitud, se crea una orden de trabajo que aparece en la pestaña [!UICONTROL Registro] del área de trabajo [!UICONTROL Ciclo de vida de datos]. Desde aquí puede supervisar el estado de la orden de trabajo a medida que procesa la solicitud.

>[!NOTE]
>
>Consulte la sección de información general sobre [cronologías y transparencia](../home.md#record-delete-transparency) para obtener detalles sobre cómo se procesan las eliminaciones de registros una vez que se ejecutan.

![La ficha [!UICONTROL Registro] del área de trabajo [!UICONTROL Ciclo de vida de datos] con la nueva solicitud resaltada.](../images/ui/record-delete/request-log.png)

## Pasos siguientes

En este documento se explica cómo eliminar registros en la interfaz de usuario de Experience Platform. Para obtener información sobre cómo realizar otras tareas de administración del ciclo de vida de datos en la interfaz de usuario, consulte [Información general sobre la IU del ciclo de vida de datos](./overview.md).

Para obtener información sobre cómo eliminar registros mediante la API de higiene de datos, consulte la [guía de extremo de orden de trabajo](../api/workorder.md).
