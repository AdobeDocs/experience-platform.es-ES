---
keywords: Experience Platform;perfil;perfil de cliente en tiempo real;perfil unificado;perfil unificado;unificado;perfil;rtcp;habilitar perfil;Activar perfil;esquema de unión;PERFIL DE UNIÓN;perfil de unión
title: Guía de IU de Union Schema
topic-legacy: guide
type: Documentation
description: En la interfaz de usuario (IU) de Adobe Experience Platform, puede ver fácilmente cualquier esquema de unión de su organización y previsualizar los campos, las identidades, las relaciones y los esquemas de contribución de una clase específica. Esta guía proporciona información detallada sobre cómo ver y explorar esquemas de unión mediante la interfaz de usuario de Platform.
exl-id: 52af0d77-e37d-4ed8-9dee-71a50b337b4e
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1028'
ht-degree: 0%

---

# [!UICONTROL Union schema] Guía de la interfaz de usuario

En la interfaz de usuario (IU) de Adobe Experience Platform, puede ver fácilmente cualquier esquema de unión de su organización y previsualizar los campos, las identidades, las relaciones y los esquemas de contribución de una clase específica. Esta guía proporciona información detallada sobre cómo ver y explorar esquemas de unión mediante la interfaz de usuario de Platform.

## Primeros pasos

Esta guía de interfaz de usuario requiere conocer los distintos servicios [!DNL Experience Platform] que se utilizan para administrar los datos del perfil del cliente en tiempo real. Antes de leer esta guía o de trabajar en la interfaz de usuario, revise la documentación de los siguientes servicios:

* [[!DNL Real-time Customer Profile]](../home.md): Proporciona un perfil de cliente unificado y en tiempo real basado en datos agregados de varias fuentes.
* [[!DNL Identity Service]](../../identity-service/home.md): Habilita  [!DNL Real-time Customer Profile] mediante el puente de identidades de fuentes de datos dispares a medida que se incorporan en  [!DNL Platform].
* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): El marco estandarizado mediante el cual se  [!DNL Platform] organizan los datos de experiencia del cliente.

## Explicación de los esquemas de unión

El perfil del cliente en tiempo real le permite crear perfiles robustos y centralizados que contengan atributos del cliente y eventos con marca de hora, y que cada cliente interactúe entre sí en sistemas integrados con Adobe Experience Platform. El formato y la estructura de estos datos los proporcionan los esquemas del Modelo de datos de experiencia (XDM), cada esquema se basa en una clase XDM y contiene campos compatibles con esa clase.

Se pueden crear esquemas para varios casos de uso, que hagan referencia a la misma clase pero que contengan campos específicos de su uso. Cuando un esquema está habilitado para Perfil, pasa a formar parte de un esquema de unión. En otras palabras, los esquemas de unión están compuestos por varios esquemas que comparten la misma clase y que se han habilitado para Perfil. El esquema de unión permite ver una amalgamación de todos los campos contenidos en esquemas que comparten la misma clase. El perfil del cliente en tiempo real utiliza el esquema de unión para crear una vista holística de cada cliente individual.

El trabajo con esquemas de unión requiere una comprensión profunda de los esquemas XDM. Para obtener más información, comience por leer los [conceptos básicos de la composición del esquema](../../xdm/schema/composition.md).

## Ver esquemas de unión

Para ir a los esquemas de unión dentro de la interfaz de usuario de Platform, seleccione **[!UICONTROL Profiles]** en el panel de navegación izquierdo y, a continuación, seleccione la pestaña **[!UICONTROL Union Schema]** . La pestaña [!UICONTROL Union Schema] se abre para mostrar el esquema de unión de la clase seleccionada actualmente.

![](../images/union-schema/union-schema-landing.png)

## Seleccionar una clase

Para mostrar el esquema de unión de una clase XDM específica, seleccione la clase en la lista desplegable **[!UICONTROL Class]**. Debido al hecho de que no todas las clases tienen esquemas de unión, solo las clases con esquemas de unión (es decir, clases con esquemas que se han habilitado para Perfil) están disponibles en la lista desplegable.

Una vez seleccionada una clase, el esquema que se muestra se actualiza para reflejar el esquema de unión de la clase seleccionada. Por ejemplo, puede seleccionar **[!UICONTROL XDM Individual Profile]** para ver el esquema de unión de esa clase.

![](../images/union-schema/union-schema-class.png)

## Explorar esquemas de unión

Puede explorar el esquema de unión desplazándose hacia arriba y hacia abajo para ver la estructura completa del esquema y seleccionando un corchete angular derecho (`>`) para expandir los campos anidados.

![](../images/union-schema/union-schema-explore.png)

Seleccione cualquier campo para ver sus detalles, como nombre para mostrar, tipo de datos, descripción, ruta, fecha creada y fecha de la última modificación. También puede ver una lista de esquemas de contribución que contengan el campo seleccionado.

![](../images/union-schema/union-schema-explore-field.png)

Al seleccionar el nombre de un esquema de contribución, se muestran los nombres de los conjuntos de datos relacionados con ese esquema que están introduciendo datos en el campo seleccionado. Cada nombre de conjunto de datos aparece como un vínculo. Al seleccionar un nombre de conjunto de datos, se abre la pestaña actividad de ese conjunto de datos en una nueva ventana.

Para obtener más información sobre conjuntos de datos, incluida la visualización de la actividad del conjunto de datos y la vista previa de los datos del conjunto de datos en la interfaz de usuario, visite la [guía de la interfaz de usuario de conjuntos de datos](../../catalog/datasets/user-guide.md).

![](../images/union-schema/union-schema-field-datasets.png)

## Ver esquemas de contribución

También puede ver qué esquemas específicos contribuyen al esquema de unión seleccionando **[!UICONTROL All contributing schemas]** para expandir la lista de esquemas. Según la clase que haya seleccionado y el número de esquemas que su organización haya creado en Platform, podría ser una lista corta que contenga un esquema único o una lista larga que contenga muchos esquemas.

![](../images/union-schema/union-schema-contributing-schemas.png)

Al seleccionar el nombre de un esquema específico, se resaltan los campos del esquema de unión que forman parte del esquema seleccionado. Una vez seleccionado un esquema, el esquema de unión aparece atenuado con barras negras que indican los campos que forman parte del esquema de contribución.

![](../images/union-schema/union-schema-select-schema.png)

## Ver identidades

A través de la interfaz de usuario puede ver una lista de identidades incluidas en el esquema de unión seleccionando **[!UICONTROL Identities]** para expandir la lista.

![](../images/union-schema/union-schema-identities.png)

La selección de una identidad individual en la lista hace que el esquema mostrado se actualice automáticamente según sea necesario para mostrar el campo de identidad. Esto podría incluir la expansión de varios campos si el campo de identidad está anidado.

El campo de identidad se resalta dentro del esquema de unión y los detalles de la identidad se muestran en el lado derecho de la pantalla. Los detalles incluyen una lista de esquemas de contribución que contienen el campo de identidad y puede explorar en profundidad para encontrar vínculos a los conjuntos de datos relacionados con ese esquema que están incorporando datos en el campo de identidad seleccionado.

![](../images/union-schema/union-schema-select-identity.png)

## Ver relaciones

La IU de esquema de unión también permite ver las relaciones que se han definido para esquemas en función de la clase de esquema seleccionada. La definición de una relación es una forma de conectar dos esquemas pertenecientes a diferentes clases para obtener perspectivas más complejas sobre los datos de los clientes.

Si se han establecido relaciones para la clase seleccionada, al seleccionar **[!UICONTROL Relationships]** se muestra una lista de campos utilizados para crear relaciones. No todos los esquemas utilizan o necesitan relaciones definidas, por lo que es común que la sección de relaciones no contenga campos.

Para obtener más información sobre las relaciones de esquema, incluido cómo definirlas mediante la interfaz de usuario, visite [este documento sobre las relaciones de esquema](../../xdm/tutorials/relationship-ui.md).

![](../images/union-schema/union-schema-relationships.png)

Si se selecciona un campo de relación en la lista, el esquema mostrado se actualiza según sea necesario para mostrar el campo de relación resaltado. Esto podría incluir la expansión de varios campos si el campo de relación está anidado.

![](../images/union-schema/union-schema-select-relationship.png)

## Pasos siguientes

Al leer esta guía, ahora sabe cómo ver y navegar por los esquemas de unión mediante la interfaz de usuario [!DNL Experience Platform]. Para obtener más información sobre los esquemas, incluido cómo se utilizan en toda la plataforma, comience leyendo la [información general del sistema XDM](../../xdm/home.md).
