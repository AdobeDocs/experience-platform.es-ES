---
title: Compatibilidad con el control de acceso basado en atributos para esquemas ad hoc
description: Una guía para restringir el acceso a los campos de datos en esquemas ad hoc generados mediante Adobe Experience Platform Query Service.
exl-id: d675e3de-ab62-4beb-9360-1f6090397a17
source-git-commit: c2832821ea6f9f630e480c6412ca07af788efd66
workflow-type: tm+mt
source-wordcount: '1013'
ht-degree: 2%

---

# Compatibilidad de control de acceso basado en atributos para esquemas ad hoc

Cualquier dato introducido en Adobe Experience Platform se encapsula mediante esquemas XDM (Experience Data Model) y puede estar sujeto a restricciones de uso definidas por su organización o por regulaciones legales.

Al ejecutar una consulta CTAS a través del servicio de consulta cuando no se especifica ningún esquema, se genera automáticamente un esquema ad hoc. A menudo es necesario restringir el uso de ciertos campos o conjuntos de datos de esquemas ad hoc para controlar el acceso a datos personales confidenciales y a información de identificación personal. Adobe Experience Platform facilita este control de acceso al permitirle etiquetar campos de esquema a través de la IU de Platform mediante la capacidad de control de acceso basado en atributos.

Las etiquetas se pueden aplicar en cualquier momento, lo que proporciona flexibilidad en la forma en que se decide administrar los datos. Sin embargo, se recomienda etiquetar los datos en cuanto se introduzcan en Platform o en cuanto los datos estén disponibles para su uso en Platform.

El etiquetado basado en esquemas es un componente importante del control de acceso basado en atributos para administrar mejor el acceso dado a usuarios o grupos de usuarios. Adobe Experience Platform permite restringir el acceso a cualquier campo de un esquema ad hoc mediante la creación y aplicación de etiquetas.

Este documento proporciona un tutorial para administrar el acceso a los datos confidenciales mediante la aplicación de etiquetas a campos de datos de esquemas ad hoc generados mediante el servicio de consulta.

## Introducción

Esta guía requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* Sistema [Experience Data Model (XDM)](../../xdm/home.md): El marco estandarizado mediante el cual Experience Platform organiza los datos de experiencia del cliente.
   * [[!DNL Schema Editor]](../../xdm/ui/overview.md): Aprenda a crear y administrar esquemas y otros recursos en la interfaz de usuario de Platform.
* [[!DNL Data Governance]](../../data-governance/home.md): descubra cómo [!DNL Data Governance] le permite administrar los datos de los clientes y garantizar el cumplimiento de las regulaciones, restricciones y políticas aplicables al uso de los datos.
* [Control de acceso basado en atributos](../../access-control/abac/overview.md): El control de acceso basado en atributos es una capacidad de Adobe Experience Platform que permite a los administradores controlar el acceso a objetos específicos o a funcionalidades basadas en atributos. Los atributos pueden ser metadatos añadidos a un objeto, como una etiqueta añadida a un campo de esquema ad hoc o normal. Un administrador define directivas de acceso que incluyen atributos para administrar permisos de acceso de usuarios.

## Creación de un esquema ad hoc

Una vez que se ha ejecutado la consulta y se han generado los resultados, se genera automáticamente un esquema ad hoc que se añade al inventario de esquemas.

Para agregar una etiqueta de datos, vaya a la pestaña de exploración del panel [!UICONTROL Esquemas] seleccionando [!UICONTROL Esquemas] en el carril izquierdo de la interfaz de usuario de Platform. Se muestra el inventario de esquemas.

>[!NOTE]
>
>Los esquemas ad hoc no se muestran de forma predeterminada en el inventario de esquemas.

## Descubra esquemas ad hoc en el inventario de esquemas de la IU de Platform {#discover-ad-hoc-schemas}

Para habilitar la visualización de esquemas ad hoc en la interfaz de usuario de Platform, seleccione el icono de filtro (![Un icono de filtro.](/help/images/icons/filter.png)) a la izquierda del campo de búsqueda y, a continuación, seleccione **[!UICONTROL Mostrar esquemas ad hoc] en el carril izquierdo que aparece.

![El carril izquierdo de las opciones de filtro del panel de esquemas tiene habilitada la opción &#39;Mostrar esquema ad hoc&#39;.](../images/data-governance/adhoc-schema-toggle.png)

Seleccione el nombre del esquema ad hoc creado recientemente en la lista disponible. Aparecerá una visualización de la estructura de esquema ad hoc.

![Diagrama de estructura de esquema ad hoc de ejemplo.](../images/data-governance/adhoc-schema-structure-diagram.png)

## Editar etiquetas de gobernanza

Para editar las etiquetas de datos de su esquema ad hoc, seleccione la pestaña [!UICONTROL Etiquetas]. El espacio de trabajo de etiquetas le permite aplicar, crear y editar etiquetas a los campos de esquema ad hoc y controlar los permisos de acceso a través de la interfaz de usuario. Todos los campos del esquema ad hoc se representan aquí.

## Editar etiquetas para el esquema o campo

Para editar las etiquetas de todo el esquema, seleccione el icono de lápiz (![Un icono de lápiz.](/help/images/icons/edit.png)) al lado del nombre del esquema en la ficha [!UICONTROL Etiquetas].

![Vista de etiquetas en el área de trabajo de esquemas con el icono de lápiz resaltado.](../images/data-governance/edit-entire-schema-labels.png)

Para aplicar una etiqueta a un campo existente, seleccione uno o más campos de la lista seguidos de [!UICONTROL Editar etiquetas de gobernanza] en la barra lateral derecha.

![La vista de etiquetas en el área de trabajo de esquemas con la opción &#39;Editar etiquetas de control&#39; resaltada en la barra lateral derecha.](../images/data-governance/edit-governance-labels.png)

## Ventana emergente Editar etiquetas

Aparece la ventana emergente [!UICONTROL Editar etiquetas]. Desde esta vista puede crear o editar etiquetas de gobernanza existentes a través de la IU de.

![La ventana emergente Editar etiquetas.](../images/data-governance/edit-labels-popover.png)

Consulte la documentación para obtener instrucciones sobre cómo [crear o editar etiquetas para el esquema o campo seleccionado](../../xdm/tutorials/labels.md#edit-the-labels-for-the-schema-or-field).

>[!NOTE]
>
>La creación de una etiqueta nueva o la edición de una etiqueta existente requieren permisos de administrador para su organización. Si no tiene privilegios de administrador, póngase en contacto con el administrador del sistema para organizar el acceso.

Las etiquetas también se pueden crear mediante el espacio de trabajo de permisos. Consulte la [guía sobre la creación de etiquetas en el área de trabajo de permisos](../../access-control/abac/ui/labels.md) para obtener instrucciones.

Una vez aplicado el nivel adecuado de control de acceso basado en atributos, el siguiente comportamiento del sistema se aplica a cualquier consulta ejecutada mediante el Servicio de consulta cuando un usuario intenta acceder a datos no accesibles:

1. Si se rechaza el acceso de un usuario a uno de los campos de un esquema, el usuario no podrá leer ni escribir en el campo restringido. Esto se aplica a los siguientes escenarios comunes:

   * Cuando un usuario intenta ejecutar una consulta con una sola columna restringida, el sistema genera un error que indica que la columna no existe.
   * Cuando un usuario intenta ejecutar una consulta con varias columnas que incluyen una columna restringida, el sistema solo devolverá los resultados de todas las columnas no restringidas.

1. Si un usuario solicita acceso a un campo calculado, debe tener acceso a todos los campos utilizados en la composición o el sistema denegará el acceso al campo calculado.

Si se establece una identidad o identidad principal en un esquema ad hoc, el sistema respeta automáticamente cualquier solicitud de higiene de datos asociada y limpia los datos de esos conjuntos de datos vinculados a la columna de identidad.

## Pasos siguientes

Después de leer este documento, tiene una mejor comprensión de cómo agregar etiquetas de uso de datos a esquemas ad hoc creados mediante consultas CTAS del servicio de consulta. Si aún no lo ha hecho, los siguientes documentos son útiles para comprender mejor el control de datos en el servicio de consultas:

* [Identidades de esquema ad hoc](./ad-hoc-schema-identities.md)
* [Gobernanza de datos](../../data-governance/home.md)
