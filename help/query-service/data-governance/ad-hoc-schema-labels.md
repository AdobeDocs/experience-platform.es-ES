---
title: Compatibilidad con el control de acceso basado en atributos para esquemas específicos
description: Una guía para restringir el acceso a los campos de datos en esquemas específicos generados a través del servicio de consulta de Adobe Experience Platform.
exl-id: d675e3de-ab62-4beb-9360-1f6090397a17
source-git-commit: 91f318596bf268aa93e8b2df9c13774aab76d13a
workflow-type: tm+mt
source-wordcount: '1040'
ht-degree: 1%

---

# Compatibilidad con el control de acceso basado en atributos para esquemas ad hoc

Los esquemas del Modelo de datos de experiencia (XDM) encapsulan cualquier dato que se introduzca en Adobe Experience Platform y pueden estar sujetos a restricciones de uso definidas por su organización o por las regulaciones legales.

Al ejecutar una consulta CTAS a través del servicio de consulta cuando no se especifica ningún esquema, se genera automáticamente un esquema ad hoc. A menudo es necesario restringir el uso de ciertos campos o conjuntos de datos de esquemas específicos para controlar el acceso a datos personales confidenciales e información personal identificable. Adobe Experience Platform facilita este control de acceso permitiéndole etiquetar campos de esquema a través de la interfaz de usuario de Platform mediante la capacidad de control de acceso basada en atributos.

Las etiquetas se pueden aplicar en cualquier momento, lo que proporciona flexibilidad en la forma en que elige administrar los datos. Sin embargo, es recomendable etiquetar los datos tan pronto como se incorporen a Platform o tan pronto como los datos estén disponibles para su uso en Platform.

El etiquetado basado en esquemas es un componente importante del control de acceso basado en atributos para administrar mejor el acceso dado a los usuarios o grupos de usuarios. Adobe Experience Platform permite restringir el acceso a cualquier campo de un esquema ad hoc mediante la creación y aplicación de etiquetas.

Este documento proporciona un tutorial para administrar el acceso a los datos confidenciales mediante la aplicación de etiquetas a los campos de datos de esquemas específicos generados mediante el servicio de consulta.

## Primeros pasos

Esta guía requiere conocer los siguientes componentes de Adobe Experience Platform:

* [Sistema del Modelo de datos de experiencia (XDM)](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html?lang=es): El marco estandarizado mediante el cual el Experience Platform organiza los datos de experiencia del cliente.
   * [[!DNL Schema Editor]](https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/overview.html): Obtenga información sobre cómo crear y administrar esquemas y otros recursos en la interfaz de usuario de Platform.
* [[!DNL Data Governance]](../../data-governance/home.md): Descubra cómo [!DNL Data Governance] le permite administrar los datos de los clientes y garantizar el cumplimiento de las regulaciones, restricciones y políticas aplicables al uso de los datos.
* [Control de acceso basado en atributos](../../access-control/abac/overview.md): El control de acceso basado en atributos es una función de Adobe Experience Platform que permite a los administradores controlar el acceso a objetos específicos o a funciones basadas en atributos. Los atributos pueden ser metadatos agregados a un objeto, como una etiqueta agregada a un campo de esquema específico o normal. Un administrador define políticas de acceso que incluyen atributos para administrar los permisos de acceso de los usuarios.

## Crear un esquema ad hoc

Una vez ejecutada la consulta y generados los resultados, se genera automáticamente un esquema ad hoc y se añade al inventario de esquemas.

Para añadir una etiqueta de datos, vaya a [!UICONTROL Esquemas] ficha examinar panel seleccionando [!UICONTROL Esquemas] en el carril izquierdo de la interfaz de usuario de Platform. Se muestra el inventario de esquema.

>[!NOTE]
>
>Los esquemas específicos no se muestran de forma predeterminada en el inventario de esquemas.

## Descubra esquemas ad hoc en el inventario de esquemas de la interfaz de usuario de Platform {#discover-ad-hoc-schemas}

Para habilitar la visualización de esquemas ad hoc en la interfaz de usuario de Platform, seleccione el icono de filtro (![Un icono de filtro.](../images/data-governance/filter.png)) a la izquierda del campo de búsqueda y, a continuación, seleccione **[!UICONTROL Mostrar esquemas específicos] en el carril izquierdo que aparece.

![Las opciones del filtro del panel Esquema están en el carril izquierdo con la opción &quot;Mostrar esquema ad hoc&quot; activada.](../images/data-governance/adhoc-schema-toggle.png)

Seleccione el nombre del esquema ad hoc creado recientemente en la lista disponible. Aparece una visualización de la estructura de esquema ad hoc .

![Diagrama de estructura de esquema ad hoc de ejemplo.](../images/data-governance/adhoc-schema-structure-diagram.png)

## Editar etiquetas de control

Para editar las etiquetas de datos del esquema ad hoc, seleccione la opción [!UICONTROL Etiquetas] pestaña . El espacio de trabajo de etiquetas le permite aplicar, crear y editar etiquetas en los campos de esquema específicos y controlar los permisos de acceso a través de la interfaz de usuario. Aquí se representan todos los campos del esquema ad hoc.

## Edición de etiquetas para el esquema o campo

Para editar las etiquetas de todo el esquema, seleccione el icono de lápiz (![Un icono de lápiz.](../images/data-governance/edit-icon.png)) al lado del nombre del esquema bajo el [!UICONTROL Etiquetas] pestaña .

![La vista de etiquetas en el espacio de trabajo de esquemas con el icono de lápiz resaltado.](../images/data-governance/edit-entire-schema-labels.png)

Para aplicar una etiqueta a un campo existente, seleccione uno o varios campos de la lista seguidos de [!UICONTROL Editar etiquetas de control] en la barra lateral derecha.

![La vista de etiquetas en el espacio de trabajo de esquemas con la opción Editar etiquetas de control resaltada en la barra lateral derecha.](../images/data-governance/edit-governance-labels.png)

## Editar la ventana emergente de etiquetas

La variable [!UICONTROL Editar etiquetas] se abre. Desde esta vista puede crear o editar etiquetas de control existentes a través de la interfaz de usuario.

![Se abre la ventana Editar etiquetas.](../images/data-governance/edit-labels-popover.png)

Consulte la documentación para obtener instrucciones sobre cómo [crear o editar etiquetas para el esquema o campo seleccionado](https://experienceleague.adobe.com/docs/experience-platform/xdm/tutorials/labels.html#edit-the-labels-for-the-schema-or-field).

>[!NOTE]
>
>La creación de una etiqueta nueva o la edición de una etiqueta existente requieren permisos de administrador para su organización. Si no tiene privilegios de administrador, póngase en contacto con el administrador del sistema para organizar el acceso.

Las etiquetas también se pueden crear mediante el espacio de trabajo de permisos. Consulte la [guía sobre la creación de etiquetas en el espacio de trabajo de permisos](../../access-control/abac/ui/labels.md) para obtener instrucciones.

Una vez que se ha aplicado el nivel adecuado de control de acceso basado en atributos, el siguiente comportamiento del sistema se aplica a cualquier consulta ejecutada mediante Query Service cuando un usuario intenta acceder a datos no accesibles:

1. Si se rechaza el acceso de un usuario a uno de los campos dentro de un esquema, el usuario no podrá leer ni escribir en el campo restringido. Esto se aplica a los siguientes escenarios comunes:

   * Cuando un usuario intenta ejecutar una consulta con solo una columna restringida, el sistema generará un error que indica que la columna no existe.
   * Cuando un usuario intenta ejecutar una consulta con varias columnas que incluyen una columna restringida, el sistema solo devolverá resultados para todas las columnas no restringidas.

1. Si un usuario solicita acceso a un campo calculado, el usuario debe tener acceso a todos los campos utilizados en la composición o el sistema denegará el acceso al campo calculado.

Si se establece una identidad o identidad principal en un esquema ad hoc, el sistema respeta automáticamente cualquier solicitud de higiene de datos asociada y limpia los datos de esos conjuntos de datos vinculados a la columna de identidad.

## Pasos siguientes

Después de leer este documento, tendrá una mejor comprensión de cómo agregar etiquetas de uso de datos a esquemas ad hoc creados a través de consultas CTAS del servicio de consulta. Si aún no lo ha hecho, los siguientes documentos son útiles para mejorar su comprensión del control de datos en el servicio de consulta:

* [Identidades de esquema ad hoc](./ad-hoc-schema-identities.md)
* [Administración de datos](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html?lang=es)
