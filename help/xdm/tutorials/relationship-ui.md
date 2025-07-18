---
keywords: Experience Platform;inicio;temas populares;ui;IU;XDM;sistema XDM;modelo de datos de experiencia;modelo de datos de experiencia;modelo de datos de experiencia;modelo de datos;modelo de datos;editor de esquemas;editor de esquemas;esquema;esquemas;esquemas;crear;relación;referencia;referencia;
solution: Experience Platform
title: Definición de una relación entre dos esquemas con el Editor de esquemas
description: Este documento proporciona un tutorial para definir una relación entre dos esquemas mediante el Editor de esquemas en la interfaz de usuario de Experience Platform.
type: Tutorial
exl-id: feed776b-bc8d-459b-9700-e5c9520788c0
source-git-commit: 5f9fdc9eff4d8bba049c03058d24e80e9b89e953
workflow-type: tm+mt
source-wordcount: '1376'
ht-degree: 9%

---

# Defina una relación de uno a uno entre dos esquemas utilizando [!DNL Schema Editor] {#relationship-ui}

>[!CONTEXTUALHELP]
>id="platform_schemas_relationships"
>title="Relaciones de esquemas"
>abstract="Los esquemas pertenecientes a diferentes clases se pueden vincular contextualmente a través de campos de relación, lo que permite crear reglas de segmentación más complejas. Consulte la documentación para obtener más información sobre las relaciones de esquemas."

>[!CONTEXTUALHELP]
>id="platform_xdm_1to1_reference_schema"
>title="Esquema de referencia"
>abstract="Seleccione el esquema con el que desea establecer una relación. Este esquema puede ser una clase diferente del esquema actual. Consulte la documentación para obtener más información sobre las relaciones de esquemas."

>[!CONTEXTUALHELP]
>id="platform_xdm_1to1_identity_namespace"
>title="Espacio de nombres de identidad de referencia"
>abstract="El área de nombres (tipo) del campo de identidad principal del esquema de referencia. El esquema de referencia debe tener un campo de identidad principal establecido para participar en una relación. Consulte la documentación para obtener más información sobre las relaciones de esquemas."

La capacidad de comprender las relaciones entre sus clientes y sus interacciones con su marca en varios canales es una parte importante de Adobe Experience Platform. La definición de estas relaciones dentro de la estructura de los esquemas [!DNL Experience Data Model] (XDM) le permite obtener información compleja sobre los datos del cliente.

Aunque las relaciones de esquema se pueden inferir mediante el uso del esquema de unión y [!DNL Real-Time Customer Profile], esto sólo se aplica a los esquemas que comparten la misma clase. Para establecer una relación entre dos esquemas que pertenecen a clases diferentes, se debe agregar un campo de relación dedicado a un esquema de origen, que hace referencia a la identidad del otro esquema relacionado.

>[!NOTE]
>
>Si los esquemas de origen y destino pertenecen a la misma clase, se debe usar un campo de relación dedicado **no**. En este caso, utilice la interfaz de usuario del esquema de unión para ver la relación. Encontrará instrucciones sobre cómo hacerlo en la sección [ver relaciones](../../profile/ui/union-schema.md#view-relationships) de la guía de IU del esquema de unión.

Este documento proporciona un tutorial para definir una relación entre dos esquemas mediante el Editor de esquemas en la interfaz de usuario [!DNL Experience Platform]. Para ver los pasos de definición de relaciones de esquema mediante la API, vea el tutorial sobre [definición de una relación mediante la API de Registro de esquemas](relationship-api.md).

>[!NOTE]
>
>Para ver los pasos sobre cómo crear una relación varios a uno en Adobe Real-Time Customer Data Platform B2B edition, consulte la guía sobre [creación de relaciones B2B](./relationship-b2b.md).

## Introducción

Este tutorial requiere una comprensión práctica de [!DNL XDM System] y del Editor de esquemas en la interfaz de usuario de [!DNL Experience Platform]. Antes de comenzar este tutorial, revise la siguiente documentación:

* [Sistema XDM en Experience Platform](../home.md): Información general sobre XDM y su implementación en [!DNL Experience Platform].
* [Conceptos básicos de la composición de esquemas](../schema/composition.md): introducción a los componentes básicos de los esquemas XDM.
* [Crear un esquema con [!DNL Schema Editor]](create-schema-ui.md): Un tutorial que cubre los conceptos básicos para trabajar con [!DNL Schema Editor].

## Definir un esquema de origen y de referencia

Se espera que ya haya creado los dos esquemas que se definirán en la relación. Para fines de demostración, este tutorial crea una relación entre los miembros del programa de fidelidad de una organización (definido en un esquema &quot;[!DNL Loyalty Members]&quot;) y su hotel favorito (definido en un esquema &quot;[!DNL Hotels]&quot;).

>[!IMPORTANT]
>
>Para establecer una relación, ambos esquemas deben tener identidades principales definidas y habilitarse para [!DNL Real-Time Customer Profile]. Consulte la sección sobre [habilitar un esquema para utilizarlo en el perfil](./create-schema-ui.md#profile) en el tutorial de creación de esquemas si necesita instrucciones sobre cómo configurar los esquemas en consecuencia.

Las relaciones de esquema están representadas por un campo dedicado dentro de un **esquema de origen** que apunta a otro campo dentro de un **esquema de referencia**. En los pasos siguientes, &quot;[!DNL Loyalty Members]&quot; será el esquema de origen, mientras que &quot;[!DNL Hotels]&quot; actuará como esquema de referencia.

Las secciones siguientes describen la estructura de cada esquema utilizado en este tutorial antes de definir una relación.

### Esquema [!DNL Loyalty Members]

El esquema de origen &quot;[!DNL Loyalty Members]&quot; se basa en la clase [!DNL XDM Individual Profile], que contiene campos que describen a los miembros de un programa de fidelidad. Uno de estos campos, `personalEmail.addess`, sirve como identidad principal para el esquema en el área de nombres [!UICONTROL Email]. Como se ve en **[!UICONTROL Propiedades del esquema]**, este esquema se ha habilitado para su uso en [!DNL Real-Time Customer Profile].

![](../images/tutorials/relationship/loyalty-members.png)

### Esquema [!DNL Hotels]

El esquema de referencia &quot;[!DNL Hotels]&quot; se basa en una clase &quot;[!DNL Hotels]&quot; personalizada y contiene campos que describen un hotel. Para participar en una relación, el esquema de referencia también debe tener una identidad principal definida y habilitada para [!UICONTROL Perfil]. En este caso, `_tenantId.hotelId`actúa como identidad principal para el esquema, usando un área de nombres de identidad &quot;[!DNL Hotel ID]&quot; personalizada.

![Habilitar para el perfil](../images/tutorials/relationship/hotels.png)

>[!NOTE]
>
>Para aprender a crear áreas de nombres de identidad personalizadas, consulte la [documentación del servicio de identidad](../../identity-service/features/namespaces.md#manage-namespaces).

## Crear un grupo de campos de relación

>[!NOTE]
>
>Este paso solo es necesario si el esquema de origen no tiene un campo de tipo cadena dedicado para utilizarlo como puntero a la identidad principal del esquema de referencia. Si este campo ya está definido en su esquema de origen, vaya al siguiente paso de [definición de un campo de relación](#relationship-field).

Para definir una relación entre dos esquemas, el esquema de origen debe tener un campo dedicado que indique la identidad principal del esquema de referencia. Puede agregar este campo al esquema de origen creando un nuevo grupo de campos de esquema o ampliando uno existente.

En el caso del esquema [!DNL Loyalty Members], se agregará un nuevo campo `preferredHotel` para indicar el hotel preferido del miembro socio socio para las visitas a la compañía. Comience por seleccionar el icono de signo más (**+**) junto al nombre del esquema de origen.

![](../images/tutorials/relationship/loyalty-add-field.png)

Aparece un nuevo marcador de posición de campo en el lienzo. En **[!UICONTROL Propiedades del campo]**, proporcione un nombre de campo y un nombre para mostrar para el campo y establezca su tipo en &quot;[!UICONTROL Cadena]&quot;. En **[!UICONTROL Asignar a]**, seleccione un grupo de campos existente para ampliarlo, o escriba un nombre único para crear un nuevo grupo de campos. En este caso, se crea un nuevo grupo de campos [!DNL Preferred Hotel].

![](../images/tutorials/relationship/relationship-field-details.png)

Cuando termine, seleccione **[!UICONTROL Aplicar]**.

![](../images/tutorials/relationship/relationship-field-apply.png)

El campo `preferredHotel` actualizado aparece en el lienzo, ubicado bajo un objeto `_tenantId` debido a que es un campo personalizado. Seleccione **[!UICONTROL Guardar]** para finalizar los cambios en el esquema.

![](../images/tutorials/relationship/relationship-field-save.png)

## Definición de un campo de relación para el esquema de origen {#relationship-field}

Una vez que el esquema de origen tenga definido un campo de referencia dedicado, puede designarlo como campo de relación.

>[!NOTE]
>
>Las relaciones solo se pueden admitir en campos de cadena o de matriz de cadenas.

Seleccione el campo `preferredHotel` en el lienzo y, a continuación, seleccione **[!UICONTROL Agregar relación]** en la barra lateral **[!UICONTROL Propiedades del campo]**.

![Editor de esquemas con la relación Agregar resaltada en la barra lateral de propiedades del campo.](../images/tutorials/relationship/add-relationship.png)

Aparecerá el cuadro de diálogo [!UICONTROL Agregar relación]. Desde este cuadro de diálogo, puede definir los parámetros necesarios para configurar un campo de relación. Para los usuarios de Real-Time CDP B2C, **solamente** puede establecer una relación uno a uno entre el esquema de origen y el de referencia.

>[!NOTE]
>
>Si tiene acceso a Real-Time CDP B2B edition, puede utilizar los controles del carril derecho del lienzo para definir un campo de relación, así como para crear una relación de varios a uno mediante el [mismo cuadro de diálogo](./relationship-b2b.md#relationship-field).

![Cuadro de diálogo Agregar relación.](../images/tutorials/relationship/add-relationship-dialog.png)

Utilice el menú desplegable de **[!UICONTROL Esquema de referencia]** y seleccione el esquema de referencia para la relación (&quot;[!DNL Hotels]&quot; en este ejemplo).

>[!NOTE]
>
>En el menú desplegable esquema de referencia solo se incluyen los esquemas que contienen una identidad principal. Esta protección evita que cree accidentalmente una relación con un esquema que aún no está configurado correctamente.

El área de nombres de identidad del esquema de referencia (en este caso, &quot;[!DNL Hotel ID]&quot;) se rellena automáticamente en **[!UICONTROL Área de nombres de identidad de referencia]**. Seleccione **[!UICONTROL Aplicar]** cuando haya terminado.

![Cuadro de diálogo Agregar relación con los parámetros de relación configurados y Aplicar resaltados.](../images/tutorials/relationship/apply-relationship.png)

El campo `preferredHotel` ahora se resalta como una relación en el lienzo, mostrando el nombre del esquema de referencia. Seleccione **[!UICONTROL Guardar]** para guardar los cambios y completar el flujo de trabajo.

![El editor de esquemas con las referencias de relación y Guardar resaltados.](../images/tutorials/relationship/relationship-save.png)

### Editar un campo de relación existente {#edit-relationship}

Para cambiar el esquema de referencia, seleccione un campo con una relación existente y, a continuación, seleccione **[!UICONTROL Editar relación]** en la barra lateral **[!UICONTROL Propiedades del campo]**.

![Editor de esquemas con la relación de edición resaltada.](../images/tutorials/relationship/edit-relationship.png)

Aparecerá el cuadro de diálogo [!UICONTROL Editar relación]. Desde aquí, puede seguir el proceso descrito en [definición de un campo de relación](#relationship-field) o eliminar la relación. Seleccione **[!UICONTROL Eliminar relación]** para eliminar la relación con el esquema de referencia.

![Cuadro de diálogo Editar relación.](../images/tutorials/relationship/edit-relationship-dialog.png)

## Filtrar y buscar relaciones {#filter-and-search}

Puede filtrar y buscar relaciones específicas dentro de sus esquemas desde la pestaña [!UICONTROL Relaciones] del área de trabajo [!UICONTROL Esquemas]. Puede utilizar esta vista para localizar y administrar rápidamente sus relaciones. Lea el documento sobre [explorar recursos de esquema](../ui/explore.md#lookup) para obtener instrucciones detalladas sobre las opciones de filtrado.

![La ficha Relaciones en el área de trabajo Esquemas.](../images/tutorials/relationship-b2b/relationship-tab.png)

## Pasos siguientes

Al seguir este tutorial, ha creado correctamente una relación uno a uno entre dos esquemas con el [!DNL Schema Editor]. Para ver los pasos sobre cómo definir relaciones mediante la API, consulte el tutorial de [definición de una relación mediante la API de Registro de esquemas](relationship-api.md).
