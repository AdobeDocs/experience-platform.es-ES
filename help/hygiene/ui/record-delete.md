---
title: Eliminar registros
description: Obtenga información sobre cómo eliminar registros en la interfaz de usuario de Adobe Experience Platform.
exl-id: 5303905a-9005-483e-9980-f23b3b11b1d9
hide: true
hidefromtoc: true
source-git-commit: a20afcd95d47e38ccdec9fba9e772032e212d7a4
workflow-type: tm+mt
source-wordcount: '1184'
ht-degree: 0%

---

# Eliminación de registros

El [[!UICONTROL Higiene de datos] workspace](./overview.md) en la interfaz de usuario de Adobe Experience Platform permite eliminar registros que participan en el servicio de identidad y en el perfil del cliente en tiempo real. Estos registros se pueden asociar a consumidores individuales o a cualquier otra entidad que se incluya en el gráfico de identidad.

>[!IMPORTANT]
>
>Las solicitudes de eliminación de registros solo están disponibles para organizaciones que han realizado compras **Adobe Healthcare Shield**.
>
>
>Las eliminaciones de registros están pensadas para utilizarse para limpiar, eliminar datos anónimos o minimizar datos. Lo son **no** para su uso en solicitudes de derechos de titulares de los datos (cumplimiento) relacionadas con regulaciones de privacidad como el Reglamento General de Protección de Datos (RGPD). Para todos los casos de uso de conformidad, utilice [Adobe Experience Platform Privacy Service](../../privacy-service/home.md) en su lugar.

## Requisitos previos

La eliminación de registros requiere una comprensión práctica del funcionamiento de los campos de identidad en Experience Platform. Específicamente, debe conocer los valores de identidad principales de las entidades cuyos registros desea eliminar, según el conjunto de datos (o conjuntos de datos) desde el que los elimine.

Consulte la siguiente documentación para obtener más información sobre las identidades en Platform:

* [Servicio de identidad de Adobe Experience Platform](../../identity-service/home.md): vincula identidades entre dispositivos y sistemas, vinculando conjuntos de datos en función de los campos de identidad definidos por los esquemas XDM a los que se ajustan.
   * [Áreas de nombres de identidad](../../identity-service/namespaces.md): las áreas de nombres de identidad definen los diferentes tipos de información de identidad que pueden relacionarse con una sola persona y son un componente requerido para cada campo de identidad.
* [Perfil del cliente en tiempo real](../../profile/home.md): aprovecha los gráficos de identidad para proporcionar perfiles de consumidor unificados en función de los datos agregados de varias fuentes, actualizados en tiempo casi real.
* [Modelo de datos de experiencia (XDM)](../../xdm/home.md): Proporciona definiciones y estructuras estándar para datos de Platform mediante el uso de esquemas. Todos los conjuntos de datos de Platform se ajustan a un esquema XDM específico y el esquema define qué campos son identidades.
   * [Campos de identidad](../../xdm/ui/fields/identity.md): Descubra cómo se define un campo de identidad en un esquema XDM.

## Crear una nueva solicitud

Para iniciar el proceso, seleccione **[!UICONTROL Crear solicitud]** en la página principal del espacio de trabajo.

![Imagen que muestra el [!UICONTROL Crear solicitud] botón seleccionado](../images/ui/record-delete/create-request-button.png)

Aparecerá el cuadro de diálogo de creación de solicitudes. De forma predeterminada, la variable **[!UICONTROL Eliminar consumidor]** La opción está seleccionada en **[!UICONTROL Acción solicitada]** sección. Deje seleccionada esta opción.

![Imagen que muestra la opción Eliminar consumidor seleccionada en el cuadro de diálogo de creación](../images/ui/record-delete/consumer-action.png)

## Seleccionar conjuntos de datos

En el **[!UICONTROL Detalles del consumidor]** , el siguiente paso es determinar si desea eliminar registros de un único conjunto de datos o de todos ellos.

Si elige **[!UICONTROL Seleccionar conjunto de datos]**, seleccione el icono de base de datos (![Imagen del icono de la base de datos](../images/ui/record-delete/database-icon.png)) y aparece un cuadro de diálogo que le permite seleccionar el conjunto de datos deseado de la lista.

![Imagen que muestra el cuadro de diálogo de selección del conjunto de datos](../images/ui/record-delete/select-dataset.png)

Si desea eliminar registros de todos los conjuntos de datos, seleccione **[!UICONTROL Todos los conjuntos de datos]**.

![Imagen que muestra el [!UICONTROL Todos los conjuntos de datos] opción seleccionada](../images/ui/record-delete/all-datasets.png)

>[!NOTE]
>
>Selección de la **[!UICONTROL Todos los conjuntos de datos]** Esta opción puede provocar que la operación de eliminación tarde más y puede no provocar una eliminación precisa del registro.

## Proporcionar identidades {#provide-identities}

>[!CONTEXTUALHELP]
>id="platform_hygiene_primaryidentity"
>title="Identidad principal"
>abstract="Una identidad principal es un atributo que vincula un registro al perfil de un consumidor en Experience Platform. El campo de identidad principal de un conjunto de datos se define mediante el esquema en el que se basa el conjunto de datos. En esta columna, debe proporcionar el tipo (o área de nombres) para la identidad principal del registro, como `email` para direcciones de correo electrónico y `ecid` para ID de Experience Cloud. Para obtener más información, consulte la guía de la IU de higiene de datos."

>[!CONTEXTUALHELP]
>id="platform_hygiene_identityvalue"
>title="Valor de identidad"
>abstract="En esta columna, debe proporcionar el valor de la identidad principal del registro, que debe corresponder al tipo de identidad proporcionado en la columna izquierda. Si el tipo de identidad principal es `email`, el valor debe ser la dirección de correo electrónico del registro. Para obtener más información, consulte la guía de la interfaz de usuario sobre higiene de datos."

Al eliminar registros, debe proporcionar información de identidad para que el sistema pueda determinar qué registros deben eliminarse. Para cualquier conjunto de datos en Platform, los registros se eliminan en función de la variable **identidad principal** campo definido por el esquema del conjunto de datos.

Al igual que todos los campos de identidad de Platform, una identidad principal se compone de dos cosas: una **type** (a veces denominado área de nombres de identidad) y una **valor**. El tipo de identidad proporciona contexto sobre cómo el campo identifica un registro (como una dirección de correo electrónico) y el valor representa la identidad específica de un registro para ese tipo (por ejemplo, `jdoe@example.com` para el `email` tipo de identidad). Los campos comunes utilizados como identidades incluyen información de la cuenta, ID de dispositivo e ID de cookie.

>[!TIP]
>
>Si no conoce la identidad principal de un conjunto de datos concreto, puede encontrarla en la interfaz de usuario de Platform. En el **[!UICONTROL Conjuntos de datos]** workspace, seleccione el conjunto de datos en cuestión en la lista. En la página de detalles del conjunto de datos, pase el ratón sobre el nombre del esquema del conjunto de datos en el carril derecho. La identidad principal se muestra junto con el nombre y la descripción del esquema.
>
>![Imagen que muestra la identidad principal de un conjunto de datos resaltado en la IU](../images/ui/record-delete/dataset-primary-identity.png)

Si elimina registros de un único conjunto de datos, todas las identidades proporcionadas deben tener el mismo tipo, ya que un conjunto de datos solo puede tener una identidad principal. Si está eliminando de todos los conjuntos de datos, puede incluir varios tipos de identidad, ya que distintos conjuntos de datos pueden tener diferentes identidades principales.

Existen dos opciones para proporcionar identidades al eliminar registros:

* [Cargar un archivo JSON](#upload-json)
* [Introducir valores de identidad manualmente](#manual-identity)

### Cargar un archivo JSON {#upload-json}

Para cargar un archivo JSON, puede arrastrar y soltar el archivo en el área proporcionada o seleccionar **[!UICONTROL Elegir archivos]** para buscar y seleccionar en el directorio local.

![Imagen que muestra los métodos para cargar JSON en la interfaz de usuario](../images/ui/record-delete/upload-json.png)

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
| `value` | El valor de identidad indicado por el tipo. |

Una vez cargado el archivo, puede continuar a [enviar la solicitud](#submit).

### Introducir identidades manualmente {#manual-identity}

Para introducir identidades manualmente, seleccione **[!UICONTROL Añadir identidad]**.

![Imagen que muestra el [!UICONTROL Añadir identidad] botón seleccionado](../images/ui/record-delete/add-identity.png)

Aparecen controles que permiten introducir las identidades de una en una. En **[!UICONTROL Identidad principal]**, utilice el menú desplegable para seleccionar el tipo de identidad. En **[!UICONTROL Valor de identidad]**, proporcione el valor de identidad principal para el registro.

![Imagen que muestra un campo de identidad añadido manualmente](../images/ui/record-delete/identity-added.png)

Para añadir más identidades, seleccione el icono de signo más (![Imagen del icono de signo más](../images/ui/record-delete/plus-icon.png)) junto a una de las filas o seleccione **[!UICONTROL Añadir identidad]**.

![Imagen que muestra cómo agregar más identidades a la solicitud](../images/ui/record-delete/more-identities.png)

## Enviar la solicitud (#submit)

Una vez que haya terminado de agregar identidades a la solicitud, en **[!UICONTROL Solicitar configuración]**, proporcione un nombre y una descripción opcional para la solicitud antes de seleccionar **[!UICONTROL Enviar]**.

![Imagen que muestra el [!UICONTROL Enviar] botón seleccionado](../images/ui/record-delete/submit.png)

Se le pedirá que confirme la lista de identidades cuyos datos desee eliminar. Seleccionar **[!UICONTROL Enviar]** para confirmar la selección.

![Imagen que muestra el cuadro de diálogo de confirmación](../images/ui/record-delete/confirm-request.png)

Una vez enviada la solicitud, se crea una orden de trabajo y aparece en la [!UICONTROL Consumidor] de la pestaña [!UICONTROL Higiene de datos] workspace. Desde aquí puede supervisar el estado de la orden de trabajo a medida que procesa la solicitud.

>[!NOTE]
>
>Consulte la sección de información general sobre [plazos y transparencia](../home.md#record-delete-transparency) para obtener más información sobre cómo se procesan las eliminaciones de registros una vez ejecutadas.

## Pasos siguientes

Este documento explica cómo eliminar registros en la interfaz de usuario de Experience Platform. Para obtener información sobre cómo realizar otras tareas de higiene de datos en la interfaz de usuario, consulte la [información general sobre higiene de datos](./overview.md).

Para obtener información sobre cómo eliminar registros mediante la API de higiene de datos, consulte la [guía de extremo de pedido de trabajo](../api/workorder.md).
