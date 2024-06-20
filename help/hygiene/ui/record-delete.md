---
title: Eliminar registros
description: Obtenga información sobre cómo eliminar registros en la interfaz de usuario de Adobe Experience Platform.
badgeBeta: label="Beta" type="Informative"
exl-id: 5303905a-9005-483e-9980-f23b3b11b1d9
source-git-commit: 9981f35732b041a92c5a371e727a8facb6636cf5
workflow-type: tm+mt
source-wordcount: '1567'
ht-degree: 8%

---

# Eliminación de registros {#record-delete}

Utilice el [[!UICONTROL Ciclo de datos] workspace](./overview.md) para eliminar registros en Adobe Experience Platform según sus identidades principales. Estos registros se pueden asociar a consumidores individuales o a cualquier otra entidad que se incluya en el gráfico de identidad.

>[!IMPORTANT]
> 
>La función de eliminación de registros está actualmente en versión beta y solo está disponible en un **versión limitada**. No está disponible para todos los clientes. Las solicitudes de eliminación de registros solo están disponibles para organizaciones en la versión limitada.
> 
> 
>Las eliminaciones de registros están pensadas para utilizarse para limpiar, eliminar datos anónimos o minimizar datos. Lo son **no** para su uso en solicitudes de derechos de titulares de los datos (cumplimiento) relacionadas con regulaciones de privacidad como el Reglamento General de Protección de Datos (RGPD). Para todos los casos de uso de conformidad, utilice [Adobe Experience Platform Privacy Service](../../privacy-service/home.md) en su lugar.

## Requisitos previos {#prerequisites}

La eliminación de registros requiere una comprensión práctica del funcionamiento de los campos de identidad en Experience Platform. Específicamente, debe conocer los valores del área de nombres de identidad de las entidades cuyos registros desea eliminar, según el conjunto de datos (o conjuntos de datos) desde el que los elimine.

Consulte la siguiente documentación para obtener más información sobre las identidades en Platform:

* [Servicio de identidad de Adobe Experience Platform](../../identity-service/home.md): vincula identidades entre dispositivos y sistemas, vinculando conjuntos de datos en función de los campos de identidad definidos por los esquemas XDM a los que se ajustan.
* [Áreas de nombres de identidad](../../identity-service/features/namespaces.md): las áreas de nombres de identidad definen los diferentes tipos de información de identidad que pueden relacionarse con una sola persona y son un componente requerido para cada campo de identidad.
* [Perfil del cliente en tiempo real](../../profile/home.md): Utiliza gráficos de identidad para proporcionar perfiles de consumidor unificados basados en datos agregados de varias fuentes, actualizados en tiempo casi real.
* [Modelo de datos de experiencia (XDM)](../../xdm/home.md): Proporciona definiciones y estructuras estándar para datos de Platform mediante el uso de esquemas. Todos los conjuntos de datos de Platform se ajustan a un esquema XDM específico y el esquema define qué campos son identidades.
* [Campos de identidad](../../xdm/ui/fields/identity.md): Descubra cómo se define un campo de identidad en un esquema XDM.

## Creación de una solicitud {#create-request}

Para iniciar el proceso, seleccione **[!UICONTROL Ciclo de datos]** en la navegación izquierda de la interfaz de usuario de Platform. El [!UICONTROL Solicitudes de ciclo vital de datos] espacio de trabajo. A continuación, seleccione **[!UICONTROL Crear solicitud]** en la página principal del espacio de trabajo.

![El [!UICONTROL Solicitudes de ciclo vital de datos] workspace con [!UICONTROL Crear solicitud] seleccionados.](../images/ui/record-delete/create-request-button.png)

Aparecerá el flujo de trabajo de creación de solicitudes. De forma predeterminada, la variable **[!UICONTROL Eliminar registro]** La opción está seleccionada en **[!UICONTROL Acción solicitada]** sección. Deje seleccionada esta opción.

>[!IMPORTANT]
> 
>Para mejorar la eficacia y reducir el coste de las operaciones de los conjuntos de datos, las organizaciones que se han trasladado al formato Delta pueden eliminar datos del servicio de identidad, del perfil del cliente en tiempo real y del lago de datos. Este tipo de usuario se denomina migración delta. Los usuarios de organizaciones que se han migrado de forma delta pueden elegir eliminar registros de uno o de todos los conjuntos de datos. Los usuarios de organizaciones que no se han sometido a la migración delta no pueden eliminar selectivamente registros de un único conjunto de datos o de todos ellos, como se muestra en la siguiente imagen. En este caso, continúe con el [Proporcionar identidades](#provide-identities) de la guía.

![El flujo de trabajo de creación de solicitudes con [!UICONTROL Eliminar registro] opción seleccionada y resaltada.](../images/ui/record-delete/delete-record.png)

## Seleccionar conjuntos de datos {#select-dataset}

El siguiente paso es determinar si desea eliminar registros de un único conjunto de datos o de todos ellos. Si esta opción no está disponible para usted, continúe con el [Proporcionar identidades](#provide-identities) de la guía.

En el **[!UICONTROL Detalles de registro]** , utilice el botón de opción para seleccionar entre un conjunto de datos específico y todos los conjuntos de datos. Si elige **[!UICONTROL Seleccionar conjunto de datos]**, proceda a seleccionar el icono de base de datos (![El icono de base de datos](../images/ui/record-delete/database-icon.png)) para abrir un cuadro de diálogo que proporcione una lista de conjuntos de datos disponibles. Seleccione el conjunto de datos deseado de la lista seguido de **[!UICONTROL Listo]**.

![El [!UICONTROL Seleccionar conjunto de datos] diálogo con un conjunto de datos seleccionado y [!UICONTROL Listo] resaltado.](../images/ui/record-delete/select-dataset.png)

Si desea eliminar registros de todos los conjuntos de datos, seleccione **[!UICONTROL Todos los conjuntos de datos]**.

![El [!UICONTROL Seleccionar conjunto de datos] diálogo con el [!UICONTROL Todos los conjuntos de datos] opción seleccionada.](../images/ui/record-delete/all-datasets.png)

>[!NOTE]
>
>Selección de la **[!UICONTROL Todos los conjuntos de datos]** Esta opción puede provocar que la operación de eliminación tarde más y puede no provocar una eliminación precisa del registro.

## Proporcionar identidades {#provide-identities}

>[!CONTEXTUALHELP]
>id="platform_hygiene_primaryidentity"
>title="Espacio de nombres de identidad"
>abstract="Un espacio de nombres de identidad es un atributo que vincula un registro al perfil de un consumidor en Experience Platform. El campo de espacio de nombres de identidad de un conjunto de datos se define mediante el esquema en el que se basa el conjunto de datos. En esta columna, debe proporcionar el tipo (o espacio de nombres) para el espacio de nombres de identidad del registro, como `email` para direcciones de correo electrónico y `ecid` para los ID de Experience Cloud. Para obtener más información, consulte la guía de la interfaz de usuario sobre el ciclo de vida de datos."

>[!CONTEXTUALHELP]
>id="platform_hygiene_identityvalue"
>title="Valor de identidad principal"
>abstract="En esta columna, debe proporcionar el valor del espacio de nombres de identidad del registro, que debe corresponder con el tipo de identidad proporcionado en la columna izquierda. Si el tipo de espacio de nombres de identidad es `email`, el valor debe ser la dirección de correo electrónico del registro. Para obtener más información, consulte la guía de la interfaz de usuario sobre el ciclo de vida de datos."

Al eliminar registros, debe proporcionar información de identidad para que el sistema pueda determinar qué registros se eliminarán. Para cualquier conjunto de datos en Platform, los registros se eliminan en función de la variable **área de nombres de identidad** campo definido por el esquema del conjunto de datos.

Al igual que todos los campos de identidad de Platform, un área de nombres de identidad está compuesta por dos cosas: una **type** (a veces denominado área de nombres de identidad) y una **valor**. El tipo de identidad proporciona contexto sobre cómo el campo identifica un registro (como una dirección de correo electrónico). El valor representa la identidad específica de un registro para ese tipo (por ejemplo, `jdoe@example.com` para el `email` tipo de identidad). Los campos comunes utilizados como identidades incluyen información de la cuenta, ID de dispositivo e ID de cookie.

>[!TIP]
>
>Si no conoce el área de nombres de identidad de un conjunto de datos concreto, puede encontrarla en la interfaz de usuario de Platform. En el **[!UICONTROL Conjuntos de datos]** workspace, seleccione el conjunto de datos en cuestión en la lista. En la página de detalles del conjunto de datos, pase el ratón sobre el nombre del esquema del conjunto de datos en el carril derecho. El área de nombres de identidad se muestra junto con el nombre y la descripción del esquema.
>
>![El panel Conjuntos de datos con un conjunto de datos seleccionado y un cuadro de diálogo de esquema abierto desde el panel de detalles del conjunto de datos. Se resaltará el ID principal del conjunto de datos.](../images/ui/record-delete/dataset-primary-identity.png)

Si elimina registros de un único conjunto de datos, todas las identidades proporcionadas deben tener el mismo tipo, ya que un conjunto de datos solo puede tener un área de nombres de identidad. Si está eliminando de todos los conjuntos de datos, puede incluir varios tipos de identidad, ya que distintos conjuntos de datos pueden tener diferentes identidades principales.

Existen dos opciones para proporcionar identidades al eliminar registros:

* [Cargar un archivo JSON](#upload-json)
* [Introduzca manualmente los valores de identidad principales](#manual-identity)

### Cargar un archivo JSON {#upload-json}

Para cargar un archivo JSON, puede arrastrar y soltar el archivo en el área proporcionada o seleccionar **[!UICONTROL Elegir archivos]** para buscar y seleccionar en el directorio local.

![Flujo de trabajo de creación de solicitudes con la interfaz de elegir archivos y arrastrar y soltar para cargar archivos JSON resaltada.](../images/ui/record-delete/upload-json.png)

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

Una vez cargado el archivo, puede continuar a [enviar la solicitud](#submit).

### Introducir identidades manualmente {#manual-identity}

Para introducir identidades manualmente, seleccione **[!UICONTROL Añadir identidad]**.

![El flujo de trabajo de creación de solicitudes con [!UICONTROL Añadir identidad] opción resaltada.](../images/ui/record-delete/add-identity.png)

Aparecen controles que permiten introducir las identidades de una en una. En **[!UICONTROL área de nombres de identidad]**, utilice el menú desplegable para seleccionar el tipo de identidad. En **[!UICONTROL Valor de identidad principal]**, proporcione el valor del área de nombres de identidad para el registro.

![Flujo de trabajo de creación de solicitudes con un campo de identidad añadido manualmente.](../images/ui/record-delete/identity-added.png)

Para añadir más identidades, seleccione el icono de signo más (![Un icono de signo más.](../images/ui/record-delete/plus-icon.png)) junto a una de las filas o seleccione **[!UICONTROL Añadir identidad]**.

![Flujo de trabajo de creación de la solicitud con el icono más y el icono de añadir identidad resaltados.](../images/ui/record-delete/more-identities.png)

## Enviar la solicitud {#submit}

Una vez que haya terminado de agregar identidades a la solicitud, en **[!UICONTROL Solicitar configuración]**, proporcione un nombre y una descripción opcional para la solicitud antes de seleccionar **[!UICONTROL Enviar]**.

>[!IMPORTANT]
> 
>Existen diferentes límites para el número total de eliminaciones de registros de identidad únicos que se pueden enviar cada mes. Estos límites se basan en el acuerdo de licencia. Las organizaciones que han comprado todas las ediciones de Adobe Real-time Customer Data Platform o Adobe Journey Optimizer pueden enviar hasta 100 000 eliminaciones de registros de identidad cada mes. Organizaciones que han realizado compras **Adobe Healthcare Shield** o **Adobe Escudo de seguridad y privacidad** puede enviar hasta 600 000 eliminaciones de registros de identidad cada mes.<br>Una sola solicitud de eliminación de registro a través de la interfaz de usuario le permite enviar 10 000 ID al mismo tiempo. El [Método de API para eliminar registros](../api/workorder.md#create) permite enviar 100 000 ID al mismo tiempo.<br>Se recomienda enviar tantos ID por solicitud como sea posible, hasta el límite de su ID. Cuando tenga intención de eliminar un gran volumen de ID, debe evitar enviar un bajo volumen o una sola solicitud de eliminación de ID por registro.

![La configuración de la solicitud es [!UICONTROL Nombre] y [!UICONTROL Descripción] campos con [!UICONTROL Enviar] resaltado.](../images/ui/record-delete/submit.png)

A [!UICONTROL Confirmar solicitud] El cuadro de diálogo parece indicar que las identidades no se pueden recuperar una vez eliminadas. Seleccionar **[!UICONTROL Enviar]** para confirmar la lista de identidades cuyos datos desea eliminar.

![El [!UICONTROL Confirmar solicitud] diálogo.](../images/ui/record-delete/confirm-request.png)

Una vez enviada la solicitud, se crea una orden de trabajo y aparece en la [!UICONTROL Registro] de la pestaña [!UICONTROL Ciclo de datos] workspace. Desde aquí puede supervisar el estado de la orden de trabajo a medida que procesa la solicitud.

>[!NOTE]
>
>Consulte la sección de información general sobre [plazos y transparencia](../home.md#record-delete-transparency) para obtener más información sobre cómo se procesan las eliminaciones de registros una vez ejecutadas.

![El [!UICONTROL Registro] de la pestaña [!UICONTROL Ciclo de datos] workspace con la nueva solicitud resaltada.](../images/ui/record-delete/request-log.png)

## Pasos siguientes

Este documento explica cómo eliminar registros en la interfaz de usuario de Experience Platform. Para obtener información sobre cómo realizar otras tareas de administración del ciclo vital de datos en la interfaz de usuario, consulte [Resumen de IU del ciclo vital de datos](./overview.md).

Para obtener información sobre cómo eliminar registros mediante la API de higiene de datos, consulte la [guía de extremo de pedido de trabajo](../api/workorder.md).
